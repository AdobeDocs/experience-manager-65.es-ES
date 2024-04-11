---
title: Lista de comprobación de seguridad
description: AEM Obtenga información acerca de las distintas consideraciones de seguridad al configurar e implementar la implementación de los elementos de seguridad de la aplicación
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '2959'
ht-degree: 0%

---

# Lista de comprobación de seguridad {#security-checklist}

AEM En esta sección se explican varios pasos que debe seguir para asegurarse de que la instalación de la sea segura cuando se implemente. La lista de comprobación debe aplicarse de arriba a abajo.

>[!NOTE]
>
>También hay disponible más información sobre las amenazas de seguridad más peligrosas publicadas por [Abrir proyecto de seguridad de aplicaciones web (OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>Hay algunos más [consideraciones de seguridad](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) aplicable en la fase de desarrollo.

## Principales medidas de seguridad {#main-security-measures}

### AEM Ejecutar en modo listo para la producción {#run-aem-in-production-ready-mode}

Para obtener más información, consulte [AEM Ejecución en modo listo para la producción](/help/sites-administering/production-ready.md).

### Habilite HTTPS para la seguridad de la capa de transporte {#enable-https-for-transport-layer-security}

Habilitar la capa de transporte HTTPS en las instancias de autor y publicación es obligatorio para tener una instancia segura.

>[!NOTE]
>
>Consulte la [Habilitar HTTP sobre SSL](/help/sites-administering/ssl-by-default.md) para obtener más información.

### Instalar revisiones de seguridad {#install-security-hotfixes}

Asegúrese de que ha instalado la última versión [Revisiones de seguridad proporcionadas por el Adobe](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=es).

### AEM Cambiar contraseñas predeterminadas para las cuentas de administrador de la consola OSGi y de la {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe recomienda después de la instalación que cambie la contraseña de los privilegiados [**AEM** `admin` cuentas](#changing-the-aem-admin-password) (en todas las instancias).

Estas cuentas incluyen:

* AEM El `admin` account

  AEM Una vez que haya cambiado la contraseña de la cuenta de administrador de, utilice la nueva contraseña al acceder a CRX.

* El `admin` contraseña para la consola web OSGi

  Este cambio también se aplica a la cuenta de administrador utilizada para acceder a la consola web, por lo que debe utilizar la misma contraseña al acceder a ella.

Estas dos cuentas utilizan credenciales independientes y tener una contraseña segura y distinta para cada una es vital para una implementación segura.

#### AEM Cambio de la contraseña de administrador de la {#changing-the-aem-admin-password}

AEM La contraseña de la cuenta de administrador de la se puede cambiar mediante la variable [Operaciones de Granite: usuarios](/help/sites-administering/granite-user-group-admin.md) consola.

Aquí puede editar la variable `admin` cuenta y [cambiar la contraseña](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>Al cambiar la cuenta de administrador también se cambia la cuenta de la consola web de OSGi. Después de cambiar la cuenta de administrador, debe cambiar la cuenta OSGi a algo diferente.

#### Importancia de cambiar la contraseña de la consola web de OSGi {#importance-of-changing-the-osgi-web-console-password}

AEM Aparte de la `admin` , si no se cambia la contraseña predeterminada para la contraseña de la consola web OSGi, puede provocar lo siguiente:

* Exposición del servidor con una contraseña predeterminada durante el inicio y el apagado (que puede tardar minutos en servidores grandes);
* Exposición del servidor cuando el repositorio está inactivo/reiniciando el paquete: y OSGI se está ejecutando.

Para obtener más información sobre cómo cambiar la contraseña de la consola web, consulte [Cambiar la contraseña de administrador de la consola web OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) más abajo.

#### Cambiar la contraseña de administrador de la consola web OSGi {#changing-the-osgi-web-console-admin-password}

Cambie la contraseña utilizada para acceder a la consola web. Utilice un [Configuración de OSGI](/help/sites-deploying/configuring-osgi.md) para actualizar las siguientes propiedades del **Consola de administración de Apache Felix OSGi**:

* **Nombre de usuario** y **Contraseña**, las credenciales para acceder a la propia consola de administración web de Apache Felix.
Se debe cambiar la contraseña *después* la instalación inicial para garantizar la seguridad de su instancia.

>[!NOTE]
>
>Consulte [Configuración de OSGI](/help/sites-deploying/configuring-osgi.md) para obtener información detallada sobre la configuración de OSGi.

**Para cambiar la contraseña de administrador de la consola web de OSGi**:

1. Uso del **Herramientas**, **Operaciones** , abra el menú **Consola web** y vaya al **Configuración** sección.
Por ejemplo, en `<server>:<port>/system/console/configMgr`.
1. Vaya a y abra la entrada de **Consola de administración de Apache Felix OSGi**.
1. Cambie el **nombre de usuario** y **contraseña**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. Seleccione **Guardar**.

### Implementar controlador de error personalizado {#implement-custom-error-handler}

El Adobe recomienda definir páginas de controladores de error personalizados, especialmente para los códigos de respuesta HTTP 404 y 500 para evitar la divulgación de información.

>[!NOTE]
>
>Consulte [¿Cómo puedo crear scripts personalizados o controladores de error?](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/custom-error-page.html) para obtener más información.

### Completar lista de comprobación de seguridad de Dispatcher {#complete-dispatcher-security-checklist}

AEM Dispatcher es una parte esencial de su infraestructura. El Adobe recomienda completar la [Lista de comprobación de seguridad de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html).

>[!CAUTION]
>
>Con Dispatcher, debe deshabilitar el selector &quot;.form&quot;.

## Pasos de verificación {#verification-steps}

### Configuración de la replicación y los usuarios de transporte {#configure-replication-and-transport-users}

AEM Una instalación estándar de especifica lo siguiente `admin` como usuario para credenciales de transporte dentro del valor predeterminado [agentes de replicación](/help/sites-deploying/replication.md). Además, el usuario administrador se utiliza para originar la replicación en el sistema de creación.

Por motivos de seguridad, ambos deben cambiarse para reflejar el caso de uso en cuestión, teniendo en cuenta los dos aspectos siguientes:

* El **usuario de transporte** no debe ser el usuario administrador. En su lugar, configure un usuario en el sistema de publicación que solo tenga derechos de acceso a las partes relevantes del sistema de publicación y utilice las credenciales de ese usuario para el transporte.

  Puede comenzar desde el usuario receptor de replicación agrupado y configurar los derechos de acceso de este usuario para que coincidan con su situación

* El **usuario de replicación** o **ID de usuario agente** tampoco debe ser el usuario administrador, sino un usuario que solo pueda ver el contenido replicado. El usuario de replicación se utiliza para recopilar el contenido que se va a replicar en el sistema de creación antes de enviarlo al editor.

### Comprobar las comprobaciones de estado de seguridad del tablero de operaciones {#check-the-operations-dashboard-security-health-checks}

AEM presenta el nuevo tablero de operaciones, destinado a ayudar a los operadores del sistema a solucionar problemas y a monitorizar el estado de una instancia.

El tablero también incluye una colección de comprobaciones de estado de seguridad. Se recomienda comprobar el estado de todas las comprobaciones de estado de seguridad antes de activar la instancia de producción. Para obtener más información, consulte la [Documentación del Operations Dashboard](/help/sites-administering/operations-dashboard.md).

### Comprobar si el contenido del ejemplo está presente {#check-if-example-content-is-present}

Todo el contenido y los usuarios de ejemplo (por ejemplo, el proyecto de Geometrixx y sus componentes) deben desinstalarse y eliminarse por completo en un sistema productivo antes de hacerlo accesible públicamente.

>[!NOTE]
>
>La muestra `We.Retail` Las aplicaciones de se eliminan si esta instancia se ejecuta en [Modo Producción lista](/help/sites-administering/production-ready.md). Si no es así, puede desinstalar el contenido de ejemplo en el Administrador de paquetes y, a continuación, buscar y desinstalar todos los archivos `We.Retail` paquetes.

Consulte [Trabajo con paquetes](package-manager.md).

### Compruebe si los paquetes de desarrollo de CRX están presentes {#check-if-the-crx-development-bundles-are-present}

Estos paquetes OSGi de desarrollo deben desinstalarse tanto en los sistemas productivos de creación como de publicación antes de hacerlos accesibles.

* Compatibilidad con CRXDE de Adobe (com.adobe.granite.crxde-support)
* Adobe Granite CRX Explorer (com.adobe.granite.crx-explorer)
* Adobe CRXDE Lite de Granite (com.adobe.granite.crxde-lite)

### Compruebe si el paquete de desarrollo de Sling está presente {#check-if-the-sling-development-bundle-is-present}

El [AEM Herramientas para desarrolladores de](/help/sites-developing/aem-eclipse.md) implemente la Instalación de soporte de las herramientas de Apache Sling (org.apache.sling.tooling.support.install).

Este paquete OSGi debe desinstalarse tanto en los sistemas productivos de creación como de publicación antes de hacerlos accesibles.

### Protect contra la falsificación de solicitudes entre sitios {#protect-against-cross-site-request-forgery}

#### El marco de protección CSRF {#the-csrf-protection-framework}

AEM 6.1 incluye un mecanismo que ayuda a protegerse contra los ataques de falsificación de solicitud en sitios múltiples, denominado **Marco de protección CSRF**. Para obtener más información sobre cómo utilizarla, consulte la [documentación](/help/sites-developing/csrf-protection.md).

#### El filtro de referente de Sling {#the-sling-referrer-filter}

Para solucionar problemas de seguridad conocidos con la falsificación de solicitudes entre sitios (CSRF) en CRX WebDAV y Apache Sling, agregue configuraciones para que el filtro Referente lo utilice.

El servicio de filtro de referente es un servicio OSGi que le permite configurar lo siguiente:

* qué métodos http se deben filtrar
* si se permite un encabezado de referente vacío
* y una lista de servidores que se permitirán además del host de servidor.

  De forma predeterminada, todas las variaciones de localhost y los nombres de host actuales a los que está enlazado el servidor están en la lista.

Para configurar el servicio del filtro de referente:

1. Abra la consola Apache Felix (**Configuraciones**) a las:

   `https://<server>:<port_number>/system/console/configMgr`

1. Iniciar sesión como `admin`.
1. En el **Configuraciones** menú, seleccione:

   `Apache Sling Referrer Filter`

1. En el `Allow Hosts` , introduzca todos los hosts que pueden utilizarse como referente. Cada entrada debe tener el formato

   &lt;protocol>://&lt;server>:&lt;port>

   Por ejemplo:

   * `https://allowed.server:80` permite todas las solicitudes de este servidor con el puerto determinado.
   * Si también desea permitir solicitudes https, debe introducir una segunda línea.
   * Si permite todos los puertos desde ese servidor, puede utilizar `0` como el número de puerto.

1. Compruebe la `Allow Empty` , si desea permitir encabezados de referente vacíos o que falten.

   >[!CAUTION]
   >
   >El Adobe recomienda que proporcione un referente mientras utiliza herramientas de línea de comandos como `cURL` en lugar de permitir un valor vacío, ya que podría exponer el sistema a ataques de CSRF.

1. Edite los métodos que utiliza este filtro para las comprobaciones con el `Filter Methods` field.

1. Clic **Guardar** para guardar los cambios.

### Configuración de OSGI {#osgi-settings}

Algunos ajustes de OSGI están configurados de forma predeterminada para facilitar la depuración de la aplicación. Cambie esta configuración en las instancias productivas de publicación y autor para evitar que la información interna se filtre al público.

>[!NOTE]
>
>Todas las configuraciones a continuación, excepto **El filtro de depuración de WCM de CQ por día**, quedan cubiertas automáticamente por [Modo Producción lista](/help/sites-administering/production-ready.md). Por lo tanto, Adobe recomienda revisar toda la configuración antes de implementar la instancia en un entorno productivo.

Se debe cambiar la configuración especificada para cada uno de los servicios siguientes:

* [Administrador de bibliotecas de Adobe Granite HTML](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * habilitar **Minificar** (para eliminar los caracteres CRLF y espacios en blanco).
   * habilitar **Gzip** (para permitir que se compriman los archivos y se acceda a ellos con una solicitud).
   * disable **Depurar**
   * disable **Programación**

* [Filtro de depuración de CQ WCM por día](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * desmarcar **Activar**

* [Filtro de WCM de CQ de día](/help/sites-deploying/osgi-configuration-settings.md):

   * solo al publicar, establecer **Modo WCM** a &quot;desactivado&quot;

* [Apache Sling JavaScript Handler](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * disable **Generar información de depuración**

* [Apache Sling JSP Script Handler](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * disable **Generar información de depuración**
   * disable **Contenido asignado**

Consulte [Ajustes de configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md).

AEM Al trabajar con los servicios de configuración, existen varios métodos para administrar los parámetros de configuración de dichos servicios; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

## Lecturas adicionales {#further-readings}

### Mitigar ataques de denegación de servicio (DoS) {#mitigate-denial-of-service-dos-attacks}

Un ataque de denegación de servicio (DoS) es un intento de hacer que un recurso de equipo no esté disponible para los usuarios a los que va destinado. Este ataque se suele realizar sobrecargando el recurso; por ejemplo:

* Una avalancha de solicitudes desde una fuente externa.
* Una solicitud de más información de la que el sistema puede entregar correctamente.

  Por ejemplo, una representación JSON de todo el repositorio.

* Al solicitar una página de contenido con un número ilimitado de URL, la URL puede incluir un identificador, algunos selectores, una extensión y un sufijo, cualquiera de los cuales se puede modificar.

  Por ejemplo, `.../en.html` también se puede solicitar como:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

  Todas las variaciones válidas (por ejemplo, devolver un `200` Respuesta de y están configurados para almacenarse en caché) son almacenados en caché por Dispatcher, lo que finalmente conduce a un sistema de archivos completo y a la ausencia de servicio para más solicitudes.

AEM Hay muchos puntos de configuración para prevenir tales ataques, pero solo se discuten aquellos puntos que se relacionan con los ataques de tipo de ataque de tipo de ataque de tipo de tipo de ataque de tipo de tipo de ataque de tipo de tipo de ataque de tipo de tipo de ataque de tipo de tipo de ataque de tipo de tipo de ataque de tipo de ataque.

**Configuración de Sling para evitar denegaciones de servicio**

Sling es *centrado en el contenido*. El procesamiento se centra en el contenido, ya que cada solicitud (HTTP) se asigna al contenido en forma de recurso JCR (un nodo de repositorio):

* El primer destino es el recurso (nodo JCR) que contiene el contenido.
* En segundo lugar, el procesador o script se encuentra en las propiedades del recurso con determinadas partes de la solicitud (por ejemplo, los selectores o la extensión).

Consulte [Procesamiento de solicitudes de Sling](/help/sites-developing/the-basics.md#sling-request-processing) para obtener más información.

Este enfoque hace que Sling sea potente y flexible, pero como siempre, es la flexibilidad la que debe administrarse cuidadosamente.

Para ayudar a evitar el uso indebido de DoS, puede hacer lo siguiente:

1. Incorporar controles en el nivel de aplicación. Debido al número de variaciones posibles, no es posible una configuración predeterminada.

   En la aplicación debe:

   * Controle los selectores de la aplicación para que *solamente* Proporcionar los selectores explícitos necesarios y devolver `404` para todos los demás.
   * Impida la salida de un número ilimitado de nodos de contenido.

1. Compruebe la configuración de los procesadores predeterminados, que pueden ser un área problemática.

   * En particular, el procesador JSON atraviesa la estructura de árbol en varios niveles.

     Por ejemplo, la solicitud:

     `http://localhost:4502/.json`

     podría volcar todo el repositorio en una representación JSON, lo que puede causar problemas significativos en el servidor. Por este motivo, Sling establece un límite en el número máximo de resultados. Para limitar la profundidad del procesamiento de JSON, establezca el valor para lo siguiente:

     **Resultados máximos de JSON** ( `json.maximumresults`)

     en la configuración de [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Cuando se supera este límite, la renderización se contrae. AEM El valor predeterminado de Sling en el entorno de trabajo de es `1000`.

   * Como medida preventiva, debe desactivar los demás procesadores predeterminados (HTML, texto sin formato, XML). De nuevo, configurando la variable [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).

   >[!CAUTION]
   >
   >AEM No deshabilite el procesador JSON porque es necesario para el funcionamiento normal de la interfaz de usuario de.

1. Utilice un cortafuegos para filtrar el acceso a su instancia.

   * El uso de un cortafuegos a nivel de sistema operativo es necesario para filtrar el acceso a puntos de su instancia que puedan provocar ataques de denegación de servicio si se dejan sin protección.

**Mitigar frente a denegaciones de servicio causadas por el uso de selectores de formulario**

>[!NOTE]
>
>AEM Esta mitigación solo debe realizarse en entornos de que no utilicen Forms.

AEM Debido a que no proporciona índices predeterminados para el `FormChooserServlet`Sin embargo, el uso de selectores de formularios en las consultas puede provocar un déclencheur AEM costoso en el recorrido del repositorio, lo que generalmente interrumpe la instancia de la aplicación de forma que se detenga. Los selectores de formularios se pueden detectar mediante la presencia del **&amp;ast;.form.&amp;ast;** cadena en consultas.

Para mitigar este problema, puede realizar los siguientes pasos:

1. Vaya a la consola web seleccionando el explorador *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Buscar por **Servlet de selector de formularios CQ WCM por día**
1. Después de hacer clic en la entrada, desactive la **Búsqueda avanzada requerida** en la siguiente ventana.

1. Haga clic en **Guardar**.

**Mitigar frente a denegaciones de servicio causadas por el servlet de descarga de recursos**

El servlet de descarga de recursos predeterminado permite a los usuarios autenticados emitir solicitudes de descarga simultáneas, arbitrariamente grandes para crear archivos ZIP de recursos. La creación de archivos ZIP de gran tamaño puede sobrecargar el servidor y la red. Para mitigar un posible riesgo de denegación de servicio (DoS) causado por este comportamiento, `AssetDownloadServlet` El componente OSGi está deshabilitado de forma predeterminada en [!DNL Experience Manager] instancia de publicación. Está habilitado en [!DNL Experience Manager] Crear instancia de forma predeterminada.

Si no necesita la capacidad de descarga, deshabilite el servlet en las implementaciones de creación y publicación. Si su configuración requiere que la capacidad de descarga de recursos esté habilitada, consulte [este artículo](/help/assets/download-assets-from-aem.md) para obtener más información. Además, puede definir un límite máximo de descargas que sea compatible con la implementación.

### Deshabilitar WebDAV {#disable-webdav}

Deshabilite WebDAV en los entornos de creación y publicación deteniendo los paquetes OSGi adecuados.

1. Conéctese a **Consola de administración Felix** que se ejecuta el:

   `https://<*host*>:<*port*>/system/console`

   Por ejemplo, `http://localhost:4503/system/console/bundles`.

1. En la lista de paquetes, busque el paquete denominado:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Para detener este paquete, en la columna Actions, haga clic en el botón stop.

1. De nuevo, en la lista de paquetes, busque el paquete llamado:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Para detener este paquete, haga clic en el botón Detener.

   >[!NOTE]
   >
   >AEM No es necesario reiniciar la.

### Compruebe que no está revelando información de identificación personal en la ruta de inicio de los usuarios {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

Es importante proteger a los usuarios asegurándose de que no expone ninguna información personal identificable en la ruta de inicio de los usuarios del repositorio.

AEM Desde la versión 6.1, la forma en que se almacenan los nombres de nodo de ID de usuario (también conocidos como autorizados) ha cambiado con una nueva implementación de `AuthorizableNodeName` interfaz. La nueva interfaz ya no expone el ID de usuario en el nombre del nodo, sino que genera un nombre aleatorio.

AEM No se debe realizar ninguna configuración para habilitarla, ya que ahora es la forma predeterminada de generar ID autorizados en los informes de.

Aunque no se recomienda, puede deshabilitarla en caso de que necesite la implementación antigua para mantener la compatibilidad con las aplicaciones existentes. Para ello, debe hacer lo siguiente:

1. Vaya a la consola web y elimine la entrada ** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** de la propiedad **requiredServicePids** in **Apache Jackrabbit Oak SecurityProvider**.

   También puede encontrar el Proveedor de seguridad de Oak buscando el **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID en las configuraciones de OSGi.

1. Elimine el **Nombre de nodo autorizable aleatorio Apache Jackrabbit Oak** Configuración de OSGi desde la consola web.

   Para facilitar la búsqueda, el PID de esta configuración es **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Para obtener más información, consulte la documentación de Oak sobre [Generación de nombre de nodo con autorización](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Paquete de protección de permisos anónimo {#anonymous-permission-hardening-package}

AEM De forma predeterminada, el sistema almacena metadatos del sistema, como los siguientes `jcr:createdBy` o `jcr:lastModifiedBy` como propiedades del nodo, junto al contenido normal, en el repositorio. Según la configuración y la configuración de control de acceso, en algunos casos esto podría dar lugar a la exposición de información de identificación personal (PII), por ejemplo, cuando estos nodos se representan como JSON o XML sin procesar.

Al igual que todos los datos del repositorio, estas propiedades están mediadas por la pila de autorización de Oak. El acceso a ellos debe restringirse de conformidad con el principio del menor privilegio.

Para admitir esto, Adobe proporciona un paquete de endurecimiento de permisos como base para que los clientes se basen en él. Funciona instalando una entrada de control de acceso &quot;denegar&quot; en la raíz del repositorio, restringiendo el acceso anónimo a las propiedades del sistema más utilizadas. El paquete está disponible para descargar [aquí](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/helper/anonymous-permissions-pkg-0.1.2.zip) AEM y se pueden instalar en todas las versiones compatibles de la aplicación de.

Para ilustrar los cambios, podemos comparar las propiedades del nodo que se pueden ver de forma anónima antes de instalar el paquete:

![Antes de instalar el paquete](/help/sites-administering/assets/before_resized.png)

con los que se pueden ver después de instalar el paquete, donde `jcr:createdBy` y `jcr:lastModifiedBy` no son visibles:

![Después de instalar el paquete](/help/sites-administering/assets/after_resized.png)

Para obtener más información, consulte las notas de la versión del paquete.

### Impedir el clickjacking {#prevent-clickjacking}

Para evitar el secuestro de clics, Adobe recomienda configurar el servidor web para que proporcione el `X-FRAME-OPTIONS` Encabezado HTTP establecido en `SAMEORIGIN`.

Para obtener más información sobre el secuestro de clics, consulte la [Sitio de OWASP](https://www.owasp.org/index.php/Clickjacking).

### Asegúrese De Replicar Correctamente Las Claves De Cifrado Cuando Sea Necesario {#make-sure-you-properly-replicate-encryption-keys-when-needed}

AEM AEM Ciertas características y esquemas de autenticación requieren que se dupliquen las claves de cifrado en todas las instancias de la.

Antes de hacerlo, la replicación de claves se realiza de forma diferente entre versiones, ya que la forma en que se almacenan las claves es diferente entre 6.3 y versiones anteriores.

Consulte a continuación para obtener más información.

#### AEM Duplicación de claves para 6.3 {#replicating-keys-for-aem}

AEM Mientras que en las versiones anteriores las claves de replicación se almacenaban en el repositorio, a partir de la versión 6.3 se almacenan en el sistema de archivos de.

Por lo tanto, para replicar las claves entre instancias, cópielas desde la instancia de origen a la ubicación de las instancias de destino en el sistema de archivos.

Más específicamente, debe hacer lo siguiente:

1. AEM Acceda a la instancia de la (normalmente una instancia de autor) que contiene el material clave que se va a copiar.
1. Busque el paquete com.adobe.granite.crypto.file en el sistema de archivos local. Por ejemplo, en esta ruta:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   El `bundle.info` dentro de cada carpeta identifica el nombre del paquete.

1. Vaya a la carpeta de datos. Por ejemplo:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copie los archivos HMAC y maestro.
1. A continuación, vaya a la instancia de destino a la que desee duplicar la clave HMAC y vaya a la carpeta de datos. Por ejemplo:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Pegue los dos archivos que ha copiado anteriormente.
1. [Actualizar el paquete de cifrado](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) si la instancia de destino ya se está ejecutando.
1. Repita los pasos anteriores para todas las instancias en las que desee replicar la clave.

#### AEM Duplicación de claves para versiones anteriores y de la versión 6.2 de {#replicating-keys-for-aem-and-older-versions}

AEM En la versión 6.2 y versiones anteriores de, las claves se almacenan en el repositorio de en la `/etc/key` nodo.

La manera recomendada de replicar de forma segura las claves en las instancias es replicar solo este nodo. Puede replicar nodos selectivamente mediante el CRXDE Lite:

1. Abra el CRXDE Lite yendo a *`https://&lt;serveraddress&gt;:4502/crx/de/index.jsp`*
1. Seleccione el `/etc/key` nodo.
1. Vaya a la **Replicación** pestaña.
1. Pulse el botón **Replicación** botón.

### Realizar una prueba de penetración {#perform-a-penetration-test}

Adobe AEM recomienda realizar una prueba de penetración de la infraestructura de su infraestructura de antes de continuar con la producción.

### Prácticas recomendadas de desarrollo {#development-best-practices}

Es fundamental que los nuevos desarrollos sigan el [Prácticas recomendadas de seguridad](/help/sites-developing/security.md) AEM para garantizar que el entorno de su entorno de permanezca seguro.
