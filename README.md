# projeto-deteccao-de-fraudes-em-transacoes-reais
Modelo de Machine Learning capaz de identificar transações fraudulentas em cartões de crédito.  
Foi utilizado um dataset com 284.807 transações reais, contendo 30 variáveis preditoras e uma variável de classificação (Class), na qual:  0: transação legítima.  1: transação fraudulenta.

# O desafio do desbalanceamento

Um dos principais desafios encontrados foi o forte desbalanceamento das classes:

Transações legítimas: 99,83%.

Transações fraudulentas: 0,17%.

Esse desbalanceamento influencia diretamente a avaliação dos modelos. Um algoritmo poderia classificar todas as transações como legítimas por conta da diferença da quantidade de "exemplos" de transações fraudulentas para transações legítimas.

Por esse motivo, foram priorizadas métricas como Precision, Recall e F1-score da classe de fraude, em vez de utilizar somente a acurácia.

# Preparação dos dados

Durante a etapa de preparação, foram realizadas as seguintes atividades:

Análise exploratória e verificação da estrutura do dataset.

Verificação de valores ausentes.

Análise da distribuição das classes.

Criação da variável Amount_log, utilizando transformação logarítmica para reduzir a assimetria dos valores das transações.

Separação dos dados em treino e teste, utilizando train_test_split, com 80% para treinamento e 20% para teste.

Utilização de stratify para preservar a proporção das classes nos conjuntos.

Padronização das variáveis com StandardScaler.

Aplicação de técnicas para lidar com o desbalanceamento, incluindo class_weight e scale_pos_weight.

# Modelos desenvolvidos

Foram treinados e avaliados três algoritmos:

Regressão Logística.

Random Forest.

XGBoost.

Posteriormente, foi realizada uma otimização do limiar de decisão do XGBoost, buscando melhorar o equilíbrio entre Precision e Recall.

# Comparação dos resultados

As métricas abaixo consideram exclusivamente a classe positiva (fraudes).

|index|Modelo|Precision|Recall|F1-score|
|---|---|---|---|---|
|0|Regressão Logística|6\.12%|91\.84%|11\.47%|
|1|Random Forest|96\.1%|75\.51%|84\.57%|
|2|XGBoost|55\.56%|86\.73%|67\.73%|
|3|XGBoost Otimizado|85\.42%|83\.67%|84\.54%|

# Interpretação

Regressão Logística: apresentou alto Recall, ou seja, o modelo detectou 91,84% das fraudes, porem gerou muitos falsos positivos por conta da baixa Precision. Esse é o modelo mais indicado caso a necessidade de identificação e prevenção de fraudes seja de extrema importância.

Random Forest: apresentou a maior Precision, mas deixou passar uma quantidade maior de fraudes (Recall - 75,51%). Esse modelo é o mais indicado nos casos em que a trava para usuários realizarem transações reais seja mais importante do que a prevenção de fraudes.

XGBoost: apresentou bom Recall, porém com menor Precision, ou seja, detectou grande parte das fraudes porém também apontou mais transações legítimas como fraude (Precision - 55,56%).

XGBoost Otimizado: apresentou um equilíbrio entre Precision e Recall, com F1-score de 84,54%. Esse é o modelo mais equilibrado.

Com base nos resultados, o XGBoost otimizado foi selecionado como modelo candidato principal, considerando o equilíbrio entre identificação de fraudes e redução de falsos alertas.

# Otimização do limiar de decisão XGBoost

O limiar padrão de classificação foi ajustado por meio da análise da curva Precision-Recall e da identificação do ponto com maior F1-score.

O limiar selecionado foi:

0,954468

A matriz de confusão apresentou:

Verdadeiros positivos: 82.

Verdadeiros negativos: 56.850.

Falsos positivos: 14.

Falsos negativos: 16.

Observação: O limiar foi selecionado utilizando o conjunto de teste. Para uma avaliação final rigorosa, o ideal é selecionar o limiar em um conjunto de validação independente e utilizar o teste apenas para a avaliação final.

# Interpretabilidade do modelo

A análise de importância das variáveis do XGBoost destacou os seguintes atributos:

V14

V10

V4

V11

V20

V12

V8

Amount_log

Amount

V3

As variáveis V1 a V28 foram obtidas por transformação PCA e, portanto, não possuem interpretação financeira direta.

# Conclusão

O projeto demonstrou como diferentes algoritmos de Machine Learning podem ser aplicados à identificação de transações fraudulentas.

Os resultados evidenciaram que a escolha do modelo depende das prioridades do negócio. Enquanto o Random Forest apresentou maior precisão, o XGBoost otimizado demonstrou um equilíbrio entre precisão e capacidade de identificação de fraudes.

Assim, a definição do modelo mais adequado deve considerar o impacto dos falsos positivos e falsos negativos, especialmente em um cenário de forte desbalanceamento de classes.

# Tecnologias utilizadas

Python

Pandas

NumPy

Matplotlib

Seaborn

Scikit-learn

XGBoost

# Fonte dos dados

Dataset: [Credit Card Fraud Detection](https://storage.googleapis.com/download.tensorflow.org/data/creditcard.csv)

## Notebook

Acesse o notebook completo com o código, análises exploratórias, treinamento dos modelos e avaliação dos resultados:

📓 [Detecção de Fraudes em Transações com Cartão de Crédito] (https://colab.research.google.com/drive/1GfG6G12-YjdzsieQM1yK4IvjLyForx-b?usp=sharing)


[📓 Acessar notebook completo](deteccao_fraudes_transacoes_vf.ipynb)
