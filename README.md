# Xerosploit

Xerosploit es un framework avanzado escrito en Python desarrollado por LionSec. Dicha herramienta es de tipo MIM (Man in the Middle), nos permite ejecutar diferentes tipos de ataques, como por ejemplo cambiar todas las imagenes que se sirven las paginas web del equipo victima, o inclusive insertar codigo HTML o .JS.

Hago esta explicación para mostrar como se instala el programa. 

Todo el credito es para LionSec.

# Instalando Xerosploit 

#### Dependecias necesarias

Para la instalación usaré una maquina con Kali Linux ( podéis ver como crear una en el respositorio https://github.com/Zoser777/Metasplotable_2). Lo primero que haré es instalar las dependencias necesarias:

    sudo apt-get install nmap hping3 build-essential ruby-dev libpcap-dev libgmp3-dev python3-pip python2 2to3
    
![imagen](https://user-images.githubusercontent.com/80277545/147164356-6b6b59a6-79f0-4872-88dc-665bdd2a3550.png)

##### Tabulate y Terminaltables

A continuación instalaremos el Tabulate y el Terminaltables, que por lo que he podido leer en varias guías son paquetes de Python que nos permiten utilizar funciones para mostrar tablas graficas con Python, esto lo podremos ver reflejado más adelante.

Por ahora instalamos lo siguiente mediante Python:

     sudo pip install tabulate
     sudo pip install terminaltables
     

![imagen](https://user-images.githubusercontent.com/80277545/147164988-38c410e7-e896-40ae-9acb-1313f5648a6d.png)

     
##### Repositorio principal

Ahora instalaremos el repositorio principal de la herramienta desde el siguiente enlace, al cuál podéis acceder para aprender más sobre esta. 

Nos dirigiremos (por ejemplo, podría ser otro directorio) a Documentos. Aquí ejecutaremos el siguiente comando para clonar el repositorio:

        cd /home/kali/Documentos
        git clone https://github.com/LionSec/xerosploit
        
Esto nos dejará lo siguiente:

![imagen](https://user-images.githubusercontent.com/80277545/147165101-9585c1e3-9e57-4c66-8ab6-425f4f8a1ba0.png)


#### Instalando xerosploit 

Ahora instalaremos el framework con el siguiente comando, para esto nos situaremos dentro de la carpeta xerosploit que se habrá creado al clonar el repositorio:

        sudo python2 install.py
        
ACLARACIÓN: DEBE SER "PYTHON2" NO PYTHON3.

A continuación seleccionaremos el sistema operativo que estemos usando. Si estamos usando una distribución de Debian (Ubuntu, Kali, Kubuntu, etc) seleccionaremos la primera opción. 

![imagen](https://user-images.githubusercontent.com/80277545/147165325-972a65b7-88b8-4372-8251-eea238544725.png)

Output de la instalación: 

![imagen](https://user-images.githubusercontent.com/80277545/147165424-f1b32b1b-6e9e-4eab-873d-2131794f007e.png)


#### "Transformando el codigo"

El programa en si mismo está escrito en Python2, para poder usarlo con un mejor desempeño lo suyo es usar Python3, para esto vamos a "transformar" el codigo, de Python2 a Python3. Esto lo haremos con la herramienta  _"2to3":

        sudo 2to3 -w xerosploit.py


![imagen](https://user-images.githubusercontent.com/80277545/147165633-0ab965a5-9165-4586-9c81-6b8d4011ddf8.png)


#### Iniciando Xerosploit.py

A continuaciónn iniciaremos el programa y veremos en "acción" los paquetes de Python de "tabulates" y "terminaltables". Para iniciar el programa ejecutaremos:

        sudo python3 xerosploit.py 

![imagen](https://user-images.githubusercontent.com/80277545/147165997-54dc668e-8796-4dbd-afa8-eea25d894718.png)


##### COnfigurando Xerosploit.py

Como se puede apreciar en la imagen, no tengo dirección Gateway. Se puede dar el caso de que al instalarlo si salga configurado, si es ese el caso, se debe ir al siguiente punto.

Para configurar el Getway, escribiremos "Help" para que nos muestre los parametros disponibles. A continuación escribiremos:

        gateway 
        
En mi caso al ser el adaptador "Adaptador solo-anfrition" , el gateway es "192.168.56.1":

![imagen](https://user-images.githubusercontent.com/80277545/147166886-01408de9-a96d-4225-8e72-c3004cdfeb4a.png)

Esto hará que se actualice el programa:

![imagen](https://user-images.githubusercontent.com/80277545/147166922-da559200-a724-4614-9886-bc4ed4843593.png)

#### Iniciando Xerosploit.py

A continuación realizaré un escaneo de la red, para ver los dispositivos que hay conectados en esta. Al ser el adaptador solo-anfrition, solo saldrá mi otra maquina de ubuntu que tengo iniciada:

Ip de mi maquina virtual ubuntu: 

![imagen](https://user-images.githubusercontent.com/80277545/147167088-7e06c114-6e88-4f06-a740-dd7b04b76fa7.png)

    192.168.56.107

Realizamos el escaneo de la red desde xerosploit:

    help

![imagen](https://user-images.githubusercontent.com/80277545/147167164-66468e0c-a184-4614-bfd9-fb79bdc50f86.png)

Elegimos la opción de "scan":

![imagen](https://user-images.githubusercontent.com/80277545/147167225-81a9f91e-2cbe-4e68-9727-dcb2aade4812.png)

Como se puede apreciar, aparece la maquina VirtualBox de Ubuntu con la IP 192.168.56.107.

A continuación realizaremos un escaneo de puertos sobre esta IP, lo que haremos es seleccionarla simplemente introduciendo dicha IP:

![imagen](https://user-images.githubusercontent.com/80277545/147167372-dd118101-f90b-4176-a861-3208b52c83e0.png)

En la maquina de Ubuntu hay un servicio de Apache en el puerto 80, vamos a ver si con un escaneo desde Kali podemos verlo. 
Introduciremos de nuevo "help" para ver todas las posibilidades que tenemos sobre la maquina atacada:

![imagen](https://user-images.githubusercontent.com/80277545/147167486-62c63a7e-b03c-4b23-8635-fb55c1f95bf1.png)

Seleccionaremos el "pscan" y ejecutaremos un "run":

        pscan
        run

![imagen](https://user-images.githubusercontent.com/80277545/147167553-5e089459-0116-402b-ad4b-d50fa03c80ce.png)

Efectivamente nos sale el servicio de Apache/HTTP activado en el puerto 80.

Para elegir otro modulo, debemos escribir "back" y "help" para volver a mostrar todas las posibilidades:

![imagen](https://user-images.githubusercontent.com/80277545/147167637-6622d156-e8e6-4f6d-9b67-2966c43b383e.png)

# Conlusión

Como se puede apreciar, la herramienta "pscan" sirve para escanear los puertos, pero también se puede realizar un ataque Dos o injectarHTML o .JS entre otras cosas. También podemos usar la opción de sniff , para capturar todo tipo de datos sensibles en la maquina atacada. 

Espero que haya sido de utilidad la guía, en caso de surgir dudas me podéis contactar en z0s3r77@gmail.com.


