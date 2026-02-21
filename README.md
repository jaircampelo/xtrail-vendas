# Projeto de ETL com o uso de Apache Hop

---

## :pushpin: Overview

Esse repositório apresenta a solução final de um projeto de ETL criado do zero  no decorrer do curso de Data Warehouse com Apache Hop, da [Plataforma Xperiun](https://xperiun.com/).

Durante o projeto foram seguidas as boas práticas da **Arquitetura Medalhão** (*bronze*, *silver* e *gold*), desde a ingestão até a criação e carregamento do modelo dimensional em um Data Warehouse hospedado no SQL Server.

Também foi implementado um sistema de monitoramento automático através do disparo de e-mails e mensagens via bot do Telegram, no decorrer do sucesso ou fracasso na execução dos workflows.

---

## :compass: Mapeamento de Soluções

Antes de tudo, através de reuniões com o cliente, aqui denominado de **Xtrail**, foi realizado o levantamento de requisitos e definido das regras de negócio. O documento resultante dessa reunião se encontra disponível em `será inserido em update futuro`.

---

## :star: Modelagem de Dados

De acordo com o Mapeamento de Soluções proposto, a modelagem foi construíd com o auxílio da plataforma [dbdiagram.io](https://dbdiagram.io) e utilizando o modelo **Star Schema*.

#### Modelo de Dados com DBML:
```
<Será inserido em update futuro>
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