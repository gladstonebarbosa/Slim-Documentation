---
title: Nomes de rota
status: live
---

Slim permite você atribuir um nome para uma rota. Nomeando uma rota permite você dinâmicamente gerar URLs usando o 
método helper urlFor. Quando você usa o método `urlFor()` do Slim para criar URLs, você pode livremente mudar os
padrões da rota sem quebrar sua aplicação. Aqui está um exemplo de uma rota nomeada:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:name', function ($name) {
        echo "Hello, $name!";
    })->name('hello');

Você pode agora gerar URLs para esta rota usando o método `urlFor()`, descrito depois nesta documentação.
O método `name()` também é incadeável:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:name', function ($name) {
        echo "Hello, $name!";
    })->name('hello')->conditions(array('name' => '\w+'));
