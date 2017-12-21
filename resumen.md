#Resumen coloquio

## Modulo 1

### T-Test student

#### Hipótesis
* Variables distribuídas normalmente
* Igual Varianza
* Muestras independientes

#### Muestras independientes: Dos muestras
##### Hipótesis nula
Las muestras tienen misma media
##### Análisis
Si obtenemos un p-valor menor a 0.05, podemos rechazar la hipótesis nula, es decir, podemos decir que las muestras no tienen misma media.
En cambio, si obtenemos un p-valor mayor a 0.05, no podemos rechazar la hipótesis nula, entonces no podemos decir que no provienen de distribuciones con igual media.
##### Ejemplo
Altura promedio entre hombres y mujeres.


#### 1 Muestra: Una muestra y un valor
##### Hipótesis nula
La media de la muestra dada es igual al valor dado
##### Análisis
Si obtenemos un p-valor menor a 0.05, podemos rechazar la hipótesis nula, es decir, la muestra no tiene la media dada
En cambio, si obtenemos un p-valor mayor a 0.05, no podemos rechazar la hipótesis nula, entonces no podemos decir que la muestra no tiene la media dada.

#### Muestras apareadas: Dos muestras relacionadas
##### Hipótesis nula
Las muestras tienen misma media
##### Análisis
Si obtenemos un p-valor menor a 0.05, podemos rechazar la hipótesis nula, es decir, podemos decir que las muestras no tienen misma media.
En cambio, si obtenemos un p-valor mayor a 0.05, no podemos rechazar la hipótesis nula, entonces no podemos decir que no provienen de distribuciones con igual media.
##### Ejemplo
Un mismo conjunto de alumnos para dos exámenes diferentes.

### Tests no paramétricos

Son utilizados cuando no valen las hipótesis que requieren los T-Test de Student.

#### Tests de rank sum, Mann-Whitney U, Wilcoxon
##### Hipótesis nula
Las muestras tienen misma distribución
##### Breves comentarios
Ordena todos los valores de mayor a menor y cuenta la cantidad de etiquetas opuestas que tiene por debajo cada muestra. Esa suma da el estadístico U. Por ejemplo: V V V M V M V M. Si tomamos los triunfos de V, tenemos 3 + 3 + 3 + 2 + 1 = 12 = U.

#### Tests de permutaciones
##### Hipótesis nula
Las muestras provienen de poblaciones con igual estadístico (media, mediana, etc)
##### Breves comentarios
* En primer lugar se calcula la diferencia entre las medias de los dos grupos, a lo que se conoce como diferencia observada (Difobservada).
* Todas las observaciones se combinan juntas sin tener en cuenta el grupo al que pertenecían.
* Se calculan todas las posibles permutaciones en las que las observaciones pueden ser agrupadas en dos grupos de tamaño nA y nB.
* Para cada permutación se calcula la diferencia entre medias (Difcalculada). El conjunto de valores calculados forman la distribución exacta de las posibles diferencias siendo cierta la hipótesis nula. A esta distribución se le conoce como permutation distribution of the mean difference.
* El p-value de dos colas se calcula como la proporción de permutaciones muestrales en las que el valor absoluto de la diferencia calculada es mayor o igual al valor absoluto de la diferencia observada.

#### Anova
Es una generalización de los T-Tests pero para más de 2 muestras.

#### Observación de T-Test en general
* Falta de evidencia != Inexistencia del efecto. (Supongamos comparación de medias de alturas entre hombres y mujeres, si obtenemos un p-valor de 0.2, esto no significa que los hombres no sean más altos que las mujeres, sino que no tenemos evidencia suficiente para afirmar que si lo son)


### Correlación

#### Correlación de Pearson
El coeficiente de Pearson mide la relación entre dos datasets. El valor obtenido oscila entre -1 y 1:
* Correlación de 1: Cuando una muestra crece, la otra también
* Correlación de 0: No hay correlación entre los datos
* Correlación de -1: Cuando una muestra crece, la otra decrece

##### Ejemplo
Recordar el ejemplo del tp, los corredores, los buenos corredores en días soleados, eran buenos también en días nublados, había correlación de 0.99, mientras que entre un día soleado y un día de lluvia se calculó una correlación de 0.065, es decir, que un corredor bueno en los días soleados, no necesariamente era bueno un día de lluvia.

#### Observación de correlación en general
* Correlación no implica causalidad


## Módulo 2

### Series temporales

#### Definición

Una serie tiempo es una secuencia de observaciones, medidos en determinados momentos del tiempo, ordenados cronológicamente y, espaciados entre sí de manera uniforme, así los datos usualmente son dependientes entre sí. El principal objetivo de una serie de tiempo X_t, donde t = 1,2,...,n es su análisis para hacer pronóstico.

#### Reducción de ruido

* Predicción con la media: Consiste en tomar una ventana de N valores, N/2 anteriores y N/2 posteriores, y reemplazar cada valor por la media de la ventana.
* Simple Moving Average (SMA): Consiste en reemplazar cada valor con la media de los n valores anteriores
* Weighted Moving Average (WMA): Similar a SMA pero ponderado, donde los valores cercanos tienen mayor peso que los más lejanos. Comienza de un peso n y lo va decrementando hasta un peso 1.
* Exponential Moving Average: Similar a los anteriores, pero pondera de manera exponencial y no lineal:
> S_t = Y1	si t=1
> S_t = a &ast; S_t + (1-a) &ast; S_(t-1)	si t>1
> Notar que a oscila entre 0 Y 1 y que mientras más cerca de 1 esté, más rápido descuenta los valores más viejos

#### Error cuadrático medio (MSE)
> (1/n)&Sigma;(i=1..n) (Ŷ_i - Y_i)^2

* "error" = resta entre estimación (media) y valor real
* "error squared": error al cuadrado
* "SSE": suma de errores al cuadrado
* "MSE": media de errores cuadráticos

#### Clasificación descriptiva

##### Estacionarias
Una serie es estacionaria cuando es estable a lo largo del tiempo, es decir, cuando la media y varianza son constantes en el tiempo. Esto se refleja gráficamente en que los valores de la serie tienden a oscilar alrededor de una media constante y la variabilidad con respecto a esa media también permanece constante en el tiempo.

##### No Estacionarias
Son series en las cuales la tendencia y/o variabilidad cambian en el tiempo. Los cambios en la media determinan una tendencia a crecer o decrecer a largo plazo, por lo que la serie no oscila alrededor de un valor constante.

* Se utiliza el test estadístico de Dickley-Fuller con la hipótesis nula de que la serie es NO estacionaria (en realidad es un test con hipótesis nula que la serie tiene una raíz unitaria, pero lo otro es una posible interpretación para nuestro fin), por lo tanto un p-valor menor a 0.05 nos sirve para rechazarla, afirmando entonces que la serie es estacionaria, y un p-valor más grande no nos dejaría rechazarla.

#### Regresión lineal
Se trata de estimar la pendiente y ordenada al origen que minimicen el error cuadrático medio (MSE) entre lo estimado y lo real. 
* Ojo, no evaluar con MSE ya que con ello se conforma, siempre va a ser el mínimo
* Se puede utilizar para predicciones, entrenando con una parte de los datos se obtienen los estimadores que luego se usaran para predecir el resto de los datos. (Si se separa una parte de los datos para test, ahí si se puede medir con MSE el estimador precalculado con el set de entrenamiento)


## Módulo 3

### Machine Learning
Un programa aprende si su performance mejora con la experiencia

* Tarea: Ej: Precedir el color de un punto en el plano
* Medida de performance: Ej: % de puntos coloreados correctamente
* Experiencia: Base de datos de puntos en el plano con su correspondiente color

#### Aprendizaje supervisado
Los datos están anotados

##### Tipos de aprendizaje supervisado
* Clasificación: Cada instancia pertenece a una clase. Ejemplo: mensaje -> {spam, no spam}
* Regresión: Cada instancia tiene un valor numérico: Ejemplo: mensaje -> probabilidad [0,1] de ser spam

##### Algoritmos de aprendizaje supervisado
* Árboles de decisión
* Support Vector Machine
* Hidden Markov Models

#### Aprendizaje no supervisado
Los datos no están anotados. (Big Data, Clustering)

#### Aprendizaje por refuerzos
Aprendizaje gradual, en base a premios y castigos

#### Overfitting
Sobreentrenar un algoritmo de aprendizaje con ciertos datos para los que se conoce el resultado deseado.

Definición más formal: Sea D el conjunto de instancias de entrenamiento y X el conjunto de todas las posibles instancias, h se sobreajusta a los datos de entrenamiento si existe h' tal que:
* error D (h) < error D (h')
* error X (h) > error X (h')

O sea: h es mejor sobre D, pero h' generaliza mejor.

##### Overfitting en árboles
Algunas posibles soluciones son:
* Criterio de parada: No construir más allá de cierta profundidad
* Pruning (poda): Construír el árbol completo, podar las ramas cuando ello mejore la exactidud sobre datos separados
* Rule post-pruning: Construir el árbol entero; convertir árbol a reglas; sacar precondiciones de las reglas cuando ello mejore su exactitud sobre datos separados; reordenar las reglas según exactitud.

#### Entrenamiento y validación
Para evitar el overfitting está bueno separar el conjunto de datos en Entrenamiento y Validación. Los datos se deben separar al azar.

##### K-Fold Cross validation
Consiste en:
1. Desordenar los datos
2. Separar en k folds de igual tamaño
3. para i = 1..k, Entrenar sobre todos los folds menos el i, evaluar sobre el i

Luego de esto tenemos k resultados, se pueden promediar o trabajarla como una distribución de resultados.
Por ejemplo, supongamos que tenemos dos hipótesis (modelos), una opción es comparar las medias, pero quizás sea mejor comparar los resultados con un test estadístico apareado.

Aunque hagamos cross validation con K-Fold, podríamos seguir overfitteando los resultados, por lo que una posible solución a esto es separar de antemano otra parte de los datos, que serán utilizados para test. Estos datos solo se usan cuando el modelo está entrenado y es solo para probar, si los resultados dan bien o mal, ya no se puede volver atrás, sino correríamos el riesgo de seguir overfitteando.

#### Medidas de performance

##### Matríz de confusión (clasificación binaria)
|  | Spam (predicho) | No Spam (predicho)
|--------|--------|--------|
| Spam (real) | TP | FN |
| No Spam (real) | FP | TN |

* TP: True Positive
* TN: True Negative
* FP: False Positive
* FN: False Negative

##### Precisión
Precisión = TP / (TP + FP)

"Cuántos de los que supusimos positivos, eran realmente positivos"

##### Recall (Exhaustividad)
Recall = TP / (TP + FN)

"Cuántos de los que eran realmente positivos, eran realmente positivos"

##### Curva ROC (Receiver operating characteristic)

TPR (Recall) vs. FPR

* TPR (True Positive Rate): TP / (TP + FN)
* FPR (False Positive Rate): FP / (FP + TN)

Construcción: Variar el umbral de detección entre 0% y 100% y para cada valor calcular la posición en el gráfico.

###### Area Under the Curve (AUC)
* Puede tomar valores entre 0 y 1
* 1 o 0 sería ideal (0 es la inversa de 1, variar el umbral al revés y se obtiene un 1)
* 0.5 es random

![ROC](curva-roc.png)

##### Matriz de confusión N-Aria

![MATRIZ-N-ARIA](matriz-confusion-n-aria.png)


## Módulo 4

SMALL WORLD

En este tipo de grafos no todos los nodes se conectan entre si, pero se puede llagar desde cualquier nodo a otro por medio de los vecinos.
La distancia típica entre cualquier par de nodos aleatoreos es alrededor de log N siendo N la cantidad de nodos del grafo

A mayor aleatoreadad del grafo tanto el camino minimo como coeficiente de clustering disminuye


DISTRIBUCION DE GRADOS
Ley de potencias y exponencial a simple vita son indistingibles.

Para distinguier entre ellas podemos utilizar loglog() y semilogy()

Con loglog() ley de potencias es una recta, y con semilogy() exponencial es una recta


REDES LIBRES DE ESCALA

Son quellas redes en las cuales hay nodos bastante más importantes que otros, denominados hubs. Estas redes comunmente se expanden agregando nuevos verticesa nodos que estan "bien" conectados

Medidas de centralidad:

Betweenness Basada en camino minimimo. La medida para cada nodo es la cantidad de caminos mínimos que pasan por el. Se puede pensar tmb en las aristas.

Closeness Para cada nodo se calcula la suma de los caminos minimos desde ese nodo al resto de los del grafo. Mientras más cerca está del resto de los nodos más importante es.

Degree El grado de cada nodo representa la importancia del mismo

Kaiz Cantidad de nodos que se conectan por algún camino ponderando la distancia

Eigenvector Sitema de puntos para cada nodo en funcion de falopa


PERCOLACION : Una medida de fiabilidad de la red

Comunidades ( Grivan-Newman)

Mediante el calculo de betweenness y sacando las aristas mas importantes en cada paso se generan comunidades en el grafo.

## Módulo 5

### Inferencia Bayesiana

Supongamos que tiramos una moneda 6 veces y obtenemos 6 caras. ¿Podemos decir que la moneda está cargada?
Con la estadística frecuentista, podemos plantearnos la probabilidad de haber obtenido las 6 caras en los 6 tiros y eso nos daría un p=0.03125 < 0.05 lo cual diría que la moneda está cargada. (Hipótesis nula de que la moneda es honesta)

El problema es que la estadística clásica nos plantea p(D|H), o sea, se pregunta cuá es la probabilidad de obtener ciertos datos dada una hipótesis, y lo que nosotros queremos es saber cuál es la probabilidad de la hipótesis dados los datos, p(H|D), es decir, cuál es la probabilidad de que la moneda esté cargada dado que obtuvimos 6 caras.

El modelo bayesiano nos permite (o mejor dicho nos obliga) a incorporar nuestra hipótesis, es decir, nuestra intuición dice que la moneda va a ser honesta, nunca vimos una moneda cargada, por lo que partimos de la idea de que no está cargada.

Críticas al frecuentismo:
* Ignora conocimiento previo
* el p-valor de corte es un número definido arbitrariamente (0.049999 se rechaza y 0.0500001 no, muy blanco o negro)
* Uso ciego
* p-hacking
* Crisis de reproducibilidad (36% de papers reproducidos en psicología)

Fórmula de la inferencia bayesiana:

p(H, D) = p(D|H)p(H) = p(H|D)p(D)

=>

posterior = (likelihood * prior) / p(D)
p(H|D) = (p(D|H)p(H)) / p(D)

#### Acumulación de evidencia

El posterior es el nuevo prior, se retroalimenta y aprende




## Módulo 6

PROCESAMIENTO DE LENGUAJE NATURAL

Word Asociation
Que palabras está más asociadas con otras. Podemos verlo contando la asociacion de lás mismas en distintos textos. Cuantas veces esas palabras aparecen una despues de la otra, o en terminos de hasta n palabras.

INFORMACION MUTUA

I(x,y) = log2 P(x,y)/(P(x)P(Y))

P(x,y) se estima con la cantidad de veces que aparece x seguido de y

ENTROPIA

Suatoria p(x) log2 P(x)

La entropía es maxima cuando la distribución es homogenea y es minima cuando está concentrado en una parte

Una palabra aporta más información si se encuentra menos veces en el texto, y mientras más frecuente es menos información aporta

LSA
Similaridad entre conceptos basados en la frecuencia de los terminos en distintos documentos

- Vector de apariciones en distintos tectos por palabra
- Reducir las dimensiones con SVD
- Calcular distancias entre palabras

Vocabulario:
* Separar en sentencias
* Separar en tokens
* Tagging
* Lematizar

Cada lema resultante es un elemento del vocabulario

