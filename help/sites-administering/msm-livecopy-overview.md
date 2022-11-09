---
title: Información general de Live Copy
seo-title: Live Copy Overview Console
description: Obtenga información sobre los conceptos básicos de la Consola de información general de Live Copy.
seo-description: Learn about the basics of the Live Copy Overview Console.
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
feature: Multi Site Manager
exl-id: 0c3488bd-5f32-4956-882c-93326a45b379
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 34%

---

# Información general de Live Copy{#live-copy-overview-console}

La variable **Información general de Live Copy** permite:

* Ver/administrar la herencia en un sitio:

   * Ver el árbol de modelo y la estructura de Live Copy correspondiente, junto con su estado de herencia
   * Cambiar el estado de herencia; por ejemplo, suspender, reanudar
   * Ver propiedades de modelo y Live Copy

* Realizar acciones de despliegue

## Apertura de la información general de Live Copy {#opening-the-live-copy-overview}

Puede abrir la Información general de Live Copy desde estas ubicaciones:

* [Panel lateral Referencias de una página de modelo (consola Sites)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Propiedades de una página de modelo](#opening-live-copy-overview-properties-of-a-blueprint-page)

### Apertura de la información general de Live Copy: Referencias para una página de modelo {#opening-live-copy-overview-references-for-a-blueprint-page}

La **Información general de Live Copy** se puede abrir desde el panel lateral **Referencias** de la consola **Sites**:

1. En la consola **Sites**, [vaya a la página de modelo y selecciónela](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Abra el **[Referencias](/help/sites-authoring/basic-handling.md#references)** panel y seleccione **Live Copies**.

   ![chlimage_1-359](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >También puede abrir Referencias primero y luego seleccionar el modelo.

1. Select **Información general de Live Copy** para mostrar y utilizar la descripción general de todas las Live Copies relacionadas con el modelo seleccionado.
1. Use **Cerrar** para salir y volver a la consola **Sites**.

### Información general sobre la apertura de Live Copy: Propiedades de una página de modelo {#opening-live-copy-overview-properties-of-a-blueprint-page}

La **Información general de Live Copy** se puede abrir al ver las propiedades de una página de modelo:

1. Abra las **Propiedades** de la página de modelo adecuada.
1. Abra la pestaña **Modelo**, la **Información general de Live Copy** se mostrará en la barra de herramientas superior:

   ![chlimage_1-360](assets/chlimage_1-360.png)

1. Select **Información general de Live Copy** para mostrar y utilizar la descripción general de todas las Live Copies relacionadas con el modelo actual.

   >[!NOTE]
   >
   >Para obtener más información, consulte también el artículo de la Base de conocimiento [Mensaje de estado de Livecopy: Sincronización Up-to-date/Green/In](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

1. Use **Cerrar** para salir y volver a la consola **Sites**.

## Información general sobre el uso de Live Copy {#using-the-live-copy-overview}

La variable **Información general de Live Copy** también se puede utilizar para realizar acciones en la Live Copy:

1. Abra la **Información general de Live Copy**.
1. Seleccione el modelo o la página de Live Copy necesarios: la barra de herramientas se actualizará para mostrar las acciones disponibles. La variable [acciones](/help/sites-administering/msm.md#terms-used) disponible dependen de si selecciona un [modelo](#actions-for-a-blueprint-page) o [live copy](#actions-for-a-live-copy-page) página:

### Acciones para una página de modelo {#actions-for-a-blueprint-page}

Cuando selecciona una página de modelo, están disponibles las siguientes acciones:

![chlimage_1-361](assets/chlimage_1-361.png)

* Editar

   * Abra la página de modelo para editarla.

* [Despliegue](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Realice un despliegue para insertar los cambios del origen a la Live Copy.

### Acciones para una página de Live Copy {#actions-for-a-live-copy-page}

Cuando selecciona una página de Live Copy, están disponibles las siguientes acciones:

![chlimage_1-362](assets/chlimage_1-362.png)

* Editar

   * Abra la página Live Copy para editarla.

* [Estado de la relación](#relationship-status)

   * Vea información sobre el estado y la herencia.

* [Sincronizar](/help/sites-administering/msm.md#rollout-and-synchronize)

   * Sincronice una Live Copy para extraer cambios del origen a la Live Copy.

* [Restablecer](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * Restablezca una página de Live Copy para eliminar todas las cancelaciones de herencia y devolver la página al mismo estado que la página de origen.

* [Suspender](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * Desactiva temporalmente la relación activa entre una Live Copy y su página de modelo.

* [Reanudar](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * La opción Reanudar le permite restablecer una relación suspendida.

* [Desasociar](/help/sites-administering/msm.md#detaching-a-live-copy)

   * Elimina permanentemente la relación activa entre una Live Copy y su página de modelo.

## Estado de la relación {#relationship-status}

La consola **Estado de la relación** tiene dos pestañas que proporcionan una amplia gama de funcionalidades:

* [Información sobre el estado de relación](#relationship-status-information)
* [Información de Live Copy](#live-copy-information)

### Información sobre el estado de relación {#relationship-status-information}

Esta pestaña proporciona información detallada sobre el estado de la relación entre el modelo y la Live Copy:

![chlimage_1-363](assets/chlimage_1-363.png)

### Información de Live Copy {#live-copy-information}

Esta pestaña le permite ver y editar la configuración de la Live Copy:

![chlimage_1-364](assets/chlimage_1-364.png)
