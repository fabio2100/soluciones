### Problema ###

* Se tiene un *backend* desarrollado en *express JS* que debe comunicarse con un servicio externo, el cual manejará distintas *urls* según se trate de distintos entornos: desarrollo y dos ambientes de producción
* Hay un desarrollo hecho que presenta inconvenientes, ya que las *urls* están definidas en lugar que no les corresponde y de manera absoluta, por lo cual para cada entorno hay que modificarlas según corresponda, ingresando a lugares donde un administrador del sistema no debería ingresar
* Para los entornos de producción, la aplicación tiene una política de *same origin*, con lo cual se pide que sea automatizada la detección del origen de acuerdo la información presente en la *request*

### Solución ###

* Debido a que son demasiadas funciones las que van a hacer uso de esta mejora, se opta por crear un *middleware*, que será introducido antes de cada función que requiere el reconocimiento de la *url de origen*
* Se crea además una variable dentro del archivo *.env* tipo *booleana* que determina si se trata de un entorno de producción o desarrollo
* Luego, el *middleware* se encargará de recibir la *url*, constatar si se trata de un entorno de producción o desarrollo y agregar un nuevo valor a la *request* con la *url base* que se usará para comunicarse con el servidor externo