---
title: Configurações da Aplicação
status: live
---

### modo

Este é um identificador para a operação do modo atual da aplicação. O modo não afeta uma funcionalidade interna da 
aplicação Slim. Em vez disso, o modo é apenas para você, opcionalmente, invocar seu próprio código para um dado modo
com o método `configMode()`.

O modo da aplicação é declarado durante a instanciação, seja como uma variável de evento ou como um parâmetro para o
construtor da aplicação Slim. Isso não pode ser mudado depois. O modo pode ser qualquer coisa que você queira - "development",
"test", e "production" são típicos, mas você está livre para usar qualquer que você queira (ex: "foo").

    <?php
    $app = new \Slim\Slim(array(
        'mode' => 'development'
    ));

Tipo de dados
: string

Valor padrão
: "development"

### debug

<div class="alert alert-info">
    <strong>Se liga!</strong> Slim converte erros em instâncias `ErrorException`.
</div>

Se o debugging está habilitado, Slim usará seu próprio manipulador de erros para mostrar uma informação de diagnóstico
para exceções não capturadas. Se o debugging está desabilitado, Slim invocará seu manipulador de erros customizado,
//passing it the otherwise uncaught Exception as its first and only argument.//

    <?php
    $app = new \Slim\Slim(array(
        'debug' => true
    ));

Tipo de dados
: boolean

Valor padrão
: true

### log.writer

Use um escritor de log customizado para direcionar mensagens de log para apropriados destinos saídas. Por padrão, o log
do Slim escreverá mensagens para `STDERR`. Se você usa um escritor de log customizado, isso deve implementar esta interface:

    public write(mixed $message, int $level);

O método `write()` é responsável por enviar a mensagem de log (não necessáriamente uma string) para um apropriado destino
de saída (ex: um arquivo de texto, um banco de dados, ou um serviço web remoto).

Para especificar um escritor de log customizado após a instanciação do Slim, você deve acessar o logger do Slim diretamente
e usar o método `setWriter()`:

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'log.writer' => new \My\LogWriter()
    ));
    // After instantiation
    $log = $app->getLog();
    $log->setWriter(new \My\LogWriter());

Tipo de dados
: mixed

Valor padrão
: \Slim\LogWriter

### log.level

<div class="alert alert-info">
    <strong>Se liga!</strong> Use as constantes definidas em `\Slim\Log` em vez de inteiros.
</div>

Slim tem 5 níveis de mensagens de log:

* \Slim\Log::DEBUG
* \Slim\Log::INFO
* \Slim\Log::WARN
* \Slim\Log::ERROR
* \Slim\Log::FATAL

The `log.level` application setting determines which logged messages will be honored and which will be ignored.
For example, if the `log.level` setting is `\Slim\Log::INFO`, debug messages will be ignored while info, warn,
error, and fatal messages will be logged.

To change this setting after instantiation you must access Slim's logger directly and use its `setLevel()` method.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'log.level' => \Slim\Log::DEBUG
    ));

    // After instantiation
    $log = $app->getLog();
    $log->setLevel(\Slim\Log::WARN);

Data Type
: integer

Default Value
: \Slim\Log::DEBUG

### log.enabled

This enables or disables Slim's logger. To change this setting after instantiation you need to access Slim's logger
directly and use its `setEnabled()` method.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'log.enabled' => true
    ));

    // After instantiation
    $log = $app->getLog();
    $log->setEnabled(true);

Data Type
: boolean

Default Value
: true

### templates.path

The relative or absolute path to the filesystem directory that contains your Slim application's template files.
This path is referenced by the Slim application's View to fetch and render templates.

To change this setting after instantiation you need to access Slim's view directly and use its `setTemplatesDirectory()`
method.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'templates.path' => './templates'
    ));

    // After instantiation
    $view = $app->view();
    $view->setTemplatesDirectory('./templates');

Data Type
: string

Default Value
: "./templates"

### view

The View class or instance used by the Slim application. To change this setting after instantiation you need to
use the Slim application's `view()` method.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'view' => new \My\View()
    ));

    // After instantiation
    $app->view(new \My\View());

Data Type
: string|\Slim\View

Default Value
: \Slim\View

### cookies.lifetime

Determines the lifetime of HTTP cookies created by the Slim application. If this is an integer, it must be a valid
UNIX timestamp at which the cookie expires. If this is a string, it is parsed by the `strtotime()` function to extrapolate
a valid UNIX timestamp at which the cookie expires.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.lifetime' => '20 minutes'
    ));

    // After instantiation
    $app->config('cookies.lifetime', '20 minutes');

Data Type
: integer|string

Default Value
: "20 minutes"

### cookies.path

Determines the default HTTP cookie path if none is specified when invoking the Slim application's `setCookie()` or
`setEncryptedCookie()` methods.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.path' => '/'
    ));

    // After instantiation
    $app->config('cookies.lifetime', '/');

Data Type
: string

Default Value
: "/"

### cookies.domain

Determines the default HTTP cookie domain if none specified when invoking the Slim application's `setCookie()` or
`setEncryptedCookie()` methods.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.domain' => 'domain.com'
    ));

    // After instantiation
    $app->config('cookies.domain', 'domain.com');

Data Type
: string

Default Value
: null

### cookies.secure

Determines whether or not cookies are delivered only via HTTPS. You may override this setting when invoking
the Slim application's `setCookie()` or `setEncryptedCookie()` methods.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.secure' => false
    ));

    // After instantiation
    $app->config('cookies.secure', false);

Data Type
: boolean

Default Value
: false

### cookies.httponly

Determines whether or not cookies are delivered only via the HTTP protocol. You may override this setting when invoking
the Slim application's `setCookie()` or `setEncryptedCookie()` methods.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.httponly' => false
    ));

    // After instantiation
    $app->config('cookies.httponly', false);

Data Type
: boolean

Default Value
: false

### cookies.secret_key

The secret key used for cookie encryption. You should change this setting if you use encrypted HTTP cookies
in your Slim application.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.secret_key' => 'secret'
    ));

    // After instantiation
    $app->config('cookies.secret_key', 'secret');

Data Type
: string

Default Value
: "CHANGE_ME"

### cookies.cipher

The mcrypt cipher used for HTTP cookie encryption. See [available ciphers](http://php.net/manual/en/mcrypt.ciphers.php).

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.cipher' => MCRYPT_RIJNDAEL_256
    ));

    // After instantiation
    $app->config('cookies.cipher', MCRYPT_RIJNDAEL_256);

Data Type
: integer

Default Value
: MCRYPT_RIJNDAEL_256

### cookies.cipher_mode

The mcrypt cipher mode used for HTTP cookie encryption. See [available cipher modes](http://php.net/manual/en/mcrypt.ciphers.php).

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.cipher_mode' => MCRYPT_MODE_CBC
    ));

    // After instantiation
    $app->config('cookies.cipher_mode', MCRYPT_MODE_CBC);

Data Type
: integer

Default Value
: MCRYPT_MODE_CBC

### http.version

By default, Slim returns an HTTP/1.1 response to the client. Use this setting if you need to return an HTTP/1.0
response. This is useful if you use PHPFog or an nginx server configuration where you communicate with backend
proxies rather than directly with the HTTP client.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'http.version' => '1.1'
    ));

    // After instantiation
    $app->config('http.version', '1.1');

Data Type
: string

Default Value
: "1.1"
