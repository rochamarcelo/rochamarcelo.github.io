---
layout: post
title:  Ler E-mails com PHP
date:   2015-11-21
description: Todo mundo sabe como enviar e-mails usando PHP mas e ler e-mails, você sabe? Neste post mostrarei como.
---

Umas das tarefas mais comuns em uma aplicação é o envio de e-mails, pode ser um e-mail de confirmação de cadastro,
de aviso de uma promoção, de alteração de cadastro, são diversos os motivos, mas e se ao invez de enviar um e-mail
for necessário ler um e-mail? neste post mostrarei como ler e-mails usando PHP.

### Instação de dependências 

- Primeiramente devemos garantir que temos a extensão imap instalada, no ubuntu podemos instalar assim:
  
  ```
  sudo apt-get install php5-imap
  ```

- Obter composer em https://getcomposer.org/download/
  ```
  curl -sS https://getcomposer.org/installer | php
  ```

### Instalando lib para ler e-mails

Para facilitar a consulta de e-mails criei uma lib. Instale com o composer:

  ```
   php composer.phar require rochasmarcelo/emailmd:dev-master --prefer-dist
  ```
### Lendo e-mails
No exemplo abaixo, vamos obter as últimas mensagens recebidas hoje (dia de execução do script).

Crie o arquivo "receber_emails.php" e copie o código abaixo:

{% highlight php %} 
<?php
    require_once 'vendor/autoload.php';
    //Gmail
    $MailBox = EmailMD\MailBoxFactory::gmail(
        'yourusername@gmail.com',
        'yourpassword'
    );

    $MailBox->reverse();//Recentes primeiro
    $MailBox->filterSince(new DateTime());//Apenas recebidos hoje
    //Get messages
    foreach ( $MailBox as $messageNumber => $message ) {
        echo 'Message number: ' . $messageNumber . PHP_EOL;
        echo $message->getSubject() . PHP_EOL;
        echo $message->getBody() . PHP_EOL;
    }
?>
{% endhighlight %}

### Mais opções
Confira a documentação da lib EmailMD em https://github.com/rochamarcelo/EmailMD
