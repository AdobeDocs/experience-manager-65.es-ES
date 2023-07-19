---
title: Herramienta Servidor Proxy (proxy.jar)
seo-title: Proxy Server Tool (proxy.jar)
description: AEM Obtenga información acerca de la herramienta de servidor proxy en la.
seo-description: Learn about the Proxy Server Tool in AEM.
uuid: 2fc1df24-8d5a-4be7-83fa-238ae65591b0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: ca98dc3c-7056-4cdc-b4d3-23e471da5730
docset: aem65
exl-id: 3df50303-5cdd-4df0-abec-80831d2ccef7
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 0%

---

# Herramienta Servidor Proxy (proxy.jar){#proxy-server-tool-proxy-jar}

El servidor proxy actúa como un servidor intermedio que transmite solicitudes entre un cliente y un servidor. El servidor proxy realiza un seguimiento de todas las interacciones cliente-servidor y genera un registro de toda la comunicación TCP. Esto le permite monitorizar exactamente lo que está pasando, sin tener que acceder al servidor principal.

Puede encontrar el servidor proxy en la carpeta de instalación adecuada:

* &lt;cq_install_path>/opt/helpers/proxy.jar
* &lt;crx_install_path>/opt/helpers/proxy.jar

Puede utilizar el servidor proxy para supervisar toda la interacción cliente-servidor, independientemente del protocolo de comunicación subyacente. Por ejemplo, puede supervisar los siguientes protocolos:

* HTTP para páginas web
* HTTPS para páginas web seguras
* SMTP para mensajes de correo electrónico
* LDAP para la administración de usuarios

AEM Por ejemplo, puede colocar el servidor proxy entre dos aplicaciones cualquiera que se comuniquen a través de una red TCP/IP; por ejemplo, un explorador web y un servidor de correo electrónico de la red de red (). AEM Esto le permite monitorizar exactamente lo que sucede cuando solicita una página de.

## Inicio de la herramienta de servidor proxy {#starting-the-proxy-server-tool}

AEM La herramienta se encuentra en la carpeta /opt/helpers de la instalación de la instalación de la. Para iniciarlo, escriba:

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### Opciones {#options}

* **q (modo silencioso)** No escribe las solicitudes en la ventana de la consola. Utilice esta opción si no desea ralentizar la conexión o si registra la salida en un archivo (consulte la opción -logfile ).
* **b (modo binario)** Si está buscando combinaciones de bytes específicas en el tráfico, habilite el modo binario. El resultado contendrá la salida hexadecimal y de caracteres.
* **t (entradas de registro de marca de tiempo)** Agrega una marca de tiempo a cada salida de registro. La marca de tiempo está en segundos, por lo que es posible que no sea adecuada para comprobar solicitudes únicas. Utilícelo para localizar eventos que se produjeron en un momento específico si utiliza el servidor proxy durante un período de tiempo más largo.
* **logfile &lt;filename> (escribir en el archivo de registro)** Escribe la conversación cliente-servidor en un archivo de registro. Este parámetro funciona también en modo silencioso.
* **i &lt;numindentions> (agregar sangría)** Cada conexión activa tiene una sangría para mejorar la legibilidad. El valor predeterminado es 16 niveles. (Nuevo en proxy.jar versión 1.16).

## Usos de la herramienta de servidor proxy {#uses-of-the-proxy-server-tool}

Los siguientes escenarios ilustran algunos de los propósitos para los que se puede utilizar la herramienta de servidor proxy:

**Buscar cookies y sus valores**

El siguiente ejemplo de entrada de registro muestra todas las cookies y sus valores enviados por el cliente en la sexta conexión abierta desde el inicio del proxy:

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**Comprobación de encabezados y sus valores** El siguiente ejemplo de entrada de registro muestra que el servidor puede realizar una conexión persistente y que el encabezado de longitud de contenido se ha establecido correctamente:

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**Comprobar si Keep-Alive funciona**

**Keep-Alive** significa que un cliente vuelve a utilizar la conexión con el servidor para transportar varios archivos (código de página, imágenes, hojas de estilo, etc.). Sin la conexión persistente, el cliente debe establecer una nueva conexión para cada solicitud.

Para comprobar si la conexión persistente funciona:

1. Inicie el servidor proxy.
1. Solicite una página.

* Si la conexión persistente funciona, el contador de conexiones nunca debe superar las 5 a 10 conexiones.
* Si la conexión persistente no funciona, el contador de conexiones aumenta rápidamente.

**Búsqueda de solicitudes perdidas**

Si pierde solicitudes en una configuración de servidor compleja, por ejemplo, con un cortafuegos y un distribuidor, puede utilizar el servidor proxy para averiguar dónde se perdió la solicitud. En el caso de un cortafuegos:

1. Iniciar un proxy antes de un cortafuegos
1. Iniciar otro proxy después de un cortafuegos
1. Utilícelos para ver hasta dónde llegan las solicitudes.

**Solicitudes suspendidas**

Si sufre solicitudes que se bloquean de vez en cuando:

1. Inicie un proxy.jar.
1. Espere o escriba el registro de acceso en un archivo, y cada entrada tendrá una marca de tiempo.
1. Cuando la solicitud comienza a bloquearse, puede ver cuántas conexiones estaban abiertas y qué solicitud está causando problemas.

## El formato de los mensajes de registro {#the-format-of-log-messages}

Las entradas de registro producidas por proxy.jar tienen el siguiente formato:

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

Por ejemplo, una solicitud de página Web puede tener el siguiente aspecto:

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C significa que esta entrada proviene del cliente (es una solicitud de una página web)
* 0 es el número de conexión (el contador de conexión comienza en 0)
* #00000 el desplazamiento en la secuencia de bytes. Esta es la primera entrada, por lo que el desplazamiento es 0.
* [GET &lt;?>] es el contenido de la solicitud; en el ejemplo, uno de los encabezados HTTP (url).

Cuando se cierra una conexión, se registra la siguiente información:

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

Muestra el número de bytes que pasaron entre el cliente y el servidor en la sexta conexión y a la velocidad media.

## Ejemplo de salida de registro {#an-example-of-log-output}

Revisaremos una plantilla simple que produce el siguiente código cuando se solicita:

```xml
<html>
  <head>
    <title>Welcome</title>
  </head>
  <body>
    Welcome to Playground<br>
    <img src="/logo.gif">
  </body>
</html>
```

AEM Si se está ejecutando en localhost:4303, inicie el servidor proxy de la siguiente manera:

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

Puede acceder al servidor de (`localhost:4303`) sin el servidor proxy, pero si accede a él a través de `localhost:4444`, el servidor proxy registrará la comunicación. Abra un explorador y acceda a una página creada con la plantilla anterior. Después, observe el archivo de registro.

>[!NOTE]
>
>Hasta la versión 1.14 de proxy.jar, las entradas de registro de una conexión no se sincronizaban, lo que significa que las entradas de registro de una conexión cliente/servidor no son necesarias en el orden secuencial correcto. Las versiones más recientes (>=1.14) del servidor proxy no tienen este problema.

Al iniciar, se escribe la siguiente información en el registro:

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

Los siguientes campos de encabezado se enumeran al principio de la primera conexión (0), que solicita la página del HTML principal:

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102936796533 HTTP/1.1 ]
C-0-#000053 -> [Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, application/vnd.ms-powerpoint, application/vnd.ms-excel, application/msword, appl]
C-0-#000194 -> [ication/x-shockwave-flash, */* ]
C-0-#000227 -> [Accept-Language: de-ch ]
C-0-#000251 -> [Accept-Encoding: gzip, deflate ]
C-0-#000283 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-0-#000347 -> [Host: localhost:4444 ]
```

El cliente solicita una conexión persistente, de modo que el servidor pueda enviar varios archivos a través de la misma conexión:

```xml
C-0-#000369 -> [Connection: Keep-Alive ]
```

El servidor proxy es una buena herramienta para comprobar si las cookies están configuradas correctamente o no. Aquí, vemos lo siguiente:

* AEM cookie de cq3session generada por el usuario de
* la cookie de cambio de modo de presentación generada por CFC
* una cookie denominada JSESSIONID; JSP la crea automáticamente si no se desactiva explícitamente con &lt;%@ page session=&quot;false&quot; %>:

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

El servidor cerrará la conexión 0 después de la solicitud. La conexión persistente no es posible porque la solicitud tiene un signo de interrogación. Esto significa que el servidor no puede devolver una versión en caché y, por lo tanto, no puede determinar la longitud del contenido en este momento, que es necesaria para una conexión persistente.

```xml
S-0-#000017 -> [Connection: Close ]
S-0-#000036 -> [Server: Communique Servlet Engine/3.5.5 ]
S-0-#000077 -> [Content-Type: text/html;charset=iso-8859-1 ]
S-0-#000121 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-0-#000158 -> [Set-Cookie: JSESSIONID=4161a56b-f193-d8-88a5-e09c5ff7ef2a;Path=/author ]
S-0-#000232 -> [ ]
```

En este caso, el servidor comienza a enviar el código del HTML en la conexión 0:

```xml
S-0-#000234 -> [<html> ]
S-0-#000242 -> [.<head> ]
S-0-#000251 -> [..<title>Welcome</title> ]
S-0-#000277 -> [.</head> ]
S-0-#000287 -> [.<body> ]
S-0-#000296 -> [..Welcome to Playground<br> ]
S-0-#000325 -> [..<img src="/author/logo.gif"> ]
S-0-#000357 -> [.</body> ]
S-0-#000367 -> [</html>]
```

La conexión 0 se cierra inmediatamente después de haber recibido el archivo HTML:

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

Ahora, la salida se inicia para la conexión 1, que descarga la imagen contenida en el código del HTML:

```xml
C-1-#000000 -> [GET /author/logo.gif HTTP/1.1 ]
C-1-#000031 -> [Accept: */* ]
C-1-#000044 -> [Referer: http://localhost:4444/author/prox.html?CFC_cK=1102936796533 ]
C-1-#000114 -> [Accept-Language: de-ch ]
C-1-#000138 -> [Accept-Encoding: gzip, deflate ]
C-1-#000170 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-1-#000234 -> [Host: localhost:4444 ]
```

De nuevo, el cliente solicita una conexión persistente:

```xml
C-1-#000256 -> [Connection: Keep-Alive ]
C-1-#000280 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-1-#000401 -> [ ]
S-1-#000000 -> [HTTP/1.0 200 OK ]
```

Para la conexión 1, el servidor puede proporcionar la conexión persistente, ya que la imagen es estática y, por lo tanto, se conoce la longitud del contenido.

```xml
S-1-#000017 -> [Connection: Keep-Alive ]
S-1-#000041 -> [Server: Communique Servlet Engine/3.5.5 ]
S-1-#000082 -> [Content-Type: image/gif ]
```

El servidor devuelve la longitud del contenido de la imagen en la conexión 1:

```xml
S-1-#000107 -> [Content-Length: 124 ]
S-1-#000128 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-1-#000165 -> [ ]
```

Ahora que la longitud del contenido está establecida, el servidor envía los datos de imagen en la conexión 1:

```xml
S-1-#000167 -> [GIF87a..........................,.......
...I....0.A..8......YDA.W...1..`i.`..6...Z...$@.F..)`..f..A.....iu.........$..;]
```

Una vez alcanzado el tiempo de espera de la conexión persistente, la conexión 1 también se cierra:

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

El ejemplo anterior es comparativamente sencillo, ya que las dos conexiones se producen de forma secuencial:

* en primer lugar, el servidor devuelve el código de HTML
* a continuación, el explorador solicita la imagen y abre una nueva conexión

En la práctica, una página puede generar muchas solicitudes paralelas de imágenes, hojas de estilo, archivos JavaScript, etc. Esto significa que los registros tienen entradas superpuestas de conexiones abiertas paralelas. En ese caso, recomendamos utilizar la opción -i para mejorar la legibilidad.
