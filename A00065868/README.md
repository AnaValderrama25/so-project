## Miniproyecto Sistemas Operativos

**Universidad ICESI**  
**Curso:** Sistemas Operativos  
**Docente:** Daniel Barragán C.  
**Tema:**  Servicios web  
**Correo:** daniel.barragan at correo.icesi.edu.co  
  
**Estudiantes:** 
* Carlos Andrés Afanador - A00054652  
* Ana Fernanda Valderrama - A00065868   
* Julian David Gonzalez - A00315288    
  
  
**URLGit:** https://github.com/AnaValderrama25/so-project/tree/A00065868/A00065868

## Objetivos
* Desplegar una aplicación en un servidor que ejecuta el sistema operativo Linux
* Realizar los ajustes y depuración necesarios para desplegar una
aplicación en Linux
* Realizar aplicaciones para obtener información del sistema operativo

## Descripción
Para el despliegue de una aplicación en un servidor se requiere conocer los procedimientos necesarios relacionados con la configuracion de las interfaces de red, ajustes de seguridad, instalación de dependencias, usuarios y herramientas de depuracíon del sistema operativo.

El siguiente proyecto consiste en el despliegue de una aplicación web para obtener información del sistema operativo (La aplicación debe permitir consulta uso de CPU, memoria y espacio en disco). Para este propósito se debe emplear el sistema operativo Ubuntu Server 16.04, el microframework flask y ambientes virtuales.

<p align="center">
  <img src="images/vista-despliegue.png" alt="webservice architecture"/>
</p>

## Actividades
* Nombre y código de todos los integrantes del grupo (máximo 3) (5%)
* Ortografía y redacción (5%)
* Descripción breve de los pasos para cumplir con lo solicitado
  * Sistema operativo Ubuntu Server 16.04 (10%)
  * Configuración de interfaces de red (10%)
  * Configuración de puertos (10%)
  * Instalación de dependencias (10%)
  * Creación de ambientes virtuales (10%)
  * Aplicación en Python (10%)
  * Validación de la ejecución del servicio (netstat) (10%)
* Pruebas de la solución a través de capturas de pantalla. Puede emplear si lo desea una herramienta de captura de pantalla a formato .gif (10%)
* El informe debe ser entregado en formato pdf a través del moodle y el informe en formato README.md debe ser subido a un repositorio de github. El repositorio de github debe ser un fork de https://github.com/ICESI-Training/so-project y para la entrega deberá hacer un Pull Request (PR) respetando la estructura definida. El código fuente y la url de github deben incluirse en el informe (10%).  
  
     
## Desarrollo  
  * Para llevar a acabo el proyecto es necesario descargar la iso de Ubuntu Server 16.04. Luego de descargada se crea una máquina virtual en VirtualBox. Una versión de tipo Linux de 64-bits. Con un procesador y dos adaptadores de red uno NAT y otro puente.  
  ![][1]  
  Desde la máquina virtual fue necesario instalar ssh, con los comandos:  
  ``` 
  $ sudo apt install openssh-client  
  $ sudo apt install openssh-server  
  ```   
  ![][2]  
  Luego, se verifica el estado de ssh con el comando
  ``` 
  $ sudo service ssh status  
  ```   
  ![][3]  
  * Se configura manualmente la interfaz enp0s8, con una dirección IP y un gateway predeterminado, y se reinicia el servicio de red  
  ![][4]  
  Para acceder desde Multiputty y que sea posible usar screen, es necesario desactivar el firewall si estaba activado:  
  ```  
  $ sudo ufw disable
  ```  
  * Luego de haber iniciado sesión en Multiputty se activa el firewall y se habilita el puerto necesario 8080:  
  ```  
  $ sudo ufw enable  
  $ sudo ufw allow 8080  
  ``` 
  * Se instalan las dependencias necesarias para la creación de ambientes virtuales de python, y posteriormente se crea un ambiente desde el usuario proyecto y se instala la librería de flask en el ambiente. Luego, se crea el servicio hello.py en el cual se realiza la consulta de uso de CPU, memoria, espacio en disco y conexiones activas.   
  Instalación de las dependencias necesarias para ambientes virtuales  
  ```  
  $ sudo apt-get install python3-pip  
  $ sudo pip3 install virtualenv    
  ```    
  ![][5]  
  * Creación del ambiente, activación, instalación de la librería flask y creación del servicion ejecutando el script hello.py  
  ```  
  $ virtualenv proyectoOperativosFinal  
  $ source proyectoOperativosFinal/bin/activate  
  $ pip install flask  
  $ vim hello.py
  ```  
  ![][6]  
  * El script en python esta compuesto por las secciones con los comandos adecuados para realizar la consulta de los recursos del sistema como CPU, espacio en disco, memoria y conexiones activas. El código contenido en el script semuestra a continuación:   
  ![][7]  
  * Se ejecuta el servicio desde el ambiente de python que creamos anteriormente, ahora ya serán posibles las consultas de la información del sistema operativo desde un navegador como chrome:   
  ```  
  $ python hello.py     
  ```  
  ![][8]  
  La anterior es el resultado de acceder desde el navegador al servicio solicitando la información de un recurso:  
  | **Recurso solicitado** | **Browser**  |
  | --- | --- |
  | Memoria | ![][9] |
  | CPU | ![][10] |
  | Espacio en disco | ![][11] |
  | Conexiones | ![][12] |  
  
  * El servicio se valida además de accediendo por el navegador, se emplea en la consola de windows y en el UbuntuServer el comando netsat, donde se puede observar que en windows la dirección remota pertenece a la que se asignó en los primeros pasos y esta conectada por ssh y desde  UbuntuServer la dirección que asignamos es la local y la remota es la que windows tiene como local, se muestra que están activos los servicios ssh y http.  
  ![][13]  
  ![][14]  
  
  
  
  
  

## Referencias
* https://www.ubuntu.com/download/server  
* https://help.ubuntu.com/community/SSH/OpenSSH/Configuring  
* https://github.com/ICESI/so-microservices-python/tree/master/01_virtualenvs  
* https://github.com/ICESI/so-discovery-service  
* http://ubuntuhandbook.org/index.php/2016/04/enable-ssh-ubuntu-16-04-lts/  
* https://help.ubuntu.com/lts/serverguide/openssh-server.html  
* http://www.ubuntu-es.org/node/191549#.WiHU_lXibIU  
* https://askubuntu.com/questions/397502/reboot-a-server-from-command-line  

[1]: images/ConfiguracionUbuntuServer.PNG  
[2]: images/InstalacionSSH.PNG  
[3]: images/EstadoSSH.PNG  
[4]: images/AsignacionIp.PNG    
[5]: images/VirtualEnv.PNG  
[6]: images/AmbienteProyetco.PNG    
[7]: images/hellopy.PNG   
[8]: images/ServiceWorking.PNG    
[9]: images/FreeMemory.PNG    
[10]: images/CPUState.PNG    
[11]: images/DiskInfo.PNG    
[12]: images/ActiveInternetConnections.PNG   
[13]: images/ConexionesUbuntu.PNG    
[14]: images/Windows.PNG  



