Memoria

Datos climáticos obtenidos por Red de Estaciones Agroclimáticas [2002-2020]. Red de Alerta e Información Fitosanitaria (RAIF)

1.- Introducción:
En este trabajo, transformaremos un conjunto de datos basados en el registro de distintas variables meteorológicas en estaciones meteorológicas de Andalucía. Concretamente se trata de datos climáticos obtenidos por la red de estaciones agroclimáticas de la Red de Alerta e Información Fitosanitaria (RAIF). 
La transformación a datos enlazados permitirá la explotación de los mismos.

2.- Proceso de transformación

2.1.- Selección de la fuente de datos
Estos datos se obtienen del portal de la Junta de Andalucía de datos abiertos (https://www.juntadeandalucia.es/datosabiertos/portal/dataset/raif-clima).
Los requisitos de selección de la fuente de datos serán:

  2.1.1.- Escenario real: datos climáticos de la red de estaciones agroclimáticas de Andalucía.
  
  2.1.2.- Disponibilidad de los datos: 
  
  2.1.2.1.- Datos en un formato procesable automáticamente: los datos están comprimidos en un .zip, que contiene ficheros .xml.
  
  2.1.2.2.- Licencia. Reconocimiento 4.0 Internacional (CC BY 4.0) 
  
  This is a human-readable summary of (and not a substitute for) the license. Advertencia. 
  Usted es libre de:
  
  •	Compartir — copiar y redistribuir el material en cualquier medio o formato
  
  •	Adaptar — remezclar, transformar y crear a partir del material
  
  •	para cualquier finalidad, incluso comercial.
  
  •	El licenciador no puede revocar estas libertades mientras cumpla con los términos de la licencia.
  
  Bajo las condiciones siguientes:
  
  • Reconocimiento — Debe reconocer adecuadamente la autoría, proporcionar un enlace a la licencia e indicar si se han realizado cambios<. Puede hacerlo de cualquier manera         razonable, pero no de una manera que sugiera que tiene el apoyo del licenciador o lo recibe por el uso que hace. 
  
  •	No hay restricciones adicionales — No puede aplicar términos legales o medidas tecnológicas que legalmente res trinjan realizar aquello que la licencia permite.
  Avisos :
  
  •	No tiene que cumplir con la licencia para aquellos elementos del material en el dominio público o cuando su utilización esté permitida por la aplicación de una excepción o       un límite.
  
  •	No se dan garantías. La licencia puede no ofrecer todos los permisos necesarios para la utilización prevista. Por ejemplo, otros derechos como los de publicidad, privacidad,     o los derechos morales pueden limitar el uso del material.
  2.1.3.- Posibilidad de enlazar con entidades genéricas (lugares)

2.2.- Análisis de datos
Al descomprimir el zip, disponemos de 3 tipos de ficheros:

•	Datos: Clim_Diario_2020.xml, Clim_Diario_2019.xml … Cargaremos sólo 2020, por agilidad en los procesos y capacidad de computación.

•	Descripción de los campos: Descripcion_Campos.xml.

•	Datos sobre las estaciones: Identificacion_EstacionesClima.xml.

En la descripción de los campos, los nombres no coinciden completamente con los campos que después encontramos en el fichero de datos, pero son fácilmente reconocibles:

![descripcion campos](imagenes/descripcion_campos.png)

Al importar de xml de datos (Clim_Diario_2020.xml), aparecen 20 líneas en blanco por cada registro (hay 20 campos). Las eliminamos con herramientas de OpenRefine.

![Filas en blanco](imagenes/filas_en_blanco.png)

Cambiamos el nombre de las columnas, porque al cargar, OpenRefine les ha antepuesto el primer tag que aparece en el xml.

![Cambio de nombre](imagenes/cambio_nombre.png)

Transformamos las columnas que son números en numéricas. Son todas las columnas menos el código de estación y la fecha de anotación del registro.

Obtenemos los siguientes tipos de datos:

![descripcion fichero datos](imagenes/campos_en_fichero_datos.png)

Con las facetas, podemos analizar para una columna, sus valores máximos, mínimos, nulos, etc.
Añadimos una columna, unión de COD_EST y FECHA para tener un identificador único de cada registro.

![Identificador unico](imagenes/identificador_unico.png)

Finalmente, utilizando el fichero de datos de estaciones (Identificacion_EstacionesClima.xml), añadimos estos datos a nuestro dataset, uniendo por código de estación:

NOMBRE	PROVINCIA	LATITUD	ALTITUD	LONGITUD	MUNICIPIO

Expresión para join con otro dataset, por identificador de estación:

cell.cross("Datos enlazados.Identificacion_EstacionesClima","ID_EST").cells["NOMBRE"].value[0]

![Se añade nombre de la estación](imagenes/add_column.nombre.png)
![Se añade nombre de la estación](imagenes/add_column.provincia.png)

Resulta el siguiente dataset:

![dataset](imagenes/dataset.png)

2.3.- Estrategia de nombrado de recursos

Usaremos ‘#’ para términos ontológicos.

Usaremos ‘/’ para individuos.

Dominio: https://raif-clima.datosenlazados.es

Ontología: https://raif-clima.datosenlazados.es/ontology#

Recursos: https://raif-clima.datosenlazados.es/recursos/

Estaciones: https://raif-clima.datosenlazados.es/recursos/estaciones

2.4.- Desarrollo del vocabulario

Usaremos la siguiente ontología, que parece que se puede ajustar bastante bien a los datos que tenemos:

The Aemet Network of Ontologies

que tiene el siguiente grafo conceptual:

![grafo ontologia AEMET](imagenes/grafo_ontologia_AEMET.png)


