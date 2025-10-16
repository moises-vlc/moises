# Resumen Docker
## INTRODUCCIÓN A LOS CONTENEDORES Y A DOCKER
### VIRTUALIZACIÓN
**¿Qué es la virtualización?**

La virtualización es un conjunto de tecnologías de hardware y software que permiten la
abstracción de hardware, creando así la “ilusión” de administrar recursos virtuales como si fueran
recursos reales, de forma transparente para los usuarios.

Es muy utilizada para el despliegue de sistemas, desarrollo de software, análisis de
malware, escalado horizontal, etc.

**¿Qué es una máquina virtual?**

Una máquina virtual permite simular una máquina (con su sistema operativo) y
ejecutar programas como si estuvieran utilizando una máquina real e independiente.

Para la creación de máquinas virtuales generalmente existen varios tipos de tecnologías:
- Máquinas virtuales de proceso
- Emuladores
- Hipervisores
- Contenedores

**¿Qué es una máquina virtual de proceso?**

Las máquinas virtuales de proceso, son un tipo de máquinas virtuales que permiten ejecutar un
programa diseñado para un sistema operativo/arquitectura concreta (distinta de la máquina
actual), como un proceso más de nuestra máquina actual.

Algunos de los principales ejemplos de este tipo de virtualización son:
- Máquina virtual de Java (JVM): ejecuta los bytecodes de Java en cualquier sistema y
arquitectura que la tenga implementada.
- Plataforma .NET: análoga a la máquina virtual de Java con productos Microsoft.

**¿Qué es un emulador?**

Un hipervisor, es una máquina virtual que simula total o parcialmente un hardware de una
máquina, permitiendo la instalación de distintos sistemas operativos (por ejemplo, virtualizar un
sistema Windows 10 Home en una máquina real Linux).

### CONTENEDORES

**¿Qué son los contenedores?**

Los contenedores son una tecnología de virtualización, que al contrario que un hipervisor (que
trata de emular un sistema completo), utiliza el sistema base de la máquina anfitrión y actúa
realmente como un “entorno privado” que comparte recursos con el sistema anfitrión, sin
virtualizar el hardware completo. 

**Contenedores para desarrollo y despliegue de aplicaciones**

Uno de los principales usos de los contenedores (aunque no el único) es facilitar el desarrollo,
distribución y el despliegue de aplicaciones.
- Compilar software es tedioso. Utilizando un contenedor, tenemos el entorno de
compilación/depuración montado con las versiones que necesitamos.
- Usar contenedores facilita el testeo, permitiendo la creación de distintos entornos de
prueba con diferentes configuraciones, etc.
- Los contenedores nos evitan problemas de compatibilidad al desplegar nuestras
aplicaciones, teniendo siempre las versiones adecuadas para ejecutar nuestro software.

**Contenedores para despliegue de servicios**

Otro de los principales usos de los contenedores es el despliegue de servidores de distinto tipo
(web, correo, bases de datos, DNS, etc.).

Además, los contenedores facilitan el “escalado horizontal” de servicios, especialmente si se
apoyan de herramientas llamadas orquestadores.

**Ventajas e inconvenientes del uso de contenedores**

Algunas de las ventajas del uso de contenedores son:
- Los contenedores ocupan menos espacio, al no tener que replicar en cada uno el sistema
operativo que están virtualizando, ya que utilizan el sistema de la máquina anfitrión.
- Multitud de empresas de software (Microsoft, Apache, Nginx, MySQL, Oracle, Wordpress,
Moodle, y un largo etc.) apoyan estas tecnologías y dan soporte tanto incorporando
sistemas de contenedores a sus sistemas operativos, como ofreciendo imágenes oficiales
de sus productos.

Algunas de las principales desventajas de los contenedores son:
- Pese a que mejoran enormemente la velocidad respecto a una virtualización por hipervisor,
siguen teniendo un rendimiento peor que una ejecución “bare metal”.
- La persistencia y el acceso/modificación a datos persistentes entre contendores es más
tedioso que si se realiza sobre una máquina real.
-  Los contenedores están pensados generalmente para el uso vía línea de comandos.

### CONTENEDORES EN SISTEMAS LINUX
**¿Es nuevo el concepto de entornos privados en sistemas Unix?**

El concepto de entornos privados, utilizado en los controladores, no es algo novedoso de los
sistemas Unix modernos. Desde hace muchos años existían algunas soluciones tales como:
- Chroot (Sistemas Unix)
- Jail (FreeBSD)

Estas utilidades son los “abuelos” del concepto actual de contenedor en los sistemas Unix.

**Sistemas privados modernos en Linux: contenedores**

En el año 2008, aparecen los contenedores modernos de sistemas Linux, con el sistema LXC (LinuX
Container). Para su desarrollo, se introdujeron nuevas capacidades en el kernel de Linux, que han
sido aprovechadas por otros sistemas de contenedores

**¿Cómo funcionan los contenedores modernos en Linux?**

Los sistemas más populares de contenedores sobre Linux, han utilizado (entre otras) dos
características del kernel aparecidas en versiones relativamente recientes:
- Linux namespaces: permite aislar procesos de forma que vean unos recursos concretos.
Los procesos que tienen un “namespace” común pueden ver recursos comunes.
- Cgroups: permite aislar, configurar y limitar el uso de recursos(memoria, procesos, E/S,
etc.).

**¿Puedo poner en marcha un contenedor Linux “A mano”?**

Sí, es posible. Tal como nos muestra la conocida autora de materiales en formato comic Julia
Evans, aquí un ejemplo de script donde se muestra como crear un contenedor de Linux “a mano”.

**Los contenedores Linux ¿Pueden funcionar en sistemas como Windows o MacOS?**

En principio, es posible ejecutar contendores Linux en sistemas diferentes a Linux, aunque es
posible que el rendimiento no sea el mismo. Algunos sistemas, para poder utilizar contenedores
Linux, necesitan que un hipervisor virtualice un sistema Linux completo y que desde ahí se lancen
los contenedores Linux.

### CONTENEDORES DOCKER

**¿Qué es Docker?**

Docker es un sistema de contenedores Linux que utiliza las características del núcleo de Linux para
permitir el desarrollo y despliegue de aplicaciones.

Docker es un proyecto de código abierto. Generalmente, dispone de varias versiones:
- Docker CE (Community Edition): el motor de Docker, de código abierto.
- Docker EE (Enterprise Edition): lo mismo que la versión CE, solo que además incluye
certificación de funcionamiento en algunos sistemas concretos y soporte con la empresa
Docker Inc.

**La arquitectura de Docker**

Esta arquitectura, la podemos resumir en 3 partes:
- Cliente: es el software encargado de comunicarse con el servidor Docker.
- Servidor (Docker Host): servicio Docker, donde se atienden a las peticiones de los clientes y
se gestionan los contenedores e imágenes.
-  Registro (Registry): lugar donde se almacenan imágenes Docker (públicas o privadas).
Incluso, de una misma imagen, se almacenan las distintas versiones.

## INSTALACIÓN DE DOCKER

### INSTALACIÓN DE DOCKER EN SISTEMAS LINUX (UBUNTU)

**Instalación desde el repositorio oficial de Ubuntu**

Es posible instalar Docker Engine desde el repositorio oficial de Ubuntu, pero no está
recomendado, ya que instala versiones antiguas. 

**Instalación desde el repositorio de Docker-CE**

A continuación detallaremos los pasos para instalar Docker Engine CE en Ubuntu desde el
repositorio oficial de Docker CE. Las versiones de Ubuntu soportadas (todas de 64 bits) son:
- Ubuntu Kinetic 22.10
- Ubuntu Jammy 22.04 (LTS)
- Ubuntu Focal 20.04 (LTS)
- Ubuntu Bionic 18.04 (LTS)

**Paso 1: Eliminando versiones antiguas de Docker Engine**

En primer lugar, deberemos eliminar otras versiones de Docker, por si estuvieran instaladas.

Para eliminar las versiones antiguas puede bastarnos con la orden:

- sudo apt-get remove docker docker-engine docker.io containerd runc

**Paso 2: Incluyendo el repositorio de Docker CE**

Para poner en marcha el repositorio, lo primero que haremos será actualizar nuestro índice de
paquetes y tras ello, instalar los paquetes necesarios (si no lo estaban ya) para que se puedan
utilizar repositorios con HTTPS.
- sudo apt-get update
- sudo apt-get install apt-transport-https ca-certificates curl
gnupg-agent software-properties-common

Una vez realizado este paso, descargamos la clave GPG del repositorio de Docker CE y la
incluiremos. Podemos hacer todo con las siguientes líneas
- sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o
/etc/apt/keyrings/docker.gpg

Ahora, solo nos queda añadir el repositorio de Docker CE como fuente para instalación de
paquetes.
- lsb_release -cs

**Paso 3: Instalando Docker Engine CE**

Por último, ya con el repositorio oficial de Docker en nuestro sistema, solo nos queda actualizar el
índice de paquetes e instalar la última versión de Docker Engine CE de la siguiente forma:
- sudo apt-get update

Finalmente, comprobaremos que Docker Engine CE se ha instalado correctamente ejecutando:
- sudo docker version

**Post instalación**

En la documentación de Docker, nos proponen algunos pasos de post instalación. Los podéis
consultar en https://docs.docker.com/engine/install/linux-postinstall/
En esta sección vamos a comentar dos de ellos: administrar Docker con usuarios sin privilegios (no
root ni sudoers) y arrancar Docker desde al inicio.

**Permitir administrar Docker con usuarios sin privilegios**

Docker utiliza sockets Unix. Para la creación y reserva de un socket Unix, es necesario tener
permisos de root, por lo cual Docker Engine necesita permisos de root para ejecutarse.

A veces, en algunos contextos, puede sernos útil que Docker se ejecute por usuarios sin permisos
de root.

Podemos configurar el aula para que dichos alumnos puedan utilizar Docker sin necesidad de proporcionarles una cuenta con permisos de root.

Para ello, en primer lugar crearemos un grupo llamado “docker”.
- sudo groupadd docker

Tras ello añadiremos a los usuarios que queremos que usen Docker sin permisos de root al grupo
con un comando similar al siguiente, donde $USER es el nombre de usuario:
- sudo usermod -aG docker $USER

**Activar/desactivar arranque al inicio**

Para indicar que el servicio de Docker se inicie al arrancar la máquina, podemos indicarlo mediante
los siguientes comandos:
- sudo systemctl enable docker.service
- sudo systemctl enable containerd.service

Si lo que queremos es deshabilitar este arranque automático, podemos usar:
- sudo systemctl disable docker.service
- sudo systemctl disable containerd.service

Para iniciar/parar/reiniciar los servicios manualmente, podemos usar:
- sudo systemctl start/stop/restart docker.service
- sudo systemctl start/stop/restart containerd.service

**2.4 Desinstalando Docker en Ubuntu**

Si en algún momento queremos desinstalar Docker en Ubuntu, podemos usar el comando
- sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin
docker-compose-plugin

Este comando eliminará Docker Engine, pero no eliminará contenedores e imágenes presentes en
el sistema. Si queremos eliminar estos datos, tenemos dos opciones.

La primera consiste en, previamente a la eliminación de Docker Engine, ejecutar el comando:
- sudo docker system prune -a

La segunda opción, se debe realizar tras eliminar Docker y consiste en el borrado manual de las
mismas, con el comando:
- sudo rm -rf /var/lib/docker

### INSTALACIÓN DE DOCKER EN SISTEMAS WINDOWS

**Pasos previos Windows 10 Pro y Windows Server: activando Hyper-v**

En este enlace se explica cómo habilitar Hyper-V en:
- Windows 10 Pro: https://docs.microsoft.com/es-es/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v
- Windows Server: https://docs.microsoft.com/es-es/windows-server/virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server

**Pasos previos Windows 10 Home: Instalando WSL2**

Antes de comenzar, nuestro sistema debe tener instalado WSL2. La guía para instalarlo se
encuentra aquí https://docs.microsoft.com/en-us/windows/wsl/install-win10

A continuación un resumen de los pasos a realizar.

En primer lugar, utilizando una consola PowerShell con permisos de administrador, debemos
habilitar WSL. Lo podemos hacer con el comando.
- dism.exe /online /enable-feature
/featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

Una vez habilitado, debemos asegurarnos que tenemos nuestro Windows 10 Home actualizado, al
menos hasta la versión “Versión 1903, Build 18362”. Puedes comprobar tu versión ejecutando el
comando “winver”

Una vez actualizado y reiniciado el sistema, debemos habilitar la característica de “Virtual
Machine”, lo cual podemos hacerlo con una consola powershell con permisos de administrador:
- dism.exe /online /enable-feature /featurename:VirtualMachinePlatform
/all /norestart

Tras ello, deberás reiniciar tu máquina antes del próximo paso.

Finalizada la instalación, con una powershell con permisos de administrador, deberás establecer
WSL2 como la versión por defecto al instalar una distribución de Linux.
- wsl --set-default-version 2

Con esto ya tienes listo WSL2 y una versión de Ubuntu instalada en tu sistema Windows.

**Instalación de Docker Desktop**

La instalación de Docker Desktop, que es la versión de Docker CE para sistemas Windows, es
sencilla y básicamente consiste en descargar el instalador desde Docker Hub, en el siguiente enlace
https://hub.docker.com/editions/community/docker-ce-desktop-windows/ y seguir las
instrucciones de instalación en pantalla.

En este enlace se puede ver un video en el que se realiza la instalación
https://www.youtube.com/watch?v=_9AWYlt86B8

Finalmente, con Docker Desktop instalado y lanzado, comprobaremos que Docker Engine CE se ha
instalado correctamente ejecutando:
- docker version

###  INSTALACIÓN DE DOCKER EN SISTEMAS MACOS

Las instrucciones para la instalación de Docker Desktop en MacOS están descritas en
https://docs.docker.com/docker-for-mac/install/.

Para realizar esta instalación, básicamente debe descargarse el paquete “.dmg” de
https://hub.docker.com/editions/community/docker-ce-desktop-mac/ y seguir las instrucciones de
instalación en pantalla.

### PLAYGROUNDS DE DOCKER

En Internet existen varios sitios que nos permiten utilizar un “playground” de distintas
herramientas, para que juguemos con ellas online, sin necesidad de instalar ni configurar nada (y
sin el riesgo de romper cosas).

## PRINCIPALES ACCIONES CON DOCKER

###  IMÁGENES Y CONTENEDORES

**¿Qué es una imagen y un contenedor?**

 Algunos conceptos a tener en cuenta son:
 
***Imágenes***

La imagen es una plantilla de solo lectura que se utiliza para crear contenedores. A
partir de una imagen pueden crearse múltiples contenedores

Las imágenes, además de tener su sistema de ficheros predefinido, tienen una serie
de parámetros predefinidos (comandos, de variables de entorno, etc.) con valores
por defecto y que se pueden personalizar en el momento de crear el contenedor.

Docker permite crear nuevas imágenes basándose en imágenes anteriores.

***Contenedores***

Son instancias de una imagen.

Pueden ser arrancados, parados y ejecutados.

Cada contenedor Docker posee un identificador único de 64 caracteres, pero
habitualmente se utiliza una versión corta con los primeros 12 caracteres.

**¿Dónde se almacenan imágenes, contenedores y datos?**

El lugar donde se almacenan contenedores e imágenes puede variar según distribución/sistema
operativo, driver de almacenamiento y versión de Docker. Normalmente, mediante el siguiente
comando de Docker, podemos ver información del sistema, incluyendo el directorio de Docker.
- docker info

### REGISTRO: DOCKER HUB

Docker Hub es una “plataforma de registro” de Docker. Los servicios básicos son gratuitos y nos
permite registrar imágenes Docker, haciéndolas públicas o privadas.

### CREANDO Y ARRANCANDO CONTENEDORES CON “DOCKER RUN”

**¿Qué hace el comando “docker run”?**

Podríamos decir que este comando crea
un contenedor a partir de una imagen y lo arranca.

**Creando contenedores sin arrancarlos**

Para crear un contenedor sin arrancarlo (recordamos, “docker run” crea y arranca), existe el
comando “docker create”. 

**Repasando caso práctico “Hello World**

En anteriores unidades propusimos un sencillo caso práctico para comprobar que funcionaba
Docker usando el siguiente comando:
- docker run hello-world

###  LISTAR CONTENEDORES DISPONIBLES EN EL SISTEMA CON “DOCKER PS”

Mediante el comando “docker ps” podemos listar los contenedores en ejecución en el sistema. Si
ejecutamos el siguiente comando:
- docker ps

Lanzando el siguiente comando:
- docker ps -a

### PARANDO Y ARRANCANDO CONTENEDORES EXISTENTES CON “DOCKER START/STOP/RESTART”

Para arrancar/parar un contenedor ya creado (recordamos, “docker run” crea y arranca), existen
los comandos “docker start”, “docker stop” y “docker restart”

La forma más habitual de usar estos comandos, es usar el nombre del comando, seguido del
identificador único o nombre asignado al contendor. Por ejemplo, con identificador:
- docker start 434d318b3771
o con nombre del contenedor
- docker start stupefied_colden

### INSPECCIONANDO CONTENEDORES CON “DOCKER INSPECT”

El comando “docker inspect” es un comando que nos proporciona diversos detalles de la
configuración de un contenedor. Ofrece distintos datos, entre ellos, identificador único (versión 64
caracteres), almacenamiento, red, imagen en que se basa, etc. Su sintaxis es:
- docker inspect IDENTIFICADOR/NOMBRE

### EJECUTANDO COMANDOS EN UN CONTENEDOR CON “DOCKER EXEC”

El comando “docker exec” nos permite ejecutar un comando dentro de un contenedor que esté en
ese momento en ejecución. La forma sintaxis habitual para utilizar este comando es la siguiente
- docker exec [OPCIONES] IDENTIFICADOR/NOMBRE COMANDO [ARGUMENTOS]

Algunos ejemplos de uso, suponiendo un contenedor en marcha, llamando “contenedor”:
- docker exec -d contenedor touch /tmp/prueba

Ejemplo que se ejecuta en “background”, gracias al parámetro “-d”. Este ejemplo simplemente crea
mediante el comando “touch” un fichero “prueba” en “/tmp”.
- docker exec -it contenedor bash

Orden que ejecutará la “shell” bash en nuestra consola (gracias al parámetro “-it” se enlaza la
entrada y salida estándar a nuestra terminal). A efectos prácticos, con esta orden accederemos a
una “shell” bash dentro del contenedor.
- docker exec -it -e VAR1=1 contenedor bash

### COPIANDO FICHEROS ENTRE ANFITRIÓN Y CONTENEDORES CON “DOCKER CP”

El comando “docker cp” es un comando que nos permite copiar ficheros y directorios del anfitrión
a un contenedor o viceversa. No se permite actualmente la copia de fichero entre contenedores.

Algunos ejemplos de uso:
- docker cp idcontainer:/tmp/prueba ./

Copia el fichero “/tmp/prueba” del contenedor con identificador o nombre “idcontainer” al
directorio actual de la máquina que ejerce como anfitrión.
- docker cp ./miFichero idcontainer:/tmp

### ACCEDIENDO A UN PROCESO EN EJECUCIÓN CON “DOCKER ATTACH”

En algunos casos, deseamos enlazar la entrada o salida estándar de nuestra terminal a un
contenedor que está ejecutando un proceso en segundo plano, de forma similar a la siguiente
- docker attach [OPCIONES] IDENTIFICADOR/NOMBRE

Para probarlo utilizaremos el siguiente ejemplo:
- sh -c "while true; do $(echo date); sleep 1; done"

Aplicamos este comando a nuestro ejemplo creando un contenedor:
- docker run -d --name=muchotexto busybox sh -c "while true; do $(echo
date); sleep 1; done"

Con ese contenedor en marcha, ya podemos probar “docker attach”. Podremos enlazar la entrada
y salida del proceso en ejecución a nuestra terminal y observar el texto generado usando:
- docker attach muchotexto

### OBTENIENDO INFORMACIÓN DE LOS LOGS CON “DOCKER LOGS”

Podemos consultar la información generada con el comando “docker logs”
- docker logs [OPCIONES] IDENTIFICADOR/NOMBRE

Un ejemplo de uso para obtener logs podría ser
- docker logs -f --until=2s muchotexto

###  RENOMBRANDO CONTENEDORES CON “DOCKER RENAME”

El comando “docker rename” nos permite cambiar el nombre asociado a un contenedor.
- docker rename contenedor1 contenedor2

### PRINCIPALES PARÁMETROS DEL COMANDO “DOCKER RUN”

Utilizando el comando
- docker run -it --name=nuestroUbuntu1 ubuntu /bin/bash

Estamos creando un nuevo contenedor a partir de la imagen “ubuntu”. Al crear este contenedor
hemos especificado los siguientes parámetros:
- Parámetro “-i”: indica que el proceso lanzado en el contenedor docker estará en modo
interactivo, es decir, enlaza la entrada estándar cuando se asigna un proceso a una
terminal.
- Parámetro “-t”: asigna al proceso lanzado al arrancar el contenedor una pseudo terminal,
facilitando el acceso al mismo desde nuestra terminal
- Parámetro “--name”: nos permite establecer un nombre a nuestro contenedor. Si no indicamos este parámetro, nos creará un nombre aleatorio.

## GESTIÓN DE IMÁGENES EN DOCKER

### LISTANDO IMÁGENES LOCALES Y PARA SU DESCARGA

**Listando imágenes locales**

Podemos obtener información de qué imágenes tenemos almacenadas localmente usando
- docker images

Podemos utilizar filtros sencillos usando la nomenclatura “docker images [REPOSITORIO[:TAG]]”
- docker images ubuntu:14.04

Si queremos utilizar algún filtro avanzado, podemos usar la opción “-f”. Aquí un ejemplo, filtrando
las imágenes que empiecen por “u” y acabe su etiqueta en “04”.
- docker images -f=reference="u*:*04"

**Listando imágenes para su descarga**

Podemos obtener información de imágenes que podemos descargar en el registro (por defecto,
Docker Hub) utilizando el comando “docker search”. Por ejemplo, con el siguiente comando:
- docker search ubuntu

### DESCARGANDO Y ELIMINANDO IMÁGENES (Y CONTENEDORES) LOCALES

**Descargando imágenes con docker pull**

Podemos almacenar imágenes localmente desde el registro sin necesidad de crear un contenedor
mediante el comando “docker pull”. Para conocer sus nombres y versiones, podemos usar el comando “docker search”
- docker pull alpine:3.10

**Observar el historial de una imagen descargada**

Podéis observar el historial de una imagen descargada, es decir, en qué versiones se basa, usando
el comando “docker history”. Por ejemplo con:
- docker history nginx

**Eliminando imágenes con “docker rmi”**

Con el comando “docker rmi” podemos eliminar imágenes almacenadas localmente
- docker rmi ubuntu:14.04

Una forma de eliminar todas las imágenes locales, que no estén siendo usadas por un contenedor, combinando “docker images -q” para obtener la lista y “docker rmi” es la siguiente:
- docker rmi $(docker images -q)

**Eliminando contenedores con “docker rm”**

Con la siguiente orden se puede borrar un contenedor por identificador o nombre
- docker rm IDENTIFICADOR/NOMBRE

Asimismo, una forma de borrar todos los contenedores (que estén parados), de forma similar a
como vimos en el anterior punto, es la siguiente:
- docker stop $(docker ps -a -q)
- docker rm $(docker ps -a -q)

**Eliminando todas las imágenes y contenedores con “docker system prune -a”**

Una forma de realizar las operaciones anteriores de golpe, es usando “docker system prune -a”,
que elimina toda imagen y contenedor parado.
- docker stop $(docker ps -a -q)
- docker system prune -a

#### CREANDO NUESTRAS PROPIAS IMÁGENES A PARTIR DE UN CONTENEDOR EXISTENTE

Podemos entender que un contenedor es
como una “capa temporal” de una imagen, por lo cual, podemos hacer un “commit” y convertir
esa “capa temporal” en una imagen. La sintaxis más habitual es la siguiente
- docker commit -a "autor" -m "comentario" ID/NOMBRE-CONTENEDOR
usuario/imagen:[version]

Si tenemos un contenedor con nombre “ubuntumod” que simplemente es un
contenedor basado en la imagen “ubuntu” en el que se ha instalado un programa y hacemos:
- contenedor basado en la imagen “ubuntu” en el que se ha instalado un programa y hacemos:
docker commit -a "Sergi" -m "Ubuntu modificado" IDCONTENEDOR
sergi/ubuntumod:2021

y tras ello, comprobamos las imágenes con
- docker images

### EXPORTANDO/IMPORTANDO IMÁGENES LOCALES A/DESDE FICHEROS

Una vez tengamos una imagen local en nuestro sistema, podemos hacer una copia de la misma, ya
sea como copia de seguridad o como forma de transportarla a otros sistemas mediante el
comando “docker save”. Por ejemplo, se puede hacer de estas dos formas:
- docker save -o copiaSeguridad.tar sergi/ubuntumod
- docker save sergi/ubuntumod > copiaSeguridad.tar

Si queremos importar el fichero para crear una imagen en nuestra máquina, podemos usar
- docker load -i copiaSeguridad.tar
- docker load < copiaSeguridad.tar

### SUBIENDO NUESTRAS PROPIAS IMÁGENES A UN REPOSITORIO (DOCKER HUB)

**Paso 1: creando repositorio para almacenar la imagen en Docker Hub**

En primer lugar, debéis crearos una cuenta en https://hub.docker.com e iniciar sesión. Una vez
iniciada sesión, debéis acceder a “Repositories” y ahí a “Create repository”.

Tras ello, podréis quedar un repositorio con vuestra cuenta y elegir si dicho repositorio es público
(cualquiera puede acceder) o privado (solo puede acceder dueño o autorizados).

**Paso 2: almacenando imagen local en repositorio Docker Hub**

En primer lugar, deberemos iniciar sesión mediante consola al repositorio mediante el comando
- docker login

Una vez iniciada sesión, debemos hacer un “commit” local de la imagen, siguiendo la estructura
vista en puntos anteriores. Un ejemplo podría ser:
- docker commit -a "Sergi" -m "Ubuntu modificado" IDCONTENEDOR
sergi/prueba

Hecho este “commit” local, debemos subirlo usando “docker push”

- docker push sergi/prueba

### GENERAR AUTOMÁTICAMENTE NUESTRAS PROPIAS IMÁGENES MEDIANTE DOCKERFILE

**Editor Visual Studio Code y plugins asociados a Docker**

Los ficheros “Dockerfile” pueden crearse con cualquier editor de texto, pero desde aquí
recomendamos el editor multiplataforma “Visual Studio Code” https://code.visualstudio.com/

Al instalarlo, si detecta Docker instalado en el sistema, el propio editor nos sugerirá una serie de
plugins. Merece la pena instalarlos. Si no, siempre podéis buscar en plugins manualmente. 

**Creando nuestro primer Dockerfile**

Empezaremos creando un sencillo “Dockerfile” donde crearemos una imagen de Ubuntu con el
editor de texto “nano” instalado. Para ello indicaremos:
-  De qué imagen base partiremos.
-  Qué comandos lanzaremos sobre la imagen base, para crear la nueva imagen
-   Qué comando se asociará por defecto al lanzar un contenedor con la nueva imagen

Creamos el fichero “Dockerfile” (Visual Studio Code le pondrá un icono de la ballena) y añadimos:
- FROM ubuntu:latest
RUN apt update && apt install -y nano
#Aquí un comentario
CMD /bin/bash

Si ahora usamos el comando “docker build” de la siguiente forma:
- docker build -t ubuntunano ./

Si queréis especificar un nombre de fichero distinto a buscar en el directorio, puede usarse la
opción “-f”, como en este ejemplo:
- docker build -t ubuntunano -f Dockerfile2 ./

**Otros comandos importantes de Dockerfile**

La opción EXPOSE nos permite indicar los puertos por defecto expuestos que tendrá un
contenedor basado en esta imagen
- EXPOSE 80 443 8080

ADD es un comando para copiar un fichero de la máquina anfitriona al nuevo contenedor, por ejemplo
- ADD ./mifichero.zip /var/www/html

Descomprimirá el contenido de “mifichero.zip” en el directorio destino de la nueva imagen.

COPY sirve para lo mismo pero excepto si queremos descomprimir un "zip"
- COPY ./mifichero.zip /var/www/html

**Comando ENTRYPOINT**

Por defecto, los contenedores Docker están configurados para que ejecuten los comandos que se
lancen mediante “/bin/sh -c”. Dicho de otra forma, los comandos que lanzábamos, eran
parámetros para “/bin/sh -c”. Podemos cambiar qué comando se usa para esto con ENTRYPOINT.
Por ejemplo:
- ENTRYPOINT ["cat"] <br>
CMD ["/etc/passwd"]

**Comando USER**

Por defecto, todos los comandos lanzados en la creación de la imagen se ejecutan con el usuario
root (usuario con UID=0). Para poder cambiar esto, podemos usar el comando USER, indicando el
nombre de usuario o UID con el que queremos que se ejecute el comando. Por ejemplo:
- USER sergi <br>
CMD id

**Comando WORKDIR**

Cada vez que expresamos el comando WORKDIR, estamos cambiando el directorio de la imagen
donde ejecutamos los comandos. Si este directorio no existe, se crea. Por ejemplo:
- WORKDIR /root <br>
CMD mkdir tmp <br>
WORKDIR /var/www/html <br>
CMD mkdir tmp

**Comando ENV**

El comando ENV nos permite definir variables de entorno por defecto en la imagen.
- ENV v1=”valor1” v2=”valor2”

**Otros comandos útiles: ARG, VOLUME, LABEL, HEALTHCHECK**

Aquí comentamos comandos útiles:
- ARG: permite enviar parámetros al propio “Dockerfile” con la opción “--build-arg” del
comando “docker build”.
- VOLUME: permite establecer volúmenes por defecto en la imágen. Hablaremos de los
volúmenes más adelante en el curso.
- LABEL: permite establecer metadatos dentro de la imagen mediante etiquetas. Uno de los
casos más típicos, sustituyendo al comando MAINTAINER, que esta “deprecated” es LABEL maintainer="sergi.profesor@gmail.com"
- HEALTHCHECK: permite definir cómo se comprobará si ese contenedor está funcionando
correctamente o no. Útil para sistemas orquestadores como “Docker swarn”, aunque otros
como “Kubernetes” incorporan su propio sistema

### TRUCOS PARA HACER NUESTRAS IMÁGENES MÁS LIGERAS

Al crear imágenes, es habitual aumentar el tamaño de las imágenes base. Algunos consejos para
dentro de lo posible, aumentar el tamaño lo menos posible:
- Usar imágenes base ligeras, tipo “Alpine”
- Utiliza comandos de limpieza tras instalaciones con “apt”, tales como “rm -rf /var/lib/apt/lists/*” tras crear una imagen para borrar las listas generadas al realizar “apt update”.

