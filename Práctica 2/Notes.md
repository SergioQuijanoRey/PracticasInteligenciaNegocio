# Notes

- Las variables no numéricas no son útiles para el *clustering*. Pero sí que son útiles para definir el filtrado para el caso de estudio
- Variables numéricas que son ordinales, como capacidad para llegar a fin de mes
- La documentación oficial de `sklearn` sobre [clustering](https://scikit-learn.org/stable/modules/clustering.html) está muy bien
- Hay muchas variables que van acompañadas de una variable *FLAG* que indica si el dato es faltante o que en este caso no aplica
    - Esto creo que lo puedo usar para realizar algunos filtrados de los datos
- No tenemos acceso a las variables que corresponden a las personas: "P<algo>"

# Algoritmos de clustering utilizados

1. K-Means
2. DB-Scan
3. Birch
4. Mean Shift
5. Agrupamiento jerárquico

# Tareas a realizar en cada dataset

1. Definir el caso de estudio
    - Para ello, definir el filtrado del `dataframe` que se nos ha dado
2. Aplicar los algoritmos de clustering al dataset restringido y extraer métricas
    - Índice de Shilhouette e índice Calinski-Harabasz
    - Hay que mirar más métricas para el clustering
3. Crear una tabla comparativa entre los algoritmos de clustering
    - Usando las métricas que hemos extraído en la parte 2.
    - Al final, unas pequeñas conclusiones sobre el comportamiento de los algoritmos
4. Estudiar el efecto de los parámetros de los algoritmos, en al menos dos algoritmos por cada caso de estudio
    - Seleccionar parámetros fundamentales a dos algoritmos, y moverlos viendo el efecto de mover dichos parámetros
    - Crear una tabla para esto, en la que se muestren como varía ciertas métricas en función de los parámetros
5. Conclusiones sobre el caso de estudio
    - Conclusiones que hemos podido extraer, gracias a todo el trabajo previo, sobre el caso de estudio concreto en el que nos encontramos
    - ie. las familias de rentas inferiores son las que más gastan en transporte público

# Ideas para los casos de estudio

- Estudiar el endeudamiento
    - En función de la renta a secas
    - En función del dinero restante (lo que entra menos lo que sale)
    - En función de la riqueza de los hogares
- Estudiar una comunidad autónoma vs otra comunidad
- Usar la edad en algún caso de estudio
- Usar el sexo en algún caso de estudio
- Sexo y cuidados?
