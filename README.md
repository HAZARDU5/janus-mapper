JanusVR Mapper
==============

A headless client for the JanusVR server that scrapes a list of URLs from a given JanusVR compatible room and follows
them a specfic number of levels deep to construct a map. User data is requested from the JanusVR server at regular
intervals so it can show the population of each room. This data is then cached for a specific length of time and
processed into a JanusVR compatible "Map Room" which users can access to see who's online.

It uses the [Laravel](http://laravel.com/) 4 PHP framework and is designed to run on a Linux server running Apache.

Dependencies
------------
* [Laravel 4 PHP Framework](http://laravel.com/)
* [Goutte PHP Web Scraper](http://github.com/fabpot/goutte)
* PHP 5.4 or higher

Installation
------------

1) `cd` to the root of the repository and follow the instructions at
[https://getcomposer.org/download/](https://getcomposer.org/download/) to install Composer.

2) The following command from the root of the repository: `php composer.phar install`. This will install any required
composer packages into the `vendor` folder. Note that you will need the `php` binary correctly set in your PATH for this
to work.

3) Run `php composer.phar update` to update any packages.

4) If developing locally you may want to set up a new folder with custom config for your environment in the `app/config`
folder. Alternately, adjust the config in the `app/config/local` folder.

5) You will need to edit `app/bootstrap/start.php` and set the `local` environment to match your development machine's
hostname. Add other environment -> hostname mappings here as needed. You can find your hostname by opening up a terminal
and running `hostname`.

6) You can also override only parts of the global config by specifying the keys you wish to override in a php file of
the same name inside the `local` folder. I.e. you can add `debug => true` to a returned array in
`app/config/local/app.php` to turn on debug mode for your local development server.

Usage
-----

* `cd` to the repository folder on your server and run `php artisan crawler:crawl` to start a crawl. This will retrieve
crawl data based on the settings in `app/config/crawler.php` and store it in the server cache at `app/storage/cache`. If
you want to run this command on a scheduled timer, add it to the user's `crontab` on the server by running the following
command: `crontab -e`.