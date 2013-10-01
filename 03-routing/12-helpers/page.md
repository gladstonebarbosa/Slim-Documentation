---
title: Route Helpers
status: live
---

Slim prover vários métodos helpers (exposto pela instância da aplicação Slim) que ajudarão você a controlar o fluxo de
sua aplicação.

Por favor esteja ciente que os seguintes métodos helpers `halt()`, `pass()`, `redirect()`, e `stop()` são implementados
usando Exceptions. Cada um lançará uma exceção `\Slim\Exception\Stop` ou `\Slim\Exception\Pass`.
Lançando a Exception nesses casos é uma simples forma de fazer com que o código do usuário pare de processar, fazer
com que o framework tome o controle e imediatamente envie a resposta necessária para o cliente. Este comportamento pode
ser surpresa se não esperado. Dê uma olhada no seguinte código.

    <?php
    $app->get('/', function() use ($app, $obj) {
        try {
            $obj->thisMightThrowException();
            $app->redirect('/success');
        } catch(\Exception $e) {
            $app->flash('error', $e->getMessage());
            $app->redirect('/error');
        }
    });

Se `$obj->thisMightThrowException()` lança uma Exception o código executará como esperado. No entanto, se nenhuma
exceção é lançada a chamada para $app->redirect() lançará uma Exception `\Slim\Exception\Stop` que será capturada pelo
bloco `catch` ao invés do framework estar redirecionando o navegador para a página "/error". Onde possível
em sua própria aplicação, você deve usar Exceptions tipados assim seus blocos `catch` são mais alcançados do que 
engulir todas as Exceptions. Em algumas situações o `thisMightThrowException()` poderá ser uma chamada para um componente
externo que você não controla, o que neste caso, digitando todas as exceções lançadas não possa ser possível.
Para estas instâncias podemos ajustar nosso código rapidamente movendo o `$app->redirect()` após o bloco try/catch para
consertar problemas.
Já que o processo irá parar no redirecionamento de erro este código agora executará como esperado.

    <?php
    $app->get('/', function() use ($app, $obj) {
        try {
            $obj->thisMightThrowException();
        } catch(Exception $e) {
            $app->flash('error', $e->getMessage());
            $app->redirect('/error');
        }
        $app->redirect('/success');
    });

### Halt

O método `halt()` do Slim irá imediatamente retornar uma resposta HTTP com um código de status e corpo.
Este método aceita dois parâmetros: o código de status HTTP e uma mensagem opcional. Slim imediatamente irá parar a aplicação
atual e enviar uma resposta HTTP para o cliente com o status especificado e a mensagem opcional (como corpo da respota).
Isto sobrescreverá o objeto existente `Slim\Http\Response`.

    <?php
    $app = new \Slim\Slim();

    //Envia um resposta de erro 500 padrão
    $app->halt(500);

    //Or if you encounter a Balrog...
    $app->halt(403, 'You shall not pass!');

Se você quer renderizar um template com uma lista de mensagem de erros, você deve usar o método `render()` do Slim.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () use ($app) {
        $errorData = array('error' => 'Permission Denied');
        $app->render('errorTemplate.php', $errorData, 403);
    });
    $app->run();

O método `halt()` pode enviar qualquer tipo de resposta HTTP para o cliente: informacional, sucesso, redirecionamento,
não encontrado, erro de cliente, erro de servidor.

### Pass

Um rota pode dizer ao Slim para continuar para a próxima combinação de rota com o método `pass()`.
Quando este método é invocado, o Slim irá imediatamente parar o processo da rota combinada e invocará a próxima rota combinada.
Se nenhuma combinação subsequente de rota é encontrada, uma resposta **404 Not Found** é enviada para o cliente.
Aqui está um exemplo. Presuma uma requisição HTTP para "GET /hello/Frank".

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/Frank', function () use ($app) {
        echo "Você não verá isso...";
        $app->pass();
    });
    $app->get('/hello/:name', function ($name) use ($app) {
        echo "Mas você verá isso!";
    });
    $app->run();

### Redirect

É facil redirecionar o cliente para outra URL com o método `redirect()` do Slim. Este método aceita
dois parâmetros: o primeiro parâmetro é a URL para a qual o cliente será redirecionado; O segundo parâmetro opcional
é o código de status HTTP. Por padrão o método `redirect()` enviará uma reposta **302 Temporary Redirect**.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () use ($app) {
        $app->redirect('/bar');
    });
    $app->run();

Ou se você deseja usar um redirecionamento permanente, você deve especificar a URL de destino como primeiro parâmetro
e o código HTTP de status como segundo parâmetro.

    <?php
    $app = new \Slim\Slim();
    $app->get('/old', function () use ($app) {
        $app->redirect('/new', 301);
    });
    $app->run();

Este método automaticamente atribuirá o Location: header. A resposta de redirecionamento HTTP será enviada para o 
cliente HTTP imediatamente.

### Stop

O método `stop()` para a aplicação Slim e envia a resposta HTTP atual para o cliente como está.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () use ($app) {
        echo "Você verá isso...";
        $app->stop();
        echo "Mas não isso";
    });
    $app->run();

### URL For

O método `urlFor()` do Slim permite você dinâmicamente criar URLs para uma rota nomeada para que, se uma rota
padrão mudar, a sua URLs vai atualizar automaticamente, sem quebrar a sua aplicação. Este exemplo demonstra
como gerar URLs para uma rota nomeada.

    <?php
    $app = new \Slim\Slim();

    //Create a named route
    $app->get('/hello/:name', function ($name) use ($app) {
        echo "Hello $name";
    })->name('hello');

    //Generate a URL for the named route
    $url = $app->urlFor('hello', array('name' => 'Josh'));

Neste exemplo, $url é "/hello/Josh". Para usar o método `urlFor()`, você deve primeiro atribuiar um nome para a rota.
Em seguida, invocar o método `urlFor()`. O primeiro parâmetro é o nome da rota e o segundo parâmetro é um array associativo
usado para substituir os parâmetros da URL da rota com os valores atuais; As chaves do array deve combinar parâmetros
na URI da rota e os valores serão usados como substituições.
