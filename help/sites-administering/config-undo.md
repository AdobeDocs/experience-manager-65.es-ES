---
title: Configuración de Deshacer para edición de página
seo-title: Configuración de Deshacer para edición de página
description: Obtenga información sobre cómo configurar la compatibilidad con Deshacer para la edición de páginas en AEM.
seo-description: Obtenga información sobre cómo configurar la compatibilidad con Deshacer para la edición de páginas en AEM.
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de Deshacer para edición de página{#configuring-undo-for-page-editing}

El servicio [](/help/sites-deploying/configuring-osgi.md) OSGi **Day CQ WCM Undo Configuration** ( `com.day.cq.wcm.undo.UndoConfigService`) expone varias propiedades que controlan el comportamiento de los comandos deshacer y rehacer para editar páginas.

## Configuración predeterminada {#default-configuration}

En una instalación estándar, la configuración predeterminada se define como propiedades en el `sling:OsgiConfig`nodo:

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

Este nodo contiene `cq.wcm.undo.whitelist` y `cq.wcm.undo.blacklist` propiedades; para las demás propiedades se toman los valores predeterminados.

>[!CAUTION]
>
>No ***debe*** cambiar nada en la `/libs` ruta.
>
>Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de funciones).

## Configuración de Deshacer y Rehacer {#configuring-undo-and-redo}

Puede configurar estas propiedades del servicio OSGi para su propia instancia.

>[!NOTE]
>
>When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

A continuación se enumeran las propiedades que se muestran en la consola web, seguidas del nombre del parámetro OSGi correspondiente, junto con una descripción y el valor predeterminado (si procede):

* **Enable**( `cq.wcm.undo.enabled`)

   * **Descripción**: Determina si los autores de la página pueden deshacer y rehacer cambios.
   * **Predeterminado**: `Selected`
   * **Tipo**: `Boolean`

* **Ruta**
( `cq.wcm.undo.path`)

   * **Descripción**: Ruta del repositorio para datos de deshacer binarios persistentes. Cuando los autores cambian datos binarios como imágenes, la versión original de los datos se mantiene aquí. Cuando se deshacen los cambios en los datos binarios, estos datos de deshacer binarios se restauran en la página.
   * **Predeterminado**: `/var/undo`
   * **Tipo**: `String`
   >[!NOTE]
   >
   >De forma predeterminada, solo los administradores pueden acceder al `/var/undo` nodo. Los autores pueden realizar operaciones de deshacer y rehacer en contenido binario únicamente después de que se les hayan concedido permisos para acceder a los datos de deshacer binarios.

* **Mínimo. valid**( `cq.wcm.undo.validity`)

   * **Descripción**: Cantidad mínima de tiempo que se almacenan los datos de deshacer binarios, en horas. Después de este período de tiempo, los datos binarios se pueden eliminar para conservar espacio en disco.
   * **Predeterminado**: `10`
   * **Tipo**: `Integer`

* **Pasos**( `cq.wcm.undo.steps`)

   * **Descripción**: Número máximo de acciones de página almacenadas en el historial de deshacer.
   * **Predeterminado**: `20`
   * **Tipo**: `Integer`

* **Persistencia**( `cq.wcm.undo.persistence`)

   * **Descripción**: La clase que persiste en el historial de deshacer. Se proporcionan dos clases de persistencia:

      * `CQ.undo.persistence.WindowNamePersistence`:: Persiste el historial mediante la propiedad window.name.
      * `CQ.undo.persistence.CookiePersistance`:: Persiste el historial mediante cookies.
   * **Predeterminado**: `CQ.undo.persistence.WindowNamePersistence`
   * **Tipo**: `String`


* **Modo** de persistencia( `cq.wcm.undo.persistence.mode`)

   * **Descripción**: Determina cuándo se mantiene el historial de deshacer. Seleccione esta opción para conservar el historial de deshacer después de cada edición de página. Borre esta opción para que solo se mantenga cuando se vuelva a cargar una página (por ejemplo, el usuario se desplaza a otra página).

      El historial de deshacer persistente utiliza recursos del explorador Web. Si el explorador de los usuarios reacciona lentamente a las ediciones de página, intente mantener el historial de deshacer en las recargas de página.

   * **Predeterminado**: `Selected`
   * **Tipo**: `Boolean`

* **Modo** Marcador( `cq.wcm.undo.markermode`)

   * **Descripción**: Especifica la señal visual que se utilizará para indicar qué párrafos se ven afectados cuando se produce una acción de deshacer o rehacer. Los siguientes valores son válidos:

      * flash: El indicador de selección de los párrafos parpadea temporalmente.
      * seleccionar: El párrafo está seleccionado.
   * **Predeterminado**: `flash`
   * **Tipo**: `String`


* **Buenos componentes**( `cq.wcm.undo.whitelist`)

   * **Descripción**: Lista de componentes que desea que se vean afectados por los comandos deshacer y rehacer. Agregue rutas de componentes a esta lista cuando funcionen correctamente con deshacer/rehacer. Añada un asterisco (&amp;ast;) para especificar un grupo de componentes:

      * El siguiente valor especifica el componente de texto de base:

         `foundation/components/text`

      * El siguiente valor especifica todos los componentes de base:

         `foundation/components/*`
   * Cuando se realiza la acción de deshacer o rehacer en un componente que no está en esta lista, aparece un mensaje que indica que el comando puede no ser fiable.

   * **Predeterminado**: La propiedad se rellena con muchos componentes que proporciona AEM.
   * **Tipo**: `String[]`


* **Componentes** malos( `cq.wcm.undo.blacklist`)

   * **Descripción**: Lista de componentes y/o operaciones de componentes que no desea que se vean afectados por el comando Deshacer. Agregue componentes y operaciones de componentes que no se comportan correctamente con el comando Deshacer:

      * Agregue una ruta de componente cuando no desee ninguna de las operaciones del componente en el historial de deshacer, por ejemplo `collab/forum/components/post`
      * Anexe dos puntos (:) y una operación a la ruta cuando desee que esa operación específica se omita del historial de deshacer (otras funciones de operaciones funcionan correctamente), por ejemplo `collab/forum/components/post:insertParagraph.`
   >[!NOTE]
   >
   >Cuando una operación está en esta lista, se sigue agregando al historial de deshacer. Los usuarios no pueden deshacer operaciones que existan antes de una operación Componente **** incorrecto en el historial de deshacer.

   * Los nombres de operación habituales son los siguientes:

      * `insertParagraph`:: El componente se agrega a la página.
      * `removeParagraph`:: El componente se elimina.
      * `moveParagraph`:: El párrafo se mueve a una ubicación diferente.
      * `updateParagraph`:: Se cambian las propiedades de párrafo.
   * **Predeterminado**: La propiedad se rellena con varias operaciones de componentes.
   * **Tipo**: `String[]`




