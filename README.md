#  E-commerce Customer Churn & Engagement Analysis

Este projeto foi desenvolvido com o objetivo de simular um cenário real de engenharia e análise de dados em grandes empresas do mercado (estilo Itaú, Nubank, Ambev e Mercado Livre). O foco principal foi investigar a evasão de clientes (churn) e o comportamento de engajamento utilizando a biblioteca **Pandas** e otimizações com **NumPy**.

## 🛠️ Tecnologias e Conceitos Aplicados
* **Python** (Lógica de Programação e Estruturas de Dados)
* **Pandas** (DataFrames, Merges, Máscaras Booleanas, GroupBy Avançado e Vetorização)
* **NumPy** (Lógica Condicional de Alta Performance com `np.select`)
* **Jupyter Notebook** (Ambiente de Desenvolvimento)

---

##  Etapas de Desenvolvimento do Projeto

### 1. Consolidação dos Dados (Silos de Dados)
Na vida real, os dados raramente vêm prontos em uma única tabela. Neste projeto, as características dos clientes (`ecommerce_customer_features.csv`) estavam separadas do status de churn (`ecommerce_customer_targets.csv`). A primeira etapa foi unificar essas fontes utilizando a chave exclusiva `Customer_ID`.

### 2. Segmentação Crítica de Churn
Para apoiar o time de Marketing, criamos um filtro avançado (máscara booleana) para isolar de forma cirúrgica o grupo de altíssimo risco. Isolamos **448 clientes** que atendiam cumulativamente aos critérios:
* Já estavam em Churn (`churned == 'Yes'`)
* Estavam há mais de 30 dias sem comprar (`days_since_last_purchase > 30`)
* Tinham menos de 3 pedidos feitos no total (`total_orders < 3`)
* **Métrica extraída:** O valor médio de pedido (`avg_order_value`) desse grupo crítico foi de **R$ 79,55**.

### 3. Diagnóstico Temático de Engajamento
Utilizando agrupamento multinível (`groupby`), cruzamos o status de fidelidade (`loyalty_member`) com o volume de chamados no suporte (`customer_support_tickets`). Descobrimos que os clientes que mais abandonam o carrinho (média de **51%**) são aqueles que **não** são membros do programa de fidelidade e possuem um alto índice de atrito no suporte (4 ou 5 tickets abertos).

### 4. Feature Engineering (Engenharia de Atributos)
Para municiar o time de CRM em campanhas de reengajamento, criamos uma nova coluna de classificação chamada `Perfil_do_Cliente` de forma 100% vetorizada (sem loops lentos), distribuindo a base em:
* **Clientes_Rotativos (Regular):** 4.495 clientes
* **Contas_Inativas (Veterano Inativo):** 1.183 clientes
* **Clientes_Novos (Novato Engajado):** 322 clientes

---

##  Desafios Enfrentados e Aprendizados (Como Solucionei)

Durante o desenvolvimento supervisionado pelo Tech Lead, encarei alguns desvios de sintaxe e lógica comuns no início da carreira, mas que foram fundamentais para consolidar o aprendizado:

###  Erro de Case-Sensitivity no Merge (`KeyError`)
* **O Problema:** Ao tentar juntar as tabelas usando `on='customer_id'`, o Python retornou um erro porque as colunas no CSV original estavam com letras maiúsculas (`Customer_ID`).
* **A Solução:** Aprendi que o Pandas é estritamente *case-sensitive*. Ajustei a string para bater exatamente com o cabeçalho físico do arquivo.

###  Filtros Incompletos e Falta de Parênteses
* **O Problema:** Na hora de construir a máscara booleana com múltiplas condições, tentei passar apenas o nome da coluna solto entre aspas (ex: `'days_since_last_purchase' > 30`), o que gerou um erro de tipo (`TypeError`).
* **A Solução:** Entendi o conceito de que o Pandas precisa saber explicitamente de qual DataFrame aquela coluna está vindo (`df_uni['coluna']`). Além disso, fixei a regra de ouro de que **cada condição precisa estar isolada entre parênteses `()`** e unida pelo operador bitwise `&` para que a precedência de execução do Python não quebre o pipeline.

###  Confusão entre Agrupamento e Métrica
* **O Problema:** No primeiro desenho do `groupby`, misturei colunas de métricas decimais contínuas (como `engagement_score`) dentro do agrupador, o que geraria milhares de linhas desnecessárias.
* **A Solução:** Compreendi a analogia das "caixas e gavetas". O `groupby` deve receber as variáveis categóricas (as etiquetas das gavetas), enquanto o método `.agg()` recebe um dicionário especificando quais operações matemáticas (como `'mean'` ou `'count'`) faremos com os números guardados ali dentro.

###  Substituição de Loops por Otimização NumPy
* **O Problema:** Para criar colunas condicionais, a primeira tendência de um desenvolvedor iniciante é criar funções com `if/elif` e usar o método `.apply(axis=1)`.
* **A Solução:** Fui orientado a pensar em performance para produção. O `.apply()` linha a linha funciona como um loop disfarçado e é extremamente lento em bases massivas. Solucionei o problema implementando o **`np.select()`**, que cria listas de condições e etiquetas na memória e processa a base inteira de uma única vez (vetorização nativa).

---
*Projeto desenvolvido por Enuk para fins de estudo e preparação para o mercado de Engenharia e Análise de Dados.*
