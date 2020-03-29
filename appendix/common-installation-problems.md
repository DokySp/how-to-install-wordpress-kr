# 자주 묻는 질문

The following are some of the most common installation problems. For more information and troubleshooting for problems with your WordPress installation, check out [FAQ Installation](https://wordpress.org/support/article/faq-installation/) and [FAQ Troubleshooting](https://wordpress.org/support/article/faq-troubleshooting/).

**I see a directory listing rather than a web page.**

The web server needs to be told to view `index.php` by default. In Apache, use the `DirectoryIndex index.php` directive. The simplest option is to create a file named `.htaccess` in the installed directory and place the directive there. Another option is to add the directive to the web server’s configuration files.

**I see lots of *Headers already sent* errors. How do I fix this?**

You probably introduced a syntax error in editing `wp-config.php`.

1. Download wp-config.php (if you don’t have shell access).
1. Open it in a text editor.
1. Check that the first line contains nothing but <?php, and that there is no text before it (not even whitespace).
1. Check that the last line contains nothing but ?>, and that there is no text after it (not even whitespace).
1. If your text editor saves as Unicode, make sure it adds no byte order mark (BOM). Most Unicode-enabled text editors do not inform the user whether or not it adds a BOM to files; if so, try using a different text editor.
Save the file, upload it again if necessary, and reload the page in your browser.

**My page comes out gibberish. When I look at the source I see a lot of “*<?php ?>*” tags.**

If the `<?php ?>` tags are being sent to the browser, it means your [PHP](https://wordpress.org/support/article/glossary/#php) is not working properly. All PHP code is supposed to be executed before the server sends the resulting [HTML](https://wordpress.org/support/article/glossary/#html) to your web browser. (That’s why it’s called a *pre*processor.) Make sure your web server meets the requirements to run WordPress, that PHP is installed and configured properly, or contact your hosting provider or system administrator for assistance.

**I keep getting an *Error connecting to database* message but I’m sure my configuration is correct.**

Try resetting your MySQL password manually. If you have access to MySQL via shell, try issuing:

```SQL
SET PASSWORD FOR 'wordpressusername'@'hostname' = OLD_PASSWORD('password');
```
If you do not have shell access, you should be able to simply enter the above into an SQL query in phpMyAdmin. Failing that, you may need to use your host’s control panel to reset the password for your database user.

**I keep getting an *Your PHP installation appears to be missing the MySQL extension which is required by WordPress* message but I’m sure my configuration is correct.**

Check to make sure that your configuration of your web-server is correct and that the MySQL plugin is getting loaded correctly by your web-server program. Sometimes this issue requires everything in the path all the way from the web-server down to the MySQL installation to be checked and verified to be fully operational. Incorrect configuration files or settings are often the cause of this issue.

**My image/MP3 uploads aren’t working.**

If you use the Rich Text Editor on a blog that’s installed in a subdirectory, and drag a newly uploaded image into the editor field, the image may vanish a couple seconds later. This is due to a problem with TinyMCE (the rich text editor) not getting enough information during the drag operation to construct the path to the image or other file correctly. The solution is to NOT drag uploaded images into the editor. Instead, click and hold on the image and select **Send to Editor**.