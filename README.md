# E-commerce Customer Churn & Engagement Analysis

Exercício de análise de dados em Python utilizando Pandas e NumPy para analisar comportamento de clientes, churn e engajamento em uma base de e-commerce.

---

## Sobre o projeto

O projeto utiliza duas bases de dados com informações de clientes.

A primeira contém características relacionadas ao comportamento de compra e a segunda contém informações sobre churn.

O objetivo foi praticar manipulação e análise de dados utilizando Pandas, além de aplicar algumas técnicas de segmentação com NumPy.

---

## Tecnologias utilizadas

- **Python 3**
- **Pandas** — manipulação e análise dos dados
- **NumPy** — operações e criação de classificações
- **Jupyter Notebook** — desenvolvimento dos exercícios

---

## Estrutura do projeto

- `ecommerce_customer_features.csv` — dados de características dos clientes
- `ecommerce_customer_targets.csv` — informações de churn
- `ecommerce.ipynb` — notebook com os exercícios e análises
- `README.md` — documentação do projeto

---

## O que foi praticado

- [x] Leitura de arquivos CSV
- [x] Manipulação de DataFrames
- [x] `merge()` para combinar diferentes bases
- [x] Filtros com máscaras booleanas
- [x] `groupby()` e agregações
- [x] Análise de churn
- [x] Análise de comportamento dos clientes
- [x] Criação de classificações com `np.select()`
- [x] Operações vetorizadas

---

## Análises realizadas

Durante os exercícios foram analisados:

- Clientes em situação de churn
- Tempo desde a última compra
- Quantidade de pedidos realizados
- Valor médio dos pedidos
- Relação entre fidelidade e tickets de suporte
- Abandono de carrinho
- Segmentação dos clientes por comportamento

---

## Principais resultados

Foi identificado um grupo de **448 clientes** que atendia simultaneamente aos critérios de churn, mais de 30 dias sem compra e menos de 3 pedidos realizados.

Também foi analisada a relação entre fidelidade e tickets de suporte, além da criação de uma classificação de clientes baseada em seu comportamento.

---

## Como executar

```bash
git clone https://github.com/EnukNogueira/ecommerce-data.git
cd ecommerce-data
pip install pandas numpy jupyter
jupyter notebook ecommerce.ipynb
```

---

## Objetivo do estudo

Este projeto faz parte dos meus estudos de Análise de Dados e foi desenvolvido para praticar operações fundamentais de Pandas e NumPy utilizando uma base de e-commerce.

---

## Autor

**Enuk Nogueira**

Estudante de Análise e Desenvolvimento de Sistemas pela PUCPR, com foco em Análise de Dados e Ciência de Dados.

[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/enuknogueira/)

[![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)](https://github.com/EnukNogueira)
