---
title: Métodos HTTP customizados
status: live
---

### Uma rota, múltiplos métodos HTTP

As vezes você precisa de uma rota para responder a múltiplos métodos HTTP; as vezes você precisa de uma para responder
a métodos HTTP customizados. Você pode realizar ambos com o método `via()` do objeto Route. Este exemplo demonstra
como mapear uma URI para um callback que responde a múltiplos métodos HTTP.

    <?php
    $app = new \Slim\Slim();
    $app->map('/foo/bar', function() {
        echo "Eu respondo a múltiplos métodos HTTP!";
    })->via('GET', 'POST');
    $app->run();

The route defined in this example will respond to both GET and POST requests for the resource identified by “/foo/bar”.
Specify each appropriate HTTP method as a separate string argument to the Route object's `via()` method. Like other
Route methods (e.g. `name()` and `conditions()`), the `via()` method is chainable:

    <?php
    $app = new \Slim\Slim();
    $app->map('/foo/bar', function() {
        echo "Fancy, huh?";
    })->via('GET', 'POST')->name('foo');
    $app->run();

### One route, custom http methods

The Route object's `via()` method is not limited to just GET, POST, PUT, DELETE, and OPTIONS methods. You may also
specify your own custom HTTP methods (e.g. if you were responding to WebDAV HTTP requests). You can define a route
that responds to a custom “FOO” HTTP method like this:

    <?php
    $app = new \Slim\Slim();
    $app->map('/hello', function() {
        echo "Hello";
    })->via('FOO');
    $app->run();
