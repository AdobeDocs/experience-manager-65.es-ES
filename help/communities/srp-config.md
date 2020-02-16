---
title: Configuración de almacenamiento
seo-title: Configuración de almacenamiento
description: Cómo acceder a la Consola de configuración de almacenamiento
seo-description: Cómo acceder a la Consola de configuración de almacenamiento
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de almacenamiento {#storage-configuration}

La configuración del almacenamiento es el medio para identificar el almacenamiento elegido para el contenido de la comunidad, también conocido como contenido generado por el usuario (UGC, por sus siglas en inglés).

Esta configuración informa al código de Comunidades de AEM de la implementación del proveedor de recursos de almacenamiento (SRP) que se va a utilizar al acceder a UGC y debe reflejar la topología establecida cuando se implementó AEM.

Para consultar las opciones de almacenamiento y las topologías de implementación, visite

* [Tienda de contenido de la comunidad](working-with-srp.md)
* [Topologías recomendadas](topologies.md)

## Consola de configuración de almacenamiento {#storage-configuration-console}

![chlimage_1-188](assets/chlimage_1-188.png)

En el entorno de creación, para llegar a la consola de configuración de almacenamiento

* Desde la navegación global: **[!UICONTROL Herramientas > Comunidades > Configuración de almacenamiento]**

Para seleccionar una opción de almacenamiento que no sea el JCR predeterminado:

* seleccionar una opción
* Configurar correctamente

   * Ver detalles para [seleccionar MSRP](msrp.md#select-msrp)
   * Ver detalles para [seleccionar DSRP](dsrp.md#select-dsrp)
   * Ver detalles para [seleccionar ASRP](asrp.md#select-asrp)

* Seleccione **[!UICONTROL Enviar]**

### Acerca del almacenamiento JCR {#about-jcr-storage}

Tenga en cuenta que si no se realiza ninguna selección, el valor predeterminado es el repositorio de AEM, JCR.

JCR *no es* un almacén común compartido por los entornos de creación y publicación. El contenido de la comunidad solo estará visible desde el entorno de creación o publicación en el que se creó.

Visite la tienda [JCR](jsrp.md) para obtener más información.

>[!NOTE]
>
>La ausencia del nodo `srpc`en `/etc/socialconfig` indica el almacén [](jsrp.md)JCR predeterminado.

