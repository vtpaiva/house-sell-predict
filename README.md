# house-sell-predict

(All the notebooks codes, in `notebooks` folder, are also documented)

#### Português 🇧🇷

---

## **Objetivo**

O objetivo desta análise é **prever se um usuário de um site imobiliário comprará uma casa** com base nos dados de seu perfil. Isso inclui variáveis como **idade**, **renda anual**, **gênero**, **tempo gasto no site** e **se o usuário clicou em um anúncio**.

## **Visão Geral do Dataset**
O dataset contém as seguintes colunas:
- **Idade**: Idade do usuário.
- **Renda Anual ($)**: Renda anual do usuário em dólares.
- **Gênero**: Gênero do usuário (Feminino ou Masculino).
- **Tempo no Site (min)**: Tempo gasto navegando no site, em minutos.
- **Anúncio Clicado**: Indica se o usuário clicou em um anúncio (Sim ou Não).
- **Compra**: Variável alvo indicando se o usuário comprou uma casa (1 para Sim, 0 para Não).

## **Análise e Resultados**

Para compreender plenamente os resultados finais e as conclusões, **cada etapa do processo será rigorosamente documentada e analisada de forma crítica.**

### **Análise Exploratória de Dados (EDA)**

* O dataset apresentou um **desbalanceamento** em relação à variável alvo, com uma proporção de **67% (não compraram) - 33% (compraram).** Consequentemente, **métricas adicionais além da acurácia simples foram consideradas.** Durante o treinamento do modelo, foi utilizada a **métrica ROC AUC,** enquanto o **F1-score, recall e precisão** foram usados para avaliar o desempenho nas classes alvo.

* O dataset continha características com **escalas variadas**, exigindo **padronização** posteriormente para mitigar seu impacto.

* O dataset incluía **2 características categóricas e 3 numéricas.** No entanto, ao visualizar os dados, observou-se que **a renda anual apresentava um comportamento mais próximo de uma característica discreta.** Essa observação levou à sua **conversão em uma característica discreta baseada em quantis.**

* As **características numéricas não apresentavam uma distribuição explicitamente conhecida**, sugerindo o uso de **métodos não paramétricos para comparação de modelos.**

* Durante a **análise de correlação**, o **método de Pearson** revelou que as características mais fortemente correlacionadas com a variável alvo eram **tempo gasto no site e idade.** Surpreendentemente, **a renda anual apresentou a correlação mais negativa.**

* Utilizando o **método de Spearman**, as correlações permaneceram semelhantes às observadas com o método de Pearson. Essa consistência sugere um **baixo impacto de outliers** e a ausência de **fortes correlações não lineares.**

* Os **gráficos KDE e de dispersão** revelaram **distribuições variáveis nas características de idade e renda anual dependendo do rótulo final.** Essa observação sugere um **certo grau de relevância dessas características** na determinação da probabilidade de compra.

* Com base nos **gráficos de barras que ilustraram a proporção de compras de casas para cada valor das características categóricas**, observou-se que nem o **gênero nem o clique em anúncios apresentaram desproporção significativa** nas taxas de compra em relação ao equilíbrio original da variável alvo. No entanto, **a renda anual demonstrou certo nível de proporcionalidade inversa** com a probabilidade de compra.

### **Pré-processamento de Dados**

* O dataset original continha **valores ausentes e inconsistentes.** Para lidar com isso, os **valores inconsistentes foram substituídos por valores nulos.** Posteriormente, todos os **valores ausentes foram imputados utilizando um algoritmo baseado em KNN.**

* A **característica de renda anual,** apresentando uma distribuição semelhante a uma variável discreta, foi **convertida em uma característica categórica baseada em quantis.** Essa abordagem foi adotada para **melhorar a interpretabilidade e facilitar a análise.**

* Devido às **escalas variadas** presentes no dataset, as características foram **padronizadas** na etapa anterior ao treinamento para **mitigar essas diferenças.**

* Em uma tentativa de **aproximar a distribuição das variáveis contínuas de uma distribuição Gaussiana,** foi aplicada a **função logarítmica,** mas **não trouxe mudanças significativas.**

### **Construção do Modelo**

* Durante o treinamento, o **método de validação cruzada** foi empregado para **aumentar a robustez do modelo.** Utilizando as **pontuações médias dos testes,** avaliou-se a **variação do desempenho da hipótese com base em diferentes configurações de hiperparâmetros.**

* O **algoritmo de Regressão Logística** inicialmente demonstrou um **alto grau de underfitting,** indicando que **limites de decisão lineares sozinhos são insuficientes** para capturar os **padrões complexos necessários para uma pontuação satisfatória.**

* Para permitir que a **Regressão Logística** capturasse alguns **padrões não lineares,** foi aplicado o método de **pré-processamento de características polinomiais** ao dataset. No entanto, o **viés da hipótese permaneceu consideravelmente alto,** e conforme o **grau polinomial aumentava, o nível de overfitting também escalava.**

* O **algoritmo Random Forest** inicialmente exibiu um **alto nível de overfitting** com **variância moderada e viés significativo.** No entanto, com a aplicação de **técnicas de regularização, o overfitting foi mitigado,** embora o **viés permanecesse alto.**

* Por fim, foi realizada uma **validação cruzada com hiperparâmetros selecionados aleatoriamente** no modelo Random Forest, mas os **resultados não mostraram melhora significativa.**

### **Avaliação do Modelo**

* Com **ROC AUC como a principal métrica de avaliação,** as hipóteses foram avaliadas com base em seu **viés e variância** utilizando o **histograma de pontuação média dos testes da validação cruzada.**

* Foram realizadas **avaliações específicas por classe** utilizando o **relatório de classificação,** com foco em **recall, precisão e F1-score** como as principais métricas de análise.

* Devido à **falta de uma distribuição explícita de dados,** foi aplicado o **método de reamostragem bootstrap, aproveitando sua natureza não paramétrica.** Isso envolveu o cálculo do **ROC AUC em várias reamostragens,** proporcionando uma **visualização mais clara da variação, viés e pontuações médias das hipóteses.**

* Além disso, o **teste de Nemenyi, um método de avaliação não paramétrico,** foi empregado para verificar se **existiam diferenças significativas entre os modelos.** A **hipótese Random Forest** demonstrou as **maiores diferenças entre os modelos.**

* Os **modelos Random Forest** foram considerados os **melhores no geral** devido ao seu **desempenho superior nas principais métricas avaliadas.**

### **Interpretação dos Resultados**

* Em ambos os modelos, as **características mais importantes foram o tempo gasto no site e a idade,** destacando sua **relevância para as previsões.**

* O **modelo baseado em Regressão Logística** apresentou um **nível mais consistente de importância entre todas as características,** enquanto os **outros modelos atribuíram maior importância ao tempo gasto no site e à idade.**

### **Recomendações para Melhorias**

* Experimentar com **algoritmos de treinamento capazes de criar limites de segmentação mais complexos** para extrair padrões que **Regressão Logística e Random Forest podem ter perdido.**

* Explorar **hiperparâmetros alternativos e métodos de regularização** para alcançar um **equilíbrio entre alto ajuste aos dados e manutenção da capacidade de generalização.**

## **Conclusão**

A análise destacou a **importância de características como tempo gasto no site e idade** na previsão de compras de casas. A Regressão Logística **enfrentou dificuldades com underfitting,** enquanto o Random Forest **demonstrou melhor desempenho,** apesar de algum viés. Métodos de validação cruzada e avaliações não paramétricas confirmaram o **Random Forest como o melhor modelo** com base nas principais métricas, mas a exploração de **algoritmos avançados e técnicas de regularização** ainda é necessária para melhorar a generalização e capturar **padrões mais complexos.**

#### English 🇺🇸

---

## **Objective**

The goal of this analysis is to **predict whether a user of a real estate website will purchase a house** based on their profile data. This includes variables such as **age**, **annual income**, **gender**, **time spent on the site**, and **whether the user clicked on an ad**.

## **Dataset Overview**
The dataset contains the following columns:
- **Age**: User's age.
- **Annual Income ($)**: User's annual income in dollars.
- **Gender**: User's gender (Female or Male).
- **Time on Site (min)**: Time spent browsing the website in minutes.
- **Ad Clicked**: Whether the user clicked on an advertisement (Yes or No).
- **Purchase**: Target variable indicating whether the user purchased a house (1 for Yes, 0 for No).

## **Analysis and Results**

To fully grasp the final results and conclusions, **every step of the process will be thoroughly documented and critically discussed.**

### **Exploratory Data Analysis (EDA)**

* The dataset exhibited **imbalance** with respect to the target feature, with a **67% (did not buy) - 33% (did buy)** proportion. Consequently, **additional evaluation metrics beyond simple accuracy were considered.** During model training, the **ROC AUC metric** was utilized, while the **F1-score, recall, and precision** were used to evaluate performance within the target classes.

* The dataset contained features with **varying scales**, necessitating **standardization** later in the process to mitigate its impact.

* The dataset included **2 categorical features and 3 numeric features.** However, upon visualizing the data, it was observed that **annual income exhibited behavior more similar to a discrete feature.** This observation prompted its **conversion to a discrete feature based on quantiles.**

* The **numeric features lacked an explicitly known distribution**, suggesting the use of **non-parametric methods for model comparison.**

* During the **correlation analysis**, the **Pearson method** revealed that the features most strongly correlated with the target column were **time spent on site and age.** Surprisingly, **annual income exhibited the most negative correlation.**

* Using the **Spearman method**, the correlations remained similar to those observed with the Pearson method. This consistency suggests a **low impact from outliers** and an absence of **strong non-linear correlations.**

* The **KDE plots** and **scatter plots** revealed **varying distributions in the age and annual income features depending on the final label.** This observation suggests a **certain degree of relevance for these features** in determining the likelihood of a purchase.

* Based on the **bar plots illustrating the ratio of house purchases for each value of the categorical features,** it was observed that neither **gender nor whether an ad was clicked showed significant disproportion** in the purchase rates relative to the original target column's balance. However, **annual income demonstrated some level of inverse proportionality** with the likelihood of making a purchase.

### **Data Preprocessing**

* The original dataset contained **missing and inconsistent values.** To address this, **inconsistent values were replaced with null values.** Subsequently, all **missing values were imputed using a KNN-based algorithm.**

* The **annual income feature**, exhibiting a distribution resembling a discrete variable, was **converted into a categorical feature based on quantiles.** This approach was adopted to **enhance interpretability and facilitate analysis.**

* Due to the **varying scales** present in the dataset, the features were **standardized** in the step prior to training to **mitigate their differences.**

* In an attempt to **make the continuous variables' distribution closer to a Gaussian distribution,** the **logarithm function** was applied, but **did not make a significant difference.**

### **Model Building**

* During the training step, the **cross-validation method** was employed to **enhance the model's robustness.** Using the **mean test scores,** it evaluated the **performance variation of the hypothesis based on different hyperparameter configurations.**

* The **Logistic Regression algorithm** initially demonstrated a **high degree of underfitting,** indicating that **linear decision boundaries alone are insufficient** to capture the **complex patterns needed for a satisfactory score.**

* To enable **Logistic Regression** to capture some **non-linear patterns,** the **polynomial features preprocessing method** was applied to the dataset. However, the **hypothesis bias remained considerably high**, and as the **polynomial degree increased, the level of overfitting also escalated.**

* The **Random Forest algorithm** initially exhibited a **high level of overfitting** with **moderate variance and significant bias.** However, with the application of **regularization techniques, overfitting was mitigated,** though the **bias remained high.**

* Finally, a **cross-validation with randomly selected hyperparameters** was performed on the Random Forest model, but the **results showed no significant improvement.**

### **Model Evaluation**

* With **ROC AUC as the primary evaluation metric**, the hypotheses were assessed based on their **bias and variance** using the **mean test score histogram from cross-validation.**

* **Class-specific evaluations** were conducted using the **classification report,** focusing on **recall, precision, and F1-score** as the main metrics for analysis.

* Due to the **lack of an explicit data distribution,** the **bootstrap resampling method, leveraging its non-parametric nature,** was applied. This involved calculating the **ROC AUC across multiple resamples,** providing a **clearer visualization of hypothesis variation, bias, and mean scores.**

* Additionally, the **Nemenyi test, a non-parametric evaluation method,** was employed to verify whether **significant differences existed between the models.** The **Random Forest hypothesis** demonstrated the **largest differences among the models.**

* The **Random Forest models** were considered the **best overall** due to their **superior performance on the primary metrics evaluated.**

### **Interpretation of Results**

* In both models, the **most important features were time spent on the website and age,** highlighting their **significance in making predictions.**

* The **Linear Regression-based model** exhibited a **more consistent level of importance across all features,** whereas the **other models assigned greater importance to time spent on the website and age.**

### **Recommendations for Improvement**

* Experiment with **training algorithms capable of creating more complex segmentation boundaries** to extract patterns that **Logistic Regression and Random Forest may have missed.**

* Explore **alternative hyperparameters and regularization methods** to achieve a **balance between high fitting to the data and maintaining generalization capabilities.**

## **Conclusion**

The analysis highlighted the **importance of features like time spent on the website and age** in predicting house purchases. Logistic Regression **struggled with underfitting,** while Random Forest **demonstrated better performance** despite some bias. Cross-validation and non-parametric methods confirmed **Random Forest as the best model** based on key metrics, but further exploration of **advanced algorithms and regularization techniques** is needed to improve generalization and capture **more complex patterns.**