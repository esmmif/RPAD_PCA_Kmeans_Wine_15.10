# RPAD_PCA_Kmeans_Wine_15.10

# Análise de Clusterização do Wine Dataset via PCA e K-Means

Este repositório contém um notebook em Python que implementa um fluxo de análise não supervisionada, utilizando Análise de Componentes Principais (PCA) para redução de dimensionalidade e o algoritmo K-Means para clusterização.

O projeto demonstra a aplicação dessas técnicas no dataset "Wine" da biblioteca `scikit-learn`.

Esse projeto é parte da disciplina de Reconhecimento de Padrões, do curso de Ciência da Computação do Instituto Federal de Educação e Tecnologia do Ceará, aluno Iuri A. Esmeraldo.

---

## Objetivo Técnico

O objetivo central é particionar as 178 amostras do Wine dataset em clusters homogêneos, com base em suas 13 características químicas. O processo envolve duas etapas principais:

1.  **Pré-processamento com PCA:** Reduzir o espaço de features de 13 para 2 dimensões, preservando o máximo de variância possível para facilitar a clusterização e permitir a visualização.
2.  **Clusterização com K-Means:** Aplicar o algoritmo K-Means sobre os dados projetados nos componentes principais para identificar os agrupamentos intrínsecos.

A análise final consiste em comparar visualmente os clusters resultantes com as classes verdadeiras do dataset (tipos de vinho) para avaliar a performance da metodologia.

---

## Dataset

-   **Fonte:** `sklearn.datasets.load_wine`
-   **Número de Amostras:** 178
-   **Número de Features:** 13 (variáveis químicas contínuas)
-   **Número de Classes:** 3 (correspondentes a três produtores distintos)

---

## Metodologia Implementada

O script segue uma sequência lógica de pré-processamento e modelagem.


### 1. Carregamento e visualização
O dataset é carregado e são exibidos alguns de seus dados.

### 2. Padronização dos Dados

As features do dataset possuem escalas e variâncias distintas. Como o PCA é um algoritmo baseado em variância, a padronização é um passo mandatório para garantir que todas as variáveis contribuam de forma equitativa para a extração dos componentes. Utilizou-se o `StandardScaler` do `scikit-learn` para transformar cada feature para ter média 0 e desvio padrão 1 (Z-Score).

### 3. Análise de Componentes Principais (PCA)

Após a padronização, o PCA foi aplicado para reduzir o número de dimensões de 13 para 2. O resultado desta etapa são os dois primeiros componentes principais, que representam as direções de maior variância nos dados. A variância total explicada por esses dois componentes é de **55.41%** (PC1: 36.20%, PC2: 19.21%), indicando que mais da metade da informação estrutural dos dados foi retida.

### 4. Clusterização K-Means

O algoritmo K-Means foi então ajustado aos dados transformados pelo PCA (`X_pca`). Foi pré-definido o número de clusters (`k=3`), pois este é o número de classes conhecido no dataset. Em um cenário puramente não supervisionado, o valor de `k` seria determinado por métodos como o "Método do Cotovelo" (Elbow Method). O K-Means particionou os dados em 3 clusters com base na minimização da inércia (soma das distâncias quadráticas intra-cluster).

### 5. Validação e Visualização

A validação do resultado da clusterização foi realizada de forma qualitativa, através da comparação de dois gráficos de dispersão:

1.  **Gráfico 1:** Plota os dados no espaço dos 2 componentes principais, coloridos pelos rótulos atribuídos pelo K-Means. Os centroides de cada cluster são destacados.
2.  **Gráfico 2:** Plota os mesmos dados, mas coloridos pelos rótulos verdadeiros (classes originais do dataset).

A alta correspondência visual entre as cores e a distribuição dos clusters nos dois gráficos demonstra a eficácia da combinação PCA + K-Means para este problema.

---

## Como Executar

1.  **Ambiente:** O código foi desenvolvido para ser executado em ambientes como Jupyter Notebook ou Google Colab.
2.  **Dependências:** As bibliotecas necessárias estão listadas no topo do script e podem ser instaladas via pip:
    ```bash
    pip install pandas numpy scikit-learn matplotlib seaborn
    ```
3.  **Execução:** Execute as células do notebook `RPAD_PCA_Wine_09_10.ipynb` sequencialmente.

---

## Conclusão

Este trabalho ilustra um pipeline eficaz onde o PCA é utilizado não apenas para visualização, mas também como uma etapa de pré-processamento que simplifica o espaço de features para um algoritmo de clusterização. A análise demonstra que a redução para 2 componentes principais foi suficiente para que o K-Means identificasse com alta precisão os três grupos distintos de vinhos, validando a metodologia como uma abordagem robusta para a descoberta de padrões em dados multidimensionais.
