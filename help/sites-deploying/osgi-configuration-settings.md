---
title: Configuración de OSGi
seo-title: Configuración de OSGi
description: Este artículo detalla los ajustes de configuración de OSGi (enumerados según el paquete) que son relevantes para la implementación del proyecto. La lista sirve de guía y no es exhaustiva.
seo-description: Este artículo detalla los ajustes de configuración de OSGi (enumerados según el paquete) que son relevantes para la implementación del proyecto. La lista sirve de guía y no es exhaustiva.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Configuración de OSGi{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) es un elemento fundamental en la pila de tecnología de AEM. Se utiliza para controlar los paquetes compuestos de AEM y su configuración.

OSGi &quot;*proporciona los primitivos estandarizados que permiten construir aplicaciones a partir de componentes pequeños, reutilizables y de colaboración. Estos componentes se pueden componer en una aplicación e implementar*&quot;.

Esto permite administrar fácilmente los paquetes, ya que se pueden detener, instalar e iniciar individualmente. Las interdependencias se gestionan automáticamente. Cada componente OSGi (consulte la Especificación [](https://www.osgi.org/Specifications/HomePage)OSGi) está contenido en uno de los distintos paquetes. When working with AEM there are several methods of managing the configuration settings for such bundles; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

Los siguientes ajustes de configuración OSGi (enumerados según el paquete) son relevantes para la implementación del proyecto. No es necesario realizar ajustes en todos los ajustes de la lista; algunos de ellos se mencionan para ayudarle a comprender el funcionamiento de AEM.

>[!CAUTION]
>
>La lista tiene por objeto servir de guía y no es exhaustiva. No todos los paquetes están enumerados, ni todos los parámetros de algunos de los paquetes que están.
>
>La configuración necesaria variará de un proyecto a otro.
>
>Consulte la consola Web para ver los valores utilizados e información detallada sobre los parámetros.

>[!NOTE]
>
>La herramienta Detalles [de configuración OSGi de](https://www.aemstuff.com/osgi.html) AEM se puede utilizar para enumerar las configuraciones de OSGi predeterminadas.

>[!NOTE]
>
>Es posible que se requieran más paquetes para áreas específicas de funcionalidad dentro de AEM. En estos casos, se pueden encontrar detalles de configuración en la página relacionados con la funcionalidad adecuada.

**AEM Replication Event Listener** Configure:

* Modos de **ejecución**, en los que los eventos de replicación se distribuirán a los oyentes. Por ejemplo, si se define como autor, entonces este es el sistema que &quot;iniciará&quot; la replicación.

* Es necesario agregar la **publicación** en modo de ejecución si el código del proyecto procesa eventos de replicación (replicación inversa) en un entorno de publicación. Por ejemplo, cuando se utiliza el despachante para vaciar del entorno de publicación o cuando se produce la replicación estándar a otras instancias de publicación.

**listener** de cambio de repositorio de AEM Configure:

* Las **Rutas**, ubicaciones para escuchar los eventos del repositorio listos para la distribución.

**Repositorio** de cliente Sling de CRX Configure el acceso al repositorio de contenido subyacente.

* La contraseña **** de administrador debe cambiarse después de la instalación para garantizar la [seguridad](/help/sites-administering/security-checklist.md) de la instancia.
* No deben ser necesarios otros cambios y hay que tener cuidado ya que pueden afectar al acceso al repositorio.

**Servicio** de correo Wiki Configure las opciones de correo electrónico para los correos electrónicos enviados por una wiki.

**Consola** de administración Apache Felix OSGi Configure:

* **Complementos**, los elementos de navegación principales (complementos de consola) que estarán disponibles en la consola **de administración web** Apache Felix como elementos de menú de nivel superior. Deshabilite los que no necesite, ya que cada uno requiere espacio y recursos.

>[!CAUTION]
>
>Asegúrese de configurar lo siguiente:
>
>**Nombre** de usuario y **Contraseña**, las credenciales para acceder a la consola de gestión web Apache Felix.
>La contraseña debe cambiarse después de la instalación inicial para garantizar la [seguridad](/help/sites-administering/security-checklist.md) de la instancia.

>[!NOTE]
>
>Esta configuración debe realizarse utilizando la consola Felix como se necesita al inicio, antes de que el repositorio esté disponible.

**Apache Sling Customizable Request Data Logger** Configure:

* **Nombre** del registrador y Formato **** de registro para configurar la ubicación y el formato de registro de solicitud y acceso (predeterminado: `request.log`). Este archivo de registro es esencial para analizar el rendimiento o la funcionalidad de depuración relacionados con la cadena web.
Esto se combina con el registrador de solicitudes Sling [Apache](#apacheslingrequestlogger).

Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md) de AEM y Registro de [Sling](https://sling.apache.org/site/logging.html).

**Apache Sling Eventing Thread Pool** Configure:

* **Tamaño** mínimo del grupo y Tamaño **** máximo del grupo, el tamaño del grupo utilizado para contener los subprocesos de evento.

* **Tamaño**de cola, el tamaño máximo de la cola de subprocesos si se agota el grupo.
El valor recomendado es `-1` porque establece la cola en ilimitada; si se establece un límite, pueden producirse pérdidas cuando se supera.

* El cambio de esta configuración puede ayudar al rendimiento en situaciones con un número elevado de eventos; por ejemplo, el uso pesado de AEM DAM o Workflow.
* Los valores específicos de su escenario deben establecerse mediante pruebas.
* Esta configuración puede afectar al rendimiento de la instancia, por lo que no debe cambiarla sin motivo ni consideración.

**Servlet** Apache Sling GET Configure algunos aspectos del procesamiento:

* **Índice** automático para habilitar o deshabilitar el procesamiento de directorios para la exploración.
* **Habilite** (o deshabilite) las representaciones predeterminadas, como **HTML**, **texto** sin formato, **JSON** o **XML**.
No debe deshabilitar JSON.

>[!NOTE]
>
>Esta configuración se configura automáticamente para instancias de producción si ejecuta AEM en modo [listo para](/help/sites-administering/production-ready.md)producción.

**Controlador** de Java Script de Apache Sling Configure los ajustes para la compilación de archivos .java como secuencias de comandos (servlets).

Ciertos ajustes pueden afectar al rendimiento, por lo que deben deshabilitarse siempre que sea posible, en particular para una instancia de producción.

* VM **** de origen y VM **de** destino, defina la versión de JDK como la que se usa como JVM de tiempo de ejecución

* para instancias de producción:

   * deshabilitar **Generar información de depuración**

**Instalador** de JCR de Apache Sling Estos parámetros probablemente no necesitan configuración, pero pueden ser útiles para saber al desarrollar o depurar. Por ejemplo, las carpetas de instalación pueden ser útiles para desproteger o crear un paquete.

* **Las carpetas de instalación llaman regexp** y **Máxima profundidad de jerarquía de las carpetas** de instalación: especifique dónde y a qué profundidad se buscan los recursos para instalar. Cuando se utiliza un comodín (como en .*/install) se buscarán todas las coincidencias apropiadas, por ejemplo `/libs/sling/install` y `/libs/cq/core/install`.

* **Ruta** de búsqueda, lista de rutas que jcrinstall busca recursos para ser instalados, junto con un número que indica el factor de ponderación de esa ruta.

**Apache Sling Job Event Handler** Configure los parámetros que administran la programación de trabajos:

* **Intervalo** de reintentos, **máximo de reintentos**, **máximo de trabajos** paralelos, tiempo **de espera de** confirmación, entre otros.

* Cambiar esta configuración puede mejorar el rendimiento en situaciones con un número elevado de trabajos; por ejemplo, el uso intensivo de AEM DAM y flujos de trabajo.
* Los valores específicos de su escenario deben establecerse mediante pruebas.
* No cambie esta configuración sin motivo, solo la tendrá debidamente en cuenta.

**Controlador** de secuencias de comandos JSP de Apache Sling Configure los ajustes relevantes de rendimiento para el controlador de secuencias de comandos JSP. Para mejorar el rendimiento, debe deshabilitar tanto como sea posible.

En particular para los casos de producción:

* deshabilitar **Generar información de depuración**
* deshabilitar **mantener Java generado**
* deshabilitar contenido **asignado**
* deshabilitar **mostrar fragmentos de origen**

>[!NOTE]
>
>Esta configuración se configura automáticamente para instancias de producción si ejecuta AEM en modo [listo para](/help/sites-administering/production-ready.md)producción.

**Configuración** de registro de Apache Sling Configure:

* **Nivel** de registro y Archivo **** de registro, para definir la ubicación y el nivel de registro de la configuración de registro central (error.log). El nivel se puede establecer en uno de `DEBUG`, `INFO`, `WARN`, `ERROR` y `FATAL`.

* **Número de archivos** de registro y umbral **de archivo** de registro para definir el tamaño y la rotación de versión del archivo de registro.

* **El patrón** de mensajes define el formato de los mensajes de registro.

Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md#global-logging) de AEM y Registro de [Sling](https://sling.apache.org/site/logging.html).

**Configuración del registrador de registros de Apache Sling (Configuración de fábrica)** Configure:

* **Nivel** de registro, **Archivo** de registro y Formato **de** mensaje para definir detalles del archivo de registro y los mensajes.

* **Registrador** para definir la categoría; por ejemplo: solo inicie sesión para com.day.cq.

* Mediante las configuraciones **de fábrica**, se puede agregar cualquier cantidad de configuraciones adicionales para satisfacer los distintos niveles de registro y categorías necesarias.
* Estas configuraciones son útiles durante el desarrollo; por ejemplo, para registrar mensajes TRACE para un servicio específico en un archivo de registro específico.
* Estas configuraciones son útiles en un entorno de producción; por ejemplo, para que los mensajes sobre un servicio específico se registren en un archivo de registro individual para facilitar la supervisión.

Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md) de AEM y Registro de [Sling](https://sling.apache.org/site/logging.html).

**Configuración del grabador de registros de Apache Sling (Configuración de fábrica)** Configure:

* **Archivo** de registro para definir la existencia de un archivo de registro.
* **Número de archivos** de registro para definir la rotación de la versión.

* El escritor puede ser utilizado por una configuración de **Apache Sling Logging Logger** .

* Estas configuraciones son útiles durante el desarrollo; por ejemplo, para registrar mensajes TRACE para un servicio específico en un archivo de registro específico.
* Estas configuraciones son útiles en un entorno de producción; por ejemplo, para que los mensajes sobre un servicio específico se registren en un archivo de registro individual para facilitar la supervisión.

Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md) de AEM y Registro de [Sling](https://sling.apache.org/site/logging.html).

**Apache Sling Main Servlet** Configure:

* **Número de llamadas por solicitud** y profundidad **de** recursión para proteger el sistema contra recursiones infinitas y llamadas de secuencia de comandos excesivas.

**Apache Sling MIME Type Service** Configure:

* **Tipos** MIME para agregar al sistema los requeridos por el proyecto. Esto permite que una `GET` solicitud de un archivo establezca el encabezado de tipo de contenido correcto para vincular el tipo de archivo y la aplicación.

**Filtro** de referente Sling de Apache Para abordar problemas de seguridad conocidos con la falsificación de solicitudes entre sitios (CSRF) en CRX WebDAV y Apache Sling, debe configurar el filtro de referente.

El servicio de filtro de referente es un servicio OSGi que le permite configurar:

* qué métodos http deben filtrarse
* si se permite un encabezado de referente vacío
* y una lista blanca de servidores para permitir además del host del servidor.

Consulte la lista de comprobación de [seguridad - Problemas con falsificación](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) de solicitudes entre sitios para obtener más información.

>[!NOTE]
>
>El Filtro de referente de Sling de Apache depende de la instalación de un paquete de corrección rápida.

**Apache Sling Request Logger** Configure:

* varios parámetros para definir cómo se registran las solicitudes.
* **Habilite Registro** de solicitudes para habilitar o deshabilitar.

* **Habilite el registro** de acceso para habilitar o deshabilitar.

Esto se asocia con el registrador de datos de solicitud personalizado [Apache Sling](#apacheslingcustomizablerequestdatalogger).

Para obtener más información, consulte [Registro](/help/sites-deploying/configure-logging.md) de AEM y Registro de [Sling](https://sling.apache.org/site/logging.html).

**Fábrica** de resolución de recursos de Apache Sling Configure los aspectos centrales de la resolución de recursos de Sling:

* **Rutas** de búsqueda de recursos, agregue cualquier ruta específica del proyecto (pero no elimine `/libs` ni `/apps`).

* **Direcciones URL** virtuales para definir las asignaciones de URL personales.

* **Asignaciones** de URL para definir cualquier alias; por ejemplo de `/content` a `/`.

* **Ubicación** de asignación, la configuración del asignador se externaliza en `/etc/map`.

* Utilice la instalación local (por ejemplo, use `https://localhost:4502/system/console/jcrresolver`) para determinar qué Resolver recursos está activo.

Para obtener más información, consulte: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>En particular, estas opciones deben configurarse en el repositorio.
>
>De lo contrario, AEM podría sobrescribir los cambios realizados en las asignaciones **de** URL mediante la consola Félix en el siguiente inicio.

**Apache Sling Servlet/Script Resolver and Error Handler** El servlet Sling y la resolución de secuencias de comandos tienen varias tareas:

1. Se utiliza como `ServletResolver` para seleccionar el Servlet o la secuencia de comandos que se va a llamar para gestionar la solicitud.

1. Actúa como el `SlingScriptResolver`.

1. Administra la gestión de errores implementando la `ErrorHandler` interfaz utilizando el mismo algoritmo para seleccionar servlets y secuencias de comandos de gestión de errores que se utiliza para resolver servlets y secuencias de comandos de procesamiento de solicitudes.

Se pueden definir varios parámetros, entre ellos:

* **Rutas** de ejecución enumera las rutas para buscar scripts ejecutables; al configurar rutas específicas, puede limitar qué secuencias de comandos se pueden ejecutar. Si no hay ninguna ruta configurada, se utiliza la ruta predeterminada ( `/` = raíz), esto permite la ejecución de todas las secuencias de comandos.
Si un valor de ruta configurado termina con una barra diagonal, se buscará en todo el subárbol. Sin esta barra final, la secuencia de comandos solo se ejecutará si es una coincidencia exacta.

* **Usuario** de secuencia de comandos: esta propiedad opcional puede especificar la cuenta de usuario del repositorio utilizada para leer las secuencias de comandos. Si no se especifica ninguna cuenta, el usuario se utiliza de forma predeterminada `admin` .

* **Extensiones** predeterminadas Lista de extensiones para las que se utilizará el comportamiento predeterminado. Esto significa que el último segmento de ruta del tipo de recurso se puede utilizar como nombre de secuencia de comandos.

**Day Commons GFX Font Helper** Al procesar gráficos puede utilizar DrawText para incrustar texto. Para ello, también puede instalar sus propias fuentes:

* Defina la ruta de **fuente** que se buscará para las fuentes específicas del proyecto.
Por ejemplo, `/apps/myapp/fonts`.

**Configuración proxy de configuración** proxy de componentes HTTP Apache para todo el código que utiliza el cliente HTTP Apache, que se utiliza cuando se realiza un HTTP; por ejemplo, al realizar la replicación.

Al crear una nueva configuración, no realice cambios en la configuración de fábrica sino que cree una nueva configuración de fábrica para este componente mediante el administrador de configuración disponible aquí: **https://localhost:4502/system/console/configMgr/**. La configuración proxy está disponible en **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>En AEM 6.0 y versiones anteriores, el proxy estaba configurado en Day Commons HTTP Client. A partir de AEM 6.1 y versiones posteriores, la configuración proxy se ha trasladado a la configuración &quot;Apache HTTP Components Proxy Configuration&quot; en lugar de a la configuración &quot;Day Commons HTTP Client&quot;.

**Day CQ Antispam** Configure el servicio antispam (Akismet) utilizado. Esto requiere que registre:

* **Proveedor**
* **Clave de API**
* **URL registrada**

**Administrador** de bibliotecas HTML de Adobe Granite Configure esto para controlar el manejo de las bibliotecas de cliente (css o js); incluyendo, por ejemplo, cómo se ve la estructura subyacente.

* Para instancias de producción:

   * active **Minify** (para eliminar caracteres de CRLF y de espacio en blanco).
   * active **Gzip** (para permitir que se comprueben los archivos y se acceda a ellos con una sola solicitud).
   * deshabilitar **depuración**
   * deshabilitar **temporización**

* Para el desarrollo de JS (especialmente al depurar/depurar):

   * deshabilitar **Minify**
   * active **Depurar** para separar los archivos para depurarlos y usarlos con firebug.
   * activar **Temporización** en caso de interés en temporización.
   * active la consola **de depuración** para ver los mensajes de registro de la consola JS.

>[!CAUTION]
>
>Al cambiar la configuración de **Minify** o **Gzip** , también deberá eliminar el contenido de `/var/clientlibs`. Esta es una versión en caché de clientlibs y se volverá a crear cuando se solicite la próxima vez.

>[!NOTE]
>
>Esta configuración se configura automáticamente para instancias de producción si ejecuta AEM en modo [listo para](/help/sites-administering/production-ready.md)producción.

**Controlador** de autenticación de encabezado HTTP CQ Day Configuración de todo el sistema para el método de autenticación básico de la solicitud HTTP.

Al utilizar grupos [de usuarios](/help/sites-administering/cug.md) cerrados puede configurar (entre otros):

* **Dominio HTTP**
* Página de inicio de sesión **predeterminada**

**Comprobación del servicio** del comprobador de vínculos de CQ por día y, si es necesario, configure:

* **Período** del programador para definir el intervalo en el que se comprueban automáticamente los vínculos externos.

* Marque Intervalo **de tolerancia de vínculo** incorrecto para el período después del cual un vínculo externo no exitoso se considera malo.
* **Patrones** de anulación de comprobación de vínculos para definir las rutas que se excluirán de la comprobación de vínculos.

**Tarea** de Day CQ Link Checker Configure los ajustes de una única tarea de comprobación de vínculos (una tarea que comprueba un vínculo externo):

* Compruebe los intervalos definidos en Intervalo **de prueba de** vínculo correcto e Intervalo de prueba de vínculo **incorrecto**

* Los distintos parámetros relacionados con los proxies para el acceso a Internet y NTLM necesarios para el acceso externo al comprobar un vínculo.

**Day CQ Mail Service** Configure el nombre de host y los detalles de acceso para el servidor de correo. Consulte la sección Configuración del servicio de correo.

**Newsletter** de CQ MCM de día Configure los distintos ajustes utilizados con la newsletter.

**Asignación** de raíz de CQ de día Configure:

* **Ruta** de destino para definir hacia dónde se redirigirá una solicitud a &quot; `/`&quot;.

Hay dos IU disponibles en AEM:

* la IU táctil es la IU estándar
* y la IU clásica depredada sigue funcionando completamente

Al utilizar la asignación raíz de AEM, puede configurar la IU que desea tener como predeterminada para su instancia:

* Para que la IU táctil sea la IU predeterminada, la ruta de acceso **de** destino debe señalar a:

   ```
      /projects.html
   ```

* Para que la IU clásica sea la IU predeterminada, la ruta de acceso **de** Target debe señalar a:

   ```
      /welcome.html
   ```

>[!NOTE]
>
>Tras una instalación estándar, la IU táctil es la IU predeterminada.

**Detalles del controlador** de autenticación SSO de Adobe Granite: Configurar el inicio de sesión único (SSO); estos ajustes suelen ser necesarios en la configuración de creación empresarial, a menudo junto con LDAP.

Hay varias propiedades de configuración disponibles:

* **Ruta** de acceso para la que está activo este controlador de autenticación. Si este parámetro se deja vacío, el controlador de autenticación se desactiva. Por ejemplo, la ruta / hace que el controlador de autenticación se utilice para todo el repositorio.

* **Clasificación** de servicios El valor de clasificación de servicios de OSGi Framework se utiliza para indicar el orden utilizado para llamar a este servicio. Se trata de un `int` valor en el que los valores más altos designan una prioridad mayor.
El valor predeterminado es `0`.

* **Nombres** de encabezadosLos nombres de los encabezados que pueden contener un ID de usuario.

* **Nombres** de cookiesNombre de las cookies que pueden contener un ID de usuario.

* **Nombres** de parámetrosNombre de los parámetros de solicitud que pueden proporcionar el ID de usuario.

* **Mapa** del usuario Para los usuarios seleccionados, el nombre de usuario extraído de la solicitud HTTP se puede reemplazar por otro en el objeto de credenciales. La asignación se define aquí. Si el nombre de usuario `admin` aparece a ambos lados del mapa, se omitirá la asignación. Tenga en cuenta que el carácter &quot;=&quot; debe tener un carácter de escape con un &quot;\&quot; inicial.

* **Formato** Indica el formato en el que se proporciona el ID de usuario. Uso:

   * `Basic` si el ID de usuario está codificado en el formato de autenticación básica HTTP
   * `AsIs` si el ID de usuario se proporciona en texto sin formato o cualquier valor de expresión regular aplicado debe utilizarse tal cual o cualquier expresión regular

**Filtro** de depuración de CQ WCM de día Resulta útil cuando se desarrolla, ya que permite el uso de sufijos como ?debug=layout al acceder a una página. Por ejemplo, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout proporcionará información de diseño que puede ser de interés para el desarrollador.

* Desactívelo en las instancias de producción para garantizar el rendimiento y la seguridad.

**Configuración del filtro** WCM de CQ de día:

* **Modo WCM **para definir el modo predeterminado.
* En una instancia de autor esto puede ser `edit`, `disable,preview` o `analytics`.
Se puede acceder a los otros modos desde la barra de tareas o bien `?wcmmode=disabled` se puede usar el sufijo para emular un entorno de producción.

* En una instancia de publicación, esto debe establecerse para `disabled` garantizar que no se pueda acceder a ningún otro modo.

>[!NOTE]
>
>Esta configuración se configura automáticamente para instancias de producción si ejecuta AEM en modo [listo para](/help/sites-administering/production-ready.md)producción.

**Configuración del configurador** del comprobador de vínculos WCM de Day CQ:

* **Lista de configuraciones** de reescritura para especificar una lista de ubicaciones para configuraciones de comprobador de vínculos basadas en contenido. Las configuraciones pueden basarse en el modo de ejecución; esto es importante para distinguir entre los entornos de autor y publicación, ya que la configuración del comprobador de vínculos puede diferir.

**Procesador** de páginas CQ WCM de día Configure:

* **Rutas**, una lista de ubicaciones en las que el sistema escucha las modificaciones de página antes de activar un `jcr:Event`.

**Rastreador** de impresiones de página de Adobe Para una instancia de autor, configure:

* **sling.auth.requirements**: establezca el valor de esta propiedad en `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Esta configuración permitirá solicitudes anónimas al servicio de seguimiento.

>[!NOTE]
>
>Consulte Impresiones [de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obtener más información.

**Estadísticas** de página de CQ WCM de día Para una instancia de publicación, configure:

* **URL para enviar datos** a fin de configurar la URL utilizada para rastrear las estadísticas de la página (es vital si una solicitud de rastreador pasa por el despachante); por ejemplo, el valor predeterminado es `https://localhost:4502/libs/wcm/stats/tracker`.

* **Secuencia de comandos de seguimiento habilitada** para habilitar ( `true`) o deshabilitar ( `false`) la inclusión de la secuencia de comandos de seguimiento en las páginas. El valor predeterminado es `false`.

>[!NOTE]
>
>Consulte Impresiones [de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obtener más información.

**Day CQ WCM Version Manager** Controle si las versiones se administran en el sistema y cómo se administran en él:

* **Crear versión al activarla**, habilitada en una instalación estándar
* **Habilitar depuración**

* **Purgar rutas**, las rutas que buscará una acción de búsqueda
* **Rutas** de versiones implícitas, las rutas en las que el control de versiones implícito está activo.

* **Edad** máxima de la versión, la edad máxima (en días) de una versión

* **Número máximo de versiones**, el número máximo de versiones que se deben conservar

Consulte Depuración [de versiones](/help/sites-deploying/version-purging.md) para obtener más información.

**Servicio** de notificación por correo electrónico de flujo de trabajo de CQ de día Configure la configuración de correo electrónico de las notificaciones enviadas por un flujo de trabajo.

**Day CQSE HTTP Service** Control del motor de servlet CQ:

* **NIO para HTTP, **Si se utiliza o no NIO para HTTP. La opción predeterminada es true. Solo se usa si HTTP está habilitado.
* **Tiempo de espera de conexión, **Tiempo de espera de conexión en milisegundos. Esta propiedad se aplica a conexiones HTTP y HTTPS. El valor predeterminado es de 60 segundos.

* **Habilite HTTPS,** esté o no habilitado HTTPS. El valor predeterminado es false.
* **Tiempo de espera** de sesión, duración predeterminada de una sesión HTTP especificada en minutos. Si el tiempo de espera es 0 o menos, las sesiones nunca se agotarán. El valor predeterminado es de 10 minutos.
* **Registro** de depuración, Escribir o no mensajes a nivel DEBUG. El valor predeterminado es false.
* **Tamaño** del búfer de solicitud, Tamaño del búfer para solicitudes en bytes. El valor predeterminado es 8 KB.
* **Número máximo de subprocesos**, número máximo de subprocesos que se utilizarán para gestionar solicitudes. El valor predeterminado es 200.

Las siguientes propiedades solo se aplican si HTTPS está habilitado.

* **Puerto** HTTPS, puerto en el que escuchar la solicitud HTTPS. El valor predeterminado es 433.
* **NIO para HTTPS**, si se debe o no utilizar NIO para HTTP. Valores predeterminados del valor de la propiedad NIO para HTTP.
* **Keystore**, ruta absoluta al almacén de claves para usar con HTTPS. Necesario si HTTPS está habilitado.
* **Contraseña** de Keystore, Contraseña para acceder a Keystore.
* **Alias** de clave, Alias de la clave secreta en Keystore.
* **Contraseña** de clave, Contraseña para desbloquear la clave secreta en Keystore.
* **Certificado** de cliente, requisito para que el cliente proporcione un certificado válido. El valor predeterminado es ninguno.

Consulte también [Activación de HTTP sobre SSL](/help/sites-administering/ssl-by-default.md) para obtener más información sobre las opciones relacionadas con SSL y una descripción completa sobre cómo habilitar HTTPS para CQSE.

**CQ Rewriter HTML Parser Factory**

Controla el analizador de HTML para el reescritor de CQ.

* **Etiquetas adicionales para procesar** : puede agregar o quitar etiquetas HTML para que el analizador las procese. De forma predeterminada, se procesan las etiquetas siguientes: A,IMG,ÁREA,FORMULARIO,BASE,VÍNCULO,SECUENCIA DE COMANDOS,CUERPO,CABEZA.
* **Conservar mayúsculas y minúsculas** : de forma predeterminada, el analizador HTML convierte atributos en mayúsculas y minúsculas (por ejemplo, eBay) en minúsculas (por ejemplo, ebay). Puede desactivarlo para conservar los atributos de mayúsculas y minúsculas del camello. Esto resulta útil cuando se utilizan marcos de front-end como Angular 2.

**Agrupación** de conexiones JDBC Day Commons Configure el acceso a una base de datos externa que se está utilizando como fuente de contenido.

Se trata de una configuración de fábrica, por lo que se pueden configurar varias instancias.

**Servicio** de sesiones de DPS de Adobe CQ Media Gestionar sesiones de DPS para su uso con publicaciones.

En particular, puede definir `dps.session.service.url.name`: el valor predeterminado es [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**CDN Rewriter** La comunicación entre AEM y un CDN debe garantizarse para que los recursos y binarios se entreguen al usuario final de forma segura. Esto implica dos tareas:

* Acceso al recurso desde AEM a través de la CDN por primera vez (o después de que caduque en la caché).
* El acceso seguro al recurso almacenado en la caché en CDN, ya que una vez que el recurso se haya almacenado en la caché en CDN, la solicitud no irá a AEM y todos los usuarios que tengan acceso a ese recurso en deben ser atendidos desde CDN.

AEM proporciona un reescritor para reescribir las URL de recursos internos en URL de CDN externas. Vuelve a escribir los vínculos que se pasarán a la CDN, incluida una firma JWS y un tiempo de caducidad para permitir el acceso seguro al recurso. Esta función se utiliza en instancias de autor.

El flujo total es el siguiente:

1. El usuario se autentica con AEM y solicita una página con recursos.
1. La página solicitada contiene un recurso similar a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. Rewriter transforma el vínculo a una URL de CDN que contiene una firma de JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. El navegador del usuario reenvía la solicitud de recurso al servidor CDN
1. CDN debe configurarse para reenviar la solicitud a AEM junto con el `cdn_sign` parámetro .
1. Un controlador de autenticación valida el `cdn_sign` parámetro y devuelve el recurso a CDN, que luego se envía al usuario

El flujo entre el navegador del usuario, la CDN y AEM se puede visualizar de la siguiente manera.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>Actualmente, esta función solo está habilitada para instancias de autor de AEM.

**CDNConfigServiceImpl** Proporciona configuraciones de CDN

La función de reescritura CDN se puede habilitar proporcionando el nombre **de dominio de distribución** CDN en la configuración de com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

El servicio también contiene otras opciones de configuración como habilitar/deshabilitar la reescritura de CDN, prefijos de ruta para los que se realiza la reescritura de CDN, valores TTL y protocolo (HTTP o HTTPS).

**CDNRewriter** Un reescritor para reescribir direcciones URL de imágenes internas en direcciones URL de CDN

El valor Atributos **de** etiqueta en com.adobe.cq.cdn.rewriter.impl.CDNRewriter se puede definir de modo que solo se vuelvan a escribir los vínculos de imagen selectivos.
