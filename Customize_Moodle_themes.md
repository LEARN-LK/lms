<h1>Customize Moodle Themes</h1>

<h2> 01 -Basic Customization (Theme Selector and Settings):</h2>

- Go to Administration > Appearance > Themes.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/128-thems.png" alt="image" style="max-width: 100%;width: 500px;">
 - Select your current theme.
- Click on the Themes Settings .
- Here, you can adjust various options like Designer mode, User themes, .

 <img src="https://github.com/LEARN-LK/lms/blob/master/img/129-thems.png" alt="image" style="max-width: 100%;width: 700px;">
 - Save your changes to see the updated theme.

<h3>02 - Add Custom Menu</h3>

- Go to Administration > Appearance > Themes.
- Select the theme you want to modify.
- Create the menu item:
-  Look for the section titled Custom menu items.
-  Each line defines a single item. Enter the details in this format:
   - Name|Link
   - Name is the text displayed for the menu item.

     <img src="https://github.com/LEARN-LK/lms/blob/master/img/130-menu.png" alt="image" style="max-width: 100%;width: 700px;">    
- Save the changes:Click Save changes at the bottom of the page.

  <img src="https://github.com/LEARN-LK/lms/blob/master/img/131-menu.png" alt="image" style="max-width: 100%;width: 500px;"> 
<h3>03 - Customising the Header</h3>

- The administrator has the capability to incorporate links, metatags, CSS, or JavaScript into the header section of your page through Site administration > Appearance > Additional HTML.

 <img src="https://github.com/LEARN-LK/lms/blob/master/img/132-header.png" alt="image" style="max-width: 100%;width: 500px;"> 
 
- In the 'Within HEAD' box, you can define HTML, CSS, or JavaScript that will be included on every page without the need to modify the Moodle code files."

  <img src="https://github.com/LEARN-LK/lms/blob/master/img/133-header.png" alt="image" style="max-width: 100%;width: 800px;"> 
- Save and Preview:

  <img src="https://github.com/LEARN-LK/lms/blob/master/img/134-header.png" alt="image" style="max-width: 100%;width: 800px;"> 

<h3>04 - Customising the Footer</h3>

- As with header options in the section above, the administrator can add links, CSS or Java Script to the footer section of your page via Site administration > Appearance > Additional HTML
- This might be useful for adding Google Analytics, for example.
- Add your HTML/CSS to the 'Before BODY is closed' box.

<h3>05 - Change Theme</h3>

- Log in as an administrator and navigate to Administration > Site administration > Appearance > Themes > Theme Selector.

  <img src="https://github.com/LEARN-LK/lms/blob/master/img/Screenshot%202024-01-05%20at%2010.27.26.png" alt="image" style="max-width: 100%;width: 900px;"> 

- In the "Appearance" section, you will see an option labeled "Themes". Click on it to see the available theme options.Change Theme: From the list of available themes, click on "Theme selector". You'll be presented with options to change the theme for different devices.
  
  <img src="https://github.com/LEARN-LK/lms/blob/master/img/Screenshot%202024-01-05%20at%2010.27.46.png" alt="image" style="max-width: 100%;width: 900px;">

- Choose a New Theme: For the device you want to change the theme for, click on the "Change theme" button next to the current theme.
- Select a New Theme: A list of available themes will appear. Choose the theme you want to apply by clicking the "Use theme" button next to it.
- Save Changes: Once you’ve selected a new theme, make sure to click "Save changes" at the bottom of the page.

<h3>06 - Add Custom Themes</h3>

- Choose a Theme: Browse the official Moodle themes repository for free themes or search online for reputable Moodle theme vendors based on features, functionalities, and appearance.

   <img src="https://github.com/LEARN-LK/lms/blob/master/img/138-0%20thems.png" alt="image" style="max-width: 100%;width: 700px;">
   
- Download or Install the Theme: Once you've chosen your theme, download it as a zip file or use the provided installation method, such as clicking on an "Install" button.
   
   <img src="https://github.com/LEARN-LK/lms/blob/master/img/137-thems.png" alt="image" style="max-width: 100%;width: 700px;">
   
- Using Moodle Plugin Installer: If your Moodle site allows it, you can upload the theme zip file directly through the Moodle interface. Navigate to Site administration > Plugins > Install plugins, and then drag and drop the zip file or use the file picker to select it.
 
   <img src="https://github.com/LEARN-LK/lms/blob/master/img/139-1%20thems.png" alt="image" style="max-width: 100%;width: 700px;">
   
- Set File Permissions (if using FTP): If you uploaded the theme via FTP, ensure the theme folder and its contents have the correct permissions for the web server to access them.

- Typically, you'll want to set the permissions to 755 (read/write/execute for owner, read/execute for group, read/execute for everyone).
  <pre><code>sudo chown -R www-data:www-data /var/www/html/moodle/theme</code></pre>
  
- Activate the Theme in Moodle: Log in as an administrator on your Moodle site. Navigate to Site administration > Appearance > Themes > Theme selector. You should see your uploaded theme listed. Click the "Use theme" button next to the theme to activate it.

<img src="https://github.com/LEARN-LK/lms/blob/master/img/141-thems.png" alt="image" style="max-width: 100%;width: 500px;">

- Clear Theme Cache (optional): In some Moodle versions, you may need to clear the theme cache for the changes to take effect. You'll usually find a "Clear theme caches" button on the Theme selector page.


