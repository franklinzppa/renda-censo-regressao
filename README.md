# renda-censo-regressao

<div align="center">
  
![header](img/header.jpg)
  
</div>

## Introdução

* O objetivo desse projeto é prever a renda de um grupo familiar utilizando informações relacionadas a sua residência. Trata-se, portanto, de um projeto de **regressão supervisionado offline**. 

* Uma aplicação possível desse projeto é utilizar o modelo como parte de um sistema de verificação de autodeclaração de renda. Esse sistema compararia a renda autodeclarada com a resposta do modelo de machine learning, a fim de verificar a integridade desse dado.

* Foi utilizada a métrica **MAE** (mean absolute error) para avaliar os modelos. Essa métrica foi escolhida para não penalizar excessivamente os erros grandes.

## Treinando modelos

* Os dados foram obtidos via consulta **SQL** utilizando a **API** do **BigQuery**, a partir do banco de dados do Censo Brasileiro de 2000, vindo da [Base dos Dados](https://basedosdados.org/).

* Trabalhou-se com um volume considerável de dados (23 features e 100000 instâncias) e foi realizada a **feature engineering** de dois novos atributos.

* O rendimento e se mostrou extremamente assimétrico, o que motivou a fazer o **tratamentos de outliers** e uma **log transformation** para tornar a variável mais normal.

* Os dados foram tratados com `OneHotEncoder` e `StandardScaler`.

* Os modelos treinados foram `RandomForestRegressor`, `XGBoostRegressor` e `LGBMRegressor` por se mostrarem mais adequados ao tamanho dos dados e por funcionarem bem com dados não lineares.

* A otimização dos hiperparâmetros foi feita utilizando a **Bayesian Optimization**.

## Resultados

* Em função das métricas e da perfomace computacional, o melhor modelo foi o `LGBMRegressor`.

<div align="center">

### Métricas de teste
Modelo | **MAE**   | MAPE | RMSE | $R^2$
-------| ---------  | -------- | ------ | -----
LGBM  | 503.9 | 64.5  | 1284.8  | 0.46

</div>

* O intervalo de confiança para o MAE ($\alpha = 95$%) foi [480.7, 527.0].


