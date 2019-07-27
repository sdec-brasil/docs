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

*SDEC: Sistema Distribuído de Emissão de Contribuição*

O SDEC foi um sistema criado com a intenção de uniformizar o padrão de notas fiscais de serviços entre os mais de 5500 municípios brasileiros, facilitando a cobrança e o repasse dos tributos provenientes (ISS).

Por ser um sistema público, ele busca também melhorar a transparência e disponibilidade desses dados.

# Invoice Explorer

O *Invoice Explorer* é uma ferramenta pública de fácil acesso que busca facilitar o desenvolvimento de aplicações para o sistema e aumentar a transparência e visibilidade desses dados. 

O Explorer possui uma interface gráfica para visualização das prefeituras, fornecendo uma espécie de painel de controle sobre as atividades econômicas daquele município e de suas empresas no sistema. Na perspectiva das empresas, é possível acompanhar sua atividade em tempo real no sistema e ter estatísticas sobre suas notas fiscais. Para o cidadão, é possível acompanhar o pagamento de impostos de empresas que participam de licitação, ou acompanhar uma parcela do orçamento da sua cidade proveninente do ISS.

O Explorer também possui uma API Rest (*GraphQL em breve*) para os desenvolvedores e parceiros. A referência da API pode ser encontrada logo mais abaixo.

## Referência da API:

# SDEC Blockchain

A SDEC Blockchain é uma blockchain permissionada. Isso quer dizer que, todos podem conectar, verificar e auditar as informações públicas, mas a construção do consenso é reservada à participantes selecionados. Nesse caso, esses participantes são as Juntas Comerciais de cada Estado, Banco do Brasil e eventuais órgãos governamentais.

## Eventos:

A Blockchain funciona como um registro universal de eventos que aconteceram e suas ordens. Para se ter o "estado" do sistema é necessário computar toda a história dele até o bloco mais recente.

Se você é familiarizado com a arquitetura Redux, é possível pensarmos nesses eventos como ações ao estado (computado) atual da Blockchain naquele ponto por dispatchers fora da rede.

Os eventos funcionam a partir de publicações.

## Publicações:

Publicações são arquivos JSON's publicados na Blockchain que descrevem eventos. A publicação de itens se dá através do comando `publish` pelo `sdec-cli`. 

Para acessar a documentação do `sdec-cli` clique [aqui.](https://sdec-brasil.github.io)

## Novo Registro de Empresa:

O registro da empresa deve ser feita pela Junta Comercial responsável. Além da publicação das informações na Blockchain, a Junta também estará autorizando os endereços respectivos a serem emissores de nota.

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
  "emissores": ["1Bw41hdEenVKdNdYN22r7Kc47qVPkSeie1"],
  "cnaes": ["3811-4/00", "3911-4/00"] 
}
```

> Note que a publicação de JSON's necessita de um objeto com somente a chave `json` que mapeia para seu objeto. Exemplo de JSON válido para publicação: `{ json: {a: 1, b: "2"} }`.


Parâmetro | Exigido | Descrição                                           | Tam. |
--------- | ------- | -------------------------------------               | ---- |
razao     |    S    | Razão Social do prestador do serviço                | 150  |
fantasia  |    N    | Nome Fantasia do prestador do serviço               |  60  |
cnpj      |    S    | Número do CNPJ do Prestador do Serviço              |  14  |
logEnd    |    S    | Tipo e nome do logradouro (Av.., Rua..., ...)       | 125  |
numEnd    |    S    | Número do imóvel                                    |  10  |
compEnd   |    N    | Complemento do endereço do prestador                |  60  |
bairroEnd |    S    | Bairro da empresa prestadora de serviço             |  60  |
cidadeEnd |    S    | Código do município do estabelecimento (do IBGE)    |   7  |
estadoEnd |    S    | Sigla da unidade da federação da empresa            |   2  |
cepEnd    |    N    | Número do CEP                                       |   8  |
email     |    N    | E-mail do prestador                                 |  80  |
tel       |    N    | Número do telefone do prestador                     |  20  |
emissores |    S    | Vetor de Endereços Públicos que emitirão notas      | >=1  |
cnaes     |    S    | Vetor de CNAE's que a empresa está permitida        | >=1  |

<aside class="notice">É possível autorizar mais de um endereço público para a emissão de notas em nome da empresa, mas recomendamos que cada um deles seja único à ela e não reutilizado.</aside>

## Alterações no Registro da Empresa:

## Emissão de Notas Fiscais:
