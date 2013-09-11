---
title: Resumo de Configuração
status: live
---

Existem duas formas de aplicar configurações em uma aplicação Slim. A primeira durante a instanciação da aplicação Slim
e a segunda após a instanciação. Todas as configurações podem ser aplicadas no momento da instanciação passando um array
associativo no construtor do objeto Slim. Todas as configurações podem ser retornadas e modificadas após a instanciação,
no entanto algumas delas não podem ser feitas simplesmente usando o método *config* da aplicação, mas isso será demonstrado
quando for necessário logo abaixo. Antes de eu listar as configurações disponíveis, quero rapidamente explicar como você
pode definir e inspecionar configurações com sua aplicação Slim.

### Durante Instanciação

Para definir configurações na instanciação, passe um array associativo no construtor do Slim.

    <?php
    $app = new Slim(array(
        'debug' => true
    ));

### Após Instanciação

Para definir configurações após instanciação, a maioria das configurações podem usar o método *config* da aplicação;
O primeiro parâmetro é o nome da configuração e o segundo parâmetro é o valor da configuração.

    <?php
    $app->config('debug', false);

Você pode também definir múltiplas configurações de uma vez usando um array associativo:

    <?php
    $app->config(array(
        'debug' => true,
        'templates.path' => '../templates'
    ));

Para retornar o valor de uma configuração, você pode também usar o método *config* da aplicação; no entanto, você apenas
passa um parâmetro - o nome da configuração que você deseja inspecionar. Se a configuração que você requer não existe,
`null` é retornado.

    <?php
    $settingValue = $app->config('templates.path'); //returns "../templates"

Você não está limitado as configurações mostradas acima; você pode também definir as suas próprias.
