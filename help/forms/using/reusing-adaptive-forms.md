---
title: Reutilización de formularios adaptables
seo-title: Reusing adaptive forms
description: Puede reutilizar un formulario adaptable existente para crear nuevos formularios adaptables.
seo-description: You can reuse an existing adaptive form to create new adaptive forms.
uuid: f1d0fb70-e255-4dd9-8e6d-fd65eaf2e81a
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
feature: Adaptive Forms
exl-id: d8ee4e82-3137-430e-aa47-b00191f2729c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 33%

---

# Reutilización de formularios adaptables {#reusing-adaptive-forms}

## Introducción {#introduction}

Si desea utilizar algunas de las propiedades de un formulario adaptable existente para generar uno nuevo, simplemente puede utilizar la funcionalidad copiar y pegar. Además, puede pegar el nuevo formulario adaptable en la ruta de carpeta deseada. Todas las propiedades de metadatos se replican y también se copian los XFA y XSD para formularios adaptables basados en XFA y XSD.

>[!NOTE]
>
>El estado y los detalles de la revisión no se copian. Por ejemplo, si el formulario adaptable se publica y, a continuación, si lo copia, el formulario adaptable pegado se encuentra en estado no publicado. Del mismo modo, si un recurso copiado está en revisión, el recurso pegado no estará incluido en la misma revisión.

### Copiar un formulario adaptable {#copy-an-adaptive-form}

Copie un formulario adaptable mediante cualquiera de los siguientes métodos:

1. Haga clic en el icono Copiar ![aem6forms_copy](assets/aem6forms_copy.png) en Acciones rápidas.

   >[!NOTE]
   >
   >Las acciones rápidas son los elementos de acción que se muestran sobre una miniatura al pasar el ratón por encima.

1. Seleccione el formulario adaptable. El proceso de selección es diferente para cada vista.

   Si está en la vista de tarjeta, vaya al modo de selección haciendo clic en la selección ![aem6forms_check-círculo](assets/aem6forms_check-circle.png) y haga clic en todos los formularios adaptables que desee copiar.

   Si está en la vista de lista, haga clic en las casillas de verificación de todos los formularios adaptables para seleccionarlos.

   >[!NOTE]
   >
   >Todos los recursos seleccionados deben ser formularios adaptables, ya que la funcionalidad de copiar y pegar solo se admite en formularios adaptables, y todos los recursos seleccionados deben estar presentes en la misma carpeta.

   Después de seleccionar los recursos, haga clic en la copia ![aem6forms_copy](assets/aem6forms_copy.png) presente en la barra de herramientas para copiar el formulario adaptable seleccionado.

### Pegar un formulario adaptable {#paste-an-adaptive-form}

Al hacer clic en la acción copiar , se sale automáticamente del modo de selección y se pega ![aem6forms_pegar](assets/aem6forms_paste.png) icono visible. A continuación, vaya a la ruta de carpeta deseada y haga clic en pegar . ![aem6forms_pegar](assets/aem6forms_paste.png) para pegar el formulario adaptable copiado.

Si está pegando el formulario en la misma carpeta o existe otro archivo con el mismo nombre de nodo (con el que está almacenado en el repositorio CRX) en la carpeta de destino, se añade un 1 al sufijo (por ejemplo, myaf se convierte en myaf1, y si ya existe myaf1 en la misma ubicación, se convierte en myaf2). Todas las demás propiedades siguen siendo las mismas que la forma adaptativa original.

Después de hacer clic en el botón pegar ![aem6forms_pegar](assets/aem6forms_paste.png) , se volverá a ocultar. Solo puede utilizar la opción Pegar una vez simultáneamente. Para volver a crear una copia del mismo recurso, cópielo de nuevo.

### Cambiar el contenido de un nuevo formulario adaptable {#change-contents-of-new-adaptive-form}

El contenido de los formularios adaptables pegados se puede cambiar utilizando los siguientes métodos para distinguirlo del formulario copiado:

1. **Cambiar las propiedades de los metadatos:**

   Puede cambiar las propiedades de metadatos del formulario adaptable, por ejemplo, el título y la descripción. Para obtener más información sobre las propiedades de los metadatos y cómo se pueden cambiar, consulte [Administración de metadatos de formulario](/help/forms/using/manage-form-metadata.md).

1. **Cambiar el XFA/XSD de los formularios adaptables basados en XFA/XSD:**

   Puede cambiar el XFA/XSD utilizado en los formularios adaptables. Para saber cómo se pueden cambiar estos formularios adaptables, consulte [Administración de metadatos de formulario](/help/forms/using/manage-form-metadata.md)

1. **Volver a publicar el formulario:**

   El recurso pegado es diferente del copiado. Puede publicarlo como un nuevo recurso para que esté disponible para los usuarios finales. Para saber cómo publicar un recurso, consulte [Publicación y cancelación de la publicación de formularios](/help/forms/using/publishing-unpublishing-forms.md)
