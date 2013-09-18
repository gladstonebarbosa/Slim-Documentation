---
title: Middleware de Rota
status: live
---

Slim permite você associar middlewares em uma rota especifica da aplicação. Quando a rota combina com a requisição HTTP
atual e é invocada, o Slim primeiro invocará os middlewares associados na ordem em que foram definidos.

### O que é middleware de rota?

Middleware de rota é qualquer coisa que retorne `true` para a função `is_callable()`. Middlewares serão invocados
na sequência que foram definidos antes da execução da função callback da rota.

### Como eu adiciono um middleware?

Quando você define uma nova rota com os métodos `get()`, `post()`, `put()`, ou `delete()` do Slim, você deve definir
o padrão da rota e uma função chamável para ser invocada quando a rota combinar com uma requisição HTTP.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () {
        //Faça alguma coisa
    });

No exemplo acima, o primeiro parâmetro é o padrão da rota. O último parâmetro é a função chamável para ser invocada
quando a rota combina com uma requisição HTTP. O padrão da rota deve sempre ser o primeiro parâmetro. A função chamável
da rota deve sempre ser o último parâmetro.

Você pode atribuir middlewares para esta rota passando cada middleware como um parâmetro string separados por vírgula:

    <?php
    function mw1() {
        echo "Isso é um middleware!";
    }
    function mw2() {
        echo "Isso é um middleware!";
    }
    $app = new \Slim\Slim();
    $app->get('/foo', 'mw1', 'mw2', function () {
        //Faça alguma coisa
    });

Quando a rota /foo é invocada, as funções `mw1` e `mw2` serão invocadas na sequência antes que a função de callback
da rota seja executada.

Suponha que você queira autenticar um determinado papel do usuário em uma rota especifica. Você poderia usar algumas 
closures mágicas desta forma:

    <?php
    // Autentica o usuário para determinado papel
    $authenticateForRole = function ( $role = 'member' ) {
        return function () use ( $role ) {
            $user = User::fetchFromDatabaseSomehow();
            if ( $user->belongsToRole($role) === false ) {
                $app = \Slim\Slim::getInstance();
                $app->flash('error', 'Login required');
                $app->redirect('/login');
            }
        };
    };
    $app = new \Slim\Slim();
    $app->get('/foo', $authenticateForRole('admin'), function () {
        //Exibe painel de controle do admin
    });

### Quais parâmetros são passados em cada middleware de rota?

Cada middleware é invocado com um parâmetro, a rota atualmente combinada `\Slim\Route`.

    <?php
    $aBitOfInfo = function (\Slim\Route $route) {
        echo "Rota atual é " . $route->getName();
    };
    $app->get('/foo', $aBitOfInfo, function () {
        echo "foo";
    });
