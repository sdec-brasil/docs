---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introdução

SDEC é um sistema distribuído 

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">É possível autorizar mais de um endereço público para a emissão de notas em nome da empresa, mas cada um deles deve ser único à ela.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete


# SDEC Blockchain

A SDEC Blockchain é uma blockchain permissionada. Isso quer dizer que, todos podem conectar, verificar e auditar as informações públicas, mas a construção do consenso é reservada à participantes selecionados. Nesse caso, esses participantes são as Juntas Comerciais de cada Estado, Banco do Brasil e eventuais órgãos governamentais.

## Eventos:

A Blockchain funciona como um registro universal de eventos que aconteceram e suas ordens. Para se ter o "estado" do sistema é necessário computar toda a história dele até o bloco mais recente.

Se você é familiarizado com a arquitetura Redux, é possível pensarmos nesses eventos como ações ao estado (computado) atual da Blockchain naquele ponto por dispatchers fora da rede.

Os eventos funcionam a partir de publicações.

## Publicações:

Publicações são.

## Novo Registro de Empresa:

O registro da empresa deve ser feita pela Junta Comercial responsável. Além da publicação das informações na Blockchain, a Junta também estará autorizando os endereços respectivos a serem emissores de nota.

<aside class="notice">É possível autorizar mais de um endereço público para a emissão de notas em nome da empresa, mas recomendamos que cada um deles seja único à ela e não seja reutilizado.</aside>

Parâmetro | Exigido | Descrição                                           | Tam. |
--------- | ------- | -------------------------------------               | ---- |
razao     |    S    | Razão Social do prestador do serviço                | 150  |
fantasia  |    N    | Nome Fantasia do prestador do serviço               |  60  |


> Exemplo de Registro de Empresa:

```json
{
  "razao": "ACME Demolições LTDA",
  "fantasia": "Indústrias ACME",
  "cnpj": "97.163.041/0001-30",
  "logEnd": "Rua do Desfiladeiro",
  "numEnd": "1",
  "compEnd": "Perto da Rocha",
  "bairroEnd": "Zona Centro",
  "cidadeEnd": "5100250",
  "estadoEnd": "MT",
  "cepEnd": "78580-000",
  "email": "acme@boom.pow",
  "tel": "65 3313-4100",
  "enderecosEmissores": ["1Bw41hdEenVKdNdYN22r7Kc47qVPkSeie1"], 
}
```

> Se lembre que a publicação de JSON's necessita de um objeto com somente a chave `json` que mapeia para seu objeto. Exemplo de JSON válido para publicação: `{ json: {a: 1, b: "2"} }`.

## Alterações no Registro da Empresa:

## Emissão de Notas Fiscais:
