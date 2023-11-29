
O **cross-site scripting** refletido ou **XSS** surge quando uma aplicação recebe dados num pedido HTTP e inclui esses dados na resposta imediata de uma forma insegura.

Suponhamos que um site Web tem uma função de pesquisa que recebe o termo de pesquisa fornecido pelo utilizador num parâmetro URL:

```https
https://insecure-website.com/search?term=gift
```

A aplicação faz eco do termo de pesquisa fornecido na resposta a este URL:

```html
<p>You searched for: gift</p>
```

Assumindo que a aplicação não efetua qualquer outro processamento dos dados, um atacante pode construir um ataque como este:

``` html
https://insecure-website.com/search?term=<script>/*+Bad+stuff+here...+*/</script>
```

Este URL resulta na resposta seguinte:

```html
<p>You searched for: <script>/* Bad stuff here... */</script></p>
```

Se outro utilizador da aplicação pedir o URL do atacante, o script fornecido pelo atacante será executado no browser do utilizador vítima, no contexto da sua sessão com a aplicação.

## XSS entre tags HTML

Quando o contexto XSS é o texto entre as tags HTML, você precisa introduzir algumas novas tags HTML projetadas para acionar a execução do JavaScript.

Algumas formas úteis de execução de JavaScript são:
```html
<script>alert(document.domain)</script> 

<img src=1 onerror=alert(1)>
```

