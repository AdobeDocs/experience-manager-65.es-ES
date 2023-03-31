---
title: Implementación de comunidades
seo-title: Deploying Communities
description: Cómo implementar AEM Communities
seo-description: How to deploy AEM Communities
content-type: reference
topic-tags: deploying
source-git-commit: cc0574ae22758d095a3ca6b91f0ceae4a8691f0e
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 3%

---


# Implementación de comunidades{#deploying-communities}

## Requisitos previos {#prerequisites}

* [Plataforma de AEM 6.5](/help/sites-deploying/deploy.md)

* Licencia de AEM Communities

* Licencias opcionales para:

   * [Funciones de Adobe Analytics para Communities](/help/communities/analytics.md)
   * [MongoDB para MSRP](/help/communities/msrp.md)
   * [Adobe Cloud para ASRP](/help/communities/asrp.md)

## Lista de comprobación de instalación {#installation-checklist}

**Para la variable [plataforma AEM](/help/sites-deploying/deploy.md#what-is-aem)**:

* Instale la última [Actualizaciones de AEM 6.5](#aem64updates).

* Si no utiliza los puertos predeterminados (4502, 4503), [configurar agentes de replicación](#replication-agents-on-author).
* [Replicar clave criptográfica](#replicate-the-crypto-key)
* Si apoyamos la globalización, [configurar traducción automatizada](/help/sites-administering/translation.md)
(la configuración de muestra se proporciona para el desarrollo).

**Para la variable [Capacidad de las comunidades](/help/communities/overview.md)**:

* Si se implementa un [publicar granja](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identificar el publicador principal](#primary-publisher)

* [Habilitar el servicio de túnel](#tunnel-service-on-author)
* [Habilitar inicio de sesión social](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Configuración de Adobe Analytics](/help/communities/analytics.md)
* Configure un [servicio de correo electrónico predeterminado](/help/communities/email.md)
* Identificar la opción para [almacenamiento UGC compartido](/help/communities/working-with-srp.md) (**SRP**)

   * Si MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [Instalar y configurar MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [Configurar Solr](/help/communities/solr.md)
      * [Seleccionar MSRP](/help/communities/srp-config.md)
   * Si la base de datos relacional es SRP [(DSRP)](/help/communities/dsrp.md)

      * [Instale el controlador JDBC para MySQL](#jdbc-driver-for-mysql)
      * [Instalar y configurar MySQL para DSRP](/help/communities/dsrp-mysql.md)
      * [Configurar Solr](/help/communities/solr.md)
      * [Seleccionar DSRP](/help/communities/srp-config.md)
   * Si el Adobe es SRP [(ASRP)](/help/communities/asrp.md)

      * Póngase en contacto con el representante de cuentas para el aprovisionamiento.
      * [Seleccionar ASRP](/help/communities/srp-config.md)
   * Si JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * No es una tienda UGC compartida:

         * UGC nunca se replica.
         * UGC solo es visible en AEM instancia o clúster en el que se introdujo.
      * El valor predeterminado es JSRP






## Últimas versiones {#latest-releases}

AEM 6.5 Communities GA incluye el paquete Communities. Para obtener información sobre las actualizaciones a AEM 6.5 [Comunidades](/help/release-notes/release-notes.md#experiencemanagercommunities), consulte [Notas de la versión de AEM 6.5](/help/release-notes/release-notes.md#communities-release-notes.html).

### Actualizaciones de AEM 6.5 {#aem-updates}

A partir de AEM 6.4, las actualizaciones para las comunidades se entregan como parte de AEM paquetes de correcciones acumulativas y Service Packs.

Para conocer las últimas actualizaciones de AEM 6.5, consulte [Paquetes de correcciones acumulativas y Service Packs de Adobe Experience Manager 6.4](https://helpx.adobe.com/es/experience-manager/aem-releases-updates.html).

### Historial de versiones {#version-history}

Al igual que en AEM 6.4 y versiones posteriores, las funciones y revisiones de AEM Communities forman parte de los paquetes fijos y los service packs acumulativos de AEM Communities. Por lo tanto, no hay paquetes de funciones independientes.

### Controlador JDBC para MySQL {#jdbc-driver-for-mysql}

La función de una comunidad utiliza una base de datos MySQL:

* Para [DSRP](/help/communities/dsrp.md): almacenamiento del contenido generado por el usuario (UGC)

El conector MySQL debe obtenerse e instalarse por separado.

Los pasos necesarios son:

1. Descargue el archivo ZIP de [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * La versión debe ser >= 5.1.38

1. Extraer `mysql-connector-java-&lt;version&gt;-bin.jar (bundle) from the archive`
1. Utilice la consola web para instalar e iniciar el paquete :

   * Por ejemplo, https://localhost:4502/system/console/bundles
   * Seleccionar **`Install/Update`**
   * Examinar... para seleccionar el paquete extraído del archivo ZIP descargado
   * Compruebe que *Controlador JDBC de oracle Corporation para MySQLcom.mysql.jdbc* está activo y debe iniciarlo en caso contrario (o comprobar los registros)

1. Si realiza la instalación en una implementación existente después de haber configurado JDBC, vuelva a conectar JDBC al nuevo conector y vuelva a guardar la configuración JDBC desde la consola web :

   * Por ejemplo, https://localhost:4502/system/console/configMgr
   * Localizar `Day Commons JDBC Connections Pool` y seleccione para abrir la configuración.
   * Seleccionar `Save`.

1. Repita los pasos 3 y 4 en todas las instancias de autor y publicación.

Encontrará más información sobre la instalación de paquetes en la sección [Consola web](/help/sites-deploying/web-console.md#bundles) página.

#### Ejemplo : Paquete de conector MySQL instalado {#example-installed-mysql-connector-bundle}

![](../assets/mysql-connector.png)

### MLS AEM Advanced {#aem-advanced-mls}

Para que la colección SRP (MSRP o DSRP) admita la búsqueda multilingüe avanzada (MLS), se necesitan nuevos complementos Solr además de un esquema personalizado y una configuración Solr. Todos los elementos necesarios se empaquetan en un archivo zip descargable.

La descarga avanzada de MLS (también conocida como &#39;phasetwo&#39;) está disponible en el repositorio de Adobe :

* [AEM-SOLR-MLS-phasetwo](https://repo1.maven.org/maven2/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * Versión 1.2.40, 6 de abril de 2016
   * Descargue AEM-SOLR-MLS-phasetwo-1.2.40.zip

Para obtener más información e información de instalación, visite [Configuración de Solr](/help/communities/solr.md) para SRP.

### Acerca de los vínculos a Package Share {#about-links-to-package-share}

**Paquetes visibles en Adobe AEM Cloud**

Los vínculos a paquetes en esta página no requieren ninguna instancia de AEM en ejecución, ya que son para el uso compartido de paquetes en `adobeaemcloud.com`. Mientras los paquetes son visibles, la variable `Install` es para instalar los paquetes en un sitio alojado de Adobe. Si desea realizar la instalación en una instancia de AEM local, seleccione `Install` generará un error.

**Instalación en una instancia de AEM local**

Para instalar los paquetes visibles en `adobeaemcloud.com` en una instancia de AEM local, el paquete primero debe descargarse en un disco local :

* Seleccione el **Recursos** ficha
* Select **descargar en disco**

En la instancia de AEM local, utilice el administrador de paquetes (por ejemplo [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)), para cargarlo en el repositorio local del paquete de AEM.

También puede acceder al paquete utilizando el paquete compartido desde la instancia de AEM local (por ejemplo, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), el `Download` se descargará en el repositorio de paquetes de la instancia de AEM local.

Una vez en el repositorio de paquetes de la instancia de AEM local, utilice el administrador de paquetes para instalar el paquete.

Para obtener más información, visite [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md#package-share).

## Implementaciones recomendadas {#recommended-deployments}

En AEM Communities, un almacén común se utiliza para almacenar contenido generado por el usuario (UGC) y, a menudo, se denomina [proveedor de recursos de almacenamiento (SRP)](/help/communities/working-with-srp.md). La implementación recomendada se centra en elegir una opción de SRP para el almacén común.

El almacén común admite la moderación y el análisis de UGC en el entorno de publicación, al tiempo que elimina la necesidad de [replicación](/help/communities/sync.md) de UGC.

* [Almacenamiento de contenido de la comunidad](/help/communities/working-with-srp.md) : analiza las opciones de almacenamiento de SRP para comunidades AEM

* [Topologías recomendadas](/help/communities/topologies.md) : analiza la topología que se va a usar en función del caso de uso y la elección de SRP

## Actualización {#upgrading}

Al actualizar a la plataforma AEM 6.5 desde versiones anteriores de AEM, es importante leer [Actualización a AEM 6.5](/help/sites-deploying/upgrade.md).

Además de actualizar la plataforma, lea [Actualización a AEM Communities 6.5](/help/communities/upgrade.md) para obtener más información sobre los cambios de Communities.

## Configuraciones {#configurations}

### Editor principal {#primary-publisher}

Cuando la implementación elegida es una [publicar granja](/help/communities/topologies.md#tarmk-publish-farm), entonces una instancia de publicación AEM debe identificarse como la variable **`primary publisher`** para actividades que no deben producirse en todas las instancias, como las funciones en las que se confía **notificaciones** o **Adobe Analytics**.

De forma predeterminada, la variable `AEM Communities Publisher Configuration` La configuración de OSGi se configura con la variable **`Primary Publisher`** casilla de verificación marcada, de modo que todas las instancias de publicación de un conjunto de servidores de publicación se autoidentifican como el principal.

Por lo tanto, es necesario **editar la configuración en todas las instancias de publicación secundarias** para desmarcar la **`Primary Publisher`** en el Navegador.

![](../assets/primary-publisher.png)

Para todas las demás instancias de publicación (secundarias) en un conjunto de servidores de publicación :

* Iniciar sesión con privilegios de administrador
* Acceda a la [consola web](/help/sites-deploying/configuring-osgi.md)

   * Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Busque la variable `AEM Communities Publisher Configuration`
* Seleccione el icono de edición
* Desmarque la **Editor principal** casilla de verificación
* Seleccione **Guardar**

### Agentes de replicación en Author {#replication-agents-on-author}

La replicación se utiliza para el contenido del sitio creado en el entorno de publicación, como los grupos de la comunidad, así como para administrar miembros y grupos de miembros del entorno de creación mediante el uso de [servicio de túnel](#tunnel-service-on-author).

Para el publicador principal, asegúrese de que la variable [Configuración del agente de replicación](/help/sites-deploying/replication.md) identifica correctamente el servidor de publicación y el usuario autorizado. El usuario autorizado predeterminado, `admin` ya tiene los permisos adecuados (es miembro de `Communities Administrators`).

Para que otro usuario tenga los permisos adecuados, debe agregarlos como miembro a la variable `administrators` grupo de usuarios (también es miembro de `Communities Administrators`).

Hay dos agentes de replicación en el entorno de creación que necesitan que la configuración del transporte sea correcta.

* Acceso a la consola Replicación en el autor

   * Desde la navegación global : **Herramientas, implementación, replicación, agentes en el autor**

* Siga el mismo procedimiento para ambos agentes :

   * **Agente predeterminado (publicar)**
   * **Agente de replicación inversa (publicar inversa)**

      1. Seleccione el agente.
      1. Select **editar**.
      1. Seleccione el **Transporte** ficha
      1. Si no es puerto `4503`, edite el **URI** para especificar el puerto correcto.

      1. Si no es un usuario `admin`, edite el **Usuario** y **Contraseña** para especificar un miembro de `administrators` grupo de usuarios.

Las siguientes imágenes muestran los resultados de cambiar el puerto de 4503 a 6103 por :

#### Agente predeterminado (publicar) {#default-agent-publish}

![configure-limits](../assets/default-agent-publish.png)

#### Agente de replicación inversa (publicar inversa) {#reverse-replication-agent-publish-reverse}

![](../assets/reverse-replication-agent.png)

### Servicio de túnel en Author {#tunnel-service-on-author}

Al utilizar el entorno de creación para [crear sitios](/help/communities/sites-console.md), [modificar las propiedades del sitio](/help/communities/sites-console.md#modifying-site-properties) o [administrar miembros de la comunidad](/help/communities/members.md), es necesario acceder a los miembros (usuarios) registrados en el entorno de publicación, no a los usuarios registrados en el autor.

El servicio de túnel proporciona este acceso mediante el agente de replicación en el autor.

Para habilitar el servicio de túnel :

* Activado **author**, inicie sesión con privilegios administrativos.
* Si el editor no es localhost:4503 o el usuario de transporte no lo es `admin`, luego [configurar el agente de replicación](#replication-agents-on-author).

* Acceda a la [Consola web](/help/sites-deploying/configuring-osgi.md)

   * Por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Busque la variable `AEM Communities Publish Tunnel Service`
* Seleccione el icono de edición
* Seleccione el **enable** casilla de verificación
* select **Guardar**

![](../assets/tunnel-service.png)

### Replicar la clave criptográfica {#replicate-the-crypto-key}

Existen dos funciones de AEM Communities que requieren que todas las instancias de servidor AEM utilicen las mismas claves de cifrado. Estos son [Analytics](/help/communities/analytics.md) y [ASRP](/help/communities/asrp.md).

A partir de AEM 6.3, el material clave se almacena en el sistema de archivos y ya no en el repositorio.

Para copiar el material clave del autor en todas las demás instancias, es necesario:

* Acceda a la instancia de AEM, normalmente una instancia de autor, que contiene el material clave que desea copiar

   * Busque la variable `com.adobe.granite.crypto.file` paquete en el sistema de archivos local

      Por ejemplo,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * La variable `bundle.info` El archivo identificará el paquete
   * Vaya a la carpeta de datos, por ejemplo,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * Copie los archivos hmac y primary node .



* Para cada instancia de AEM de destino

   * Vaya a la carpeta de datos, por ejemplo,

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * Pegar los 2 archivos copiados anteriormente
   * Es necesario [actualizar el paquete Granite Crypto](#refresh-the-granite-crypto-bundle) si la instancia de AEM de destino está ejecutándose.


>[!CAUTION]
>
>Si ya se ha configurado otra función de seguridad basada en las claves criptográficas, replicar las claves criptográficas podría dañar la configuración. Para obtener asistencia, [póngase en contacto con el servicio de atención al cliente](https://helpx.adobe.com/es/marketing-cloud/contact-support.html).

#### Replicación del repositorio {#repository-replication}

Tener el material clave almacenado en el repositorio, como ocurrió con AEM 6.2 y anteriores, se puede conservar especificando la siguiente propiedad del sistema en el primer inicio de cada instancia de AEM (que crea el repositorio inicial) :

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>Es importante verificar que la variable [agente de replicación en author](#replication-agents-on-author) está correctamente configurado.

Con el material clave almacenado en el repositorio, la forma de replicar la clave criptográfica de autor a otras instancias es la siguiente:

Uso [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* Vaya a [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Seleccionar `/etc/key`
* Apertura `Replication` ficha
* Seleccionar `Replicate`

* [actualizar el paquete Granite Crypto](#refresh-the-granite-crypto-bundle)

![](../assets/replicare-repository.png)

#### Actualizar el paquete de criptografía de Granite {#refresh-the-granite-crypto-bundle}

* En cada instancia de publicación, acceda a la variable [Consola web](/help/sites-deploying/configuring-osgi.md)

   * Por ejemplo, [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* Localizar `Adobe Granite Crypto Support` paquete (com.adobe.granite.crypto)
* Select **Actualizar**

![](../assets/refresh-granite-bundle.png)

* Después de un momento, **Correcto** El cuadro de diálogo debe aparecer:
   `Operation completed successfully.`

### Servidor HTTP Apache {#apache-http-server}

Si utiliza el servidor HTTP Apache, asegúrese de utilizar el nombre de servidor correcto para todas las entradas relevantes.

En particular, tenga cuidado de usar el nombre de servidor correcto, no `localhost`, en el `RedirectMatch`.

#### ejemplo de httpd.conf {#httpd-conf-sample}

```shell
<IfModule alias_module>
     # XAMPP does not have a favicon; this prevents any 404 errors which may arise.
     Redirect 404 /favicon.ico
     <Location /favicon.ico>
         ErrorDocument 404 "No favicon"
     </Location>

    # Return from "Sign Out" generates response header directing you to "/", generating a 404 error
    # The RedirectMatch resolves it correctly when modified for the target Community Site :
    RedirectMatch ^/$ https://[server name]/content/sites/engage/en.html
 ...
 </IfModule>
```

### Dispatcher {#dispatcher}

Si utiliza un Dispatcher, consulte :

* AEM [Dispatcher](https://helpx.adobe.com/es/experience-manager/dispatcher/using/dispatcher.html) documentación
* [Instalación de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Configuración de Dispatcher para Communities](/help/communities/dispatcher.md)
* [Problemas conocidos](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentación de Communities relacionadas {#related-communities-documentation}

* Visita [Administración de sitios de comunidades](/help/communities/administer-landing.md) para obtener información sobre la creación de un sitio de comunidad, la configuración de plantillas de sitio de comunidad, la moderación del contenido de la comunidad, la administración de miembros y la configuración de mensajes.

* Visita [Desarrollo de comunidades](/help/communities/communities.md) para obtener información sobre el marco de componentes sociales (SCF) y la personalización de componentes y funciones de Communities.

* Visita [Creación de componentes de Communities](/help/communities/author-communities.md) para aprender a crear con y configurar componentes de Communities.

