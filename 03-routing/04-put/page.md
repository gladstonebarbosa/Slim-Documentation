---
title: Rotas PUT
status: live
---

Use o método `put()` do Slim para mapear uma função callback para uma URI que é requisitada com o método HTTP PUT.

    <?php
    $app = new \Slim\Slim();
    $app->put('/books/:id', function ($id) {
        //Update book identified by $id
    });

Nesse exemplo, uma requisição HTTP PUT para "/books/1" invocará a função callback associada, passando "1" como
o parâmetro da função de callback.

O primeiro parâmetro do método `put()` do Slim é o URI. O último parâmetro é qualquer coisa que retorne `true` para
a função `is_callable()`. Tipicamente, o último parâmetro será uma [função anônima][anon-func].

### Sobrescrita de Método

Infelizmente, navegadores modernos não provêem suporte nativo para requisições HTTP PUT. Para trabalhar esta limitação,
assegure que o método do seu formulário HTML seja "post", então adicione um parâmetro de sobrescrita de método para
o seu formulário HTML dessa forma:

    <form action="/books/1" method="post">
        ... other form fields here...
        <input type="hidden" name="_METHOD" value="PUT"/>
        <input type="submit" value="Update Book"/>
    </form>

Se você está usando [Backbone.js][backbone] ou um cliente HTTP de linha de comando, você pode também sobrescrever o
método HTTP usando o cabeçalho **X-HTTP-Method-Override**.

[anon-func]: http://php.net/manual/en/functions.anonymous.php
[backbone]: http://documentcloud.github.com/backbone/
