---
title: Reutilización de formularios adaptables
seo-title: Reutilización de formularios adaptables
description: Puede reutilizar un formulario adaptable existente para crear nuevos formularios adaptables.
seo-description: Puede reutilizar un formulario adaptable existente para crear nuevos formularios adaptables.
uuid: f1d0fb70-e255-4dd9-8e6d-fd65eaf2e81a
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---


# Reutilización de formularios adaptables {#reusing-adaptive-forms}

## Introducción {#introduction}

Si desea utilizar algunas de las propiedades de un formulario adaptable existente para generar uno nuevo, simplemente puede utilizar la funcionalidad copiar y pegar. Además, puede pegar el nuevo formulario adaptable en la ruta de carpeta deseada. Todas las propiedades de metadatos se replican y también se copian los XFA y XSD para formularios adaptables basados en XFA y XSD.

>[!NOTE]
>
>El estado y los detalles de la revisión no se copian. Por ejemplo, si el formulario adaptable se publica y, a continuación, si lo copia, el formulario adaptable pegado se encuentra en estado no publicado. Del mismo modo, si un recurso copiado está en revisión, el activo pegado no se encuentra en la misma revisión.

### Copiar un formulario adaptable {#copy-an-adaptive-form}

Copie un formulario adaptable mediante cualquiera de los siguientes métodos:

1. Haga clic en el icono Copiar ![aem6forms_copy](assets/aem6forms_copy.png) de Acciones rápidas.

   >[!NOTE]
   >
   >Las acciones rápidas son los elementos de acción que se muestran sobre una miniatura al pasar el ratón por encima.

1. Seleccione el formulario adaptable. El proceso de selección es diferente para las diferentes vistas.

   Si está en la vista de tarjeta, vaya al modo de selección haciendo clic en el icono de selección ![aem6forms_check-círculo](assets/aem6forms_check-circle.png) y haga clic en todos los formularios adaptables que desee copiar.

   Si está en la vista de lista, haga clic en las casillas de verificación de todos los formularios adaptables para seleccionarlos.

   >[!NOTE]
   >
   >Todos los recursos seleccionados deben ser formularios adaptables, ya que la funcionalidad de copiar y pegar solo se admite en formularios adaptables, y todos los recursos seleccionados deben estar presentes en la misma carpeta.

   Después de seleccionar los recursos, haga clic en el icono Copiar ![aem6forms_copy](assets/aem6forms_copy.png) que se encuentra en la barra de herramientas para copiar el formulario adaptable seleccionado.

### Pegar un formulario adaptable {#paste-an-adaptive-form}

Al hacer clic en la acción de copia, se sale automáticamente del modo de selección y el icono pegar ![aem6forms_pegar](assets/aem6forms_paste.png) queda visible. A continuación, vaya a la ruta de carpeta deseada y haga clic en el icono ![aem6forms_pasta](assets/aem6forms_paste.png) para pegar el formulario adaptable copiado.

Si está pegando en la misma carpeta o en otro archivo con el mismo nombre de nodo (con el que está almacenado en el repositorio CRX) existe en esta carpeta de destino, se añade 1 al sufijo (por ejemplo, myaf se convierte en myaf1 y si myaf1 existe en la misma ubicación, myaf se convierte en myaf2. Todas las demás propiedades siguen siendo las mismas que la forma adaptativa original.

Después de hacer clic en el icono ![aem6forms_pasta](assets/aem6forms_paste.png), se volverá a ocultar. Al mismo tiempo, solo puede pegar una vez. Para volver a crear una copia del mismo recurso, cópiela de nuevo.

### Cambiar el contenido del nuevo formulario adaptable {#change-contents-of-new-adaptive-form}

El contenido de los formularios adaptables pegados se puede cambiar utilizando los siguientes métodos para distinguirlo del formulario copiado:

1. **Cambiar propiedades de metadatos:**

   Puede cambiar las propiedades de metadatos del formulario adaptable, por ejemplo, el título y la descripción. Para obtener más información sobre las propiedades de los metadatos y cómo pueden cambiarse, consulte [Administración de metadatos del formulario](/help/forms/using/manage-form-metadata.md)

1. **Cambiar XFA/XSD para Forms adaptable basado en XFA/XSD:**

   Puede cambiar el XFA/XSD utilizado en los formularios adaptables. Para saber cómo se pueden cambiar estos formularios adaptables, consulte [Administración de metadatos de formulario](/help/forms/using/manage-form-metadata.md)

1. **Volver a publicar:**

   El recurso pegado es diferente del copiado. Puede publicarlo como un nuevo recurso para que esté disponible para los usuarios finales. Para obtener información sobre cómo publicar un recurso, consulte [Publicación y cancelación de la publicación de formularios](/help/forms/using/publishing-unpublishing-forms.md)

