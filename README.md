# WP checklist
##### A checklist for a new Wordpress project

_This list has been intended to fit as many projects as possible. Therefore, it is okay if your wordpress site developing process distinguishes from what you will see below._

- [ ] Change permalinks ([1](#Settings/Permalinks))
- [ ] Don’t crop on thumbnails ([2](#Settings/Media))
- [ ] Disable comments (3)
- [ ] essential pages
- [ ] Set static Home and Blog page
- [ ] enable and set up needed plugins
- [ ] set up frequent backups
- [ ] child theme
- [ ] hide update notifications for all but admin (4)
- [ ] hide wordpress version (5)
- [ ] delete readme from the root folder
- [ ] Whitelist for wp-admin (6)
- [ ] Set file permissions
- [ ] Correct display of page titles
- [ ] Limit the number of revisions on each post (7)
- [ ] Custom login page url
- [ ] Custom logo on login page (8)
- [ ] Generate sitemap.xml
- [ ] .htaccess -> gzip, expires headers (9)
- [ ] Google Analytics
- [ ] 404 page
- [ ] Add favicon
- [ ] Google Page Insights

---


##### 1. Settings/Permalinks
##### 2. Settings/Media uncheck crop on thumbnails
##### 3. Settings/Discussion uncheck leave comments on new posts
##### 4. To hide update notifications for all but admin user copy code below to your functions.php file
```
function hide_update_notice_to_all_but_admin_users()
{
    if (!current_user_can('update_core')) {
        remove_action( 'admin_notices', 'update_nag', 3 );
    }
}
add_action( 'admin_head', 'hide_update_notice_to_all_but_admin_users', 1 );
```

##### 5. To hide WP version add following to your functions.php file
```
<?php remove_action('wp_head', 'wp_generator'); ?>
```

##### 6. If you have a static IP and you know all the IP's from where people will access the admin part of the site, you can copy the  .htaccess file from assets/wp-admin/.htaccess inside your wp-admin folder (NOT root directory. Don't forgot to input your IP to be able to access the admin area yourself.

##### 7. To set limit of revisions for each post copy code below to your wp-config.php file
```
define( 'WP_POST_REVISIONS', 3 );
```

##### 8. To use custom logo on the login page copy the code below to your funcions.php
```
function custom_login_logo() { echo '<style type="text/css"> h1 a { background-image: url('.get_bloginfo('template_directory').'/images/custom-login-logo.png) !important; } </style>'; } 
add_action('login_head', 'custom_login_logo');
```

##### 9. Place .htaccess from assets in your root directory

