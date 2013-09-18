---
title: Parâmetros de Rota
status: live
---

Você pode embutir parâmetros em URIs de rotas. Nesse exemplo, eu tenho dois parâmetros em minha URI da rota, ":one"
e ":two":

    <?php
    $app = new \Slim\Slim();
    $app->get('/books/:one/:two', function ($one, $two) {
        echo "O primeiro parâmetro é " . $one;
        echo "O segundo parâmetro é " . $two;
    });

Para criar um parâmetro para a URL, coloque no inicio do nome do parâmetro ":". Quando a rota combina a atual requisição
HTTP, os valores para cada parâmetro da rota são extraidos da URI da requisição HTTP e passados para a função callback
associada na ordem que aparecem.

### Parâmetros Wildcard

Você pode também usar parâmetros do tipo wildcard. Esses parâmetros capturarão um ou muitos segmentos da URI 
que correspondam para o parâmtro wildcard em um array. Um parâmetro wildcard é identificado por um "+" como sufixo do
parâmetro; isso caso contrário, age da mesma forma como um parâmetro normal de rota. Aqui está um exemplo:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:name+', function ($name) {
        // Faça alguma coisa
    });

Quando você invoca este exemplo com uma URI "/hello/Josh/T/Lockhard", o parâmetro `$name` no callback da rota
será igual a `array('Josh', 'T', 'Lockhart')`.

### Parâmetros opcionais de rota

<div class="alert alert-warning">
    <strong>Se liga!</strong> Segmentos opcionais de rota são experimental. Eles devem apenas ser usados
    da maneira demonstrada abaixo.
</div>

Você pode também ter parâmetros opcionais em suas rotas. Esses parâmetros são ideais para uma rota de arquivo de blog.
Para declarar parâmetros opcionais, especifique o padrão da rota dessa forma:

    <?php
    $app = new Slim();
    $app->get('/archive(/:year(/:month(/:day)))', function ($year = 2010, $month = 12, $day = 05) {
        echo sprintf('%s-%s-%s', $year, $month, $day);
    });

Cada segmento de rota subsequente é opcional. Esta rota aceitará requisições HTTP para:

* /archive
* /archive/2010
* /archive/2010/12
* /archive/2010/12/05

Se um segmento opcional de rota é omitido da requisição HTTP, o valores padrões na assinatura do callback são usados.

Atualmente, você pode apenas usar segmentos opcionais de rota em situações como a do exemplo acima onde cada segmento
de rota é subsequentemente opcional. Você pode encontrar está funcionalidade instável quando usado em cenários diferentes
do exemplo acima.
