---
title: Publicación y cancelación de la publicación de formularios y documentos
seo-title: Publicación y cancelación de la publicación de formularios y documentos
description: Puede programar la publicación y cancelación de la publicación de formularios. Los formularios publicados se replican en la instancia de publicación.
seo-description: Puede programar la publicación y cancelación de la publicación de formularios. Los formularios publicados se replican en la instancia de publicación.
uuid: 0bad5608-b7a8-4599-81cc-2cd0a3dc7dd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# Publicación y cancelación de la publicación de formularios y documentos{#publishing-and-unpublishing-forms-and-documents}

AEM Forms permite crear, publicar y cancelar la publicación de formularios fácilmente. Para obtener más información sobre AEM Forms, consulte [Introducción a la administración de formularios](../../forms/using/introduction-managing-forms.md).

El servidor de AEM Forms proporciona dos instancias: Autor y publicación. La instancia de autor sirve para crear y administrar recursos y recursos de formulario. La instancia de publicación sirve para mantener los recursos y recursos relacionados disponibles para los usuarios finales. Puede importar XDP y PDF forms en el modo Autor. Para obtener más información, consulte [Obtención de documentos XDP y PDF en AEM Forms](../../forms/using/get-xdp-pdf-documents-aem.md).

## Recursos admitidos   {#supported-assets-nbsp}

AEM Forms admite los siguientes tipos de recursos:

* Formularios adaptables
* Documentos adaptables
* Fragmentos de formulario adaptables
* Temas
* Plantillas de formulario (formularios XFA)
* PDF forms
* Documento (documentos PDF planos)
* Conjuntos de formularios
* Recurso (imágenes, Esquemas y hojas de estilo)

Inicialmente, todos los recursos solo están disponibles en la instancia Autor. Un administrador o un autor de formulario puede publicar todos los recursos excepto los recursos.

Al seleccionar un formulario y publicarlo, también se publican sus recursos y recursos relacionados. Sin embargo, los recursos dependientes no se publican. En este contexto, los recursos y recursos relacionados son recursos que un recurso publicado utiliza o a los que hace referencia. Los recursos dependientes son recursos que hacen referencia a un recurso publicado.

Su Forms adaptable puede utilizar algunas configuraciones, configuraciones y personalizaciones que no se publican automáticamente. Se recomienda publicar o activar estos recursos antes de publicar un formulario adaptable.

* Plantillas de formulario adaptable editables
* Configuraciones de Cloud Service para Adobe Sign, Typekit, reCAPTCHA y modelos de datos de formulario
* Otras configuraciones de servicios de Cloud solo se activan si el usuario tiene permisos de administrador.
* Personalizaciones. Entre ellos se incluyen, entre otros:

   * Diseños personalizados
   * Aspectos personalizados
   * Archivo CSS: tomado como entrada en el cuadro de diálogo de propiedades del contenedor de formulario adaptable
   * Categoría de la biblioteca de clientes: se toma como entrada en el cuadro de diálogo de propiedades del contenedor de formularios adaptables
   * Cualquier otra biblioteca de cliente que se pueda incluir como parte de una plantilla de formulario adaptable.
   * Rutas de diseño

## Estados de recursos {#asset-states}

Un recurso puede tener los siguientes estados:

* **Sin publicar:** recurso que nunca se ha publicado (el estado sin publicar solo se aplica a los recursos de Forms). Los recursos de Correspondence Management no tienen un estado No publicado).
* **Publicado**: Recurso que se ha publicado y está disponible en la instancia de publicación
* **Modificado**: Recurso que se modifica después de publicarse

## Publicar un recurso {#publish-an-asset}

1. Inicie sesión en el servidor de AEM Forms.
1. Utilice una de las siguientes opciones para seleccionar y publicar un recurso.

   1. Mueva el puntero sobre un recurso y toque **[!UICONTROL Publicar]** ![aem6forms_world](assets/aem6forms_globe.pngasset.png).
   1. Siga uno de estos procedimientos y toque Publicar:

      * Si está en la vista de tarjeta, toque **[!UICONTROL Ingrese la selección]** ![aem6forms_check-círculo](assets/aem6forms_check-circle.png) y toque el recurso. El recurso está seleccionado.
      * Si se encuentra en la vista de lista, seleccione la casilla de verificación de un recurso. El recurso está seleccionado.
      * Toque un recurso para mostrar sus detalles.
      * Muestre las propiedades de un recurso tocando Propiedades de Vista ![viewproperties](assets/viewproperties.png).

      >[!NOTE]
      >
      >No seleccione varios recursos. No se puede publicar varios recursos a la vez.


1. Cuando el proceso de publicación se inicio, aparece un cuadro de diálogo de confirmación con todos los recursos y recursos relacionados. En el cuadro de diálogo que contiene recursos relacionados, toque **[!UICONTROL Publicar]**. El recurso se publica y aparece el cuadro de diálogo de éxito Publicar recursos.

   >[!NOTE]
   >
   >Para los formularios adaptables, junto con los recursos relacionados, también se muestra el nombre de la página Formulario adaptable.

   ![Cuadro de diálogo de confirmación con todos los recursos y recursos relacionados](assets/p4.png)

   Cuadro de diálogo de confirmación con todos los recursos y recursos relacionados.

   >[!NOTE]
   >
   >En Forms Manager, si el usuario no tiene permiso para publicar los recursos enumerados, la acción Publicar está desactivada. Un recurso que requiere permisos adicionales se muestra en rojo.

   Después de publicar un recurso, las propiedades de metadatos del recurso se copian en la instancia de publicación y el estado del recurso se cambia a Publicado. El estado de los recursos dependientes que se publican también se cambia a Publicado.

   Después de publicar un recurso, puede utilizar Forms Portal para mostrar todos los recursos de una página web. Para obtener más información, consulte [Introducción a la publicación de formularios en un portal](../../forms/using/introduction-publishing-forms.md).

## Publicar todos los recursos de administración de correspondencia {#publish-all-the-correspondence-management-assets}

AEM Forms permite publicar todos los recursos de la Administración de correspondencia en un servidor de una sola vez. Los recursos publicados incluyen todos los recursos de Correspondence Management y las dependencias relacionadas.

Complete los siguientes pasos para publicar todos los recursos de la administración de correspondencia en un servidor:

1. Inicie sesión en el servidor de AEM Forms.
1. Toque **Adobe Experience Manager** en la barra de navegación global.
1. Toque ![herramientas](assets/tools.png) y luego toque **Forms**.
1. Toque **Publicar recursos de administración de correspondencia**.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   Aparece la página Publicar todos los recursos de gestión de correspondencia y muestra la información sobre la última vez que se intentó el proceso de Publicar recursos de gestión de correspondencia.

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. Toque **Publicar** y, en el mensaje de confirmación, toque **Aceptar**.

   Una vez completado el proceso por lotes, puede realizar la vista de los detalles de la última ejecución. Esto incluye información como el inicio de sesión del administrador y si el lote se ejecutó correctamente o falló.

   >[!NOTE]
   >
   >El proceso de publicación no se puede cancelar una vez iniciado. Además, mientras la operación de publicación está en curso, no cree, elimine, modifique ni publique ningún recurso ni inicie la operación Exportar todos los recursos de gestión de correspondencia.

## Automatizar la publicación y cancelación de publicaciones para Forms y Documentos {#automate-publishing-and-unpublishing-for-forms-amp-documents}

AEM Forms permite programar la publicación y cancelación de publicaciones de recursos para Forms y Documentos. Puede especificar la programación en el Editor de metadatos. Para obtener más información sobre la administración de metadatos de formulario, consulte [Administración de metadatos de formulario.](../../forms/using/manage-form-metadata.md)

Siga estos pasos para programar la fecha y hora de publicación y cancelación de la publicación de recursos de Forms y Documentos:

1. Seleccione un recurso y toque **[!UICONTROL Propiedades de Vista]**. Se abre la página Propiedades de metadatos.
1. En la página Propiedades de metadatos, toque **[!UICONTROL Avanzado]** y, a continuación, toque **[!UICONTROL Editar]** ![illustratorcc_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png).
1. En los campos **[!UICONTROL Publicar a tiempo]** y **[!UICONTROL Tiempo de inactividad de publicación]**, seleccione la fecha y la hora.\
   Toque **[!UICONTROL Listo]** ![aem6forms_check](assets/aem6forms_check.png).

## Cancelar la publicación de un recurso {#unpublish-an-asset}

1. Seleccione un recurso que se publique y toque **[!UICONTROL Cancelar publicación]** ![Cancelar publicación](assets/unpublish.png).
1. Utilice una de las siguientes opciones para seleccionar y cancelar la publicación de un recurso.

   1. Mueva el puntero sobre un recurso y toque **[!UICONTROL Cancelar publicación]** ![cancelar publicación](assets/unpublish.png).
   1. Siga uno de estos procedimientos y toque Cancelar publicación:

      * Si está en la vista de tarjeta, toque **[!UICONTROL Ingrese la selección]** ![aem6forms_check-círculo](assets/aem6forms_check-circle.png) y toque el recurso. El recurso está seleccionado.

      * Si está en la vista de lista, pase el ratón sobre un recurso y toque ![selectassetmark](assets/selectassetcheckmark.png). El recurso está seleccionado.

      * Toque un recurso para mostrar sus detalles.
      * Muestre las propiedades de un recurso tocando Propiedades de Vista ![viewproperties](assets/viewproperties.png).

1. Cuando se produce la inicio del proceso de cancelación de la publicación, aparece un cuadro de diálogo de confirmación. Toque **[!UICONTROL Cancelar la publicación]**.

   >[!NOTE]
   >
   >Solo se cancelará la publicación del recurso seleccionado y no se cancelarán la publicación de sus recursos secundarios y referenciados, si los hubiera.

## Revertir un recurso o una carta a la versión publicada anteriormente {#revert-an-asset-or-letter-to-the-previously-published-version}

Cada vez que publica un recurso o una carta después de editarlo, se crea una versión del recurso o la carta. Puede revertir un recurso o una carta a una versión publicada anteriormente. Es posible que deba hacerlo si algo sale mal con la versión actual del recurso o documento.

>[!NOTE]
>
>No devuelva una carta a un estado publicado por última vez si se elimina del sistema cualquier recurso dependiente utilizado en esa carta publicada.

1. Seleccione un recurso y toque **[!UICONTROL Revertir a la versión previamente publicada]** ![reverttopreviouslypublishedversion](assets/reverttopreviouslypublishedversion.png).
1. Antes de revertir el recurso, aparece un cuadro de diálogo de confirmación. Puntee **[!UICONTROL Revertir]**.

   El recurso o la carta se revertirán a su versión publicada anteriormente.

## Eliminar un recurso {#delete-an-asset}

>[!NOTE]
>
>Al eliminar un recurso, éste se elimina de la instancia de publicación. Al eliminar un recurso también se elimina su historial de versiones, excepto la versión base.

1. Seleccione un recurso y toque **[!UICONTROL Eliminar]** ![eliminar](assets/delete.png).

   >[!NOTE]
   >
   >La opción Eliminar también está disponible cuando se muestran los detalles del recurso tocando un recurso o las propiedades de un recurso tocando Propiedades de Vista ![viewproperties](assets/viewproperties.png).

1. Antes de eliminar el recurso, aparece un cuadro de diálogo de confirmación. Toque **[!UICONTROL Eliminar]**.

   >[!NOTE]
   >
   >Solo se elimina el recurso seleccionado y los recursos dependientes y no se eliminan. Para comprobar las referencias de un recurso, toque ![referencias](assets/references.png) y, a continuación, seleccione un recurso.
   >
   >
   >Si el recurso que intenta eliminar es un recurso secundario de otro recurso, no se elimina. Para eliminar un recurso de este tipo, elimine las referencias de este recurso de otros recursos y vuelva a intentarlo.

## Formularios adaptables protegidos {#protected-adaptive-forms}

Puede habilitar la autenticación para los formularios a los que desee que accedan los usuarios seleccionados. Cuando se habilita la autenticación para los formularios, los usuarios ven una pantalla de inicio de sesión antes de acceder a ellos. Solo los usuarios con credenciales autorizadas pueden acceder a los formularios.

Para habilitar la autenticación en los formularios:

1. En el navegador, abra configMgr en la instancia de publicación.\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. En la Configuración de la consola web de Adobe Experience Manager, haga clic en **Servicio de autenticación Sling de Apache** para configurarlo.
1. En el cuadro de diálogo Servicio de autenticación Apache Sling que aparece, utilice el botón **+** para agregar rutas.\
   Cuando se agrega una ruta, el servicio de autenticación se activa para los formularios de esa ruta.
