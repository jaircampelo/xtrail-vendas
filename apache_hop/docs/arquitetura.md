# Arquitetura em Camadas

O projeto segue arquitetura em camadas inspirada no padrão **Medallion**, composta por:

- Bronze
- Silver
- Gold (Data Warehouse)

## Bronze — Camada de Ingestão

Responsável pela captura dos dados exatamente como chegam da origem.

- Dados crus
- Sem transformações
- Estrutura fiel à fonte
- Apenas ingestão

## Silver — Camada de Tratamento

Responsável por qualidade e preparação analítica.

- Limpeza de dados
- Remoção de duplicados
- Enriquecimento via merge
- Criação de SCD
- Construção da tabela dCalendario
- Padronização de estruturas

## Gold — Camada Analítica

Entrega dados prontos para consumo BI.

- Criação de Primary Keys
- Implementação de Surrogate Keys
- Persistência no banco DW
- Estrutura dimensional final

# Estrutura de Pastas do Projeto

```
pache_hop/  
│
├── datasets/
│   └── raw/
│
├── docs/
│
├── logs/
│
├── metadata/
│
├── pipelines/
│   ├── bronze/
│   ├── silver/
│   ├── gold/
│   ├── integrations/
│   │   └── telegram/
│   │
│   └── utils/
│
└── workflows/
    └── orquestracao/
```

# Modelagem Dimensional

## Dimensões

- dCalendario
- dClientes
- dProdutos
- dSubcategorias
- dTerritorios

## Fatos

- fDevolucoes
- fMetas
- fVendas

## Slowly Changing Dimension

Implementado em:

>dProdutos

Colunas:

- Surrogate Key
- data_inicio
- data_fim
- produto_versao

Permite rastrear histórico de alterações.

# Orquestração

Execução diária automatizada via workflow principal:

## Fluxo de Execução

1. Início
2. Notificação Telegram
3. Definição Variáveis Incrementais
4. Carga Bronze
5. Carga Silver
6. Carga Gold Dimensões
7. Carga Gold Fatos
8. Limpeza Staging
9. Notificação Sucesso

## Tratamento de Erros

- Interrupção imediata
- Envio de e-mail
- Alerta Telegram com logs

# Monitoramento

- Monitoramento por etapa
- Logs específicos por execução
- Alertas automáticos

# Workflows

- carga_bronze
- carga_silver
- carga_gold_dimensoes
- carga_gold_fatos
- limpa_staging
- orquestracao_dw

# Convenções de Transform

| Tipo           | Prefixo |
| -------------- | ------- |
| Fonte          | src     |
| Transformação  | trf     |
| Validação      | val     |
| Enriquecimento | enr     |
| Saída          | out     |

# Governança

- Versionamento via Git
- Padronização de nomenclatura
- Separação por responsabilidade
- Documentação contínua