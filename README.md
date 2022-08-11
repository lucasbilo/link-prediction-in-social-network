# Link Prediction in Social Network using Machine Learning

    - Facultad de Ingeniería de la Universidad de Buenos Aires.
    - Asignatura: Teoría de Algoritmos II.
    - Profesor: Martín Buchwald.
    - Alumno: Lucas Biló.

En este trabajo se realizó la predicción de links de una red social utilizando Machine Learning.

El dataset utilizado se obtuvo de aquí: https://www.kaggle.com/datasets/andreagarritano/twitch-social-networks

Para el set de test se utilizo una fracción random del 20% del dataset original. Ya que el set de test brindado no sirve para la predicción que yo estoy realizando, apunta hacia otro lado.

El dataset contaba con únicamente nodos que estaban conectados (justamente la red), así que genere nuevos datos de nodos que no estaban conectados. Ya que para la predicción que voy a realizar, se necesitan nodos que esten conectados (target = 1) y que no lo esten (target = 0).

La metrica utilizada para comparar fue **auc roc** (Area Under the Receiver Operating Characteristic Curve). Al final de los modelos, se gráfico la matriz de confusión y el top de los features más importantes.

---
### **Desarrollo**:

El trabajo se encuentra divido principalmente en 3 partes:

1) **EDA**: Analisis de la red y preparación de la misma para el encoding.
2) **Featuring**: se calcularon distintos features de la red:
    - Seguidores/Siguiendo de cada nodo
    - Devuelve el seguido
    - Comunidades
    - Camino más corto
    - Indice de Katz
    - HITS (Hubs and Authorities)
    - Page Rank
    - Distancia Jaccard
    - Distancia Coseno
    - Preferential Attachment

3) Finalmente se desarrollaron distintos modelos:
    - XGBoost
    - Random Forest
    - K-nearest neighbors
    - SVM (Support Vector Machines)
    - Multi-layer Perceptron

---
### **Resultados**:
<center>

| Modelo | Score (train) | Score (test)|
| ------ | ------------- | ----------- |
| XGB | 0.9666 | 0.8916 |
| RF  | 0.9645 | 0.8902 |
| KNN | 0.9407 | 0.8861 |
| SVM | 0.9208 | 0.8479 |
| MLP | 0.9177 | 0.8143 |

</center>

---

### **Conclusiones**:

El modelo que mayor score consiguio fue el XGBoost, muy cerca estuvo el RF y KNN. El feature que mas importancia tomo fue el del camino más corto, seguido por otros calculados en la parte 2. Ninguno de los features que venían con el dataset original tuvo mayor importancia.