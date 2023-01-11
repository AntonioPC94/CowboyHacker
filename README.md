author: Antonio Peñalver Caro
id: Máquina Cowboy Hacker
categories: Hacking Ético
environments: Web
status: Published

# Máquina: Cowboy Hacker

En esta máquina, lo primero que haremos será realizar un “NMap” a la dirección IP objetivo para ver qué puertos tiene abiertos.

![Untitled000](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled000.png)

Al finalizar el escaneo, podremos comprobar que la máquina tiene los siguientes puertos abiertos:

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%201.png)

Como tiene el puerto 21 abierto, el cual pertenece al servicio FTP, vamos a intentar acceder a él como usuario anónimo (anonymous) a través del siguiente comando:

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%202.png)

Una vez dentro, intentaremos listar el contenido del servidor FTP a con el comando “ls”.

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%203.png)

Tal y como se observa en la imagen anterior, el servidor nos ha mostrado un par de ficheros de texto, de los cuales desconocemos (Por el momento) su contenido.

Para poder visualizar el contenido de los ficheros, nos los tendremos que descargar primero con el comando “get (NombreFichero)”.

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%204.png)

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%205.png)

Ahora que los tenemos descargados, nos saldremos del FTP y le lanzaremos un “cat” a ambos ficheros para ver qué contienen:

Contenido de locks.txt:

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%206.png)

Contenido de task.txt:

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%207.png)

Aparentemente, el fichero locks.txt contiene posibles contraseñas de usuario. Y el fichero task.txt contiene un posible nombre de usuario, el cual se llama lin.

A continuación, lo que vamos a hacer, es realizar un ataque de fuerza brutal al fichero locks.txt, para ver qué contraseña es la que nos va a permitir acceder por SSH a la máquina anfitriona.

Para ello, utilizaremos el comando “hydra” con los siguientes parámetros:

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%208.png)

Como podemos observar en la imagen anterior, el comando “hydra” nos ha devuelto la contraseña que tenemos que utilizar para poder acceder a la máquina anfitriona por SSH.

Ahora lo que vamos a hacer, es acceder con las credenciales que hemos obtenido al servicio SSH de la máquina objetivo:

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%209.png)

Como se observa en la imagen anterior, ya estamos dentro de la máquina anfitriona. Ahora vamos a realizar un “ls” para ver si hay algo dentro del directorio en que nos encontramos:

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%2010.png)

En la imagen anterior, se ve que hay un fichero llamado user.txt, entonces lo que vamos a hacer ahora, es ver qué hay dentro de dicho fichero:

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%2011.png)

Lo que nos muestra es el fichero, es una de las flags del ejercicio.

Por último, vamos a realizar una pequeña escalada de privilegios para poder descubrir cuál es la última flag del ejercicio. Para ello, tendremos que usar el comando “sudo -l” para ver qué puede ejecutar el usuario lin como administrador.

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%2012.png)

lin puede usar el comando “tar” como administrador, por lo tanto, nos vamos a ir a la página GTFOBins y buscaremos si se puede explotar dicho comando:

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%2013.png)

En la página hay varias maneras de explotar dicho comando, pero nosotros vamos a utilizar la primera opción que nos ofrece:

![Untitled](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/Untitled%2014.png)

Como se observa en la imagen anterior, ya hemos conseguido acceder como administrador a la máquina anfitriona y accediendo a la carpeta de “root”, conseguimos sacar el fichero “root.txt”, el cual necesitábamos para poder obtener la última flag.

Le realizamos un “cat” al fichero y este nos devolverá como resultado la última flag.

![WhatsApp Image 2023-01-10 at 16.53.01.jpeg](Ma%CC%81quina%20Cowboy%20Hacker%2054f0539d9c6e4da58cc78d13d3719c13/WhatsApp_Image_2023-01-10_at_16.53.01.jpeg)
