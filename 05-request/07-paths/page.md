---
title: Paths de Requisição
status: live
---

Toda requisição HTTP recebida pelo Slim terá uma raiz e um recurso URI.

### URI Raiz

A **raiz URI** é o caminho físico da URL do diretório no qual a aplicação Slim é instanciada e executada.
Se uma aplicação Slim é instanciada no **index.php** dentro do diretório topo na raiz do documento do host virtual,
a URI raiz será uma string vazia. Se uma aplicação Slim é instanciada e executada no **index.php** dentro do subdiretório
físico do documento raiz do host virtual, a URI raiz será um caminho para esse subdiretório com uma barra no inicio e sem
uma barra no final.

### Recurso URI

O **recurso URI** é o caminho da URI virtual de um recurso de uma aplicação. O recurso URI será combinado com as rotas
da aplicação Slim.

Presuma que a aplicação Slim está instalada em um subdiretório físicio **/foo** por baixo da raiz do documento do seu
host virtual. Presuma também a URL completa da requisição HTTP (o que você veria no navegador na barra de endereço) é  **/foo/books/1**. 
A URI raiz é **/foo** (o caminho do diretório físico no qual o Slim é instanciado) e o recurso URI é **/books/1** (o caminho para o recurso da aplicação).

Você pode obter a raiz e o recurso de uma URI com os métodos `getRootUri()` e `getResourceUri()`:

    <?php
    $app = new Slim();

    // Obter objeto de requisição
    $req = $app->request();

    //Obter URI raiz
    $rootUri = $req->getRootUri();

    //Obter recurso URI
    $resourceUri = $req->getResourceUri();
