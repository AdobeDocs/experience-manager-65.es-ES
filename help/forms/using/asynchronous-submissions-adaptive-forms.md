---
title: Envío asíncrono de formularios adaptables
seo-title: Envío asíncrono de formularios adaptables
description: Aprenda a configurar el envío asincrónico para formularios adaptables.
seo-description: Aprenda a configurar el envío asincrónico para formularios adaptables.
uuid: 6555ac63-4d99-4b39-a2d0-a7e61909106b
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 0a0d2109-ee1f-43f6-88e5-1108cd215da6
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---


# Envío asíncrono de formularios adaptables{#asynchronous-submission-of-adaptive-forms}

Tradicionalmente, los formularios web se configuran para enviarse sincrónicamente. En el envío sincrónico, cuando los usuarios envían un formulario, se les redirige a una página de acuse de recibo, a una página de agradecimiento o, en caso de error en el envío, a una página de error. Sin embargo, las experiencias web modernas, como las aplicaciones de una sola página, están ganando popularidad cuando la página web permanece estática mientras que la interacción cliente-servidor se produce en segundo plano. Ahora puede proporcionar esta experiencia con formularios adaptables configurando el envío asincrónico.

En el envío asincrónico, cuando un usuario envía un formulario, el desarrollador del formulario rellena una experiencia independiente como redirigir a otro formulario o a una sección independiente del sitio web. El autor también puede añadir servicios separados como el envío de datos a un almacén de datos diferente o añadir un motor de análisis personalizado. En caso de envío asincrónico, un formulario adaptable se comporta como una aplicación de una sola página, ya que el formulario no se vuelve a cargar o su URL no cambia cuando los datos del formulario enviados se validan en el servidor.

Siga leyendo para obtener más información sobre el envío asincrónico en formularios adaptables.

## Configurar el envío asincrónico {#configure}

Para configurar el envío asincrónico de un formulario adaptable:

1. En el modo de creación de formularios adaptables, seleccione el objeto Contenedor de formulario y pulse ![cmppr1](assets/cmppr1.png) para abrir sus propiedades.
1. En la sección **[!UICONTROL Submission]** properties , habilite **[!UICONTROL Usar envío asincrónico]**.
1. En la sección **[!UICONTROL Al enviar]**, seleccione una de las siguientes opciones para realizar el envío correcto del formulario.

   * **[!UICONTROL Redirigir a URL]**: Redirige a la dirección URL o página especificada en el envío del formulario. Puede especificar una dirección URL o examinar para elegir la ruta a una página en el campo **[!UICONTROL Redirigir URL/Path]**.
   * **[!UICONTROL Mostrar mensaje]**: Muestra un mensaje sobre el envío del formulario. Puede escribir un mensaje en el campo de texto debajo de la opción Mostrar mensaje . El campo de texto admite el formato de texto enriquecido.

1. Toque ![check-button1](assets/check-button1.png) para guardar las propiedades.

## Funcionamiento del envío asincrónico {#how-asynchronous-submission-works}

AEM Forms proporciona controladores de éxito y de errores listos para usar para los envíos de formularios. Los controladores son funciones del lado del cliente que se ejecutan en función de la respuesta del servidor. Cuando se envía un formulario, los datos se transmiten al servidor para su validación, lo que devuelve una respuesta al cliente con información sobre el suceso success o error del envío. La información se pasa como parámetros al controlador correspondiente para ejecutar la función.

Además, los autores y desarrolladores de formularios pueden escribir reglas a nivel de formulario para anular los controladores predeterminados. Para obtener más información, consulte [Sustituir controladores predeterminados por reglas](#custom).

Primero vamos a revisar la respuesta del servidor para los eventos de éxito y de error.

### Respuesta del servidor para el evento de éxito de envío {#server-response-for-submission-success-event}

La estructura de la respuesta del servidor para el evento de éxito de envío es la siguiente:

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

La respuesta del servidor en caso de que el envío del formulario se realice correctamente incluye:

* Tipo de formato de datos del formulario: XML o JSON
* Datos de formulario en formato XML o JSON
* Opción seleccionada para redireccionar a una página o mostrar un mensaje como se ha configurado en el formulario
* Dirección URL de la página o contenido del mensaje, según la configuración del formulario

El controlador de éxito lee la respuesta del servidor y, en consecuencia, redirige a la dirección URL de la página configurada o muestra un mensaje.

### Respuesta del servidor para el evento de error de envío {#server-response-for-submission-error-event}

La estructura de la respuesta del servidor para el evento de error de envío es la siguiente:

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

La respuesta del servidor en caso de error en el envío del formulario incluye:

* Motivo del error, error de CAPTCHA o validación del lado del servidor
* Lista de objetos de error, que incluye la expresión SOM del campo en el que se ha producido un error al efectuar la validación y el mensaje de error correspondiente

El controlador de errores lee la respuesta del servidor y, en consecuencia, muestra el mensaje de error en el formulario.

## Sobrescribir los controladores predeterminados mediante las reglas {#custom}

Los desarrolladores y autores de formularios pueden escribir reglas, a nivel de formulario, en el editor de código para anular los controladores predeterminados. La respuesta del servidor para eventos de éxito y error se expone en el nivel de formulario, al que los desarrolladores pueden acceder mediante `$event.data` en las reglas.

Realice los siguientes pasos para escribir reglas en el editor de código para controlar los eventos de éxito y error.

1. Abra el formulario adaptable en modo de creación, seleccione cualquier objeto de formulario y pulse ![edit-rules1](assets/edit-rules1.png) para abrir el editor de reglas.
1. Seleccione **[!UICONTROL Formulario]** en el árbol de objetos de formulario y pulse **[!UICONTROL Crear]**.
1. Seleccione **[!UICONTROL Editor de código]** en la lista desplegable de selección de modo.
1. En el editor de código, pulse **[!UICONTROL Editar código]**. Pulse **[!UICONTROL Editar]** en el cuadro de diálogo de confirmación.
1. Elija **[!UICONTROL Envío correcto]** o **[!UICONTROL Error en envío]** en la lista desplegable **[!UICONTROL Evento]**.
1. Escriba una regla para el evento seleccionado y pulse **[!UICONTROL Listo]** para guardar la regla.

