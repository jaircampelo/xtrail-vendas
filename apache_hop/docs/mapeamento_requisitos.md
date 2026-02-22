# Mapeamento de Requisitos
## Projeto de Data Warehouse - Cliente: Xtrail

Este documento apresenta o mapeamento de requisitos levantados após reuniões realizadas com a empresa Xtrail, com o objetivo de estruturar a construção de um Data Warehouse (DW) corporativo. A iniciativa visa organizar, consolidar e estruturar os dados da empresa, proporcionando melhor performance analítica, padronização e governança de dados, escalabilidade, integridade e confiabilidade das informações, além de suporte estratégico à tomada de decisão.

## Objetivos Estratégicos

- **Performance Analítica**: Otimização de consultas e análises complexas  
- **Governança de Dados**: Padronização e controle de qualidade  
- **Escalabilidade**: Crescimento sustentável da infraestrutura  
- **Decisão Estratégica**: Suporte baseado em dados confiáveis  

---

## Contexto Atual e Objetivo do Projeto

### Ambiente Atual
A empresa Xtrail armazena seus dados operacionais em um banco de dados PostgreSQL, contendo informações relacionadas a vendas, clientes, produtos, territórios, custos e devoluções. Entretanto, o ambiente atual apresenta limitações significativas para análises estratégicas e consolidação histórica dos dados.

### Objetivo Principal
Desenvolver um Data Warehouse de Vendas que permita análises multidimensionais, consolidação histórica e acompanhamento de indicadores estratégicos. Este projeto estabelecerá a base formal para o desenvolvimento do ambiente analítico da empresa.

### Fontes de Dados Identificadas
- **Banco de Dados Operacional**: Banco relacional PostgreSQL contendo dados transacionais de vendas e cadastros corporativos  
- **Planilha de Metas Comerciais**: Arquivo Excel fornecido pelo gerente comercial, onde cada aba representa um ano com dados de mês e valor da meta mensal

---

## Indicadores e Requisitos Analíticos

### Indicadores de Negócio Identificados
1. **Valor de Vendas**: Acompanhamento do faturamento total  
2. **Metas Comerciais**: Objetivos mensais estabelecidos  
3. **Custos**: Despesas operacionais associadas  
4. **Devoluções**: Volume de produtos devolvidos  
5. **Resultado**: Lucro e margem de contribuição  
6. **Meta x Realizado**: Comparativo de desempenho  

### Principais Análises Solicitadas

#### Análise por Cliente
- Total de vendas por cliente  
- Metas associadas e custos  
- Devoluções por cliente  
- Dados demográficos (idade, nome completo)  

**Observação:** Base de clientes pode conter inconsistências, necessitando tratamento antes da carga

#### Análise por Território
- Região e território  
- Localização geográfica  
- Vendas, metas e custos por região  
- Devoluções por território  

#### Análise por Produto
- Vendas por produto individual  
- Histórico de alterações cadastrais  
- Controle de mudanças ao longo do tempo  
- Performance por categoria e subcategoria  

#### Análise Temporal
- Segmentação por ano  
- Análise por semestre e trimestre  
- Dados mensais detalhados  
- Dimensão de tempo estruturada  

---

## Requisitos Técnicos e Próximos Passos

### Arquitetura do Data Warehouse
- **Integração**: Coletar dados de fontes  
- **Camadas**: Construir camadas analíticas  
- **Modelagem**: Estruturar fatos e dimensões  
- **Governança**: Monitorar e controlar qualidade  
- **Tratamento**: Padronizar e limpar registros  

> O Data Warehouse deverá contemplar modelagem dimensional completa com estruturação em fatos e dimensões, controle de histórico de alterações, tratamento de dados inconsistentes, padronização de informações e consolidação de dados de múltiplas fontes em uma estrutura escalável.

### Escopo do Projeto

**Inclui:**  
- Levantamento de requisitos  
- Modelagem dimensional  
- Integração de dados  
- Tratamento e padronização  
- Criação de camadas analíticas  
- Implementação de monitoramento

### Próximos Passos
1. **Validação e Aprovação**  
   - Validação deste documento pela Xtrail e aprovação formal do projeto  
2. **Modelagem**  
   - Definição do modelo dimensional e arquitetura técnica  
3. **Desenvolvimento**  
   - Construção do ambiente de dados e implementação das camadas  
4. **Qualidade e Testes**  
   - Validação de integridade e testes de qualidade dos dados  
5. **Implantação**  
   - Deploy em produção e início das operações analíticas  

---

## Contato
**JAIR CAMPELO**  
- E-mail: [jairjrcampelo@gmail.com](mailto:jairjrcampelo@gmail.com)  
- Telefone: (91) 98061-2086  
- LinkedIn: [linkedin.com/in/jaircampelo](https://www.linkedin.com/in/jaircampelo)