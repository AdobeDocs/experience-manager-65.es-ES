---
title: Publicar carpetas en Brand Portal
seo-title: Publicar carpetas en Brand Portal
description: Obtenga información sobre cómo publicar y cancelar la publicación de carpetas en Brand Portal.
seo-description: Obtenga información sobre cómo publicar y cancelar la publicación de carpetas en Brand Portal.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
translation-type: tm+mt
source-git-commit: 9c73abc3291f2847c705cb649d2993fb186b0993

---


# Publish folders to Brand Portal{#publish-folders-to-brand-portal}

Como administrador de Recursos Adobe Experience Manager (AEM), puede publicar recursos y carpetas en la instancia de AEM Assets Brand Portal (o programar el flujo de trabajo de publicación para una fecha y hora posteriores) de su organización. Sin embargo, primero debe integrar Recursos AEM con Brand Portal. Para obtener más información, consulte [Configuración de la integración de AEM Assets con Brand Portal](/help/assets/brand-portal-configuring-integration.md).

Después de publicar un recurso o una carpeta, estará disponible para los usuarios de Brand Portal.

Si realiza las modificaciones posteriores en el recurso o la carpeta original en Recursos AEM, los cambios no se reflejarán en Brand Portal hasta que vuelva a publicar el recurso o la carpeta. Esta función garantiza que los cambios en curso no estén disponibles en Brand Portal. Solo los cambios aprobados publicados por un administrador están disponibles en Brand Portal.

## Publish folders to Brand Portal {#publish-folders-to-brand-portal-1}

1. En la interfaz de Recursos AEM, coloque el puntero sobre la carpeta deseada y seleccione la opción **Publicar** en las acciones rápidas.

   Como alternativa, seleccione la carpeta que desee y siga los pasos posteriores.

   ![publish2bp](assets/publish2bp.png)

1. **Publicar carpetas ahora**

   Para publicar las carpetas seleccionadas en Brand Portal, realice una de las acciones siguientes:

   * En la barra de herramientas, seleccione **Publicación** rápida. A continuación, en el menú, seleccione **Publicar en Brand Portal**.

   * En la barra de herramientas, seleccione **Administrar publicación**.
   1. En **Acción** , seleccione **Publicar en Brand Portal**, en **Programación** , seleccione **Ahora** y haga clic en **Siguiente.**
   1. Confirme su selección en **Ámbito** y haga clic en **Publicar en Brand Portal**.
   Aparece un mensaje que indica que la carpeta se ha puesto en cola para su publicación en Brand Portal. Inicie sesión en la interfaz de Brand Portal para ver la carpeta publicada.

   **Publicar carpetas más tarde**

   Para programar el flujo de trabajo de publicación en Brand Portal de carpetas de recursos para una fecha u hora posterior:

   1. Una vez que haya seleccionado los recursos o las carpetas que desea publicar, seleccione **Administrar publicación** en la barra de herramientas de la parte superior.
   1. En **Acción** , seleccione **Publicar en Brand Portal**, en **Programación** , seleccione **Más adelante**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Seleccione una fecha **de** activación y especifique la hora. Haga clic en **Siguiente**. 
   1. Confirme la selección en **Ámbito**. Haga clic en **Siguiente**. 
   1. Especifique un título de flujo de trabajo en **Flujos de trabajo**. Haga clic en **Publicar posteriormente**.

      ![management eschedulepub](assets/manageschedulepub.png)



## Unpublish folders from Brand Portal {#unpublish-folders-from-brand-portal}

Puede eliminar cualquier carpeta de recursos publicada en Brand Portal cancelándola de la publicación de la instancia de AEM Author. Después de cancelar la publicación de la carpeta original, su copia ya no estará disponible para los usuarios de Brand Portal.

Tiene la opción de cancelar la publicación de carpetas desde Brand Portal rápidamente o programarlas para una fecha y hora posteriores. Para cancelar la publicación de carpetas de recursos desde Brand Portal:

1. En la interfaz de Recursos AEM de la instancia de AEM Author, seleccione la carpeta que desee cancelar la publicación.

   ![publish2bp-1](assets/publish2bp.png)

1. En la barra de herramientas, haga clic en **Administrar publicación**.

1. **Cancelar la publicación de Brand Portal ahora**

   Para cancelar rápidamente la publicación de la carpeta deseada desde Brand Portal:

   1. En la barra de herramientas, seleccione **Administrar publicación**.
   1. En **Acción** , seleccione **Cancelar publicación en Brand Portal**, en **Programación** , seleccione **Ahora** y haga clic en **Siguiente.**
   1. Confirme su selección en **Ámbito** y haga clic en **Cancelar publicación desde Brand Portal**.
   ![confirmar-cancelar publicación](assets/confirm-unpublish.png)

   **Cancelar la publicación de Brand Portal más tarde**

   Para programar la publicación de una carpeta desde Brand Portal a una fecha y hora posteriores:

   1. En la barra de herramientas, seleccione **Administrar publicación**.
   1. En **Acción** , seleccione **Cancelar publicación en Brand Portal** y, en **Programación** , seleccione **Más adelante**.
   1. Seleccione una fecha **de** activación y especifique la hora. Haga clic en **Siguiente**. 
   1. Confirme la selección en **Ámbito** y haga clic en **Siguiente**.
   1. Especifique un título **** de workflow en **Flujos de trabajo**. Haga clic en **Cancelar publicación posteriormente.**

      ![flujos de trabajo sin publicar](assets/unpublishworkflows.png)


>[!NOTE]
>
>El procedimiento para publicar o cancelar la publicación de un recurso en o desde Brand Portal es similar al procedimiento correspondiente para una carpeta.

