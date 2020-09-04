---
title: Implementación de comunidades
seo-title: Implementación de comunidades
description: Cómo implementar AEM Communities
seo-description: Cómo implementar AEM Communities
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
translation-type: tm+mt
source-git-commit: 7e05502b590fb2c7c36919f94611efe999262d32
workflow-type: tm+mt
source-wordcount: '1890'
ht-degree: 1%

---


# Implementación de comunidades{#deploying-communities}

## Requisitos previos {#prerequisites}

* [AEM 6.5 Platform](/help/sites-deploying/deploy.md)

* Licencia de AEM Communities

* Licencias opcionales para:

   * [Funciones de Adobe Analytics para Comunidades](/help/communities/analytics.md)
   * [MongoDB para MSRP](/help/communities/msrp.md)
   * [Adobe Cloud para ASRP](/help/communities/asrp.md)

## Lista de comprobación de instalación {#installation-checklist}

**Para la plataforma[AEM](/help/sites-deploying/deploy.md#what-is-aem)**

* instalar las últimas actualizaciones de [AEM 6.5](#aem64updates)

* si no utiliza los puertos predeterminados (4502, 4503), [configure los agentes de replicación](#replication-agents-on-author)
* [replicar la clave criptográfica](#replicate-the-crypto-key)
* si admite globalización, [configure la traducción](/help/sites-administering/translation.md)automatizada (se proporciona configuración de muestra para el desarrollo)

**Para la capacidad de[Comunidades](/help/communities/overview.md)**

* si implementa un conjunto de servidores [de](/help/sites-deploying/recommended-deploys.md#tarmk-farm)publicación, [identifique el editor principal](#primary-publisher)

* [habilitar el servicio de túnel](#tunnel-service-on-author)
* [habilitar inicio de sesión social](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [configurar Adobe Analytics](/help/communities/analytics.md)
* configurar un servicio de correo electrónico [predeterminado](/help/communities/email.md)
* identificar la opción para el almacenamiento [UGC](/help/communities/working-with-srp.md) compartido (**SRP**)

   * si MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [instalar y configurar MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [configurar Solr](/help/communities/solr.md)
      * [seleccionar MSRP](/help/communities/srp-config.md)
   * si la base de datos relacional SRP [(DSRP)](/help/communities/dsrp.md)

      * [instalar el controlador JDBC para MySQL](#jdbc-driver-for-mysql)
      * [instalar y configurar MySQL para DSRP](/help/communities/dsrp-mysql.md)
      * [configurar Solr](/help/communities/solr.md)
      * [seleccionar DSRP](/help/communities/srp-config.md)
   * si Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * trabajar con el representante de cuentas para aprovisionar
      * [seleccionar ASRP](/help/communities/srp-config.md)
   * si JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * no es una tienda UGC compartida:

         * UGC nunca se replica
         * UGC solo visible en AEM instancia o clúster en el que se introdujo
      * el valor predeterminado es JSRP

   Para la función de **[habilitación](/help/communities/overview.md#enablement-community)**

   * [instalar y configurar FFmpeg](/help/communities/ffmpeg.md)
   * [instalar el controlador JDBC para MySQL](#jdbc-driver-for-mysql)
   * [instalar AEM Communities SCORM Engine](#scorm-package)
   * [instalar y configurar MySQL para la habilitación](/help/communities/mysql.md)






## Latest Releases {#latest-releases}

AEM 6.5 Communities GA incluye el paquete Communities. Para conocer las actualizaciones de AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities), consulte [AEM Notas](/help/release-notes/release-notes.md#communities-release-notes.html)de la versión 6.5.

### Actualizaciones de AEM 6.5 {#aem-updates}

A partir de AEM 6.4, las actualizaciones a las comunidades se entregan como parte de AEM paquetes de correcciones acumulativas y Service Packs.

Para obtener las actualizaciones más recientes de AEM 6.5, consulte Paquetes de correcciones acumulativas y Service Packs de [Adobe Experience Manager 6.4](https://helpx.adobe.com/es/experience-manager/aem-releases-updates.html).

### Historial de versiones {#version-history}

Al igual que en AEM 6.4 y versiones posteriores, las funciones y revisiones de AEM Communities forman parte de los paquetes de correcciones y los Service Packs acumulativos de AEM Communities. Por lo tanto, no hay paquetes de funciones independientes.

### Controlador JDBC para MySQL {#jdbc-driver-for-mysql}

Dos funciones de Communities usan una base de datos MySQL :

* para [activación](/help/communities/enablement.md) : grabación de actividades y alumnos SCORM
* para [DSRP](/help/communities/dsrp.md) : almacenamiento de contenido generado por el usuario (UGC)

El conector MySQL debe obtenerse e instalarse por separado.

Los pasos necesarios son:

1. descargue el archivo ZIP de [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * la versión debe ser >= 5.1.38

1. extraer mysql-Connector-java-&lt;version>-bin.jar (paquete) del archivo
1. utilice la consola web para instalar y inicio del paquete:

   * por ejemplo, https://localhost:4502/system/console/bundles
   * select **`Install/Update`**
   * Examinar... para seleccionar el paquete extraído del archivo ZIP descargado
   * compruebe que el controlador JDBC de Oracle Corporation para MySQLcom.mysql.jdbc* está activo y inicio si no (o compruebe los registros)

1. si realiza la instalación en una implementación existente después de haber configurado JDBC, vuelva a conectar JDBC al nuevo conector al volver a guardar la configuración JDBC desde la consola web:

   * por ejemplo, https://localhost:4502/system/console/configMgr
   * localizar `Day Commons JDBC Connections Pool` configuración
   * seleccionar para abrir
   * select `Save`

1. Repita los pasos 3 y 4 en todas las instancias de creación y publicación

Encontrará más información sobre la instalación de paquetes en la página Consola [](/help/sites-deploying/web-console.md#bundles) web.

#### Ejemplo: Paquete de conector MySQL instalado {#example-installed-mysql-connector-bundle}

![](../assets/chlimage_1-125.png)

### Paquete SCORM {#scorm-package}

El Modelo de referencia de objetos de contenido compartido (SCORM) es una colección de estándares y especificaciones para el aprendizaje electrónico. SCORM también define cómo se puede empaquetar el contenido en un archivo ZIP transferible.

El motor AEM Communities SCORM es necesario para la [función de habilitación](/help/communities/overview.md#enablement-community) . Paquetes de Scorm admitidos en comunidades AEM 6.5:

* [cq-social-scorm-package, versión 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) que incluye el motor [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) .

**Para instalar un paquete SCORM**

1. Instale el paquete [cq-social-scorm-package, versión 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg)desde Package Share
1. Descargue `/libs/social/config/scorm/database_scormengine_data.sql` de la instancia cq y ejecútela en el servidor mysql para crear un esquema de scormEngineDB actualizado.
1. Añada `/content/communities/scorm/RecordResults` en la propiedad Rutas excluidas en el filtro CSRF desde `https://<hostname>:<port>/system/console/configMgr` los editores.

#### Registro SCORM {#scorm-logging}

Como instalado, toda la actividad de habilitación se registra de forma incorrecta en la consola del sistema.

Si lo desea, el nivel de registro se puede establecer en WARN para el `RusticiSoftware.*` paquete.

Para trabajar con registros, consulte [Uso de registros de auditoría y archivos](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)de registro.

### MLS AEM avanzado {#aem-advanced-mls}

Para que la colección SRP (MSRP o DSRP) admita la búsqueda multilingüe avanzada (MLS), se necesitan nuevos complementos Solr además de una configuración personalizada de esquema y Solr. Todos los elementos necesarios se empaquetan en un archivo zip descargable.

La descarga avanzada de MLS (también conocida como &#39;phasetwo&#39;) está disponible en el repositorio de Adobe:

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * versión 1.2.40, 6 de abril de 2016
   * descargar AEM-SOLR-MLS-phasetwo-1.2.40.zip

Para obtener información detallada y sobre la instalación, visite [Solr Configuration](/help/communities/solr.md) for SRP.

### Acerca de los vínculos para compartir paquetes {#about-links-to-package-share}

**Paquetes visibles en Adobe AEM Cloud**

Los vínculos a los paquetes de esta página no requieren ninguna instancia de AEM en ejecución, ya que son para el uso compartido de paquetes en `adobeaemcloud.com`. Mientras los paquetes son visibles, el `Install`botón es para instalar los paquetes en un sitio alojado de Adobe. Si desea realizar la instalación en una instancia de AEM local, la selección `Install`producirá un error.

**Cómo instalar en una instancia de AEM local**

Para instalar los paquetes visibles en `adobeaemcloud.com` una instancia de AEM local, el paquete debe descargarse primero en un disco local:

* select the **Assets** tab
* seleccione **descargar en disco**

En la instancia de AEM local, utilice el administrador de paquetes (por ejemplo, [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) para cargar en el repositorio de paquetes de AEM local.

Como alternativa, si accede al paquete mediante el uso compartido de paquetes desde la instancia de AEM local (por ejemplo, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), el `Download`botón se descargará en el repositorio de paquetes de la instancia de AEM local.

Una vez en el repositorio de paquetes de la instancia de AEM local, utilice el administrador de paquetes para instalar el paquete.

Para obtener más información, visite [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md#package-share).

## Implementaciones recomendadas {#recommended-deployments}

En AEM Communities, un almacén común se utiliza para almacenar contenido generado por el usuario (UGC) y se le suele llamar proveedor de recursos de [almacenamiento (SRP)](/help/communities/working-with-srp.md). La implementación recomendada se centra en elegir una opción de SRP para la tienda común.

El almacén común admite moderación y análisis de UGC en el entorno de publicación, al tiempo que elimina la necesidad de [replicación](/help/communities/sync.md) de UGC.

* [Almacenamiento](/help/communities/working-with-srp.md) de contenido de comunidad: analiza las opciones de almacenamiento de SRP para las comunidades AEM

* [Topologías](/help/communities/topologies.md) recomendadas: analiza la topología que se va a usar en función del caso de uso y la opción de SRP

## Actualización {#upgrading}

Al actualizar a la plataforma AEM 6.5 desde versiones anteriores de AEM, es importante leer [Actualización a AEM 6.5](/help/sites-deploying/upgrade.md).

Además de actualizar la plataforma, lea [Actualización a AEM Communities 6.5](/help/communities/upgrade.md) para conocer los cambios de las comunidades.

## Configuraciones {#configurations}

### Editor principal {#primary-publisher}

Cuando la implementación elegida es un conjunto de servidores [de](/help/communities/topologies.md#tarmk-publish-farm)publicación, una instancia de publicación AEM debe identificarse como **`primary publisher`** para actividades que no deben producirse en todas las instancias, como las funciones que dependen de **notifications **o **Adobe Analytics**.

De forma predeterminada, la configuración de `AEM Communities Publisher Configuration` OSGi se configura con la casilla de verificación **`Primary Publisher`** activada, de modo que todas las instancias de publicación de un conjunto de servidores de publicación se identificarán como principales.

Por lo tanto, es necesario **editar la configuración en todas las instancias** de publicación secundarias para desmarcar la **`Primary Publisher`** casilla de verificación.

![](../assets/chlimage_1-126.png)

Para el resto de instancias de publicación (secundarias) en un conjunto de servidores de publicación:

* iniciar sesión con privilegios de administrador
* acceder a la consola [web](/help/sites-deploying/configuring-osgi.md)

   * por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* ubique la variable `AEM Communities Publisher Configuration`
* seleccione el icono de edición
* desmarcar la casilla **Editor** principal
* select **Save**

### Agentes de replicación en el autor {#replication-agents-on-author}

La replicación se utiliza para el contenido del sitio creado en el entorno de publicación, como grupos de la comunidad, así como para administrar miembros y grupos de miembros desde el entorno de creación mediante el servicio [de](#tunnel-service-on-author)túnel.

Para el publicador principal, asegúrese de que la configuración [del agente de](/help/sites-deploying/replication.md) replicación identifique correctamente al servidor de publicación y al usuario autorizado. El usuario autorizado predeterminado `admin,` ya tiene los permisos adecuados (es miembro de `Communities Administrators`).

Para que algún otro usuario tenga los permisos adecuados, debe agregarse como miembro al grupo de `administrators` usuarios (también como miembro de `Communities Administrators`).

Hay dos agentes de replicación en el entorno de creación que necesitan configurar correctamente la configuración de transporte.

* acceder a la consola de replicación en el autor

   * desde la navegación global: **Herramientas, implementación, replicación, agentes en el autor**

* seguir el mismo procedimiento para ambos agentes:

   * **Agente predeterminado (publicación)**
   * **Agente de replicación inversa (publicar en sentido inverso)**

      1. seleccione el agente
      1. select **edit**
      1. select the **Transport** tab
      1. si no es un puerto `4503`, edite el **URI** para especificar el puerto correcto

      1. si no es usuario `admin`, edite el **usuario** y la **contraseña** para especificar un miembro del grupo de `administrators` usuarios

Las siguientes imágenes muestran los resultados de cambiar el puerto de 4503 a 6103 por :

#### Agente predeterminado (publicación) {#default-agent-publish}

![configure-limit](../assets/configure-limits.png)

#### Agente de replicación inversa (publicar en sentido inverso) {#reverse-replication-agent-publish-reverse}

![](../assets/chlimage_1-128.png)

### Servicio de túnel en el autor {#tunnel-service-on-author}

Al utilizar el entorno de autor para [crear sitios](/help/communities/sites-console.md), [modificar propiedades](/help/communities/sites-console.md#modifying-site-properties) del sitio o [administrar miembros](/help/communities/members.md)de la comunidad, es necesario acceder a los miembros (usuarios) registrados en el entorno de publicación, no a los usuarios registrados en el autor.

El servicio de túnel proporciona este acceso mediante el agente de replicación del autor.

Para habilitar el servicio de túnel:

* en **autor**
* iniciar sesión con privilegios administrativos
* si publisher no es localhost:4503 o el usuario de transporte no lo es `admin`, [configure el agente de replicación](#replication-agents-on-author)

* acceder a la consola [web](/help/sites-deploying/configuring-osgi.md)

   * por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* ubique la variable `AEM Communities Publish Tunnel Service`
* seleccione el icono de edición
* marque la casilla **enable **box
* select **Save**

![](../assets/chlimage_1-129.png)

### Replicar la clave de cifrado {#replicate-the-crypto-key}

Existen dos funciones de AEM Communities que requieren que todas las instancias de servidor AEM utilicen las mismas claves de cifrado. Son [Analytics](/help/communities/analytics.md) y [ASRP](/help/communities/asrp.md).

A partir de AEM 6.3, el material clave se almacena en el sistema de archivos y ya no en el repositorio.

Para copiar el material clave del autor en todos los demás casos, es necesario:

* acceder a la instancia de AEM, normalmente una instancia de autor, que contiene el material clave que copiar

   * localice el `com.adobe.granite.crypto.file` paquete en el sistema de archivos local, por ejemplo:

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * el `bundle.info` archivo identificará el paquete
   * navegue a la carpeta de datos, por ejemplo:

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * copia de los archivos hmac y nodo principal



* para cada instancia de AEM de destinatario

   * navegue a la carpeta de datos, por ejemplo:

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * pegar los 2 archivos copiados anteriormente
   * es necesario [actualizar el paquete](#refresh-the-granite-crypto-bundle) Granite Crypto si la instancia de destinatario AEM se está ejecutando actualmente


>[!CAUTION]
>
>Si ya se ha configurado otra característica de seguridad basada en claves criptográficas, replicar las claves criptográficas podría dañar la configuración. Para obtener ayuda, [póngase en contacto con el servicio de atención](https://helpx.adobe.com/es/marketing-cloud/contact-support.html)al cliente.

#### Replicación del repositorio {#repository-replication}

El hecho de tener el material clave almacenado en el repositorio, como ocurrió con AEM 6.2 y versiones anteriores, se puede conservar especificando la siguiente propiedad del sistema en el primer inicio de cada instancia de AEM (que crea el repositorio inicial):

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>Es importante verificar que el agente de [replicación del autor](#replication-agents-on-author) esté correctamente configurado.

Con el material clave almacenado en el repositorio, la manera de replicar la clave criptográfica de autor a otras instancias es la siguiente:

Uso del [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* vaya a [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* select `/etc/key`
* abrir `Replication` , ficha
* select `Replicate`

* [actualizar el paquete Granite Crypto](#refresh-the-granite-crypto-bundle)

![](../assets/chlimage_1-130.png)

#### Actualizar el paquete de criptografía de granito {#refresh-the-granite-crypto-bundle}

* en cada instancia de publicación, acceda a la consola [web](/help/sites-deploying/configuring-osgi.md)

   * por ejemplo, [https://&lt;servidor>:&lt;puerto>/sistema/consola/paquetes](https://localhost:4503/system/console/bundles)

* localizar `Adobe Granite Crypto Support` paquete (com.adobe.granite.crypto)
* seleccionar **Actualizar**

![](../assets/chlimage_1-131.png)

* después de un momento, debería aparecer un **Éxito **diálogo :
   `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

Si utiliza el servidor Apache HTTP, asegúrese de utilizar el nombre de servidor correcto para todas las entradas relevantes.

En particular, tenga cuidado de utilizar el nombre de servidor correcto, no `localhost`, en el `RedirectMatch`.

#### muestra de httpd.conf {#httpd-conf-sample}

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

Si utiliza un despachante, consulte :

* Documentación de AEM [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)
* [Instalación de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Configuración de Dispatcher para Comunidades](/help/communities/dispatcher.md)
* [Problemas conocidos](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentación de comunidades relacionadas {#related-communities-documentation}

* Visite [Administración de sitios](/help/communities/administer-landing.md) de comunidades para obtener información sobre cómo crear un sitio de comunidad, configurar plantillas de sitio de comunidad, moderar contenido de comunidad, administrar miembros y configurar mensajes.

* Visite [Desarrollar comunidades](/help/communities/communities.md) para conocer el marco de componentes sociales (SCF) y personalizar componentes y características de Comunidades.

* Visite [Creación de componentes](/help/communities/author-communities.md) de comunidades para obtener información sobre cómo crear y configurar componentes de comunidades.

