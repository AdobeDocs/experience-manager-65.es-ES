---
title: Asociación de revisores de envío con un formulario
seo-title: Asociación de revisores de envío con un formulario
description: Aprenda a asociar revisores de envío con un formulario en AEM Forms. Los revisores asociados revisan un formulario enviado a través del portal de formularios.
seo-description: Aprenda a asociar revisores de envío con un formulario en AEM Forms. Los revisores asociados revisan un formulario enviado a través del portal de formularios.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
translation-type: tm+mt
source-git-commit: 55c12683ba66b3aace07ea83931c9c32ea65663e

---


# Asociación de revisores de envío con un formulario {#associating-submission-reviewers-with-a-form}

Al crear un formulario, puede especificar los usuarios que lo revisan mediante el portal de formularios y proporcionar comentarios. Su organización puede recopilar comentarios y retrabajar los formularios enviados.

AEM Forms permite asociar un grupo de revisores a un formulario. Los usuarios agregados a un grupo de revisión de un formulario ven los envíos de este formulario y proporcionan sus comentarios.

Los grupos de revisores asignados a un formulario solo pueden revisar los envíos del formulario especificado.

## Requisitos previos {#prerequisite}

### Habilitación de la propiedad de grupos de revisor de envío para formularios adaptables mediante el editor de esquemas de metadatos {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Para asociar un grupo de revisores a un formulario, edite el esquema de metadatos de los formularios adaptables. De forma predeterminada, no se puede agregar un grupo de revisores a un formulario enviado.

Para editar el esquema de metadatos:

1. En el modo de creación, en Experience Manager, haga clic en **Herramientas** > **Recursos** > Esquemas **de metadatos**.
1. En la página Formularios de esquema, vaya a **Formularios** > **Formularios creados en AEM.**

   La dirección URL de la página es:

   ```
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Seleccione Formulario **** adaptable y haga clic en **Editar**.
1. En la página Editar formulario, haga clic en **Avanzadas**.
1. En la ficha Avanzado, arrastre y suelte el componente Texto **** de una sola línea disponible en Formulario de compilación.
1. Seleccione el componente de texto agregado para ver su configuración.

   En Configuración, introduzca `./jcr:content/metadata/form-submission-reviewer-group` en el campo Asignar a propiedad.

   El campo de grupo del revisor de envío de las propiedades avanzadas del formulario adaptable se activa con el nombre que especifique en Etiqueta de campo.

## Asociación de revisores de envío con un formulario {#associating-submission-reviewers-with-a-form-1}

Para asociar revisores de envío con un formulario adaptable, cree un grupo de revisores y agregue usuarios a él. Agregue el grupo de revisores creado en el campo revisor de envío de formulario en las propiedades avanzadas del formulario.
Los grupos de usuarios permiten asociar diferentes conjuntos de revisores de envío con diferentes formularios adaptables. Esta función evita que un usuario no autorizado revise el envío.

Antes de realizar los siguientes pasos, consulte [Requisito previo](../../forms/using/adding-reviewers-form.md#prerequisite).

Para crear un grupo y agregarle miembros, vaya a **Herramientas** > **Operaciones** > **Seguridad** > **Grupos**.
Para obtener más información, consulte Administración [de usuarios y servicios](/help/sites-administering/security.md).
Asegúrese de agregar el grupo que crea como miembro del grupo de usuarios predeterminado: **forms-submit-reviewers**. Este grupo de usuarios se envía con AEM Forms y garantiza que los usuarios se añadan como revisores de envío.

Para asociar grupos de usuarios con un formulario adaptable:

1. En el modo de creación, vaya a **Formularios** > **Formularios y documentos**.
1. Utilice la opción **Seleccionar **para seleccionar un formulario adaptable y haga clic en **Ver propiedades**.
1. En la ventana Propiedades del formulario, haga clic en **Editar** y, a continuación, en **AVANZADO**.
1. Introduzca el grupo en el campo de grupo de revisor de envío y haga clic en **Finalizado**.

   El campo de grupo de revisor de envío aparece con el nombre especificado en el esquema de metadatos editado de los formularios adaptables.

>[!NOTE]
>
>Replique usuarios y formularios para garantizar la disponibilidad de los usuarios y formularios en la implementación remota de AEM Forms.
>
>Asegúrese de que todos los usuarios se replican como miembros revisores de los grupos de usuarios en la implementación remota.

