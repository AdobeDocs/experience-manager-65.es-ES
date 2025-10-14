---
title: Implementación de comunidades
description: Obtenga información sobre cómo implementar comunidades y funciones de la comunidad en Adobe Experience Manager.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1658'
ht-degree: 0%

---

# Implementación de comunidades {#deploying-communities}

## Requisitos previos {#prerequisites}

* [AEM Plataforma de.5](/help/sites-deploying/deploy.md)

* Licencia de AEM Communities

* Licencias opcionales para:

   * [Funciones de Adobe Analytics para comunidades](/help/communities/analytics.md)
   * [MongoDB para MSRP](/help/communities/msrp.md)
   * [Adobe Cloud para ASRP](/help/communities/asrp.md)

## Lista de comprobación de instalación {#installation-checklist}

AEM **Para la [plataforma de](/help/sites-deploying/deploy.md#what-is-aem)**

* AEM Instalar las últimas [actualizaciones de la versión 6.5 de](#aem64updates)

* Si no usa los puertos predeterminados (4502, 4503), [configure los agentes de replicación](#replication-agents-on-author)
* [Replicar la clave criptográfica](#replicate-the-crypto-key)
* Si es compatible con la globalización, [configure la traducción automatizada](/help/sites-administering/translation.md)
(se proporciona la configuración de muestra para el desarrollo)

**Para la [capacidad Communities](/help/communities/overview.md)**

* Si implementa una [granja de servidores de publicación](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [identifique el editor principal](#primary-publisher)

* [Habilitar el servicio de túnel](#tunnel-service-on-author)
* [Habilitar inicio de sesión social](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Configuración de Adobe Analytics](/help/communities/analytics.md)
* Configurar un [servicio de correo electrónico predeterminado](/help/communities/email.md)
* Identificar la opción de [almacenamiento UGC compartido](/help/communities/working-with-srp.md) (**SRP**)

   * Si MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [Instalación y configuración de MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [Configurar Solr](/help/communities/solr.md)
      * [Seleccionar MSRP](/help/communities/srp-config.md)

   * Si la base de datos relacional SRP [(DSRP)](/help/communities/dsrp.md)

      * [Instalar el controlador JDBC para MySQL](#jdbc-driver-for-mysql)
      * [Instalar y configurar MySQL para DSRP](/help/communities/dsrp-mysql.md)
      * [Configurar Solr](/help/communities/solr.md)
      * [Seleccionar DSRP](/help/communities/srp-config.md)

   * Si el Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * Póngase en contacto con su representante de cuentas para el aprovisionamiento
      * [Seleccionar ASRP](/help/communities/srp-config.md)

   * Si JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * No es un almacén de UGC (contenido generado por el usuario) compartido:

         * UGC nunca se replica
         * AEM UGC solo es visible en la instancia o clúster de la instancia o clúster en el que se ha introducido.

         * El valor predeterminado es JSRP

## Últimas versiones {#latest-releases}

AEM.5 Communities GA incluye el paquete Communities. AEM AEM Para obtener más información acerca de las actualizaciones de las [Comunidades](/help/release-notes/release-notes.md#experiencemanagercommunities) de la versión 6.5 de la versión, consulte las [Notas de la versión de la versión 6.5 de la versión](/help/release-notes/release-notes.md#communities-release-notes.html) de la versión de la versión 6..

### AEM Actualizaciones de.5 {#aem-updates}

AEM AEM A partir de la versión 6.4, las actualizaciones de las comunidades se entregarán como parte de los paquetes de correcciones acumulativas y paquetes de servicio de la aplicación de, que se incluyen en la versión de.

AEM Para obtener las últimas actualizaciones de la versión 6.5 de la versión, consulte [Paquetes de correcciones acumulativas y paquetes de servicio de Adobe Experience Manager 6.4](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates).

### Historial de versiones {#version-history}

AEM Al igual que en la versión 6.4 de y posteriores, las funciones y revisiones de AEM Communities forman parte de los paquetes de correcciones acumulativos y los paquetes de servicio de AEM Communities. Por lo tanto, no hay paquetes de funciones independientes.

### Controlador JDBC para MySQL {#jdbc-driver-for-mysql}

Una función de Communities utiliza una base de datos MySQL:

* Para [DSRP](/help/communities/dsrp.md): almacenando UGC

El conector MySQL debe obtenerse e instalarse por separado.

Los pasos necesarios son:

1. Descargar el archivo ZIP desde [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * La versión debe ser >= 5.1.38

1. Extraiga mysql-connector-java-&lt;version>-bin.jar (paquete) del archivo
1. Utilice la consola web para instalar e iniciar el paquete:

   * Por ejemplo, https://localhost:4502/system/console/bundles
   * Seleccionar **`Install/Update`**
   * Examinar... para seleccionar el paquete extraído del archivo ZIP descargado
   * Compruebe que el controlador JDBC de *Oracle Corporation para MySQLcom.mysql.jdbc* esté activo y, en caso contrario, inícielo (o compruebe los registros)

1. Si realiza la instalación en una implementación existente después de configurar JDBC, vuelva a enlazar JDBC al nuevo conector volviendo a guardar la configuración de JDBC desde la consola web :
   * Por ejemplo, https://localhost:4502/system/console/configMgr
   * Buscar configuración de `Day Commons JDBC Connections Pool`
   * Seleccionar para abrir
   * Seleccionar `Save`

1. Repita los pasos 3 y 4 en todas las instancias de autor y publicación

Encontrará más información sobre la instalación de paquetes en la página [Consola web](/help/sites-deploying/web-console.md).

#### Ejemplo : Paquete de conector MySQL instalado {#example-installed-mysql-connector-bundle}

![paquete de conector](assets/connector-bundle.png)



### AEM MLS avanzado de {#aem-advanced-mls}

Para que la colección SRP (MSRP o DSRP) admita la búsqueda multilingüe avanzada (MLS), se requieren nuevos complementos de Solr, además de un esquema personalizado y una configuración de Solr. Todos los elementos necesarios se empaquetan en un archivo zip descargable.

La descarga avanzada de MLS (también conocida como `phasetwo`) está disponible en el repositorio de Adobe:

* AEM-SOLR-MLS-phasettwo

  AEM Para obtener el paquete MLS avanzado, consulte [MLS avanzado](deploy-communities.md#aem-advanced-mls) en la sección de implementación de la documentación de &lbrace;Advanced MLS.

   * Versión 1.2.40, 6 de abril de 2016
   * AEM Descargar-SOLR-MLS-phasetwo-1.2.40.zip

Para obtener detalles e información de instalación, visite [Configuración de Solr](/help/communities/solr.md) para SRP.

### Acerca de los vínculos de Package Share {#about-links-to-package-share}

**Paquetes visibles en Adobe AEM Cloud**

AEM Los vínculos a los paquetes de esta página no requieren la ejecución de instancias de, tal como se encuentran en el recurso compartido de paquetes de `adobeaemcloud.com`. Mientras los paquetes estén visibles, el botón `Install` sirve para instalar los paquetes en un sitio alojado en el Adobe. AEM Si se va a realizar la instalación en una instancia de la instancia local de la, al seleccionar `Install` se producirá un error.

AEM **Cómo realizar la instalación en la instancia de la local**

AEM Para instalar los paquetes visibles en `adobeaemcloud.com` en una instancia local de, el paquete debe descargarse primero en un disco local:

* Seleccione la ficha **Assets**
* Seleccionar **descargar en disco**

AEM AEM En la instancia de la instancia local de la, use el Administrador de paquetes (por ejemplo, [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) para cargar en el repositorio de paquetes de la instancia local de la.

AEM AEM Como alternativa, al acceder al paquete mediante Package Share desde la instancia de la instancia de la instancia local de la instancia (por ejemplo, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), el botón `Download` se descarga en el repositorio de paquetes de la instancia de la instancia de la instancia local de la instancia de la instancia de la.

AEM Una vez que esté en el repositorio de paquetes de la instancia de la instancia local de, utilice el Administrador de paquetes para instalar el paquete.

Para obtener más información, visite [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md#package-share).

## Implementaciones recomendadas {#recommended-deployments}

En AEM Communities, se usa un almacén común para almacenar UGC y a menudo se denomina [proveedor de recursos de almacenamiento (SRP)](/help/communities/working-with-srp.md). La implementación recomendada se centra en elegir una opción de SRP para el almacén común.

El almacén común admite la moderación y el análisis de UGC en el entorno de publicación, a la vez que elimina la necesidad de [replicación](/help/communities/sync.md) de UGC.

* [Almacén de contenido de la comunidad](/help/communities/working-with-srp.md) : analiza las opciones de almacenamiento SRP para AEM Communities

* [Topologías recomendadas](/help/communities/topologies.md) : describe la topología que se debe usar según el caso de uso y la opción de SRP

## Actualización {#upgrading}

AEM AEM AEM Al actualizar a la plataforma de la versión 6.5 de la versión de la versión de la versión anterior de la versión de la versión de la versión de la versión de la versión de la versión, es importante leer [Actualización a la versión 6.5](/help/sites-deploying/upgrade.md) de la versión de la versión de la versión de la versión de la versión de la versión de la versión de la versión de la versión de.

Además de actualizar la plataforma, lea [Actualización a AEM Communities 6.5](/help/communities/upgrade.md) para obtener más información acerca de los cambios en las comunidades.

## Configuraciones {#configurations}

### Editor principal {#primary-publisher}

AEM Si la implementación elegida es una [granja de servidores de publicación](/help/communities/topologies.md#tarmk-publish-farm), se debe identificar una instancia de publicación como la **`primary publisher`** para las actividades que no deben producirse en todas las instancias. Por ejemplo, las características que dependen de **notifications** o **Adobe Analytics**.

De manera predeterminada, la configuración de OSGi `AEM Communities Publisher Configuration` está configurada con la casilla de verificación **`Primary Publisher`** marcada, de manera que todas las instancias de publicación de un conjunto de servidores de publicación se identificarían automáticamente como principales.

Por lo tanto, es necesario **editar la configuración en todas las instancias de publicación secundarias** para desactivar la casilla de verificación **`Primary Publisher`**.

![publicador principal](assets/primary-publisher.png)

Para todas las demás instancias de publicación (secundarias) de un conjunto de servidores de publicación:

* Iniciar sesión con privilegios de administrador
* Acceder a la [consola web](/help/sites-deploying/configuring-osgi.md)

   * Por ejemplo, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Buscar `AEM Communities Publisher Configuration`
* Seleccione el icono de edición
* Desmarque la casilla **Editor principal**
* Seleccionar **Guardar**

### Agentes de replicación en Autor {#replication-agents-on-author}

La replicación se utiliza para el contenido del sitio creado en el entorno de publicación, como los grupos de la comunidad, y para administrar miembros y grupos de miembros desde el entorno de creación mediante el [servicio de túnel](#tunnel-service-on-author).

Para el editor principal, asegúrese de que [Replication Agent Config](/help/sites-deploying/replication.md) identifica correctamente el servidor de publicación y al usuario autorizado. El usuario autorizado predeterminado `admin,` ya tiene los permisos apropiados (es miembro de `Communities Administrators`).

Para que otros usuarios tengan los permisos adecuados, deben agregarse como miembros al grupo de usuarios `administrators` (también como miembros de `Communities Administrators`).

Hay dos agentes de replicación en el entorno de creación que necesitan que la configuración de transporte esté correctamente configurada.

* Acceso a la consola de replicación en el autor

   * En la navegación global, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]** > **[!UICONTROL Agentes en el autor]**

* Siga el mismo procedimiento para ambos agentes:

   * **Agente predeterminado (publicar)**
   * **Agente de replicación inversa (publicación inversa)**

      1. Seleccione el agente
      1. Seleccionar **editar**
      1. Seleccione la ficha **Transporte**
      1. Si no es el puerto `4503`, edite el **URI** para especificar el puerto correcto

      1. Si no es el usuario `admin`, edite **Usuario** y **Contraseña** para especificar un miembro del grupo de usuarios `administrators`

Las siguientes imágenes muestran los resultados de cambiar el puerto de 4503 a 6103 por:

#### Agente predeterminado (publicar) {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### Agente de replicación inversa (publicación inversa) {#reverse-replication-agent-publish-reverse}

![agente de replicación inversa](assets/reverse-replication-agent.png)

### Servicio de túnel de autor {#tunnel-service-on-author}

Cuando se usa el entorno de creación para [crear sitios](/help/communities/sites-console.md), [modificar las propiedades del sitio](/help/communities/sites-console.md#modifying-site-properties) o [administrar los miembros de la comunidad](/help/communities/members.md), es necesario tener acceso a los miembros (usuarios) registrados en el entorno de publicación, no a los usuarios registrados en el autor.

El servicio de túnel proporciona este acceso mediante el agente de replicación en el autor.

Para habilitar el servicio de túnel:

* Inicie sesión con privilegios administrativos en la instancia de autor.
* Si el publicador no es localhost:4503 o el usuario de transporte no es `admin`,
entonces [configure el agente de replicación](#replication-agents-on-author)

* Acceder a la [consola web](/help/sites-deploying/configuring-osgi.md)

   * Por ejemplo, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Buscar `AEM Communities Publish Tunnel Service`
* Seleccione el icono de edición
* Marque la casilla **habilitar**
* Seleccionar **Guardar**

  ![servicio-túnel](assets/tunnel-service.png)

### Replicar la clave criptográfica {#replicate-the-crypto-key}

Existen dos funciones de AEM Communities AEM que requieren que todas las instancias de servidor de la utilicen las mismas claves de cifrado. Estos son [Analytics](/help/communities/analytics.md) y [ASRP](/help/communities/asrp.md).

AEM A partir de la versión 6.3, el material clave se almacena en el sistema de archivos y ya no en el repositorio.

Para copiar el material clave de Autor en todas las demás instancias, es necesario:

* AEM Acceda a la instancia de (normalmente una instancia de autor) que contiene el material clave que desea copiar

   * Busque el paquete `com.adobe.granite.crypto.file` en el sistema de archivos local,
por ejemplo,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * El archivo `bundle.info` identifica el paquete

   * Vaya a la carpeta de datos,
por ejemplo,

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * Copie los archivos hmac y del nodo principal

* AEM Para cada instancia de destino de la

   * Vaya a la carpeta de datos,
por ejemplo,

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * Pegue los dos archivos copiados anteriormente
   * AEM Es necesario [actualizar el paquete Granite Crypto](#refresh-the-granite-crypto-bundle) si se está ejecutando la instancia de destino

>[!CAUTION]
>
>Si ya se ha configurado otra característica de seguridad basada en las claves criptográficas, la replicación de las claves criptográficas podría dañar la configuración. Para obtener ayuda, [póngase en contacto con el Servicio de atención al cliente](https://experienceleague.adobe.com/es?support-solution=General&support-tab=home&lang=es#support).

#### Replicación del repositorio {#repository-replication}

AEM Se puede conservar el material clave almacenado en el repositorio, como era el caso de la versión 6.2 y anteriores de la. AEM Especifique la propiedad del sistema `-Dcom.adobe.granite.crypto.file.disable=true` en el primer inicio de cada instancia de la instancia de la (que crea el repositorio inicial).

>[!NOTE]
>
>Compruebe que el agente de replicación [de Author](#replication-agents-on-author) esté configurado correctamente.

Con el material de clave almacenado en el repositorio, la manera de replicar la clave criptográfica desde el autor a otras instancias es la siguiente:

Usando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Vaya a [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Seleccionar `/etc/key`
* Abrir la ficha `Replication`
* Seleccionar `Replicate`

* [Actualizar el paquete de Granite Crypto](#refresh-the-granite-crypto-bundle)

  ![repositorio replicare](assets/replicare-repository.png)

#### Actualizar el paquete de cifrado de Granite {#refresh-the-granite-crypto-bundle}

* En cada instancia de publicación, acceda a la [consola web](/help/sites-deploying/configuring-osgi.md)

   * Por ejemplo, [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* Busque el paquete `Adobe Granite Crypto Support` (com.adobe.granite.crypto)
* Seleccionar **Actualizar**

  ![cripto de granito](assets/granite-crypto.png)

* Después de un momento, debería aparecer un cuadro de diálogo **Correcto**:
  `Operation completed successfully.`

### Servidor HTTP Apache {#apache-http-server}

Si utiliza el servidor HTTP de Apache, asegúrese de utilizar el nombre de servidor correcto para todas las entradas relevantes.

En particular, asegúrese de usar el nombre de servidor correcto, no `localhost`, en `RedirectMatch`.

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

Si utiliza un Dispatcher, consulte:

* AEM Documentación de [Dispatcher](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates) de la
* [Instalación de Dispatcher](https://experienceleague.adobe.com/es/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install)
* [Configuración de Dispatcher para comunidades](/help/communities/dispatcher.md)
* [Problemas conocidos](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## Documentación de comunidades relacionadas {#related-communities-documentation}

* Visite [Sitios de administración de comunidades](/help/communities/administer-landing.md) para obtener información sobre cómo crear un sitio de comunidad, configurar plantillas de sitios de comunidad, moderar contenido de la comunidad, administrar miembros y configurar mensajes.

* Visite [Desarrollo de comunidades](/help/communities/communities.md), donde podrá obtener información acerca del marco de componentes sociales (SCF) y la personalización de componentes y características de las comunidades.

* Visite [Creación de componentes de comunidades](/help/communities/author-communities.md), donde aprenderá a crear y configurar componentes de comunidades.
