# Notes

- En este fichero guardaremos la tabla en la que indicamos lo que se pide en el guión de prácticas
- Además, hay que añadir una captura de pantalla con las subidas del usuario de *DrivenData*: *Submissions*

# Tabla

| Nombre Propuesta  | Fecha y hora de subida | Posición ocupada | Score Training | Score Test Driven Data | Descripción incremental                                                                                                                                      | Descripción preprocesado                                                                      | Descripción Algoritmo                                                       | Configuración de parámetros |
| ---               | ---                    | ---              | ---            | ---                    | ---                                                                                                                                                          | ---                                                                                           | ---                                                                         |                             |
| Primera Propuesta | 27/12/2021 12:08       | 793              | -              | 0.8182                 | Primer modelo funcional. Hacemos lo mínimo para hacer una submission. No tenemos información sobre los resultados en training. Esto se añadirá más tarde | Nos quedamos solo con las variables numéricas, imputamos los missing values usando la mediana | Regresión logística, entrenando dos modelos para las dos variables objetivo | C = 1, regularización l2    |
| Segunda Propuesta | fecha                  | pos              | score          | score                  | 1. En vez de eliminar las variables no numéricas, las paso a numéricas usando one hot encoding

# Por cada subida

- Por cada subida hay que guardar:
    1. Script de python usado para obtener los resultados de la subid
    2. Fichero `.csv` con la clasificación que hemos realizado
