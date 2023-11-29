---
tags:
  - Pentest
  - WEB
---
## Como detectar vulnerabilidades de injeção de SQL

Você pode detectar a injeção de SQL manualmente usando um conjunto sistemático de testes em todos os pontos de entrada do aplicativo. Para fazer isso, você normalmente envia:

- O caractere de cotação única `'` e procure erros ou outras anomalias.
- Alguma sintaxe específica do SQL que é avaliada para o valor base ( original ) do ponto de entrada e para um valor diferente, e procura diferenças sistemáticas nas respostas do aplicativo.
- Condições booleanas, como `OR 1=1` e `OR 1=2`, e procure diferenças nas respostas do aplicativo.
- Cargas úteis projetadas para acionar atrasos de tempo quando executadas em uma consulta SQL e procurar diferenças no tempo necessário para responder.
- [ORIENTAL](https://portswigger.net/burp/application-security-testing/oast) cargas úteis projetadas para acionar uma interação de rede fora de banda quando executadas em uma consulta SQL e monitorar quaisquer interações resultantes.

## Injeção de SQL em diferentes partes da consulta

A maioria das vulnerabilidades de injeção de SQL ocorre dentro do `WHERE` cláusula de `SELECT` consulta. Os testadores mais experientes estão familiarizados com esse tipo de injeção de SQL.

No entanto, vulnerabilidades de injeção de SQL podem ocorrer em qualquer local da consulta e dentro de diferentes tipos de consulta. Alguns outros locais comuns onde a injeção de SQL surge são:

- No `UPDATE` instruções, dentro dos valores atualizados ou `WHERE` cláusula.
- No `INSERT` instruções, dentro dos valores inseridos.
- No `SELECT` instruções, dentro do nome da tabela ou coluna.
- No `SELECT` declarações, dentro do `ORDER BY` cláusula.

## Exemplos de injeção SQL
Existem muitas vulnerabilidades, ataques e técnicas de injeção de SQL que ocorrem em diferentes situações. Alguns exemplos comuns de injeção de SQL incluem:

- [Recuperando dados ocultos](https://portswigger.net/web-security/sql-injection#retrieving-hidden-data), onde você pode modificar uma consulta SQL para retornar resultados adicionais.
- [Subvertendo a lógica do aplicativo](https://portswigger.net/web-security/sql-injection#subverting-application-logic), onde você pode alterar uma consulta para interferir na lógica do aplicativo.
- [Ataques da UNIÃO](https://portswigger.net/web-security/sql-injection/union-attacks), onde você pode recuperar dados de diferentes tabelas de banco de dados.
- [Injeção cega de SQL](https://portswigger.net/web-security/sql-injection/blind), onde os resultados de uma consulta que você controla não são retornados nas respostas do aplicativo.

## Recuperando dados ocultos

Imagine um aplicativo de compras que exibe produtos em diferentes categorias. Quando o usuário clica no **Presentes** categoria, o navegador solicita o URL:

`https://insecure-website.com/products?category=Gifts`

Isso faz com que o aplicativo faça uma consulta SQL para recuperar detalhes dos produtos relevantes do banco de dados:

`SELECT * FROM products WHERE category = 'Gifts' AND released = 1`

Esta consulta SQL solicita que o banco de dados retorne:

- todos os detalhes (`*`)
- do `products` mesa
- onde `category` é `Gifts`
- e `released` é `1`.

A restrição `released = 1` está sendo usado para ocultar produtos que não são liberados. Poderíamos assumir produtos não lançados, `released = 0`.

O aplicativo não implementa nenhuma defesa contra ataques de injeção de SQL. Isso significa que um invasor pode construir o seguinte ataque, por exemplo:

`https://insecure-website.com/products?category=Gifts'--`

Isso resulta na consulta SQL:

`SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1`

Fundamentalmente, observe que `--` é um indicador de comentário no SQL. Isso significa que o restante da consulta é interpretado como um comentário, removendo-o efetivamente. Neste exemplo, isso significa que a consulta não inclui mais `AND released = 1`. Como resultado, todos os produtos são exibidos, incluindo aqueles que ainda não foram lançados.

Você pode usar um ataque semelhante para fazer com que o aplicativo exiba todos os produtos em qualquer categoria, incluindo categorias que eles não conhecem:

`https://insecure-website.com/products?category=Gifts'+OR+1=1--`

Isso resulta na consulta SQL:

`SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1`

A consulta modificada retorna todos os itens em que `category` é `Gifts`, ou `1` é igual a `1`. Como `1=1` é sempre verdade, a consulta retorna todos os itens.