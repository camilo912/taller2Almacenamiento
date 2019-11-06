# taller2Almacenamiento

En este taller se parte de un kernel de kaggle y se implementa en tres diferentes casos:
-   python con almacenamiento local
-   python con almacenamiento en nube (s3)
-   pyspark con almacenamiento en nube (s3)

El kernel de kaggle contiene un caso de analítica de datos en el cual se comparan dos técnicas de IR: okapi bm25 y word2vec en su capacidad de representar documentos y extraer información relaci0nada a una consulta específica.

Los datos que se usaron vienen de https://www.kaggle.com/snapcrack/all-the-news/download y el kernel de kaggle está disponible en: https://www.kaggle.com/girianantharaman/dual-embeddings-space-model-demo

En este caso de analítica no se hace un gran preprocesamiento del texto, solamente se convierte a minúscula y se tokeniza por oraciones y por palabras. 

Para el modelo de word2vec, se entrena un modelo con las oraciones de todos los documentos como entradas para crear los n-gramas y se obtiene así el "embedding" de cada palabra dentro del "bag of words", posteriormente se representa cada documento como el centroide de las representaciones de sus palabras, osea la media en cada dimensión de representación de cada palabra. Al final se calcula el centroide de la consulta, se mide la distancia de cada documento hacia la consulta con la distancia del coseno y se rankea según esta distancia, se obienen los 5 documentos con menor distancia a la consulta. Para este modelo se trabaja con 2 embeddings, los ins y los outs, para cada uno de estos se hace el proceso previo y se calculan los 5 documentos con menor distancia a la consulta.

Para el modelo de okapi bm25 se calcula la relevancia de cada palabra con relación a la consulta, se suman las relevencias de cada palabra de cada documento y de esta forma se obtiene la relevancia de cada documento hacia la consulta. Se rankea según esta relevancia y se obtienen los 5 documentos más relevantes.