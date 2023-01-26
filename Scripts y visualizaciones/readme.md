# Evaluación de acciones en el futbol 

## Objetivo del análisis:

El objetivo del presente trabajo es analizar el método “Valuing Actions by Establishing Probabilities (VAEP)” y cuan efectivo resulta para explicar el rendimiento de los jugadores y los equipos.

## Resumen de la metodología a analizar:

El método VAEP se utiliza para evaluar el rendimiento individual de cada jugador tomando en cuenta cuanto mejora la probabilidad de anotar un gol y cuanto disminuye la probabilidad de conceder un gol después de una acción (pase, regate, etc).
	
Para cada evento del partido se toman los 3 eventos posteriores y se estima la probabilidad de anotar y conceder un gol en 10 acciones posteriores luego de la acción que realice el jugador . El puntaje de la acción quedara dado por la suma de cuanto mejora la probabilidad de anotar un gol y cuanto empeora la probabilidad de conceder un gol. De esta manera un jugador podría ser evaluado en forma “objetiva” por la suma del puntaje asignado a todas sus acciones y no por datos sin tanto contexto como la cantidad de pases realizados, regates exitosos, etc.

[Video con la explicación de la metodología](https://www.youtube.com/watch?v=xyyZLs_N1F0) 

## Datasets utilizados:

**1)** Datos de los partidos jugados en las ligas española, inglesa e italiana en la temporada 2017/2018.

* Directorio en el proyecto: *dataset/vaep/matches*
* Archivos: *matches_England*, *matches_Italy*, *Matches_Spain*

**2)** Resultado del análisis VAEP obtenidos con una versión modificada del código realizado por el equipo “Friends of tracking”:

* Directorio en el proyecto: *dataset/vaep/analysisOutcome*
* Archivos:

    * **EventsPerMatch (Eng,Esp,Ita)**: Evaluación de cada acción realizada por partido incluyendo cuanto mejora la probabilidad de anotar cuanto empeora la probabilidad de conceder y la valuación total de la acción.
    * **ActionRatingAnalysis (Eng,Esp,Ita)**: Evaluación del rendimiento total de cada jugador (agregando el puntaje de todas sus acciones)  y valoración del tipo de acción (disparo, pase, drible, etc) normalizada.
    * **rankingAnalysis (Eng,Esp,Ita)**: Evaluación del rendimiento total de cada jugador normalizado y sin normalizar
    * **riskAnalysis (Eng,Esp,Ita)**: Evaluación de la toma de riesgo del jugador analizando si las acciones son exitosas o no y puntuando usando la metodologia.  

## Scripts realizados:

* Directorio en el proyecto: *Jupyter notebook/Vaep/*
* Archivos:
    * **datasetCreation** : Toma los datos de los archivos CSV  y convierte los datasets que se usaran para el análisis en archivos parquet y los datasets que se usaran para visualización los guarda en una base de datos postgres. 
    * **Data Analysis** : Realiza un análisis de como mejora el porcentaje de victorias de un equipo a medida que su puntuación VAEP crece. 
    * **resultPrediction** : Se utiliza un algoritmo random Forest para inferir si un equipo le ganara un partido a otro en base a la puntuación VAEP acumulada en partidos anteriores   

## Visualización en superset:

* Top 10 de jugadores según VAEP total
* Top 10 de jugadores según riesgo de jugada
* Top 10 jugadores según VAEP defensivo
* Comparación entre real Madrid y Barcelona y visualización de cuanto influye cada jugador
* Comparación entre Messi y Cristiano Ronaldo según puntuación VAEP por acción	

[Link al Dashboard](http://localhost:8088/superset/dashboard/p/4AREddrEdWQ/) (credenciales: admin/admin)

## Referencias

* **Ambiente utilizado:**

    https://github.com/MuttData/bigdata-workshop-es
    
*  **Dataset completo con la informacion de la temporada 2017/2018**

    https://www.kaggle.com/datasets/aleespinosa/soccer-match-event-dataset

* **Repositorio código creado por "Friends of tracking":**

    https://github.com/soccer-analytics-research/fot-valuing-actions
   
* **Explicación del código creado por "Friends of tracking":**

    https://www.youtube.com/watch?v=0ol_eLLEQ64 
    
    https://www.youtube.com/watch?v=Ep9wXQgAFaE 
    
    https://www.youtube.com/watch?v=WlORqYIb-Gg
    
    https://www.youtube.com/watch?v=w9G0z3eGCj8
        
* **Versión modificada del primer script para usar archivos CSV:**

    https://github.com/soccer-analytics-research/fot-valuing-actions
    
* **Papers sobre el método VAEP:**:

    Tom Decroos, Lotte Bransen, Jan Van Haaren, and Jesse Davis. [Actions Speak Louder than Goals: Valuing Player Actions in Soccer](https://arxiv.org/abs/1802.07127). In Proceedings of the 25th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining, pp. 1851-1861. 2019.

    Luca Pappalardo, Paolo Cintia, Alessio Rossi, Emanuele Massucco, Paolo Ferragina, Dino Pedreschi, and Fosca Giannotti. [A Public Data Set of Spatio-Temporal Match Events in Soccer Competitions](https://www.nature.com/articles/s41597-019-0247-7). Scientific Data 6, no. 1 (2019): 1-15.


