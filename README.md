# E-commerce Customer Churn & Engagement Analysis

Análise de dados em Python com Pandas e NumPy para investigar evasão de clientes (churn) e padrões de engajamento em uma base de e-commerce.

---

## Sobre o projeto

Este projeto simula um cenário real de análise de dados em empresas de grande porte. A base de dados contém informações de clientes divididas em dois arquivos separados, replicando a realidade de sistemas com silos de dados. O objetivo foi unificar essas fontes, extrair métricas de churn e engajamento, e gerar segmentações acionáveis para times de Marketing e CRM.

---

## Tecnologias utilizadas

- **Python 3**
- **Pandas** — DataFrames, merges, máscaras booleanas, GroupBy avançado e vetorização
- **NumPy** — lógica condicional de alta performance com `np.select`
- **Jupyter Notebook** — ambiente de desenvolvimento e documentação

---

## Estrutura dos dados

| Arquivo | Conteúdo |
|---|---|
| `ecommerce_customer_features.csv` | Características dos clientes (comportamento, frequência, valor de pedido) |
| `ecommerce_customer_targets.csv` | Status de churn por cliente |

A chave de junção entre os dois arquivos é `Customer_ID`.

---

## Etapas da análise

### 1. Consolidação dos dados
Unificação das duas fontes usando `pd.merge()` pela chave `Customer_ID`, replicando a integração de silos de dados comum em ambientes corporativos.

### 2. Segmentação crítica de churn
Isolamento de 448 clientes de altíssimo risco via máscara booleana com três critérios cumulativos: já em churn, mais de 30 dias sem compra e menos de 3 pedidos no total. O valor médio de pedido desse grupo foi de **R$ 79,55**.

### 3. Diagnóstico de engajamento
Agrupamento multinível (`groupby`) cruzando status de fidelidade com volume de tickets de suporte. Descoberta: clientes não-fidelizados com 4 ou 5 tickets abertos têm média de abandono de carrinho de **51%**.

### 4. Feature Engineering
Criação da coluna `Perfil_do_Cliente` de forma 100% vetorizada com `np.select`, classificando a base em:

| Segmento | Clientes |
|---|---|
| Clientes Rotativos (Regular) | 4.495 |
| Contas Inativas (Veterano Inativo) | 1.183 |
| Clientes Novos (Novato Engajado) | 322 |

---

## Aprendizados técnicos documentados

Durante o desenvolvimento, foram identificados e corrigidos erros comuns de quem está começando com Pandas:

**Case-sensitivity no merge** — colunas no CSV estavam com `Customer_ID` (maiúsculo), não `customer_id`. Pandas é estritamente case-sensitive.

**Máscaras booleanas com múltiplas condições** — cada condição precisa estar entre parênteses `()` e unida pelo operador bitwise `&`, não pelo `and` do Python nativo.

**GroupBy com variáveis erradas** — colunas contínuas (como `engagement_score`) não pertencem ao agrupador; pertencem ao `.agg()`. O `groupby` recebe apenas variáveis categóricas.

**`.apply()` vs vetorização** — `.apply(axis=1)` é um loop disfarçado e lento em bases grandes. `np.select()` processa a base inteira de uma vez na memória.

---

## Como executar

```bash
# Clone o repositório
git clone https://github.com/EnukNogueira/ecommerce-data.git
cd ecommerce-data

# Instale as dependências
pip install pandas numpy jupyter

# Abra o notebook
jupyter notebook ecommerce.ipynb
```

---

## Autor

**Enuk Nogueira** — Desenvolvedor focado em Engenharia de Dados e Automação de Processos

[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/enuknogueira/)
[![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)](https://github.com/EnukNogueira)
