# ChessMatch-V2
Este proyecto es parte del curso **IIC3633 - Sistemas Recomendadores** de la **Pontificia Universidad Católica de Chile**.

Es la segunda versión del proyecto llamado ChessMatch, cuyo objetivo es analizar las partidas de un jugador de ajedrez y recomendarle un jugador profesional con un estilo de juego similar. Como mejora respecto a la versión anterior, se planea implementar un embedding de N factores latentes para los jugadores y también la capacidad de identificar el estilo de juego del usuario, determinando por el cluster al que pertenece.

Los integrantes son Benjamín Varela, Francisco Meza, Vicente Navarro y Tiare Marín.

🔗 Repositorio original (v1): [ChessMatch](https://github.com/212113114/ChessMatch)

## Datos

Los datos utilizados vienen de la página https://www.pgnmentor.com/files.html en formato PGN, pero fueron preprocesados para solo incluir el nombre y los movimientos de uno de los jugadores.

## Modelo

### V1:
En la primera versión del modelo se utilizó Sentence-BERT para vectorizar partidas de los 17 campeones mundiales de ese entonces (18 actualmente). Para abordar el desbalance de clases, se aplicó SMOTE durante el entrenamiento.

Posteriormente, se entrenó un modelo SVM para clasificar cada partida según el campeón correspondiente. Las filas de la matriz de confusión resultante se utilizaron como embedding representativo de cada jugador. Para la evaluación, se generaron embeddings del mismo modo usando partidas no vistas y se predijo el jugador profesional más cercano usando similaridad de coseno.

Los resultados fueron prometedores:

  -Con más de 100 partidas para construir el embedding de test, se logró una precisión superior al 80%.

  -Al usar todas las partidas de test, se alcanzó un 100% de precisión.

Todo esto puede ser visto en el [repositorio original](https://github.com/212113114/ChessMatch)

### V2:

Para esta segunda versión, planeamos construir los embeddings de una forma distinta: utilizando una cantidad N de clusters para agrupar las partidas. El vector representativo de cada jugador se basará en la proporción de partidas que caen en cada cluster.

Además, no queremos limitarnos solo a los campeones mundiales: nuestro objetivo es trabajar con datos de todos los jugadores profesionales disponibles. De esta forma, no solo se podrá recomendar al jugador profesional más similar, sino también identificar el grupo de jugadores (cluster) que comparten un estilo de juego similar.






