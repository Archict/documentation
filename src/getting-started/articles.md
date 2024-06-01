# Articles

Now let's create the page for our articles. Here is the steps we'll follow:

1. Create the route with a basic controller (`/articles/{id}`)
2. Add a directory with some articles
3. Render them with Twig

**Let's go!**

## Create the route and the controller

First, let's create a basic empty controller

```php
# src/Controller/ArticlesController.php
<?php
declare(strict_types=1);

namespace Archict\Archict\Controller;

use Archict\Router\RequestHandler;
use Psr\Http\Message\ServerRequestInterface;

final class ArticlesController implements RequestHandler
{
    public function handle(ServerRequestInterface $request): string
    {
        return 'Article ' . $request->getAttribute('id');
    }
}
```

And then declare our route in `Application` with

```php
$collector->addRoute(Method::GET, '/article/{id:\d+}', new ArticlesController());
```

`/article/{id:\d+}` matches all uri beginning with `/article/` followed by a number, we call this number `id` so we can get it back in the controller via the attributes of the request.

If you go to <http://localhost:8080/article/42>, you should see a white page with just `Article 42` writed.

## Add some articles

In a real blog, we should implement a database and store our existing articles inside, but it's not the matter of this tutorial so we'll go to a shorter path: filesystem. We will store our articles inside `public/articles` and name them with their ids. For example, article 42 will have path `public/articles/42.html.twig`. I let you create some Twig templates corresponding to our system and then we can tune the controller to get them.

## Twig rendering

The controller need to:

- get the seeked article id
- check if it exists
- render it

```php
# src/Controller/ArticlesController.php
<?php
declare(strict_types=1);

namespace Archict\Archict\Controller;

use Archict\Archict\Services\Twig;
use Archict\Router\HTTPExceptionFactory;
use Archict\Router\RequestHandler;
use Psr\Http\Message\ServerRequestInterface;

final readonly class ArticlesController implements RequestHandler
{
    public function __construct(private Twig $twig)
    {
    }

    public function handle(ServerRequestInterface $request): string
    {
        // Get article id
        $article_id = $request->getAttribute('id');

        // Check it exists
        $filename = __DIR__ . '/../../public/articles/' . $article_id . '.html.twig';
        if (! file_exists($filename)) {
            throw HTTPExceptionFactory::NotFound("Article $article_id not found");
        }

        // Render it
        return $this->twig->render($filename);
    }
}
```

Don't forget to add the argument to the controller constructor in `Application`

```php
$collector->addRoute(Method::GET, '/article/{id:\d+}', new ArticlesController($this->twig));
```

Now if you go to <http://localhost:8080/article/42>, you should see you article. You can replace 42 by any number, if the article doesn't exists you'll get the message that the page doesn't exist.
