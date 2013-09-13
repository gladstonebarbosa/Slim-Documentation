---
title: GET Routes
status: live
---

Use o método `get()` do Slim para mapear uma função callback em uma URI que é requisitada com o método HTTP GET.

    <?php
    $app = new \Slim\Slim();
    $app->get('/books/:id', function ($id) {
        //Mostra livro identificado pelo $id
    });

Neste exemplo, uma requisição HTTP GET para "/books/1" será invocada com a função de callback associada, passando "1"
como  o parâmetro do callback.

O primeiro parâmetro do método `get()` do Slim é um recurso de URI. O último parâmetro é qualquer coisa que retorne
`true` para a função `is_callable()`. Tipicamente, o último parâmetro será uma [função anônima][anon-func].

[anon-func]: http://php.net/manual/en/functions.anonymous.php
