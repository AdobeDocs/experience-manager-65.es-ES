---
title: Lista de comprobación de seguridad
seo-title: Lista de comprobación de seguridad
description: Obtenga información sobre las distintas consideraciones de seguridad al configurar e implementar AEM.
seo-description: Obtenga información sobre las distintas consideraciones de seguridad al configurar e implementar AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
translation-type: tm+mt
source-git-commit: 474fc122f557f32d34fddd9d35a113431f6ce491
workflow-type: tm+mt
source-wordcount: '2841'
ht-degree: 0%

---


# Lista de comprobación de seguridad {#security-checklist}

Esta sección trata de varios pasos que debe realizar para garantizar que la instalación de AEM sea segura cuando se implemente. La lista de comprobación debe aplicarse de arriba a abajo.

>[!NOTE]
>
>También se dispone de más información [sobre las amenazas de seguridad más peligrosas, tal como se publica en Open Aplicación web Security Project (OWASP)](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).

>[!NOTE]
>
>Existen algunas [consideraciones de seguridad](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) adicionales aplicables en la fase de desarrollo.

## Principales medidas de seguridad {#main-security-measures}

### Ejecutar AEM en modo listo para producción {#run-aem-in-production-ready-mode}

Para obtener más información, consulte [Ejecución de AEM en modo listo para la producción](/help/sites-administering/production-ready.md).

### Habilitar HTTPS para la seguridad de capa de transporte {#enable-https-for-transport-layer-security}

La activación de la capa de transporte HTTPS en instancias de creación y publicación es obligatoria para tener una instancia segura.

>[!NOTE]
>
>Consulte la sección [Habilitación de HTTP sobre SSL](/help/sites-administering/ssl-by-default.md) para obtener más información.

### Instalar revisiones de seguridad {#install-security-hotfixes}

Asegúrese de que ha instalado las [revisiones de seguridad más recientes proporcionadas por Adobe](https://helpx.adobe.com/es/experience-manager/kb/aem63-available-hotfixes.html).

### Cambiar las contraseñas predeterminadas de las cuentas de administración de la Consola de AEM y OSGi {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe recomienda encarecidamente que después de la instalación cambie la contraseña de las [**cuentas** `admin` privilegiadas](#changing-the-aem-admin-password) (en todas las instancias).

Estas cuentas incluyen:

* La cuenta de AEM `admin`

   Una vez que haya cambiado la contraseña de la cuenta de administrador de AEM, deberá utilizar la nueva contraseña al acceder a CRX.

* La contraseña `admin` para la consola Web OSGi

   Este cambio también se aplicará a la cuenta de administrador utilizada para acceder a la consola web, por lo que deberá utilizar la misma contraseña al acceder a ella.

Estas dos cuentas utilizan credenciales independientes y tener una contraseña clara y segura para cada una de ellas es vital para una implementación segura.

#### Cambio de la contraseña de administración de AEM {#changing-the-aem-admin-password}

La contraseña de la cuenta de administrador de AEM se puede cambiar mediante la consola [Operaciones de granito - Usuarios](/help/sites-administering/granite-user-group-admin.md).

Aquí puede editar la cuenta `admin` y [cambiar la contraseña](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>Al cambiar la cuenta de administrador también se cambia la cuenta de la consola web OSGi. Después de cambiar la cuenta de administrador, debe cambiar la cuenta OSGi por otra diferente.

#### Importancia de cambiar la contraseña de la consola web OSGi {#importance-of-changing-the-osgi-web-console-password}

Aparte de la cuenta de AEM `admin`, si no se cambia la contraseña predeterminada para la contraseña de la consola web OSGi, puede producirse lo siguiente:

* Exposición del servidor con una contraseña predeterminada durante el inicio y el apagado (que puede tardar minutos en los servidores grandes);
* Exposición del servidor cuando el repositorio está inactivo o reiniciando el paquete y OSGI se está ejecutando.

Para obtener más información sobre cómo cambiar la contraseña de la consola web, consulte [Cambio de la contraseña de administración de la consola web OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) a continuación.

#### Cambio de la contraseña de administración de la consola web OSGi {#changing-the-osgi-web-console-admin-password}

También debe cambiar la contraseña utilizada para acceder a la consola web. Esto se realiza configurando las siguientes propiedades de la [Consola de administración OSGi de Apache Felix](/help/sites-deploying/osgi-configuration-settings.md):

**Nombre de** usuario y  **contraseña**, las credenciales para acceder a la consola de gestión web Apache Felix.
La contraseña debe cambiarse después de la instalación inicial para garantizar la seguridad de la instancia.

Para ello:

1. Vaya a la consola web en `<server>:<port>/system/console/configMgr`.
1. Vaya a **Apache Felix OSGi Management Console** y cambie el **nombre de usuario** y la **contraseña**.

   ![climage_1-3](assets/chlimage_1-3.png)

1. Haga clic en **Guardar**.

### Implementar el controlador de errores personalizado {#implement-custom-error-handler}

Adobe recomienda definir las páginas de tratamiento de errores personalizadas, especialmente para los códigos de respuesta HTTP 404 y 500 para evitar la divulgación de información.

>[!NOTE]
>
>Consulte [Cómo puedo crear secuencias de comandos personalizadas o controladores de errores](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) artículo de la base de conocimiento para obtener más información.

### Lista de comprobación de seguridad de despachante completa {#complete-dispatcher-security-checklist}

AEM Dispatcher es una parte fundamental de su infraestructura. Adobe recomienda encarecidamente que complete la [lista de comprobación de seguridad del despachante](https://helpx.adobe.com/experience-manager/dispatcher/using/security-checklist.html).

>[!CAUTION]
>
>Con Dispatcher debe deshabilitar el selector &quot;.form&quot;.

## Pasos de verificación {#verification-steps}

### Configurar usuarios de replicación y transporte {#configure-replication-and-transport-users}

Una instalación estándar de AEM especifica `admin` como el usuario de las credenciales de transporte dentro de los [agentes de replicación](/help/sites-deploying/replication.md) predeterminados. Además, el usuario administrador se utiliza para originar la replicación en el sistema de creación.

Por motivos de seguridad, ambos deben modificarse para reflejar el caso de uso particular que se examina, teniendo presentes los dos aspectos siguientes:

* El **usuario de transporte** no debe ser el usuario administrador. En su lugar, configure un usuario en el sistema de publicación que solo tenga derechos de acceso a las partes relevantes del sistema de publicación y utilice las credenciales de ese usuario para el transporte.

   Puede realizar inicios desde el usuario del receptor de replicación integrado y configurar los derechos de acceso de este usuario para que coincidan con su situación

* El **usuario de replicación** o **ID de usuario del agente** no debe ser también el usuario administrador, sino un usuario que solo puede ver contenido que se supone que se debe replicar. El usuario de replicación se utiliza para recopilar el contenido que se va a replicar en el sistema de creación antes de enviarlo al editor.

### Compruebe las comprobaciones de estado de seguridad del Panel de operaciones {#check-the-operations-dashboard-security-health-checks}

AEM 6 presenta el nuevo Panel de operaciones, que tiene por objeto ayudar a los gestores de sistemas a solucionar problemas y supervisar el estado de una instancia.

El panel también incluye una serie de controles de seguridad. Se recomienda que verifique el estado de todas las comprobaciones de seguridad antes de empezar a usar la instancia de producción. Para obtener más información, consulte la [documentación de Panel de operaciones](/help/sites-administering/operations-dashboard.md).

### Compruebe si el contenido de ejemplo está presente {#check-if-example-content-is-present}

Todos los usuarios y el contenido de ejemplo (por ejemplo, el proyecto de Geometrixx y sus componentes) deben desinstalarse y eliminarse completamente en un sistema productivo antes de ponerlo a disposición del público.

>[!NOTE]
>
>Las aplicaciones We.Retail de muestra se eliminan si esta instancia se está ejecutando en [Modo listo para la producción](/help/sites-administering/production-ready.md). Si, por alguna razón, no es el caso, puede desinstalar el contenido de muestra si ingresa al Administrador de paquetes, busca y desinstala todos los paquetes de We.Retail. Para obtener más información, consulte [Trabajo con paquetes](package-manager.md).

### Compruebe si los paquetes de desarrollo de CRX están presentes {#check-if-the-crx-development-bundles-are-present}

Estos paquetes OSGi de desarrollo deben desinstalarse tanto en los sistemas productivos de creación como de publicación antes de hacerlos accesibles.

* Compatibilidad con CRXDE de Adobe (com.adobe.granite.crxde-support)
* Explorador de Adobe Granite CRX (com.adobe.granite.crx-explorer)
* CRXDE Lite de granito de Adobe (com.adobe.granite.crxde-lite)

### Compruebe si el paquete de desarrollo Sling está presente {#check-if-the-sling-development-bundle-is-present}

Las [Herramientas para desarrolladores de AEM para Eclipse](/help/sites-developing/aem-eclipse.md) implementan la Instalación de soporte de herramientas de Apache Sling (org.apache.sling.tooling.support.install).

Este paquete OSGi debe desinstalarse tanto en los sistemas productivos de creación como de publicación antes de hacerlos accesibles.

### Protect contra falsificación de solicitudes entre sitios {#protect-against-cross-site-request-forgery}

#### El marco de protección del CSRF {#the-csrf-protection-framework}

AEM 6.1 incluye un mecanismo que ayuda a proteger contra los ataques de falsificación de solicitudes entre sitios, denominado **Marco de protección de CSRF**. Para obtener más información sobre cómo utilizarla, consulte la [documentación](/help/sites-developing/csrf-protection.md).

#### El filtro Remitente del reenvío Sling {#the-sling-referrer-filter}

Para abordar problemas conocidos de seguridad con la falsificación de solicitudes entre sitios (CSRF) en CRX WebDAV y Apache Sling, debe agregar configuraciones para el filtro de Remitente del reenvío para utilizarlo.

El servicio de filtro de remitente del reenvío es un servicio OSGi que le permite configurar:

* qué métodos http deben filtrarse
* si se permite un encabezado de remitente del reenvío vacío
* y una lista de servidores que se permitirá además del host del servidor.

   De forma predeterminada, todas las variaciones de localhost y los nombres de host actuales a los que está enlazado el servidor están en la lista.

Para configurar el servicio de filtros de remitente del reenvío:

1. Abra la consola Apache Felix (**Configuraciones**) en:

   `https://<server>:<port_number>/system/console/configMgr`

1. Inicie sesión como `admin`.
1. En el menú **Configuraciones**, seleccione:

   `Apache Sling Referrer Filter`

1. En el campo `Allow Hosts`, introduzca todos los hosts permitidos como remitentes del reenvío. Cada entrada debe ser del formulario

   &lt;protocol>://&lt;server>:&lt;port>

   Por ejemplo:

   * `https://allowed.server:80` permite todas las solicitudes de este servidor con el puerto determinado.
   * Si también desea permitir solicitudes https, debe introducir una segunda línea.
   * Si permite todos los puertos de ese servidor, puede utilizar `0` como número de puerto.

1. Seleccione el campo `Allow Empty` si desea permitir encabezados de remitente del reenvío vacíos o ausentes.

   >[!CAUTION]
   >
   >Se recomienda proporcionar un remitente del reenvío mientras se utilizan herramientas de línea de comandos como `cURL` en lugar de permitir un valor vacío, ya que podría exponer su sistema a ataques de CSRF.

1. Edite los métodos que este filtro debe utilizar para las comprobaciones con el campo `Filter Methods`.

1. Haga clic en **Guardar** para guardar los cambios.

### Configuración OSGI {#osgi-settings}

Algunos ajustes de OSGI se establecen de forma predeterminada para facilitar la depuración de la aplicación. Es necesario cambiar estos datos en las instancias productivas de publicación y creación para evitar que la información interna se filtre al público.

>[!NOTE]
>
>Todos los ajustes siguientes, a excepción de **El filtro de depuración de CQ WCM de día**, se cubren automáticamente en el [modo de preparación para la producción](/help/sites-administering/production-ready.md). Debido a esto, recomendamos revisar todos los ajustes antes de implementar la instancia en un entorno productivo.

Para cada uno de los siguientes servicios es necesario cambiar la configuración especificada:

* [Administrador](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager) de biblioteca HTML de Adobe Granite:

   * habilite **Minificar** (para eliminar caracteres de CRLF y de espacio en blanco).
   * habilite **Gzip** (para permitir que se comprueben los archivos y se acceda a ellos con una solicitud).
   * deshabilitar **Depurar**
   * deshabilitar **Temporización**

* [Filtro](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter) de depuración de CQ WCM de día:

   * desmarcar **Habilitar**

* [Filtro](/help/sites-deploying/osgi-configuration-settings.md) WCM CQ de día:

   * solo en la publicación, establezca **Modo WCM** en &quot;deshabilitado&quot;

* [Controlador](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler) de Java Script de Apache Sling:

   * deshabilitar **Generar información de depuración**

* [Controlador](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler) de secuencias de comandos Apache Sling JSP:

   * deshabilitar **Generar información de depuración**
   * deshabilitar **Contenido asignado**

Para obtener más información, consulte [Configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md).

Al trabajar con AEM existen varios métodos para gestionar los parámetros de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más detalles y las prácticas recomendadas.

## Lecturas adicionales {#further-readings}

### Mitigar los ataques de denegación de servicio (DoS) {#mitigate-denial-of-service-dos-attacks}

Un ataque de denegación de servicio (DoS) es un intento de hacer que un recurso de equipo no esté disponible para los usuarios previstos. Esto suele hacerse sobrecargando el recurso; por ejemplo:

* Con una avalancha de solicitudes de una fuente externa.
* Con una solicitud de más información de la que el sistema puede entregar correctamente.

   Por ejemplo, una representación JSON de todo el repositorio.

* Al solicitar una página de contenido con un número ilimitado de direcciones URL, la dirección URL puede incluir un identificador, algunos selectores, una extensión y un sufijo, cualquiera de los cuales se puede modificar.

   Por ejemplo: `.../en.html` también se puede solicitar como:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   Todas las variaciones válidas (p. ej., devolver una respuesta `200` y configuradas para almacenarse en caché) serán almacenadas en caché por el despachante, lo que finalmente conducirá a un sistema de archivos completo y a la ausencia de servicio para más solicitudes.

Hay muchos puntos de configuración para prevenir estos ataques, aquí solamente discutimos los directamente relacionados con AEM.

**Configuración de Sling para evitar DoS**

Sling está *centrado en el contenido*. Esto significa que el procesamiento se centra en el contenido, ya que cada solicitud (HTTP) se asigna al contenido en forma de recurso JCR (un nodo de repositorio):

* El primer destinatario es el recurso (nodo JCR) que contiene el contenido.
* En segundo lugar, el procesador, o secuencia de comandos, se encuentra desde las propiedades del recurso en combinación con determinadas partes de la solicitud (por ejemplo, selectores o la extensión).

>[!NOTE]
>
>Esto se trata con más detalle en [Sling Request Processing](/help/sites-developing/the-basics.md#sling-request-processing).

Este enfoque hace que Sling sea muy poderoso y muy flexible, pero como siempre es la flexibilidad que necesita ser administrada cuidadosamente.

Para ayudar a evitar el uso indebido de DoS, puede:

1. Incorporar controles a nivel de aplicación; debido al número de variaciones posibles, no es posible una configuración predeterminada.

   En la aplicación debe:

   * Controle los selectores de la aplicación, de modo que *sólo* proporcione los selectores explícitos necesarios y devuelva `404` para todos los demás.
   * Evite la salida de un número ilimitado de nodos de contenido.

1. Compruebe la configuración de los procesadores predeterminados, que puede ser un área problemática.

   * En particular, el procesador JSON que puede invertir la estructura de árbol en varios niveles.

      Por ejemplo, la solicitud:

      `http://localhost:4502/.json`

      podría volcar todo el repositorio en una representación JSON. Esto causaría problemas significativos en el servidor. Por este motivo, Sling establece un límite en el número de resultados máximos. Para limitar la profundidad del procesamiento JSON, puede establecer el valor para:

      **Resultados**  máximos de JSON(  `json.maximumresults`)

      en la configuración para el [Servlet de GET Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Cuando se supera este límite, el procesamiento se contraerá. El valor predeterminado para Sling dentro de AEM es `200`.

   * Como medida preventiva, deshabilite los demás procesadores predeterminados (HTML, texto sin formato, XML). Nuevamente configurando el [Servlet de GET Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >No deshabilite el procesador JSON, esto es necesario para el funcionamiento normal de AEM.

1. Utilice un servidor de seguridad para filtrar el acceso a su instancia.

   * Es necesario usar un cortafuegos de nivel de sistema operativo para filtrar el acceso a los puntos de la instancia que podrían provocar ataques de denegación de servicio si se dejan sin proteger.

**Mitigar contra los errores causados por el uso de selectores de formularios**

>[!NOTE]
>
>Esta mitigación solo debe realizarse en entornos de AEM que no utilicen Forms.

Dado que AEM no proporciona índices predeterminados para `FormChooserServlet`, el uso de selectores de formulario en consultas déclencheur una inversión costosa del repositorio, que normalmente interrumpe la instancia de AEM. Los selectores de formulario se pueden detectar con la presencia del **&amp;ast;.form.&amp;ast;** cadena en consultas.

Para mitigar esto, siga los pasos a continuación:

1. Vaya a la consola web señalando el explorador a *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Buscar **servlet de selector de formularios CQ WCM**
1. Después de hacer clic en la entrada, deshabilite el **Requisito de búsqueda avanzada** en la siguiente ventana.

1. Haga clic en **Guardar**.

**Mitigar los errores causados por el servlet de descarga de recursos**

El servlet de descarga de recursos predeterminado de AEM permite a los usuarios autenticados emitir solicitudes de descarga concurrentes de gran tamaño arbitrario para crear archivos ZIP de recursos visibles para ellos que pueden sobrecargar el servidor o la red.

Para mitigar los posibles riesgos de DoS causados por esta función, el componente OSGi `AssetDownloadServlet` está deshabilitado de forma predeterminada para las instancias de publicación en las versiones de AEM más recientes.

Si la configuración requiere que el servidor de descarga de recursos esté habilitado, consulte [este artículo](/help/assets/download-assets-from-aem.md) para obtener más información.

### Deshabilitar WebDAV {#disable-webdav}

WebDAV debe deshabilitarse tanto en la entorno de creación como en la de publicación. Esto se puede hacer deteniendo los paquetes OSGi adecuados.

1. Conéctese a la **Consola de administración Felix** que se ejecuta en:

   `https://<*host*>:<*port*>/system/console`

   Por ejemplo `http://localhost:4503/system/console/bundles`.

1. En la lista de paquetes, busque el paquete llamado:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Haga clic en el botón Detener (en la columna Acciones) para detener este paquete.

1. Otra vez en la lista de paquetes, encuentre el paquete llamado:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Haga clic en el botón Detener para detener este paquete.

   >[!NOTE]
   >
   >No es necesario reiniciar el AEM.

### Verifique que no esté revelando información de identificación personal en la ruta de inicio del usuario {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

Es importante que proteja a los usuarios asegurándose de que no expone ninguna información personal en la ruta de inicio de los usuarios del repositorio.

Desde AEM 6.1, la forma en que se almacenan los nombres de nodos de ID de usuario (también conocidos como autorizables) se cambia con una nueva implementación de la interfaz `AuthorizableNodeName`. La nueva interfaz ya no mostrará el ID de usuario en el nombre del nodo, sino que generará un nombre aleatorio.

No es necesario realizar ninguna configuración para habilitarla, ya que ésta es la forma predeterminada de generar ID autorizables en AEM.

Aunque no se recomienda, puede deshabilitarlo en caso de que necesite la implementación anterior para la compatibilidad con las aplicaciones existentes. Para ello, debe:

1. Vaya a la consola web y elimine la entrada** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName*** de la propiedad **requiredServicePids** en **Apache Jackrabbit Oak SecurityProvider**.

   También puede encontrar el proveedor de seguridad Oak buscando el **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID en las configuraciones de OSGi.

1. Elimine la configuración de OSGi **Apache Jackrabbit Oak Random Authorizable Node Name** desde la consola web.

   Para facilitar la búsqueda, tenga en cuenta que el PID de esta configuración es **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Para obtener más información, consulte la documentación de Oak sobre [Generación de nombres de nodos con autorización](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Evitar el rastreo de clics {#prevent-clickjacking}

Para evitar el &quot;clickjacking&quot; recomendamos configurar el servidor web para proporcionar el encabezado HTTP `X-FRAME-OPTIONS` establecido en `SAMEORIGIN`.

Para obtener más [información sobre el rastreo de clics, consulte el sitio OWASP](https://www.owasp.org/index.php/Clickjacking).

### Asegúrese De Replicar Correctamente Las Claves De Cifrado Cuando Sea Necesario {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Determinadas funciones de AEM y esquemas de autenticación requieren que se replicen las claves de cifrado en todas las instancias AEM.

Antes de hacer esto, tenga en cuenta que la replicación de claves se realiza de manera diferente entre las versiones, ya que la manera en que se almacenan las claves es diferente entre las versiones 6.3 y anteriores.

Consulte a continuación para obtener más información.

#### Replicar claves para AEM 6.3 {#replicating-keys-for-aem}

Mientras que en versiones anteriores las claves de replicación se almacenaban en el repositorio, comenzando con AEM 6.3, se almacenan en el sistema de archivos.

Por lo tanto, para replicar las claves en las instancias, debe copiarlas de la instancia de origen a la ubicación de las instancias de destinatario en el sistema de archivos.

Más concretamente, debe:

1. Acceda a la instancia de AEM, normalmente una instancia de autor, que contiene el material clave que copiar;
1. Busque el paquete com.adobe.granite.crypto.file en el sistema de archivos local. Por ejemplo, en esta ruta:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   El archivo `bundle.info` dentro de cada carpeta identificará el nombre del paquete.

1. Vaya a la carpeta de datos. Por ejemplo:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copie los archivos principales y HMAC.
1. A continuación, vaya a la instancia de destinatario a la que desee realizar el duplicado de la clave HMAC y navegue hasta la carpeta de datos. Por ejemplo:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Pegue los dos archivos que copió anteriormente.
1. [Actualice Crypto ](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) Bundlesi la instancia de destinatario ya se está ejecutando.
1. Repita los pasos anteriores para todas las instancias en las que desee replicar la clave.

>[!NOTE]
>
>Puede volver al método previo 6.3 de almacenamiento de claves agregando el parámetro siguiente cuando instale por primera vez AEM:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Replicar claves para AEM versiones 6.2 y anteriores {#replicating-keys-for-aem-and-older-versions}

En AEM versión 6.2 y anteriores, las claves se almacenan en el repositorio bajo el nodo `/etc/key`.

La manera recomendada de replicar de forma segura las claves en todas las instancias es replicar sólo este nodo. Puede replicar nodos de forma selectiva mediante CRXDE Lite:

1. Para abrir el CRXDE Lite, vaya a *https://&lt;serveraddress>:4502/crx/de/index.jsp*
1. Seleccione el nodo `/etc/key`.
1. Vaya a la ficha **Replicación**.
1. Pulse el botón **Replicación**.

### Realizar una prueba de penetración {#perform-a-penetration-test}

Adobe recomienda encarecidamente realizar una prueba de penetración de su infraestructura AEM antes de continuar con la producción.

### Optimizaciones para el desarrollo {#development-best-practices}

Es fundamental que el nuevo desarrollo siga las [Optimizaciones de seguridad](/help/sites-developing/security.md) para garantizar que su entorno AEM permanezca seguro.
