# New project

In this short tutorial, we'll see how to create a blog with a main page and some articles.

There is some prerequisites before beginning. You need to have [PHP 8.2 or newer](https://www.php.net/downloads) and [composer](https://getcomposer.org/download/) installed on your computer

First step, create the project itself:

```bash
composer create-project archict/archict my_blog
cd my_blog
composer install
```

This first command create a new directory named `my_blog` containing all files which comes with Archict:

- `config/` is a collection of YAML file for configuration of [Services](../documentation/services.md)
- `public/` is the only accessible to end users
- `src/` contains all your source code
- `templates/` contains Twig templates

There is some others files and directories but they are not important now, we'll see what we can do with them later.

Want to see what it looks like now? Type `php -S localhost:8080 -t ./public` in your terminal and go to <http://localhost:8080> in your prefered browser. By default Arhict project comes with 2 pages: the main page you currently see and a second one (just for the example) located at <http://localhost:8080/status>.

Now we are ready to begin the road to our glorious blog!
