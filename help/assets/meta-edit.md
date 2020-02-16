---
title: Cómo editar o agregar metadatos
description: Obtenga información sobre los metadatos de los recursos en Recursos AEM y las distintas formas de editar los metadatos de los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Cómo editar o agregar metadatos {#how-to-edit-or-add-metadata}

Los metadatos son información adicional sobre el recurso que se puede buscar. Se extrae automáticamente al cargar una imagen. Puede editar los metadatos existentes o agregar nuevas propiedades de metadatos a los campos existentes (por ejemplo, cuando un campo de metadatos está en blanco).

Dado que las empresas necesitan vocabularios de metadatos fiables y controlados, AEM Assets no permite la adición ad-hoc de nuevas propiedades de metadatos. Aunque los autores no pueden agregar campos de metadatos nuevos para los recursos, los desarrolladores sí pueden hacerlo. Consulte [Creación de una nueva propiedad de metadatos para los recursos](meta-edit.md#editing-metadata-schema).

## Editar metadatos de un recurso {#editing-metadata-for-an-asset}

Para editar metadatos:

1. Realice una de las acciones siguientes:

   * En la interfaz de usuario de Recursos, seleccione el recurso y toque o haga clic en el icono **[!UICONTROL Ver propiedades]** de la barra de herramientas.
   * En la miniatura del recurso, seleccione la acción rápida **[!UICONTROL Ver propiedades]** .
   * En la página de recursos, toque o haga clic en el icono **[!UICONTROL Ver propiedades]** de la barra de herramientas.
      ![chlimage_1-168](assets/chlimage_1-168.png)
   La página de recursos muestra todos los metadatos del recurso. Estos metadatos se extrajeron automáticamente al cargarse (ingeridos) en Recursos AEM.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. Realice ediciones en los metadatos de las distintas fichas, según sea necesario, y cuando termine, toque o haga clic en **[!UICONTROL Guardar]** en la barra de herramientas para guardar los cambios. Toque o haga clic en **[!UICONTROL Cerrar]** para volver a la interfaz web de Recursos.

   >[!NOTE]
   >
   >Si un campo de texto está vacío, no hay ningún conjunto de metadatos existente. Puede introducir un valor en el campo y guardarlo para agregar esa propiedad de metadatos.

Cualquier cambio en los metadatos de un recurso se vuelve a escribir en el binario original como parte de sus datos XMP. Esto se realiza mediante el flujo de trabajo de reescritura de metadatos de AEM. Los cambios realizados en las propiedades existentes (como `dc:title`) se sobrescriben y las propiedades creadas recientemente (incluidas las propiedades personalizadas como `cq:tags`) se agregan junto con el esquema.

Se admite y activa la escritura de XMP en las plataformas y formatos de archivo descritos en los requisitos [técnicos.](/help/sites-deploying/technical-requirements.md)

## Editar esquema de metadatos {#editing-metadata-schema}

Para obtener más información sobre cómo editar el esquema de metadatos, consulte [Edición de formularios](metadata-schemas.md#edit-metadata-schema-forms)de esquema de metadatos.

## Registro de un espacio de nombres personalizado en AEM {#registering-a-custom-namespace-within-aem}

Puede añadir sus propios espacios de nombres en AEM. Al igual que hay espacios de nombres predefinidos como cq, jcr y sling, puede tener un espacio de nombres para los metadatos del repositorio y el procesamiento de XML.

1. Vaya a la página de administración del tipo de nodo `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Toque o haga clic en **[!UICONTROL Espacios]** de nombres en la parte superior de la página. La página de administración del espacio de nombres se muestra en una ventana.

1. Para agregar un espacio de nombres, toque o haga clic en **[!UICONTROL Nuevo]** en la parte inferior.
1. Especifique un espacio de nombres personalizado en la convención de espacio de nombres XML (especifique el identificador en forma de URI y un prefijo asociado para el identificador) y toque o haga clic en **[!UICONTROL Guardar]**.
