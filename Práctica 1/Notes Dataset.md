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
1. PRISM: problemas con variables numéricas aunque no estaban llegando dichas variables numéricas

# Datasets

## 01: Heart Disease

- No he podido usar PRISM por problemas con variables numéricas aunque estaba pre-procesando los datos correctamente
1. Variables correladas
    - El siguiente grupo de variables están muy correladas:
        - ExerciseAngina
        - Oldpeak
        - ST_SLOPE (la que más correlación tiene con la clase de salida)
        - HeartDisease
    - HeartDisease con ChestPainType
2. Borramos las filas que tengan missing values. Mirando la tabla de entrada y la tabla de salida, vemos que no hemos encontrado missing values
3. La clase 0 tiene 508 ejemplos, la clase 1 tiene 410. Hay un ligero balanceo pero no es demasiasdo importante
4. En el *Exploratory Data Analysis* muestra que tenemos bastantes outliers. En cada *cross-validation*, borramos solo en training usando `3 * IQR`
5. Cross validation funciona, pero las curvas ROC por algun motivo no se muestran bien
6. No tenemos algoritmos con resultados catastróficos
7. Ajustamos los valores de Random Forest y de Redes neuronales
    - Usamos `Parameter Optimization Loop`
    - Para las redes neuronales, tenemos que quitar los missing values y la normalizacion para que vaya bien. Esto provoca que los resultados sean muy malos
8. Borramos las variables que están muy correladas y vemos que pasa
    - Del grupo, me quedo con `ST_SLOPE` porque es la que más correlada está con `HeartDisease`
