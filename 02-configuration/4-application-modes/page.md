---
title: Modos da Aplicação
status: live
---

É uma pratica comum executar aplicações web em um especifico modo dependendo do estado atual do projeto.
Se você está desenvolvendo a aplicação, você executará a aplicação no modo "development". Se você está testando
a aplicação, você executará-la no modo "test"; se você lançar a aplicação, você executará-la no modo "production".

Slim suporta o conceito de modos, nisso você pode definir seus próprios modos e incitar o Slim a se preparar
apropriadamente para o modo atual. Por exemplo, você pode querer habilitar o debug no modo "development" mas não
no modo "production". Os exemplos abaixo demonstram como configurar o Slim diferentemente para um dado modo.

### O que é modo?

Tecnicamente, um modo de aplicação é meramente uma string de texto - como "development" ou "production" - que tem
uma função de callback associada, usada para preparar a aplicação Slim apropriadamente. O modo da aplicação pode ser
qualquer coisa como: "testing", "production", "development", ou mesmo "foo".

### Como eu atribuo um modo de aplicação?

<div class="alert alert-info">
    <strong>Se liga!</strong> O modo da aplicação pode ser apenas atribuido durante a instanciação e não pode
    ser mudado depois.
</div>

#### Use uma variável de ambiente

Se o Slim ver uma variável de ambiente chamada "SLIM_MODE", ele atribuirá o modo da aplicação para o valor dessa variável.

    <?php
    $_ENV['SLIM_MODE'] = 'production';

#### Use configuração da aplicação

Se uma variável de ambiente não é encontrada, Slim irá olhar para o modo na configuração da aplicação.

    <?php
    $app = new \Slim\Slim(array(
        'mode' => 'production'
    ));

#### Modo padrão

Se a variável de ambiente e configuração da aplicação não são encontradas, Slim atribuirá o modo da aplicação para "development".

### Configurar para um modo especifico

Após você instanciar a aplicação Slim, você pode configuarar o Slim para um modo especifico com o método `configureMode()`
do Slim. Este método aceita dois parâmetros: o nome do modo desejável e uma função para ser imediatamente invocada
se o primeiro parâmetro combinar com o modo atual da aplicação.

Presuma que o modo atual da aplicação é "production". Apenas a função associada com o modo "production" será invocada.
A função associada com o modo "development" será ignorada até que o modo da aplicação seja mudado para "development".

    <?php
    // Atribue o modo atual
    $app = new \Slim\Slim(array(
        'mode' => 'production'
    ));

    // Only invoked if mode is "production"
    $app->configureMode('production', function () use ($app) {
        $app->config(array(
            'log.enable' => true,
            'debug' => false
        ));
    });

    // Invocado apenas se o modo for "development"
    $app->configureMode('development', function () use ($app) {
        $app->config(array(
            'log.enable' => false,
            'debug' => true
        ));
    });
