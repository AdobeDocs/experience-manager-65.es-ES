---
title: Usar CAPTCHA en formularios adaptables
seo-title: Using CAPTCHA in adaptive forms
description: Aprenda a configurar el servicio AEM CAPTCHA o Google reCAPTCHA en formularios adaptables.
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in adaptive forms.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
feature: Adaptive Forms
exl-id: 9b4219b8-d5eb-4099-b205-d98d84e0c249
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 100%

---

# Usar CAPTCHA en formularios adaptables{#using-captcha-in-adaptive-forms}

CAPTCHA (prueba de Turing completamente automática y pública para diferenciar ordenadores de humanos) es un programa que se utiliza comúnmente en transacciones en línea para distinguir entre humanos y programas o bots automatizados. Plantea un desafío y evalúa la respuesta del usuario para determinar si es un humano o un bot que interactúa con el sitio. Evita que el usuario continúe si la prueba falla y ayuda a que las transacciones en línea sean seguras al impedir que los bots publiquen contenido no deseado o con fines malintencionados.

AEM Forms admite CAPTCHA en formularios adaptables. Puede utilizar el servicio reCAPTCHA de Google para implementar CAPTCHA.

>[!NOTE]
>
>* AEM Forms solo admite reCaptcha v2. No existe compatibilidad con ninguna otra versión.
>* CAPTCHA en formularios adaptables no es compatible con el modo sin conexión en la aplicación de AEM Forms.
>


## Configurar el servicio ReCAPTCHA de Google {#google-recaptcha}

Los creadores de formularios pueden utilizar el servicio reCAPTCHA de Google para implementar CAPTCHA en formularios adaptables. Ofrece funcionalidades de CAPTCHA avanzadas para proteger su sitio. Para obtener más información sobre cómo funciona reCAPTCHA, consulte [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![Recaptcha](assets/recaptcha_new.png)

Para implementar el servicio reCAPTCHA en AEM Forms haga lo siguiente:

1. Obtener el [par de claves de la API reCAPTCHA](https://www.google.com/recaptcha/admin) de Google. Incluye una clave de sitio y un secreto.
1. Crear un contenedor de configuración para los servicios en la nube.

   1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
      * Consulte la documentación del [Explorador de configuración](/help/sites-administering/configurations.md) para obtener más información.
   1. Haga lo siguiente para habilitar la carpeta global para configuraciones de nube u omita este paso para crear y configurar otra carpeta para configuraciones de servicios en la nube.

      1. En el Explorador de configuración, seleccione la carpeta **[!UICONTROL global]** y pulse **[!UICONTROL Propiedades]**.

      1. En el cuadro de diálogo Propiedades de configuración, habilite **[!UICONTROL Configuraciones de nube]**.
      1. Pulse **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.
   1. En el Explorador de configuración, pulse **[!UICONTROL Crear]**.
   1. En el cuadro de diálogo Crear configuración, especifique un título para la carpeta y habilite **[!UICONTROL Configuraciones de nube]**.
   1. Pulse **[!UICONTROL Crear]** para crear la carpeta habilitada para las configuraciones del servicio en la nube.


1. Configure el servicio en la nube para reCAPTCHA.

   1. En la instancia de autor de AEM, vaya a ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. Pulse **[!UICONTROL reCAPTCHA]**. Se abre la página de configuración. Seleccione el contenedor de configuración creado en el paso anterior y pulse **[!UICONTROL Crear]**.
   1. Especifique el nombre, la clave del sitio y la clave secreta para el servicio reCAPTCHA y pulse **[!UICONTROL Crear]** para crear la configuración del servicio en la nube.
   1. En el cuadro de diálogo Editar componente, especifique el sitio y las claves secretas obtenidas en el paso 1. Pulse **Guardar configuración** y, a continuación, **Aceptar** para completar la configuración.

   Una vez configurado el servicio reCAPTCHA, estará disponible para su uso en formularios adaptables. Para obtener más información, consulte [Usar CAPTCHA en formularios adaptables](#using-captcha).

## Usar CAPTCHA en formularios adaptables {#using-captcha}

Para usar CAPTCHA en formularios adaptables haga lo siguiente:

1. Abra un formulario adaptable en modo Edición.

   >[!NOTE]
   >
   >Asegúrese de que el contenedor de configuración seleccionado al crear el formulario adaptable contenga el servicio en la nube reCAPTCHA. También puede editar las propiedades del formulario adaptable para cambiar el contenedor de configuración asociado al formulario.

1. Desde el explorador de componentes, arrastre y suelte el componente **Captcha** en el formulario adaptable.

   >[!NOTE]
   >
   >No se puede usar más de un componente Captcha en un formulario adaptable. Además, no se recomienda utilizar CAPTCHA en un panel marcado para la carga lenta o en un fragmento.

   >[!NOTE]
   >
   >Captcha tiene un plazo y caduca en aproximadamente un minuto. Por lo tanto, se recomienda colocar el componente Captcha justo antes del botón Enviar en el formulario adaptable.

1. Seleccione el componente Captcha que ha añadido y pulse ![cmppr](assets/cmppr.png) para editar sus propiedades.
1. Especifique un título para el widget CAPTCHA. El valor predeterminado es **Captcha**. Seleccione **Ocultar título** si no desea que aparezca el título.
1. En el desplegable **Servicio Captcha**, seleccione **reCaptcha** para habilitar el servicio reCAPTCHA si lo configuró como se describe en [Servicio ReCAPTCHA de Google](#google-recaptcha). Seleccione una configuración en la lista desplegable Configuración. Seleccione el tamaño **Normal** o **Compacto** para el widget reCAPTCHA.

   >[!NOTE]
   >
   >No seleccione **[!UICONTROL Predeterminado]** en el menú desplegable del servicio Captcha, ya que el servicio CAPTCHA AEM predeterminado está obsoleto.

1. Guarde las propiedades.

El servicio reCAPTCHA está habilitado en el formulario adaptable. Puede obtener una vista previa del formulario y ver cómo funciona CAPTCHA.

### Mostrar u ocultar el componente CAPTCHA en base a reglas {#show-hide-captcha}

Puede seleccionar mostrar u ocultar el componente CAPTCHA en función de las reglas que aplique en un componente de un formulario adaptable. Pulse el componente, seleccione ![editar reglas](assets/edit-rules-icon.svg) y pulse **[!UICONTROL Crear]** para crear una regla. Para obtener más información sobre la creación de reglas, consulte [Editor de reglas](rule-editor.md).

Por ejemplo, el componente CAPTCHA debe mostrarse en un formulario adaptable solo si el campo Valor de moneda del formulario tiene un valor superior a 25 000.

Pulse **[!UICONTROL Valor de moneda]** en el formulario y cree las siguientes reglas:

![Mostrar u ocultar reglas](assets/rules-show-hide-captcha.png)

### Validar CAPTCHA {#validate-captcha}

Puede validar el CAPTCHA en un formulario adaptable al enviar el formulario o basar la validación CAPTCHA en las acciones y condiciones del usuario.

#### Validar el CAPTCHA al enviar el formulario {#validation-form-submission}

Para validar un CAPTCHA automáticamente al enviar un formulario adaptable:

1. Pulse el componente CAPTCHA y seleccione ![cmppr](assets/configure-icon.svg) para ver las propiedades del componente.
1. En la sección **[!UICONTROL Validar CAPTCHA]**, seleccione **[!UICONTROL Validar el CAPTCHA al enviar el formulario]**.
1. Pulse ![Listo](assets/save_icon.svg) para guardar las propiedades del componente.

#### Validar el CAPTCHA en base a las acciones y condiciones del usuario {#validate-captcha-user-action}

Para validar un CAPTCHA basado en condiciones y acciones del usuario:

1. Pulse el componente CAPTCHA y seleccione ![cmppr](assets/configure-icon.svg) para ver las propiedades del componente.
1. En la sección **[!UICONTROL Validar CAPTCHA]**, seleccione **[!UICONTROL Validar el CAPTCHA en base a una acción del usuario]**.
1. Pulse ![Listo](assets/save_icon.svg) para guardar las propiedades del componente.

[!DNL Experience Manager Forms] ofrece la API `ValidateCAPTCHA` para validar un CAPTCHA con condiciones predefinidas. Puede invocar la API utilizando una acción de envío personalizada o definiendo reglas sobre los componentes de un formulario adaptable.

El siguiente es un ejemplo de un API `ValidateCAPTCHA` para validar un CAPTCHA con condiciones predefinidas:

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
    	GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

El ejemplo significa que la API `ValidateCAPTCHA` valida el CAPTCHA en el formulario solo si el número de dígitos en el cuadro numérico especificado por el usuario mientras rellena el formulario es mayor de 5.

**Opción 1: Usar la API [!DNL Experience Manager Forms] ValidateCAPTCHA para validar el CAPTCHA mediante una acción de envío personalizada**

Siga estos pasos para usar la API `ValidateCAPTCHA` para validar el CAPTCHA con una acción de envío personalizada:

1. Añada el script que incluya la API `ValidateCAPTCHA` para la acción de envío personalizada. Para obtener más información acerca de las acciones de envío personalizadas, consulte [Crear una acción de envío personalizada para formularios adaptables](custom-submit-action-form.md).
1. Seleccione el nombre de la acción de envío personalizada en la lista desplegable **[!UICONTROL Enviar acción]** en las propiedades de **[!UICONTROL Envío]** de un formulario adaptable.
1. Pulse **[!UICONTROL Enviar]**. El CAPTCHA se valida según las condiciones definidas en la API `ValidateCAPTCHA` de la acción de envío personalizada.

**Opción 2: Usar la API [!DNL Experience Manager Forms] ValidateCAPTCHA para validar el CAPTCHA en una acción del usuario antes de enviar el formulario**

También puede invocar la API `ValidateCAPTCHA` al aplicar reglas en un componente de un formulario adaptable.

Por ejemplo, añade un botón **[!UICONTROL Validar CAPTCHA]** en un formulario adaptable y crea una regla para invocar un servicio haciendo clic en un botón.

La siguiente imagen ilustra cómo puede invocar un servicio al hacer clic en un botón **[!UICONTROL Validar CAPTCHA]**:

![Validar CAPTCHA](assets/captcha-validation1.gif)

Puede invocar el servlet personalizado que incluye la API `ValidateCAPTCHA` mediante el editor de reglas y habilitar o deshabilitar el botón de envío del formulario adaptable en base al resultado de validación.

Del mismo modo, puede utilizar el editor de reglas para incluir un método personalizado para validar el CAPTCHA en un formulario adaptable.

### Añadir servicios CAPTCHA personalizados {#add-custom-captcha-service}

[!DNL Experience Manager Forms] Ofrece reCAPTCHA como servicio CAPTCHA. Con todo, puede agregar un servicio personalizado para que se muestre en la lista desplegable **[!UICONTROL Servicio CAPTCHA]**.

A continuación se muestra un ejemplo de implementación de la interfaz para agregar un servicio CAPTCHA adicional al formulario adaptable:

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` hace referencia a la ruta de recurso del componente CAPTCHA en el repositorio de Sling. Utilice esta propiedad para incluir detalles específicos del componente CAPTCHA. Por ejemplo, `captchaPropertyNodePath` incluye información para la configuración de nube reCAPTCHA configurada en el componente CAPTCHA. La información de configuración de nube ofrece la configuración **[!UICONTROL Clave del sitio]** y **[!UICONTROL Clave secreta]** para implementar el servicio reCAPTCHA.

`userResponseToken` hace referencia a la `g_recaptcha_response` que se genera después de resolver un CAPTCHA en un formulario.
