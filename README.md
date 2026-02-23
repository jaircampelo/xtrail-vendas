# Projeto de ETL com o uso de Apache Hop

---

## :pushpin: Overview

Esse repositório apresenta a solução final de um projeto de ETL criado do zero  no decorrer do curso de Data Warehouse com Apache Hop, da [Plataforma Xperiun](https://xperiun.com/).

Durante o projeto foram seguidas as boas práticas da **Arquitetura Medalhão** (*bronze*, *silver* e *gold*), desde a ingestão até a criação e carregamento do modelo dimensional em um Data Warehouse hospedado no SQL Server.

Também foi implementado um sistema de monitoramento automático através do disparo de e-mails e mensagens via bot do Telegram, no decorrer do sucesso ou fracasso na execução dos workflows.

---

## :compass: Mapeamento de Soluções

Antes de tudo, através de reuniões com o cliente, aqui denominado de **Xtrail**, foi realizado o levantamento de requisitos e definido das regras de negócio. O documento resultante dessa reunião se encontra disponível em [mapeamento_requisitos.md](apache_hop/docs/mapeamento_requisitos.md).

---

## :star: Modelagem de Dados

De acordo com o Mapeamento de Soluções proposto, a modelagem foi construíd com o auxílio da plataforma [dbdiagram.io](https://dbdiagram.io) e utilizando o modelo **Star Schema*.

#### Modelo de Dados com DBML:
```sql
table dClientes {
  cliente_id              int pk
  cliente_nome_completo   varchar(100)
  cliente_data_nascimento date
  cliente_idade           int
  cliente_estado_civil    varchar(100)
  cliente_email           varchar(50)
  cliente_sexo            varchar(1)
  cliente_nivel_educacao  varchar(50)
  cliente_ocupacao        varchar(50)
  cliente_data_cadastro   date
  cliente_data_registro   datetime
}

table dTerritorios {
  territorio_id             int pk
  territorio_regiao         varchar(50)
  territorio_pais           varchar(50)
  territorio_continente     varchar(50)
  territorio_data_registro  datetime
}

table dProdutos {
  produto_sk            int pk
  produto_id            int
  produto_SKU           varchar(50)
  produto_nome          varchar(50)
  produto_modelo        varchar(50)
  produto_descricao     varchar(50)
  produto_cor           varchar(50)
  produto_tamanho       varchar(50)
  produto_estilo        varchar(50)
  custo_unitario        float
  preco_unitario        float
  data_inicio           datetime
  data_fim              datetime
  produto_versao        int
  produto_data_registro datetime
}

table dSubcategoria {
  subcategoria_id            int pk
  subcategoria_nome          varchar(50)
  categoria_nome             varchar(50)
  subcategoria_data_registro datetime
}

table dCalendario {
  data                date pk
  data_key            int
  ano_num             int
  mes_num             int
  mes_nome            varchar(50)
  mes_nome_abrev      varchar(3)
  mes_ano_nome_abrev  varchar(10)
  trimestre_num       int
  trimestre_nome      varchar(2)
  trimestre_ano_nome  varchar(10)
  semestre_num        int
  semestre_nome       varchar(50)
}

table fVendas {
  pedido_data           date           [ref:> dCalendario.data]
  estoque_data          date
  pedido_num            varchar(7) pk
  produto_sk            int            [ref:> dProdutos.produto_sk]
  subcategoria_id       int            [ref:> dSubcategoria.subcategoria_id]
  cliente_id            int            [ref:> dClientes.cliente_id]
  territorio_id         int            [ref:> dTerritorios.territorio_id]
  pedido_item_linha     int pk
  pedido_qtd            int
  vendas_data_registro  datetime
}

table fDevolucoes {
  devolucao_id              int pk
  devolucao_data            date  [ref:> dCalendario.data]
  territorio_id             int   [ref:> dTerritorios.territorio_id]
  produto_sk                int   [ref:> dProdutos.produto_sk]
  devolucao_qtd             int
  devolucoes_data_registro  datetime
}

table fMetas {
  meta_data           date pk [ref:> dCalendario.data]
  meta_valor          float
  metas_data_registro datetime
}
```

---

## :1st_place_medal: :2nd_place_medal: :3rd_place_medal: Arquitetura Medalhão

O tratamento de dados foi dividido em 3 camadas dentro do Apache Hop:

1. Camada Bronze
>Responsável por trazer os dados brutos do bando de dados, aqui não foi realizada nenhuma grande transformação, preservando a integridade da fonte.

2. Camada Silver
>Nessa camada foram realizadas as principais transformações, como:
>
>- Tratamento de dados sujos e duplicados
>- Enriquecimento de tabelas com merge 
>- Criação de SCD para versionamento de tabelas dimensão
>- Elaboração da tabela dCalendario
>- Entre outros

3. Camada Gold
>Nessa etapa foram criadas as *Primary Keys* e as tabelas foram levadas, já tratadas, para o banco de dados DW prontas para uso.

---

## :arrow_forward: Orquestração do DW

Para orquestrar a carga de dados dentro do DW, todos os pipelines foram inseridos através de worflows, de modo que:
1. Camada Bronze é executada
2. Se sucesso, camada Silver é executada
3. Se sucesso, camada Gold é executada

Por fim, foi criado um pipeline responsável pela limpeza de todos os dados da Stage Área (*bronze* e *silver*), mantendo apenas a estrutura através de *truncate table* via comando SQL.

---

## :satellite: Sistemas de Monitoramento

Com o uso de transforms dentro do Apache Hop, foi criado um sistema de disparo de e-mails relatando o sucesso de carregamento do DW ou a falha na execução de alguma etapa do processo de ETL.

Também foi criado um bot no Telegram, que é responsável por enviar mensagens customizadas indicando em qual etapa o processo de carregamento dos dados se encontra, e através do monitoramento de logs, em caso de erro, dispara uma mensagem indicando a camada onde o erro ocorreu e o log de transação mostrando a causa do erro.

---

## :wrench: Tecnologias Utilizadas

- Apache Hop
- Microsoft SQL Server
- PostgreSql
- DBeaver
- dbdiagram.io
- vsCode
- Git/GitHub
- Telegram Bot API

---

## Agradecimentos

Gostaria de agradecer especialmente ao [Alex Pereira](https://www.linkedin.com/in/alex-pereira-dataenginner-businessanalytics-datascience?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app) por ministrar o curso com excelência, e também ao [Alison Pezzott](https://www.linkedin.com/in/alisonpezzott?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app) por uma bela introdução de mais de 3h sobre Github, o que possibilitou a publicação desse projeto.