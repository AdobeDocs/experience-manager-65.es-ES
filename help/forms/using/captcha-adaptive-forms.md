---
title: Uso de CAPTCHA en formularios adaptables
seo-title: Uso de CAPTCHA en formularios adaptables
description: Obtenga información sobre cómo configurar el servicio AEM CAPTCHA o Google reCAPTCHA en formularios adaptables.
seo-description: Obtenga información sobre cómo configurar el servicio AEM CAPTCHA o Google reCAPTCHA en formularios adaptables.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
translation-type: tm+mt
source-git-commit: abfb6dced1ffd8d0dd11eaab1e66c78704df543f

---


# Uso de CAPTCHA en formularios adaptables{#using-captcha-in-adaptive-forms}

CAPTCHA (Prueba pública de Turing completamente automatizada para distinguir entre ordenadores y humanos) es un programa comúnmente utilizado en transacciones en línea para distinguir entre humanos y programas o bots automatizados. Plantea un desafío y evalúa la respuesta del usuario para determinar si es un humano o un bot que interactúa con el sitio. Evita que el usuario continúe si la prueba falla y ayuda a garantizar la seguridad de las transacciones en línea evitando que los bots publiquen contenido no deseado o con fines malintencionados.

AEM Forms admite CAPTCHA en formularios adaptables. Puede utilizar el servicio reCAPTCHA de Google para implementar CAPTCHA.

>[!NOTE] {graybox=&quot;true&quot;}
>
>* Los formularios AEM solo admiten reCaptcha v2. No se admite ninguna otra versión.
>* CAPTCHA en formularios adaptables no se admite en modo sin conexión en la aplicación de AEM Forms.
>



## Configurar el servicio ReCAPTCHA por Google {#google-recaptcha}

Los autores de formularios pueden utilizar el servicio reCAPTCHA de Google para implementar CAPTCHA en formularios adaptables. Ofrece capacidades avanzadas de CAPTCHA para proteger su sitio. Para obtener más información sobre cómo funciona reCAPTCHA, consulte [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![Recaptcha](assets/recaptcha_new.png)

Para implementar el servicio reCAPTCHA en AEM Forms:

1. Obtenga el par [de claves de la API de](https://www.google.com/recaptcha/admin) reCAPTCHA de Google. Incluye una clave del sitio y un secreto.
1. Cree un contenedor de configuración para servicios en la nube.

   1. Vaya a **[!UICONTROL Herramientas > General > Navegador]** de configuración.
   1. Haga lo siguiente para habilitar la carpeta global para las configuraciones de nube o omita este paso para crear y configurar otra carpeta para las configuraciones de servicio en la nube.

      1. En el navegador de configuración, seleccione la carpeta **[!UICONTROL global]** y toque **[!UICONTROL Propiedades]**.

      1. En el cuadro de diálogo Propiedades de configuración, habilite Configuraciones **[!UICONTROL de nube]**.
      1. Toque **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.
   1. En el navegador de configuración, toque **[!UICONTROL Crear]**.
   1. En el cuadro de diálogo Crear configuración, especifique un título para la carpeta y habilite Configuraciones **[!UICONTROL de nube]**.
   1. Toque **[!UICONTROL Crear]** para crear la carpeta habilitada para las configuraciones de servicio en la nube.


1. Configure el servicio en la nube para reCAPTCHA.

   1. En la instancia de creación de AEM, vaya a ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. Toque **[!UICONTROL reCAPTCHA]**. Se abre la página Configuraciones. Seleccione el contenedor de configuración creado en el paso anterior y toque **[!UICONTROL Crear]**.
   1. Especifique Nombre, Clave del sitio y Clave secreta para el servicio reCAPTCHA y toque **[!UICONTROL Crear]** para crear la configuración del servicio en la nube.
   1. En el cuadro de diálogo Editar componente, especifique el sitio y las claves secretas obtenidas en el paso 1. Toque **Guardar configuración** y, a continuación, toque **Aceptar** para completar la configuración.
   Una vez configurado el servicio reCAPTCHA, estará disponible para su uso en formularios adaptables. Para obtener más información, consulte [Uso de CAPTCHA en formularios](#using-captcha)adaptables.

## Utilizar CAPTCHA en formularios adaptables {#using-captcha}

Para utilizar CAPTCHA en formularios adaptables:

1. Abra un formulario adaptable en modo de edición.

   >[!NOTE]
   >
   >Asegúrese de que el contenedor de configuración seleccionado al crear el formulario adaptable contiene el servicio de nube reCAPTCHA. También puede editar las propiedades del formulario adaptable para cambiar el contenedor de configuración asociado al formulario.

1. Desde el navegador de componentes, arrastre y suelte el componente **Captcha** en el formulario adaptable.

   >[!NOTE]
   >
   >No se admite el uso de más de un componente Captcha en un formulario adaptable. Además, no se recomienda utilizar CAPTCHA en un panel marcado para la carga diferida o en un fragmento.

   >[!NOTE]
   >
   >Captcha diferencia el tiempo y caduca en aproximadamente un minuto. Por lo tanto, se recomienda colocar el componente Captcha justo antes del botón Enviar en el formulario adaptable.

1. Seleccione el componente Captcha que ha agregado y toque ![cmppr](assets/cmppr.png) para editar sus propiedades.
1. Especifique un título para la utilidad CAPTCHA. The default value is **Captcha**. Seleccione **Ocultar título** si no desea que aparezca el título.
1. En la lista desplegable del servicio **** Captcha, seleccione **reCaptcha** para habilitar el servicio reCAPTCHA si lo configuró como se describe en el servicio [ReCAPTCHA de Google](#google-recaptcha). Seleccione una configuración en la lista desplegable Configuración. Además, seleccione el tamaño como **Normal** o **Compacto** para la utilidad reCAPTCHA.

   >[!NOTE]
   >
   >No seleccione **[!UICONTROL Predeterminado]** en la lista desplegable Servicio Captcha porque el servicio CAPTCHA AEM predeterminado está obsoleto.

1. Guarde las propiedades.

El servicio reCAPTCHA está habilitado en el formulario adaptable. Puede obtener una vista previa del formulario y ver cómo funciona CAPTCHA.
