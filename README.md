
# Data analysis: Aircraft accidents

## Introduction

This project aims to investigate aircraft accidents since the beginning of the 20th century. As a result of this research, we will produce a written report and an interactive dashboard that compiles and displays the collected information.

To begin the project, we had one dataset that gathered data on aircraft accidents from the beginning of the 20th century to 2009.

Regarding the organization of the project, it consists of three files created with Jupyter Notebooks. The first file carries out the first phase of data transformation, along with a small exploratory data analysis to peek at the nature of the data. The second file has a text analyzer that identifies adverse weather conditions. In the third file, we have the exploratory data analysis and the code for our dashboard.

We carried out the entire investigation using **Python** as our programming language. Additionally, we used specialized Python libraries and a small **SQL** database to store the data.

<hr>

## Development of the project

### ETL

Our first step was to transform the data. To do so, we used the following Python libraries, **pandas**, **numpy**, and **seaborn**. We also used the **os** module to manage directories. The changes made were as follows:

- Conversion of missing values to Nan data type (they originally appeared as char '?')
- Elimination of metadata columns
- Normalization of column names  and their letter case
- Elimination of rows when null records of the columns represented a low percentage of the total (less than 16%)
- Elimination of fields with a high percentage of missing values
- We converted some columns with string data types from object to numeric or date types.
- We sought inconsistencies in the way of adding up fatalities. Then, we corrected them when necessary, using external sources for this task.
- Detection and correction of outliers.
- Creation of a column to store the names of the countries where the accidents occurred.
- Replacement of data holding US States' names with the name of that country.
- We did something similar with regions and cities in the rest of the world, changing the original data for the corresponding country.
- We created a "Collisions" column to record accidents involving two or more aircraft.
- We renamed the "total_fatalities" column, which contained the total number of deaths on board, as "on_air_fatalities."
- We created a new column called "total_fatalities" that would contain the total number of deaths from accidents, adding up all categories, including ground deaths.
- We capitalized fields with a string data type to normalize the data.



### NLP (Natural Language Processing)

In the second notebook, we used the **nltk** library to filter weather conditions that affect flights. The main idea was to find text that provided clues about adverse weather factors. To achieve this, we processed all the data in the "summary" column (all those values had a text that reported what had happened in the accident). The processing consisted of the following steps:

- Create a list from the values in the "summary" field, where each element is a value from the column.
- Concatenate all the strings (separated by white space) in the list to form a single text.
- Remove punctuation.
- Remove all digits from the text.

Once we obtained a string consisting only of alphabetical characters, we used the process of lemmatization, which involves bringing a word to a standardized form known as a lemma. In the case of nouns and adjectives, the lemma is the singular form, while for verbs, the lemma is their infinitive form. This process in nltk creates a list with each lemma separated, so we had to make a single string again (as in step B), but this time formed by lemmas. When we finished this step, we removed the words that didn't add value to the text using the `stopwords.words()` method. Then, we converted everything to lowercase to normalize the data and facilitate the next step of word filtering. Afterward, we proceeded to visualize; firstly, the most frequent words; second, the most frequent bigrams; and third, the most frequent trigrams. We defined a bigram as a set of two consecutive words and a trigram as a set of three consecutive words.

Those visualizations helped us find keywords. Also, we could observe what the most frequent word combinations were, along with their importance in the structure of the texts. However, this was just the first approach since we still had to remove some words, bigrams, and trigrams that did not provide information about adverse weather conditions. Once removed, we obtained words, bigrams, and trigrams expressing adverse weather conditions. We created two lists, one with poor weather conditions keywords and the other with bigrams. With those keywords and bigrams, we could identify the records in which weather conditions affected the flight or were the main factor in the accident. Then, we created a binary column that recorded a 1 for those flights that faced adverse weather conditions and a 0 for those that did not. Finally, we saved the data in a database.

<hr>

## Dashboard

To create the Dashboard, we used the Panel bootstrap template, which allows us to lay out the graphs (pleasantly and aesthetically). This template has two areas, a sidebar, and a "main" area. In the first one, descriptions and controller widgets for the dynamics of the graphs can be placed. The main area of the template is where we can lay out the graphics or their container widgets. That main area is built  with rows and columns  using the **Panel** library. Within these rows and columns, we can place the objects we want.
The graphics were made using **Hvplot**, **Holoviews**, and **matplotlib**. The last one was used to make use of its aggregation functions. 


<hr>
<hr>

### Espa??ol

<hr>



# An??lisis de datos: accidentes a??reos


## Introducci??n

El presente trabajo tiene como objetivo investigar los accidentes a??reos producidos desde inicios del siglo XX. Como productos de esta investigaci??n obtendremos, por un lado un informe escrito y por el otro un dashboard interactivo que recopile y muestre la informaci??n
recogida. 

Para iniciar el trabajo contamos con un ??nico dataset que re??ne datos de accidentes a??reos desde comienzos del siglo XX hasta la actualidad. 

En cuanto a la organizaci??n del proyecto, este consta de tres archivos creados con Jupyter Notebooks. En el primero se realiza la primera fase de transformaci??n de datos, junto a un peque??o an??lisis exploratorio de datos para tener una mejor idea de la naturaleza de los datos. En el segundo archivo, hay un analizador de texto que identifica condiciones de mal 
tiempo. En el tercero se encuentra el an??lisis exploratorio de datos y el c??digo de nuestro dashboard. Para llevar adelante toda la investigaci??n, elegimos **Python** como nuestro lenguaje de programaci??n. Adicionalmente, utilizamos tanto librer??as especializadas de este lenguaje, como una peque??a base **SQL** para almacenar los datos.

<hr>

## Desarrollo del proyecto

### ETL

La primera etapa del proyecto consisti?? en transformar los datos, utilizando para estos las librer??as **pandas**, **numpy** y **seaborn**, tambi??n utilizamos el m??dulo **os** para gestionar directorios. Los cambios realizados fueron los siguientes. 

- Conversi??n de valores faltantes a tipo de dato Nan (figuraban como char ???????)
- Eliminamos columnas de metadatos
- Normalizamos los nombres de las columnas al cambiar su nombre y escribirlos en min??sculas.
- Eliminamos filas cuando los registros nulos de las columnas representaban un bajo porcentaje del total (menor al 16%)
- Eliminamos las columnas con un mayor n??mero de valores faltantes. 
- Convertimos a tipos de datos m??s espec??ficos, ya sea a fecha o num??ricos.
- Buscamos inconsistencias en la suma de fatalidades de los registros del dataset, corregimos cuando fue necesario, utilizando fuentes externas para esta tarea.
- Detectamos y corregimos outliers
- Creamos una columna para almacenar los nombres de los pa??ses de los siniestros
- Reemplazamos los datos que ten??an nombres de Estados estadounidenses por el nombre del pa??s.
- Algo similar hicimos con regiones y ciudades del resto del mundo, cambiamos el dato original por el pa??s correspondiente
- Creamos una columna ???Collisions??? para registrar los accidentes en los que estaban involucrados m??s de un avi??n al mismo tiempo.
- Renombramos la columna ???total_fatalities??? que conten??a el total de muertes a bordo como ???on_air_fatalities??? 
- Creamos una nueva columna a la que llamamos ???total_fatalities??? que contendr??a el total de muertos por accidentes, sumando todas las categor??as incluyendo las muertes en tierra.
- Capitalizamos los campos con tipo de dato string para normalizar la data.


### NLP (procesamiento de lenguaje natural) 

En el segundo notebook utilizamos la librer??a **nltk** para filtrar condiciones meteorol??gicas que afectan a los vuelos, la idea principal era encontrar texto que de indicios de factores meteorol??gicos adversos. Para lograrlo, procesamos todos los datos en la columna ???summary???(cada uno de estos datos posee una cadena de texto que informa lo ocurrido en el accidente). El procesamiento consisti?? de los siguientes pasos:

- Crear una lista a partir de los valores del  campo ???summary???, en los que cada elemento sea un valor de la columna. 
- Concatenar cada uno de esos elementos para formar una ??nica string, separando cada elemento con un espacio.
- Remover la puntuaci??n.
- Remover todos los d??gitos en el texto.

Una vez que obtuvimos una string solo de caracteres alfab??ticos, utilizamos el proceso de lematizaci??n, que consiste en llevar una palabra a una forma estandarizada conocida como lema. En en el caso de los sustantivos, el lema es el singular, algo similar ocurre con los adjetivos, mientras que para los verbos el lema es su forma infinitiva. Este proceso en nltk crea una lista con cada lema separado, por lo tanto tuvimos que volver a crear una sola string como en el paso B, pero esta vez formada por lemas. Cuando terminamos este paso, quitamos las palabras que no agregan ning??n valor al texto utilizando el m??todo `stopwords.words()`, llevamos todo a min??sculas para normalizar los datos y favorecer el paso siguiente de filtraci??n de palabras. Luego, procedimos a visualizar; primero, las palabras m??s frecuentes; segundo, los bigramas m??s frecuentes y tercero, los trigramas de mayor frecuencia. Definimos a un bigrama como un conjunto de dos palabras consecutivas y a un trigrama como uno de tres palabras consecutivas.

Estas visualizaciones nos ayudaron a comprender tanto cu??les eran las palabras claves as?? como las combinaciones de palabras m??s frecuentes y su importancia en la estructura de los textos. Sin embargo, este paso solo fue el primero dado que todav??a deb??amos quitar palabras, bigramas y trigramas que no aportaran informaci??n sobre condiciones meteorol??gicas adversas. Una vez quitadas, llegamos a obtener informaci??n de mucho inter??s. Creamos dos listas, una con palabras claves y la otra con bigramas clave. Con estas listas pudimos identificar los registros en los que las condiciones meteorol??gicas condicionaron el vuelo o fueron el factor principal del accidente. Despu??s, creamos una columna binaria que registrara con un 1 aquellos vuelos que enfrentaron condiciones meteorol??gicas adversas y con un 0 a aquellos que no. Finalmente guardamos los datos en una base de datos. 

<hr>

## Dashboard

Para la creaci??n del Dashboard utilizamos el template bootstrap de Panel, que permite realizar el layout de los gr??ficos de una manera bastante amena y est??tica. Este template tiene, b??sicamente, dos zonas, una sidebar y una zona principal, en la primera pueden disponerse descripciones y widgets controladores de la din??mica de los gr??ficos. En la segunda se situ??n los gr??ficos o widgets contenedores de gr??ficos. La disposici??n de esta zona est?? dada por filas y columnas que se crean a trav??s de c??digo en Python y utilizando la librer??a **Panel**. Dentro de estas filas y columnas se pueden ubicar los objetos que deseemos. Los gr??ficos se hicieron con las librer??as
**Hvplot**, **Holoviews** y **matplotlib**, esta ??ltima para utilizar funciones de agregaci??n.

<hr>
<hr>
