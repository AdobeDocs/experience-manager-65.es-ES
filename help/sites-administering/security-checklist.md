---
title: Lista de comprobación de seguridad
seo-title: Security Checklist
description: Obtenga información sobre las distintas consideraciones de seguridad al configurar e implementar AEM.
seo-description: Learn about the various security considerations when configuring and deploying AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
source-git-commit: 70c2d7c910f61169869aab9fdcbff4c4564ea9bd
workflow-type: tm+mt
source-wordcount: '2818'
ht-degree: 1%

---

# Lista de comprobación de seguridad {#security-checklist}

Esta sección trata de los distintos pasos que debe realizar para garantizar que la instalación de AEM sea segura cuando se implemente. La lista de comprobación está pensada para aplicarse de arriba a abajo.

>[!NOTE]
>
>También se dispone de más información sobre las amenazas a la seguridad más peligrosas, según la publicación de [Abrir proyecto de seguridad de aplicaciones web (OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>Hay algunas [consideraciones de seguridad](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) aplicable en la fase de desarrollo.

## Medidas de seguridad principales {#main-security-measures}

### Ejecutar AEM en modo listo para producción {#run-aem-in-production-ready-mode}

Para obtener más información, consulte [Ejecución de AEM en el modo Producción lista](/help/sites-administering/production-ready.md).

### Habilite HTTPS para la seguridad de la capa de transporte {#enable-https-for-transport-layer-security}

La activación de la capa de transporte HTTPS en las instancias de autor y publicación es obligatoria para tener una instancia segura.

>[!NOTE]
>
>Consulte la [Habilitación de HTTP en SSL](/help/sites-administering/ssl-by-default.md) para obtener más información.

### Instalar revisiones de seguridad {#install-security-hotfixes}

Asegúrese de haber instalado la última [Revisiones de seguridad proporcionadas por el Adobe](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=es).

### Cambiar contraseñas predeterminadas para las cuentas de administración de la consola AEM y OSGi {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe recomienda después de la instalación que cambie la contraseña de los privilegiados [**AEM** `admin` cuentas](#changing-the-aem-admin-password) (en todas las instancias).

Estas cuentas incluyen:

* El AEM `admin` account

   Después de cambiar la contraseña de la cuenta de administrador de AEM, use la nueva contraseña al acceder a CRX.

* La variable `admin` contraseña para la consola web OSGi

   Este cambio también se aplica a la cuenta de administrador utilizada para acceder a la consola web, por lo que debe utilizar la misma contraseña al acceder a ella.

Estas dos cuentas utilizan credenciales independientes y tener una contraseña segura y distinta para cada una es vital para una implementación segura.

#### Cambio de la contraseña de administrador de AEM {#changing-the-aem-admin-password}

La contraseña de la cuenta de administrador de AEM se puede cambiar mediante la variable [Operaciones de Granite: usuarios](/help/sites-administering/granite-user-group-admin.md) consola.

Aquí puede editar el `admin` cuenta y [cambiar la contraseña](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>Al cambiar la cuenta de administrador también se cambia la cuenta de la consola web OSGi. Después de cambiar la cuenta de administrador, debe cambiar la cuenta de OSGi por otra distinta.

#### Importancia de cambiar la contraseña de la consola web OSGi {#importance-of-changing-the-osgi-web-console-password}

Aparte de la AEM `admin` , si no se cambia la contraseña predeterminada para la contraseña de la consola web OSGi, puede conllevar lo siguiente:

* Exposición del servidor con una contraseña predeterminada durante el inicio y el apagado (que puede tardar minutos en los servidores grandes);
* Exposición del servidor cuando el repositorio está inactivo/reiniciando el paquete - y OSGI se está ejecutando.

Para obtener más información sobre cómo cambiar la contraseña de la consola web, consulte [Cambio de la contraseña de administrador de la consola web OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) más abajo.

#### Cambio de la contraseña de administrador de la consola web OSGi {#changing-the-osgi-web-console-admin-password}

Cambie la contraseña utilizada para acceder a la consola web. Utilice un [Configuración de OSGI](/help/sites-deploying/configuring-osgi.md) para actualizar las siguientes propiedades de la variable **Consola de administración Apache Felix OSGi**:

* **Nombre de usuario** y **Contraseña**, las credenciales para acceder a la consola de gestión web Apache Felix.
La contraseña debe cambiarse *after* la instalación inicial para garantizar la seguridad de su instancia.

>[!NOTE]
>
>Consulte [Configuración de OSGI](/help/sites-deploying/configuring-osgi.md) para obtener información detallada sobre la configuración de OSGi.

**Para cambiar la contraseña de administrador de la consola web OSGi**:

1. Al usar la variable **Herramientas**, **Operaciones** , abra **Consola web** y vaya a la **Configuración** para obtener más información.
Por ejemplo, en `<server>:<port>/system/console/configMgr`.
1. Vaya a la entrada y ábrala para **Consola de administración Apache Felix OSGi**.
1. Cambie el **nombre de usuario** y **password**.

   ![Chlimage_1-3](assets/chlimage_1-3.png)

1. Seleccione **Guardar**.

### Implementar el controlador de errores personalizado {#implement-custom-error-handler}

Adobe recomienda definir páginas de tratamiento de errores personalizadas, especialmente para los códigos de respuesta HTTP 404 y 500 para evitar la divulgación de información.

>[!NOTE]
>
>Consulte [¿Cómo puedo crear scripts personalizados o gestores de errores?](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/custom-error-page.html?lang=en) para obtener más información.

### Lista de comprobación de seguridad completa de Dispatcher {#complete-dispatcher-security-checklist}

AEM Dispatcher es una parte fundamental de su infraestructura. Adobe recomienda completar la [Lista de comprobación de seguridad de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=en).

>[!CAUTION]
>
>Con Dispatcher debe desactivar el selector &quot;.form&quot;.

## Pasos de la verificación {#verification-steps}

### Configuración de usuarios de replicación y transporte {#configure-replication-and-transport-users}

Una instalación estándar de AEM especifica `admin` como usuario para credenciales de transporte dentro del valor predeterminado [agentes de replicación](/help/sites-deploying/replication.md). Además, el usuario administrador se utiliza para originar la replicación en el sistema de creación.

Por motivos de seguridad, ambos deben cambiarse para reflejar el caso de uso particular que se examina, teniendo en cuenta los dos aspectos siguientes:

* La variable **usuario de transporte** no debe ser el usuario administrador. En su lugar, configure un usuario en el sistema de publicación que solo tenga derechos de acceso a las partes relevantes del sistema de publicación y use las credenciales de ese usuario para el transporte.

   Puede empezar desde el usuario receptor de replicación agrupado y configurar los derechos de acceso de este usuario para que coincidan con su situación

* La variable **usuario de replicación** o **Id De Usuario Del Agente** tampoco debe ser el usuario administrador, sino un usuario que solo puede ver el contenido que se replica. El usuario de replicación se utiliza para recopilar el contenido que se replicará en el sistema de creación antes de enviarlo al editor.

### Compruebe las comprobaciones de estado de seguridad del panel de operaciones {#check-the-operations-dashboard-security-health-checks}

AEM 6 presenta el nuevo Tablero de operaciones, destinado a ayudar a los operadores de sistemas a solucionar problemas y controlar el estado de una instancia.

El panel también incluye una colección de comprobaciones de estado de seguridad. Se recomienda comprobar el estado de todas las comprobaciones de estado de seguridad antes de poner en marcha la instancia de producción. Para obtener más información, consulte la [Documentación del panel de operaciones](/help/sites-administering/operations-dashboard.md).

### Comprobar si el contenido de ejemplo está presente {#check-if-example-content-is-present}

Todos los usuarios y el contenido de ejemplo (por ejemplo, el proyecto de Geometrixx y sus componentes) deben desinstalarse y eliminarse completamente en un sistema productivo antes de hacerlo accesible al público.

>[!NOTE]
>
>El ejemplo `We.Retail` las aplicaciones se eliminan si esta instancia se está ejecutando en [Modo listo para la producción](/help/sites-administering/production-ready.md). Si no es así, puede desinstalar el contenido de muestra en el Administrador de paquetes, buscando y desinstalando todo `We.Retail` paquetes.

Consulte [Trabajar Con Paquetes](package-manager.md).

### Compruebe si los paquetes de desarrollo CRX están presentes {#check-if-the-crx-development-bundles-are-present}

Estos paquetes OSGi de desarrollo deben desinstalarse tanto en sistemas productivos de creación como de publicación antes de hacerlos accesibles.

* Compatibilidad con Adobe CRXDE (com.adobe.granite.crxde-support)
* Explorador de Adobe Granite CRX (com.adobe.granite.crx-explorer)
* CRXDE Lite de Adobe Granite (com.adobe.granite.crxde-lite)

### Compruebe si el paquete de desarrollo de Sling está presente {#check-if-the-sling-development-bundle-is-present}

La variable [Herramientas para desarrolladores de AEM](/help/sites-developing/aem-eclipse.md) implemente la instalación de soporte de Apache Sling Tooling (org.apache.sling.tooling.support.install).

Este paquete OSGi debe desinstalarse tanto en sistemas productivos de creación como de publicación antes de hacerlos accesibles.

### Protect contra falsificación de solicitudes entre sitios {#protect-against-cross-site-request-forgery}

#### Marco de protección del CSRF {#the-csrf-protection-framework}

AEM 6.1 se envía con un mecanismo que ayuda a protegerse contra los ataques de falsificación de solicitudes entre sitios, llamados **Marco de protección CSRF**. Para obtener más información sobre cómo utilizarlo, consulte la [documentación](/help/sites-developing/csrf-protection.md).

#### Filtro de referente de Sling {#the-sling-referrer-filter}

Para solucionar problemas de seguridad conocidos con Falsificación de solicitudes entre sitios (CSRF) en CRX WebDAV y Apache Sling, agregue configuraciones para el filtro Referente para utilizarlo.

El servicio de filtro de referente es un servicio OSGi que permite configurar lo siguiente:

* qué métodos http deben filtrarse
* si se permite un encabezado de referente vacío
* y una lista de servidores a permitir además del host del servidor.

   De forma predeterminada, todas las variaciones de localhost y los nombres de host actuales a los que está enlazado el servidor están en la lista.

Para configurar el servicio de filtro de referente:

1. Abra la consola Apache Felix (**Configuraciones**) en:

   `https://<server>:<port_number>/system/console/configMgr`

1. Iniciar sesión como `admin`.
1. En el **Configuraciones** seleccione:

   `Apache Sling Referrer Filter`

1. En el `Allow Hosts` , introduzca todos los hosts permitidos como referente. Cada entrada debe ser del formulario

   &lt;protocol>://&lt;server>:&lt;port>

   Por ejemplo:

   * `https://allowed.server:80` permite todas las solicitudes de este servidor con el puerto determinado.
   * Si también desea permitir solicitudes https, debe introducir una segunda línea.
   * Si permite todos los puertos de ese servidor, puede utilizar `0` como número de puerto.

1. Marque la `Allow Empty` , si desea permitir encabezados de referente vacíos o ausentes.

   >[!CAUTION]
   >
   >Adobe recomienda proporcionar un referente mientras se utilizan herramientas de línea de comandos como `cURL` en lugar de permitir un valor vacío, ya que podría exponer su sistema a ataques de CSRF.

1. Edite los métodos que este filtro utiliza para las comprobaciones con el `Filter Methods` campo .

1. Haga clic en **Guardar** para guardar los cambios.

### Configuración de OSGI {#osgi-settings}

Algunos ajustes de OSGI se establecen de forma predeterminada para permitir una depuración más sencilla de la aplicación. Cambie esta configuración en las instancias productivas de publicación y creación para evitar fugas de información interna en el público.

>[!NOTE]
>
>Todas las configuraciones a continuación, excepto para **Filtro de depuración Day CQ WCM**, se cubren automáticamente con la variable [Modo listo para la producción](/help/sites-administering/production-ready.md). Como tal, Adobe recomienda revisar todos los ajustes antes de implementar la instancia en un entorno productivo.

Para cada uno de los servicios siguientes, se debe cambiar la configuración especificada:

* [Administrador de biblioteca de HTML de Adobe Granite](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * enable **Minificar** (para eliminar los caracteres CRLF y los espacios en blanco).
   * enable **Gzip** (para permitir que se comprueben los archivos y se acceda a ellos con una solicitud).
   * disable **Depuración**
   * disable **Temporización**

* [Filtro de depuración Day CQ WCM](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * desmarcar **Habilitar**

* [Filtro WCM Day CQ](/help/sites-deploying/osgi-configuration-settings.md):

   * en publicar solamente, establezca **Modo WCM** a &quot;deshabilitado&quot;

* [Controlador JavaScript de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * disable **Generar información de depuración**

* [Controlador de scripts JSP de Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * disable **Generar información de depuración**
   * disable **Contenido asignado**

Consulte [Ajustes de configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md).

Al trabajar con AEM, existen varios métodos para administrar los ajustes de configuración de dichos servicios; see [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

## Lecturas adicionales {#further-readings}

### Mitigar ataques de denegación de servicio (DoS) {#mitigate-denial-of-service-dos-attacks}

Un ataque de denegación de servicio (DoS) es un intento de hacer que un recurso de equipo no esté disponible para los usuarios a los que va destinado. Este ataque se realiza a menudo sobrecargando el recurso; por ejemplo:

* Un flujo de solicitudes de una fuente externa.
* Solicitud de más información de la que el sistema puede entregar correctamente.

   Por ejemplo, una representación JSON de todo el repositorio.

* Al solicitar una página de contenido con un número ilimitado de direcciones URL, la dirección URL puede incluir un control, algunos selectores, una extensión y un sufijo, cualquiera de los cuales se puede modificar.

   Por ejemplo, `.../en.html` también se puede solicitar como:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   Todas las variaciones válidas (por ejemplo, devuelve un valor `200` y están configurados para ser almacenados en caché) son almacenados en caché por Dispatcher, lo que finalmente conduce a un sistema de archivos completo y no hay servicio para solicitudes adicionales.

Hay muchos puntos de configuración para prevenir estos ataques, pero solamente los puntos que se relacionan con AEM se discuten aquí.

**Configuración de Sling para evitar DoS**

Sling es *centrado en el contenido*. El procesamiento se centra en el contenido, ya que cada solicitud (HTTP) se asigna al contenido en forma de recurso JCR (un nodo de repositorio):

* El primer destino es el recurso (nodo JCR) que contiene el contenido.
* En segundo lugar, el renderizador o la secuencia de comandos se encuentran en las propiedades del recurso con ciertas partes de la solicitud (por ejemplo, selectores o la extensión).

Consulte [Procesamiento de solicitudes de Sling](/help/sites-developing/the-basics.md#sling-request-processing) para obtener más información.

Este enfoque hace que Sling sea potente y flexible, pero como siempre es la flexibilidad que debe administrarse cuidadosamente.

Para evitar el uso indebido de DoS, puede hacer lo siguiente:

1. Incorpore controles en el nivel de aplicación. Debido al número de variaciones posibles, no es posible una configuración predeterminada.

   En su aplicación debe:

   * Controle los selectores en la aplicación, de modo que *only* servir los selectores explícitos necesarios y devolver `404` para todos los demás.
   * Impida la salida de un número ilimitado de nodos de contenido.

1. Compruebe la configuración de los procesadores predeterminados, que puede ser un área problemática.

   * En concreto, el renderizador JSON transfiere la estructura de árbol a varios niveles.

      Por ejemplo, la solicitud:

      `http://localhost:4502/.json`

      podría volcar todo el repositorio en una representación JSON que puede causar problemas importantes en el servidor. Por este motivo, Sling establece un límite en el número de resultados máximos. Para limitar la profundidad de la renderización JSON, establezca el valor para lo siguiente:

      **Resultados máximos de JSON** ( `json.maximumresults`)

      en la configuración de [Servlet de GET Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Cuando se supera este límite, el procesamiento se contrae. El valor predeterminado de Sling en AEM es `1000`.

   * Como medida preventiva, debe deshabilitar los demás procesadores predeterminados (HTML, texto sin formato, XML). De nuevo, configurando la variable [Servlet de GET Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >No deshabilite el procesador JSON porque es necesario para el funcionamiento normal de AEM.

1. Utilice un cortafuegos para filtrar el acceso a la instancia.

   * El uso de un cortafuegos a nivel de sistema operativo es necesario para filtrar el acceso a los puntos de la instancia que pueden provocar ataques de denegación de servicio si se dejan sin proteger.

**Mitigar frente a errores causados por el uso de selectores de formularios**

>[!NOTE]
>
>Esta mitigación solo debe realizarse en entornos AEM que no utilicen Forms.

Debido a que AEM no proporciona índices predeterminados para la variable `FormChooserServlet`, el uso de selectores de formularios en las consultas puede producir el déclencheur de una travesía costosa del repositorio, normalmente paralizando la instancia de AEM. Los selectores de formularios se pueden detectar con la presencia de **&amp;ast;.form.&amp;ast;** en las consultas.

Para mitigar este problema, puede realizar los siguientes pasos:

1. Vaya a la consola web señalando el navegador a *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Buscar **Servlet de selector de formularios CQ WCM Day**
1. Después de hacer clic en la entrada, desactive la **Requisito de búsqueda avanzada** en la siguiente ventana.

1. Haga clic en **Guardar**.

**Mitigar frente a errores causados por el servlet de descarga de recursos**

El servlet predeterminado de descarga de recursos permite a los usuarios autenticados emitir solicitudes de descarga concurrentes y arbitrariamente grandes para crear archivos ZIP de recursos. La creación de archivos ZIP de gran tamaño puede sobrecargar el servidor y la red. Para mitigar el riesgo potencial de denegación de servicio (DoS) causado por este comportamiento, `AssetDownloadServlet` El componente OSGi está deshabilitado de forma predeterminada en [!DNL Experience Manager] publicar instancia. Está activado [!DNL Experience Manager] instancia de autor de forma predeterminada.

Si no necesita la capacidad de descarga, deshabilite el servlet en las implementaciones de autor y publicación. Si la configuración requiere que la capacidad de descarga de recursos esté habilitada, consulte [este artículo](/help/assets/download-assets-from-aem.md) para obtener más información. Además, puede definir un límite máximo de descarga que su implementación pueda admitir.

### Deshabilitar WebDAV {#disable-webdav}

Deshabilite WebDAV en los entornos de autor y publicación deteniendo los paquetes OSGi adecuados.

1. Conéctese a la **Consola de administración Felix** en ejecución:

   `https://<*host*>:<*port*>/system/console`

   Por ejemplo, `http://localhost:4503/system/console/bundles`.

1. En la lista de paquetes, busque el paquete llamado:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Para detener este paquete, en la columna Actions , haga clic en el botón stop .

1. De nuevo, en la lista de paquetes, busque el paquete llamado:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Para detener este paquete, haga clic en el botón stop .

   >[!NOTE]
   >
   >No es necesario reiniciar el AEM.

### Compruebe que no está revelando información de identificación personal en la ruta principal de los usuarios {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

Es importante proteger a los usuarios asegurándose de que no exponga ninguna información personal identificable en la ruta principal del repositorio para los usuarios.

Desde AEM 6.1, la forma en que se almacenan los nombres de nodo de ID de usuario (también conocidos como autorizables) cambia con una nueva implementación de la variable `AuthorizableNodeName` interfaz. La nueva interfaz ya no expone el ID de usuario en el nombre del nodo, sino que genera un nombre aleatorio.

No se debe realizar ninguna configuración para habilitarla, ya que ahora es la forma predeterminada de generar ID autorizables en AEM.

Aunque no se recomienda, puede deshabilitarla en caso de que necesite la implementación antigua para la compatibilidad con versiones anteriores con sus aplicaciones existentes. Para ello, debe hacer lo siguiente:

1. Vaya a la consola web y elimine la entrada** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** de la propiedad **requiredServicePids** en **Proveedor de seguridad de Apache Jackrabbit Oak**.

   También puede encontrar el proveedor de seguridad de Oak buscando la variable **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID en las configuraciones de OSGi.

1. Elimine el **Nombre de nodo autorizado aleatorio de Apache Jackrabbit Oak** Configuración de OSGi desde la consola web.

   Para facilitar la búsqueda, el PID de esta configuración es **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Para obtener más información, consulte la documentación de Oak sobre [Generación de nombres de nodo autorizada](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Impedir el clickjacking {#prevent-clickjacking}

Para evitar el secuestro de clics, Adobe recomienda configurar el servidor web para que proporcione la variable `X-FRAME-OPTIONS` El encabezado HTTP está configurado en `SAMEORIGIN`.

Para obtener más información sobre el secuestro de clics, consulte la [Sitio OWASP](https://www.owasp.org/index.php/Clickjacking).

### Asegúrese De Replicar Correctamente Las Claves De Cifrado Cuando Sea Necesario {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Algunas funciones de AEM y esquemas de autenticación requieren que duplique las claves de cifrado en todas las instancias de AEM.

Antes de hacerlo, la replicación de claves se realiza de forma diferente entre versiones, ya que la forma en que se almacenan las claves es diferente entre la versión 6.3 y las anteriores.

Consulte a continuación para obtener más información.

#### Duplicación de claves para AEM 6.3 {#replicating-keys-for-aem}

Mientras que en versiones anteriores las claves de replicación se almacenaban en el repositorio, comenzando con AEM 6.3, se almacenan en el sistema de archivos.

Por lo tanto, para replicar las claves en las instancias, cópielas desde la instancia de origen a la ubicación de las instancias de destino en el sistema de archivos.

Más específicamente, debe hacer lo siguiente:

1. Acceda a la instancia de AEM (normalmente una instancia de autor) que contiene el material clave que se va a copiar.
1. Busque el paquete com.adobe.granite.crypto.file en el sistema de archivos local. Por ejemplo, en esta ruta:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   La variable `bundle.info` dentro de cada carpeta identifica el nombre del paquete.

1. Vaya a la carpeta de datos. Por ejemplo:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copie los archivos HMAC y maestro.
1. A continuación, vaya a la instancia de destino a la que desee duplicar la clave HMAC y vaya a la carpeta de datos. Por ejemplo:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Pegue los dos archivos que ha copiado anteriormente.
1. [Actualizar el paquete criptográfico](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) si la instancia de destino ya se está ejecutando.
1. Repita los pasos anteriores para todas las instancias en las que desee replicar la clave.

>[!NOTE]
>
>Puede volver al método pre-6.3 de almacenamiento de claves añadiendo el siguiente parámetro al instalar por primera vez AEM:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Duplicación de claves para AEM 6.2 y versiones anteriores {#replicating-keys-for-aem-and-older-versions}

En AEM versión 6.2 y anteriores, las claves se almacenan en el repositorio bajo el `/etc/key` nodo .

La manera recomendada de replicar las claves de forma segura en todas las instancias es replicar solo este nodo. Puede replicar nodos selectivamente mediante el CRXDE Lite:

1. Abra el CRXDE Lite yendo a *`https://&lt;serveraddress&gt;:4502/crx/de/index.jsp`*
1. Seleccione el `/etc/key` nodo .
1. Vaya a la **Replicación** pestaña .
1. Pulse el botón **Replicación** botón.

### Realizar una prueba de penetración {#perform-a-penetration-test}

Adobe recomienda realizar una prueba de penetración de su infraestructura de AEM antes de continuar con la producción.

### Prácticas recomendadas de desarrollo {#development-best-practices}

Es fundamental que los nuevos avances sigan el [Prácticas recomendadas de seguridad](/help/sites-developing/security.md) para garantizar que el entorno de AEM permanezca seguro.
