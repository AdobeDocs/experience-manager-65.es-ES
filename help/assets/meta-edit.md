---
title: Cómo editar o agregar metadatos
description: Obtenga información sobre los metadatos de los recursos [!DNL Adobe Experience Manager Assets] de diversas formas para editar los metadatos de los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 4748eed3ce484e8446b641ccbc7b5d76cb66f428
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 2%

---


# Cómo editar o agregar metadatos {#how-to-edit-or-add-metadata}

Los metadatos son información adicional sobre el recurso que se puede buscar. Se extrae automáticamente al cargar una imagen. Puede editar los metadatos existentes o agregar nuevas propiedades de metadatos al campo existente, por ejemplo, cuando un campo de metadatos está en blanco.

Las organizaciones necesitan vocabularios de metadatos fiables y controlados. Por lo tanto, [!DNL Experience Manager Assets] no permite la adición a petición de nuevas propiedades de metadatos. Los desarrolladores y no los autores pueden agregar nuevos campos de metadatos para los recursos. Consulte [Creación de propiedades de metadatos para recursos](meta-edit.md#editing-metadata-schema).

## Editar metadatos de un recurso {#editing-metadata-for-an-asset}

Para editar metadatos, siga estos pasos:

1. Realice una de las acciones siguientes:

   * En la [!DNL Assets] interfaz, seleccione el recurso y haga clic en Propiedades **[!UICONTROL de la]** Vista en la barra de herramientas.
   * En la miniatura del recurso, seleccione la acción rápida Propiedades de la **[!UICONTROL Vista]** .
   * En la página de recursos, haga clic en el icono **[!UICONTROL de información Propiedades]** de ![Vista de](assets/do-not-localize/info-circle-icon.png) recursos de la barra de herramientas.

   La página de recursos muestra todos los metadatos del recurso. Los metadatos se extraen cuando se carga el recurso (se ingesta) en [!DNL Experience Manager].

   ![Seleccionar propiedades de un recurso para vista de sus metadatos](assets/asset-metadata.png)

   *Figura: Edite o agregue metadatos en la página[!UICONTROL Propiedades]del recurso.*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the [!DNL Assets] web interface.

   >[!NOTE]
   >
   >Si un campo de texto está vacío, no hay ningún conjunto de metadatos existente. Puede introducir un valor en el campo y guardarlo para agregar esa propiedad de metadatos.

Cualquier cambio en los metadatos de un recurso se vuelve a escribir en el binario original como parte de sus datos XMP. El flujo de trabajo de escritura de metadatos agrega los metadatos al binario original. Los cambios realizados en las propiedades existentes (como `dc:title`) se sobrescriben y las propiedades nuevas (incluidas las propiedades personalizadas como `cq:tags`) se agregan con el esquema.

Se admite y activa la escritura de XMP en las plataformas y formatos de archivo descritos en los requisitos [técnicos.](/help/sites-deploying/technical-requirements.md)

## Editar esquema de metadatos {#editing-metadata-schema}

Para obtener más información, consulte [Edición de formularios](metadata-schemas.md#edit-metadata-schema-forms)de esquema de metadatos.

## Registrar una Área de nombres personalizada en [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Puede agregar sus propias Áreas de nombres dentro de [!DNL Experience Manager]. Al igual que hay Áreas de nombres predefinidas como `cq`, `jcr`, y `sling`, puede tener una Área de nombres para los metadatos del repositorio y el procesamiento de XML.

1. Acceda a la página de administración del tipo de nodo `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Para acceder a la página Administración de Áreas de nombres, haga clic en **[!UICONTROL Áreas de nombres]** en la parte superior de la página.
1. Para agregar una Área de nombres, haga clic en **[!UICONTROL Nuevo]** en la parte inferior de la página.
1. Especifique una Área de nombres personalizada en la convención de Área de nombres XML. Especifique el ID en forma de URI y un prefijo asociado para el ID. Haga clic en **[!UICONTROL Guardar]**.

>[!MORELIKETHIS]
>
>* [Acerca de los metadatos y sus necesidades en Recursos](metadata.md)
>* [Metadatos XMP](xmp.md)
>* [Referencia de esquemas de metadatos](meta-ref.md)

