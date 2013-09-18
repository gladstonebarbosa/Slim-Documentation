---
title: Condições de rota
status: live
---

Slim permite você atribuir condições para os parâmetros da sua rota. Se as condições especificadas não são encontradas,
a rota não será executada. Por exemplo, se você precisa de uma rota com um segundo segmento que deve ser um ano de 4 dígitos,
você pode forçar essa condição dessa forma:

    <?php
    $app = new \Slim\Slim();
    $app->get('/archive/:year', function ($year) {
        echo "You are viewing archives from $year";
    })->conditions(array('year' => '(19|20)\d\d'));

Invoque o método `conditions()` do objeto Route. O primeiro e único parâmetro é um array associativo com chaves
que combinam qualquer parâmetro da rota e valores que são expressões regulares.

### Condições de rota para todo o aplicativo

Se muitas das rotas da sua aplicação Slim aceitam os mesmos parâmetros e usam as mesmas condições, você pode definir
condições de rotas padrão para toda a aplicação:

    <?php
    \Slim\Route::setDefaultConditions(array(
        'firstName' => '[a-zA-Z]{3,}'
    ));

Defina condições de rota para toda a aplicação antes de você definir rotas da aplicação. Quando você define uma rota,
a rota automaticamente será atribuída para qualquer condição geral de rota definida com `\Slim\Route::setDefaultConditions()`.
Se por qualquer razão você precisa obter as condições padrão de rota para toda a aplicação, você pode obtêr-las com
`\Slim\Route::getDefaultConditions()`. Esse método estatico retorna um array das condições padrões de rota que foram definidas.

Você pode sobescrever a condição padrão de rota, redefinindo a condição quando você define a rota, dessa forma:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:firstName', $callable)
        ->conditions(array('firstName' => '[a-z]{10,}'));

Você pode somar novas condições para uma certa rota dessa forma:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:firstName/:lastName', $callable)
        ->conditions(array('lastName' => '[a-z]{10,}'));
