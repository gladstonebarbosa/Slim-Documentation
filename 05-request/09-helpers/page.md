---
title: Helpers de Requisição
status: live
---

O objeto de requisição do Slim prover vários métodos "helper" para obter informações HTTP comuns:

### Content Type

Obtém o tipo de conteúdo da requisição (ex: "application/json;charset=utf-8"):

    <?php
    $req = $app->request();
    $req->getContentType();

### Tipo de Mídia

Obtém o tipo de mídia da requisição (ex: "application/json"):

    <?php
    $req = $app->request();
    $req->getMediaType();

### Parâmetros do Tipo da Mídia

Obtém os parâmetrs do tipo de mídia (ex: [charset => "utf-8"]):

    <?php
    $req = $app->request();
    $req->getMediaTypeParams();

### Charset do conteúdo

Obtém o conjunto de caracteres do conteúdo da requisição (ex: "utf-8"):

    <?php
    $req = $app->request();
    $req->getContentCharset();

### Tamanho do Conteúdo

Obtém o tamanho do conteúdo da requisição:

    <?php
    $req = $app->request();
    $req->getContentLength();

### Host

Obtém o host da requisição (ex: "slimframework.com"):

    <?php
    $req = $app->request();
    $req->getHost();

### Host com Porta

Obtém o host com a porta da requisição (ex: "slimframework.com:80"):

    <?php
    $req = $app->request();
    $req->getHostWithPort();

### Porta

Obtém a porta da requisição (ex: 80):

    <?php
    $req = $app->request();
    $req->getPort();

### Esquema

Obtém o esquema da requisição (ex: "http" or "https"):

    <?php
    $req = $app->request();
    $req->getScheme();

### Caminho

Obtém o caminho da requisição (URI raiz + recurso da URI):

    <?php
    $req = $app->request();
    $req->getPath();

### URL

Obtém a URL da requisição (esquema + host [ + port se não padrão ]):

    <?php
    $req = $app->request();
    $req->getUrl();

### Endereço IP

Obtém o endereço IP da requisição:

    <?php
    $req = $app->request();
    $req->getIp();

### Referer

Referer o referrer da requisição:

    <?php
    $req = $app->request();
    $req->getReferrer();

### Agente de usuário

Obtém o agente de usuário da requisição:

    <?php
    $req = $app->request();
    $req->getUserAgent();
