---
title: Cabeçalhos de requisição
status: live
---

Um aplicação Slim automaticamente analisará todos os cabeçalhos de uma requisição HTTP. Você pode acessá-los usando o 
método `headers()` do objeto de requisição.

    <?php
    $app = new \Slim\Slim();

    // Obtem o objeto de requisição
    $req = $app->request();

    // Retorna os cabeçalhos da requisição como um array associativo
    $headers = $req->headers();

    // Get the ACCEPT_CHARSET header
    $charset = $req->headers('ACCEPT_CHARSET');

No segundo exemplo, o método `headers()` irá tanto retornar um valor de string ou `null` se o cabeçalho com o 
nome passado não existir.

A especificação HTTP determina que os nomes de cabeçalhos HTTP podem ser maiusculos, minusculos ou ambos. Slim é inteligente o suficiente
para analisar e retornar valores do cabeçalho se você pedi-lo usando um valor maiusculo, minusculo, misturado, com underline ou traços.
Sendo assim use a convenção de nome com a qual você se sinta mais confortavel.
