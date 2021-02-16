---
title: Uso de un formulario
seo-title: Uso de un formulario
description: Vista y actualización del formulario asociado a una tarea o un punto de inicio en la aplicación de AEM Forms
seo-description: Vista y actualización del formulario asociado a una tarea o un punto de inicio en la aplicación de AEM Forms
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---


# Uso de un formulario {#working-with-a-form}

Si un formulario está habilitado para la sincronización en la aplicación de formularios, se descarga y puede trabajar con él directamente.

Los formularios se descargan en la aplicación y están disponibles sin conexión. Por ejemplo: está ejecutando una empresa bancaria y un cliente rellena una aplicación en el sitio. La aplicación es un formulario adaptable que acepta información de sus clientes y la almacena para su revisión. El administrador revisa el formulario y crea un formulario de verificación en AEM instancia de autor. El administrador habilita la sincronización del formulario con la aplicación de AEM Forms. Si el formulario de verificación está disponible en la aplicación de AEM Forms, el agente de campo puede utilizar un dispositivo móvil para comprobar los detalles del cliente. El dispositivo móvil se sincroniza con el servidor y el formulario de verificación se carga en la aplicación. El agente de campo puede visitar al cliente, verificar los detalles, guardar los datos como borrador o enviar el formulario de verificación. El formulario se sincroniza con el servidor cada vez que la aplicación está en línea.

Para sincronizar el formulario en la aplicación de AEM Forms:

1. En la instancia de autor, seleccione un formulario y haga clic en **Propiedades de la Vista**.
1. En la página de propiedades, haga clic en **Avanzado.**
1. En Avanzadas, active la opción: **Sincronice con la aplicación de AEM Forms** y toque **Guardar**.

Para sincronizar varios formularios, en la instancia de creación, seleccione varios formularios en el administrador de formularios y toque **Sincronizar con la aplicación de AEM Forms**. Cuando se publica el formulario, la aplicación de AEM Forms se puede conectar al servidor de publicación y recuperar los formularios.

>[!NOTE]
>
>Formularios admitidos:
>
>* Formularios adaptables (sin carga diferida)
>* Formularios móviles

>
>
Los archivos adjuntos de nivel de formulario no se admiten en los formularios adaptables recuperados en la aplicación de AEM Forms sincronizados con el servidor OSGi de AEM Forms. Los usuarios pueden adjuntar archivos en un campo si el autor ha habilitado los datos adjuntos de nivel de campo en el momento de crear el formulario.

**Para abrir y actualizar un formulario**

1. Para abrir un formulario, toque el formulario en la pantalla de inicio.
1. Puede actualizar los campos del formulario, agregar archivos adjuntos, guardarlos como borrador y enviarlos.
