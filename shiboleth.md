# LIAF SSO - Shibboleth SP (Recommended for those who are familiar with Linux)

The LIAF SSO document describes how to implement Single Sign-On (SSO) for their Learning Management System (LMS). It likely provides instructions on configuring and integrating SSO, enabling users to access the LMS with a single set of login credentials across various systems. This approach improves user convenience and security by minimizing the need to remember multiple passwords and simplifying the authentication process.

***Testing environment*** 

* OS version : Ubuntu 22.04
* php version : 
* Moodle Version : 4.3
* SSL/ HTTPS Certificates issued ( using Letsencrypt )
* sudo access to the server. All following commands have to be entered as the root user. Best way to do it is, by login in as root with ``` sudo su ```

Shibboleth SP installation

Install needed packages:

 apt install libapache2-mod-shib ntp --no-install-recommends 

***Moodle Apache Config***

'''http''' config: {{{ /etc/apache2/sites-enabled/mdl.conf }}}


{{{
<VirtualHost *:80>

	ServerName mdl.Your-Domain
	ServerAdmin you@yourwebsite.com
	DocumentRoot /var/www/html/moodle #Location of Moodle installation

	ErrorLog ${APACHE_LOG_DIR}/mdl-error.log
	CustomLog ${APACHE_LOG_DIR}/mdl-access.log combined

</VirtualHost>
}}}

***Install Letsencrypt and enable HTTPS:***

{{{
* apt install python3-certbot-apache
* certbot --apache -d idp.YOUR-DOMAIN
}}}

***Shibboleth SP Installation***

Install needed packages:

{{{ apt install libapache2-mod-shib ntp --no-install-recommends }}}

***Shibboleth SP Configuration***

Web application need to be connected to LIAF, therefore, download Federation Metadata Signing Certificate:

{{{
    cd /etc/shibboleth/
    wget https://fr.ac.lk/signedmetadata/metadata-signer -O federation-cert.pem
}}}

Edit shibboleth2.xml opportunely: {{{ vim /etc/shibboleth/shibboleth2.xml }}}

{{{
#!xml
. . .

    <!-- The ApplicationDefaults element is where most of Shibboleth's SAML bits are defined. -->
    <ApplicationDefaults entityID="https://YOUR_DNS/shibboleth"
        REMOTE_USER="eppn subject-id pairwise-id persistent-id"
        cipherSuites="DEFAULT:!EXP:!LOW:!aNULL:!eNULL:!DES:!IDEA:!SEED:!RC4:!3DES:!kRSA:!SSLv2:!SSLv3:!TLSv1:!TLSv1.1">

. . .

        <Sessions lifetime="28800" timeout="3600" relayState="ss:mem"
                  checkAddress="false" handlerSSL="true" cookieProps="https">

. . .

            <SSO discoveryProtocol="SAMLDS" discoveryURL="https://fds.ac.lk">
              SAML2
            </SSO>

. . .

        <Errors supportContact="you@you-domain"
             helpLocation="/about-this-service.html"
             styleSheet="/shibboleth-sp/main.css"/>

. . .

	<MetadataProvider type="XML" url="https://fr.ac.lk/signedmetadata/metadata.xml" legacyOrgName="true" backingFilePath="test-metadata.xml" reloadInterval="600">

      		<MetadataFilter type="Signature" certificate="federation-cert.pem" verifyBackup="false"/>

      		<MetadataFilter type="RequireValidUntil" maxValidityInterval="864000" />
        </MetadataProvider>

. . .

        <!-- Simple file-based resolvers for separate signing/encryption keys. -->
        <CredentialResolver type="File" use="signing"
            key="mdl-signing-key.pem" certificate="mdl-signing-cert.pem"/>
        <CredentialResolver type="File" use="encryption"
            key="mdl-encrypt-key.pem" certificate="mdl-encrypt-cert.pem"/>

	<ApplicationOverride id="mdl" entityID="https://mdl.Your-Domain/shibboleth">
		<CredentialResolver type="File" use="signing"
            		key="mdl-signing-key.pem" certificate="mdl-signing-cert.pem"/>
        	<CredentialResolver type="File" use="encryption"
            		key="mdl-encrypt-key.pem" certificate="mdl-encrypt-cert.pem"/>
	</ApplicationOverride>
    </ApplicationDefaults>

    <!-- Policies that determine how to process and authenticate runtime messages. -->
    <SecurityPolicyProvider type="XML" validate="true" path="security-policy.xml"/>

}}}

Now lets create those certificate pairs.


* {{{ /usr/sbin/shib-keygen -n mdl-signing -e https://YOUR-DNS/shibboleth }}}
* {{{ /usr/sbin/shib-keygen -n mdl-encrypt -e https://YOUR-DNS/shibboleth }}}


Activate required attributes from  the {{{ /etc/shibboleth/attribute-map.xml }}} For the example, lets uncomment all, but make sure you didnt messed with the file.  


Then check the shibboleth configuration for errors by, 

{{{ shibd -t /etc/shibboleth/shibboleth2.xml }}}


Edit Moodle virtual host as follows:

config file: {{{ /etc/apache2/sites-enabled/mdl-le-ssl.conf }}}

{{{
<IfModule mod_ssl.c>
<VirtualHost *:443>
	
	ServerName mdl.Your-Domain
	ServerAdmin you@yourwebsite.com
	DocumentRoot /var/www/mdl #Location of Moodle installation

	ErrorLog ${APACHE_LOG_DIR}/mdl-error.log
	CustomLog ${APACHE_LOG_DIR}/mdl-access.log combined

        #SSL Certificates issued by letsencrypt
        SSLCertificateFile /etc/letsencrypt/live/mdl.Your-Domain/fullchain.pem
        SSLCertificateKeyFile /etc/letsencrypt/live/mdl.Your-Domain/privkey.pem
        Include /etc/letsencrypt/options-ssl-apache.conf

        <Location />
             ShibRequestSetting applicationId mdl  
        </Location>
        #Defining shibboleth application override

        <Directory /var/www/mdl/auth/shibboleth/index.php> 
             AuthType shibboleth
             ShibRequestSetting applicationId mdl
             ShibRequireSession On
             require valid-user
        </Directory>
        #Double Check Moodle installation path

</VirtualHost>
</IfModule>
}}}

Next, enable apache shibboleth module and restart apache.

{{{
#!bash
    a2enmod shib
    systemctl reload apache2.service
}}}

== Register both services with LIAF ==

We have now set up shibboleth SP for the entity.It has to be registered with LIAF before using the Federation discovery Service to point different IDP's.

Download the  metadata from both applications by going to the following URL's. 

* {{{ https://mdl.YOUR-DOMAIN/Shibboleth.sso/Metadata }}}

Now register them with LIAF separately. 

***Enabling Moodle Plugin***

As Moodle admin, go to the '''Site administration''' >>> '''Plugins''' >>> '''Authentication''' and click on the '''Shibboleth''' enable '''eye'''. Next go to its settings.


Fill in the fields of the form. 

The fields 'Username', 'First name', 'Surname', etc. should contain the name of the environment variables of the Shibboleth attributes that you want to map onto the corresponding Moodle variable. Especially the 'Username' field is of great importance because this attribute is used for the Moodle authentication of Shibboleth users.

Username: eppn

Moodle WAYF service: No

Shibboleth Service Provider logout handler URL: /Shibboleth.sso/Logout

Data mapping (First name): givenName

Data mapping (Surname): surname

Data mapping (Email address): mail

Update local (Email address): On Creation

Lock value (Email address): Locked


Click Save.


* Adjust  attribute-map .xml  as
{{{
    <Attribute name="urn:mace:dir:attribute-def:sn" id="sn"/>
    <Attribute name="urn:oid:2.5.4.4" id="sn"/>
    <Attribute name="urn:mace:dir:attribute-def:givenName" id="givenName"/>
    <Attribute name="urn:oid:2.5.4.42" id="givenName"/>
    <Attribute name="urn:mace:dir:attribute-def:mail" id="mail"/>
    <Attribute name="urn:oid:0.9.2342.19200300.100.1.3" id="mail"/>
    <Attribute name="urn:mace:dir:attribute-def:email" id="email"/>
    <Attribute name="urn:oid:1.3.6.1.4.1.5923.1.1.1.10" id="email"/>
}}}

* Adjust attribute-policy.xml as 

{{{

        <AttributeRule attributeID="sn">
            <PermitValueRule xsi:type="ANY" />
        </AttributeRule>

        <AttributeRule attributeID="givenName">
            <PermitValueRule xsi:type="ANY" />
        </AttributeRule>

        <AttributeRule attributeID="mail">
            <PermitValueRule xsi:type="ANY" />
        </AttributeRule>

        <AttributeRule attributeID="email">
            <PermitValueRule xsi:type="ANY" />
        </AttributeRule>
}}}

After, restart shibd and apache2

Now using a private browser, try to log in to both systems using your IDP test user.
