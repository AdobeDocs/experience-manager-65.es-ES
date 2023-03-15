---
title: Agregar archivos adjuntos
seo-title: Adding attachments
description: Agregue fotografías y notas garabateadas como anotaciones a su tarea en la aplicación de AEM Forms
seo-description: Add photographs and scribble notes as annotations to your task in the AEM Forms app
uuid: 3d2738b4-fd43-44ec-8eaf-a2ad4b7e5af5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: d5976ed2-4482-495c-bf77-6d192379cfef
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 100%

---

# Agregar archivos adjuntos{#adding-attachments}

## Agregar archivos adjuntos en formularios sincronizados con el servidor de flujo de trabajo de AEM Forms (AEM Forms en JEE) {#adding-annotations}

La aplicación de AEM Forms permite adjuntar imágenes, notas garabateadas y notas de texto al formulario sincronizado con el servidor JEE de AEM Forms. Si el formulario se carga desde un servidor del flujo de trabajo de AEM Forms, los archivos adjuntos se agregan al formulario. Puede pulsar el botón de archivos adjuntos ![attachment-app](assets/attachments-app.png) para ver todos los archivos adjuntos de un formulario juntos. La notificación roja especifica el número de archivos adjuntos en el formulario. Si no hay datos adjuntos en el formulario, no verá el botón de notificaciones rojo. Si no hay datos adjuntos en el formulario, al pulsar el botón de archivos adjuntos ![attch](assets/attch.png), verá opciones para adjuntar fotos o garabatos.

Las opciones son las siguientes:

* **Galería**: permite agregar una imagen de las imágenes guardadas en el dispositivo.

* **Cámara**: permite tomar una imagen y agregarla al formulario.

* **Notas**: permite agregar un garabato o una nota de texto. Use ![garabato](assets/scribble.png) para agregar un garabato y el ![teclado](assets/keyboard.png) para agregar una nota de texto.

>[!NOTE]
>
>Los archivos adjuntos agregados por un usuario son visibles para otros usuarios de aplicaciones de AEM Forms. Otros usuarios no pueden eliminar los archivos adjuntos que haya agregado un usuario.

### Pantalla de archivos adjuntos {#the-attachments-screen}

Para ver todos los archivos adjuntos en un lugar, pulse ![attachment-app](assets/attachments-app.png). Aquí puede agregar, cambiar el nombre y eliminar archivos adjuntos.

![Todos los archivos adjuntos en un lugar](assets/attachments-screen.png)

Puede usar el botón **+** de la pantalla de archivos adjuntos para adjuntar otra imagen, garabato o texto.

### Agregar una fotografía {#adding-a-photograph}

Puede utilizar la cámara del dispositivo móvil o guardar imágenes en el dispositivo para adjuntar una imagen en el formulario.

1. Pulse el botón de archivos adjuntos ![attch](assets/attch.png) de la parte inferior de la ventana.
1. Pulse **Galería** o **Cámara** en la ventana emergente que aparece.
1. En función de la opción seleccionada, realice lo siguiente:

   1. Si selecciona **Cámara**.

      Tome una foto. A continuación, pulse el botón **Usar** ![use-pic](assets/use-pic.png).

      O pulse el botón **Repetir** ![retake](assets/retake.png) para volver a tomar la fotografía.

   1. Si selecciona **Galería**.

      Aparecerá el explorador de imágenes del dispositivo. En el explorador de imágenes de su dispositivo, pulse la imagen que desea adjuntar.

### Agregar una nota {#adding-a-note}

La opción **Notas** permite agregar garabatos hechos a mano alzada y archivos adjuntos de texto en el formulario.

1. Pulse el botón de archivos adjuntos ![attch](assets/attch.png) de la parte inferior de la ventana.
1. Pulse **Notas** en la ventana emergente que aparece.
1. En la interfaz de usuario de Notas que se inicia, realice un garabato a mano alzada.

   ![Interfaz de Garabatos](assets/scribble-ui.png)

   Garabato

   Puede utilizar las siguientes opciones en la interfaz de garabatos:

   * **Borrar**: borra la pantalla.
   * **Botón Listo**: adjunta el garabato actual.
   * **Botón Cancelar**: descarta el garabato actual y sale de la interfaz de usuario de Garabatos.
   * ![teclado](assets/keyboard.png): borra el garabato y permite agregar una nota de texto.

   ![Teclado en los garabatos de la aplicación de AEM Forms](assets/keyboard-inapp.png)

## Archivos adjuntos en formularios sincronizados con los servidores de AEM Forms sin flujo de trabajo de AEM Forms (AEM Forms en OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Los archivos adjuntos para formularios móviles sincronizados con servidores OSGi de AEM Forms funcionan de forma similar a los servidores JEE de AEM Forms.

Los archivos adjuntos de nivel de formulario no son compatibles con los formularios adaptables cargados en la aplicación desde un servidor OSGi de AEM Forms. Para adjuntar imágenes o notas de texto, active los archivos adjuntos de nivel de campo en el formulario cuando lo cree. Arrastre y suelte el componente de archivo adjunto desde el explorador de componentes del campo.

En el caso de los formularios adaptables, puede ver los archivos adjuntos en el documento de registro (DoR). Consulte, [Generar un documento de registro para formularios adaptables que no sean XFA](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
