[Back to Home](../README.md)
# Wordpress
* use Sage theme (https://roots.io/sage/) and its inbuilt Gulp workflow (docs at [Sage: Theme Installation](https://roots.io/sage/docs/theme-installation/))

## Plugins
* be wary of using too many plugins for stuff that can be nicely solved in code.
* plugins can sometimes load unnecessary bloat (which not only increases size & requests but can also prove to be a pain to modify later on).
* sometimes it’s useful to disable default styles (or scripts) in some plugin and rather write your own (as is the case with Woocommerce, Woocommerce Germanized or WPML)
* on the other hand: if client control of the functionality is preferable, plugin could be useful

## Functions & Namespacing
* your functions should go into separate files
* sage structure is a good inspiration here (your functions go into lib/woocommerce.php, etc.)
* for adding functions to WP actions & filters in namespaced files, the notation is following:

```
namespace Roots\Sage\LwzAdmin;

add_filter( 'init', __NAMESPACE__ . '\\my_init_function' );
function my_init_function() {
}
```

## Bedrock & Composer
* Composer is a php package manager, it can also take care of your plugins and wordpress core.
* when deploying your Bedrock app to Fortrabbit, Composer runs and installs dependencies. This way the server will always have clean versions of the plugins
* paid plugins need to be installed manually and overriden in .gitignore
* installing plugins through Composer is easy as   
`composer require wpackagist-plugin/%plugin-slug%`
* to update plugins to latest version, run  
`composer update`
* to update wordpress core, you need to change the desired version in composer.json before running `composer update`

## Fortrabbit
* it’s best to use Bedrock here
* for local development, use the SLD copy of amazon-s3-plugin.php & add S3 credentials to your used environment (eg. config/environments/development.php). See (https://bitbucket.org/sleighdogs/fortrabbit-amazon-s3-plugin) for more info
* for more info follow [Fortrabbit: Install WordPress 4](https://help.fortrabbit.com/install-wordpress-4)
* when using git for deploy, we set it so it’s simultaneously pushed to fortrabbit & our own repo (eg. bitbucket). You can set two push urls like this and push through `git push both`

```
git remote add both me@original:something.git
git remote set-url --add --push both me@original:something.git
git remote set-url --add --push both git://somewhere/something.git
```

## Backups
* try to have some form of automated backups running
* one way is to use UpdraftPlus that backups database to your DropBox account. That way you have all your db backups in one place and don’t have to care much about it, but other ways are also perfectly fine as long as they work for you

## E-mails
* probably the easiest way to setup emails in environments where default wp_mail won’t work (eg. fortrabbit) is to use Mandrill and its wordpress plugin. You can setup a free account for testing and the just switch it the API key for client’s later
