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
    7. Comprobar que la curva ROC se visualiza correctamente
- Ajustar un par de algoritmos
    8. Ajustar los valores para un par de parámetros
        - Intento ajustar G-mean, pero con el nodo `loop_end`, que espera una varible flow, no se puede actualizar el G-Mean (o al menos no sé cómo hacer eso)

# Técnicas avanzadas que probar al menos una vez

- [ ] Usar un árbol de decisión para medir la importancia de las variables
    - Una vez hecho eso, probar con quitar las variables que no han tenido importancia
- [ ] Borrado del ruido usando un *Ensemble filter* o similar
- [ ] Imputar missing values usando un predictor
- [x] Reducción de datos para un problema que tenga demasiadas categorías
    - Lo he hecho en el primer dataset
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
7. La curva ROC se muestra mal para un par de algoritmos
    - En la memoria, con Latex mostrar también las curvas ROC de formas individuales en un mosaico
8. Ajustamos los valores de Random Forest y de Redes neuronales
    - Usamos `Parameter Optimization Loop`
    - Para las redes neuronales, tenemos que quitar los missing values y la normalizacion para que vaya bien. Esto provoca que los resultados sean muy malos
9. Borramos las variables que están muy correladas y vemos que pasa
    - Del grupo, me quedo con `ST_SLOPE` porque es la que más correlada está con `HeartDisease`

-------------------------------------------------------------------------------

## 02: Mobile Prizes

- Aplicando PCA con dimensión 2 se ven muy buenos resultados
- Deberíamos hacer las métricas para cada una de las clases. Sin embargo nos quedamos con la clase 1 como clase positiva
- En Support Vector Machine, no estamos haciendo la adaptación a multiclase. Probar con un One-To-One o similares
- En redes neuronales, también estamos teniendo problemas por ser un problema multiclase
- Todos estos problemas los podemos vender como problemas de los algoritmos. También lo podemos vender como problemas de KNIME para generar estructuras complejas
    - Es muy complicado hacer una adaptación tipo One vs All
    - No se pueden usar redes neuronales con softmax en la capa de salida
- **Bonus**: hemos aplicado PCA para el proceso de aprendizaje
    - Además aplicamos PCA de forma correcta
    - Es decir, separamos en training y test, calculamos sobre training y aplicamos esto tanto en training como en test
1. Variables Correladas
    - Memoria RAM muy correlada con la variable de salida
    - Los dos valores para los píxeles están muy correlados entre sí, como era de esperar
    - `sc_w` y `sc_h` muy correladas entre sí
2. Missing Values
    - No hay missing values en el dataset
3. Clase de salida desbalanceada
    - Las clases están perfectamente balanceadas
4. Outliers
    - Vemos que tenemos bastantes outliers
    - Por tanto, en cada cross validation borramos outliers con `3*IQR`
5. Cross Validation funciona
    - Obtenemos los resultados de forma correcta
6. Algoritmos con resultados catastróficos
    - Tres algoritmos tienen resultados catastróficos (miramos G-Mean)
        - Redes neuronales: en KNIME no podemos especificar más de una neurona de salida con SoftMax
        - Support Vector machine sin normalizar: la falta de normalización junto con la no adaptación a multiclase
        - Support Vector machine normalizado: no tenemos adaptación a multiclase
7. Comprobar que la curva ROC se visualiza correctamente
    - Parece que se visualiza correctamente la curva ROC
    - Sin embargo, se ve que los resultados no son tan buenos como deberían
    - Notar que estamos visualizando la curva ROC de una sola clase, y no de las cuatro clases
8. Ajustar los valores de un par de algoritmos
    - Los mejores algoritmos que hemos encontrado son (mirando G-Mean):
        - Naive Bayes
        - Random Forest
        - K-NN
    - Ajusto los parámetros de:
        - Random Forest: se consigue una buena optimización del Accuracy
        - Naive Bayes: intento ajustar algunos parámetros pero no consigo modifcar el accuracy
        - K-NN: obtenemos muy buenos resultados
9. En el EDA, vemos que PCA de tamaño 2 genera muy buenos resultados (muy buena separación)
    - Por esto, era de esperar los buenos resultados de K-NN obtenidos

-------------------------------------------------------------------------------

## 03: Bank Marketing

- Dataset mucho más grande, los modelos tardan mucho más en entrenarse
- PCA en dos dimensiones no muestra muy buenos resultados
- Hay atributos que tienen muchos valores constantes
    - Por ejemplo, `pdays` tiene casi todos los valores en 999.
    - En UCI vemos que esto significa que el cliente no ha sido contactado
- En la página de UCI especifican que no hay *missing values*, así que suponemos que estos valores no son *missing values*
- En el **paper original** *S. Moro, P. Cortez and P. Rita. A Data-Driven Approach to Predict the Success of Bank Telemarketing. Decision Support Systems, Elsevier, 62:22-31, June 2014*:
    - Se dice que el mejor modelo fue una red neuronal
    - Se da la selección de variables que ellos encontraron de forma óptima
- Support Vector Machine tarda demasiado en entrenar, incluso normalizando
    - Por eso, ponemos un `partitioning` para poder bajar la carga a dicho algoritmo para poder bajar la carga a dicho algoritmo
    - De hecho, SVM con normalización la tenemos que quitar porque no se ejecuta en un tiempo razonable (en menos de una hora)
1. Variables muy correladas linealmente entre ellas
    - Housing y loan están muy correladas
    - Previous, PDays y POutcome muy correladas
    - Emp.var.rate y cons.price.idx muy correladas
    - Euribor3m y nr.employed muy correladas
    - Ninguna variable está excesivamente correlada con la variable de salida
2. Missing values
     - No tenemos missing values como muestra el nodo que borra los missing values
3. Clase de salida desbalanceada
    - La salida "no" tiene muchos más ejemplos que la salida "yes"
4. Outliers
    - Hay variables con muchos outliers, como `duration`
    - Por eso borramos variables de salida con `3*IQR`
        - **Problema**: esto borra demasiados datos. Tenemos que usar una técnica más avanzada
5. Comprobar que cross validation funciona
6. Comprobar que no haya algoritmos en Cross Validation con resultados catastróficos (esto demuestra algún fallo concreto en el problema)
7. Comprobar que la curva ROC se visualiza correctamente
8. Ajustar los valores para un par de parámetros

