# Romper la autorización (***Broken Access Control***).

     

Requisitos:
1. Máquina ***Router-Ubu***.
2. Máquina ***Kali Linux***.
3. Máquina ***Ubu_srv_01***

Una aplicación incorrecta de los permisos de la aplicación puede conducir a que un usuario pueda realizar actividades que en principio no debería poder realizar. Estos privilegios pueden ser usados para eliminar archivos, ver información confidencial o instalar malware. Habitualmente ocurre cuando un sistema presenta vulnerabilidades que permiten saltarse el sistema de autorización.

## Ejercicio 1: Eliminar las reseñas de 5 estrellas de los clientes.

***OBJETIVO***: Eliminar las mejores reseñas.

***PISTAS***: 

* Necesitarás realizar un hack previo para conseguir logarte como administrador. Concretamente el laboratorio 25-D: Iniciar sesión con el usuario administrador.

***RESOLUCIÓN***. Los pasos para resolver el reto son.

Ve a la página de login.
```
http://192.168.20.80:3000/#/login
```

Lógate como administrador poniendo en el email lo siguiente.
```
' or 1=1--
```

y en el password el que quieras.

Ve a la sección de administración de la aplicación.
```
http://192.168.20.80:3000/#/administration
```

Elimina las reseñas de 5 estrellas haciendo clic en el icono de la papelera.

![borrar](../img/lab-25-H/202311101949.png)

Aunque este reto se consigue suplantando la identidad del administrador, demuestra que es necesario implementar mecanismos más robustos para poder realizar ciertas acciones en la aplicación, como por ejemplo eliminar las reseñas. Aplicar una 2FA podría evitar este tipo de ataques o reducir el riesgo.


## Ejercicio 2: Poner una reseña a nombre de otro usuario.

***OBJETIVO***: Suplantar la identidad de otro usuario en una reseña.

***PISTAS***: 

* Usa Burp para determinar cómo se envía la información de reseña de un usuario anónimo.

***RESOLUCIÓN***. Los pasos para resolver el reto son.

Inicia Burp y desactiva la interceptación.

Si estás logado desconéctate.

Ahora vamos a poner una reseña anónima, puesto que no estamos logados a la aplicación. Para ello Selecciona la opción ***Customer feedback*** en el menú de la izquierda.

![borrar](../img/lab-25-H/202311102021.png)

Observa cómo la reseña es anónima y se le ha dado la puntuación mínima (1 estrella). NO HAGAS clic en el botón ***Submit***.

![Reseña anónima](../img/lab-25-H/202311102022.png)

Activa la interceptación de Burp y luego haz clic en el botón ***Submit***.

Como puedes observar en la imagen, la información que se envía al servidor es la lógica. Haz clic en ***Drop*** para no enviar la reseña.

![Drop](../img/lab-25-H/202311102024.png)

Vuelve a Firefox, activa las herramientas del desarrollador y estudia el código relacionado con el formulario. Para facilitar la práctica, localiza el campo ***userID***.

Observarás que hay un campo con ese nombre, de tipo ***input*** que está oculto.

![Hidden](../img/lab-25-H/202311102025.png)

Elimina el atributo ***Hidden*** y verás cómo se renderiza el control en el formulario.

![Nuevo campo](../img/lab-25-H/202311102026.png)

Tiene toda la pinta que, cuando el usuario está logado, se envía su identificador a través de este campo oculto. Escribe un valor, por ejemplo ***15*** y haz clic de nuevo en el botón ***Submit***. Burp capturará la request. Si tienes problemas, vuelve a cargar la página e inténtalo de nuevo.

Localiza la requests y envíala al ***Repeater***. Luego ve a la herramienta ***Repeater***.

![Nuevo campo](../img/lab-25-H/202311102027.png)

Envía la request y observa la response. Efectivamente, como sospechamos se ha enviado el identificador de usuario. 

![id 15](../img/lab-25-H/202311102028.png)

Solo queda mejorar el ataque e introducir el id de un usuario "importante" en la aplicación, por ejemplo, el administrador. En hackeos previos fuimos capaces de obtener los ids de todos los usuarios. El del administrador es el.












***FIN DEL LABORATORIO***


