---
title: Eliminación de formularios y recursos relacionados
seo-title: Eliminación de formularios y recursos relacionados
description: Cómo eliminar un formulario o un recurso en AEM Forms y el impacto en los recursos a los que se hace referencia y en los formularios XFA.
seo-description: Cómo eliminar un formulario o un recurso en AEM Forms y el impacto en los recursos a los que se hace referencia y en los formularios XFA.
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Eliminación de formularios y recursos relacionados {#deleting-forms-and-related-resources}

Puede eliminar los formularios y recursos para quitar estos recursos del repositorio. La operación de eliminación funciona en todos los tipos de recursos y carpetas.

Si elimina un recurso de la instancia Autor, el recurso también se elimina de la instancia Publicar. El servidor de AEM Forms consta de instancias de autor y publicación. La instancia de autor sirve para crear y administrar recursos y recursos de formularios. La instancia Publicar contiene los recursos de formularios publicados y los recursos relacionados disponibles para los usuarios finales.

## Cómo eliminar un formulario {#how-to-delete-a-form}

1. Inicie sesión en la interfaz de usuario de AEM Forms mediante el acceso `https://[hostname]:[portport]/aem/forms.html.`
1. Desplácese hasta el formulario que desee eliminar y selecciónelo. Haga clic en Eliminar ![aem6forms_delete2](assets/aem6forms_delete2.png) en la barra de herramientas y confirme la operación de eliminación.

   >[!NOTE]
   >
   >Solo se puede eliminar un formulario a la vez. Elimine varios formularios individualmente o elimine la carpeta principal.

1. Antes de eliminar un recurso, AEM Forms comprueba la existencia de referencias y solicita una confirmación explícita. Haga clic en Forzar eliminación si desea eliminar el recurso independientemente del estado de la relación.

   >[!NOTE]
   >
   >La eliminación de un recurso al que hacen referencia otros recursos puede provocar problemas funcionales.

   >[!NOTE]
   >
   >Si el recurso seleccionado es una carpeta y contiene dicho recurso en su jerarquía, elimine otros recursos individualmente o elimine toda la carpeta.

## Impacto de la eliminación de un formulario XFA al que se hace referencia {#impact-of-deleting-a-referenced-xfa-form}

En AEM Forms, una plantilla de formulario XFA puede ser referida por un formulario adaptable u otra plantilla de formulario XFA. Además, una plantilla puede hacer referencia a un recurso u otra plantilla XFA.

No es aconsejable eliminar un formulario XFA al que se hace referencia mediante un formulario adaptable, ya que puede dañar el formulario adaptable. Cuando un formulario adaptable hace referencia a un formulario XFA, sus campos están enlazados. Tras la eliminación de XFA, el formulario adaptable no puede sincronizar sus campos con los campos XFA y muestra un mensaje de error para dichos campos. Para obtener más información sobre el impacto de la eliminación de XFA a la que se hace referencia y sobre los AF sucios, consulte [Actualización de formularios](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p)XFA a los que se hace referencia.

Para eliminar un formulario XFA de este tipo, actualice el formulario adaptable y elimine los enlaces con los campos XFA.
