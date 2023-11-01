# Configuración del entorno de laboratorio basado en VirtualBox.

## Ejercicio 1: Instalación de VirtualBox para Windows.

Aunque existen muchos hipervisores para realizar las prácticas, en este curso hemos elegido ***VirtualBox*** de Oracle. Los procedimientos que se describen vienen referidos a este hipervisor.

Para instalar VirtualBox en Windows, debemos seguir los pasos indicados en: https://www.virtualbox.org/

Se recomienda crear una carpeta para ubicar los archivos de las máquinas virtuales. Desde la terminal de Windows ejecutamos:
```
mkdir C:\VMs
```

También es conveniente indicar a VirtualBox esta carpeta como repositorio de las nuevas VMs que se crearán. Para ello, en la herramienta de administración de VirtualBox, elegimos ***Archivo/Preferencias***. En el cuadro de texto ***Carpeta predeterminada de máquinas***, escribimos:
```
C:\VMs
```

Hacemos clic en ***Aceptar***


## Ejercicio 2: Descarga de las OVAs de las VMs.

En la plataforma Moodle se publicará la URL de descarga de las VMs


## Ejercicio 3: Importación y configuracion de la VM ***Router-ubu***

En VirtualBox, elegimos la opción de menú ***Archivo/Importar servicio virtualizado***. Elegimos el archivo ***Router-ubu.ova***, que hemos descargado previamente, y hacemos clic en ***Siguiente***. En ***Política de dirección MAC*** elegimos ***Incluir todas las direcciones de adaptador de red***. Repasamos el resto de la configuración y hacemos clic en ***Importar***.

En la lista de máquinas virtuales, seleccionamos ***Router-ubu*** y comprobamos la  configuración. Los valores más importantes son los siguientes:

* *General*: Es una VM con sistema operativo ***Ubuntu*** que está configurada para actuar de ***router*** entre sus dos interfaces de red (comentado en breve)
* *Sistema*: Tiene asignada ***1 GB RAM*** y ***1 core*** que es más que suficiente para realizar su cometido.
* *Red*: IMPORTANTE!!! Tenemos dos adaptadores. El primero de ellos está conectado a una ***Red interna*** de VirtualBox, que hemos llamado ***Laboratorio***. El segundo adaptador, deberá mover el tráfico hacia la red física en la que está conectado tu equipo, por eso es del tipo ***Adaptador de puente***

Es el momento de repasar la configuración correcta para los adaptadores de red de ***Router-ubu***. En VirtualBox, con la máquina virtual seleccionada, hacemos clic en el botón ***configuración***, y en el panel izquierdo del cuadro de diálogo, seleccionamos ***Red***. Aparecerán cuatro pestañas donde podemos configurar los adaptadores de red (esta VM usa dos tarjetas, por lo que solo debemos fijarnos en las dos primeras pestañas)

La primera pestaña, llamada ***Adaptador 1*** es la que está asociada con la interfaz de red que conecta este router con la red ***laboratorio***. Debemos asegurar que en ***Conectado a*** aparece ***Red Interna*** y, en el ***nombre*** de la red interna, aparece ***Laboratorio***. Si no fuera así, corregirlo convenientemente.

La tarjeta "interna" tendrá configurada en el sistema operativo la dirección IP ***192.168.20.1*** (de la red de laboratorio), que será la puerta de enlace de todas las VMs que vamos a utilizar.


Ahora seleccionamos la segunda pestaña, llamada ***Adaptador 2***. Ahí tendrás que asegurarte que aparece la configuración ***Adaptador de puente*** en ***Conectado a*** y que has seleccionado en ***Nombre*** la interfaz de red ***FÍSICA*** mediante la cual tu equipo tiene conexión a la red local. Guardamos la configuración haciendo clic en ***Aceptar***. 

Iniciamos la VM ***Router-ubu***.

Iniciamos sesión con el usuario:
```
antonio
```


y el password:
```
Pa55w.rd
```

Es el momento de comprobar si la máquina tiene conexión con Internet. (Nota: CTRL+C cuando responda el ping)
```
ping www.google.es
```

Con esto hemos terminado la importación y configuración del router.


## Ejercicio 4: Importación y configuracion de la VM KaliLinux2022_2

En VirtualBox, elegimos la opción de menú ***Archivo/Importar servicio virtualizado***. Elegimos el archivo ***KaliLinux2022_2.ova***, que hemos descargado previamente, y hacemos clic en ***Siguiente***.  En ***Política de dirección MAC*** elegimos ***Incluir todas las direcciones de adaptador de red***. Repasamos el resto de la configuración y hacemos clic en ***Importar***.

En la lista de máquinas virtuales, seleccionamos ***KaliLinux2022_2*** y comprobamos la  configuración. Los valores más importantes son los siguientes:

* *General*: Es una VM con sistema operativo ***Ubuntu*** que tiene instalada la suite ***Kali***

* *Sistema*: Tiene asignada ***4 GB RAM*** y ***2 cores*** 
* *Red*: Su tarjeta de red está conectada a la ***Red interna*** llamada ***Laboratorio***. 

En VirtualBox, con la máquina virtual seleccionada, hacemos clic en el botón ***configuración***, y en el panel izquierdo del cuadro de diálogo, seleccionamos ***Red***. Aparecerán cuatro pestañas donde podemos configurar los adaptadores de red (esta VM usa una sola tarjeta, por lo que solo debemos fijarnos en primera pestaña).

La pestaña llamada ***Adaptador 1*** es la que está asociada con la interfaz de red que conecta a red ***laboratorio***. Debemos asegurar que en ***Conectado a*** aparece ***Red Interna*** y, en el ***nombre*** de la red interna, aparece ***Laboratorio***. Si no fuera así, corregirlo convenientemente.

La tarjeta  tendrá configurada en el sistema operativo la dirección IP ***192.168.20.9*** (de la red de laboratorio).


Guardamos la configuración haciendo clic en ***Aceptar***. 

Iniciamos la VM ***KaliLinux2022_2***.

Iniciamos sesión con el usuario:
```
antonio
```

y el password:
```
Pa55w.rd
```

Es el momento de comprobar si la máquina tiene conexión con Internet. (Nota: CTRL+C cuando responda el ping)
```
ping www.google.es
```

## Ejercicio 5. Importación y configuracion de la VM ubu_srv_JUICE_SHOP.

En VirtualBox, elegimos la opción de menú ***Archivo/Importar servicio virtualizado***. Elegimos el archivo ***ubu_srv_01.ova***, que hemos descargado previamente, y hacemos clic en ***Siguiente***.  En ***Política de dirección MAC*** elegimos ***Incluir todas las direcciones de adaptador de red***. Repasamos el resto de la configuración y hacemos clic en ***Importar***.

En la lista de máquinas virtuales, seleccionamos ***ubu_srv_JUICE_SHOP*** y comprobamos la  configuración. Los valores más importantes son los siguientes:

* *General*: Es una VM con sistema operativo ***Ubuntu Server 20.04***.

* *Sistema*: Tiene asignada ***3 GB RAM*** y ***1 cores***. En función de la capacidad de tu hardware podrías bajarla a ***1 GB RAM***.
* *Red*: Su primera tarjeta de red está conectada a la ***Red interna*** llamada ***Laboratorio***.

En VirtualBox, con la máquina virtual seleccionada, hacemos clic en el botón ***configuración***, y en el panel izquierdo del cuadro de diálogo, seleccionamos ***Red***. La pestaña llamada ***Adaptador 1*** es la que está asociada con la interfaz de red que conecta a red ***laboratorio***. Debemos asegurar que en ***Conectado a*** aparece ***Red Interna*** y, en el ***nombre*** de la red interna, aparece ***Laboratorio***. Si no fuera así, corregirlo convenientemente.

La tarjeta tiene configurada en el sistema operativo la dirección IP ***192.168.20.80*** (de la red de laboratorio).


Guardamos la configuración haciendo clic en ***Aceptar***. 

Iniciamos la VM ***ubu_srv_JUICE_SHOP***.

Iniciamos sesión con el usuario:
```
antonio
```

y el password:
```
Pa55w.rd
``` 

Con esto hemos terminado la importación y configuración de la máquina Ubu_srv_JUICE_SHOP.

## Ejercicio 6: Clonado del repositorio de GitHub.

Algunos laboratorios requieren tener ciertos archivos presentes en la máquina virtual. La forma más efectiva de conseguirlo es clonar el repositorio en dicha máquina virtual.

Abre una terminal y asegurate que el comando ***git*** está presente.
Nota: Si no estuviera instalado, descárgalo e instálalo.
```
git --version
```

```
cd $HOME

git clone https://github.com/antsala/SecureProgramming_LABS.git
```
