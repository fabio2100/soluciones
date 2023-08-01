### Situación inicial
* Se tiene desarrollado un sistema que trabaja con *NodeJS(Express server)* y que usa una base de datos *Mongo*
* Dicho sistema se encuentra en funcionamiento y permite registrar *usuarios* usando como identificado el *email*
### Modificación solicitada
* Se requiere que se valide el mismo *email* con el que el *usuario* desea registrarse en otra tabla de una base de datos totalmente independiente, incluso del sistema, la cual está desarrollada en *PostgresSQL*
### Solución lograda
* Se modifica la lógica con la cual se guarda el usuario (se realiza una validación con *User.find* y si la supera se realiza *User.save*)
* La parte anterior mencionada se coloca dentro de una función, la cual devolverá una *promise*, resolviéndose o rechazándose según la condición del paso anterior
* Se realiza un post hacia la otra base de datos usando *Axios* y enviando como parámetro el *email*
* En el otro sistema se crea una función que hace uso del módulo *pg* (Este sistema también se encuentra desarrollado en *NodeJS*), la cual realiza una consulta *SELECT COUNT* sobre la tabla correspondiente y devolverá distintos estados de protocolos *http* según fallo de servidor(500), el correo electrónico ya se encuentra usado en esta tabla (401) o se puede registrar el *email* acá(204)
* Luego, se colocan ambas funciones dentro de un *Promise.all* y según se resuelvan correctamente se procede a *User.save* o al rechazo de la operación con la información indicada 