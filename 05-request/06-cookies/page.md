---
title: Requisições de Cookie
status: live
---

### Obter Cookies

Uma aplicação Slim automaticamente analisará cookies enviado com a requisição HTTP atual. Você pode obter valores de cookie
com o método `getCookie()` dessa forma:

    <?php
    $foo = $app->getCookie('foo');

Apenas Cookies enviados com a atual requisição HTTP são acessiveis com este método.
Se você atribuir um cookie durante a requisição atual, o mesmo não será acessível com este método até a requisição subsequente.
Se você quer obter um array de todos os cookies enviados com a atual requisição, você deve usar o método `cookies()` do objeto de requisição:

    <?php
    $cookies = $app->request()->cookies();

Quando multiplos cookies com o mesmo nome estão disponiveis (ex: porque eles tem caminhos diferentes) apenas o mais especifico
é retornado. Veja RFC 2109.

### Obter Cookies Criptografados

Se você anteriormente atribuiu um cookie criptografado, você pode obter seu valor descriptografado com o método `getEncryptedCookie()`:

    <?php
    $value = $app->getEncryptedCookie('foo');

Se o cookie foi modificado enquanto com o cliente HTTP, Slim automaticamente destruirá o valor do cookie e invalidará o 
cookie na próxima resposta HTTP. Você pode desabilitar este comportamento passando `false` como o segundo parâmetro:

    <?php
    $value = $app->getEncryptedCookie('foo', false);

Se você destruir cookies inválidos ou não, `null` é retornado se o cookie não existe ou é inválido.
