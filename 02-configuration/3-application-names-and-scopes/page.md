---
title: Nomes e Escopos da Aplicação
status: live
---

Quando você construir uma aplicação Slim, você entrará vários escopos em seu código (ex: escopo global e escopo de função).
Você provavelmente precisará de uma referência para sua aplicação Slim em cada escopo. Existem várias maneiras de fazer isso:

* Use nomes de aplicação com o método estatico `getInstance()` do Slim
* Passe a instancia da aplicação para dentro do escopo da função com a palavra chave `use`

### Nomes da Aplicação

Toda aplicação do Slim pode receber um nome. **This is optional**. Nomes ajudam você a obter uma referência
para a instacia da aplicação Slim em qualquer escopo em torno do seu código. Aqui é como você atribue e obtem um nome de aplicação:

    <?php
    $app = new \Slim\Slim();
    $app->setName('foo');
    $name = $app->getName(); // "foo"

### Resolução de Escopo

Então, como você obtem uma referência para sua aplicação Slim? O exemplo abaixo, demonstra como obter uma referência
para a aplicação Slim dentro de uma função de callback de uma rota. A variável `$app` é usada no escopo global para
definir a rota HTTP GET. Mas a variável `$app` é também necessária dentro do escopo do callback da rota para renderizar
um template.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () {
        $app->render('foo.php'); // <-- ERROR
    });

Este exemplo falha porque a variável `$app` é indisponível dentro da função de callback da rota.

#### Currying

Podemos injetar a variável `$app` dentro da função de callback com a palavra chave `use`:

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () use ($app) {
        $app->render('foo.php'); // <-- SUCCESS
    });

#### Capturar através de nome

Você pode usar também o método estatico `getInstance()` do Slim:

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', 'foo');
    function foo() {
        $app = Slim::getInstance();
        $app->render('foo.php');
    }
