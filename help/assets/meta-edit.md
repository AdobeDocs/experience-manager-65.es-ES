---
title: Cómo editar o agregar metadatos
description: Obtenga información sobre los metadatos de los recursos en [!DNL Adobe Experience Manager Assets] y sobre varias formas de editar los metadatos de los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Cómo editar o agregar metadatos {#how-to-edit-or-add-metadata}

Los metadatos son información adicional sobre el recurso que se puede buscar. Se extrae automáticamente al cargar una imagen. Puede editar los metadatos existentes o agregar nuevas propiedades de metadatos a los campos existentes (por ejemplo, cuando un campo de metadatos está en blanco).

Debido a que las organizaciones necesitan vocabularios de metadatos fiables y controlados, [!DNL Experience Manager Assets] no permite la adición ad-hoc de nuevas propiedades de metadatos. Aunque los autores no pueden agregar campos de metadatos nuevos para los recursos, los desarrolladores sí pueden hacerlo. Consulte [Creación de una nueva propiedad de metadatos para los recursos](meta-edit.md#editing-metadata-schema).

## Editar metadatos de un recurso {#editing-metadata-for-an-asset}

Para editar metadatos:

1. Realice una de las acciones siguientes:

   * En la [!DNL Assets] interfaz, seleccione el recurso y haga clic en Propiedades **[!UICONTROL de la]** Vista en la barra de herramientas.
   * En la miniatura del recurso, seleccione la acción rápida Propiedades de la **[!UICONTROL Vista]** .
   * En la página de recursos, haga clic en Propiedades de **[!UICONTROL Vista]** ![chlimage_1-168](assets/chlimage_1-168.png) en la barra de herramientas.
   La página de recursos muestra todos los metadatos del recurso. Los metadatos se extraen cuando el recurso se carga (se ingesta) en Experience Manager.

   ![seleccione Propiedades del recurso para los metadatos de vista](assets/asset-metadata.png)

   *Figura: Edite o agregue metadatos en la página Propiedades del recurso.*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the Assets web interface.

   >[!NOTE]
   >
   >Si un campo de texto está vacío, no hay ningún conjunto de metadatos existente. Puede introducir un valor en el campo y guardarlo para agregar esa propiedad de metadatos.

Cualquier cambio en los metadatos de un recurso se vuelve a escribir en el binario original como parte de sus datos XMP. Esto se realiza mediante el flujo de trabajo de escritura de metadatos de Experience Manager. Los cambios realizados en las propiedades existentes (como `dc:title`) se sobrescriben y las propiedades creadas recientemente (incluidas las propiedades personalizadas como `cq:tags`) se agregan junto con el esquema.

Se admite y activa la escritura de XMP en las plataformas y formatos de archivo descritos en los requisitos [técnicos.](/help/sites-deploying/technical-requirements.md)

## Editar esquema de metadatos {#editing-metadata-schema}

Para obtener más información sobre cómo editar el esquema de metadatos, consulte [Editar formularios](metadata-schemas.md#edit-metadata-schema-forms)de esquema de metadatos.

## Registro de una Área de nombres personalizada en Experience Manager {#registering-a-custom-namespace-within-aem}

Puede agregar sus propias Áreas de nombres dentro de Experience Manager. Al igual que hay Áreas de nombres predefinidas como cq, jcr y sling, puede tener una Área de nombres para los metadatos del repositorio y el procesamiento de XML.

1. Vaya a la página de administración del tipo de nodo `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Haga clic en **[!UICONTROL Áreas de nombres]** en la parte superior de la página. La página Administración de Áreas de nombres se muestra en una ventana.

1. Para agregar una Área de nombres, haga clic en **[!UICONTROL Nuevo]** en la parte inferior.
1. Especifique una Área de nombres personalizada en la convención de Área de nombres XML (especifique el identificador en forma de URI y un prefijo asociado para el identificador) y haga clic en **[!UICONTROL Guardar]**.
