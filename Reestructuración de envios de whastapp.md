## Restructuración de envíos de Whatsapp

* Se tiene un sistema que permite enviar whatsapp con un mensaje predefinido, para ello se hace uso de *whatsapp api*. La función es muy simple, solo redirige a la *api*, donde el usuario selecciona el contacto y envía el mensaje predefinido

## Limitaciones de la funcionalidad a mejorar
* No se permite la carga de teléfonos
* Redirige a *whatsapp*, con lo cual obliga al uso de la cuenta de la aplicación actualmente activa, ya sea *whatsapp web* o la aplicación según sea *andriod o ios*
## Solución planteada
## Elección de api elegida y generación y almacenamiento de token
* Hacer uso de *wassenger*, una *api* que permite el envío de mensajes whatsapp
* En dicha plataforma, se debe de generar un token, el cual será almacenado para el usuario actual 
* Se crea una *migración* para agregar un nuevo campo en la tabla de usuarios, donde se colocará el token
* Para el almacenamiento del token, se agrega la funcionalidad en la *configuración* del usuario, agregando el campo, y luego se realiza un *update* incluyendo el nuevo campo
## Modificación del envío de whatsapp
* Hasta el momento, existía un botón desde el cual se abría directamente la aplicación *whatsapp* con el mensaje predefinido y se seleccionaba el contacto a enviar
* Esto se modifica, y al presional el mismo botón, se desplegará un *modal*, el cual contiene, en su body, dos *radio button* para seleccionar el tipo de envío de *whatsapp*, opción *api o wassenger*. Además se incluyen párrafos informativos, visibles o ocultos según opción elegida. Se agrega un *input* para agregar el número de teléfono. Este *input* se llenará automáticamente de acuerdo a si se encuentra almacenado el número de teléfono para el registro seleccionado. Además, existen *párrafos informativos* en estado *hidden* con los posibles resultados de las operaciones de la api *wassenger*
* En el *footer* del modal se dispone del botón para enviar, que variará según la funcionalidad elegida (de acuerdo al radio buttón)
* En caso de elegir el envío usando *api de whatsapp*, se comprobará la existencia o no de un número de teléfono. En caso de no existir, se abrirá la aplicación y se podrá elegir el usuario a enviar; mientras que si existe el número, la aplicación abrirá, con la diferencia de dirigir directamente al teléfono ingresado, y luego almacenará el número en el registro seleccionado para que sea visible la próxima vez que se intenta compartir dicho estudio. 
* Mientras que en caso de seleccionar *wassegener*, el número de teléfono pasa a ser obligatorio. Al presionar enviar ya habiendo ingresado un teléfono, se llamará al *endpoint* de un controlador del servidor con los datos proporcionados: nombre del usuario, mensaje predefinido y número de teléfono. Se debe llamar primero a un controlador propio debido a que *wassenger* exige realizar llamadas solo desde el *backend* como seguridad, para que el token no quede expuesto. Luego en nuestro controlador, con el nombre de usuario buscamos el *token* asociado al mismo, y con este *token* se realiza la petición al *endpoint de wassenger*. El *endpoint* responderá con sus posibles estados (error de token, número de teléfono asociado con formato incorrecto, número no registrado en *whatsapp*), desde los cuales en el controlador se elabora una respuesta y se envía al *frontend*. Dentro del *frontend* estas respuestas son procesadas según su estado y mostrarán temporalmente alguno de los *párrafos* que se encontraban en estado *hidden*
