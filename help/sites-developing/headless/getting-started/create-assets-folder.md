---
title: Guía de inicio rápido Creación de una carpeta de recursos sin encabezado
description: Utilice modelos de fragmentos de contenido de AEM para definir la estructura de los fragmentos de contenido, la base del contenido sin encabezado.
exl-id: 8d913056-fcfa-4cdd-b40a-771f13dfd0f4
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 78%

---

# Guía de inicio rápido Creación de una carpeta de recursos sin encabezado {#creating-an-assets-folder}

Utilice modelos de fragmentos de contenido de AEM para definir la estructura de los fragmentos de contenido, la base del contenido sin encabezado. A continuación, los fragmentos de contenido se almacenan en carpetas de recursos.

## ¿Qué es una carpeta de recursos? {#what-is-an-assets-folder}

[Ahora que ha creado modelos de fragmentos de contenido](create-content-model.md) que definen la estructura que desea para los futuros fragmentos de contenido, probablemente tenga ganas de crear algunos fragmentos.

Sin embargo, primero debe crear una carpeta de recursos en la que almacenarlos.

Las carpetas de recursos se utilizan para lo siguiente [organizar recursos de contenido tradicionales](/help/assets/manage-assets.md) le gustan las imágenes y el vídeo y los fragmentos de contenido.

## Cómo crear una carpeta de recursos {#how-to-create-an-assets-folder}

Un administrador solo tendría que crear carpetas ocasionalmente para organizar el contenido a medida que se crea. Para los fines de esta guía de introducción, solo necesitamos crear una carpeta.

1. AEM Inicie sesión en el menú principal y, a continuación, seleccione: **Navegación > Recursos > Archivos**.
1. Clic **Crear > Carpeta**.
1. Proporcione un **Título** y **Nombre** para su carpeta.
   * El **Título** debe ser descriptivo.
   * El **Nombre** se convertirá en el nombre de nodo en el repositorio.
      * Se generará automáticamente en función del título y se ajustará según las [convenciones de nomenclatura de AEM.](/help/sites-developing/naming-conventions.md)
      * Se puede modificar si es necesario.

   ![Crear carpeta](assets/assets-folder-create.png)
1. Seleccione la carpeta que ha creado y, a continuación, seleccione **Propiedades** en la barra de herramientas (o utilice la variable `p` [método abreviado de teclado.](/help/sites-authoring/keyboard-shortcuts.md))
1. En la ventana **Propiedades**, seleccione la pestaña **Servicios de nube**.
1. Para la **Configuración de nube**, seleccione la [configuración que creó anteriormente.](create-configuration.md)
   ![Configurar la carpeta de recursos](assets/assets-folder-configure.png)
1. Haga clic en **Guardar y cerrar**.
1. Clic **OK** en la ventana de confirmación.

   ![Ventana de confirmación](assets/assets-folder-confirmation.png)

Puede crear subcarpetas adicionales dentro de la carpeta que ha creado. Las subcarpetas heredarán la **Configuración de nube** de la carpeta principal. Sin embargo, esto se puede sobrescribir si desea utilizar modelos de otra configuración.

Si está usando una estructura de sitio localizada, puede [crear una raíz de idioma](/help/assets/multilingual-assets.md) debajo de la nueva carpeta.

## Siguientes pasos {#next-steps}

Ahora que ha creado una carpeta para los fragmentos de contenido, puede pasar a la cuarta parte de la guía de introducción y [crear fragmentos de contenido.](create-content-fragment.md)

>[!TIP]
>
>Para obtener información detallada acerca de la administración de fragmentos de contenido, consulte la [Documentación de fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)
