# Projeto-C318: Detetecção de Fraudes e anomalias com Modelo Semi-Supervisionado

Nesse Projeto estamos usando o Famoso Dataset Creditcard.csv que possui dados de várias transações bancárias em bancos europeus.

<img src='./images/Credit-cards.jpg' width=500px>

Os dados já possuem um Target mostrando o que é Anomalia e o que não é. As variáveis possuem um Teor secretivo. Estão definidas como (V1, V2, V3, V8, ...., V28) entaõ não é possível saber do que elas falam.
Mas isso pouco importa porque já possuimos a Target. Só precisamos relacionar os dados. Isso provavelmente foi feito nesse Dataset por questão de segurança, já que os dados tratam de transações bancárias que, por sua vez, são dados sensíveis.

<img src='./images/cyber.jpg' width=500px>


#### Pré-Processamento

Para processar os dados aplicamos o PCA para reduzir a dimensionalidade do Dataset Original, visto que ele possuía 28 variáveis. Foi diminuido para 20, o que no final aumentou a precisão do modelo.

#### Primeiro Modelo: Isolation Forest

Usamos o Isolation Forest, um modelo não-supervisionado para detecção de anomalia, para segmentar os Outliers.
O Isolation Forest já segmenta as anomalias nos primeiros nós das Árvores. Uma comparação é feita com os níveis das itrees geradas para chegar a um resultado.

<img src='./images/isoforest.png' width=500px>

Mesmo após a utilização do modelo, ainda não temos confirmado todas as anomalias.
Precisamos passar os dados anomolos por um classificador.

#### Segundo Modelo: Classificador RandomForest

Após termos separados nossos conjuntos de dados anomalos, devemos fazer uma classificação para que o modelo possa identificar as anomalias. 

<img src='./images/Rforest.png' width=500px>

Random Forest é um modelo supervisionado que também segmenta os dados, mas usa as labels como referência.

#### Métricas de Avaliação: Precision e Recall

Ao final do treinamento de ambos os modelos, foi aplicado os conceitos de Precision e Recall. É necessário saber quantos falsos positivos há no modelo e quantos falsos negativos existem. Não podemos classificar toda anomalia como ameaça, mas também não podemos deixar muitas anomalias livres da inspeção.

<img src='./images/PandR.png' width=500px>

Aplicando as métricas tivemos ao final do primeiro modelo:

Precisão somente com o Isolation Forest: 0.07
Revocação somente com o Isolation Forest: 0.85

E ao final do Segundo:

Precisão após classificador supervisionado: 0.96
Revocação após classificador supervisionado: 0.92

Ao final, gerei um mapa de calor para mostrar quantos Falsos Positivos, Falsos negativos, Verdadeiros positivos e Verdadeiros Negativos houveram.

<img src='./images/PandR2.png' width=500px>
