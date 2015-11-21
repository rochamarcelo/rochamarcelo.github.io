---
layout: post
title:  Criando formulários funcionais sem PHP ou Javascript
date:   2015-11-20
description: Você já criou algum site estático e precisou incluir um formulário de contato funcional, neste post mostrarei como criar um formulário funcional em uma página estática sem utilizar PHP e Javascript.
---

Você já criou algum site estático e em um determinado momento o seu cliente solicitou para incluir um formulário de contato ou talvez no servidor do cliente não tem e não pode instalar PHP, ou talvez você está usando jekyll? Eu já passei por isso algumas vezes, para nossa felicidade existe o FORMSPREE, neste post mostrarei como criar um formulário funcional em uma página estática sem utilizar PHP e Javascript.

### O que é FORMSPREE

É um serviço que permite enviar e-mails a partir de um formulário HTML. 

### Crie o seu formulário

Primeiramente crie o seu formulário contendo os campos name, _replyTo, e message. O campo _replyTo é usado pelo FORMSPREE como Reply-To do e-mail, desta forma, você pode responder diretamente para a pessoa que preencheu o formulário.

{{ "{% highlight html linenos "}}%}
<form method="POST">
    <label>Nome</label>
    <input type="text" name="name" placeholder="Nome" required>
    <br />
    <label>E-mail</label>
    <input type="email" name="_replyto" placeholder="E-mail" required>
    <br />
    <label>Mensagem</label>
    <textarea rows="5" name="message" placeholder="Mensagem" required></textarea>
    <br />
    <input type="submit" value="Enviar" />
</form>
{{ "{% endhighlight "}}%}

### Enviando formulário ao FORMSPREE

Agora que você já criou o seu formulário,  altere o atributo action do seu formulario para "//formspree.io/voce@seudominio.com.br” sendo que “voce@seudominio.com.br” é o endereço de email que você deseja receber as mensagens.

```html 
<form  action="//formspree.io/voce@seudominio.com.br" method="POST">….
</form>
```

### Definindo Assunto

Para facilitar a identificação de mensagens recebidas do seu formulário é recomendado definir um assunto, podemos fazer isso incluindo um input hidden “_subject” como no exemplo:

```html 
<input type="hidden"  name="_subject" value="Contato pelo site!">
```

### Definindo URL de agradecimento

O FORMSPREE mostra uma página de agradecimento padrão quando o usuário envia o formulário, recomendo definir uma URL para uma página de agradecimento sua, para isso incluimos um input hidden “_next” contendo a URL.

```html 
<input type="hidden" name="_next" value="//seudominio.com.br/obrigado.html" />
```

### Evitando spam

Para evitar o recebimento de spam no seu e-mail, inclua o input text “_gotcha” mas deixe oculto via CSS.  O FORMSPREE ira ignorar qualquer envio em que for informado um valor para o input “_gotcha”.

```
 <input type="text" name="_gotcha" style="display:none" />
```

### Versão final do formulário:

```html 
<form  action="//formspree.io/voce@seudominio.com.br" method="POST">
```

Agora voc

```html 
<form  action="//formspree.io/voce@seudominio.com.br" method="POST">
    <label>Nome</label>
    <input type="text" name="name" placeholder="Nome" required>
    <br />
    <label>E-mail</label>
    <input type="email" name="email" placeholder="E-mail" required>
    <br />


    <input type="hidden"  name="_subject" value="Contato pelo site!">
    <input type="hidden" name="_next" value="//seudominio.com.br/obrigado.html" />
    <input type="text" name="_gotcha" style="display:none" />
    <label>Mensagem</label>
    <textarea rows="5" name="message" placeholder="Mensagem" required></textarea>
    <br />
    <input type="submit" value="Enviar" />
</form>
```

### Finalizar

Para finalizar você precisa testar um envio do formulário e confirmar o e-mail que recebe as mensagens. Acesse a URL do seu formulário, preencha as informações e envie o formulário. O FORMSPREE enviará um e-mail para você confirmar o e-mail, clique no link de confirmação e pronto o seu formulário está funcional.
