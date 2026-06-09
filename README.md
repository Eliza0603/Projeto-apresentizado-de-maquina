# Projeto Final: Previsão de Custos Médicos Hospitalares

**Disciplina:** Introdução ao Aprendizado de Máquina
**Professor:** Everton Meyer da Silva
**Instituição:** IFSP Câmpus Campinas

## Integrantes

* Giovana Giovanin (CP3026337)
* Maria Eduarda Ribeiro Padovani Loschi (CP3025811)

---

## 1. Descrição do Problema e Motivação

O mercado de seguros de saúde utiliza dados demográficos e hábitos de vida para calcular o risco e o custo de cuidados médicos de seus beneficiários. Prever esses custos de forma precisa é vital para que a empresa possa precificar suas apólices de seguro de maneira competitiva, evitando prejuízos financeiros ou a cobrança de valores abusivos dos clientes.

O objetivo deste projeto é construir um pipeline completo de Machine Learning para prever a variável-alvo **`charges`** (custos médicos faturados), caracterizando um problema de regressão.

---

## 2. Dataset Utilizado

**Nome do Dataset:** Medical Cost Personal Dataset

**Fonte:**
https://www.kaggle.com/datasets/mirichoi0218/insurance

O conjunto de dados contém informações demográficas, características pessoais e hábitos de vida dos beneficiários, juntamente com os custos médicos faturados.

### Atributos da Base

* `age`: Idade do beneficiário (Inteiro)
* `sex`: Gênero do beneficiário (male/female)
* `bmi`: Índice de Massa Corporal (Numérico)
* `children`: Número de filhos/dependentes (Inteiro)
* `smoker`: Indica se o beneficiário é fumante (yes/no)
* `region`: Região de residência nos EUA (Categórico)
* `charges`: Custos médicos faturados (Target - Numérico)

---

## 3. Metodologia Adotada

### Parte 1: Análise Exploratória de Dados (EDA)

Na primeira fase, analisamos as distribuições e correlações. O principal insight gerado foi que o fato de fumar, combinado com um IMC elevado, faz os custos médicos aumentarem de forma não linear, sendo o principal fator de impacto no preço final do seguro.

### Parte 2: Modelagem e Avaliação

Para garantir o rigor estatístico e evitar o Data Leakage (Vazamento de Dados), separamos a base em 80% para treino e 20% para teste antes de qualquer pré-processamento.

**Pré-processamento:**

* StandardScaler para variáveis numéricas.
* OneHotEncoder para variáveis categóricas.

**Modelos Testados:**

* Linear Regression (Baseline)
* Random Forest Regressor
* Gradient Boosting Regressor

**Otimização:**

* GridSearchCV com validação cruzada de 5 dobras (5-Fold Cross Validation).

---

## 4. Principais Resultados

| Modelo                                     | MAE           | RMSE          | R² Score   |
| ------------------------------------------ | ------------- | ------------- | ---------- |
| Linear Regression (Baseline)               | $4.181,19     | $5.796,28     | 78,35%     |
| Random Forest (Puro)                       | $2.543,97     | $4.567,77     | 86,56%     |
| Random Forest (Otimizado via GridSearchCV) | $2.575,23     | $4.443,50     | 87,28%     |
| Gradient Boosting (Melhor Modelo)          | **$2.443,48** | **$4.329,57** | **87,92%** |

### Conclusões da Modelagem

1. Os modelos baseados em árvores apresentaram desempenho superior à Regressão Linear por conseguirem capturar relações não lineares presentes nos dados.
2. O Gradient Boosting foi o modelo com melhor desempenho geral, alcançando R² de 87,92%.
3. A otimização dos hiperparâmetros por meio do GridSearchCV melhorou o desempenho do Random Forest, elevando seu R² para 87,28%.

---

## 5. Estrutura do Projeto

```text
Projeto/
│
├── README.md
├── Parte1_EDA.ipynb
├── Parte2_Modelagem.ipynb
└── segurosdatabase.csv
```

---

## 6. Instruções para Execução

### Instalação das Dependências

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### Execução

1. Baixe ou clone o repositório.
2. Certifique-se de que o arquivo `segurosdatabase.csv` esteja no mesmo diretório dos notebooks.
3. Abra os notebooks em Jupyter Notebook ou Google Colab.
4. Execute todas as células em ordem.
5. Os resultados apresentados neste README poderão ser reproduzidos automaticamente.
