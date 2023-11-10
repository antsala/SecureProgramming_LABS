# SecureProgramming_LABS

Laboratorios para las formaciones de Programación Segura están en la URL https://github.com/antsala/SecureProgramming_LABS.git


## Carpeta 00. Despliegue del laboratorio.

1. Laboratorio 00: ***Preparación del entorno de laboratorio en Windows***. Los ejercicios a realizar son:
   - Instalación de VirtualBox para Windows.
   - Descarga de las OVAs de la VMs.
   - Importación y configuracion de la VM ***Router-ubu***.
   - Importación y configuracion de la VM ***KaliLinux2022_2***.
   - Importación y configuracion de la VM ***Ubu_srv_JUICE_SHOP***.
   - Clonado del repositorio de GitHub.

## Carpeta 25. Ataque a aplicaciones Web.

1. Laboratorio 25-A: ***OWASP*** y la "Tienda de Zumos". Los ejercicios a realizar son:
   - ¿Qué es ***Juice Shop***?
   - Instalación de ***Juice Shop***.
   - Instalación de ***OWASP ZAP***.

2. Laboratorio 25-B: Aprender a usar ***Juice Shop***.

3. Laboratorio 25-C: Descubrir el ***ScoreBoard*** y la sección ***Admin***.
   - Descubrir el "Scoreboard"
   - Descubrir la sección "Admin"

4. Laboratorio 25-D: Ataques de Inyección.
   - Hacer un pedido de la oferta especial de navidad de 2014.
   - Exfiltrar el esquema de la base de datos.
   - Obtener las credenciales de todos los usuarios.
   - Iniciar sesión con el usuario administrador.
   - Iniciar sesión con un usuario que ni siquiera existe.


5. Laboratorio 25-E: Romper la autenticación (***Broken Authentication***).
   - Cambiar el password del usuario ***Bender*** sin usar ni inyección de SQL ni la opción ***Contraseña olvidada***.
   - Romper la autenticación 2FA.
   - Resetear el password del usuario Bjoern a través del mecanismo de contraseña olvidada.
   - Iniciar sesión con la cuenta de Gmail de Bjoern.
   - Resetear la contraseña del usuario ***Bender*** por medio del mecanismo de contraseña olvidada.
   - Resetear la contraseña del usuario ***Jim*** por medio del mecanismo de contraseña olvidada.

6. Laboratorio 25-F: Exposición de datos sensibles (***Sensitive Data Exposure***).
   - Acceder a un documento confidencial.
   - Ganar acceso a los logs del servidor.
   - Fuga de información a través de la API.
   - Acceder a un archivo de backup olvidado por un programador.
   - Localiza el endpoint que sirve datos de uso de la aplicación para que sean leídos por un popular sistema de monitorización.
   - Robar los datos personales de otro sin usar inyección.
   - Localizar en Internet información fugada del password de un usuario.
   - Determina la respuesta a la pregunta de seguridad de ***Emma***.


7. Laboratorio 25-G: Validación de datos de entrada inapropiada (***Improper Input Validation***).
   - Registrar a un usuario con privilegios de administrador. 
   - Hacer un pedido que te hará rico.
   
8. Laboratorio 25-H: Romper la autorización (***Broken Access Control***).