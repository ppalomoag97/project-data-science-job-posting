# Proyecto Final de Ciencia de Datos - Modelos de aprendizaje automático


#### Introduccón
El objetivo de este proyecto es entrenar y evaluar diferentes modelos de predicción que nos ayuden a explicar mejor un set de datos escogido a nuestra elección. A lo largo del proceso, se realizarán tareas de recolección de datos, limpieza y manipulación de datos, análisis de características, selección, evaluación y visualización de datos, para finalmente terminar concluyendo con la elección del mejor modelo.

#### Propósito del proyecto
En el caso de este proyecto, el problema principal al que queremos dar respuesta, es decir, la variable predictiva que queremos tratar de explicar en un primer momento, es el 'Salario Promedio' de los perfiles de trabajo dentro del ámbito 'DATA', mediante una serie de características utulizando modelos de regresión.
En mitad del proyecto, llegamos a la conclusión que nuestro set de datos no es el correcto para el objetivo propuesto inicialmente, por lo que tenemos que cambiar nuestro propósito al siguiente: tratar de predecir el 'Perfil Profesional' en base a una serie de características, unas 'originales' del set de datos, y otras 'sintéticas' que generaremos a lo largo del proyecto. Para ello, se utilizarás modelos de clasificación.
De esta manera, nuestro proyecto quedaría divido en dos partes, una primera parte de 'Regresión, que recoge los siguientes pasos:
'1.1. Análisis Exploratorio de datos - (Regresión).ipynb'
'1.2. Limpieza y manipulación de datos - (Regresión).ipynb'
'1.3. Aprendizaje automático - (Regresión).ipynb'.

Y una segunda parte de clasificación, en la que no volvemos a repetir la fase de EDA, porque la comprensión del set de datos ya ha sido satisfactoria en el primera fase. Se divide en los siguientes pasos:
'2.1. Limpieza y manipulación de datos - (Clasificación).ipynb'
'2.2. Aprendizaje automático - (Clasificación).ipynb'.

#### Recolección de datos
El set de datos que hemos escogido proviene del portal de datos 'Kaggle', y consiste en ofertas de trabajo publicadas en el portal de empleo 'Glassdoor', que se han obtenido mediante 'scraping'. En la página donde están publicados los datos, están disponibles dos sets de datos, uno con los datos 'brutos' y otro con los datos 'tratados'. En nuestro caso, para agilizar el proyecto, hemos decidido trabajar sobre los datos 'tratados', recogidos bajo el nombre 'Cleaned_DS_Jobs.csv' y que se encuentran dentro de la carpeta 'dataset'. 
A continuación, se especifican las variables iniciales del set de datos junto a una breve explicación para una mejor comprensión:
+ Job Title: Título de la posición ofertada
+ Salary Estimate: Rango de salario para el tipo de posición.
+ Job Description: Descripción completa del puesto de trabajo.
+ Rating: Valoración del post del puesto de trabajo.
+ Company: Nombre de la compañía.
+ Location: Ubicación de la compañía.
+ Headquarter: Ubicación de la sede de la compañía.
+ Size: Número de empleados de la compañía.
+ Type of ownership: Describe el tipo de compañía i.e ong/pública/privada etc
+ Industry: Industria de la compañía
+ Sector: Sector de la compañía
+ Revenue: Ingresos totales de la compañía
+ min_salary: Salario mínimo
+ max_salary: Salario máximo
+ avg_salary: Salario medio
+ job_state: Estado de la posición de trabajo
+ same_state: Mismo estado que la sede
+ company_age: Edad de la compañía
+ python,excel,hadoop,spark,aws,tableau,big_data: Habilidades en forma de boleano (1)
+ job_simp: Título de la posición ofertada limpio
+ seniority: si el trabajo es senior o no (boleano)
  
#### Análisis Exploratorio de Datos (EDA)
En la parte de Análisis Exploratorio de datos, se analizan datos nulos y se valora como tratarlos posteriormente, además de realizar un análisis expecífico de cada variable en la que se concluye con la acción a realizar en la siguiente fase.

#### Limpieza y manipulación de datos
En este proceso se llevan a cabo una serie de acciones especificadas en la parte previa de Análisis Exploratorio de datos para le caso de Regresión, y otras acciones ejecutadas directamente en la parte de Clasificación. 
En la parte de Regresión se recogen los pasos en el archivo '1.2. Limpieza y manipulación de datos - (Regresión).ipynb' y se llevan a cabo las siguientes acciones:
+ Acción 1: Eliminar la columna 'Job Title'
+ Acción 2: Recategorizar los 'na' de la columna job_simp y eliminar los 'na' restantes al no tratarse de posiciones dentro del sector de data.
+ Acción 3: Eliminar columnas 'Salary Estimation', 'min_salary' y 'max_salary'
+ Acción 4: Eliminar columna 'Job Description'
+ Acción 5: Eliminar columna 'Rating'
+ Acción 6: Eliminar columna 'Company Name'
+ Acción 7: Agrupar la columna 'Location' por estado en lugar de por ciudad.
+ Acción 8: En el caso de la columna 'Headquarters', encontramos muchos valores distintos de ciudades, en este caso generaremos una nueva columna agrupada por país, ya que se ven valores de países diferentes de EEUU, y para EEUU se especifica el estado. Además, se corregirán valores faltantes, como -1, a los que se asignará el valor de la columna 'Location' y 'New York, 061' que se cambiará por 'New York, NY'.
+ Acción 9: Corregir los -1 de la columna 'Size' como 'Unknown'
+ Acción 10: Corregir los -1 de la columna 'Type of ownership' y reorganizar valores para tener menos columnas
+ Acción 11: Eliminar la columna 'Industry' por demasiados valores únicos, utilizaremos la de Sector, que nos aporta información parecida y más agrupada.
+ Acción 12: Modificar el valor -1 de la columna 'Sector' por 'Unknown'.
+ Acción 13: Modificaremos el valor -1 por 'Unknown' para la variable 'Revenue'
+ Acción 14: Eliminaremos la columna job_state debido a que estaba creada en base a Location y ya la hemos gestionado por nuestra parte.
+ Acción 15: Esta columna fue creada en base al año de creación de la compañía. Tenemos valores a -1, que corresponde a cuando no se tenían datos. Como se desconcoe la información, se dará como valor 1 para 1 para tener un dato interpretable.
+ Acción 16: Esta columna tenemos demasiado valores nulos, por lo que procederemos a eliminarla.
+ Acción 17: Crear nuevas columnas de habiliades en base a la columna Job Description
El resultado de esta fase se guarda en un csv dentro de la carpeta datataset bajo el nombre 'Cleaned_job_position.csv'.

En la segunda parte de Clasificación se recogen los pasos en el archivo '2.1. Limpieza y manipulación de datos - (Clasificación).ipynb' y se llevan a cabo las siguientes acciones:
+ Acción 1: Generar nuestra variable objetivo 'job_desc'. En base a la columna original 'Job Title', donde teníamos toda la información de la oferta de trabajo, generaremos una nueva variable, clasificando los puestos de trabajo en categorías según el texto original. Para la definición de categorías, utilizaremos dos funciones que unificaremos después en función del tipo de puesto y del nivel de experiencia.
+ Acción 2: Corregir los -1 de la columna 'Size' como 'Unknown'
+ Acción 3: Corregir los -1 de la columna 'Type of ownership' y reorganizar valores para tener menos columnas
+ Acción 4: Modificar el valor -1 de la columna 'Sector' por 'Unknown'
+ Acción 5: Modificaremos el valor -1 por 'Unknown' para la variable 'Revenue'
+ Acción 6: Cambiar el valor -1 de la columna 'company_age' a 1
+ Acción 7: Eliminar columnas 'Job Title','Salary Estimate','min_salary','max_salary','Job Description','Rating','Company Name','Industry','seniority','tableau','Location','Headquarters','job_state','same_state','python','excel','hadoop','spark','aws','big_data','job_simp','job_description','experience'.
+ Acción 8: Crear nuevas columnas de habilidades en base a años de experiencia. Para tener un set de datos que nos sea útil en la creación de un modelo de predicción de clasificación, generaremos datos sintéticos con el valor de las variables sobre habilidades. Originalmente, son varibales binarias, marcadas con '1' si en la oferta de trabajo se requiere de dicha habilidad y con '0' si no se menciona en la oferta. Por lo tanto, realizaremos una transformación de dichas habilidades con valores aleatorios según los años de experienca que, por cada categoría de 'job_desc' se puede requerir en el mercado laboral.
El resultado de esta fase se guarda en un csv dentro de la carpeta dataset bajo el nombre './dataset/Cleaned_job_position_CLASSIFICATION.csv' y será el data set con el que trabjaremos en la siguiente fase.

#### Aprendizaje automático
En la primera fase de '1.3. Aprendizaje automático - (Regresión).ipynb', se utilizan dos modelos, uno de Regresión Lineal y otro de Árbol de Decisión.

Para Rregresión Lineal, se utilizan únicamente variables numéricas  y se incluyen Regularizaciones Ridge y Lasso, posteriormente se evaluan resultados mediante MSE y R^2. 

Para Árbol de Decisión, se utiliza LabelEncoder y OrdinalEncoder para transformar variables categóricas a numéricas e introduimos todas en el modelo. También evaluamos con MSE y R^2. Se realiza también un escalado de datos y se tratan de hacer pruebas eliminando variables sobre habilidades, pero se termina concluyendo, dado que estamos obteniendo resultados de accuracy muy bajos, que el set de datos no está preparado para el propósito esperado. De esta manera, en este punto del trabajo, decidimos comenzar de nuevo, creando una serie de datos sintéticos para generar modelos de predicción de clasificación.


En la segunda fase del proyecto, entrenaremos cuatro modelos de clasificación: Árbol de decisión, Regresión logística, Random Forest, y Gradient Boosting. Aplicamos técnicas de validación cruzada (K-folds) para cada uno de los modelos y así poder obtener una evaluación promedio que nos ayuda a escoger el modelo que mejor se comporta con datos no vistos.

Finalmente, realizamos un ajuste de hiperparámetros con GridSearchCV para obtener los mejores parámetros del mejor modelo esogido anteriormente.

En definitiva, resumimos los pasos a seguir:

     2.2.1 - División del set de datos en entrenamiento y prueba
     
     2.2.2 - Modelos de Regresión Logística, Árbol de decisión, Random Forest y Gradient Boosting
     
     2.2.3 - Validación cruzada
     
     2.2.4 - Ajuste de hiperparámetros

Se termina esta parte realizando una evaluación de nuestro modelo con datos reales.

#### Resultados
Después de la validación cruzada para comparar el comportamiento de los 4 modelos, escogemos el modelo de Random Forest y Gradient Boosting que presentann una media más elevada y una varianza con valores más elevados.

El Random Forest, siendo un ensamblaje de múltiples árboles de decisión, tiende a ser más robusto frente a los datos de entrenamiento, ya que promedia los resultados de múltiples árboles y reduce la varianza del modelo. Esto le permite manejar mejor los datos ruidosos y es menos propenso al sobreajuste en comparación con modelos individuales como los árboles de decisión.

Aunque la Regresión Logística y el Árbol de Decisión son modelos valiosos, pueden no capturar la complejidad y las interacciones en los datos tan bien como el Random Forest. La Regresión Logística es más adecuada para relaciones lineales, mientras que el Árbol de Decisión puede ser susceptible al sobreajuste. El Gradient Boosting también es un modelo poderoso, pero puede ser más sensible a los parámetros de ajuste y al tiempo de entrenamiento.

#### Conclusión
Falta de un data set más completo y con más registros para hacer mejores interpretaciones.

Sesgo por poca representatividad de categorías como ‘Machine Learning Engineer’ o ‘Computer Scientist’, por ejemplo.

Tiempo en contra, añadir regularizaciones de Ridge y Lasso.

Resultados muy parecidos entre Random Forest (entrenamiento independiente) y Gradient Boosting (entrenamiento secuencial).


#### Origen del set de datos 
https://www.kaggle.com/datasets/rashikrahmanpritom/data-science-job-posting-on-glassdoor/data

#### Presentación del proyecto
https://docs.google.com/presentation/d/1IzLoNSaBYajYKBN_lJC-2Vg7iuRODF8Ah_LnWg8XEAw/edit#slide=id.p


Patricia Palomo Aguilar
https://www.linkedin.com/in/patriciapalomoaguilar/




