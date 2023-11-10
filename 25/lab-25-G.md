# Validación de datos de entrada inapropiada (***Improper Input Validation***).

     

Requisitos:
1. Máquina ***Router-Ubu***.
2. Máquina ***Kali Linux***.
3. Máquina ***Ubu_srv_JUICE_SHOP***

La pricipal amenaza a la que se ve sometida una aplicación web es la ausencia o un control incorrecto del texto que puede introducir un atacante en un campo de formulario o parámetro en general. Es conocido por todos que si usas un buen framework de desarrollo, éste debería proteger tu aplicación frente a este tipo de debilidades.

## Ejercicio 1: Registrar a un usuario con privilegios de administrador. 

***OBJETIVO***: Conseguir que un usuario convencional acceda a la parte de administración de la aplicación.

***PISTAS***: 

* Estudia la ***Request/Response*** que se genera cuando se registra un nuevo usuario. 
* Reenvía la request cambiando algún parámetro.

***RESOLUCIÓN***. Los pasos para resolver el reto son.

Como siempre iniciamos ***ZAP***.

Realiza con ZAP una exploración manual sobre la siguiente URL.
```
http://192.168.20.80:3000
```

A continuación registra un nuevo usuario, tal y como se muestra en la imagen.
(Nota: observa la URL en la que se crea el usuario)

![Register](../img/lab-25-G/202311031911.png)

Pulsa el botón para crear el usuario.

Intenta entrar en la sección ***Administration***, escribiendo la siguiente URL en la barra de direcciones.
(Nota: Esta sección se descubrió en el ***Ejercicio 2*** del laboratorio ***lab-25-C***)
```
http://192.168.20.80:3000/#/administration
```

![403](../img/lab-25-G/202212051116.png)


A continuación, accede a ZAP y localiza en el historial, la request que registró al usuario. Esta request es de tipo ***POST***. (Filtrar por POST)

![Request POST](../img/lab-25-G/202311031917.png)

En la Request puedes observar los campos que se envían al servidor para crear al nuevo usuario.

![Request](../img/lab-25-G/202311031927.png)

Y la response indica que el ***role*** del usuario es ***customer***.

![Response](../img/lab-25-G/202212051053.png)

Hacemos clic derecho en la request anterior y elegimos ***Open/Resend with Request Editor*** para editarla.

Modifica los parámetros hasta que tengan la siguiente forma.

![Otra Request](../img/lab-25-G/202212051101.png)

Hacemos clic en el botón ***Send***.

En la respuesta podrás ver que la API ha aceptado la creación del usuario de esta forma tan simple.

![Otra Response](../img/lab-25-G/202311031942.png)

Observa como la response es aceptada ***success***. Mira también los valores para los campos ***email*** (otraprueba@gmail.com) y ***role*** (admin). El password es el que pusiste.

Cierra la sesión con el usuario actual e inicia sesión con el nuevo usuario. A continuación escribe en la barra de direcciones la siguiente URL.
```
http://192.168.20.80:3000/#/administration
```

Podrás comprobar que puedes acceder a la sección de administración de la aplicación.

![Administración](../img/lab-25-G/202212051124.png)


## Ejercicio 2: Hacer un pedido que te hará rico.

***OBJETIVO***: Conseguir que el total a pagar de un pedido sea una cantidad negativa.

***PISTAS***: 

* Haz un pedido. Modifica la cantidad del elemento que has pedido y estudia la request correspondiente.
* Reenvía la request cambiando algún parámetro.

***RESOLUCIÓN***. Los pasos para resolver el reto son.

Como siempre iniciamos ***ZAP***.

Realiza con ZAP una exploración manual sobre la siguiente URL.
```
http://192.168.20.80:3000
```

Inicia sesión con tu usuario de la aplicación y haz un pedido de una unidad de zumo de limón. Podrás comprobar que es posible cambiar la cantidad, pero que esta no puede ser negativa. 

![Zumo de limón](../img/lab-25-G/202212052029.png)

Cambia la cantidad de producto a ***5 unidades***.

Localiza la request que actualiza la cantidad de producto a ***5 unidades***. 

![Request 5 unidades](../img/lab-25-G/202311041123.png)

Haz clic en ella con botón derecho y ejecuta ***Open/Resend with Request Editor***. Edita el parámetro ***quantity*** y pon una cantidad negativa, por ejemplo ***-100***.

![Request -100 unidades](../img/lab-25-G/202311041126.png)

Reenvía la Request por medio del botón ***Send***.

A continuación, en la aplicación realiza el proceso de ***Checkout*** y comprobarás que tendrás más dinero que antes.

![Rico](../img/lab-25-G/202212052021.png)


## Ejercicio 3: Registrar un usuario con privilegios de administrador.

***OBJETIVO***: Conseguir registrar un usuario como administrador enviando una request al servidor.

***PISTAS***: 
* Registra un usuario en la aplicación y captura la request que se envía al servidor.
* Compárala con una request de un administrador real (En un reto anterior aprendiste a convertirte en administrador) y busca en qué se diferencia un usuario administrador de un cliente normal.
* Reenvía la request original para registrar otro usuario con permisos de administrador.
* Usa ZAP o Burp.

***RESOLUCIÓN***. Los pasos para resolver el reto son.

Inicia Burp y configura el navegador para que lo use como proxy. Desactiva la interceptación de Burp.

Carga la página para registrar un nuevo usuario.
```
http://192.168.20.80:3000/login#/register
```

Rellena el formulario con la siguiente información.

Email.
```
prueba@hotmail.com
```

Password.
```
Pa55w.rd
```

Repeat Password.
```
Pa55w.rd
```

Como pregunta de seguridad, elige la que te apetezca. Rellena también la respuesta a dicha pregunta.

NO HAGAS clic aún en el botón ***Register***

En Burp, activa la interceptación.

Regresa al navegador y haz clic en ***Register***. Vuelve a Burp y haz clic en el botón ***Forward*** hasta alcanzar la request que nos interesa. Debe ser parecida a esta.

![Request](../img/lab-25-G/202311041126.png)

En la request puedes ver los campos que se envian al servidor. Sería interesante conocer cuáles son los enviados cuando el usuario es un administrador. Para facilitar la elaboración de esta práctica te aportamos esa información. No obstante, si quieres obtenerla por tí mismo, vuelve a realizar el laboratorio donde nos logamos como administrador. El laboratorio es ***lab-25-D Ejercicio 4. Iniciar sesión con el usuario administrador***.

En la siguiente imagen puedes ver dos request enviadas al servidor. Una para cuando el usuario es administrador y la otra cuando es un cliente.

![Request2](../img/lab-25-G/202311041126.png)

Si te das cuenta, la única diferencia importante está en el campo ***role***, que tiene el valor ***admin*** o ***customer***.

En Burp, vamos a modificar la request que tenemos capturada, agregando ***role=admin***, tal y como puedes ver en la siguiente imagen.

![Role Admin](../img/lab-25-G/202311041126.png)

Haz clic en el botón ***Forward*** para enviar la Request al servidor y desactiva la interceptación.

Inicia sesión con el usuario que has creado.

Email.
```
prueba@hotmail.com
```

Password.
```
Pa55w.rd
```

Accede a la sección de administración.
```
http://192.168.20.80:3000/#/administration
```

Podrás comprobar que eres administrador de la aplicación.










***FIN DEL LABORATORIO***
