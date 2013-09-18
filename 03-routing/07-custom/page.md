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

A rota definida neste exemplo responderá para ambas as requisições GET e POST em recursos identificados por "/for/bar".
Especifique cada método HTTP apropriado como parâmetros do tipo string para o método `via()` do objeto Route.
Como outros métodos do objeto Route (ex: `name()` e `conditions()`), o método `via()` é encadeável:

    <?php
    $app = new \Slim\Slim();
    $app->map('/foo/bar', function() {
        echo "Fancy, huh?";
    })->via('GET', 'POST')->name('foo');
    $app->run();

### Uma rota, métodos HTTP customizados

O método `via()` do objeto Route não é limitado apenas para os métodos GET, POST, PUT, DELETE e OPTIONS. Você pode
também especificar seu próprio método HTTP customizado (ex: se você estivesse respondendo  para requisições WebDAV HTTP).
Você pode definir uma rota que responda para um método customizado HTTP "FOO" dessa forma:

    <?php
    $app = new \Slim\Slim();
    $app->map('/hello', function() {
        echo "Hello";
    })->via('FOO');
    $app->run();
