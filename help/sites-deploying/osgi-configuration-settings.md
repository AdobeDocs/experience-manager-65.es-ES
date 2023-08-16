---
title: Ajustes de configuración de OSGi
seo-title: OSGi Configuration Settings
description: Este artículo detalla los ajustes de configuración de OSGi (enumerados según el paquete) que son relevantes para la implementación del proyecto. La lista sirve de directriz y no es exhaustiva.
seo-description: This article details the OSGi configuration settings (listed according to bundle) that are relevant to project implementation. The list acts as a guideline and it is not exhaustive.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: Configuring
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '3429'
ht-degree: 0%

---

# Ajustes de configuración de OSGi{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) AEM es un elemento fundamental en la pila tecnológica de los. AEM Se utiliza para controlar los paquetes compuestos de y su configuración de los paquetes de componentes de la interfaz de usuario de la interfaz de usuario de.

OSGi &quot;*proporciona las primitivas estandarizadas que permiten crear aplicaciones a partir de componentes pequeños, reutilizables y de colaboración. Estos componentes se pueden componer en una aplicación e implementarse*&quot;.

Esta funcionalidad permite administrar fácilmente los paquetes, ya que se pueden detener, instalar e iniciar individualmente. Las interdependencias se gestionan automáticamente. Cada componente OSGi (consulte la [Especificación de OSGi](https://docs.osgi.org/specification/)) está contenido en uno de los distintos paquetes. AEM Al trabajar con los paquetes, existen varios métodos para administrar los ajustes de configuración de dichos paquetes; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

Las siguientes opciones de configuración de OSGi (enumeradas según el paquete) son relevantes para la implementación del proyecto. AEM No es necesario ajustar todos los ajustes enumerados, algunos se mencionan para ayudarle a comprender cómo funciona la configuración de la lista de la manera en que funciona la.

>[!CAUTION]
>
>La lista tiene por objeto servir de directriz y no es exhaustiva. No se enumeran todos los paquetes ni todos los parámetros de algunos de los paquetes que sí lo están.
>
>La configuración necesaria varía según el proyecto.
>
>Consulte la consola web para obtener información detallada sobre los parámetros y los valores utilizados.

>[!NOTE]
>
>La herramienta Diferencias de configuración de OSGi, que forma parte de la variable [AEM Herramientas de](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17488.html?lang=es), se puede utilizar para enumerar las configuraciones predeterminadas de OSGi.

>[!NOTE]
>
>AEM Es posible que se requieran paquetes adicionales para áreas específicas de funcionalidad dentro de la aplicación de la. En estos casos, los detalles de configuración se pueden encontrar en la página relacionada con la funcionalidad adecuada.

**AEM Listener de eventos de replicación** Configurar:

* El **Modos de ejecución**, en el que se distribuyen los eventos de replicación a los oyentes. Por ejemplo, si se define como autor, es el sistema el que &quot;inicia&quot; la replicación.

* Agregar el modo de ejecución **publicar** si el código del proyecto procesa eventos de replicación (replicación inversa) en un entorno de publicación. Por ejemplo, cuando se utiliza Dispatcher para vaciar del entorno de publicación o cuando se produce la replicación estándar en otras instancias de publicación.

**AEM Listador de cambio de repositorio** Configurar:

* El **Rutas**, ubicaciones para detectar eventos de repositorio listos para su distribución.

**Repositorio de clientes de CRX Sling** Configure el acceso al repositorio de contenido subyacente.

* El **Contraseña de administrador** debe cambiarse después de la instalación para garantizar que [seguridad](/help/sites-administering/security-checklist.md) de su instancia.
* No deben ser necesarios otros cambios y debe tenerse cuidado, ya que pueden afectar al acceso al repositorio.

**Consola de administración de Apache Felix OSGi** Configurar:

* **Complementos**, los elementos de navegación principales (complementos de consola) que estarán disponibles en la **Consola de administración web Apache Felix** como elementos de menú de nivel superior. Deshabilite las que no necesite, ya que cada una de ellas requiere espacio y recursos.

>[!CAUTION]
>
>Asegúrese de configurar lo siguiente:
>
>**Nombre de usuario** y **Contraseña**, las credenciales para acceder a la propia consola de administración web de Apache Felix.
>La contraseña debe cambiarse después de la instalación inicial para garantizar la [seguridad](/help/sites-administering/security-checklist.md) de su instancia.

>[!NOTE]
>
>Esta configuración debe realizarse utilizando la consola Felix según sea necesario al inicio, antes de que el repositorio esté disponible.

**Registrador de datos de solicitud personalizable de Apache Sling** Configurar:

* **Nombre del registrador** y **Formato de registro** para configurar la ubicación y el formato del registro de solicitudes y acceso (predeterminado: `request.log`). Este archivo de registro es esencial al analizar el rendimiento o la funcionalidad de depuración relacionada con la cadena web. Está emparejado con el [Registrador de solicitudes de Apache Sling](#apacheslingrequestlogger).

Consulte [AEM Registro de](/help/sites-deploying/configure-logging.md) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Grupo de hilos de eventos de Apache Sling** Configurar:

* **Tamaño mínimo del grupo** y **Tamaño máximo del grupo**, el tamaño del grupo utilizado para albergar subprocesos de evento.

* **Tamaño de cola**, el tamaño máximo de la cola de subprocesos si se agota el grupo.
El valor recomendado es `-1` porque establece la cola en ilimitada. Si se establece un límite, pueden producirse pérdidas cuando se supera.

* Cambiar esta configuración puede ayudar al rendimiento en escenarios con un número elevado de eventos. AEM Por ejemplo, uso intensivo de DAM o flujo de trabajo de la.
* Los valores específicos de su escenario deben establecerse con pruebas.
* Esta configuración puede afectar al rendimiento de su instancia, por lo que no la cambie sin motivo y teniendo en cuenta los motivos.

**Apache Sling GET Servlet** Configure algunos aspectos del procesamiento:

* **Índice automático** para habilitar/deshabilitar el procesamiento de directorios para la exploración.
* **Activar** (o deshabilitar) las representaciones predeterminadas, como **HTML**, **Texto sin formato**, **JSON**, o **XML**.
No deshabilite JSON.

>[!NOTE]
>
>AEM Esta configuración se configura automáticamente para las instancias de producción si ejecuta en el [Modo Producción lista](/help/sites-administering/production-ready.md).

**Apache Sling JavaScript Handler** Configure las opciones para la compilación de archivos .java como scripts (servlets).

Ciertas configuraciones pueden afectar al rendimiento. Deshabilite esta configuración siempre que sea posible, especialmente en el caso de una instancia de producción.

* **VM de origen** y **VM de destino**, defina la versión de JDK que se utiliza como JVM de tiempo de ejecución

* para instancias de producción:

   * disable **Generar información de depuración**

**Programa de instalación de Apache Sling JCR** Es probable que estos parámetros no necesiten configuración, pero puede resultar útil conocerlos al desarrollar o depurar. Por ejemplo, las carpetas de instalación pueden ser útiles para proteger o desproteger, o crear un paquete.

* **Nombre de carpetas de instalación regexp** y **Profundidad máxima de jerarquía de las carpetas de instalación** : especifique dónde y a qué profundidad se buscan los recursos que se van a instalar en las carpetas del repositorio. Cuando se usa un comodín (como en ).&#42;/install) se buscan todas las coincidencias adecuadas, por ejemplo, `/libs/sling/install` y `/libs/cq/core/install`.

* **Ruta de búsqueda**, una lista de rutas en las que jcrinstall busca los recursos que se van a instalar, junto con un número que indica el factor de ponderación de esa ruta.

**Controlador de eventos del trabajo Apache Sling** Configure parámetros que administren la programación de trabajos:

* **Intervalo de reintento**, **Máximo de reintentos**, **Máximo de trabajos paralelos**, **Confirmar tiempo de espera**, entre otros.

* AEM Cambiar esta configuración puede mejorar el rendimiento en escenarios con un número elevado de trabajos; por ejemplo, un uso intensivo de DAM y flujos de trabajo de la administración de flujos de trabajo (DAM) y de la administración de flujos de trabajo.
* Los valores específicos de su escenario deben establecerse con pruebas.
* No cambie esta configuración sin motivo, solo cambie después de haber tomado las debidas medidas.

**Apache Sling JSP Script Handler** Configure las opciones relevantes de rendimiento para el controlador de scripts JSP. Para mejorar el rendimiento, debe deshabilitar tanto como sea posible.

En particular para las instancias de producción:

* disable **Generar información de depuración**
* disable **Mantener Java generado™**
* disable **Contenido asignado**
* disable **Mostrar fragmentos de origen**

>[!NOTE]
>
>AEM Esta configuración se configura automáticamente para las instancias de producción si ejecuta en el [Modo Producción lista](/help/sites-administering/production-ready.md).

**Configuración de registro de Apache Sling** Configurar:

* **Nivel de registro** y **Archivo de registro**, para definir la ubicación y el nivel de registro de la configuración del registro central (error.log). El nivel se puede establecer en uno de `DEBUG`, `INFO`, `WARN`, `ERROR`, y `FATAL`.

* **Número de archivos de registro** y **Umbral de archivo de registro** para definir el tamaño y la rotación de versiones del archivo de registro.

* **Patrón de mensajes** define el formato de los mensajes de registro.

Consulte [AEM Registro de](/help/sites-deploying/configure-logging.md#global-logging) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Configuración del registrador de Apache Sling (configuración de fábrica)** Configurar:

* **Nivel de registro**, **Archivo de registro** y **Formato del mensaje** para definir los detalles del archivo de registro y los mensajes.

* **Logger** para definir la categoría; por ejemplo, registrar solo para com.day.cq.

* Mediante **Configuraciones de fábrica**, se puede añadir cualquier número de configuraciones adicionales para satisfacer los distintos niveles de registro y categorías necesarios.
* Estas configuraciones son útiles durante el desarrollo; por ejemplo, para registrar mensajes del TRACE para un servicio específico en un archivo de registro específico.
* Estas configuraciones son útiles en un entorno de producción; por ejemplo, para tener mensajes sobre un servicio específico registrados en un archivo de registro individual para facilitar la monitorización.

Consulte [AEM Registro de](/help/sites-deploying/configure-logging.md) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Configuración del escritor de registro de Apache Sling (configuración de fábrica)** Configurar:

* **Archivo de registro** para definir la existencia de un archivo de registro.
* **Número de archivos de registro** para definir la rotación de versión.

* El escritor puede ser utilizado por un **Configuración del registrador de Apache Sling** configuración.

* Estas configuraciones son útiles durante el desarrollo; por ejemplo, para registrar mensajes del TRACE para un servicio específico en un archivo de registro específico.
* Estas configuraciones son útiles en un entorno de producción; por ejemplo, para tener mensajes sobre un servicio específico registrados en un archivo de registro individual para facilitar la monitorización.

Consulte [AEM Registro de](/help/sites-deploying/configure-logging.md) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Servlet principal de Apache Sling** Configurar:

* **Número de llamadas por solicitud** y **Profundidad de recursión** para proteger su sistema contra la recursión infinita y las llamadas excesivas a secuencias de comandos.

**Servicio de tipo MIME de Apache Sling** Configurar:

* **Tipos MIME** para agregar al sistema los tipos requeridos por el proyecto. Al hacerlo, se permite `GET` Solicitud en un archivo para establecer el encabezado de tipo de contenido correcto para vincular el tipo de archivo y la aplicación.

**Filtro de referente de Apache Sling** Para solucionar problemas de seguridad conocidos con la falsificación de solicitudes entre sitios (CSRF) en CRX WebDAV y Apache Sling, debe configurar el filtro Referente.

El servicio de filtro de referente es un servicio OSGi que le permite configurar lo siguiente:

* qué métodos http se deben filtrar
* si se permite un encabezado de referente vacío
* y una lista de servidores que se permitirán además del host de servidor.

Consulte la [Lista de comprobación de seguridad - Problemas con la falsificación de solicitudes entre sitios](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obtener más información.

>[!NOTE]
>
>El filtro de referente de Apache Sling depende de la instalación de un paquete de correcciones rápidas.

**Registrador de solicitudes de Apache Sling** Configurar:

* varios parámetros para definir cómo se registran las solicitudes.
* **Activar registro de solicitudes**, para habilitar o deshabilitar.

* **Activar registro de acceso**, para habilitar o deshabilitar.

Junto con el [Registrador de datos de solicitud personalizable de Apache Sling](#apacheslingcustomizablerequestdatalogger).

Consulte [AEM Registro de](/help/sites-deploying/configure-logging.md) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling Resource Resolver Factory** Configure los aspectos centrales de la resolución de recursos de Sling:

* **Rutas de búsqueda de recursos**, agregue cualquier ruta específica del proyecto (pero no elimine `/libs` o `/apps`).

* **URL virtuales** para definir las asignaciones de URL personalizadas.

* **Asignaciones de URL** para definir alias. Por ejemplo, desde `/content` hasta `/`.

* **Ubicación de asignación**, la configuración del asignador externalizada en `/etc/map`.

* Utilice su instalación local (por ejemplo, use `https://localhost:4502/system/console/jcrresolver`) para determinar qué Resource Resolver está activo.

Consulte: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>Configure estas opciones en el repositorio.
>
>De lo contrario, se realizarán cambios en **Asignaciones de URL** AEM El uso de la consola Felix puede ser sobrescrito por los que se utilizan en el siguiente inicio de la aplicación de.

**Apache Sling Servlet/Script Resolver y controlador de errores** Sling Servlet y Script Resolver tienen varias tareas:

1. Se utiliza como. `ServletResolver` para seleccionar el servlet o el script al que llamar para administrar la solicitud.

1. Actúa como el `SlingScriptResolver`.

1. Administra la gestión de errores implementando el `ErrorHandler` interfaz que utiliza el mismo algoritmo para seleccionar los servlets y scripts de gestión de errores que se utiliza para resolver los servlets y scripts de procesamiento de solicitudes.

Se pueden configurar varios parámetros, entre ellos:

* **Rutas de ejecución** - Enumera las rutas para buscar scripts ejecutables. Al configurar rutas específicas, puede limitar qué scripts se pueden ejecutar. Si no se configura ninguna ruta, se utiliza el valor predeterminado ( `/` = root), permitiendo la ejecución de todos los scripts.
Si un valor de ruta configurado termina con una barra diagonal, se busca en todo el subárbol. Sin esta barra diagonal, la secuencia de comandos solo se ejecuta si coincide exactamente.

* **Usuario de script** : esta propiedad opcional puede especificar la cuenta de usuario del repositorio utilizada para leer los scripts. Si no se especifica ninguna cuenta, la variable `admin` user se utiliza de forma predeterminada.

* **Extensiones predeterminadas** : La lista de extensiones para las que se utiliza el comportamiento predeterminado. El último segmento de ruta del tipo de recurso se puede utilizar como nombre de script.

**Configuración proxy de componentes HTTP de Apache** - La configuración proxy para todo el código que utiliza el cliente HTTP de Apache, utilizado cuando se realiza un HTTP. Por ejemplo, en la replicación.

Al crear una configuración, no cambie la configuración de fábrica. En su lugar, cree una configuración de fábrica para este componente con el administrador de configuración disponible aquí: **https://localhost:4502/system/console/configMgr/**. La configuración proxy está disponible en **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>AEM En la versión 6.0 y versiones anteriores, el proxy se configuraba en el cliente HTTP de Day Commons. AEM A partir de la versión 6.1 y versiones posteriores de, la configuración proxy se ha trasladado a la &quot;Configuración proxy de componentes HTTP Apache&quot; en lugar de a la configuración &quot;Cliente HTTP Day Commons&quot;.

**Day CQ Antispam** Configure el servicio antispam (Akismet) utilizado. Esta función requiere que registre lo siguiente:

* **Proveedor**
* **Clave de API**
* **URL registrada**

**Administrador de bibliotecas de Adobe Granite HTML** Configure para controlar la administración de bibliotecas de cliente (css o js), incluido, por ejemplo, cómo se ve la estructura subyacente.

* Para instancias de producción:

   * habilitar **Minificar** (para eliminar los caracteres CRLF y espacios en blanco).
   * habilitar **Gzip** (para permitir que se compriman los archivos y se acceda a ellos con una solicitud).
   * disable **Depurar**
   * disable **Programación**

* Para el desarrollo de JS (especialmente cuando se activa la depuración/depuración):

   * disable **Minificar**
   * habilitar **Depurar** para separar los archivos para la depuración y utilizarlos con fire bug.
   * habilitar **Programación** si está interesado en el momento.
   * habilitar **Depurar** para ver los mensajes de registro de la consola JS.

>[!CAUTION]
>
>Al cambiar la configuración de **Minificar** o **Gzip**, elimine el contenido de la caché de clientlibs. Consulte [Artículo de Knowledge Base](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html?lang=es) para obtener más información.

>[!NOTE]
>
>AEM Esta configuración se configura automáticamente para las instancias de producción si ejecuta en el [Modo Producción lista](/help/sites-administering/production-ready.md).

**Controlador de autenticación de encabezado HTTP CQ de día** Configuración de todo el sistema para el método de autenticación básico de la solicitud HTTP.

Al utilizar [grupos de usuarios cerrados](/help/sites-administering/cug.md), puede configurar, entre otras, las siguientes opciones:

* **Dominio HTTP**
* El **Página de inicio de sesión predeterminada**

**Servicio Day CQ Link Checker** Marque y, si es necesario, configure:

* **Período del programador** para definir el intervalo con el que se deben comprobar automáticamente los vínculos externos.

* Marque **Intervalo de tolerancia de vínculo incorrecto** para el periodo tras el cual un vínculo externo que no ha tenido éxito se considera incorrecto.
* **Patrones de anulación de verificación de vínculos**, para definir las rutas que se excluirán de la comprobación de vínculos.

**Tarea del verificador de vínculos CQ diarios** Configure las opciones de una sola tarea del verificador de vínculos (una tarea que comprueba un vínculo externo):

* Compruebe los intervalos definidos en **Intervalo de prueba de vínculo correcto** y **Intervalo de prueba de vínculo incorrecto**

* Los distintos parámetros relacionados con los proxies para el acceso a Internet y NTLM que son necesarios para el acceso externo al comprobar un vínculo.

**Day CQ Mail Service** Configure el nombre de host y los detalles de acceso para el servidor de correo. Consulte la sección Configuración del servicio de correo.

**Newsletter de CQ MCM del día** Configure las distintas opciones utilizadas con la newsletter.

**Asignación de raíz de CQ de día** Configurar:

* **Ruta de destino** para definir dónde desea enviar una solicitud a `/`&quot; se redirige a.

AEM Hay dos interfaces de usuario disponibles en la:

* la IU táctil es la IU estándar
* y la IU clásica obsoleta sigue funcionando por completo

AEM Con la asignación de raíz puede configurar la interfaz de usuario que desea tener como predeterminada para su instancia:

* Para que la IU táctil sea la IU predeterminada, la variable **Ruta de destino** debe señalar lo siguiente:

  ```shell
     /projects.html
  ```

* Para que la IU clásica sea la IU predeterminada, la variable **Ruta de destino** debe señalar lo siguiente:

  ```shell
     /welcome.html
  ```

>[!NOTE]
>
>En una instalación estándar, la IU táctil optimizada es la IU predeterminada.

**Controlador de autenticación SSO de Adobe Granite** : configure los detalles de SSO (inicio de sesión único). Estos detalles suelen ser necesarios en configuraciones de creación empresariales, a menudo con LDAP.

Hay varias propiedades de configuración disponibles:

* **Ruta**
Ruta de acceso para la que está activo este controlador de autenticación. Si este parámetro se deja vacío, el controlador de autenticación se desactiva. Por ejemplo, la ruta / hace que el controlador de autenticación se utilice para todo el repositorio.

* **Clasificación de servicios**
El valor de clasificación del servicio marco OSGi se utiliza para indicar el orden utilizado para llamar a este servicio. Este valor es un `int` valor en el que los valores más altos designan una prioridad mayor.
El valor predeterminado es `0`.

* **Nombres de encabezado**
Nombres de encabezados que pueden contener un ID de usuario.

* **Nombres de cookies**
Nombres de cookies que podrían contener un ID de usuario.

* **Nombres de parámetros**
Nombres de los parámetros de solicitud que pueden proporcionar el ID de usuario.

* **Mapa del usuario**
Para los usuarios seleccionados, el nombre de usuario extraído de la solicitud HTTP se puede reemplazar por uno diferente en el objeto de credenciales. La asignación se define aquí. Si el nombre de usuario `admin` aparece a ambos lados del mapa y se ignora la asignación. El carácter &quot;=&quot; debe tener un carácter de escape &quot;\&quot; inicial.

* **Formato**
Indica el formato en el que se proporciona el ID de usuario. Uso:

   * `Basic` si el ID de usuario está codificado en el formato de autenticación HTTP Basic
   * `AsIs` si el ID de usuario se proporciona en texto sin formato o cualquier valor de expresión regular aplicado debe utilizarse tal cual o cualquier expresión regular

**Filtro de depuración de CQ WCM por día** Esto resulta útil a la hora de desarrollar, ya que permite el uso de sufijos como ?debug=layout cuando se accede a una página. Por ejemplo, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout proporciona información de diseño que puede ser de interés para el desarrollador.

* Para garantizar el rendimiento y la seguridad, deshabilite en instancias de producción.

**Filtro de WCM de CQ de día** Configurar:

* **Modo WCM** para definir el modo predeterminado.
* En una instancia de autor, este modo puede ser `edit`, `disable,preview`, o `analytics`.
Se puede acceder a los demás modos desde la barra de tareas o el sufijo `?wcmmode=disabled` se puede utilizar para emular un entorno de producción.

* En una instancia de publicación, este modo debe configurarse como `disabled` para garantizar que no se pueda acceder a ningún otro modo.

>[!NOTE]
>
>AEM Esta configuración se configura automáticamente para las instancias de producción si ejecuta en el [Modo Producción lista](/help/sites-administering/production-ready.md).

**Configurador del verificador de vínculos de CQ WCM por día** Configurar:

* **Lista de configuraciones de reescritura** para especificar una lista de ubicaciones para las configuraciones del verificador de vínculos basado en contenido. Las configuraciones se pueden basar en el modo de ejecución. Este hecho es importante para distinguir entre los entornos de creación y publicación, ya que la configuración del verificador de vínculos puede diferir.

**Day CQ WCM Page Manager Factory** Configurar:

* **Comprobación de activación del subárbol de página** para que un usuario (sin permisos de replicación) elimine o mueva páginas (incluso si las páginas no están activadas).

**Procesador de páginas WCM CQ por día** Configurar:

* **Rutas**, una lista de ubicaciones en la que el sistema escucha las modificaciones de la página antes de activar un `jcr:Event`.

**Rastreador de impresiones de página de Adobe** Para una instancia de autor, configure como se indica a continuación:

* **sling.auth.requirements**: establezca el valor de esta propiedad en `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Esta configuración permite solicitudes anónimas al servicio de seguimiento.

>[!NOTE]
>
>Consulte [Impresiones de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obtener más información.

**Estadísticas de página de CQ WCM de día** Para una instancia de publicación, configure:

* **URL para enviar datos** para configurar la dirección URL utilizada para rastrear estadísticas de página (es vital si una solicitud de seguimiento pasa a través de Dispatcher); por ejemplo, la dirección URL predeterminada es `https://localhost:4502/libs/wcm/stats/tracker`.

* **Script de seguimiento habilitado** para habilitar ( `true`) o deshabilite ( `false`) la inclusión de la secuencia de comandos de seguimiento en las páginas. El valor predeterminado es `false`.

>[!NOTE]
>
>Consulte [Impresiones de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obtener más información.

**Administrador de versiones de CQ WCM de día** Controle si las versiones se administran en el sistema y cómo:

* **Crear versión al activar**, habilitado en una instalación estándar
* **Activar depuración**

* **Purgar rutas**, las rutas que busca una acción de búsqueda.
* **Rutas de versiones implícitas**, las rutas en las que está activo el control de versiones implícito.

* **Edad máxima de la versión**, la edad máxima (en días) de una versión

* **Número máximo de versiones**, el número máximo de versiones que se deben mantener

Consulte [Depuración de versiones](/help/sites-deploying/version-purging.md) para obtener más información.

**Servicio de notificación por correo electrónico del flujo de trabajo CQ diario** Configure las opciones de correo electrónico para las notificaciones enviadas por un flujo de trabajo.

**HTML de reescritura CQ fábrica de analizador**

Controla el analizador de HTML para la reescritura CQ.

* **Etiquetas adicionales para procesar** : puede añadir o quitar etiquetas de HTML para que las procese el analizador. De forma predeterminada, se procesan las siguientes etiquetas: A, IMG, AREA, FORM, BASE, LINK, SCRIPT, BODY, HEAD.
* **Conservar mayúsculas y minúsculas** - De forma predeterminada, el analizador HTML convierte los atributos en minúscula (por ejemplo, `eBay`) a minúsculas (por ejemplo, `ebay`). Puede desactivar esta configuración para conservar los atributos de mayúsculas y minúsculas. Esta configuración es útil cuando se utilizan marcos de front-end como Angular 2.

**Grupo de conexiones JDBC de Day Commons** Configure el acceso a una base de datos externa que se esté utilizando como origen de contenido.

Una configuración de fábrica, para que se puedan configurar varias instancias.

**Reescritura CDN** AEM Debe garantizarse la comunicación entre los recursos y una red de distribución de contenido (CDN) para que los recursos o binarios se entreguen a un usuario final de forma segura. Este proceso implica las dos tareas siguientes:

* AEM Acceder al recurso desde la red de distribución de contenido (CDN) desde la primera vez (o después de que caducara en la caché) a través de la red de distribución de contenido (CDN).
* Acceder a los recursos almacenados en caché en CDN de forma segura. AEM Una vez que el recurso se almacena en caché en CDN, la solicitud no se envía a CDN y todos los usuarios que tengan acceso a ese recurso en deben recibir servicios desde CDN.

AEM proporciona un reescritor para reescribir las URL de los recursos internos en URL de CDN externas. Reescribe los vínculos para pasarlos a la CDN, incluida una firma JWS y el tiempo de caducidad para permitir que el recurso se acceda de forma segura. Esta función se debe utilizar en instancias de autor.

El flujo total es el siguiente:

1. AEM El usuario se autentica con los recursos y solicita una página con ellos.
1. La página solicitada contiene un recurso similar a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. Rewriter transforma el vínculo en una URL de CDN que contiene una firma JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. A continuación, el explorador del usuario reenvía la solicitud de recurso al servidor CDN
1. AEM CDN debe configurarse para reenviar la solicitud a la red de distribución de contenido (CDN) junto con la red de distribución de contenido (CDN) de la red de `cdn_sign` parámetro.
1. Un controlador de autenticación valida el `cdn_sign` y devuelve el recurso a CDN, que luego se entrega al usuario

AEM El flujo entre el explorador del usuario, la red de distribución de contenido (CDN) y la red de distribución de contenido () se puede visualizar de la siguiente manera.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>AEM Esta función solo está habilitada para instancias de autor de.

**CDNConfigServiceImpl** Proporciona configuraciones de CDN

La función de reescritura de CDN se puede habilitar proporcionando lo siguiente **Nombre de dominio de distribución CDN** en la configuración de com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

El servicio también contiene otras opciones de configuración como habilitar/deshabilitar la reescritura de CDN, prefijos de ruta para los que se realiza la reescritura de CDN, valores TTL y protocolo (HTTP o HTTPS).

**CDNRewriter** Un reescritor para reescribir URL de imagen interna en URL de CDN

El **Atributos de etiqueta** El valor de com.adobe.cq.cdn.rewriter.impl.CDNRewriter se puede definir para que solo se reescriban los vínculos de imagen selectivos.
