# SQL E-commerce Analytics

Projeto de banco de dados relacional com foco em **SQL (básico ao intermediário)**, simulando uma operação de e-commerce para análise de indicadores de negócio.

## Objetivo

Construir um projeto completo de dados com foco principal em SQL, cobrindo:

- modelagem relacional;
- criação de esquema com regras de integridade;
- consultas analíticas para responder perguntas reais de negócio;
- organização reprodutível para portfólio técnico.

## Escopo

O projeto simula dados de:

- clientes;
- produtos e categorias;
- pedidos e itens de pedido;
- pagamentos;
- entregas;
- vendedores.

Com essa base, serão geradas análises como:

- faturamento mensal;
- ticket médio;
- produtos mais vendidos;
- retenção/recompra;
- atraso de entrega;
- performance por vendedor/região.

## Estrutura do repositório

sql-ecommerce-analytics/
  docs/
  sql/
  data/
  notebooks/
  etl/
  results/
  README.md
  .gitignore

##Organização dos scripts SQL

01_schema.sql: criação das tabelas, chaves e constraints.
02_seed.sql: carga inicial de dados para testes.
03_views.sql: views de apoio analítico.
04_queries_basicas.sql: consultas SQL básicas.
05_queries_intermediarias.sql: CTEs, subqueries e window functions.
06_performance_indices.sql: índices e otimização.
07_quality_checks.sql: validações de qualidade e consistência.

##STACK PLANEJADA

- Banco de dados: PostgreSQL
- SQL: modelagem + análise
- Python (apoio): carga e execução de consultas
- IA (apoio mínimo): consumo de views para experimento simples

##STATUS DO PROJETO
Em construção: etapa atual de modelagem e estruturação inicial.
