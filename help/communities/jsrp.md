---
title: 'JSRP: proveedor de recursos de almacenamiento de JCR'
description: JSRP es más adecuado para entornos de demostración o desarrollo de una instancia de Publish y una instancia de autor
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# JSRP: proveedor de recursos de almacenamiento de JCR {#jsrp-jcr-storage-resource-provider}

## Acerca de JSRP {#about-jsrp}

Cuando AEM Communities utiliza JSRP como opción de almacenamiento (la predeterminada), el contenido de la comunidad se almacena en el JCR y el contenido generado por el usuario (UGC) solo es accesible desde la instancia de autor o publicación en la que se publicó.

Debido a la simplicidad de la implementación, JSRP es más adecuado para entornos de demostración o desarrollo de una instancia de Publish y una instancia de autor.

Vea también [Características de las opciones de SRP](working-with-srp.md#characteristics-of-srp-options) y [Topologías recomendadas](topologies.md).

## Configuración {#configuration}

### Seleccionar JSRP {#select-jsrp}

De forma predeterminada, JSRP es la opción de almacenamiento de UGC.

La [consola de configuración de almacenamiento](srp-config.md) permite seleccionar la configuración de almacenamiento predeterminada, que identifica qué implementación de SRP utilizar.

En el entorno de creación, para llegar a la consola Configuración de almacenamiento

* Desde la navegación global: **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Configuración de almacenamiento]**

* Seleccione **[!UICONTROL Proveedor de recursos de almacenamiento JCR (JSRP)]**

* Seleccionar **[!UICONTROL Enviar]**

![jsrp-configuration](assets/jsrp-configuration.png)

### Publicación de la configuración {#publishing-the-configuration}

Aunque JSRP es la configuración predeterminada, para asegurarse de que se establece la configuración idéntica en el entorno de publicación:

* Desde la navegación global: **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]**
* Seleccione **[!UICONTROL Activar árbol]** > **[!UICONTROL Ruta de inicio]**:

   * Examinar `/conf/global/settings/community/srpc/`

* Seleccionar **[!UICONTROL Activar]**

## Administración de datos de usuario {#managing-user-data}

Para obtener información sobre *usuarios*, *perfiles de usuario* y *grupos de usuarios* que se especifican con frecuencia en el entorno de publicación, visite:

* [Sincronización de usuarios](sync.md)
* [Administración de usuarios y grupos de usuarios](users.md)

## Resolución de problemas {#troubleshooting}

### UGC no visible en JCR {#ugc-not-visible-in-jcr}

Asegúrese de que JSRP se ha configurado para ser el proveedor predeterminado comprobando la configuración de la opción de almacenamiento. De forma predeterminada, el proveedor de recursos de almacenamiento es JSRP.

En todas las instancias de autor y de Publish AEM AEM, vuelva a visitar la consola Configuración de almacenamiento o marque el repositorio de:

* En JCR, si [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * No contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc), lo que significa que el proveedor de almacenamiento es JSRP.
   * Si el nodo srpc existe y contiene el nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), las propiedades de defaultconfiguration deben definir JSRP para que sea el proveedor predeterminado.

### UGC no visible en la instancia de autor {#ugc-not-visible-on-author-instance}

Esto no es un error. Una característica de JSRP es que el contenido de la comunidad introducido en el entorno de publicación solo es visible en el entorno de Publish.

### UGC no visible en la instancia de Publish {#ugc-not-visible-on-publish-instance}

Si hay una sola instancia de Publish o un clúster de publicación implementado, siga las instrucciones de [UGC Not Visible in JCR](#ugc-not-visible-in-jcr).

Si se implementa un conjunto de servidores de publicación, una característica de JSRP es que el contenido de la comunidad solo es visible en la instancia de Publish en la que se publicó.

Para que UGC sea visible desde cualquier instancia de Publish, se requiere un clúster de publicación.
