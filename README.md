# Link Prediction in Social Network using Machine Learning

    - Facultad de Ingeniería de la Universidad de Buenos Aires.
    - Asignatura: Teoría de Algoritmos II.
    - Profesor: Martín Buchwald.
    - Alumno: Lucas Biló.

En este trabajo se realizó la predicción de links de una red social utilizando Machine Learning.

El dataset utilizado se obtuvo de aquí: https://www.kaggle.com/datasets/andreagarritano/twitch-social-networks

Para el set de test se utilizo una fracción random del 20% del dataset original. Ya que el set de test brindado no sirve para la predicción que yo estoy realizando, apunta hacia otro lado.

El dataset contaba con únicamente nodos que estaban conectados (justamente la red), así que genere nuevos datos de nodos que no estaban conectados. Ya que para la predicción que voy a realizar, se necesitan nodos que esten conectados (target = 1) y que no lo esten (target = 0).

La metrica utilizada para comparar fue **auc roc** (Area Under the Receiver Operating Characteristic Curve, https://www.analyticsvidhya.com/blog/2020/06/auc-roc-curve-machine-learning/). Al final de los modelos, se gráfico la matriz de confusión y el top de los features más importantes (si es posible).

Otra cosa para comentar, es que se utilizo el **Randomized Search** para buscar los mejores **hiperparametros** para los distintos modelos. Estos hiperparametros serán los que mejor se adecuen al modelo para obtener una mejor predicción en train. Se probaron varios según el modelo, aunque en algunos casos se setearon menos ya que el entrenamiento y prueba de dichos parametros puede tardar muchisimo.

---
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
---
### **Resultados**:

AUC ROC:

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

Matriz de confusión:

<center>

| Modelo | TP | FP | TN | FN |
| ------ | ---- | ---- | ---- | ---- |
| XGB | 3937 | 66 | 11844 | 7902 |
| RF  | 3213 | 44 | 11866 | 8626 | 
| KNN | 8582 | 1500 | 10410 | 3257 |
| SVM | 536 | 8 | 11902 | 11303 |
| MLP | 1044 | 15 | 11895 | 10795 |

</center>

---

### **Conclusiones**:

El modelo que mayor score consiguio fue el XGBoost, muy cerca estuvo el RF y KNN. Por lo tanto, con el featuring que se realizo este modelo es el mejor para predicir al set de test seleccionado.

Se pueden ver varias diferencias en la matriz de confusión. Por ejemplo, el KNN tuvo una mayor cantidad de verdaderos positivos, pero muchos mas falsos positivos que el resto. En general, se puede ver que los modelos funcionan mejor para la predicción de no-links (target = 0) y no tan bien para conexiones posibles (target = 1).

Solo se pudo calcular los features que más importancia tomaron para los modelos XGB y RF. En ambos casos fueron muy parecidos, donde el top fue: el camino más corto, el Preferential Attachment y los siguiendo.