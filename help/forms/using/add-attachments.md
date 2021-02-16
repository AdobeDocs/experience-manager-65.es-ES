---
title: Añadir archivos adjuntos
seo-title: Añadir archivos adjuntos
description: Añadir fotografías y garabatear notas como anotaciones a la tarea en la aplicación de AEM Forms
seo-description: Añadir fotografías y garabatear notas como anotaciones a la tarea en la aplicación de AEM Forms
uuid: 3d2738b4-fd43-44ec-8eaf-a2ad4b7e5af5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: d5976ed2-4482-495c-bf77-6d192379cfef
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# Añadiendo datos adjuntos{#adding-attachments}

## Añadir datos adjuntos en formularios sincronizados con AEM Forms Workflow Server (AEM Forms en JEE) {#adding-annotations}

La aplicación de AEM Forms le permite adjuntar imágenes, notas con garabatos y notas de texto al formulario sincronizado con el servidor AEM Forms JEE. Si el formulario se carga desde un servidor de AEM Forms Workflow, los datos adjuntos se agregan al formulario. Puede tocar el botón de datos adjuntos ![attachment-app](assets/attachments-app.png) para ver todos los datos adjuntos de un formulario juntos. La notificación roja especifica el número de datos adjuntos en el formulario. Si no hay datos adjuntos en el formulario, no podrá ver el botón rojo de notificaciones. Si no hay datos adjuntos en el formulario, al tocar el botón ![adjuntar](assets/attch.png), obtendrá opciones para adjuntar fotos o garabatos.

Sus opciones son:

* **Galería**: Permite agregar una imagen de las imágenes guardadas en el dispositivo.

* **Cámara**: Permite tomar una imagen y agregarla al formulario.

* **Notas**: Permite agregar un garabato o una nota de texto. Utilice ![garabatos](assets/scribble.png) para agregar un garabato y ![teclado](assets/keyboard.png) para agregar una nota de texto.

>[!NOTE]
>
>Los datos adjuntos agregados por un usuario son visibles para otros usuarios de la aplicación de AEM Forms. Otros usuarios no pueden eliminar los archivos adjuntos agregados por un usuario.


### Pantalla Archivos adjuntos {#the-attachments-screen}

Para ver todos los archivos adjuntos en un lugar, toque ![attachment-app](assets/attachments-app.png). Aquí puede agregar, cambiar el nombre y eliminar archivos adjuntos.

![Todos los datos adjuntos en un lugar](assets/attachments-screen.png)

Puede utilizar el botón **+** de la pantalla Datos adjuntos para adjuntar otra imagen, un garabato o texto.

### Añadir una fotografía {#adding-a-photograph}

Puede utilizar la cámara del dispositivo móvil o las imágenes guardadas en el dispositivo para adjuntar una imagen en el formulario.

1. Toque el botón de datos adjuntos ![adjunto](assets/attch.png) en la parte inferior de la ventana.
1. Toque **Galería** o **Cámara** en la ventana emergente que aparece.
1. En función de la opción seleccionada, realice lo siguiente:

   1. Si selecciona **Cámara**.

      Toma una fotografía. A continuación, toque el botón **Use** ![use-pic](assets/use-pic.png).

      O toque el botón **Reproducir** ![retomar](assets/retake.png) para retomar la fotografía.

   1. Si selecciona **Galería**.

      Aparece el navegador de imágenes del dispositivo. En el navegador de imágenes del dispositivo, toque la imagen que desee adjuntar.

### Añadir una nota {#adding-a-note}

La opción **Notas** permite agregar garabatos a mano alzada y datos adjuntos de texto en el formulario.

1. Toque el botón de datos adjuntos ![adjunto](assets/attch.png) en la parte inferior de la ventana.
1. Toque **Notas** en la ventana emergente que aparece.
1. En la interfaz de usuario de Notes que se inicia, capture un garabato a mano alzada.

   ![Interfaz de garabatos](assets/scribble-ui.png)

   Garabato

   Puede utilizar las siguientes opciones en la interfaz de garabatos:

   * **Borrar**: Borra la pantalla.
   * **Botón** Listo: Adjunta el garabato actual.
   * **Botón** Cancelar: Desecha el garabato actual y sale de la interfaz de usuario de Garabatos.
   * ![teclado](assets/keyboard.png): Borra el garabato y le permite agregar una nota de texto.

   ![Teclado en garabatear aplicación de AEM Forms](assets/keyboard-inapp.png)

## Datos adjuntos en formularios sincronizados con los servidores de AEM Forms sin AEM Forms Workflow (AEM Forms en OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

Los archivos adjuntos para formularios móviles sincronizados con servidores OSGi de AEM Forms funcionan de forma similar a los servidores AEM Forms JEE.

Los archivos adjuntos de nivel de formulario no son compatibles con los formularios adaptables cargados en la aplicación desde un servidor OSGi de AEM Forms. Para adjuntar imágenes o notas de texto, active los datos adjuntos de nivel de campo en el formulario cuando lo cree. Arrastre y suelte el componente de archivo adjunto desde el navegador de componentes del campo.

En el caso de los formularios adaptables, puede realizar la vista de los archivos adjuntos en el documento del registro (DoR). Consulte [Generar Documento de registro para formularios adaptables que no sean XFA](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
