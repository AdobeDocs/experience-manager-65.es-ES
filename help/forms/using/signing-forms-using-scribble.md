---
title: Aplicar firmas electrónicas a un formulario utilizando firmas de anotaciones
seo-title: Apply electronic signatures to a form using scribble signatures
description: Firma de formularios mediante anotaciones
seo-description: Signing forms using scribble
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: Adaptive Forms
exl-id: 096f61b0-59f4-4699-9093-8fb1ed81fded
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Aplicar firmas electrónicas a un formulario utilizando firmas de anotaciones{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

Puede usar la variable **Firma manuscrita** y **Paso de firma** componente para dibujar la firma (Scribble) en un formulario adaptable. El componente Paso de firma muestra una versión PDF del formulario adaptable. Se necesita una opción Documento de registro activada o formularios adaptables basados en plantillas de formulario para utilizar el componente de paso Firma.

![Cuadro de diálogo de signo de almohadilla](/help/forms/using/assets/scribble-signature.png)

## Varias opciones disponibles en la ventana de firma

* **A:** Haga clic en el **Pincel de pintura** para dibujar su firma en lienzo.
* **B:** Haga clic en el **Borrar** para borrar la firma en el lienzo.
* **C:** Haga clic en el **Geolocalización** para añadir geolocalización junto con la firma.
* **D:** Haga clic en el **Teclado** para escribir su nombre en lienzo.

Una vez que pulse Listo![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) en la ventana Scribble signature , no puede editar la firma. Si desea editar la firma, debe ignorar la firma actual y volver a firmarla con la opción Pincel/Teclado anterior.

Puede pulsar el botón **Configurar** ![configure](assets/configure.png) para establecer la proporción de aspecto del lienzo de firma manuscrita.
* Cuando la proporción de aspecto del lienzo de firma de Scribble es menor que 1, la información de geolocalización se agrega en la parte inferior del lienzo de firma Scribble.

* Cuando la proporción de aspecto del lienzo de firma de Scribble es mayor que 1, la información de geolocalización se agrega al lado derecho del lienzo de firma Scribble.

![firma de anotaciones - inferior](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>Las firmas siempre se guardan en formato PNG.

## Configuración de un formulario adaptable para utilizar Scribble Signature {#configure-an-adaptive-form-to-use-scribble-signature}

1. Crear un documento de registro activado o un formulario adaptable basado en una plantilla de formulario. Para obtener información paso a paso, consulte [Creación de un formulario adaptable](../../forms/using/creating-adaptive-form.md).
1. Arrastre y suelte la **Firma manuscrita** del navegador de componentes al formulario adaptable.
1. Toque . **Configurar** ![configure](assets/configure.png) icono. Abre el navegador de propiedades y muestra las propiedades del componente Firma de anotaciones. Configure las propiedades del componente Scribble Signature.
1. Arrastre y suelte el componente Paso de firma desde el navegador de componentes al formulario adaptable.

   >[!NOTE]
   >
   >El componente Paso de firma ocupa el ancho completo disponible para el formulario. Se recomienda no tener ningún otro componente en la sección que contenga el componente Paso de firma.

1. En el navegador de contenido, pulse **Contenedor de formulario** y pulse el botón **Configurar** ![](/help/forms/using/assets/configure.png) icono. Abre el explorador de propiedades y muestra las propiedades del contenedor de formularios adaptables. Vaya a **Contenedor de formulario adaptable** > **Firma electrónica** y desmarque **Habilitar Adobe Sign** . Puntee en Listo ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para guardar los cambios.

   >[!NOTE]
   >
   >Cuando se añade un componente Paso de firma a un formulario adaptable, la opción Habilitar Adobe Sign se selecciona automáticamente.

1. Toque . **Configurar** ![configure](assets/configure.png) icono. Abre el navegador de propiedades y muestra las propiedades del paso Firma. Configure las siguientes propiedades:

   * **Nombre del elemento**: Especifique el nombre del componente.

   * **Título:** Especifique un título único del componente.
   * **Mensaje de plantilla:** Especifique el mensaje que se mostrará mientras se carga el PDF de firma. Los servicios de Adobe Sign tardan algún tiempo en preparar y cargar el PDF de firma.
   * **Servicio de firma:** Seleccione el **Firma manuscrita** .

   * **Clase CSS**: Especifique la clase CSS de la biblioteca de cliente, si la hay. Se recomienda utilizar [temáticas](../../forms/using/themes.md) y [estilos en línea](../../forms/using/inline-style-adaptive-forms.md) en lugar de la clase CSS.

   Puntee en Listo ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para guardar los cambios. La firma se ha configurado correctamente.

   Ahora, al rellenar un formulario, se muestra una versión PDF del formulario adaptable y se proporcionan las opciones para firmar el documento PDF. Para obtener información detallada, consulte [Firmar un formulario adaptable con firma manuscrita](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Firmar un formulario adaptable con firma manuscrita {#sign-an-adaptive-form-using-scribble-signature}

1. Después de rellenar un formulario adaptable y llegar a la página Paso de firma, se muestra la pantalla de firma.

   ![Cuadro de diálogo de signo de almohadilla](/help/forms/using/assets/esignscribblesign.jpg)

1. Haga clic en **[!UICONTROL Sign]**. Aparecerá el cuadro de diálogo del signo de garabateo. Firme el formulario y haga clic en Finalizado ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) para guardar la firma.

   ![Cuadro de diálogo de signo de almohadilla](/help/forms/using/assets/scribblewidget.png)

1. Haga clic en Completar para finalizar el proceso de firma.

   ![Completar el proceso de firma](/help/forms/using/assets/scribblecomplete.jpg)

Las firmas se agregan al formulario y el control de formulario se mueve al panel siguiente.
