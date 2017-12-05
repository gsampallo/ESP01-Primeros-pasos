# ESP01-Primeros-pasos

Luego de comprar el módulo, me surgieron dos preguntas:
1.	¿Cómo lo conecto a Arduino? 
2.	¿Y cómo hago para que entre en la protoboard?
La 2da la dejo para más adelante porque podemos resolver fácilmente usando cables, es engorroso, poco prolijo, pero funciona. NO es una solución permanente.
Lo primero que hay que entender es que este módulo viene cargado de fabrica con un firmware que utiliza los comandos AT. Los comandos AT es un lenguaje que se convirtió en estándar abierto para configurar y parametrizar modems.
Entonces en baso a lo anterior, si queremos conectar Arduino (UNO o el nano no importa) tenemos que utilizar los puertos de comunicación serial; a primera instancia representa un problema porque el UNO solo tiene un puerto Serial que también se utiliza para programar el equipo. Con lo cual si los utilizamos para conectar al ESP no tendríamos forma de interactuar con el Arduno.
Como solución podemos utilizar una librería que se llama SoftwareSerial, que permite utilizar crear un segundo puerto serie utilizando alguno de los otros puertos digitales.
No hace falta buscar mucho en google para encontrar muchos (muchisimos) ejemplos de como hacerlo; abajo esta el modo de como yo logre hacerlo funcionar:

![Diagrama](https://raw.githubusercontent.com/gsampallo/ESP01-Primeros-pasos/master/esp01_primeros_pasos_bb.png) 

Una vez que lo tenemos conectado, debemos cargar el sketch esp01_primer_paso.ino, basicamente lo que hace es utilizar el Arduino como intermediario para conectarse al ESP; luego de subirlo al Arduino, tenemos que abrir el Monitor Serie y vamos a ver la pantalla desde donde podemos enviar comandos AT al ESP.

El primero comando que vamos a querer enviar es AT, a lo que el modulo debe responder OK.

Lo segundo que tendriamos que hacer es configurar el modo en el que queremos que opere el ESP, existen tres modos:
 1 :  station mode  
 2 :  softAP mode  
 3 :  softAP + station mode
 
Para consultar el modo actual debemos ejecutar: AT+CWMODE?
Lo comun es cambiar al modo tres, donde luego se configura el ESP para que se conecte al wifi y tenga acceso a internet.
Para cambiar el modo AT+CWMODE=3, luego cuando el modulo nos confirme, podriamos pedirle la lista de las redes wifi disponibles con AT+CWLAP.
Finalmente para asignarle la red utilizamos AT+CWJAP=”nombreRed”,”clave”
Una vez que el modulo nos confirma que esta conectado, podemos ver la IP asignada con AT+CIFSR

Para enviar datos al modulo, por ejemplo mediante el puerto 80, debemos habilitar la posibilidad de multiples conexiones e indicar sobre que puerto va a estar escuchando las peticiones,para ello utilizamos:

habilitar multiples conexiones
AT+CIPMUX=1
Atiende en el puerto 80.El primer parametro indica que crea el servidor, si en lugar de 1 utilizamos 0 lo elimina.
AT+CIPSERVER=1,80

En el archivo pdf encontraran un resumen de los comandos AT, tambien pueden buscarlos en google donde facilmente encontran muchoas indicaciones de como usarlos.

[![Video](https://img.youtube.com/vi/u7bUrcXkQRo/0.jpg)](https://www.youtube.com/watch?v=u7bUrcXkQRo)








