---
title: Cómo utilizar la herramienta Servidor proxy
seo-title: Cómo utilizar la herramienta Servidor proxy
description: El servidor proxy actúa como servidor intermedio que transmite solicitudes entre un cliente y un servidor
seo-description: El servidor proxy actúa como servidor intermedio que transmite solicitudes entre un cliente y un servidor
uuid: 30f4f46d-839e-4d23-a511-12f29b3cc8aa
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: dfbc1d2f-80c1-4564-a01c-a5028b7257d7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Cómo utilizar la herramienta Servidor proxy{#how-to-use-the-proxy-server-tool}

El servidor proxy actúa como servidor intermedio que transmite solicitudes entre un cliente y un servidor. El servidor proxy realiza un seguimiento de todas las interacciones cliente-servidor y genera un registro de toda la comunicación TCP. Esto le permite monitorear exactamente lo que sucede, sin tener que acceder al servidor principal.

Puede encontrar el servidor proxy en la instalación de AEM aquí:

`crx-quickstart/opt/helpers/proxy-2.1.jar`

Puede utilizar el servidor proxy para supervisar toda la interacción cliente-servidor, independientemente del protocolo de comunicación subyacente. Por ejemplo, puede supervisar los siguientes protocolos:

* HTTP para páginas Web
* HTTPS para páginas Web seguras
* SMTP para mensajes de correo electrónico
* LDAP para administración de usuarios

Por ejemplo, puede colocar el servidor proxy entre dos aplicaciones cualesquiera que se comuniquen a través de una red TCP/IP; Por ejemplo, un navegador web y AEM. Esto le permite monitorear exactamente lo que sucede cuando solicita una página de CQ.

## Inicio de la herramienta Servidor proxy {#starting-the-proxy-server-tool}

Inicie el servidor en la línea de comandos:

`java -jar proxy-2.1.jar <host> <remoteport> <localport> [options]`

**Parámetros**

`<host>`

Esta es la dirección host de la instancia de CRX a la que desea conectarse. Si la instancia está en el equipo local, entonces será `localhost`.

`<remoteport>`

Es el puerto host de la instancia CRX de destino. Por ejemplo, el valor predeterminado de una instalación de AEM recién instalada es **`4502`** y el valor predeterminado de una instancia de autor de AEM recién instalada es `4502`.

`<localport>`

Este es el puerto del equipo local al que desea conectarse para acceder a la instancia de CRX a través del proxy.

**Opciones**

`-q` (modo silencioso)

No escribe la salida en la ventana de la consola. Utilícelo si no desea ralentizar la conexión o si registra la salida en un archivo (consulte la opción -logfile).

`-b`(modo binario)

Si busca combinaciones de bytes específicas en el tráfico, habilite el modo binario. El resultado contendrá la salida hexadecimal y de caracteres.

`-t` (entradas de registro de marca de hora)

Agrega una marca de hora a cada salida del registro. La marca de hora se marca en segundos, por lo que puede que no sea adecuada para comprobar solicitudes únicas. Utilícelo para localizar eventos que se produjeron en un momento específico si utiliza el servidor proxy durante un período de tiempo más largo.

`-logfile <filename>`(escribir en el archivo de registro)

Escribe la conversación cliente-servidor en un archivo de registro. Este parámetro también funciona en modo silencioso.

**`-i <numIndentions>`**(añadir sangría)

Cada conexión activa tiene una sangría para una mejor legibilidad. El valor predeterminado es 16 niveles. Esta función se introdujo con `proxy.jar version 1.16`.

### Formato de registro {#log-format}

Todas las entradas de registro producidas por proxy-2.1.jar tienen el siguiente formato:

`[timestamp (optional)] [Client|Server]-[ConnectionNumber]-[BytePosition] ->[Character Stream]`

Por ejemplo: una solicitud para una página Web puede tener el siguiente aspecto:

`C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]`

* C significa que esta entrada proviene del cliente (es una solicitud para una página Web)
* 0 es el número de conexión (el contador de conexiones comienza en 0)
* &#x200B;# 00000 el desplazamiento en el flujo de bytes. Esta es la primera entrada, por lo que el desplazamiento es 0.
* `[GET <?>]` es el contenido de la solicitud, en el ejemplo uno de los encabezados HTTP (url).

Cuando se cierra una conexión, se registra la siguiente información:

```
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

Muestra el número de bytes que pasaron entre el cliente ( `C`) y el servidor ( `S`) en la sexta conexión y a la velocidad promedio.

**Ejemplo de salida de registro**

Como ejemplo, considere una página que produzca el siguiente código cuando se le solicite:

### Ejemplo {#example}

Como ejemplo, considere un documento HTML muy sencillo ubicado en el repositorio en

`/content/test.html`

junto a un archivo de imagen ubicado en

`/content/test.jpg`

El contenido de `test.html` es:

```xml
<html>
<head>
    <title>Test</title>
</head>
<body>
    Test<br>
    <img src="test.jpg">
</body>
</html>
```

Suponiendo que la instancia de AEM se está ejecutando en `localhost:4502` nosotros iniciamos el proxy de este modo:

`java -jar proxy.jar localhost 4502 4444 -logfile test.log`

Ahora se puede acceder a la instancia de CQ/CRX a través del proxy en `localhost:4444` y todas las comunicaciones a través de este puerto se registran en `test.log`.

Si ahora vemos el resultado del proxy, veremos la interacción entre el navegador y la instancia de AEM.

Al iniciar, el proxy genera lo siguiente:

```xml
starting proxy for localhost:4502 on port 4444
using logfile: <some-dir>/crx-quickstart/opt/helpers/test.log
```

A continuación, abrimos un navegador y accedemos a la página de prueba:

`http://localhost:4444/content/test.html`

y vemos que el explorador realiza una `GET` solicitud para la página:

```shell
C-0-#000000 -> [GET /content/test.html HTTP/1.1 ]
C-0-#000033 -> [Host: localhost:4444 ]
C-0-#000055 -> [Connection: keep-alive ]
C-0-#000079 -> [User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11 ]
C-0-#000212 -> [Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8 ]
C-0-#000285 -> [Accept-Encoding: gzip,deflate,sdch ]
C-0-#000321 -> [Accept-Language: en-US,en;q=0.8 ]
C-0-#000354 -> [Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.3 ]
C-0-#000402 -> [Cookie: login-token=179ba6bd-e0a7-4909-a965-e11c7f2bc2fc%3a618bd8a8-fbaf-43c5-827d-c84c62248c5e_22ee860cc9036fee%3acrx.default%3b21148fb0-eb6c]
C-0-#000543 -> [-43c9-a2b9-c8d40618d8ae%3ad87a3d1a-5e9a-4d5a-bab1-0ee60ad6d8df_d0e4ddce0fcd84b6%3acrx.default%3b5cb95227-ea51-47bf-850b-68ad1dfd7297%3af3bbb6]
C-0-#000684 -> [59-7913-4285-8857-832c087bafd5_c484727d3b3665ad%3acrx.default; ys-cq-siteadmin-tree=o%3Awidth%3Dn%253A240%5EselectedPath%3Ds%253A/content ]
C-0-#000824 -> [ ]
```

La instancia de AEM responde con el contenido del archivo `test.html`:

```shell
S-0-#000000 -> [HTTP/1.1 200 OK ]
S-0-#000017 -> [Connection: Keep-Alive ]
S-0-#000041 -> [Server: Day-Servlet-Engine/4.1.24  ]
S-0-#000077 -> [Content-Type: text/html;charset=utf-8 ]
S-0-#000116 -> [Content-Length: 104 ]
S-0-#000137 -> [Date: Mon, 16 Jul 2012 11:23:38 GMT ]
S-0-#000174 -> [Last-Modified: Mon, 16 Jul 2012 11:19:27 GMT ]
S-0-#000220 -> [ ]
S-0-#000222 -> [<html>]
S-0-#000229 -> [<head>]
S-0-#000236 -> [    <title>Test</title>]
S-0-#000260 -> [</head> ]
S-0-#000269 -> [<body>]
S-0-#000276 -> [ Test<br>]
S-0-#000286 -> [    <img src="test.jpg">]
S-0-#000311 -> [</body>]
S-0-#000319 -> [</html>]
```

### Usos del servidor proxy {#uses-of-the-proxy-server}

Los siguientes escenarios ilustran algunos de los propósitos para los que se puede utilizar el servidor proxy:

**Comprobar las cookies y sus valores**

El siguiente ejemplo de entrada de registro muestra todas las cookies y sus valores enviados por el cliente en la sexta conexión abierta desde que se inició el proxy:

`C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]`

**Comprobación de encabezados y sus valores**

El siguiente ejemplo de entrada de registro muestra que el servidor puede establecer una conexión permanente y que el encabezado de longitud de contenido está configurado correctamente:

```
S-7-#000017 -> [Connection: Keep-Alive ]
 ...
 S-7-#000107 -> [Content-Length: 124 ]
```

**Comprobación de si la función Mantener activo funciona**

Mantener vivo es una característica de HTTP que permite al cliente reutilizar la conexión TCP con el servidor para realizar varias solicitudes (para el código de página, imágenes, hojas de estilo, etc.). Sin el mantenimiento, el cliente tiene que establecer una nueva conexión para cada solicitud.

Para comprobar si la función Mantener viva funciona:

* Inicie el servidor proxy.
* Solicite una página.
* Si la función Mantener vivo funciona, el contador de conexiones nunca debe superar las 5 a 10 conexiones.
* Si la función Mantener vivo no funciona, el contador de conexiones aumenta rápidamente.

**Búsqueda de solicitudes perdidas**

Si pierde solicitudes en un servidor complejo, por ejemplo con un servidor de seguridad y un distribuidor, puede utilizar el servidor proxy para averiguar dónde se perdió la solicitud. En el caso de un servidor de seguridad:

* Iniciar un proxy antes de un servidor de seguridad
* Iniciar otro proxy después de un servidor de seguridad
* Utilícelos para ver hasta dónde llegan las solicitudes.

**Solicitudes en cola**

Si experimenta solicitudes de bloqueo de vez en cuando:

* Inicie el proxy.
* Espere o escriba el registro de acceso en un archivo con cada entrada con una marca de tiempo.
* Cuando la solicitud empieza a colgar, puede ver cuántas conexiones estaban abiertas y qué solicitud está causando problemas.

