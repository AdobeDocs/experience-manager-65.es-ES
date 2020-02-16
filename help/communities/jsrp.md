---
title: JSRP - Proveedor de recursos de almacenamiento JCR
seo-title: JSRP - Proveedor de recursos de almacenamiento JCR
description: JSRP es generalmente el más adecuado para entornos de demostración o desarrollo de una instancia de publicación y una instancia de autor
seo-description: JSRP es generalmente el más adecuado para entornos de demostración o desarrollo de una instancia de publicación y una instancia de autor
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
translation-type: tm+mt
source-git-commit: aa2c75e061e00ba74d54843a5f35bb7d82d12a92

---


# JSRP - Proveedor de recursos de almacenamiento JCR {#jsrp-jcr-storage-resource-provider}

## Acerca de JSRP {#about-jsrp}

Cuando AEM Communities utiliza JSRP como opción de almacenamiento (opción predeterminada), el contenido de la comunidad se almacena en JCR y el contenido generado por el usuario (UGC) solo se puede acceder desde la instancia de creación o publicación en la que se publicó.

Debido a la simplicidad de la implementación, JSRP es generalmente el más adecuado para entornos de demostración o desarrollo de una instancia de publicación y una instancia de autor.

Consulte también [Características de las Opciones](working-with-srp.md#characteristics-of-srp-options) de SRP y Topologías [](topologies.md)recomendadas.

## Configuración {#configuration}

### Seleccionar JSRP {#select-jsrp}

De forma predeterminada, JSRP es la opción de almacenamiento para UGC.

La consola [Configuración](srp-config.md) de almacenamiento permite seleccionar la configuración de almacenamiento predeterminada, que identifica la implementación de SRP que se va a utilizar.

En el entorno de creación, para llegar a la consola de configuración de almacenamiento

* Desde la navegación global: **[!UICONTROL Herramientas > Comunidades > Configuración de almacenamiento]**

![chlimage_1-234](assets/chlimage_1-234.png)

* Select **[!UICONTROL JCR Storage Resource Provider (JSRP)]**
* Seleccione **[!UICONTROL Enviar]**

### Publicación de la configuración {#publishing-the-configuration}

Aunque JSRP es la configuración predeterminada, para asegurarse de que la configuración idéntica se establece en el entorno de publicación:

* Sobre el autor:

   * Desde la navegación global: **[!UICONTROL Herramientas > Implementación > Replicación]**
   * Seleccione **[!UICONTROL Activar árbol]**
   * **[!UICONTROL Ruta de inicio]**:

      * Vaya a `/conf/global/settings/community/srpc/`
   * Seleccionar **[!UICONTROL activar]**


## Administración de datos de usuario {#managing-user-data}

Para obtener información sobre *usuarios*, perfiles *de* usuario y grupos *de* usuarios, que a menudo se introducen en el entorno de publicación, visite

* [Sincronización de usuarios](sync.md)
* [Administración de usuarios y grupos de usuarios](users.md)

## Solución de problemas {#troubleshooting}

### UGC no visible en JCR {#ugc-not-visible-in-jcr}

Compruebe la configuración de la opción de almacenamiento para asegurarse de que JSRP se ha configurado como el proveedor predeterminado. De forma predeterminada, el proveedor de recursos de almacenamiento es JSRP.

En todas las instancias de AEM de creación y publicación, vuelva a la consola de configuración de almacenamiento o compruebe el repositorio de AEM:

* en JCR, si [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * No contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) , significa que el proveedor de almacenamiento es JSRP
   * Si el nodo srpc existe y contiene la configuración [predeterminada](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)del nodo, las propiedades de configuración predeterminada deben definir JSRP para que sea el proveedor predeterminado

### UGC no visible en la instancia de creación {#ugc-not-visible-on-author-instance}

Esto no es un error. Una característica del JSRP es que el contenido de la comunidad introducido en el entorno de publicación solo será visible en el entorno de publicación.

### UGC no visible en instancia de publicación {#ugc-not-visible-on-publish-instance}

Si se implementa una única instancia de publicación o un clúster de publicación, siga las instrucciones para [UGC Not Visible en JCR](#ugc-not-visible-in-jcr).

Si se implementa un conjunto de servidores de publicación, una característica del JSRP es que el contenido de la comunidad solo estará visible en la instancia de publicación en la que se publicó.

Para que UGC esté visible desde cualquier instancia de publicación, se requiere un clúster de publicación.
