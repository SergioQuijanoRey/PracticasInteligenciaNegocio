# Qué deberíamos explorar en cada dataset

- Preprocesado de los datos (**probar empíricamente** si este preprocesado mejora o empeora los algoritmos)
    1. Variables muy correladas linealmente entre ellas
        - Probar con borrar estas variables correladas
    2. Missing values
        - Probar con imputar *missing values*
    3. Clase de salida desbalanceada
        - Probar con SMOTE para generar un mejor balanceo
    4. Outliers
        - Probar con borrar los outliers con `3 * IQR`
- Cross Validation concreto
    5. Comprobar que cross validation funciona
    6. Comprobar que no haya algoritmos en Cross Validation con resultados catastróficos (esto demuestra algún fallo concreto en el problema)
- Ajustar un par de algoritmos
    7. Ajustar los valores para un par de parámetros

# Técnicas avanzadas que probar al menos una vez

- [ ] Usar un árbol de decisión para medir la importancia de las variables
    - Una vez hecho eso, probar con quitar las variables que no han tenido importancia
- [ ] Borrado del ruido usando un *Ensemble filter* o similar
- [ ] Imputar missing values usando un predictor
- [ ] Reducción de datos para un problema que tenga demasiadas categorías
- [ ] Balancear clases usando *SMOTE*

# Algoritmos que me han dado problemas

- Algoritmos que me han dado problemas, y que por tanto no he podido usar:
1. Random Forest: con el X-Aggregator
2. PRISM: problemas con variables numéricas aunque no estaban llegando dichas variables numéricas

# Datasets

## 01: Heart Disease

- No he podido usar *Random Forest* porque el `X-Aggregator` fallaba por algún motiva
