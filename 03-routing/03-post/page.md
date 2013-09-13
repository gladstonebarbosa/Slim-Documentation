---
title: Rotas POST
status: live
---

Use o método `post()` do Slim para mapear uma função callback em uma URI que é requisitada com o método HTTP POST.

    <?php
    $app = new \Slim\Slim();
    $app->post('/books', function () {
        //Criar livro
    });

Neste exemplo, uma requisição HTTP POST para "/books" invocará a função callback associada.

O primeiro parâmetro do método `post()` é um recurso URI. O último parâmetro é qualquer coisa que retorne `true` para
a função `is_callable()`. Tipicamente, o último parâmetro será uma [função anônima][anon-func].

[anon-func]: http://php.net/manual/en/functions.anonymous.php
