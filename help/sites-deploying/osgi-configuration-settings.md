---
title: Ajustes de configuración de OSGi
seo-title: OSGi Configuration Settings
description: Este artículo detalla los ajustes de configuración de OSGi (enumerados según el paquete) que son relevantes para la implementación del proyecto. La lista actúa como directriz y no es exhaustiva.
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
source-git-commit: d3923e5e693e7426ee57e81e203f31964a23af3a
workflow-type: tm+mt
source-wordcount: '3430'
ht-degree: 0%

---

# Ajustes de configuración de OSGi{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) es un elemento fundamental de la pila tecnológica de AEM. Se utiliza para controlar los paquetes compuestos de AEM y su configuración.

OSGi &quot;*proporciona los primitivos estandarizados que permiten construir aplicaciones a partir de componentes pequeños, reutilizables y colaborativos. Estos componentes se pueden componer en una aplicación e implementar*&quot;.

Esta funcionalidad permite administrar fácilmente los paquetes, ya que se pueden detener, instalar e iniciar individualmente. Las interdependencias se gestionan automáticamente. Cada componente OSGi (consulte la [Especificación de OSGi](https://docs.osgi.org/specification/)) está contenido en uno de los distintos paquetes. Al trabajar con AEM, existen varios métodos para administrar los ajustes de configuración de estos paquetes; see [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

Los siguientes ajustes de configuración de OSGi (enumerados según el paquete) son relevantes para la implementación del proyecto. No es necesario ajustar todos los ajustes de la lista, algunos de ellos se mencionan para ayudarle a comprender el funcionamiento de AEM.

>[!CAUTION]
>
>La lista tiene por objeto servir de guía y no es exhaustiva. No se enumeran todos los paquetes, ni todos los parámetros de algunos de los paquetes que sí.
>
>La configuración necesaria varía de un proyecto a otro.
>
>Consulte la consola web para ver los valores utilizados y la información detallada sobre los parámetros.

>[!NOTE]
>
>La herramienta OSGi Configuration Diff (diferencia de configuración de OSGi), que forma parte de la [Herramientas AEM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17488.html?lang=en), se puede usar para listar las configuraciones predeterminadas de OSGi.

>[!NOTE]
>
>Es posible que se requieran más paquetes para áreas específicas de funcionalidad dentro de AEM. En estos casos, los detalles de configuración se pueden encontrar en la página relacionada con la funcionalidad adecuada.

**Detector de eventos de replicación de AEM** Configurar:

* La variable **Modos de ejecución**, en la que los eventos de replicación se distribuyen a los oyentes. Por ejemplo, si se define como autor, es el sistema el que &quot;inicia&quot; la replicación.

* Añadir el modo de ejecución **publicar** si el código del proyecto procesa eventos de replicación (replicación inversa) en un entorno de publicación. Por ejemplo, cuando se utiliza Dispatcher para vaciar del entorno de publicación o cuando se produce la replicación estándar a otras instancias de publicación.

**Agente de cambio del repositorio AEM** Configurar:

* La variable **Rutas**, ubicaciones para escuchar eventos de repositorio listos para su distribución.

**Repositorio de cliente CRX Sling** Configure el acceso al repositorio de contenido subyacente.

* La variable **Contraseña de administrador** debe cambiarse después de la instalación para garantizar que [seguridad](/help/sites-administering/security-checklist.md) de su instancia.
* No deben ser necesarios otros cambios y se debe tener cuidado, ya que pueden afectar al acceso al repositorio.

**Consola de administración Apache Felix OSGi** Configurar:

* **Complementos**, los elementos de navegación principales (complementos de consola) que estarán disponibles en la **Consola de administración web Apache Felix** como elementos de menú de nivel superior. Deshabilite los que no necesite, ya que cada uno requiere espacio y recursos.

>[!CAUTION]
>
>Asegúrese de configurar lo siguiente:
>
>**Nombre de usuario** y **Contraseña**, las credenciales para acceder a la consola de gestión web Apache Felix.
>La contraseña debe cambiarse después de la instalación inicial para garantizar que [seguridad](/help/sites-administering/security-checklist.md) de su instancia.

>[!NOTE]
>
>Esta configuración debe realizarse utilizando la Consola Felix tal como es necesaria al inicio - antes de que el repositorio esté disponible.

**Registrador de datos de solicitud personalizable de Apache Sling** Configurar:

* **Nombre del registrador** y **Formato de registro** para configurar la ubicación y el formato del registro de solicitud y acceso (predeterminado: `request.log`). Este archivo de registro es esencial para analizar el rendimiento o la funcionalidad de depuración relacionada con la cadena web. Está emparejado con la variable [Registrador de solicitudes de Apache Sling](#apacheslingrequestlogger).

Consulte [Registro de AEM](/help/sites-deploying/configure-logging.md) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Grupo de subprocesos de eventos de Apache Sling** Configurar:

* **Tamaño mínimo del grupo** y **Tamaño máximo del grupo**, el tamaño del grupo utilizado para mantener los subprocesos de evento.

* **Tamaño de cola**, el tamaño máximo de la cola de subprocesos si se agota el grupo.
El valor recomendado es `-1` porque establece la cola en ilimitada. Si se establece un límite, pueden producirse pérdidas cuando se supera.

* Cambiar esta configuración puede ayudar al rendimiento en escenarios con un número elevado de eventos. Por ejemplo, uso intensivo AEM DAM o Workflow.
* Los valores específicos de su escenario deben establecerse mediante pruebas.
* Estos ajustes pueden afectar al rendimiento de la instancia, por lo que no los cambie sin motivo y teniendo debidamente en cuenta.

**Servlet de GET Apache Sling** Configure algunos aspectos de la renderización:

* **Índice automático** para habilitar/deshabilitar la renderización de directorios para la exploración.
* **Habilitar** (o deshabilite) las representaciones predeterminadas, como **HTML**, **Texto sin formato**, **JSON** o **XML**.
No deshabilite JSON.

>[!NOTE]
>
>Esta configuración se configura automáticamente para instancias de producción si ejecuta AEM en [Modo listo para la producción](/help/sites-administering/production-ready.md).

**Controlador JavaScript de Apache Sling** Configure las opciones para la compilación de archivos .java como secuencias de comandos (servlets).

Ciertos ajustes pueden afectar al rendimiento. Deshabilite estos ajustes siempre que sea posible, especialmente para una instancia de producción.

* **VM de origen** y **VM de destino**, defina la versión de JDK que se utiliza como JVM de tiempo de ejecución

* para instancias de producción:

   * disable **Generar información de depuración**

**Instalador JCR de Apache Sling** Estos parámetros probablemente no necesitan configuración, pero pueden resultar útiles para saberlo al desarrollar o depurar. Por ejemplo, las carpetas de instalación pueden ser útiles para desproteger o desproteger, o para crear un paquete.

* **Carpeta de instalación regexp** y **Profundidad máxima de jerarquía de las carpetas de instalación** - especifique dónde y a qué profundidad se buscan las carpetas del repositorio para los recursos que se van a instalar. Cuando se utiliza un comodín (como en .&#42;/install) se buscan todas las coincidencias adecuadas, por ejemplo, `/libs/sling/install` y `/libs/cq/core/install`.

* **Ruta de búsqueda**, lista de rutas que jcrinstall busca los recursos que se van a instalar, junto con un número que indica el factor de ponderación para esa ruta.

**Controlador de eventos de trabajo Apache Sling** Configure los parámetros que administran la programación de trabajos:

* **Intervalo de reintento**, **Reintentos máximos**, **Trabajos paralelos máximos**, **Tiempo de espera de confirmación**, entre otros.

* Cambiar esta configuración puede mejorar el rendimiento en escenarios con un número elevado de trabajos; por ejemplo, un uso intensivo de AEM DAM y flujos de trabajo.
* Los valores específicos de su escenario deben establecerse mediante pruebas.
* No cambie esta configuración sin motivo, solo cambie después de tener en cuenta.

**Controlador de scripts JSP de Apache Sling** Configure las opciones relevantes de rendimiento para el controlador de scripts JSP. Para mejorar el rendimiento, debe deshabilitar tanto como sea posible.

En particular para las instancias de producción:

* disable **Generar información de depuración**
* disable **Mantener Java™ generado**
* disable **Contenido asignado**
* disable **Mostrar fragmentos de origen**

>[!NOTE]
>
>Esta configuración se configura automáticamente para instancias de producción si ejecuta AEM en [Modo listo para la producción](/help/sites-administering/production-ready.md).

**Configuración de registro de Apache Sling** Configurar:

* **Nivel de registro** y **Archivo de registro**, para definir la ubicación y el nivel de registro de la configuración de registro central (error.log). El nivel se puede establecer en uno de los `DEBUG`, `INFO`, `WARN`, `ERROR`y `FATAL`.

* **Número de archivos de registro** y **Umbral del archivo de registro** para definir el tamaño y la rotación de la versión del archivo de registro.

* **Patrón de mensaje** define el formato de los mensajes de registro.

Consulte [Registro de AEM](/help/sites-deploying/configure-logging.md#global-logging) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Configuración del registrador de Apache Sling (configuración de fábrica)** Configurar:

* **Nivel de registro**, **Archivo de registro** y **Formato del mensaje** para definir los detalles del archivo de registro y los mensajes.

* **Registrador** para definir la categoría; por ejemplo, solo registre para com.day.cq.

* Usando **Configuraciones de fábrica**, se puede agregar cualquier cantidad de configuraciones adicionales para satisfacer los distintos niveles de registro y categorías necesarios.
* Estas configuraciones son útiles durante el desarrollo; por ejemplo, para registrar mensajes de TRACE para un servicio específico en un archivo de registro específico.
* Estas configuraciones son útiles en un entorno de producción; por ejemplo, para que los mensajes sobre un servicio específico se registren en un archivo de registro individual para facilitar la monitorización.

Consulte [Registro de AEM](/help/sites-deploying/configure-logging.md) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Configuración de Apache Sling Logging Writer (Configuración de fábrica)** Configurar:

* **Archivo de registro** para definir la existencia de un archivo de registro.
* **Número de archivos de registro** para definir la rotación de la versión.

* El escritor puede ser utilizado por un **Configuración del registrador de Apache Sling** configuración.

* Estas configuraciones son útiles durante el desarrollo; por ejemplo, para registrar mensajes de TRACE para un servicio específico en un archivo de registro específico.
* Estas configuraciones son útiles en un entorno de producción; por ejemplo, para que los mensajes sobre un servicio específico se registren en un archivo de registro individual para facilitar la monitorización.

Consulte [Registro de AEM](/help/sites-deploying/configure-logging.md) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Servlet principal de Apache Sling** Configurar:

* **Número de llamadas por solicitud** y **Profundidad de recursividad** para proteger su sistema contra recursiones infinitas y llamadas de script excesivas.

**Servicio de tipo MIME de Apache Sling** Configurar:

* **Tipos MIME** para agregar al sistema los tipos requeridos por el proyecto. Al hacerlo, se permite un `GET` solicite en un archivo que configure el encabezado de tipo de contenido correcto para vincular el tipo de archivo y la aplicación.

**Filtro de referente de Apache Sling** Para solucionar problemas de seguridad conocidos con Falsificación de solicitudes entre sitios (CSRF) en CRX WebDAV y Apache Sling, debe configurar el filtro Referente .

El servicio de filtro de referente es un servicio OSGi que le permite configurar:

* qué métodos http deben filtrarse
* si se permite un encabezado de referente vacío
* y una lista de servidores a permitir además del host del servidor.

Consulte la [Lista de comprobación de seguridad: problemas con la falsificación de solicitudes entre sitios](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obtener más información.

>[!NOTE]
>
>El filtro de referente de Apache Sling depende de la instalación de un paquete de correcciones rápidas.

**Registrador de solicitudes de Apache Sling** Configurar:

* varios parámetros para definir cómo se registran las solicitudes.
* **Habilitar registro de solicitud**, para habilitar o deshabilitar.

* **Habilitar registro de acceso**, para habilitar o deshabilitar.

Emparejado con [Registrador de datos de solicitud personalizable de Apache Sling](#apacheslingcustomizablerequestdatalogger).

Consulte [Registro de AEM](/help/sites-deploying/configure-logging.md) y [Registro de Sling](https://sling.apache.org/documentation/development/logging.html).

**Fábrica de resolución de recursos de Apache Sling** Configure aspectos centrales de la resolución de recursos de Sling:

* **Rutas de búsqueda de recursos**, agregue cualquier ruta específica del proyecto (pero no elimine `/libs` o `/apps`).

* **URL virtuales** para definir las asignaciones de URL de vanidad.

* **Asignaciones de URL** para definir cualquier alias. Por ejemplo, desde `/content` a `/`.

* **Ubicación de asignación**, la configuración del asignador externalizada en `/etc/map`.

* Utilice la instalación local (por ejemplo, use `https://localhost:4502/system/console/jcrresolver`) para determinar qué Resource Resolver está activo.

Consulte: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>Configure estas opciones en el repositorio.
>
>De lo contrario, los cambios realizados en **Asignaciones de URL** el uso de la consola Felix puede ser sobrescrito por AEM en el siguiente inicio.

**Apache Sling Servlet/Script Resolver y Gestor de errores** El Servlet de Sling y el Resoltor de secuencias de comandos tienen varias tareas:

1. Se usa como el `ServletResolver` para seleccionar el servlet o el script al que llamar para gestionar la solicitud.

1. Actúa como el `SlingScriptResolver`.

1. Gestiona la gestión de errores implementando la variable `ErrorHandler` utilizando el mismo algoritmo para seleccionar servlets y secuencias de comandos de gestión de errores que se utiliza para resolver servlets y secuencias de comandos de procesamiento de solicitudes.

Se pueden configurar varios parámetros, entre ellos:

* **Rutas de ejecución** - Enumera las rutas para buscar scripts ejecutables. Al configurar rutas específicas, puede limitar qué secuencias de comandos se pueden ejecutar. Si no hay ninguna ruta configurada, se usa la ruta predeterminada ( `/` = root), permitiendo la ejecución de todas las secuencias de comandos.
Si un valor de ruta configurado termina con una barra diagonal, se buscará en todo el subárbol. Sin una barra diagonal así, el script solo se ejecuta si es una coincidencia exacta.

* **Usuario de secuencia de comandos** - Esta propiedad opcional puede especificar la cuenta de usuario del repositorio utilizada para leer los scripts. Si no se especifica ninguna cuenta, la variable `admin` se utiliza de forma predeterminada.

* **Extensiones predeterminadas** - La lista de extensiones para la que se utiliza el comportamiento predeterminado. El último segmento de ruta del tipo de recurso se puede usar como nombre de secuencia de comandos.

**Configuración proxy de componentes HTTP de Apache** - La configuración proxy para todo el código que utiliza el cliente HTTP de Apache, utilizado cuando se realiza un HTTP. Por ejemplo, en la replicación.

Al crear una configuración, no cambie la configuración de fábrica. En su lugar, cree una configuración de fábrica para este componente mediante el administrador de configuración disponible aquí: **https://localhost:4502/system/console/configMgr/**. La configuración del proxy está disponible en **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>En AEM versión 6.0 y anteriores, el proxy se configuró en Day Commons HTTP Client. A partir de AEM versión 6.1 y posteriores, la configuración de proxy se ha trasladado a la &quot;Configuración proxy de componentes HTTP Apache&quot; en lugar de la configuración &quot;Cliente HTTP Day Commons&quot;.

**Antispam CQ Day** Configure el servicio antispam (Akismet) utilizado. Esta función requiere que registre lo siguiente:

* **Proveedor**
* **Clave de API**
* **URL registrada**

**Administrador de biblioteca de HTML de Adobe Granite** Configure para controlar la administración de las bibliotecas de cliente (css o js), incluido, por ejemplo, cómo se ve la estructura subyacente.

* Para instancias de producción:

   * enable **Minificar** (para eliminar los caracteres CRLF y los espacios en blanco).
   * enable **Gzip** (para permitir que se comprueben los archivos y se acceda a ellos con una solicitud).
   * disable **Depuración**
   * disable **Temporización**

* Para el desarrollo de JS (especialmente cuando se crea o depura):

   * disable **Minificar**
   * enable **Depuración** para separar los archivos para la depuración y usarlos con el error de activación.
   * enable **Temporización** si está interesado en el tiempo.
   * enable **Depuración** para ver los mensajes de registro de la consola JS.

>[!CAUTION]
>
>Al cambiar la configuración para **Minificar** o **Gzip**, elimine el contenido de la caché clientlibs. Consulte [Artículo de la base de conocimiento](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html?lang=en) para obtener más información.

>[!NOTE]
>
>Esta configuración se configura automáticamente para instancias de producción si ejecuta AEM en [Modo listo para la producción](/help/sites-administering/production-ready.md).

**Controlador de autenticación de encabezado HTTP Day CQ** Configuración de todo el sistema para el método de autenticación básico de la solicitud HTTP.

Al usar [grupos de usuarios cerrados](/help/sites-administering/cug.md), puede configurar, entre otros, lo siguiente:

* **Dominio HTTP**
* La variable **Página de inicio de sesión predeterminada**

**Servicio Day CQ Link Checker** Marque y, si es necesario, configure:

* **Período del planificador** para definir el intervalo en el que se comprueban automáticamente los vínculos externos.

* Marque **Intervalo de tolerancia de vínculo incorrecto** para el periodo después del cual un vínculo externo fallido se considera malo.
* **Patrones de anulación de comprobación de enlace**, para definir las rutas que se excluirán de la comprobación de vínculos.

**Tarea del verificador de vínculos de CQ de día** Configure las opciones de una tarea de verificación de vínculos únicos (una tarea que comprueba un vínculo externo):

* Compruebe los intervalos definidos en **Intervalo de prueba de vínculo correcto** y **Intervalo de prueba de vínculo incorrecto**

* Los distintos parámetros relacionados con los proxies para acceso a Internet y NTLM necesarios para acceso externo al comprobar un vínculo.

**Day CQ Mail Service** Configure el nombre de host y los detalles de acceso para el servidor de correo. Consulte la sección Configuración del servicio de correo .

**Newsletter de Day CQ MCM** Configure los distintos ajustes utilizados con la newsletter.

**Asignación de raíz de CQ de día** Configurar:

* **Ruta de destino** para definir dónde una solicitud a `/`&quot; se redirige a.

Hay dos IU disponibles en AEM:

* la IU táctil es la IU estándar
* y la IU clásica obsoleta sigue funcionando completamente

Con AEM asignación raíz puede configurar la IU que desea tener como predeterminada para su instancia:

* Para que la IU táctil sea la IU predeterminada, la variable **Ruta de destino** debe señalar lo siguiente:

   ```shell
      /projects.html
   ```

* Para que la IU clásica sea la predeterminada, la variable **Ruta de destino** debe señalar lo siguiente:

   ```shell
      /welcome.html
   ```

>[!NOTE]
>
>En una instalación estándar, la IU táctil es la IU predeterminada.

**Controlador de autenticación SSO de Granite de Adobe** - Configurar los detalles de SSO (inicio de sesión único). Estos detalles suelen ser necesarios en configuraciones de autor empresariales, a menudo con LDAP.

Hay varias propiedades de configuración disponibles:

* **Ruta**
La ruta de acceso para la que está activo este controlador de autenticación. Si este parámetro se deja vacío, el controlador de autenticación se desactiva. Por ejemplo, la ruta / hace que el controlador de autenticación se utilice para todo el repositorio.

* **Clasificación de servicios**
El valor de Clasificación del servicio de OSGi Framework se utiliza para indicar el orden utilizado para llamar a este servicio. Este valor es un 
`int` donde los valores más altos designan mayor prioridad.
El valor predeterminado es `0`.

* **Nombres de encabezado**
Nombres de encabezados que pueden contener un ID de usuario.

* **Nombres de cookies**
Los nombres de las cookies que pueden contener un ID de usuario.

* **Nombres de parámetros**
Los nombres de los parámetros de solicitud que pueden proporcionar el ID de usuario.

* **Mapa del usuario**
Para los usuarios seleccionados, el nombre de usuario extraído de la solicitud HTTP se puede reemplazar por uno diferente en el objeto credentials . La asignación se define aquí. Si el nombre de usuario 
`admin` aparece a ambos lados del mapa, se ignora la asignación. El carácter &quot;=&quot; debe omitirse con un signo &quot;\&quot; inicial.

* **Formato**
Indica el formato en el que se proporciona el ID de usuario. Uso:

   * `Basic` si el ID de usuario está codificado en el formato de autenticación básica HTTP
   * `AsIs` si el ID de usuario se proporciona en formato de texto sin formato o cualquier valor aplicado de expresión regular debe usarse tal cual o cualquier expresión regular

**Filtro de depuración Day CQ WCM** Esto resulta útil cuando se desarrolla, ya que permite el uso de sufijos como ?debug=layout al acceder a una página. Por ejemplo, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout proporciona información de diseño que puede ser de interés para el desarrollador.

* Para garantizar el rendimiento y la seguridad, deshabilite en las instancias de producción.

**Filtro WCM Day CQ** Configurar:

* **Modo WCM** para definir el modo predeterminado.
* En una instancia de autor, este modo puede ser `edit`, `disable,preview`o `analytics`.
Se puede acceder a los demás modos desde la barra de tareas o desde el sufijo `?wcmmode=disabled` se puede utilizar para emular un entorno de producción.

* En una instancia de publicación, este modo debe estar definido como `disabled` para garantizar que no se pueda acceder a ningún otro modo.

>[!NOTE]
>
>Esta configuración se configura automáticamente para instancias de producción si ejecuta AEM en [Modo listo para la producción](/help/sites-administering/production-ready.md).

**Configurador del verificador de vínculos de CQ WCM Day** Configurar:

* **Lista de configuraciones de reescritura** para especificar una lista de ubicaciones para las configuraciones del verificador de vínculos basadas en contenido. Las configuraciones se pueden basar en el modo de ejecución. Este hecho es importante para distinguir entre los entornos de autor y publicación, ya que la configuración del verificador de vínculos puede diferir.

**Fábrica de administrador de páginas de CQ WCM Day** Configurar:

* **Comprobación de activación del subárbol de páginas** para que un usuario (sin permisos de replicación) elimine o mueva páginas (incluso si las páginas no están activadas).

**Procesador de páginas Day CQ WCM** Configurar:

* **Rutas**, una lista de ubicaciones en las que el sistema escucha las modificaciones de la página antes de activar un `jcr:Event`.

**Rastreador de impresiones de página de Adobe** Para una instancia de autor, configure como se indica a continuación:

* **sling.auth.requirements**: establezca el valor de esta propiedad en `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Esta configuración permite solicitudes anónimas al servicio de seguimiento.

>[!NOTE]
>
>Consulte [Impresiones de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obtener más información.

**Estadísticas de página de Day CQ WCM** Para una instancia de publicación, configure:

* **URL para enviar datos** para configurar la URL utilizada para rastrear las estadísticas de la página (es vital si una solicitud de rastreador pasa por Dispatcher); por ejemplo, el valor predeterminado es `https://localhost:4502/libs/wcm/stats/tracker`.

* **Script de seguimiento habilitado** para habilitar ( `true`) o deshabilitar ( `false`) la inclusión de la secuencia de comandos de seguimiento en las páginas. El valor predeterminado es `false`.

>[!NOTE]
>
>Consulte [Impresiones de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obtener más información.

**Day CQ WCM Version Manager** Controle si las versiones se administran en su sistema y cómo se administran:

* **Crear versión al activar**, habilitado en una instalación estándar
* **Habilitar depuración**

* **Purgar rutas**, las rutas que busca una acción de búsqueda.
* **Rutas de versiones implícitas**, las rutas en las que el control de versiones implícito está activo.

* **Edad máxima de la versión**, la edad máxima (en días) de una versión

* **Número máximo de versiones**, el número máximo de versiones que se van a mantener

Consulte [Depuración de versiones](/help/sites-deploying/version-purging.md) para obtener más información.

**Servicio de notificación de correo electrónico del flujo de trabajo CQ de día** Configure las opciones de correo electrónico para las notificaciones enviadas por un flujo de trabajo.

**CQ Rewriter HTML Parser Factory**

Controla el analizador de HTML para el reescritor de CQ.

* **Etiquetas adicionales para procesar** - Puede añadir o eliminar las etiquetas HTML que el analizador procesará. De forma predeterminada, se procesan las etiquetas siguientes: A,IMG,AREA,FORMULARIO,BASE,VÍNCULO,SECUENCIA DE COMANDOS,CUERPO,HEAD.
* **Preservar mayúsculas y minúsculas** - De forma predeterminada, el analizador de HTML convierte los atributos en mayúsculas y minúsculas (por ejemplo, `eBay`) a minúsculas (por ejemplo, `ebay`). Puede desactivar esta configuración para conservar los atributos de mayúsculas y minúsculas del camello. Esta configuración es útil cuando se utilizan marcos de front-end como Angular 2.

**Agrupamiento de conexiones JDBC Day Commons** Configure el acceso a una base de datos externa que se esté utilizando como fuente de contenido.

Una configuración de fábrica, de modo que se puedan configurar varias instancias.

**Reescritura de CDN** Se debe garantizar la comunicación entre AEM y una CDN para que los recursos y binarios se entreguen a un usuario final de forma segura. Este proceso incluye las dos tareas siguientes:

* Acceso al recurso desde AEM mediante la CDN por primera vez (o después de que caduque en la caché).
* Acceso seguro al recurso almacenado en caché en CDN. Una vez que el recurso se almacena en caché en CDN, la solicitud no se dirige a AEM y todos los usuarios que tienen acceso a ese recurso en deben proporcionarse desde CDN.

AEM proporciona un reescritor para reescribir las URL de recursos internos en direcciones URL de CDN externas. Reescribe los vínculos que se pasarán a la CDN, incluida una firma JWS y un tiempo de caducidad para permitir el acceso seguro al recurso. Esta función se utilizará en instancias de autor.

El flujo general es el siguiente:

1. El usuario se autentica con AEM y solicita una página con recursos.
1. La página solicitada contiene un recurso similar a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. Rewriter transforma el vínculo a una URL de CDN que contiene una firma JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. A continuación, el navegador del usuario reenvía la solicitud de recurso al servidor CDN
1. La CDN debe configurarse para reenviar la solicitud a AEM junto con la variable `cdn_sign` parámetro.
1. Un gestor de autenticación valida el `cdn_sign` y devuelve el recurso a CDN que luego se envía al usuario

El flujo entre el navegador del usuario, la CDN y la AEM se puede visualizar de la siguiente manera.

![Chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>Esta función solo está habilitada para AEM instancias de autor.

**CDNConfigServiceImpl** Proporciona configuraciones de CDN

La función de reescritura de CDN se puede habilitar proporcionando **Nombre de dominio de distribución CDN** en la configuración de com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

El servicio también contiene otras opciones de configuración como habilitar/deshabilitar la reescritura de CDN, prefijos de ruta para los que se realiza la reescritura de CDN, valores TTL y protocolo (HTTP o HTTPS).

**Teclado CDNR** Un reescritor para reescribir URL de imágenes internas en URL de CDN

La variable **Atributos de etiqueta** en com.adobe.cq.cdn.rewriter.impl.CDNRewriter se puede definir para que solo se reescriban los vínculos de imagen selectivos.
