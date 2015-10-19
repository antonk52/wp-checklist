# WP checklist
##### A checklist for a new Wordpress project

_This list is intended to fit as many projects as possible. Therefore, it is okay if your wordpress site developing process distinguishes from what you will see below._

- [ ] Change permalinks ([1](#1-change-permalinks))
- [ ] Don’t crop on thumbnails ([2](#2-dont-crop-on-thumbnails))
- [ ] Disable comments ([3](#3-disable-comments))
- [ ] Essential pages (home, services, about, blog, contact, 404)
- [ ] Set static Home and Blog page
- [ ] Enable and set up needed plugins
- [ ] Set up frequent backups
- [ ] Child theme
- [ ] Hide update notifications for all but admin ([4](#4-hide-notifications))
- [ ] Hide wordpress version ([5](#5-hide-version))
- [ ] Delete readme from the root folder
- [ ] Whitelist for wp-admin ([6](#6-whitelist-wp-admin-access))
- [ ] Set file permissions
- [ ] Correct display of page titles
- [ ] Limit the number of revisions on each post ([7](#7-limit-revisions))
- [ ] Custom login page url
- [ ] Custom logo on login page ([8](#8-custom-logo))
- [ ] Generate sitemap.xml
- [ ] .htaccess -> gzip, expires headers ([9](#9-htacces-with-gzip-and-expire-headers))
- [ ] Google Analytics
- [ ] Add favicon
- [ ] Google Page Insights

---


##### 1. Change permalinks
Go to `Settings -> Permalinks` in the admin panel and pick the desired option.

##### 2. Don't crop on thumbnails
Go to `Settings -> Media` in the admin panel and uncheck `crop on thumbnails`.

##### 3. Disable comments
Go to `Settings -> Discussion` in the admin panel and uncheck `leave comments on new posts`.

##### 4. Hide notifications
To hide update notifications for all users but the admin user, copy the code below to your functions.php file
```
function hide_update_notice_to_all_but_admin_users()
{
  if (!current_user_can('update_core')) {
    remove_action( 'admin_notices', 'update_nag', 3 );
  }
}
add_action( 'admin_head', 'hide_update_notice_to_all_but_admin_users', 1 );
```

##### 5. Hide version
To hide the WordPress version, add the following to your functions.php file
```
<?php remove_action('wp_head', 'wp_generator'); ?>
```

##### 6. Whitelist wp-admin access
If you have a static IP and you know all the IP's from where people will access the admin part of the site, you can copy the  .htaccess file from `assets/wp-admin/.htaccess` in this repo inside your wp-admin folder (NOT root directory). Don't forgot to input your IP to be able to access the admin area yourself.

##### 7. Limit revisions
To set a limit of revisions for each post, copy the code below to your wp-config.php file
```
define( 'WP_POST_REVISIONS', 3 );
```

##### 8. Custom logo
To use a custom logo on the login page, copy the code below to your functions.php
```
function custom_login_logo()
{
  echo '
  <style type="text/css">
    h1 a {
      background-image: url('.get_bloginfo('template_directory').'/images/CUSTOM-LOGIN-LOGO.png) !important;
    }
  </style>
  ';
}
add_action('login_head', 'custom_login_logo');
```

##### 9. .htacces with gzip and expire headers
Place the .htaccess from `/assets` in this repo in your root directory.
