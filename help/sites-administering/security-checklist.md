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
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '2842'
ht-degree: 0%

---

# Lista de comprobación de seguridad {#security-checklist}

Esta sección trata de los distintos pasos que debe realizar para garantizar que la instalación de AEM sea segura cuando se implemente. La lista de comprobación está pensada para aplicarse de arriba a abajo.

>[!NOTE]
>
>También está disponible más información [sobre las amenazas de seguridad más peligrosas publicadas por Open Web Application Security Project (OWASP)](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).

>[!NOTE]
>
>Hay algunas [consideraciones de seguridad](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) adicionales aplicables en la fase de desarrollo.

## Medidas de seguridad principales {#main-security-measures}

### Ejecutar AEM en modo Producción lista {#run-aem-in-production-ready-mode}

Para obtener más información, consulte [Ejecución de AEM en modo listo para la producción](/help/sites-administering/production-ready.md).

### Habilitar HTTPS para la seguridad de capa de transporte {#enable-https-for-transport-layer-security}

La activación de la capa de transporte HTTPS en las instancias de autor y publicación es obligatoria para tener una instancia segura.

>[!NOTE]
>
>Consulte la sección [Activación de HTTP sobre SSL](/help/sites-administering/ssl-by-default.md) para obtener más información.

### Instalar revisiones de seguridad {#install-security-hotfixes}

Asegúrese de que ha instalado las [revisiones de seguridad más recientes proporcionadas por Adobe](https://helpx.adobe.com/es/experience-manager/kb/aem63-available-hotfixes.html).

### Cambiar contraseñas predeterminadas para las cuentas de administración de la consola AEM y OSGi {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe recomienda encarecidamente que después de la instalación cambie la contraseña de las cuentas [**AEM** `admin` privilegiadas](#changing-the-aem-admin-password) (en todas las instancias).

Estas cuentas incluyen:

* La cuenta de AEM `admin`

   Una vez que haya cambiado la contraseña de la cuenta de administrador de AEM, deberá utilizar la nueva contraseña al acceder a CRX.

* La contraseña `admin` para la consola web OSGi

   Este cambio también se aplicará a la cuenta de administrador utilizada para acceder a la consola web, por lo que deberá utilizar la misma contraseña al acceder a ella.

Estas dos cuentas utilizan credenciales independientes y tener una contraseña segura y distinta para cada una es vital para una implementación segura.

#### Cambio de la contraseña de administrador de AEM {#changing-the-aem-admin-password}

La contraseña de la cuenta de administrador de AEM se puede cambiar a través de la consola [Operaciones de Granite - Usuarios](/help/sites-administering/granite-user-group-admin.md).

Aquí puede editar la cuenta `admin` y [cambiar la contraseña](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>Al cambiar la cuenta de administrador también se cambia la cuenta de la consola web OSGi. Después de cambiar la cuenta de administrador, debe cambiar la cuenta de OSGi por otra distinta.

#### Importancia de cambiar la contraseña de la consola web OSGi {#importance-of-changing-the-osgi-web-console-password}

Además de la cuenta de AEM `admin`, si no se cambia la contraseña predeterminada para la contraseña de la consola web OSGi, puede provocar lo siguiente:

* Exposición del servidor con una contraseña predeterminada durante el inicio y el apagado (que puede tardar minutos en los servidores grandes);
* Exposición del servidor cuando el repositorio está inactivo/reiniciando el paquete - y OSGI se está ejecutando.

Para obtener más información sobre cómo cambiar la contraseña de la consola web, consulte [Cambio de la contraseña de administrador de la consola web OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) a continuación.

#### Cambio de la contraseña de administrador de la consola web OSGi {#changing-the-osgi-web-console-admin-password}

También debe cambiar la contraseña utilizada para acceder a la consola web. Esto se hace configurando las siguientes propiedades de la Consola de administración [Apache Felix OSGi](/help/sites-deploying/osgi-configuration-settings.md):

**Nombre** de usuario y  **contraseña**, las credenciales para acceder a la Consola de gestión web Apache Felix.
La contraseña debe cambiarse después de la instalación inicial para garantizar la seguridad de la instancia.

Para ello:

1. Vaya a la consola web en `<server>:<port>/system/console/configMgr`.
1. Vaya a la **Consola de administración Apache Felix OSGi** y cambie el **nombre de usuario** y la **contraseña**.

   ![Chlimage_1-3](assets/chlimage_1-3.png)

1. Haga clic en **Guardar**.

### Implementar el controlador de error personalizado {#implement-custom-error-handler}

Adobe recomienda definir las páginas de tratamiento de errores personalizadas, especialmente para los códigos de respuesta HTTP 404 y 500 para evitar la divulgación de información.

>[!NOTE]
>
>Consulte el artículo [Cómo puedo crear secuencias de comandos personalizadas o controladores de errores](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) de la base de conocimiento para obtener más información.

### Lista de comprobación de seguridad completa de Dispatcher {#complete-dispatcher-security-checklist}

AEM Dispatcher es una parte fundamental de su infraestructura. Adobe recomienda encarecidamente que complete la [lista de comprobación de seguridad del despachante](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=es#getting-started).

>[!CAUTION]
>
>Con Dispatcher debe desactivar el selector &quot;.form&quot;.

## Pasos de verificación {#verification-steps}

### Configuración de usuarios de replicación y transporte {#configure-replication-and-transport-users}

Una instalación estándar de AEM especifica `admin` como usuario para las credenciales de transporte dentro de los [agentes de replicación](/help/sites-deploying/replication.md) predeterminados. Además, el usuario administrador se utiliza para originar la replicación en el sistema de creación.

Por motivos de seguridad, ambos deben cambiarse para reflejar el caso de uso particular que se examina, teniendo en cuenta los dos aspectos siguientes:

* El **usuario de transporte** no debe ser el usuario administrador. En su lugar, configure un usuario en el sistema de publicación que solo tenga derechos de acceso a las partes relevantes del sistema de publicación y use las credenciales de ese usuario para el transporte.

   Puede empezar desde el usuario receptor de replicación agrupado y configurar los derechos de acceso de este usuario para que coincidan con su situación

* El **usuario de replicación** o **Id de usuario del agente** no debe ser el usuario administrador, sino un usuario que solo puede ver el contenido que se supone que debe replicarse. El usuario de replicación se utiliza para recopilar el contenido que se replicará en el sistema de creación antes de enviarlo al editor.

### Compruebe las comprobaciones de estado de seguridad del panel de operaciones {#check-the-operations-dashboard-security-health-checks}

AEM 6 presenta el nuevo Tablero de operaciones, destinado a ayudar a los operadores de sistemas a solucionar problemas y controlar el estado de una instancia.

El panel también incluye una colección de comprobaciones de estado de seguridad. Se recomienda comprobar el estado de todas las comprobaciones de estado de seguridad antes de poner en marcha la instancia de producción. Para obtener más información, consulte la [Documentación del panel de operaciones](/help/sites-administering/operations-dashboard.md).

### Compruebe si el contenido de ejemplo está presente {#check-if-example-content-is-present}

Todos los usuarios y el contenido de ejemplo (por ejemplo, el proyecto de Geometrixx y sus componentes) deben desinstalarse y eliminarse completamente en un sistema productivo antes de que sea accesible al público.

>[!NOTE]
>
>Las aplicaciones We.Retail de muestra se eliminan si esta instancia se ejecuta en [Production Ready Mode](/help/sites-administering/production-ready.md). Si, por cualquier razón, este no es el caso, puede desinstalar el contenido de muestra yendo al Administrador de paquetes, buscando y desinstalando todos los paquetes de We.Retail. Para obtener más información, consulte [Trabajo con paquetes](package-manager.md).

### Compruebe si los paquetes de desarrollo CRX están presentes {#check-if-the-crx-development-bundles-are-present}

Estos paquetes OSGi de desarrollo deben desinstalarse tanto en sistemas productivos de creación como de publicación antes de hacerlos accesibles.

* Compatibilidad con Adobe CRXDE (com.adobe.granite.crxde-support)
* Explorador de Adobe Granite CRX (com.adobe.granite.crx-explorer)
* CRXDE Lite de Adobe Granite (com.adobe.granite.crxde-lite)

### Compruebe si el paquete de desarrollo de Sling está presente {#check-if-the-sling-development-bundle-is-present}

Las [AEM herramientas para desarrolladores de Eclipse](/help/sites-developing/aem-eclipse.md) implementan la instalación de soporte de herramientas Apache Sling (org.apache.sling.tooling.support.install).

Este paquete OSGi debe desinstalarse tanto en sistemas productivos de creación como de publicación antes de hacerlos accesibles.

### Protect contra falsificación de solicitudes entre sitios {#protect-against-cross-site-request-forgery}

#### El marco de protección del CSRF {#the-csrf-protection-framework}

AEM 6.1 se envía con un mecanismo que ayuda a protegerse contra los ataques de falsificación de solicitudes entre sitios, llamados **CSRF Protection Framework**. Para obtener más información sobre cómo utilizarla, consulte la [documentación](/help/sites-developing/csrf-protection.md).

#### El filtro de referente de Sling {#the-sling-referrer-filter}

Para solucionar problemas de seguridad conocidos con la falsificación de solicitudes entre sitios (CSRF) en CRX WebDAV y Apache Sling, debe añadir configuraciones para el filtro Referente para utilizarlo.

El servicio de filtro de referente es un servicio OSGi que le permite configurar:

* qué métodos http deben filtrarse
* si se permite un encabezado de referente vacío
* y una lista de servidores a permitir además del host del servidor.

   De forma predeterminada, todas las variaciones de localhost y los nombres de host actuales a los que está enlazado el servidor están en la lista.

Para configurar el servicio de filtro de referente:

1. Abra la consola Apache Felix (**Configurations**) en:

   `https://<server>:<port_number>/system/console/configMgr`

1. Inicie sesión como `admin`.
1. En el menú **Configurations**, seleccione:

   `Apache Sling Referrer Filter`

1. En el campo `Allow Hosts`, introduzca todos los hosts permitidos como referente. Cada entrada debe ser del formulario

   &lt;protocol>://&lt;server>:&lt;port>

   Por ejemplo:

   * `https://allowed.server:80` permite todas las solicitudes de este servidor con el puerto determinado.
   * Si también desea permitir solicitudes https, debe introducir una segunda línea.
   * Si permite todos los puertos de ese servidor, puede utilizar `0` como número de puerto.

1. Compruebe el campo `Allow Empty` si desea permitir encabezados de referente vacíos o que faltan.

   >[!CAUTION]
   >
   >Se recomienda proporcionar un referente mientras se utilizan herramientas de línea de comandos como `cURL` en lugar de permitir un valor vacío, ya que podría exponer su sistema a ataques de CSRF.

1. Edite los métodos que este filtro debe utilizar para las comprobaciones con el campo `Filter Methods` .

1. Haga clic en **Guardar** para guardar los cambios.

### Configuración OSGI {#osgi-settings}

Algunos ajustes de OSGI se establecen de forma predeterminada para permitir una depuración más sencilla de la aplicación. Es necesario cambiar estas instancias en las instancias productivas de publicación y creación para evitar fugas de información interna en el público.

>[!NOTE]
>
>Todos los ajustes siguientes, con la excepción de **The Day CQ WCM Debug Filter**, se cubren automáticamente con el [Modo preparado para la producción](/help/sites-administering/production-ready.md). Debido a esto, recomendamos revisar todos los ajustes antes de implementar la instancia en un entorno productivo.

Para cada uno de los siguientes servicios, es necesario cambiar la configuración especificada:

* [Administrador de bibliotecas HTML de Adobe Granite](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * habilite **Minificar** (para eliminar los caracteres CRLF y los espacios en blanco).
   * habilite **Gzip** (para permitir que se comprueben los archivos y se acceda a ellos mediante una solicitud).
   * deshabilitar **Depurar**
   * deshabilitar **Temporización**

* [Filtro](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter) de depuración de CQ WCM de día:

   * desmarque **Habilitar**

* [Filtro WCM Day CQ](/help/sites-deploying/osgi-configuration-settings.md):

   * en solo publicación, establezca **WCM Mode** en &quot;disabled&quot;

* [Controlador de Java Script de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * deshabilitar **Generar información de depuración**

* [Controlador de script JSP de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * deshabilitar **Generar información de depuración**
   * deshabilitar **Contenido asignado**

Para obtener más información, consulte [Configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md).

Al trabajar con AEM hay varios métodos para administrar los ajustes de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

## Lecturas adicionales {#further-readings}

### Mitigar los ataques de denegación de servicio (DoS) {#mitigate-denial-of-service-dos-attacks}

Un ataque de denegación de servicio (DoS) es un intento de hacer que un recurso de equipo no esté disponible para los usuarios a los que va destinado. Esto suele hacerse sobrecargando el recurso; por ejemplo:

* Con un flujo de solicitudes de una fuente externa.
* Con una solicitud de más información de la que el sistema puede entregar correctamente.

   Por ejemplo, una representación JSON de todo el repositorio.

* Al solicitar una página de contenido con un número ilimitado de direcciones URL, la dirección URL puede incluir un control, algunos selectores, una extensión y un sufijo, cualquiera de los cuales se puede modificar.

   Por ejemplo, `.../en.html` también se puede solicitar como:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   Todas las variaciones válidas (por ejemplo, devolver una respuesta `200` y están configuradas para almacenarse en caché) serán almacenadas en caché por el despachante, lo que finalmente dará lugar a un sistema de archivos completo y a que no se proporcione ningún servicio para solicitudes adicionales.

Hay muchos puntos de configuración para prevenir estos ataques, aquí solamente discutimos los relacionados directamente con AEM.

**Configuración de Sling para evitar DoS**

Sling es *centrado en el contenido*. Esto significa que el procesamiento se centra en el contenido, ya que cada solicitud (HTTP) se asigna al contenido en forma de recurso JCR (un nodo de repositorio):

* El primer destino es el recurso (nodo JCR) que contiene el contenido.
* En segundo lugar, el renderizador, o secuencia de comandos, se encuentra desde las propiedades del recurso en combinación con ciertas partes de la solicitud (por ejemplo, selectores o la extensión).

>[!NOTE]
>
>Esto se trata con más detalle en [Sling Request Processing](/help/sites-developing/the-basics.md#sling-request-processing).

Este enfoque hace que Sling sea muy potente y muy flexible, pero como siempre es la flexibilidad que necesita ser administrada cuidadosamente.

Para ayudar a evitar el uso indebido de DoS, puede:

1. Incorporar controles a nivel de aplicación; debido al número de variaciones posible, no es factible una configuración predeterminada.

   En su aplicación debe:

   * Controle los selectores de la aplicación, de modo que *solo* proporcione los selectores explícitos necesarios y devuelva `404` los demás.
   * Impida la salida de un número ilimitado de nodos de contenido.

1. Compruebe la configuración de los procesadores predeterminados, que puede ser un área problemática.

   * En concreto, el procesador JSON que puede invertir la estructura de árbol en varios niveles.

      Por ejemplo, la solicitud:

      `http://localhost:4502/.json`

      podría volcar todo el repositorio en una representación JSON. Esto causaría problemas importantes en el servidor. Por este motivo, Sling establece un límite en el número de resultados máximos. Para limitar la profundidad de la renderización JSON, puede establecer el valor para:

      **Resultados**  máximos de JSON(  `json.maximumresults`)

      en la configuración del [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Cuando se supera este límite, se contraerá el procesamiento. El valor predeterminado para Sling dentro de AEM es `200`.

   * Como medida preventiva, desactive los demás procesadores predeterminados (HTML, texto sin formato, XML). Una vez más, configurando el [Servlet de GET Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >No deshabilite el procesador JSON, esto es necesario para el funcionamiento normal de AEM.

1. Utilice un cortafuegos para filtrar el acceso a la instancia.

   * El uso de un cortafuegos a nivel de sistema operativo es necesario para filtrar el acceso a los puntos de la instancia que pueden provocar ataques de denegación de servicio si se dejan sin proteger.

**Mitigar frente a errores causados por el uso de selectores de formularios**

>[!NOTE]
>
>Esta mitigación solo debe realizarse en entornos AEM que no utilicen Forms.

Dado que AEM no proporciona índices predeterminados para el `FormChooserServlet`, el uso de selectores de formularios en las consultas déclencheur una travesía costosa del repositorio, que normalmente reduce la instancia de AEM a una parada. Los selectores de formularios se pueden detectar con la presencia del formulario **&amp;ast;.form.&amp;ast;** cadena en consultas.

Para mitigar esto, siga los siguientes pasos:

1. Vaya a la consola web señalando su navegador a *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Busque **Day CQ WCM Form Chooslet**
1. Después de hacer clic en la entrada, desactive el **Requisito de búsqueda avanzada** en la siguiente ventana.

1. Haga clic en **Guardar**.

**Mitigar frente a errores causados por el servlet de descarga de recursos**

El servlet de descarga de recursos predeterminado en AEM permite que los usuarios autenticados emitan solicitudes de descarga concurrentes de gran tamaño arbitrario para crear archivos ZIP de recursos visibles para ellos que puedan sobrecargar el servidor o la red.

Para mitigar los posibles riesgos de DoS causados por esta función, el componente `AssetDownloadServlet` OSGi está deshabilitado de forma predeterminada para las instancias de publicación en las últimas versiones de AEM.

Si la configuración requiere que el servidor de descarga de recursos esté habilitado, consulte [este artículo](/help/assets/download-assets-from-aem.md) para obtener más información.

### Deshabilitar WebDAV {#disable-webdav}

WebDAV debe deshabilitarse en los entornos de autor y publicación. Esto se puede hacer deteniendo los paquetes OSGi adecuados.

1. Conéctese a la Consola de administración **Felix** que se ejecuta en:

   `https://<*host*>:<*port*>/system/console`

   Por ejemplo `http://localhost:4503/system/console/bundles`.

1. En la lista de paquetes, busque el paquete llamado:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Haga clic en el botón de parada (en la columna Actions ) para detener este paquete.

1. De nuevo en la lista de paquetes, busque el paquete llamado:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Haga clic en el botón stop para detener este paquete.

   >[!NOTE]
   >
   >No es necesario reiniciar el AEM.

### Compruebe Que No Está Mostrando Información De Identificación Personal En La Ruta Principal {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path} De Los Usuarios

Es importante que proteja a sus usuarios asegurándose de que no expone ninguna información personal identificable en la ruta de inicio del repositorio para los usuarios.

Desde AEM 6.1, la forma en que se almacenan los nombres de nodo de ID de usuario (también conocidos como autorizables) cambia con una nueva implementación de la interfaz `AuthorizableNodeName` . La nueva interfaz ya no mostrará el ID de usuario en el nombre del nodo, pero en su lugar generará un nombre aleatorio.

No es necesario realizar ninguna configuración para habilitarla, ya que esta es la forma predeterminada de generar ID autorizables en AEM.

Aunque no se recomienda, puede deshabilitarla en caso de que necesite la implementación antigua para la compatibilidad con versiones anteriores con sus aplicaciones existentes. Para ello, debe:

1. Vaya a la consola web y elimine la entrada** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** de la propiedad **requiredServicePids** en **Apache Jackrabbit Oak SecurityProvider**.

   También puede encontrar el proveedor de seguridad de Oak buscando el **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID en las configuraciones de OSGi.

1. Elimine la configuración OSGi **Apache Jackrabbit Oak Random Authorizable Node Name** de la consola web.

   Para facilitar la búsqueda, tenga en cuenta que el PID de esta configuración es **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Para obtener más información, consulte la documentación de Oak sobre [Generación de nombres de nodos autorizables](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Impedir el secuestro de clics {#prevent-clickjacking}

Para evitar el secuestro de clics, le recomendamos que configure su servidor web para que proporcione el encabezado `X-FRAME-OPTIONS` HTTP establecido en `SAMEORIGIN`.

Para obtener más [información sobre el secuestro de clics, consulte el sitio OWASP](https://www.owasp.org/index.php/Clickjacking).

### Asegúrese de replicar correctamente las claves de cifrado cuando sea necesario {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Algunas funciones de AEM y esquemas de autenticación requieren que duplique las claves de cifrado en todas las instancias de AEM.

Antes de hacer esto, tenga en cuenta que la replicación de claves se realiza de forma diferente entre versiones, ya que la forma en que se almacenan las claves es diferente entre la versión 6.3 y las anteriores.

Consulte a continuación para obtener más información.

#### Duplicación de claves para AEM 6.3 {#replicating-keys-for-aem}

Mientras que en versiones anteriores las claves de replicación se almacenaban en el repositorio, comenzando con AEM 6.3, se almacenan en el sistema de archivos.

Por lo tanto, para poder replicar las claves en todas las instancias, debe copiarlas desde la instancia de origen a la ubicación de las instancias de destino en el sistema de archivos.

Más específicamente, debe:

1. Acceda a la instancia de AEM, normalmente una instancia de autor, que contiene el material clave que se va a copiar;
1. Busque el paquete com.adobe.granite.crypto.file en el sistema de archivos local. Por ejemplo, en esta ruta:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   El archivo `bundle.info` dentro de cada carpeta identificará el nombre del paquete.

1. Vaya a la carpeta de datos. Por ejemplo:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copie los archivos HMAC y maestro.
1. A continuación, vaya a la instancia de destino a la que desee duplicar la clave HMAC y vaya a la carpeta de datos. Por ejemplo:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Pegue los dos archivos que ha copiado anteriormente.
1. [Actualice Crypto ](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) Bundlesi la instancia de destino ya se está ejecutando.
1. Repita los pasos anteriores para todas las instancias en las que desee replicar la clave.

>[!NOTE]
>
>Puede volver al método de almacenamiento de claves pre 6.3 añadiendo el siguiente parámetro cuando instale por primera vez AEM:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Duplicación de claves para AEM 6.2 y versiones anteriores {#replicating-keys-for-aem-and-older-versions}

En AEM versión 6.2 y anteriores, las claves se almacenan en el repositorio bajo el nodo `/etc/key`.

La manera recomendada de replicar las claves de forma segura en todas las instancias es replicar solo este nodo. Puede replicar nodos selectivamente mediante el CRXDE Lite:

1. Abra el CRXDE Lite en *https://&lt;serveraddress>:4502/crx/de/index.jsp*
1. Seleccione el nodo `/etc/key`.
1. Vaya a la pestaña **Replication**.
1. Pulse el botón **Replication**.

### Realizar una prueba de penetración {#perform-a-penetration-test}

Adobe recomienda encarecidamente realizar una prueba de penetración de su infraestructura de AEM antes de continuar con la producción.

### Prácticas recomendadas de desarrollo {#development-best-practices}

Es fundamental que el nuevo desarrollo siga las [Prácticas recomendadas de seguridad](/help/sites-developing/security.md) para garantizar que el entorno AEM permanezca seguro.
