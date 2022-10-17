---
title: Uso de un formulario
seo-title: Working with a Form
description: Ver y actualizar el formulario asociado a una tarea o punto de inicio en la aplicación AEM Forms
seo-description: View and update the form associated with a task or Startpoint in the AEM Forms app
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
source-git-commit: 3c691a9e8673f3229368abbd550982d207eb8ac6
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Uso de un formulario {#working-with-a-form}

Si un formulario está habilitado para la sincronización en la aplicación de formularios, este se descarga y puede trabajar con él directamente.

Los formularios se descargan en la aplicación y están disponibles sin conexión. Por ejemplo, está ejecutando una empresa bancaria y un cliente rellena una aplicación en su sitio. La aplicación es un formulario adaptable que acepta información de sus clientes y la almacena para su revisión. El administrador revisa el formulario y crea un formulario de verificación en AEM instancia de autor. El administrador habilita la sincronización del formulario con la aplicación de AEM Forms. Si el formulario de verificación está disponible en la aplicación de AEM Forms, el agente de campo puede utilizar un dispositivo móvil para comprobar los detalles del cliente. El dispositivo móvil se sincroniza con el servidor y el formulario de verificación se carga en la aplicación. El agente de campo puede visitar al cliente, verificar los detalles, guardar datos como borrador o enviar el formulario de verificación. El formulario se sincroniza con el servidor cada vez que la aplicación está en línea.

Para sincronizar el formulario en la aplicación de AEM Forms:

1. En la instancia de autor, seleccione un formulario y haga clic en **Ver propiedades**.
1. En la página de propiedades, haga clic en **Avanzado.**
1. En Avanzado, active la opción: **Sincronización con la aplicación AEM Forms** y toque **Guardar**.

Para sincronizar varios formularios, en la instancia de autor, seleccione varios formularios en el administrador de formularios y pulse **Sincronización con la aplicación AEM Forms**. Cuando se publica el formulario, la aplicación de AEM Forms puede conectarse al servidor de publicación y recuperar los formularios.

Si la aplicación de AEM de formulario AFA no se puede sincronizar, realice los siguientes pasos para solucionar el problema de sincronización:

1. Vaya a la **https://&#39;[server]:[puerto]&#39;system/console/configMgr**.
1. Busque la variable **[!UICONTROL Controlador de autenticación de token de Granite de Adobe]** y haga clic en **[!UICONTROL Editar]**.
1. Seleccione el **[!UICONTROL Ninguna]** en el menú desplegable de la **[!UICONTROL Atributo SameSite para la cookie de token de inicio de sesión]** atributo.
1. Haga clic en **[!UICONTROL Guardar]**.

![Sincronizar imagen con la aplicación de Android de AFA](/help/forms/using/assets/afaandroid.png)

>[!NOTE]
>
>Formularios admitidos:
>
>* Formularios adaptables (sin carga diferida)
>* Formularios móviles
>
>Los archivos adjuntos de nivel de formulario no son compatibles con los formularios adaptables recuperados en la aplicación de AEM Forms sincronizados con el servidor OSGi de AEM Forms. Los usuarios pueden adjuntar archivos en un campo si el autor ha habilitado los archivos adjuntos de nivel de campo en el momento de crear el formulario.


**Para abrir y actualizar un formulario**

1. Para abrir un formulario, pulse el botón **[!UICONTROL Formulario]** en la pantalla de inicio.
1. Puede actualizar los campos del formulario, agregar archivos adjuntos, guardar como borrador y enviarlo.
