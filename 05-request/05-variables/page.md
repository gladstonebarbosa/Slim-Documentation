---
title: Variáveis da Requisição
status: live
---

Uma requisição HTTP pode ter variáveis associadas (não fique confuso com variáveis de rota). As variáveis
GET, POST, ou PUT enviadas com a requisição HTTP atual são expostas pelo objeto de requisição do Slim.

Se você quer rapidamente obter um valor de uma variável sem considerar seu tipo, use o método `params()` do objeto de 
requisição:

    <?php
    $req = $app->request();
    $paramValue = $req->params('paramName');

O método `params()` irá primeiro procurar váriaveis PUT, então POST, e por último GET. Se nenhuma variável é encontrada.
`null` é retornado. Se você quer apenas procurar por um especifico tipo de variável, você pode usar esses métodos:

    <?php
    // Obtem o objeto de requisição
    $req = $app->request();

    //variável GET
    $paramValue = $req->get('paramName');

    //variável POST
    $paramValue = $req->post('paramName');

    //variável PUT
    $paramValue = $req->put('paramName');

Se uma variável não existe, cada método acima retornará `null`. Você pode também invocar qual uma dessas funções
sem qualquer parâmetro para obter um array de todas as variáveis de determinado tipo:

    <?php
    $req = $app->request();
    $allGetVars = $req->get();
    $allPostVars = $req->post();
    $allPutVars = $req->put();
