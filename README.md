# Laravel htaccess
.htaccess file to be put in the root folder of your Laravel so that it can be opened without the need to modify any Laravel folders/files when you are uploading the script in the public_html folder of your shared web hosting.


# Laravel Security on Shared Hosting

Using Laravel on Shared Hosting is a bit tricky since we do not have the access ( or limited ) to the SSH. Furthermore, we can't also modify the server settings such as document root. In order to make sure the HTTP Request goes to the public folder, we need to modify the rewrite rule as in the file .htaccess in this git.

However, there are also some securities concern IF you upload ALL Laravel folders and files in the public_html. Thus, you need to modify the directory structure to increase your Laravel project.

To make requests coming to Laravel go to the public folder, you can follow the steps below:

1) Move all Laravel files and folders except the "public" folder to a directory outside of public_html. Let's call this directory "laravel".

2) Move the contents of the "public" folder inside the "laravel" directory to the public_html directory.

3) Edit the index.php file inside the public_html directory and modify the following lines:

FROM

`
require __DIR__.'/../vendor/autoload.php';
$app = require_once __DIR__.'/../bootstrap/app.php';
`

TO

`
require __DIR__.'/../laravel/vendor/autoload.php';
$app = require_once __DIR__.'/../laravel/bootstrap/app.php';
`

4) In the public_html directory, create a new file named .htaccess if it does not already exist.

5) Edit the .htaccess file and add the following lines:

`
RewriteEngine On
RewriteRule ^(.*)$ laravel/public/$1 [L]
`


6) Save the .htaccess file.

With these steps, requests coming to your domain will now be redirected to the public folder of Laravel.
