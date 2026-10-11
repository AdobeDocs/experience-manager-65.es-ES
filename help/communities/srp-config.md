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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 4%
---
# Configuración de almacenamiento {#storage-configuration}

La configuración de almacenamiento es el medio para identificar el almacenamiento elegido para el contenido de la comunidad, también conocido como contenido generado por el usuario (UGC).

Esta configuración informa al código AEM Communities de qué implementación del proveedor de recursos de almacenamiento (SRP) se utiliza al acceder a UGC. Debe reflejar la topología establecida cuando se implementó Adobe Experience Manager (AEM).

Para ver un análisis de las opciones de almacenamiento y las topologías de implementación, visite:

* [Almacenamiento de contenido de comunidad](working-with-srp.md)
* [Topologías recomendadas](topologies.md)

## Consola de configuración de almacenamiento {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

En el entorno de creación, para acceder a la consola de configuración de Storage.

* En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Configuración de almacenamiento]**

Para seleccionar una opción de almacenamiento que no sea el JCR predeterminado:

* Seleccione una opción
* Configure correctamente

  * Ver detalles de [seleccionar MSRP](msrp.md#select-msrp)
  * Ver detalles de [seleccionar DSRP](dsrp.md#select-dsrp)
  * Ver detalles de [seleccionar ASRP](asrp.md#select-asrp)

* Seleccione **[!UICONTROL Enviar]**.

### Acerca del almacenamiento JCR {#about-jcr-storage}

Si no se realiza ninguna selección, el valor predeterminado es el repositorio de AEM, JCR.

JCR *no es* un almacén común compartido por los entornos Author y Publish. El contenido de la comunidad solo es visible desde el entorno de creación o publicación en el que se creó.

Visite [Tienda JCR](jsrp.md) para obtener más información.

>[!NOTE]
>
>La ausencia del nodo `srpc` en `/etc/socialconfig` indica el almacén JCR [predeterminado](jsrp.md).
