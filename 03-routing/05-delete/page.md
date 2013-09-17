---
title: Rotas DELETE
status: live
---

Use o método `delete()` do Slim para mapear uma função callback para uma URI que é requisitada com o método HTTP DELETE.

    <?php
    $app = new \Slim\Slim();
    $app->delete('/books/:id', function ($id) {
        //Delete book identified by $id
    });

Nesse exemplo, uma requisição HTTP DELETE para "/books/1" invocará a função callback associada, passando "1" como o
parâmetro da função de callback.

O primeiro parâmetro do método `delete()` do Slim é o URI. O último parâmetro é qualquer coisa que 
retorne `true` para a função `is_callable`. Tipicamente, o último parâmetro será uma [função anônima][anon-func].

### Sobescrita de Método

Infelizmente, navegadores modernos não provêem suporte nativo para requisições HTTP DELETE. Para trablhar esta limitação,
assegure que o método do seu formulário HTML seja "post", então adicione um parâmetro de sobrescrita de método 
para o seu formulário HTML dessa forma:

    <form action="/books/1" method="post">
        ... other form fields here...
        <input type="hidden" name="_METHOD" value="DELETE"/>
        <input type="submit" value="Delete Book"/>
    </form>


Se você está usando [Backbone.js][backbone] ou um cliente HTTP de linha de comando, você pode também sobrescrever o
método HTTP usando o cabeçalho **X-HTTP-Method-Override**.

[anon-func]: http://php.net/manual/en/functions.anonymous.php
[backbone]: http://documentcloud.github.com/backbone/
