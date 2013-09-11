---
title: Olá Mundo
status: live
---

Instancie uma aplicação Slim:

    $app = new \Slim\Slim();

Defina uma rota HTTP GET:

    $app->get('/hello/:name', function ($name) {
        echo "Hello, $name";
    });

Execute a aplicação Slim:

    $app->run();
