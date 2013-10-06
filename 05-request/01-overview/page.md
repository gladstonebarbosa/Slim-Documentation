---
title: Request Overview
status: live
---
Cada instancia da aplicação Slim tem um objeto de requisição. O objeto de requisição é uma abstração da requisição HTTP
atual e permite você facilmente interagir com as variáveis de ambiente da aplicação Slim. Embora cada
aplicação Slim inclua um objeto de requisição padrão, a classe `\Slim\Http\Request` é independente; você pode
instanciar a classe
Each Slim application instance has one request object. The request object is an abstraction of the current
HTTP request and allows you to easily interact with the Slim application's environment variables. Although each
Slim application includes a default request object, the `\Slim\Http\Request` class is idempotent; você pode instanciar 
a classe à vontade (no middleware ou em outro lugar na sua aplicação Slim) sem afetar a aplicação como um todo.
Você pode obter uma referencia para o objeto da aplicação Slim dessa forma:

    <?php
    // Retorna instancia de \Slim\Http\Request
    $request = $app->request();
