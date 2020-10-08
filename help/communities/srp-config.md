---
title: Configuración de almacenamiento
seo-title: Configuración de almacenamiento
description: Cómo acceder a la consola de configuración de Almacenamiento
seo-description: Cómo acceder a la consola de configuración de Almacenamiento
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 5%

---


# Configuración de almacenamiento {#storage-configuration}

La configuración de almacenamiento es el medio para identificar el almacenamiento elegido para el contenido de la comunidad, también conocido como contenido generado por el usuario (UGC).

Esta configuración informa al código de AEM Communities de la implementación del proveedor de recursos de almacenamiento (SRP) que se va a utilizar al acceder a UGC y debe reflejar la topología establecida cuando se implementó AEM.

Para consultar las opciones de almacenamiento y las topologías de implementación, visite:

* [Tienda de contenido de la comunidad](working-with-srp.md)
* [Topologías recomendadas](topologies.md)

## Consola de configuración de almacenamiento {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

En el entorno de creación, para llegar a la consola de configuración de almacenamiento.

* En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > Configuración de **[!UICONTROL Almacenamiento]**

Para seleccionar una opción de almacenamiento distinta del JCR predeterminado:

* Seleccione una opción
* Configurar correctamente

   * Ver detalles para [seleccionar MSRP](msrp.md#select-msrp)
   * Ver detalles para [seleccionar DSRP](dsrp.md#select-dsrp)
   * Ver detalles para [seleccionar ASRP](asrp.md#select-asrp)

* Seleccione **[!UICONTROL Enviar]**.

### Acerca del Almacenamiento JCR {#about-jcr-storage}

Tenga en cuenta que si no se realiza ninguna selección, el valor predeterminado es el repositorio de AEM, JCR.

JCR *no es* un almacén común compartido por el autor y los entornos de publicación. El contenido de la comunidad solo estará visible desde el entorno de creación o publicación en el que se creó.

Visite la tienda [JCR](jsrp.md) para obtener más información.

>[!NOTE]
>
>La ausencia del nodo `srpc` en `/etc/socialconfig` indica el almacén [](jsrp.md)JCR predeterminado.
