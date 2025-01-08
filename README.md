# house-sell-predict

#### Português 🇧🇷

---

## Objetivo

O objetivo desta análise é prever se um usuário de um site de imóveis comprará uma casa com base nos dados do seu perfil. Isso inclui variáveis como idade, renda anual, gênero, tempo gasto no site e se o usuário clicou em um anúncio.

## Visão Geral do Dataset
O dataset contém as seguintes colunas:
- **Idade**: Idade do usuário.
- **Renda Anual ($)**: Renda anual do usuário em dólares.
- **Gênero**: Gênero do usuário (Feminino ou Masculino).
- **Tempo no Site (min)**: Tempo gasto navegando no site, em minutos.
- **Anúncio Clicado**: Se o usuário clicou em um anúncio (Sim ou Não).
- **Compra**: Variável alvo indicando se o usuário comprou uma casa (1 para Sim, 0 para Não).

## Análise e Resultados

Para compreender plenamente os resultados finais e as conclusões, cada etapa do processo será rigorosamente documentada e analisada de forma crítica.

### Análise Exploratória de Dados (EDA)

* O dataset apresentou um desbalanceamento em relação à variável alvo, com uma proporção de 67% (não compraram) - 33% (compraram). Como resultado, métricas de avaliação adicionais além da acurácia simples foram consideradas. Durante o treinamento do modelo, foi utilizada a métrica ROC AUC, enquanto o F1-score, juntamente com recall e precisão, foram usados para avaliar o desempenho nas classes alvo.

* O dataset continha características com escalas variadas, o que exigiu padronização em uma etapa posterior para mitigar essas diferenças.

* O dataset incluía 2 características categóricas e 3 numéricas. No entanto, ao visualizar os dados, observou-se que a renda anual apresentava um comportamento mais próximo de uma variável discreta. Isso levou à sua conversão em uma característica discreta com base em quantis.

* As características numéricas não apresentavam uma distribuição explicitamente conhecida, sugerindo o uso de métodos não paramétricos para a comparação de modelos.

* Durante a análise de correlação, o método de Pearson revelou que as características mais fortemente correlacionadas com a coluna alvo eram o tempo gasto no site e a idade. Surpreendentemente, a renda anual apresentou a correlação mais negativa.

* Utilizando o método de Spearman, as correlações permaneceram semelhantes às observadas com o método de Pearson. Essa consistência sugere um baixo impacto de outliers e a ausência de fortes correlações não lineares.

* Os gráficos de KDE e de dispersão revelaram distribuições variáveis nas características de idade e renda anual dependendo do rótulo final. Essa observação sugere certa relevância dessas características na determinação da probabilidade de uma compra.

* Com base nos gráficos de barras que ilustraram a proporção de compras de casas para cada valor das características categóricas, observou-se que nem o gênero nem o clique em anúncios apresentaram desproporção significativa nas taxas de compra em relação ao equilíbrio original da coluna alvo. No entanto, a renda anual demonstrou certo nível de proporcionalidade inversa com a probabilidade de compra.

### Pré-processamento de Dados

* O dataset original continha valores ausentes e inconsistentes. Para lidar com isso, os valores inconsistentes foram substituídos por valores nulos. Posteriormente, todos os valores ausentes foram imputados utilizando um algoritmo baseado em KNN.

* A característica de renda anual, apresentando uma distribuição semelhante a uma variável discreta, foi convertida em uma característica categórica com base em quantis. Essa abordagem foi adotada para melhorar a interpretabilidade e facilitar a análise.

* Devido às escalas variadas presentes no dataset, as características foram padronizadas na etapa anterior ao treinamento para mitigar essas diferenças.

* Em uma tentativa de aproximar a distribuição das variáveis contínuas de uma distribuição Gaussiana, foi aplicada a função logarítmica. No entanto, essa transformação não trouxe mudanças significativas.

### Construção do Modelo



### Avaliação do Modelo



### Interpretação dos Resultados



### Recomendações para Melhoria



## Conclusão

#### English 🇺🇸

---

## Objective

The goal of this analysis is to predict whether a user of a real estate website will purchase a house based on their profile data. This includes variables such as age, annual income, gender, time spent on the site, and whether the user clicked on an ad.

## Dataset Overview
The dataset contains the following columns:
- **Age**: User's age.
- **Annual Income ($)**: User's annual income in dollars.
- **Gender**: User's gender (Female or Male).
- **Time on Site (min)**: Time spent browsing the website in minutes.
- **Ad Clicked**: Whether the user clicked on an advertisement (Yes or No).
- **Purchase**: Target variable indicating whether the user purchased a house (1 for Yes, 0 for No).

## Analysis and Results

To fully grasp the final results and conclusions, every step of the process will be thoroughly documented and critically discussed.

### Exploratory Data Analysis (EDA)

* The dataset exhibited imbalance with respect to the target feature with a 67% (did not buy) - 33% (did buy) proportion. Consequently, additional evaluation metrics beyond simple accuracy were considered. During model training, the ROC AUC metric was utilized, while the F1-score, along with recall and precision, were used to evaluate performance within the target classes.

* The dataset contained features with varying scales, necessitating standardization later in the process to mitigate its impact.

* The dataset included 2 categorical features and 3 numeric features. However, upon visualizing the data, it was observed that annual income exhibited behavior more similar to a discrete feature. This observation prompted its conversion to a discrete feature based on quantiles.

* The numeric features lacked an explicitly known distribution, suggesting the use of non-parametric methods for model comparison.

* During the correlation analysis, the Pearson method revealed that the features most strongly correlated with the target column were time spent on site and age. Surprisingly, annual income exhibited the most negative correlation.

* Using the Spearman method, the correlations remained similar to those observed with the Pearson method. This consistency suggests a low impact from outliers and an absence of strong non-linear correlations.

* The KDE plots and scatter plots revealed varying distributions in the age and annual income features depending on the final label. This observation suggests a certain degree of relevance for these features in determining the likelihood of a purchase.

* Based on the bar plots illustrating the ratio of house purchases for each value of the categorical features, it was observed that neither gender nor whether an ad was clicked showed significant disproportion in the purchase rates relative to the original target column's balance. However, annual income demonstrated some level of inverse proportionality with the likelihood of making a purchase.

### Data Preprocessing

* The original dataset contained missing and inconsistent values. To address this, inconsistent values were replaced with null values. Subsequently, all missing values were imputed using a KNN-based algorithm.

* The annual income feature, exhibiting a distribution resembling a discrete variable, was converted into a categorical feature based on quantiles. This approach was adopted to enhance interpretability and facilitate analysis.

* Due to the varying scales present in the dataset, the features were standardized in the step prior to training to mitigate their differences.

* In an attempt to make the continuous variables distribution closer to a gaussian distributions, the logarithm function was applied, but did not make a huge difference.

### Model Building




### Model Evaluation


### Interpretation of Results


### Recommendations for Improvement


## Conclusions