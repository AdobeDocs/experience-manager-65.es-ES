---
title: Configuración de almacenamiento
seo-title: Storage Configuration
description: Cómo acceder a la consola de configuración de almacenamiento
seo-description: How to access the Storage Configuration Console
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 4%

---

# Configuración de almacenamiento {#storage-configuration}

La configuración de almacenamiento es el medio para identificar el almacenamiento elegido para el contenido de la comunidad, también conocido como contenido generado por el usuario (UGC).

Esta configuración informa al código AEM Communities AEM de qué implementación del proveedor de recursos de almacenamiento (SRP) se va a utilizar al acceder a UGC y debe reflejar la topología establecida cuando se implementó el.

Para ver un análisis de las opciones de almacenamiento y las topologías de implementación, visite:

* [Almacenamiento de contenido de comunidad](working-with-srp.md)
* [Topologías recomendadas](topologies.md)

## Consola de configuración de almacenamiento {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

En el entorno de creación, para acceder a la consola de configuración de Storage.

* En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Communities]** > **[!UICONTROL Configuración de almacenamiento]**

Para seleccionar una opción de almacenamiento que no sea el JCR predeterminado:

* Seleccione una opción
* Configure correctamente

   * Ver detalles de [seleccionar MSRP](msrp.md#select-msrp)
   * Ver detalles de [seleccionar DSRP](dsrp.md#select-dsrp)
   * Ver detalles de [seleccionar ASRP](asrp.md#select-asrp)

* Seleccione **[!UICONTROL Enviar]**.

### Acerca del almacenamiento JCR {#about-jcr-storage}

AEM Tenga en cuenta que si no se realiza ninguna selección, el valor predeterminado es el repositorio de, JCR.

JCR es *no* un almacén común compartido por los entornos de creación y publicación. El contenido de la comunidad solo será visible desde el entorno de creación o publicación en el que se creó.

Visita [Almacén JCR](jsrp.md) para obtener más información.

>[!NOTE]
>
>La ausencia del nodo `srpc` bajo `/etc/socialconfig` indica el valor predeterminado [Almacén JCR](jsrp.md).
