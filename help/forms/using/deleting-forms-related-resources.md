---
title: Eliminación de formularios y recursos relacionados
seo-title: Eliminación de formularios y recursos relacionados
description: Eliminación de un formulario o un recurso en AEM Forms y el impacto en los recursos a los que se hace referencia y de referencia y en los formularios XFA.
seo-description: Eliminación de un formulario o un recurso en AEM Forms y el impacto en los recursos a los que se hace referencia y de referencia y en los formularios XFA.
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# Eliminación de formularios y recursos relacionados {#deleting-forms-and-related-resources}

Puede eliminar los formularios y recursos para quitar estos recursos del repositorio. La operación de eliminación funciona en todos los tipos de recursos y carpetas.

Si elimina un recurso de la instancia de autor, el recurso también se elimina de la instancia de publicación. El servidor de AEM Forms consta de instancias de Autor y Publicación . La instancia Autor es para crear y administrar recursos y recursos de formularios. La instancia Publicar contiene los recursos de formularios publicados y los recursos relacionados disponibles para los usuarios finales.

## Cómo eliminar un formulario {#how-to-delete-a-form}

1. Inicie sesión en la interfaz de usuario de AEM Forms accediendo a `https://[hostname]:'port'/aem/forms.html.`
1. Desplácese hasta el formulario que quiera eliminar y selecciónelo. Haga clic en Eliminar ![aem6forms_delete2](assets/aem6forms_delete2.png) en la barra de herramientas y confirme la operación de eliminación.

   >[!NOTE]
   >
   >Solo se puede eliminar un formulario a la vez. Elimine varios formularios individualmente o elimine la carpeta principal.

1. Antes de eliminar un recurso, AEM Forms comprueba si hay referencias y solicita una confirmación explícita. Haga clic en Forzar eliminación si desea eliminar el recurso independientemente del estado de la relación.

   >[!NOTE]
   >
   >La eliminación de un recurso al que otros recursos hacen referencia puede causar problemas funcionales.

   >[!NOTE]
   >
   >Si el recurso seleccionado es una carpeta y contiene dicho recurso en su jerarquía, elimine otros recursos de forma individual o elimine toda la carpeta.

## Impacto de eliminar un formulario XFA al que se hace referencia {#impact-of-deleting-a-referenced-xfa-form}

En AEM Forms, una plantilla de formulario XFA se puede referir mediante un formulario adaptable u otra plantilla de formulario XFA. Además, una plantilla puede hacer referencia a un recurso u otra plantilla XFA.

No es aconsejable eliminar un formulario XFA al que se hace referencia mediante un formulario adaptable, ya que puede dañar el formulario adaptable. Cuando un formulario adaptable hace referencia a un formulario XFA, sus campos están enlazados. Tras la eliminación de XFA, el formulario adaptable no puede sincronizar sus campos con los campos XFA y muestra un mensaje de error para dichos campos. Para obtener más información sobre el impacto de la eliminación de XFA a la que se hace referencia y sobre los AF sucios, consulte [Actualización de formularios XFA a los que se hace referencia](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p).

Para eliminar un formulario XFA de este tipo, actualice el formulario adaptable y elimine los enlaces con los campos XFA.
