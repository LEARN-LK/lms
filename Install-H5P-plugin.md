<h1>Install the H5P plugin</h1>

* Access your Moodle installation with administrator credentials. Navigate to Site Administration in the admin menu, click on Plugins, and select the option to install plugins. Next, click on the button labeled "Install plugins from the Moodle plugins directory."
  
<img src="https://github.com/LEARN-LK/lms/blob/master/img/78-h5p-plugin1.png"  style="max-width: 100%;width: 700px;"><img src="https://github.com/LEARN-LK/lms/blob/master/img/79-h5p-plugin2.png"  style="max-width: 100%;width: 600px;">
*  At this point, you may have to log into your moodle.org account. Locate the H5P plugin page and press the button labelled Install now.
  
<img src="https://github.com/LEARN-LK/lms/blob/master/img/80-h5p-plugin3.png"  style="max-width: 100%;width: 700px;">
<img src="https://github.com/LEARN-LK/lms/blob/master/img/81-h5p-plugin4.png"  style="max-width: 100%;width: 700px;">
<img src="https://github.com/LEARN-LK/lms/blob/master/img/82-h5p-plugin5.png"  style="max-width: 100%;width: 700px;">
*  On the following screen, click the "Install now" link next to the site on which you want to install H5P.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/83-h5p-plugin6.png?raw=true"  style="max-width: 100%;width: 700px;">  

* if you having this kind of error:

> [!NOTE]
> There is a request to install plugin Interactive Content – H5P (mod_hvp) version 2023122500 from the Moodle plugins directory on this site. However, the location /var/www/html/moodle/mod is not writable. You need to give write access for the web server user to the location, then press the continue button to repeat the check.


* follow this Step :
<pre><code>sudo chown -R www-data:www-data /var/www/html/moodle/mod
sudo chmod -R 755 /var/www/html/moodle/mod
sudo chmod -R 775 /var/www/html/moodle/mod/data
</code></pre>


*  You'll be redirected back to your site; confirm the installation by clicking on "Continue."

<img src="https://github.com/LEARN-LK/lms/blob/master/img/84-h5p-plugin7.png"  style="max-width: 100%;width: 700px;">       
*  Review the installation log and look for any error messages. Afterward, click "Continue" again.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/85-h5p-plugin8.png"  style="max-width: 100%;width: 700px;">
     
*  You are now on the Plugins check page. Confirm that the H5P plugin status is set to "To be installed." Continue by clicking the button labeled "Upgrade Moodle database now" (Note: This process may take some time).
  
<img src="https://github.com/LEARN-LK/lms/blob/master/img/86-h5p-plugin9.png"  style="max-width: 100%;width: 700px;">      
*  You should now see a message from the H5P plugin. Take note of whether the content types were automatically installed. If not, proceed to the next section on uploading and creating content. Click "Continue" when you are ready to proceed.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/87-h5p-plugin10.png"  style="max-width: 100%;width: 700px;">     
*  Verify the H5P Settings and press Save changes. The default settings should be fine for most sites.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/88-h5p-plugin11.png"  style="max-width: 100%;width: 700px;">   
  
