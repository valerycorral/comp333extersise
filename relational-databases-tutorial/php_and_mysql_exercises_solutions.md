# PHP and MYSQL Tutorial Exercises Solution for COMP 333

Created by Sebastian Zimmeck for
Wesleyan University - COMP 333: Software Engineering

## Deploying PHP Scripts

1. Deploying the Hello World PHP script does not work because
   a) your browser is not a web server; it can only render client-side files.
   b) GitHub Pages only allows us to serve static web pages. Their web server
   does not have PHP installed.

2. We need some cloud computing or hosting that runs a PHP interpreter on
   their server. Heroku does so and we can follow the instructions they give on
   <https://www.heroku.com/php>. (We will revisit deployment of our app on
   Heroku in a few weeks. For the time being, we will use a local server with
   PHP via XAMPP <https://sourceforge.net/projects/xampp/>).
