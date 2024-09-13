# LIAF SSO - Shibboleth SP (Recommended for those who are familiar with Linux)

LIAF SSO facilitates Moodle admins to get rid of need of creating student/staff user account manually. The people can access the Moodle site either by their [eduID](https://eduid.lk/) or their campus credentials.

The document describes the way to implement the [LIAF Single Sign-On (SSO)](https://fds.ac.lk/?entityID=https%3A%2F%2Fmdqtest.learn.ac.lk%2Fmoodle%2Fauth%2Fsaml2%2Fsp%2Fmetadata.php&return=https%3A%2F%2Fmdqtest.learn.ac.lk%2Fmoodle%2Fauth%2Fsaml2%2Fsp%2Fmodule.php%2Fsaml%2Fsp%2FdiscoResponse%3FAuthID%3D_d74a632720fb9ac65e78981fcf2cb59df22ff2e252%253Ahttps%253A%252F%252Fmdqtest.learn.ac.lk%252Fmoodle%252Fauth%252Fsaml2%252Fsp%252Fmodule.php%252Fsaml%252Fsp%252Flogin%252Fmdqtest.learn.ac.lk%253FReturnTo%253Dhttps%25253A%25252F%25252Fmdqtest.learn.ac.lk%25252Fmoodle%25252Fauth%25252Fsaml2%25252Flogin.php%25253Fwants%252526idp%25253Dc20fdc0a583f7d847e917aa67c86089a%252526passive%25253Doff&returnIDParam=idpentityid) for Moodle.

<!-- The LIAF SSO document describes how to implement Single Sign-On (SSO) for their Learning Management System (LMS). It likely provides instructions on configuring and integrating SSO, enabling users to access the LMS with a single set of login credentials across various systems. This approach improves user convenience and security by minimizing the need to remember multiple passwords and simplifying the authentication process.-->

***Tested and verified on*** 

* OS version : Ubuntu 22.04/24.04
* php version : 8.1.2
* Moodle Version : 4.3

***Requirement***

* SSL/HTTPS enabled for your sp FQDN (In this guide letsencrypt is used to secure FQDN)
* sudo access to the server. All following commands have to be entered as the root user. Best way to do it is, by login in as root with ``` sudo su ```
## if you are going to use Letsencrypt to secure your FQDN

Install Letsencrypt and enable HTTPS:
```
apt install python3-certbot-apache
certbot --apache -d YOUR_FQDN
```
(or you can use a commecrcial SSL certificate)

## Shibboleth SP installation

Install needed packages:

```apt install libapache2-mod-shib ntp --no-install-recommends ```

### Shibboleth SP Configuration

Web application need to be connected to LIAF, therefore, download Federation Metadata Signing Certificate:

```
    cd /etc/shibboleth/
    wget https://fr.ac.lk/signedmetadata/metadata-signer -O federation-cert.pem
```

Edit shibboleth2.xml opportunely: 

``` vim /etc/shibboleth/shibboleth2.xml ```
```
...
    <!-- The ApplicationDefaults element is where most of Shibboleth's SAML bits are defined. -->
    <ApplicationDefaults entityID="https://YOUR_DNS/shibboleth"
        REMOTE_USER="eppn subject-id pairwise-id persistent-id"
        cipherSuites="DEFAULT:!EXP:!LOW:!aNULL:!eNULL:!DES:!IDEA:!SEED:!RC4:!3DES:!kRSA:!SSLv2:!SSLv3:!TLSv1:!TLSv1.1">
...

            <SSO discoveryProtocol="SAMLDS" discoveryURL="https://fds.ac.lk">
              SAML2
            </SSO>
...

        <Errors supportContact="tac@learn.ac.lk"
             helpLocation="/about-this-service.html"
             styleSheet="/shibboleth-sp/main.css"/>
...

	<MetadataProvider type="XML" url="https://fr.ac.lk/signedmetadata/metadata.xml" legacyOrgName="true" backingFilePath="test-metadata.xml" reloadInterval="600">

      		<MetadataFilter type="Signature" certificate="federation-cert.pem" verifyBackup="false"/>

      		<MetadataFilter type="RequireValidUntil" maxValidityInterval="864000" />
        </MetadataProvider>
...
        <!-- Simple file-based resolvers for separate signing/encryption keys. -->
        <CredentialResolver type="File" use="signing"
            key="mdl-signing-key.pem" certificate="mdl-signing-cert.pem"/>
        <CredentialResolver type="File" use="encryption"
            key="mdl-encrypt-key.pem" certificate="mdl-encrypt-cert.pem"/>
...
```

Now lets create those certificate pairs.


* ``` /usr/sbin/shib-keygen -n mdl-signing -e https://YOUR-DNS/shibboleth ```
* ``` /usr/sbin/shib-keygen -n mdl-encrypt -e https://YOUR-DNS/shibboleth ```

Then check the shibboleth configuration for errors by, 

```
shibd -t /etc/shibboleth/shibboleth2.xml 
systemctl restart apache2
systemctl restart shibd
```

Edit Moodle virtual host as follows:

config file: ``` /etc/apache2/sites-enabled/mdl-le-ssl.conf ```

```
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

        <Location /moodle>
         	#ShibRequestSetting applicationId mdl
        </Location>

        <Directory /var/www/html/moodle/auth/shibboleth/index.php>
	     AuthType shibboleth
              #ShibRequestSetting applicationId mdl
             ShibRequireSession On
             require valid-user
	</Directory>
        #Double Check Moodle installation path

</VirtualHost>
</IfModule>
```

Next, enable apache shibboleth module and restart apache.

```
    a2enmod shib
    systemctl reload apache2.service
```

***Register both services with LIAF***

We have now set up shibboleth SP for the entity.It has to be registered with LIAF before using the Federation discovery Service to point different IDP's.

Download the  metadata from both applications by going to the following URL's. 

* ```https://YOUR-DNS/Shibboleth.sso/Metadata ```

Now register moodle service with LIAF .

Go to https://liaf.ac.lk/#join and follow the Service provider registration. 

Once the federation operator approves your request you will be sent a SP registration link.

you will be asked to use the content of your metadata file on federation registry registration. You may have to answer several questions describing your service to the federation provider.

Once you registered successfully you have enable the Shibboleth support in the application itself. For that Moodle and Wordpress has pluggins to be enabled and configured.

### Enabling Moodle Plugin

As Moodle admin, go to the '''Site administration''' >>> '''Plugins''' >>> '''Authentication''' and click on the '''Shibboleth''' enable '''eye'''. Next go to its settings.

***Fill in the fields of the form.***

The fields 'Username', 'First name', 'Surname', etc. should contain the name of the environment variables of the Shibboleth attributes that you want to map onto the corresponding Moodle variable. Especially the 'Username' field is of great importance because this attribute is used for the Moodle authentication of Shibboleth users.

```
Username: eppn

Moodle WAYF service: No

Shibboleth Service Provider logout handler URL: /Shibboleth.sso/Logout

Data mapping (First name): givenName

Data mapping (Surname): surname

Data mapping (Email address): mail

Update local (Email address): On Creation

Lock value (Email address): Locked

```
Click Save.

* Adjust  ```attribute-map.xml```  as

```cd /etc/shibboleth/```

``` vi attribute-map.xml```
Check and add the details if it's missing in the file
  
```bash
    <Attribute name="urn:mace:dir:attribute-def:sn" id="sn"/>
    <Attribute name="urn:oid:2.5.4.4" id="sn"/>
    <Attribute name="urn:mace:dir:attribute-def:givenName" id="givenName"/>
    <Attribute name="urn:oid:2.5.4.42" id="givenName"/>
    <Attribute name="urn:mace:dir:attribute-def:mail" id="mail"/>
    <Attribute name="urn:oid:0.9.2342.19200300.100.1.3" id="mail"/>
    <Attribute name="urn:mace:dir:attribute-def:email" id="email"/>
    <Attribute name="urn:oid:1.3.6.1.4.1.5923.1.1.1.10" id="email"/>
```
* Add following lines in ```attribute-policy.xml```.

``` vi attribute-policy.xml```
  
```bash
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
```

After, restart shibd and apache2
```
systemctl restart apache2
systemctl restart shibd
```
Now using a private browser, try to log in to both systems using your IDP test user.

## Steps for logging into Moodle using LIAF SSO

   - **Browse to the Moodle URL**: Visit the specified Moodle URL.
   - **Select the Login Button**: Click the login button located in the top right corner of the screen.
   - **Choose LIAF SSO**: You'll be redirected to a login page. Select the "Shibboleth Login" login button (As Administrator,Button name can be changed by ```Site Administration``` > ```Plugin``` > ```Authentication``` > ```Sibboleth``` > ```Authentication Method name```).
   - **Choose Your Institution**: If your institution is part of a federation, use the dropdown button to select your specific institution.
   - **Enter Credentials**: Enter your institutional username and password.
   - **Login**: Click the "Login" or "Sign In" button. Your institution's authentication system will verify your identity.
   - **Access Moodle**: After successful authentication, you will be logged into your Moodle account.

