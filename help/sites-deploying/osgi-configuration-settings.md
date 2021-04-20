---
title: Ajustes de configuración de OSGi
seo-title: Ajustes de configuración de OSGi
description: Este artículo detalla los ajustes de configuración de OSGi (enumerados según el paquete) que son relevantes para la implementación del proyecto. La lista actúa como directriz y no es exhaustiva.
seo-description: Este artículo detalla los ajustes de configuración de OSGi (enumerados según el paquete) que son relevantes para la implementación del proyecto. La lista actúa como directriz y no es exhaustiva.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3806'
ht-degree: 0%

---


# Configuración de OSGi{#osgi-configuration-settings}

[](https://www.osgi.org/) OSGies un elemento fundamental de la pila tecnológica de AEM. Se utiliza para controlar los paquetes compuestos de AEM y su configuración.

OSGi &quot;*proporciona los primitivos estandarizados que permiten construir aplicaciones a partir de componentes pequeños, reutilizables y colaborativos. Estos componentes se pueden componer en una aplicación e implementar*&quot;.

Esto permite una administración sencilla de los paquetes, ya que se pueden detener, instalar e iniciar individualmente. Las interdependencias se gestionan automáticamente. Cada componente OSGi (consulte la [Especificación OSGi](https://www.osgi.org/Specifications/HomePage)) está contenido en uno de los distintos paquetes. Al trabajar con AEM hay varios métodos para administrar los ajustes de configuración de estos paquetes; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

Los siguientes ajustes de configuración de OSGi (enumerados según el paquete) son relevantes para la implementación del proyecto. No es necesario ajustar todos los ajustes de la lista, algunos de ellos se mencionan para ayudarle a comprender el funcionamiento de AEM.

>[!CAUTION]
>
>La lista tiene por objeto servir de guía y no es exhaustiva. No se enumeran todos los paquetes, ni todos los parámetros de algunos de los paquetes que sí.
>
>La configuración necesaria variará de un proyecto a otro.
>
>Consulte la consola web para ver los valores utilizados y la información detallada sobre los parámetros.

>[!NOTE]
>
>La herramienta OSGi Configuration Diff (Diferencias de configuración de OSGi), que forma parte de [AEM Tools](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html), puede utilizarse para enumerar las configuraciones predeterminadas de OSGi.

>[!NOTE]
>
>Es posible que se requieran más paquetes para áreas específicas de funcionalidad dentro de AEM. En estos casos, los detalles de configuración se pueden encontrar en la página relacionada con la funcionalidad adecuada.

**AEM** Listener de Eventos de ReplicaciónConfigure:

* **Run Modes**, en el que los eventos de replicación se distribuirán a los oyentes. Por ejemplo, si se define como autor, entonces este es el sistema que &quot;iniciará&quot; la replicación.

* El modo de ejecución **publish** debe agregarse si el código del proyecto procesa eventos de replicación (replicación inversa) en un entorno de publicación. Por ejemplo, cuando se utiliza el despachante para vaciar del entorno de publicación o cuando se produce la replicación estándar a otras instancias de publicación.

**AEM Repositorio cambiar** listenerConfigure:

* Las **Rutas**, ubicaciones para escuchar los eventos del repositorio listos para su distribución.

**Repositorio de cliente CRX Sling** Configure el acceso al repositorio de contenido subyacente.

* La **Contraseña de administrador** debe cambiarse después de la instalación para garantizar la [seguridad](/help/sites-administering/security-checklist.md) de la instancia.
* No deben ser necesarios otros cambios y se debe tener cuidado, ya que pueden afectar al acceso al repositorio.

**Wiki Mail** ServiceConfigure las opciones de correo electrónico para los correos electrónicos enviados por una wiki.

**Consola de administración Apache Felix OSGi** Configure:

* **Plugins**, los elementos de navegación principales (complementos de consola) que estarán disponibles en los elementos de menú de nivel superior de las  **consolas de administración web** Apache Felix. Deshabilite los que no necesite, ya que cada uno requiere espacio y recursos.

>[!CAUTION]
>
>Asegúrese de configurar lo siguiente:
>
>**Nombre** de usuario y  **contraseña**, las credenciales para acceder a la Consola de gestión web Apache Felix.
>La contraseña debe cambiarse después de la instalación inicial para garantizar la [seguridad](/help/sites-administering/security-checklist.md) de la instancia.

>[!NOTE]
>
>Esta configuración debe realizarse utilizando la Consola Felix tal como es necesaria al inicio - antes de que el repositorio esté disponible.

**Registrador de datos de solicitud personalizable de Apache SlingConfigure:** 

* **Nombre del** registrador y  **formato de registro** para configurar la ubicación y el formato de la solicitud y el registro de acceso (predeterminado:  `request.log`). Este archivo de registro es esencial para analizar el rendimiento o la funcionalidad de depuración relacionada con la cadena web.
Esto está emparejado con el [registrador de solicitudes de Apache Sling](#apacheslingrequestlogger).

Para obtener más información, consulte [AEM Logging](/help/sites-deploying/configure-logging.md) y [Sling Logging](https://sling.apache.org/site/logging.html).

**Agrupamiento de subprocesos de eventos de Apache SlingConfigure:** 

* **Tamaño** mínimo del grupo y Tamaño  **máximo del grupo**, el tamaño del grupo utilizado para mantener los subprocesos de evento.

* **Tamaño de cola**, el tamaño máximo de la cola de subprocesos si se agota el grupo.
El valor recomendado es `-1` ya que establece la cola como ilimitada; si se establece un límite, pueden producirse pérdidas al superarse.

* Cambiar esta configuración puede ayudar a que se realice el rendimiento en escenarios con un número elevado de eventos; por ejemplo, uso intensivo AEM DAM o Workflow.
* Los valores específicos de su escenario deben establecerse mediante pruebas.
* Estos ajustes pueden afectar al rendimiento de la instancia, por lo que no los cambie sin motivo y teniendo debidamente en cuenta.

**Apache Sling** ServletConfigure algunos aspectos de la renderización:

* **Indexación automática** para habilitar/deshabilitar la renderización de directorios para la exploración.
* **Habilite**  (o deshabilite) las representaciones predeterminadas, como  **HTML**,  **texto sin formato**,  **** JSONo  **XML**.
No debe deshabilitar JSON.

>[!NOTE]
>
>Esta configuración se configura automáticamente para instancias de producción si ejecuta AEM en [Modo preparado para producción](/help/sites-administering/production-ready.md).

**Apache Sling Java Script** HandlerConfigure las opciones para la compilación de archivos .java como secuencias de comandos (servlets).

Ciertos ajustes pueden afectar al rendimiento, deben deshabilitarse siempre que sea posible, en particular para una instancia de producción.

* S **Source VM** y **Target VM**, defina la versión de JDK como la que se usa como JVM de tiempo de ejecución

* para instancias de producción:

   * deshabilitar **Generar información de depuración**

**Instalador JCR Apache Sling** Estos parámetros probablemente no necesitan configuración, pero pueden ser útiles para saber al desarrollar o depurar. Por ejemplo, las carpetas de instalación pueden ser útiles para desproteger o crear un paquete.

* **Carpeta de instalación nombre** regexpandir  **Máx. profundidad de jerarquía de carpetas de instalación** : especifique dónde y a qué profundidad se buscan las carpetas del repositorio para que se instalen los recursos. Cuando se utiliza un comodín (como en .*/install) se buscarán todas las coincidencias adecuadas, por ejemplo, `/libs/sling/install` y `/libs/cq/core/install`.

* **Ruta de búsqueda**, lista de rutas que jcrinstall busca recursos para instalar, junto con un número que indica el factor de ponderación para esa ruta.

**Controlador de eventos de trabajo Apache SlingConfigure los parámetros que administran la programación de trabajos:** 

* **Intervalo** de reintento,  **Máximo de reintentos**,  **Máximo de trabajos paralelos**,  **Conocimiento de tiempo de espera**, entre otros.

* Cambiar esta configuración puede mejorar el rendimiento en escenarios con un número elevado de trabajos; por ejemplo, un uso intensivo de AEM DAM y flujos de trabajo.
* Los valores específicos de su escenario deben establecerse mediante pruebas.
* No cambie esta configuración sin motivo, solo cambie después de tener en cuenta.

**Controlador de scripts Apache Sling JSP** Configure los ajustes relevantes de rendimiento para el controlador de scripts JSP. Para mejorar el rendimiento, debe deshabilitar tanto como sea posible.

En particular para las instancias de producción:

* deshabilitar **Generar información de depuración**
* deshabilitar **Mantener Java generado**
* deshabilitar **Contenido asignado**
* deshabilitar **Mostrar fragmentos de origen**

>[!NOTE]
>
>Esta configuración se configura automáticamente para instancias de producción si ejecuta AEM en [Modo preparado para producción](/help/sites-administering/production-ready.md).

**Configuración del registro de Apache Sling** Configure:

* **Archivo de** registro  **de Leveland**, para definir la ubicación y el nivel de registro de la configuración de registro central (error.log). El nivel se puede establecer en uno de `DEBUG`, `INFO`, `WARN`, `ERROR` y `FATAL`.

* **Número de** archivos de registro y  **de** umbral de archivo de registro para definir el tamaño y la rotación de la versión del archivo de registro.

* **El patrón de** mensaje define el formato de los mensajes de registro.

Para obtener más información, consulte [AEM Logging](/help/sites-deploying/configure-logging.md#global-logging) y [Sling Logging](https://sling.apache.org/site/logging.html).

**Configuración del registrador de Apache Sling (Configuración de fábrica)**  Configure:

* **Nivel** de registro,  **archivo** de registro y formato  **de** mensaje para definir detalles del archivo de registro y los mensajes.

* **** Registro para definir la categoría; por ejemplo, solo registre para com.day.cq.

* Al utilizar **Factory Configurations**, se puede agregar cualquier cantidad de configuraciones adicionales para satisfacer los distintos niveles de registro y categorías necesarios.
* Estas configuraciones son útiles durante el desarrollo; por ejemplo, para registrar mensajes de TRACE para un servicio específico en un archivo de registro específico.
* Estas configuraciones son útiles en un entorno de producción; por ejemplo, para que los mensajes sobre un servicio específico se registren en un archivo de registro individual para facilitar la monitorización.

Para obtener más información, consulte [AEM Logging](/help/sites-deploying/configure-logging.md) y [Sling Logging](https://sling.apache.org/site/logging.html).

**Configuración de Apache Sling Logging Writer (Configuración de fábrica)**  Configure:

* **Archivo de** registro para definir la existencia de un archivo de registro.
* **Número de** archivos de registro para definir la rotación de la versión.

* El escritor se puede utilizar mediante una configuración **Apache Sling Logger Configuration**.

* Estas configuraciones son útiles durante el desarrollo; por ejemplo, para registrar mensajes de TRACE para un servicio específico en un archivo de registro específico.
* Estas configuraciones son útiles en un entorno de producción; por ejemplo, para que los mensajes sobre un servicio específico se registren en un archivo de registro individual para facilitar la monitorización.

Para obtener más información, consulte [AEM Logging](/help/sites-deploying/configure-logging.md) y [Sling Logging](https://sling.apache.org/site/logging.html).

**Apache Sling Main** ServletConfigure:

* **Número de llamadas por solicitud** y  **repetición** profundos para proteger el sistema contra recursiones infinitas y llamadas de script excesivas.

**Apache Sling MIME Tipo** ServiceConfigure:

* **Los** tipos MIME para agregar al sistema los requeridos por el proyecto. Esto permite una solicitud `GET` en un archivo para establecer el encabezado de tipo de contenido correcto para vincular el tipo de archivo y la aplicación.

**Filtro** de referente de Apache SlingPara solucionar problemas de seguridad conocidos con falsificación de solicitudes entre sitios (CSRF) en CRX WebDAV y Apache Sling, debe configurar el filtro de referente.

El servicio de filtro de referente es un servicio OSGi que le permite configurar:

* qué métodos http deben filtrarse
* si se permite un encabezado de referente vacío
* y una lista de servidores a permitir además del host del servidor.

Consulte la [Lista de comprobación de seguridad: problemas con la falsificación de solicitudes entre sitios](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obtener más información.

>[!NOTE]
>
>El filtro de referente de Apache Sling depende de la instalación de un paquete de correcciones rápidas.

**Registrador de solicitudes** de Apache SlingConfigure:

* varios parámetros para definir cómo se registran las solicitudes.
* **Habilite el registro de solicitudes** para habilitar o deshabilitar.

* **Habilite el registro de acceso** para habilitar o deshabilitar.

Esto está emparejado con el [registrador de datos de solicitud personalizado de Apache Sling](#apacheslingcustomizablerequestdatalogger).

Para obtener más información, consulte [AEM Logging](/help/sites-deploying/configure-logging.md) y [Sling Logging](https://sling.apache.org/site/logging.html).

**Apache Sling Resource Resolver** FactoryConfigure aspectos centrales de la resolución de recursos de Sling:

* **Ruta** de búsqueda de recursos, agregue cualquier ruta específica del proyecto (pero no elimine  `/libs` ni  `/apps`).

* **URL** virtuales para definir las asignaciones de URL de vanidad.

* **Asignaciones** de URL para definir cualquier alias; por ejemplo, de  `/content` a  `/`.

* **Ubicación** de asignación, la configuración del asignador externalizada en  `/etc/map`.

* Utilice su instalación local (por ejemplo, utilice `https://localhost:4502/system/console/jcrresolver`) para determinar qué Resource Resolver está activo.

Para obtener más información, consulte: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>En particular, estas opciones deben configurarse en el repositorio.
>
>De lo contrario, los cambios realizados en **URL Mappings** mediante la consola Felix podrían ser sobrescritos por AEM al siguiente inicio.

**Apache Sling Servlet/Resolver script y** Controlador de erroresEl Servlet Sling y el Resolver script tienen varias tareas:

1. Se utiliza como `ServletResolver` para seleccionar el Servlet o Script al que llamar para gestionar la solicitud.

1. Actúa como `SlingScriptResolver`.

1. Administra la gestión de errores implementando la interfaz `ErrorHandler` utilizando el mismo algoritmo para seleccionar servlets y secuencias de comandos de gestión de errores que se utilizan para resolver servlets y secuencias de comandos de procesamiento de solicitudes.

Se pueden configurar varios parámetros, entre ellos:

* **Execution** incluye las rutas para buscar scripts ejecutables; al configurar rutas específicas, puede limitar qué secuencias de comandos se pueden ejecutar. Si no se configura ninguna ruta, se utiliza la predeterminada ( `/` = root), esto permite la ejecución de todas las secuencias de comandos.
Si un valor de ruta configurado termina con una barra diagonal, se buscará en todo el subárbol. Sin esta barra diagonal, la secuencia de comandos solo se ejecutará si es una coincidencia exacta.

* **Usuario de script** : esta propiedad opcional puede especificar la cuenta de usuario del repositorio que se utiliza para leer las secuencias de comandos. Si no se especifica ninguna cuenta, el usuario `admin` se utiliza de forma predeterminada.

* **Extensiones** predeterminadasLista de extensiones para las que se utilizará el comportamiento predeterminado. Esto significa que el último segmento de ruta del tipo de recurso se puede usar como nombre de secuencia de comandos.

**Day Commons GFX Font** HelperAl procesar gráficos, puede utilizar DrawText para incrustar texto. Para ello, también puede instalar sus propias fuentes:

* Defina la **Ruta de fuente** que se buscará para fuentes específicas del proyecto.
Por ejemplo, `/apps/myapp/fonts`.

**Configuración proxy de componentes HTTP de ApacheConfiguración proxy** para todo el código que utiliza el cliente HTTP de Apache, utilizado cuando se realiza un HTTP; por ejemplo, en la replicación.

Al crear una nueva configuración, no realice cambios en la configuración de fábrica sino que cree una nueva configuración de fábrica para este componente mediante el administrador de configuración disponible aquí: **https://localhost:4502/system/console/configMgr/**. La configuración del proxy está disponible en **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>En AEM 6.0 y versiones anteriores, el proxy se configuró en Day Commons HTTP Client. A partir de AEM versión 6.1 y posteriores, la configuración proxy se ha trasladado a la &quot;Configuración proxy de componentes HTTP Apache&quot; en lugar de la configuración &quot;Cliente HTTP Day Commons&quot;.

**Day CQ** AntispamConfigure el servicio antispam (Akismet) utilizado. Esto requiere que registre lo siguiente:

* **Proveedor**
* **Clave de API**
* **URL registrada**

**Adobe Granite HTML Library** ManagerConfigure esto para controlar el manejo de las bibliotecas de cliente (css o js); incluyendo, por ejemplo, cómo se ve la estructura subyacente.

* Para instancias de producción:

   * habilite **Minificar** (para eliminar los caracteres CRLF y los espacios en blanco).
   * habilite **Gzip** (para permitir que se comprueben los archivos y se acceda a ellos mediante una solicitud).
   * deshabilitar **Depurar**
   * deshabilitar **Temporización**

* Para el desarrollo de JS (especialmente al activar/depurar):

   * deshabilitar **Minificar**
   * habilite **Debug** para separar los archivos para depurarlos y utilizarlos con firebug.
   * habilite **Timing** en caso de interés en la temporización.
   * habilite la consola **Debug** para ver los mensajes de registro de la consola JS.

>[!CAUTION]
>
>Al cambiar la configuración de **Minify** o **Gzip** también deberá eliminar el contenido de `/var/clientlibs`. Esta es una versión en caché de clientlibs y se reconstruirá cuando se solicite la próxima vez.

>[!NOTE]
>
>Esta configuración se configura automáticamente para instancias de producción si ejecuta AEM en [Modo preparado para producción](/help/sites-administering/production-ready.md).

**Day CQ HTTP Header Authentication** HandlerConfiguración de todo el sistema para el método de autenticación básico de la solicitud HTTP.

Al utilizar [grupos de usuarios cerrados](/help/sites-administering/cug.md) puede configurar (entre otros):

* **Dominio HTTP**
* La **Página de inicio de sesión predeterminada**

**Comprobación de servicio del Verificador de enlaces de CQ** de día y, si es necesario, configure:

* **Periodo** del planificador para definir el intervalo en el que se deben comprobar automáticamente los vínculos externos.

* Marque **Intervalo de tolerancia de enlace incorrecto** para el periodo después del cual un vínculo externo fallido se considera malo.
* **Patrones de anulación de verificación de vínculo**, para definir las rutas que se excluirán de la comprobación de vínculos.

**Day CQ Link Checker** TaskConfigure los ajustes de una tarea de verificación de vínculos únicos (una tarea que comprueba un vínculo externo):

* Compruebe los intervalos definidos en **Intervalo de prueba de enlace correcto** y **Intervalo de prueba de enlace incorrecto**

* Los distintos parámetros relacionados con los proxies para acceso a Internet y NTLM necesarios para acceso externo al comprobar un vínculo.

**Day CQ Mail** ServiceConfigure el nombre de host y los detalles de acceso para el servidor de correo. Consulte la sección Configuración del servicio de correo .

**Newsletter de Day CQ MCM** Configure los distintos ajustes que se usan con la newsletter.

**Day CQ Root** MappingConfigure:

* **Target** Path para definir a dónde se redirigirá una solicitud de &quot;  `/`&quot;.

Hay dos IU disponibles en AEM:

* la IU táctil es la IU estándar
* y la IU clásica obsoleta sigue funcionando completamente

Con AEM asignación raíz puede configurar la IU que desea tener como predeterminada para su instancia:

* Para que la IU táctil sea la IU predeterminada, la **Ruta de destino** debe señalar a:

   ```
      /projects.html
   ```

* Para que la IU clásica sea la IU predeterminada, la **Ruta de destino** debe señalar a:

   ```
      /welcome.html
   ```

>[!NOTE]
>
>Tras una instalación estándar, la IU táctil es la IU predeterminada.

**Adobe Granite SSO Authentication** HandlerConfiguración del inicio de sesión único (SSO) detalles; estos suelen ser necesarios en configuraciones de creación empresarial, a menudo junto con LDAP.

Hay varias propiedades de configuración disponibles:

* ****
PathPath para el que está activo este controlador de autenticación. Si este parámetro se deja vacío, el controlador de autenticación se desactiva. Por ejemplo, la ruta / hace que el controlador de autenticación se utilice para todo el repositorio.

* **El valor Clasificación del servicio**
de Service RankingOSGi Framework se utiliza para indicar el pedido utilizado para llamar a este servicio. Esto es un 
`int` donde los valores más altos designan mayor prioridad.
El valor predeterminado es `0`.

* **Nombres de**
encabezadoLos nombres de los encabezados que pueden contener un ID de usuario.

* **Nombres de**
cookiesLos nombres de las cookies que pueden contener un ID de usuario.

* **Parámetros**
NombresLos nombres de los parámetros de solicitud que pueden proporcionar el ID de usuario.

* **Mapa**
de usuariosPara los usuarios seleccionados, el nombre de usuario extraído de la solicitud HTTP se puede reemplazar por uno diferente en el objeto de credenciales. La asignación se define aquí. Si el nombre de usuario 
`admin` aparece a ambos lados del mapa, se ignorará la asignación. Tenga en cuenta que el carácter &quot;=&quot; debe omitirse con un &quot;\&quot; inicial.

* ****
FormatoIndica el formato en el que se proporciona el ID de usuario. Uso:

   * `Basic` si el ID de usuario está codificado en el formato de autenticación básica HTTP
   * `AsIs` si el ID de usuario se proporciona en formato de texto sin formato o cualquier valor aplicado de expresión regular debe usarse tal cual o cualquier expresión regular

**Filtro de depuración de CQ WCM de díaResulta útil cuando se desarrolla, ya que permite el uso de sufijos como ?debug=layout al acceder a una página.** Por ejemplo, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout proporcionará información de diseño que puede ser de interés para el desarrollador.

* Desactívelo en las instancias de producción para garantizar el rendimiento y la seguridad.

**Day CQ WCM** FilterConfigure:

* **Modo WCM **para definir el modo predeterminado.
* En una instancia de autor, puede ser `edit`, `disable,preview` o `analytics`.
Se puede acceder a los demás modos desde la barra de tareas o se puede utilizar el sufijo `?wcmmode=disabled` para emular un entorno de producción.

* En una instancia de publicación, esto debe establecerse en `disabled` para garantizar que no se pueda acceder a ningún otro modo.

>[!NOTE]
>
>Esta configuración se configura automáticamente para instancias de producción si ejecuta AEM en [Modo preparado para producción](/help/sites-administering/production-ready.md).

**Configurador del verificador de vínculos de CQ WCM DayConfigure:** 

* **Lista de** configuraciones de reescritura para especificar una lista de ubicaciones para configuraciones de linkchecker basadas en contenido. Las configuraciones se pueden basar en el modo de ejecución; esto es importante para distinguir entre los entornos de autor y publicación, ya que la configuración del verificador de enlaces puede diferir.

**Day CQ WCM Page** ProcessorConfigure:

* **Rutas**, una lista de ubicaciones en las que el sistema escucha las modificaciones de la página antes de activar un  `jcr:Event`.

**Rastreador de impresiones de página de AdobePara una instancia de autor, configure:** 

* **sling.auth.requirements**: establezca el valor de esta propiedad en  `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Esta configuración permitirá solicitudes anónimas al servicio de seguimiento.

>[!NOTE]
>
>Consulte [Impresiones de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obtener más información.

**Estadísticas de página de CQ WCM de díaPara una instancia de publicación, configure:** 

* **URL para enviar** datos para configurar la URL utilizada para rastrear las estadísticas de la página (es vital si una solicitud de rastreador pasa por el despachante); por ejemplo, el valor predeterminado es  `https://localhost:4502/libs/wcm/stats/tracker`.

* **La secuencia de comandos de seguimiento** está habilitada para habilitar (  `true`) o deshabilitar (  `false`) la inclusión de la secuencia de comandos de seguimiento en las páginas. El valor predeterminado es `false`.

>[!NOTE]
>
>Consulte [Impresiones de página](/help/sites-deploying/configuring.md#enabling-page-impressions) para obtener más información.

**Day CQ WCM Version** ManagerControle si las versiones se administran en su sistema y cómo se administran:

* **Crear versión en activación**, habilitada en una instalación estándar
* **Habilitar depuración**

* **Purgar rutas**, las rutas en las que buscará una acción de búsqueda
* **Rutas de versiones implícitas**, las rutas en las que el control de versiones implícito está activo.

* **Edad máxima de la versión**, la edad máxima (en días) de una versión

* **Número máximo de versiones**, el número máximo de versiones que se van a mantener

Consulte [Depuración de versiones](/help/sites-deploying/version-purging.md) para obtener más información.

**Servicio Day CQ Workflow Email Notification** Configure los ajustes de correo electrónico para las notificaciones enviadas por un flujo de trabajo.

**Day CQSE HTTP** ServiceControle el motor Servlet CQ:

* **NIO para HTTP, **Si se utiliza o no NIO para HTTP. La opción predeterminada es true. Solo se utiliza si HTTP está habilitado.
* **Tiempo de espera de conexión, **Tiempo de espera de conexión en milisegundos. Esta propiedad se aplica tanto a conexiones HTTP como HTTPS. El valor predeterminado es de 60 segundos.

* **Habilitar HTTPS,** si HTTPS está habilitado o no. El valor predeterminado es false.
* **Tiempo de espera de sesión**, duración predeterminada de una sesión HTTP especificada en minutos. Si el tiempo de espera es 0 o menos, las sesiones nunca se agotarán. El valor predeterminado es de 10 minutos.
* **Registro de depuración**, escriba o no mensajes a nivel de depuración. El valor predeterminado es false.
* **Tamaño del búfer de solicitud**, Tamaño del búfer para solicitudes en bytes. El valor predeterminado es 8 KB.
* **Número máximo de subprocesos**, número máximo de subprocesos que se utilizan para gestionar solicitudes. El valor predeterminado es 200.

Las siguientes propiedades solo se aplican si HTTPS está habilitado.

* **Puerto** HTTPS, puerto en el que escuchar la solicitud HTTPS. El valor predeterminado es 433.
* **NIO para HTTPS**, si se utiliza o no NIO para HTTP. El valor predeterminado es el valor de la propiedad NIO para HTTP.
* **Almacén de claves**, ruta absoluta al almacén de claves que se utilizará para HTTPS. Necesario si HTTPS está habilitado.
* **Contraseña** del almacén de claves, Contraseña para acceder al almacén de claves.
* **Alias de clave**, Alias de la clave secreta en el almacén de claves.
* **Contraseña de clave**, Contraseña para desbloquear la clave secreta en el almacén de claves.
* **Certificado de cliente**, requisito para que el cliente proporcione un certificado válido. El valor predeterminado es ninguno.

Consulte también [Habilitación de HTTP sobre SSL](/help/sites-administering/ssl-by-default.md) para obtener más información sobre las opciones relacionadas con SSL y una descripción completa sobre cómo habilitar HTTPS para CQSE.

**CQ Rewriter HTML Parser Factory**

Controla el analizador HTML para el reescritor de CQ.

* **Etiquetas adicionales para procesar** : puede añadir o eliminar etiquetas HTML para que el analizador las procese. De forma predeterminada, se procesan las etiquetas siguientes: A,IMG,AREA,FORMULARIO,BASE,VÍNCULO,SECUENCIA DE COMANDOS,CUERPO,HEAD.
* **Preservar mayúsculas y minúsculas** : de forma predeterminada, el analizador HTML convierte los atributos en mayúsculas (p. ej. eBay) a minúsculas (p. ej., ebay). Puede desactivarlo para conservar los atributos de mayúsculas y minúsculas del camello. Esto resulta útil cuando se utilizan marcos de front-end como Angular 2.

**JDBC Connections Day Commons** PoolConfigure el acceso a una base de datos externa que se utiliza como fuente para el contenido.

Se trata de una configuración de fábrica, por lo que se pueden configurar varias instancias.

**Servicio de sesiones DPS de Adobe CQ Media** Administrar sesiones DPS para su uso con Publicaciones.

En particular, puede definir el `dps.session.service.url.name`: el valor predeterminado es [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**CDN** RewriterSe debe garantizar la comunicación entre AEM y una CDN para que los recursos/binarios se entreguen al usuario final de forma segura. Esto implica dos tareas:

* Acceder al recurso desde AEM a través de la CDN por primera vez (o después de que caduque en la caché).
* El acceso al recurso almacenado en caché en CDN de forma segura, ya que una vez que el recurso se almacena en caché en CDN, la solicitud no va a AEM y todos los usuarios que tienen acceso a ese recurso en deben proporcionarse desde CDN.

AEM proporciona un reescritor para reescribir las URL de recursos internos en direcciones URL de CDN externas. Reescribe los vínculos que se pasarán a la CDN, incluida una firma JWS y un tiempo de caducidad para permitir el acceso seguro al recurso. Esta función se utilizará en instancias de autor.

El flujo general es el siguiente:

1. El usuario se autentica con AEM y solicita una página con recursos.
1. La página solicitada contiene un recurso similar a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. Rewriter transforma el vínculo a una URL de CDN que contiene una firma JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. A continuación, el navegador del usuario reenvía la solicitud de recurso al servidor CDN
1. La CDN debe configurarse para reenviar la solicitud a AEM junto con el parámetro `cdn_sign`.
1. Un gestor de autenticación valida el parámetro `cdn_sign` y devuelve el recurso a CDN que luego se envía al usuario

El flujo entre el navegador del usuario, la CDN y la AEM se puede visualizar de la siguiente manera.

![Chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>Actualmente, esta función solo está habilitada para AEM instancias de autor.

**** CDNConfigServiceImplProporciona configuraciones de CDN

La función de reescritura de CDN se puede habilitar proporcionando **CDN distribution domain name** en la configuración de com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

El servicio también contiene otras opciones de configuración como habilitar/deshabilitar la reescritura de CDN, prefijos de ruta para los que se realiza la reescritura de CDN, valores TTL y protocolo (HTTP o HTTPS).

**** CDNRewriterRedactor para reescribir URL de imágenes internas en URL de CDN

El valor **Tag Attributes** en com.adobe.cq.cdn.rewriter.impl.CDNRewriter se puede definir para que solo se reescriban los vínculos de imagen selectivos.
