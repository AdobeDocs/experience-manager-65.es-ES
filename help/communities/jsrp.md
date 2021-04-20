---
title: 'JSRP: proveedor de recursos de almacenamiento JCR'
seo-title: 'JSRP: proveedor de recursos de almacenamiento JCR'
description: JSRP es generalmente el más adecuado para entornos de demostración o desarrollo de una instancia de publicación y una instancia de autor
seo-description: JSRP es generalmente el más adecuado para entornos de demostración o desarrollo de una instancia de publicación y una instancia de autor
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---


# JSRP - Proveedor de recursos de almacenamiento JCR {#jsrp-jcr-storage-resource-provider}

## Acerca de JSRP {#about-jsrp}

Cuando AEM Communities utiliza JSRP como opción de almacenamiento (la predeterminada), el contenido de la comunidad se almacena en JCR y el contenido generado por el usuario (UGC) solo es accesible desde la instancia de autor o publicación en la que se publicó.

Debido a la simplicidad de la implementación, JSRP es generalmente el más adecuado para entornos de demostración o desarrollo de una instancia de publicación y una instancia de autor.

Consulte también [Características de las opciones de SRP](working-with-srp.md#characteristics-of-srp-options) y [Topologías recomendadas](topologies.md).

## Configuración {#configuration}

### Seleccione JSRP {#select-jsrp}

De forma predeterminada, JSRP es la opción de almacenamiento para UGC.

La [consola de configuración de almacenamiento](srp-config.md) permite seleccionar la configuración de almacenamiento predeterminada, que identifica qué implementación de SRP utilizar.

En el entorno de creación, para llegar a la consola de configuración de almacenamiento

* Desde la navegación global: **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Configuración del almacenamiento]**

* Seleccione **[!UICONTROL proveedor de recursos de almacenamiento JCR (JSRP)]**

* Seleccione **[!UICONTROL Enviar]**

![jsrp-configuration](assets/jsrp-configuration.png)

### Publicación de la configuración {#publishing-the-configuration}

Aunque JSRP es la configuración predeterminada, para garantizar que la configuración idéntica esté establecida en el entorno de publicación:

* Desde la navegación global: **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]**
* Seleccione **[!UICONTROL Activar árbol]** > **[!UICONTROL Ruta de inicio]**:

   * Vaya a `/conf/global/settings/community/srpc/`

* Seleccione **[!UICONTROL Activar]**

## Administración de datos de usuario {#managing-user-data}

Para obtener información sobre *usuarios*, *perfiles de usuario* y *grupos de usuarios*, que a menudo se introducen en el entorno de publicación, visite:

* [Sincronización de usuarios](sync.md)
* [Administración de usuarios y grupos de usuarios](users.md)

## Solución de problemas {#troubleshooting}

### UGC no visible en JCR {#ugc-not-visible-in-jcr}

Asegúrese de que JSRP se haya configurado para ser el proveedor predeterminado comprobando la configuración de la opción de almacenamiento. De forma predeterminada, el proveedor de recursos de almacenamiento es JSRP.

En todas las instancias de creación y publicación de AEM, vuelva a la consola Configuración de almacenamiento o compruebe el repositorio de AEM:

* En JCR, si [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * No contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc), significa que el proveedor de almacenamiento es JSRP.
   * Si el nodo srpc existe y contiene el nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), las propiedades de la configuración predeterminada deben definir JSRP para que sea el proveedor predeterminado.

### UGC no visible en la instancia de autor {#ugc-not-visible-on-author-instance}

Este no es un error. Una característica de JSRP es que el contenido de la comunidad introducido en el entorno de publicación solo será visible en el entorno de publicación.

### UGC no visible en la instancia de publicación {#ugc-not-visible-on-publish-instance}

Si se implementa una sola instancia de publicación o un clúster de publicación, siga las instrucciones para [UGC Not Visible in JCR](#ugc-not-visible-in-jcr).

Si se implementa un conjunto de servidores de publicación, una característica de JSRP es que el contenido de la comunidad solo será visible en la instancia de publicación en la que se publicó.

Para que UGC sea visible desde cualquier instancia de publicación, se requiere un clúster de publicación.
