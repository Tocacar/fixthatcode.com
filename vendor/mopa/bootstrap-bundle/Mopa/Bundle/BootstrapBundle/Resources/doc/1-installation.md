Installation
============

Prerequisites
-------------

### Less (recommended)

Less is not required, but is extremely helpful when using bootstrap2 variables, or mixins,
If you want to have a easier life, have a look into:
If you do not have less installed, currently you have several option, but please do NOT ask for help.

[Less Documentation](https://github.com/phiamo/MopaBootstrapBundle/blob/master/Resources/doc/less-installation.md)

Installation
------------

1. Add this bundle to your project in composer.json:

    1.2. Plain BootstrapBundle
        symfony 2.1 uses composer (http://www.getcomposer.org) to organize dependencies:

        ```json
           {
               "require": {
                   "mopa/bootstrap-bundle": "dev-master",
               }
           }
        ```
    1.2. BootstrapBundle and twitters bootstrap

        To have composer managing twitters bootstrap too, you can either run it with
        --install-suggests or add the following to your composer.json:

        ```json
           {
               "require": {
                   "mopa/bootstrap-bundle": "dev-master",
                   "twitter/bootstrap": "master"
               },
               "repositories": [
                   {
                       "type": "package",
                       "package": {
                           "version": "master", /* whatever version you want */
                           "name": "twitter/bootstrap",
                           "source": {
                               "url": "https://github.com/twitter/bootstrap.git",
                               "type": "git",
                               "reference": "master"
                           },
                           "dist": {
                               "url": "https://github.com/twitter/bootstrap/zipball/master",
                               "type": "zip"
                           }
                       }
                   }
               ]
           }
        ```

    1.3. BootstrapBundle, twitters bootstrap and further suggests

        ```json
           {
               "require": {
                   "mopa/bootstrap-bundle": "dev-master",
                   "twitter/bootstrap": "master",
                   "knplabs/knp-paginator-bundle": "dev-master",
                   "knplabs/knp-menu-bundle": "dev-master",
                   "craue/formflow-bundle": "dev-master"
               },
               "repositories": [
                   {
                       "type": "package",
                       "package": {
                           "version": "master", /* whatever version you want */
                           "name": "twitter/bootstrap",
                           "source": {
                               "url": "https://github.com/twitter/bootstrap.git",
                               "type": "git",
                               "reference": "master"
                           },
                           "dist": {
                               "url": "https://github.com/twitter/bootstrap/zipball/master",
                               "type": "zip"
                           }
                       }
                   }
               ]
           }
        ```

    1.4. BootstrapBundle, twitters bootstrap and automatic symlinking

        If you decided to let composer install twitters bootstrap, you might want to activate auto symlinking and checking, after composer update/install.
        So add this to your existing scripts section in your composer json:
        (recommended!)

           ```json
           {
               "scripts": {
                   "post-install-cmd": [
                       "Mopa\\Bundle\\BootstrapBundle\\Composer\\ScriptHandler::postInstallSymlinkTwitterBootstrap"
                   ],
                   "post-update-cmd": [
                       "Mopa\\Bundle\\BootstrapBundle\\Composer\\ScriptHandler::postInstallSymlinkTwitterBootstrap"
                   ]
               }
           }
           ```

        There is also a console command to check and / or install this symlink:

           ```bash
           php app/console mopa:bootstrap:install
           ```

        With these steps taken, bootstrap should be install into vendor/twitter/bootstrap/ and a symlink
        been created into vendor/mopa/bootstrap-bundle/Mopa/BootstrapBundle/Resources/bootstrap.

    1.5. Include bootstrap manually or in another way:

        For including bootstrap there are different solutions, why using this one?
        have a look into [Including Bootstrap](https://github.com/phiamo/MopaBootstrapBundle/blob/master/Resources/doc/including-bootstrap.md)

2. Add this bundle to your app/AppKernel.php:

    ``` php
    // application/ApplicationKernel.php
    public function registerBundles()
    {
        return array(
            // ...
            new Mopa\Bundle\BootstrapBundle\MopaBootstrapBundle(),
            // ...
        );
    }
    ```

    2.1. If you decided to add knp-menu-bundle, knp-paginator-bundle, or craue-formflow-bundle add them too:

    ``` php
    // application/ApplicationKernel.php
    public function registerBundles()
    {
        return array(
            // ...
            new Mopa\Bundle\BootstrapBundle\MopaBootstrapBundle(),
            new Knp\Bundle\MenuBundle\KnpMenuBundle(),
            new Knp\Bundle\PaginatorBundle\KnpPaginatorBundle(),
            new Craue\FormFlowBundle\CraueFormFlowBundle(),
            // ...
        );
    }
    ```

3. If you like configure your config.yml (not mandatory)

    ``` yaml
    mopa_bootstrap:
        form:
            show_legend: false # default is true
            show_child_legend: false # default is true
            error_type: block # or inline which is default
    ```

