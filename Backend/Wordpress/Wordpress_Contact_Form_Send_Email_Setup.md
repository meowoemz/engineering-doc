Prerequisite:
 
    - Installed Wordpress
    - Installed Contact Form Plugin
    - Admin access
    - SMTP information
    
Login into Wordpress Control Panel.

Install mail plugin, in this case, we use `WP MAIL SMTP`, active the plugin after installation.

At plugin `setting` tab, enter `SMTP` information, in this case, we use google SMTP, `Client ID`, `Client Secrect` and `Authorized redirect URI
` are required.

https://developers.google.com/identity/sign-in/web/devconsole-project

Then you can send test email to verify plugin functionality.

**_References_**:

http://www.wpbeginner.com/plugins/how-to-send-email-in-wordpress-using-the-gmail-smtp-server/

https://wpforms.com/how-to-fix-wordpress-contact-form-not-sending-email-issue/