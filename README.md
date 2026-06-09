# 🏥 Projeto Final: Previsão de Custos Médicos Hospitalares
**Disciplina:** Introdução ao Aprendizado de Máquina  
**Professor:** Everton Meyer da Silva  
**Instituição:** IFSP Câmpus Campinas  

### 👥 Integrantes
* Giovana Giovanin (CP3026337)
* Maria Eduarda Ribeiro Padovani Loschi (CP3025811)

---

## 📌 1. Descrição do Problema e Motivação
O mercado de seguros de saúde utiliza dados demográficos e hábitos de vida para calcular o risco e o custo de cuidados médicos de seus beneficiários. Prever esses custos de forma precisa é vital para que a empresa possa precificar suas apólices de seguro de maneira competitiva, evitando prejuízos financeiros ou a cobrança de valores abusivos dos clientes. 

O objetivo deste projeto é construir um pipeline completo de Machine Learning para prever a variável-alvo **`charges`** (custos médicos faturados), caracterizando um problema de **Regressão**.

---

## 📊 2. Estrutura da Base de Dados
O dataset contém informações de beneficiários individuais, divididas nos seguintes atributos:
* `age`: Idade do beneficiário (Inteiro)
* `sex`: Gênero do beneficiário (male/female)
* `bmi`: Índice de Massa Corporal (Numérico)
* `children`: Número de filhos/dependentes (Inteiro)
* `smoker`: Indica se o beneficiário é fumante (yes/no)
* `region`: Região de residência nos EUA (Categórico)
* `charges`: Custos médicos faturados (Target - Numérico)

---

## 🔬 3. Metodologia Adotada

### Parte 1: Análise Exploratória de Dados (EDA)
Na primeira fase, analisamos as distribuições e correlações. O principal insight gerado foi que **o fato de fumar, combinado com um IMC (BMI) elevado, faz os custos médicos aumentarem de forma explosiva (não-linear)**, sendo o principal fator de impacto no preço final do seguro.

### Parte 2: Modelagem e Avaliação
Para garantir o rigor estatístico e evitar o **Data Leakage (Vazamento de Dados)**, separamos a base em **80% Treino e 20% Teste antes de qualquer pré-processamento**. 
* **Pré-processamento:** Variáveis numéricas foram normalizadas com `StandardScaler` e as categóricas foram transformadas com `OneHotEncoder(drop='first')`.
* **Modelos Testados:** Avaliamos 3 técnicas através de `Pipeline`: *Linear Regression* (como Baseline), *Random Forest Regressor* e *Gradient Boosting Regressor* (abordagem avançada para ponto extra).
* **Otimização:** Aplicamos `GridSearchCV` com **Validação Cruzada de 5 dobras (5-fold CV)** para tunar os hiperparâmetros do Random Forest.

---

## 📈 4. Principais Resultados

A tabela abaixo resume o desempenho das técnicas no conjunto de testes:

| Modelo | MAE (Erro Médio) | RMSE | R² Score (Precisão) |
| :--- | :--- | :--- | :--- |
| **Linear Regression (Baseline)** | \$4,181.19 | \$5,796.28 | 78.35% |
| **Random Forest (Puro)** | \$2,543.97 | \$4,567.77 | 86.56% |
| **Random Forest (Otimizado via CV)** | - | - | 84.42% |
| **Gradient Boosting (Melhor Modelo)** | **\$2,443.48** | **\$4,329.57** | **87.92%** |

### Conclusões da Modelagem:
1. Os modelos baseados em árvores (*Random Forest* e *Gradient Boosting*) superaram o baseline por conseguirem capturar as relações não-lineares presentes nos dados (como a interação IMC + Fumante).
2. O **Gradient Boosting** foi o melhor modelo, explicando **87,92%** da variabilidade dos custos e reduzindo o erro médio em quase **\$1.737,00 por cliente** comparado à Regressão Linear.
3. A Validação Cruzada do Random Forest resultou em **84.42%**, provando que o modelo é estável e possui ótima capacidade de generalização para dados reais de novos clientes (sem sofrer de *overfitting*).

---

## 🛠️ 5. Instruções para Execução
1. Certifique-se de ter as bibliotecas instaladas: `pip install pandas numpy scikit-learn`
2. Certifique-se de que o arquivo `segurosdatabase.csv` está no mesmo diretório dos notebooks.
3. Execute o notebook da Parte 2 para reproduzir os treinos e os resultados da tabela.
