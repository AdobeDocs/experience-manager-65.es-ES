---
title: Configurar Deshacer para editar páginas
seo-title: Configuring Undo for Page Editing
description: AEM Obtenga información sobre cómo configurar la compatibilidad con Deshacer para la edición de páginas en la.
seo-description: Learn how to configure Undo support for page editing in AEM.
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
exl-id: 2cf3ac3f-ee17-480d-a32a-c57631502693
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 3%

---

# Configurar Deshacer para editar páginas{#configuring-undo-for-page-editing}

El [Servicio OSGi](/help/sites-deploying/configuring-osgi.md)  **Configuración de deshacer de CQ WCM por día** ( `com.day.cq.wcm.undo.UndoConfigService`) expone varias propiedades que controlan el comportamiento de los comandos Deshacer y Rehacer para editar páginas.

## Configuración predeterminada {#default-configuration}

En una instalación estándar, la configuración predeterminada se define como propiedades en la `sling:OsgiConfig`nodo:

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

Este nodo contiene `cq.wcm.undo.whitelist` y `cq.wcm.undo.blacklist` , para las demás propiedades se toman los valores predeterminados.

>[!CAUTION]
>
>Usted ***debe*** no cambie nada en el `/libs` ruta.
>
>Esto se debe al contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de funciones).

## Configuración de Deshacer y Rehacer {#configuring-undo-and-redo}

Puede configurar estas propiedades del servicio OSGi para su propia instancia.

>[!NOTE]
>
>AEM Al trabajar con los servicios de configuración, existen varios métodos para administrar los parámetros de configuración de dichos servicios; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

A continuación, se enumeran las propiedades tal como se muestran en la consola web, seguidas del nombre del parámetro OSGi correspondiente, junto con una descripción y el valor predeterminado (cuando corresponda):

* **Enable**
( `cq.wcm.undo.enabled`)

   * **Descripción**: Determina si los autores de la página pueden deshacer y rehacer los cambios.
   * **Predeterminado**: `Selected`
   * **Tipo**: `Boolean`

* **Ruta**
( `cq.wcm.undo.path`)

   * **Descripción**: Ruta del repositorio para los datos de deshacer binarios persistentes. Cuando los autores cambian datos binarios, como imágenes, la versión original de los datos se mantiene aquí. Cuando se deshacen los cambios en los datos binarios, estos datos de deshacer binarios se restauran en la página.
   * **Predeterminado**: `/var/undo`
   * **Tipo**: `String`

  >[!NOTE]
  >
  >De forma predeterminada, solo los administradores pueden acceder a `/var/undo` nodo. Los autores solo pueden realizar operaciones de deshacer y rehacer en el contenido binario una vez que se les han concedido permisos para acceder a los datos de deshacer binarios.

* **Min. validez**
( `cq.wcm.undo.validity`)

   * **Descripción**: Cantidad mínima de tiempo que se almacenan los datos de deshacer binarios, en horas. Después de este período de tiempo, los datos binarios están disponibles para su eliminación, para conservar espacio en disco.
   * **Predeterminado**: `10`
   * **Tipo**: `Integer`

* **Pasos**
( `cq.wcm.undo.steps`)

   * **Descripción**: Número máximo de acciones de página almacenadas en el historial de deshacer.
   * **Predeterminado**: `20`
   * **Tipo**: `Integer`

* **Persistencia**
( `cq.wcm.undo.persistence`)

   * **Descripción**: La clase que persiste en el historial de deshacer. Se proporcionan dos clases de persistencia:

      * `CQ.undo.persistence.WindowNamePersistence`: conserva el historial utilizando la propiedad window.name.
      * `CQ.undo.persistence.CookiePersistance`: conserva el historial utilizando cookies.

   * **Predeterminado**: `CQ.undo.persistence.WindowNamePersistence`
   * **Tipo**: `String`

* **Modo de persistencia**
( `cq.wcm.undo.persistence.mode`)

   * **Descripción**: Determina cuándo se mantiene el historial de deshacer. Seleccione esta opción para mantener el historial de deshacer después de cada edición de página. Desactive esta opción para que solo se mantenga cuando se vuelva a cargar una página (por ejemplo, cuando el usuario navegue a una página diferente).

     La persistencia del historial de deshacer utiliza recursos del explorador web. Si el explorador del usuario reacciona lentamente a las ediciones de página, intente mantener el historial de deshacer en las recargas de la página.

   * **Predeterminado**: `Selected`
   * **Tipo**: `Boolean`

* **Modo de marcador**
( `cq.wcm.undo.markermode`)

   * **Descripción**: especifica la señal visual que se utiliza para indicar qué párrafos se ven afectados cuando se produce una operación de deshacer o rehacer. Los siguientes valores son válidos:

      * flash: El indicador de selección de los párrafos parpadea temporalmente.
      * select: El párrafo está seleccionado.

   * **Predeterminado**: `flash`
   * **Tipo**: `String`

* **Componentes correctos**
( `cq.wcm.undo.whitelist`)

   * **Descripción**: Una lista de componentes que desea que se vean afectados por los comandos Deshacer y Rehacer. Añada rutas de componentes a esta lista cuando funcionen correctamente con Deshacer/Rehacer. Anexe un asterisco (&amp;ast;) para especificar un grupo de componentes:

      * El siguiente valor especifica el componente de texto de base:

        `foundation/components/text`

      * El siguiente valor especifica todos los componentes de base:

        `foundation/components/*`

   * Cuando se emiten acciones de deshacer o rehacer a un componente que no está en esta lista, aparece un mensaje que indica que el comando puede no ser fiable.

   * **Predeterminado** AEM : la propiedad se rellena con muchos componentes que proporciona el.
   * **Tipo**: `String[]`

* **Componentes incorrectos**
( `cq.wcm.undo.blacklist`)

   * **Descripción**: Una lista de componentes u operaciones de componentes que no desea que se vean afectadas por el comando Deshacer. Añada componentes y operaciones de componentes que no se comporten correctamente con el comando Deshacer:

      * Añada una ruta de componente cuando no desee ninguna de las operaciones del componente en el historial de deshacer, por ejemplo, `collab/forum/components/post`
      * Anexe dos puntos (:) y una operación a la ruta cuando desee que esa operación específica se omita del historial de deshacer (otras operaciones funcionan correctamente), por ejemplo, `collab/forum/components/post:insertParagraph.`

  >[!NOTE]
  >
  >Cuando una operación está en esta lista, se agrega al historial de deshacer. Los usuarios no pueden deshacer operaciones que existan antes de un **Componente incorrecto** operación en el historial de deshacer.

   * Los nombres de operación habituales son los siguientes:

      * `insertParagraph`: El componente se añade a la página.
      * `removeParagraph`: el componente se elimina.
      * `moveParagraph`: el párrafo se mueve a una ubicación diferente.
      * `updateParagraph`: las propiedades del párrafo se cambian.

   * **Predeterminado**: la propiedad se rellena con varias operaciones de componente.
   * **Tipo**: `String[]`
