---
title: Configuración de almacenamiento
seo-title: Configuración de almacenamiento
description: Acceso a la Consola de Configuración de Almacenamiento
seo-description: Acceso a la Consola de Configuración de Almacenamiento
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 5%

---


# Configuración de almacenamiento {#storage-configuration}

La configuración del almacenamiento es la forma de identificar el almacenamiento elegido para el contenido de la comunidad, también conocido como contenido generado por el usuario (UGC).

Esta configuración informa al código de AEM Communities de qué implementación del proveedor de recursos de almacenamiento (SRP) se utilizará al acceder a UGC y debe reflejar la topología establecida cuando se implementó AEM.

Para un análisis de las opciones de almacenamiento y las topologías de implementación, visite:

* [Almacenamiento de contenido de la comunidad](working-with-srp.md)
* [Topologías recomendadas](topologies.md)

## Consola de configuración de almacenamiento {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

En el entorno de creación, para llegar a la consola de configuración de almacenamiento.

* En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Configuración del almacenamiento]**

Para seleccionar una opción de almacenamiento que no sea el JCR predeterminado:

* Seleccione una opción
* Configure correctamente

   * Consulte los detalles para [seleccionar MSRP](msrp.md#select-msrp)
   * Consulte los detalles para [seleccionar DSRP](dsrp.md#select-dsrp)
   * Consulte los detalles para [seleccionar ASRP](asrp.md#select-asrp)

* Seleccione **[!UICONTROL Enviar]**.

### Acerca del almacenamiento JCR {#about-jcr-storage}

Tenga en cuenta que si no se realiza ninguna selección, el valor predeterminado es el repositorio AEM, JCR.

JCR es *no* un almacén común compartido por los entornos de autor y publicación. El contenido de la comunidad solo será visible desde el entorno de creación o publicación en el que se creó.

Visite [JCR Store](jsrp.md) para obtener más información.

>[!NOTE]
>
>La ausencia del nodo `srpc` en `/etc/socialconfig` indica el [almacén de JCR](jsrp.md) predeterminado.
