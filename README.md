# DengAi
Predicción de casos de fiebre de Dengue mediante algoritmos de aprendizaje supervisado.

Datos obtenidos del sitio web de Driven Data.

**Participante**: Diego Pastor Bonet

**Datos del modelo final elegido**
* MAE test (DrivenData): 27.4543
* MAE validación: 18.46917808219178
* Algoritmo ML: Clustering K-means, Regresión Lineal
* Hiperparámetros: 
  * n = 3 
  * max_iter = 300 
  * tol = 0.01
* Lista de características:

  * year
  * weekofyear
  * precipitation_amt_mm
  * reanalysis_air_temp_k
  * reanalysis_avg_temp_k
  * reanalysis_max_air_temp_k
  * reanalysis_min_air_temp_k
  * reanalysis_precip_amt_kg_per_m2
  * reanalysis_relative_humidity_percent
  * reanalysis_specific_humidity_g_per_kg
  * station_avg_temp_c
  * station_diur_temp_rng_c
  * station_max_temp_c
  * station_min_temp_c
  * station_precip_mm
  * season
  * city_bin
  * ndvi_avg
  * etiqueta

 
A lo largo de este análisis se elaborará un modelo de predicción que podrá ser puestos a prueba en la web de DrivenData.

En primer lugar se hará un procesado teniendo en cuenta las necesidades estructurales de la competición.

Se escogerán los mejores candidatos a algoritmos de agrupamiento, a continuación, se probarán también varios modelos de predicción para encontrar el mejor posible. Finalmente, todo esto será puesto a prueba mediante un conjunto de validación y posteriormente por la web mediante un conjunto de test. La métrica que se utilizará para evaluar los modelos será el error absoluto medio (MAE) aportado por DrivenData.

El objetivo será alcanzar el menor valor de MAE entregando diferentes intentos con combinaciones de grupos de características y algoritmos a esta web.

En base a esta métrica, el conjunto de datos mejor valorado ha sido el conformado por el conjunto de datos original, al que se le ha añadido la etiqueta de cluster generada por el algoritmo K-Means con tres clusters. Este es además el algoritmo de agrupamiento que mejor resultado obtuvo en la práctica anetrior. El modelo de predicción que mejor ha funcionado es el de Regresión Lineal.

Otras combinaciones como una sub-selección de características, diferentes modelos de predicción o diferentes algoritmos de agrupamiento han dado todos peores resultados que éste, sin embargo, aún hay espacio para seguir investigando, especialmente con diferentes conjuntos de características.

---
# Conclusiones
---

| Modelo | MAE test (DrivenData) | MAE validación | Algoritmo | Hiperparámetros | 
| --- | --- | --- | --- | --- 
| svm_kmeans_n3 | 32.6130 | 16.7671 | K-Means - SVM | n_clusters=3, n_init=10, max_iter = 300, tol = 0.01 
| knn_kmeans_n5 | 30.7981 | 16.5651 | K-Means - KNN | n_neighbors=5, n_clusters=3, n_init=10, max_iter = 300, tol = 0.01 
| tree_kmeans_n3 | 30.9351 | 13.8527 | K-Means - Árbol de decisión | random_state=0, n_clusters=3, n_init=10, max_iter = 300, tol = 0.01 
| regres_kmeans_n3 | 27.4543 | 18.4692 | K-Means - Regresión Lineal | n_clusters=3, n_init=10, max_iter = 300, tol = 0.01 
| regres_kmeans_n2 | 29.5697 | 19.1781 | K-Means - Regresión Lineal | n_clusters=2, n_init=10, max_iter = 300, tol = 0.01 
| regres_dbscan  | 29.9904 | 17.8356 | DBSCAN - Regresión Lineal | eps=0.7, min_samples = 3 
| regres_kmeans_n3_reduct | 29.9591 | 18.8288 | K-Means - Regresión Lineal | n_clusters=3, n_init=10, max_iter = 300, tol = 0.01 

El modelo elegido es por tanto regres_kmeans_n3 puesto que obtiene el mejor resultdo en la validación de MAE de la página web de DrivenData.

Al poder contar con varios algoritmos de aprendizaje supervisado, como lo son SVM, KNN, el Árbol de decisión o la Regrsión Lineal hemos sido capaces de identificar cuál genera mejor resultado y proceder a optimizarlo.

Lo mismo ha sucedido con los algoritmos de agrupamiento que utilizamos en la actividad anterior. En esta actividad ya fueron validados y se seleccionó el mejor, pero se le ha dado una nueva oportunidad al DBSCAN y se ha probado a utilizar dos clsuters en K-Means.

Ha sido sorprendente el pobre resultado que ha tenido el modelo regres_kmeans_n3_reduct, pues se esperaba que el hecho de reducir el número de características iba a afectar positivamente al modelo. Al final no ha ocurrido así, muy posiblemente porque no se ha hecho la selección más adecuada de características.

Cabe señalar que las evaluaciones de MAE en el conjunto de validación no se correlacionan con las de la web, esto es curioso dado que los datos del conjunto de validación no alimentan los modelos y no debería haber overfitting.

Sin embargo, a la vista de los resultados, queda claro que se ha incurrido en alguna clase de sesgo durante la elaboración de los modelos, tal vez algún overfitting que no somos capaces de detectar.

Cabe también mencionar que durante la optimización de hiperparámetros del algoritmo K-Means, la variación de los parámetros n_init, max_iter y tol (iniciación de centroides, número máximo de iteraciones y tolerancia) no afecta nada en absoluto a los resultados de los clusters. Esto puede ser porque los clusters están muy bien separados y existe una tendencia muy marcada a alcanzar ese resultado que no puede ser modificada por estos parámetros.

El resultado final de MAE = 27.4543 de DrivenData se considera exitoso puesto que supera la barrera de 28.9111 impuesta por el profesor.
Es posible que se pudiera haber mejorado aún más mediante nuevas selecciones de características distintas a la realizada, sin embargo, la limitación de intentos en la página web ha sido un escollo en este aspecto.

---
# Competición
---

![image](https://github.com/user-attachments/assets/0292aa99-0739-491b-b2cb-503633b7a6ab)

Mejor resultado corresponde al modelo regres_kmeans_n3.

![image](https://github.com/user-attachments/assets/37d7e67c-6e2f-4999-adf3-78ae271d5f72)

