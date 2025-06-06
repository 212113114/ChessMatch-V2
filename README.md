# ChessMatch-V2
Este proyecto es parte del curso **IIC3633 - Sistemas Recomendadores** de la **Pontificia Universidad Católica de Chile**.

Es la segunda versión del proyecto llamado ChessMatch, cuyo objetivo es analizar las partidas de un jugador de ajedrez y recomendarle un jugador profesional con un estilo de juego similar. Como mejora respecto a la versión anterior, se planea implementar un embedding de N factores latentes para los jugadores y también la capacidad de identificar el estilo de juego del usuario, determinando por el cluster al que pertenece y también recomendar un set de partidas del jugador recomendando de acuerdo al perfil del usuario.

Los integrantes son Benjamín Varela, Francisco Meza, Vicente Navarro y Tiare Marín.

🔗 Repositorio original (v1): [ChessMatch](https://github.com/212113114/ChessMatch)

## Datos

Los datos utilizados vienen de la página https://www.pgnmentor.com/files.html en formato PGN, se usaron datos de los [50 jugadores más importantes](https://www.chess.com/lessons/hall-of-fame-the-50-greatest-chess-players-of-all-time) segun chess.com

## Modelo

### V1:
En la primera versión del modelo se utilizó Sentence-BERT para vectorizar partidas de los 17 campeones mundiales de ese entonces (18 actualmente). Para abordar el desbalance de clases, se aplicó SMOTE durante el entrenamiento.

Posteriormente, se entrenó un modelo SVM para clasificar cada partida según el campeón correspondiente. Las filas de la matriz de confusión resultante se utilizaron como embedding representativo de cada jugador. Para la evaluación, se generaron embeddings del mismo modo usando partidas no vistas y se predijo el jugador profesional más cercano usando similaridad de coseno.

Los resultados fueron prometedores:

  -Con más de 100 partidas para construir el embedding de test, se logró una precisión superior al 80%.

  -Al usar todas las partidas de test, se alcanzó un 100% de precisión.

Todo esto puede ser visto en el [repositorio original](https://github.com/212113114/ChessMatch)

### V2:
Se probaran 3 embeddings para partidas distintos: Sbert, e5-large-v2 y GNN.

Para esta segunda versión, planeamos construir los embeddings de los jugadores de una forma distinta: utilizando una cantidad N de clusters para agrupar las partidas. El vector representativo de cada jugador se basará en la proporción de partidas que caen en cada cluster.

Con los datos de los 50 jugadores más importantes de la historia, para un usuario le recomendaremos uno de estos jugadores, su cluster de estilo de juego y un set de partidas personalizado del jugador recomendado para su estudio.

## Archivos
preprocesamiento+Sbert.ipynb: contiene la limpieza y guardado de los datos, además de la creación del embedding para partidas con Sbert

e5_large_v2.ipynb: contiene la creacion del embedding para partidas con e5-large-v2

GNN: contiene la creacion del embedding para partidas con GNN

clustering_sbert.ipynb: contiene el testeo del modelo con SBERT

clustering_e5.ipynb: contiene el testeo del modelo con e5-large-v2

clustering_gnn.ipynb: contiene el testeo del modelo con GNN, este es el modelo definitivo debido a que dio mejores resultados

## Archivos adicionales

Githuh no admite archivos con un tamaño mayor a 25 mb, por lo que los archivos adicionales estarán en este [drive](https://drive.google.com/drive/folders/1xWqTHg10bwfcVWvEcJvj7nwwGMYrgiOV), todos los archivos csv descargados tienen que ir en la carpeta "csvs"








