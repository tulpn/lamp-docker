# LAMP Docker Environment

A quick and easy to use docker-compose based PHP environment for developing.

Uses ```php:7.4-apache``` as a base image for the PHP + Apache setup. This makes use of mpm_prefork!

The custom Dockerfile for the build allows you to quickly setup any additional PHP extensions, comes with:
- PDO_mysql
- GD
- ZIP
- SOAP
- Sockets
- Intl
- OpCache
- XSL

You can create any vhosts files in the ```apache2/site-available``` folder and then just modify the ```apach2/init.sh``` file. 

The ```htdocs``` folder holds any of your projects. 

The ```logs``` folder automatically mounts to the internal ```/var/logs/apache``` folder and therefore you have all log files - if specified handy on your system. 

For any custom PHP settings, simply add anything into the ```php/php.ini``` file, which will be added as a 999-custom php ini file to the web container, overwriting any default settings (but not replacing the original php.ini file)

The database is specified in the docker-compose.yml file and is currently set to Mariadb.

Both the Database and the Web container load the ```.env``` file. The entire DB setup is handled with the default ```mysql_``` settings from the ```.env``` file. Hence, it makes sense to update this prior to building the environment. 

You can then access any API Keys/Secrets / Settings from the ```.env``` file in the web container, and even in PHP.

Composer is installed in the web container as well and can be directly access via the ```composer``` command. 

There is no .gitignore file included, do not use .env approach without gitignore, but since this is not intended for production, instead for quick and dirty PoC PHP environments of developers this is left to the developer!


# Logging
```Could not reliably determine the server's fully qualified domain name, using [...]```

Can be ignored, as it is just a warning and not relevant for local development


# Building & Starting Environment
```docker-compose up --build``` or in the background with ```docker-compose up -d```


# Todo
- Add easy SSL support 
- Use sed or similar to adjust vhost files based on Environment variables, instead of hardcoding
- Setup xdebug by default