# How-to-Upgrade-Magento-Version-from-2.3.X-to-2.4.0-
How to Upgrade Magento Version from 2.3.X to 2.4.0?

Step 1: If you are directly performing the upgrade on your live site then first put your site into maintenance mode by running below command.

1 php bin/magento maintenance:enable

Step 2: If you are performing the upgrade on your local system then you can skip step 1 and start with step 2.
Take a backup of the composer.json

1  cp composer.json composer.json.bak

Step 3: Install the Composer update plugin

1  composer require magento/composer-root-update-plugin=~1.0 --no-update
2  composer update

 

Step 4: Update composer.json file with latest version. In our case, it is Magento Version 2.4.0. Navigate to your Magento 2 installation root path and run below command

1 composer require magento/product-community-edition=2.4.0 --no-update


Step 5: Run below command

1 composer update
This command will take some time to finish. This command will actually download all the required packages and upgrade your Magento version from 2.3.x to 2.4.0. After this command finish, run below commands

Step 6: Clear cache and regenerate code.

php bin/magento cache:clean
 
rm -rf var/cache/*
 
rm -rf var/page_cache/*
 
rm -rf generated/code/*
 
php bin/magento setup:upgrade
  
php bin/magento setup:di:compile
  
php bin/magento setup:static-content:deploy -f

Step 7: Disable maintenance mode

1 php bin/magento maintenance:disable

Note: Remove update directory from your root folder as update directory is not a part of Magento 2.4
