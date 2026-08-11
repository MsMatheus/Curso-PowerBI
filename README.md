# 📊 Trilha de Aprendizado em Power BI & Data Analytics | Comunidade Data Driven

<p align="center">
  <img src="https://img.shields.io/badge/Power_BI-F2C94C?style=for-the-badge&logo=powerbi&logoColor=black" alt="Power BI Badge" />
  <img src="https://img.shields.io/badge/DAX-Advanced-blue?style=for-the-badge" alt="DAX Badge" />
  <img src="https://img.shields.io/badge/SQL_Server-CC292B?style=for-the-badge&logo=microsoftsqlserver&logoColor=white" alt="SQL Server Badge" />
  <img src="https://img.shields.io/badge/Status-Conclu%C3%ADdo-brightgreen?style=for-the-badge" alt="Status Badge" />
</p>

---

## 📌 Sobre o Repositório

Este repositório documenta a minha jornada de capacitação e aprimoramento técnico em **Business Intelligence (BI)** e **Análise de Dados**, desenvolvida ao longo do curso da **Comunidade Data Driven** (com a instrução da **Kátia**)[cite: 1]. 

O objetivo principal deste projeto/documentação é demonstrar a aplicação prática dos conceitos aprendidos — desde a extração e transformação de dados em escala até a criação de modelos relacionais robustos, fórmulas DAX avançadas e visualizações estratégicas voltadas para a tomada de decisão[cite: 1].

---

## 🚀 Principais Competências Desenvolvidas

### 1. 🧹 ETL & Power Query (Linguagem M)
- **Extração e Conexão de Dados**: Conexão com múltiplas fontes (SQL Server, arquivos Excel, CSV e dados em nuvem)[cite: 1, 5].
- **Tratamento e Limpeza**: Remoção de duplicadas, alteração de tipos de dados, tratamento de valores nulos, substituição de erros e padronização[cite: 5].
- **Modelagem no Power Query**: Transposição, unpivot (despivotar colunas), mesclagem e união de consultas (*Merge* e *Append*).

### 2. 🏗️ Modelagem de Dados Relacional
- **Esquemas Dimensional**: Implementação das melhores práticas de modelagem **Star Schema** (Esquema em Estrela) e **Snowflake**.
- **Tabelas Fato vs. Dimensão**: Separação clara entre eventos quantitativos (Fatos) e contextos analíticos (Dimensões/Dicionários).
- **Relacionamentos e Cardinalidade**: Configuração correta de relacionamentos `1:N` e `N:1`, gerenciamento de direção de filtro e uso de tabelas `dCalendario` customizadas.

### 3. 🧮 DAX (Data Analysis Expressions) Avançado
- **Medidas Explícitas vs. Implícitas**: Criação de arquitetura de medidas organizadas em pastas para otimização de performance.
- **Contextos de Avaliação**: Domínio sobre Contexto de Linha, Contexto de Filtro e Transição de Contexto.
- **Manipulação de Filtros**:
  - `CALCULATE`, `FILTER`, `ALL`, `ALLEXCEPT`, `ALLSELECTED`, `USERELATIONSHIP`.
- **Inteligência Temporal (Time Intelligence)**:
  - Comparação ano a ano (*YoY*), mês a mês (*MoM*).
  - Cálculo de acumulados no ano (*YTD*, *QTD*, *MTD*), `SAMEPERIODLASTYEAR`, `DATEADD` e acumulados móveis.

---

## 💻 Exemplos de Fórmulas DAX Desenvolvidas

```dax
// Cálculo de Total de Vendas / Receita
Total Receita = 
SUMX(
    fVendas, 
    fVendas[Quantidade] * fVendas[PrecoUnitario]
)

// Comparativo com o Mesmo Período do Ano Anterior (YoY)
Receita Ano Anterior = 
CALCULATE(
    [Total Receita],
    SAMEPERIODLASTYEAR(dCalendario[Data])
)

// Variação Percentual YoY
% Crescimento YoY = 
VAR _ReceitaAtual = [Total Receita]
VAR _ReceitaAnterior = [Receita Ano Anterior]
RETURN
DIVIDE(
    _ReceitaAtual - _ReceitaAnterior,
    _ReceitaAnterior,
    0
)
