---
title: Installation
status: live
---

### Instalação pelo Composer

Instale o composer em seu projeto:

    curl -s https://getcomposer.org/installer | php

Crie um arquivo `composer.json` na raiz do seu projeto:

    {
        "require": {
            "slim/slim": "2.*"
        }
    }

Instale via composer:

    php composer.phar install

Adicione esta linha no arquivo `index.php` da sua aplicação:

    <?php
    require 'vendor/autoload.php';

### Instalação manual

Baixe e extraia o Slim Framework no diretório do seu projeto e use `require` no arquivo `index.php` da sua aplicação.
Você também precisará registrar o autoloader do Slim.

    <?php
    require 'Slim/Slim.php';
    \Slim\Slim::registerAutoloader();
