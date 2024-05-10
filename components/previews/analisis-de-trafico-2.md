---
title: Analisis de trafico - Parte 2
description: Introduccion al analisis de trafico
excerpt:
  En esta ocasion comenzaremos a utilizar Tcpdump, una herramienta de linea de comandos que puede capturar e interpretar el trafico de un archivo o desde una interfaz de red.
datetime: 2024-04-09T20:35:07.000+00:00
tags:
  - Wireshark
  - Traffic Analysis
  - Tcpdump
featured: true
category: What is ?
author: Nicolas Gula
type: article
coverImage:  https://learn.g2.com/hubfs/G2CM_FI634_Learn_Article_Images_%5BNetwork_traffic_analysis%5D_V1a.png
coverImageAlt: Microsoft AD
coverImageWidth: "2725"
coverImageHeight: "1400"
ogImage: "/assets/blog/hello-world/cover.jpg"
ogImageAlt: something
language: "Spanish"
---

## Tcpdump

Tcpdump es una herramienta de línea de comandos que captura y analiza paquetes de datos desde una interfaz de red o archivo. Es compatible con sistemas Unix y Windows (a través de WinDump) y puede ser utilizado remotamente mediante SSH. Aunque inicialmente puede parecer abrumador debido a su variedad de funciones y filtros, una vez dominadas las funciones esenciales, se vuelve fácil de usar. Utiliza bibliotecas como pcapy y libpcap para capturar paquetes de cualquier dispositivo en la red local, permitiendo una visualización completa del tráfico de red.

Para comenzar a utilizar Tcpdump, es crucial familiarizarse con sus características esenciales. Esto incluye comprender algunas opciones básicas, aprender comandos y cómo capturar tráfico en archivos PCAP y leerlos después.

### Localizar Tcpdump

![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/tcpdump/1.png)

### Instalar Tcpdump
![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/tcpdump/2.png)

### Version

![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/tcpdump/3.png)

## Captura de trafico

Estos comandos se pueden combinar para controlar cómo se muestra la salida en STDOUT y qué se guarda en el archivo de captura. Aunque no son todos los disponibles, estos son los más comunes y útiles.

- **-D**: Muestra las interfaces disponibles para capturar.
- **-i**: Selecciona una interfaz para capturar (por ejemplo, -i eth0).
- **-n**: No resuelve nombres de host.
- **-nn**: No resuelve nombres de host ni puertos conocidos.
- **-e**: Captura la cabecera Ethernet junto con los datos de la capa superior.
- **-X**: Muestra el contenido de los paquetes en formato hexadecimal y ASCII.
- **-XX**: Lo mismo que -X, pero especifica también las cabeceras Ethernet.
- **-v, -vv, -vvv**: Aumenta la verbosidad de la salida mostrada y guardada.
- **-c**: Captura un número específico de paquetes y luego finaliza el programa.
- **-s**: Define cuánto del paquete capturar.
- **-S**: Cambia los números de secuencia relativos en la visualización de la captura a números de secuencia absolutos (13248765839 en lugar de 101).
- **-q**: Imprime menos información de protocolo.
- **-r file.pcap**: Lee desde un archivo.
- **-w file.pcap**: Escribe en un archivo.

### Interfaces disponibles

![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/tcpdump/4.png)



### Elegir Interfaz

En esta terminal, usamos tcpdump y seleccionamos la interfaz eth0 para capturar el tráfico. Al emitir el comando, tcpdump comenzará a rastrear el tráfico y mostrará los primeros paquetes en la interfaz. 

![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/tcpdump/5.png)


### Deshabilitar la resolucion de nombres

Al utilizar el interruptor -nn, indicamos a tcpdump que no resuelva direcciones IP ni números de puerto en nombres de host y puertos comunes. En esta representación, el último octeto indica el puerto de origen/destino de la conexión.

![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/tcpdump/6.png)


### Mostrar el encabezado Ethernet

Al usar el interruptor -e, indicamos a tcpdump que incluya los encabezados de Ethernet en la salida de la captura junto con su contenido habitual. Esto se evidencia en el resultado, donde el primer y segundo campo, que generalmente constan de la marca de tiempo y el inicio del encabezado IP, ahora muestran la marca de tiempo y la dirección MAC de origen del host.

![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/tcpdump/7.png)

### Incluye salida ASCII y hexadecimal 

Al usar el interruptor -X, podemos visualizar el paquete de manera más clara. Esto nos proporciona una salida ASCII a la derecha para interpretar el texto claro correspondiente a la salida hexadecimal a la izquierda.

![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/tcpdump/8.png)


## Tcpdump Output

Revisar los resultados de TCPDump puede ser abrumador al principio. Sin embargo, al analizar los interruptores básicos que hemos utilizado, hemos obtenido diferentes vistas del tráfico capturado. Es importante tomarnos un momento para comprender este resultado y explicar lo que estamos viendo. Cada campo en la salida tiene su significado, y cuanto más detallados sean nuestros filtros, más información se mostrará en cada encabezado.

![](https://raw.githubusercontent.com/NicolasGula/NicolasGula/master/public/images/photos/tcpdump/9.png)

- Amarillo: Marca de tiempo.
- Verde: Protocolo. En este caso TCP. Origen y destino. IP.port == 172.64.147.188.443
- Celeste: Flags utilizadas.
- Azul: Numeros de secuencia y de confirmacion utilizados para rastrear el segmento TCP.
- Violeta: Opciones de protocolo. Valores TCP negociados entre el cliente y el servidor.

Con TCPDump, podemos ver el tráfico de red y analizarlo en busca de problemas o interacciones sospechosas. Esto requiere comprender cómo funciona una red y cómo usar los filtros proporcionados por TCPDump. Con esta comprensión, podemos identificar rápidamente anomalías en la red. Por ejemplo, podemos crear un sistema IDS/IPS utilizando TCPDump y un script Bash para analizar paquetes interceptados y tomar medidas según un patrón específico, como prohibir una dirección IP que envíe demasiadas solicitudes de eco ICMP en un período determinado.


## Entrada/salida de archivos con Tcpdump 

Al usar `-w`, guardaremos nuestra captura en un archivo. Es importante considerar que al capturar tráfico de red, podemos ocupar rápidamente el espacio de almacenamiento en el disco. Cuanto más grande sea nuestro segmento de red, más rápido se llenará el almacenamiento. El uso de los conmutadores demostrados anteriormente puede ayudar a ajustar la cantidad de datos almacenados en nuestros archivos PCAP.

En progreso ...