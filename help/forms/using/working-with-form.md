---
title: Trabajar con un formulario
seo-title: Working with a Form
description: Ver y actualizar el formulario asociado a una tarea o punto de inicio en la aplicación de AEM Forms
seo-description: View and update the form associated with a task or Startpoint in the AEM Forms app
uuid: 7481ca5c-a2c0-4697-9008-1e51bce2012e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 8a5e038e-b39a-41de-88a0-47642e5bd5bf
exl-id: adff5339-e026-4924-a401-f249f37fc6e6
source-git-commit: eb71119474f03a969a721c792b6f1ac330f9dbf3
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 97%

---

# Trabajar con un formulario {#working-with-a-form}

Si un formulario está habilitado para la sincronización en la aplicación de Forms, este se descarga y puede trabajar con él directamente.

Los formularios se descargan en la aplicación y están disponibles sin conexión. Por ejemplo, ejecuta una empresa bancaria y un cliente rellena una solicitud en su sitio. La solicitud es un formulario adaptable que acepta información de sus clientes y la almacena para revisarla. El administrador revisa el formulario y crea un formulario de verificación en la instancia de autor de AEM. El administrador habilita la sincronización del formulario con la aplicación de AEM Forms. Si el formulario de verificación está disponible en la aplicación de AEM Forms, su agente de campo puede utilizar un dispositivo móvil para comprobar los detalles del cliente. El dispositivo móvil se sincroniza con el servidor y el formulario de verificación se carga en la aplicación. Su agente de campo puede visitar a su cliente, comprobar los detalles, guardar datos como borrador o enviar el formulario de verificación. El formulario se sincroniza con el servidor cada vez que la aplicación está en línea.

Para sincronizar su formulario en la aplicación de AEM Forms:

1. En la instancia de autor, seleccione un formulario y haga clic en **Ver propiedades**.
1. En la página Propiedades, haga clic en **Avanzadas**.
1. En Avanzadas, habilite la opción: **Sincronizar con la aplicación de AEM Forms** y pulse **Guardar**.

Para sincronizar varios formularios, en la instancia de autor, seleccione varios formularios en el administrador de formularios y pulse **Sincronizar con la aplicación de AEM Forms**. Cuando se publica el formulario, la aplicación de AEM Forms puede conectarse al servidor de publicación y recuperar los formularios.

Si su aplicación AFA Android (aplicación de AEM Forms) no se puede sincronizar, realice los siguientes pasos para solucionar el problema de sincronización:

1. Vaya a la **https://[server]:[puerto]/system/console/configMgr**.
1. Busque el **[!UICONTROL Controlador de autenticación de token de Adobe Granite]** y haga clic en **[!UICONTROL Editar]**.
1. Seleccione la opción **[!UICONTROL Ninguno]** en el menú desplegable del atributo **[!UICONTROL Atributo SameSite para la cookie del token de inicio de sesión]**.
1. Haga clic en **[!UICONTROL Guardar]**.

![Sincronizar imagen con la aplicación de AFA Android](/help/forms/using/assets/afaandroid.png)

>[!NOTE]
>
>Formularios admitidos:
>
>* Formularios adaptables (sin carga diferida)
>* Mobile Forms
>
>Los archivos adjuntos de nivel de formulario no son compatibles con los formularios adaptables recuperados en la aplicación de AEM Forms sincronizados con el servidor OSGi de AEM Forms. Los usuarios pueden adjuntar archivos en un campo si el autor ha habilitado los archivos adjuntos de nivel de campo en el momento de crear el formulario.


**Para abrir y actualizar un formulario**

1. Para abrir un formulario, pulse el botón **[!UICONTROL Formulario]** en la pantalla de inicio.
1. Puede actualizar los campos del formulario, agregar archivos adjuntos, guardar como borrador y enviarlo.
