## Lab 2 - Programación Orientada a Objetos 2021

### TrendingTopics

## Configuración inicial

* Instalar Java 8.
  * Comprobar si lo tienen instalado y si es la versión correcta `$ java -v`
  * En ubuntu, se instala sólo con `sudo apt install openjdk-8-jdk`
  * Comprobar la variable de entorno `$JAVA_HOME`. Instrucciones [acá](https://docs.opsgenie.com/docs/setting-java_home)

* Instalar scala 2
  * https://docs.scala-lang.org/getting-started/index.html

* [Optional] Instalar Spark
  * Descargar Spark 2.4.7 def [sitio oficial](https://spark.apache.org/downloads.html)
  * Descomprimir en una carpeta, por ejemplo `/opt/spark`
  * Configurar `$SPARK_HOME` con el path a la carpeta de instalación


### TrendingNER

Trendingner es un programa que cuenta NERs con un modelo heurístico sencillo.
Una vez que hayan terminado la implementación, la entrada del programa es un archivo json con suscripciones con el siguiente formato:

```json
[
    {
        "url": "URL_TEMPLATE",
        "urlParams": ["PARAM1", "PARAM2"],
        "urlType": "rss or reddit"
    }
]
```
El programa imprime las 20 entidades nombradas con mayor frecuencia.

#### Ejecución

El programa toma un único argumento opcional con el nombre del archivo json con
las suscripciones. Para ejecutarlo, utilicen uno de los siguientes comandos:

```bash
$ sbt run
$ sbt "run <json_filename>"
```

### trendingner_spark

Trendingner es un programa que cuenta NERs con un modelo neuronal pre-entrenado de Spark.
Tiene las mismas funcionalidades que  `trendingner`.

Para ejecutarlo, asegúrate de tener:
* Una buena conexión wifi
* Al menos 8GB de memoria RAM
* Un cpu multinúcleo razonablemente moderno

#### Ejecución

Antes de ejecutar el servicio por **primera vez** es necesario
configurar la biblioteca log4j si no lo has hecho antes:

```bash
cd $SPARK_HOME/conf # Folder where you installed SPARK, maybe /opt/spark
cp log4j.properties.template log4j.properties
```

Para compilar y ejecutar el servicio, ejecute:

```bash
sbt assembly
$SPARK_HOME/bin/spark-submit --class "edu.paradigmas.TrendingNer" --master local[2] --num-executors 2 --executor-memory 1g --driver-memory 1g target/scala-2.11/TrendingNER-assembly-0.1.0-SNAPSHOT.jar
```

## Estilos

Para corroborar el estilo de código, ejecutar:
```bash
$ sbt scalastyle
```