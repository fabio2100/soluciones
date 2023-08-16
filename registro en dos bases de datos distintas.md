### Registro de usuarios en dos bases de datos distintas-> *mongo* y *postgresql*

* Se tiene que registrar un usuario dentro del ambas base de datos, y dar respuesta del éxito o fallo al intento del usuario de registrarse. 
* Las bases de datos y las tablas ya se encuentran creadas, con lo cual lo que se debe hacer es la escritura de ambas tablas de las bases de datos. 
* El registro se hace con correo electrónico, el cual es único para ambas tablas y debe confirmarse
* El sistema se encuentra en *NodeJS*

### Solución

* Se recibe la información del usuario. 
* Se crea una función para registrar el usuario en *postgresql* -> usando la librería *pg*. Se usa una *api* con otro sistema y se realiza la comunicación con protocolo *http*
* Se crea otra función para registrar el usuario en *mongo* -> Usando *mongoose*, la respuesta se trata con *promosas*
* Luego, se corren las funciones usando *Promise.All*, primero la que escribe sobre *postgresql*, en caso de acierto, se escribe sobre *mongo*
* En caso de acierto, se envía el correo electrónico de confirmación
* Si llega a fallar alguna de las dos escrituras, no se elimina nada en el momento 
* En caso que un usuario quiera registrarse, si no ha confirmado su correo electrónico, puede escribir el mismo correo, por lo cual es acá cuando se realiza el borrado