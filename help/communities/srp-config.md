---
title: Configuración de almacenamiento
seo-title: Storage Configuration
description: Acceso a la Consola de Configuración de Almacenamiento
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

La configuración del almacenamiento es la forma de identificar el almacenamiento elegido para el contenido de la comunidad, también conocido como contenido generado por el usuario (UGC).

Esta configuración informa al código de AEM Communities de qué implementación del proveedor de recursos de almacenamiento (SRP) se utilizará al acceder a UGC y debe reflejar la topología establecida cuando se implementó AEM.

Para un análisis de las opciones de almacenamiento y las topologías de implementación, visite:

* [Almacenamiento de contenido de la comunidad](working-with-srp.md)
* [Topologías recomendadas](topologies.md)

## Consola de configuración de almacenamiento {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

En el entorno de creación, para llegar a la consola de configuración de almacenamiento.

* En la navegación global, seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Configuración de almacenamiento]**

Para seleccionar una opción de almacenamiento que no sea el JCR predeterminado:

* Seleccione una opción
* Configure correctamente

   * Consulte los detalles para [selección de MSRP](msrp.md#select-msrp)
   * Consulte los detalles para [seleccionar DSRP](dsrp.md#select-dsrp)
   * Consulte los detalles para [seleccionar ASRP](asrp.md#select-asrp)

* Seleccione **[!UICONTROL Enviar]**.

### Acerca del almacenamiento JCR {#about-jcr-storage}

Tenga en cuenta que si no se realiza ninguna selección, el valor predeterminado es el repositorio AEM, JCR.

JCR es *not* una tienda común compartida por los entornos de autor y publicación. El contenido de la comunidad solo será visible desde el entorno de creación o publicación en el que se creó.

Visita [Almacenamiento JCR](jsrp.md) para obtener más información.

>[!NOTE]
>
>La ausencia del nodo `srpc` under `/etc/socialconfig` indica el valor predeterminado [Almacén JCR](jsrp.md).
