---
title: Configurações da Aplicação
status: live
---

### modo

Este é um identificador para a operação do modo atual da aplicação. O modo não afeta uma funcionalidade interna da 
aplicação Slim. Em vez disso, o modo é apenas para você opcionalmente, invocar seu próprio código para um modo dado
com o método `configMode()`.

O modo da aplicação é declarado durante a instanciação, seja como uma variável de evento ou como um parâmetro para o
construtor da aplicação Slim. Isso não pode ser mudado depois. O modo pode ser qualquer coisa que você queira, 
os mais típicos são - "development", "test", e "production", mas você está livre para usar qualquer que você queira 
(ex: "foo").

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
passando como primeiro e único parâmetro do seu manipulador a exceção não capturada.

    <?php
    $app = new \Slim\Slim(array(
        'debug' => true
    ));

Tipo de dados
: boolean

Valor padrão
: true

### log.writer

Use um escritor de log customizado para direcionar mensagens de log para apropriados destinos de saída. Por padrão, o log
do Slim escreverá mensagens para `STDERR`. Se você usa um escritor de log customizado, seu log deve implementar esta interface:

    public write(mixed $message, int $level);

O método `write()` é responsável por enviar a mensagem de log (não necessariamente uma string) para um apropriado destino
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

A configuração `log.level` determina quais mensagens de log serão honradas e quais serão ignoradas.
Por exemplo, se a configuração `top.level` é `\Slim\Log::INFO`, mensagens de debug serão ignoradas enquanto
info, warn, error e fatal messages serão honradas.

Para mudar esta configuração após instanciação, você deve acessar o logger do Slim diretamente usando o método `setLevel()`.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'log.level' => \Slim\Log::DEBUG
    ));
    // After instantiation
    $log = $app->getLog();
    $log->setLevel(\Slim\Log::WARN);

Tipo de dados
: integer

Valor padrão
: \Slim\Log::DEBUG

### log.enabled

Este habilita ou desabilita o logger do Slim. Para mudar esta configuração após instanciação, você precisa acessar o logger
do Slim diretamente e usar o método `setEnabled()`.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'log.enabled' => true
    ));
    // After instantiation
    $log = $app->getLog();
    $log->setEnabled(true);

Tipo de dados
: boolean

Valor padrão
: true

### templates.path

O caminho relativo ou absoluto para o diretório de sistema de arquivos que contém os arquivos de template da sua aplicação
Slim. Este caminho é referenciado pela View do Slim para obter e renderizar templates.

Para mudar esta configuração após instanciação, você precisa acessar a view do Slim 
diretamente e usar o método `setTemplatesDirectory()`

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'templates.path' => './templates'
    ));
    // After instantiation
    $view = $app->view();
    $view->setTemplatesDirectory('./templates');

Tipo de dados
: string

Valor padrão
: "./templates"

### view

A classe View ou instância usada pela aplicação Slim. Para mudar esta configuração após instanciação, você precisa
usar o método `view()` do Slim.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'view' => new \My\View()
    ));
    // After instantiation
    $app->view(new \My\View());

Tipo de dados
: string|\Slim\View

Valor padrão
: \Slim\View

### cookies.lifetime

Determina o tempo de vida dos cookies HTTP criados pela aplicação Slim. Se for um inteiro, deverá ter um
UNIX timestamp válido para a expiração do cookie. Se isso for uma string, será validada pela função `strtotime()` para extrapolar
um UNIX timestamp válido para a expiração do cookie.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.lifetime' => '20 minutes'
    ));
    // After instantiation
    $app->config('cookies.lifetime', '20 minutes');

Tipo de dados
: integer|string

Valor padrão
: "20 minutes"

### cookies.path

Determina o caminho padrão para os cookies HTTP se nada for especificado quando invocado os métodos `setCookie()`
ou `setEncryptedCookie()` da aplicação Slim.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.path' => '/'
    ));
    // After instantiation
    $app->config('cookies.lifetime', '/');

Tipo de dados
: string

Valor padrão
: "/"

### cookies.domain

Determina o domínio padrão para os cookies HTTP se nada for especificado quando invocado os métodos `setCookie()` ou
`setEncryptedCookie()` da aplicação Slim.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.domain' => 'domain.com'
    ));
    // After instantiation
    $app->config('cookies.domain', 'domain.com');

Tipo de dados
: string

Valor padrão
: null

### cookies.secure

Determina ou não, se cookies são entregues apenas por HTTPS. Você pode sobrescrever esta configuração quando invoca
os métodos `setCookie()` ou `setEncryptedCookie()` da aplicação Slim.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.secure' => false
    ));
    // After instantiation
    $app->config('cookies.secure', false);

Tipo de dados
: boolean

Valor padrão
: false

### cookies.httponly

Determina ou não, se cookies são entregues apenas pelo protocolo HTTP. Você pode sobrescrever esta configuração quando
invoca os métodos `setCookie()` ou `setEncryptedCookie()` da aplicação Slim.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.httponly' => false
    ));
    // After instantiation
    $app->config('cookies.httponly', false);

Tipo de dados
: boolean

Valor padrão
: false

### cookies.secret_key

A chave secreta usada para criptografia de cookie. Você deve (aconselhável) mudar esta configuração se você usa
cookies HTTP criptografos em sua aplicação Slim.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.secret_key' => 'secret'
    ));
    // After instantiation
    $app->config('cookies.secret_key', 'secret');

Tipo de dados
: string

Valor padrão
: "CHANGE_ME"

### cookies.cipher

O criptograma mcrypt usado para criptografia de cookie HTTP. Veja [criptograma disponíveis](http://php.net/manual/en/mcrypt.ciphers.php).

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.cipher' => MCRYPT_RIJNDAEL_256
    ));
    // After instantiation
    $app->config('cookies.cipher', MCRYPT_RIJNDAEL_256);

Tipo de dados
: integer

Valor padrão
: MCRYPT_RIJNDAEL_256

### cookies.cipher_mode

O modo do criptograma do mcrypt usado para criptografia de cookie HTTP. Veja [modos de criptograma disponíveis](http://php.net/manual/en/mcrypt.ciphers.php).

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'cookies.cipher_mode' => MCRYPT_MODE_CBC
    ));
    // After instantiation
    $app->config('cookies.cipher_mode', MCRYPT_MODE_CBC);

Tipo de dados
: integer

Valor padrão
: MCRYPT_MODE_CBC

### http.version

Por padrão, Slim retorna uma resposta HTTP/1.1 para o cliente. Use esta configuração se você precisa retornar 
uma resposta HTTP/1.0. Isto é útil se você use PHPFrog ou uma configuração de servidor nginx onde você se comunica
com backend e proxies ao invés de cliente HTTP diretamente.

    <?php
    // During instantiation
    $app = new \Slim\Slim(array(
        'http.version' => '1.1'
    ));
    // After instantiation
    $app->config('http.version', '1.1');

Tipo de dados
: string

Valor padrão
: "1.1"
