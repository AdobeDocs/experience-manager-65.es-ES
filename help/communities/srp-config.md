---
title: Configuración de almacenamiento
description: Obtenga información acerca de la consola Configuración de almacenamiento como medio para identificar el almacenamiento elegido para el contenido de la comunidad, también conocido como contenido generado por el usuario.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 4%

---

# Configuración de almacenamiento {#storage-configuration}

La configuración de almacenamiento es el medio para identificar el almacenamiento elegido para el contenido de la comunidad, también conocido como contenido generado por el usuario (UGC).

Esta configuración informa al código AEM Communities de qué implementación del proveedor de recursos de almacenamiento (SRP) se utiliza al acceder a UGC. Debe reflejar la topología establecida cuando se implementó Adobe Experience Manager AEM ().

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

AEM Si no se realiza ninguna selección, el valor predeterminado es el repositorio de, JCR.

JCR es *no* un almacén común compartido por los entornos Author y Publish. El contenido de la comunidad solo es visible desde el entorno de creación o publicación en el que se creó.

Visita [Almacén JCR](jsrp.md) para obtener más información.

>[!NOTE]
>
>La ausencia del nodo `srpc` bajo `/etc/socialconfig` indica el valor predeterminado [Almacén JCR](jsrp.md).
