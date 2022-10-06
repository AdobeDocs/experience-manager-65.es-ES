---
title: Configuración de la caché de formularios adaptables
seo-title: Configure adaptive forms cache
description: La caché de formularios adaptables está diseñada específicamente para formularios y documentos adaptables. Almacena en caché formularios adaptables y documentos adaptables con el objetivo de reducir el tiempo necesario para procesar un formulario o documento adaptable en el cliente.
seo-description: The adaptive forms cache is designed specifically for adaptive forms and documents. It caches adaptive forms and adaptive documents with the objective of reducing the time required to render an adaptive form or document on the client.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
role: Admin
exl-id: 153986f0-b6ff-4278-8bb6-70c320a4e539
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 36%

---

# Configuración de la caché de formularios adaptables {#configure-adaptive-forms-cache}

Una caché es un mecanismo para acortar los tiempos de acceso a los datos, reducir la latencia y mejorar las velocidades de entrada y salida (E/S). La caché de formularios adaptables almacena únicamente el contenido del HTML y la estructura JSON de un formulario adaptable sin guardar ningún dato prerellenado. Ayuda a reducir el tiempo necesario para procesar un formulario adaptable en el cliente. Está diseñado específicamente para formularios adaptables.

## Configuración de la caché de formularios adaptables en las instancias de autor y publicación {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Vaya al Administrador de configuración de la consola web de AEM en `https://[server]:[port]/system/console/configMgr`.
1. Haga clic en **[!UICONTROL Configuración del canal web de comunicaciones interactivas y formularios adaptables]** para editar sus valores de configuración.
1. En el cuadro de diálogo [!UICONTROL Editar valores de configuración], especifique el número máximo de formularios o documentos que una instancia del servidor de AEM [!DNL Forms] puede almacenar en caché en el campo **[!UICONTROL Número de formularios adaptables]**. El valor predeterminado es 100.

   >[!NOTE]
   >
   >Para desactivar la caché, establezca el valor del campo Número de formularios adaptables en **0**. La caché se restablece y todos los formularios y documentos se eliminan de ella cuando se desactiva o cambia su configuración.

   ![Cuadro de diálogo de configuración para la caché del HTML de formularios adaptables](assets/cache-configuration-edit.png)

1. Haga clic en **[!UICONTROL Guardar]** para guardar la configuración.

El entorno está configurado para utilizar formularios adaptables de caché y recursos relacionados.


## (Opcional) Configuración de la caché de formularios adaptables en Dispatcher {#configure-the-cache}

También puede configurar el almacenamiento en caché de formularios adaptables en Dispatcher para mejorar el rendimiento.

### Requisitos previos {#pre-requisites}

* Active la opción [Combinar o prerrellenar los datos en el cliente](prepopulate-adaptive-form-fields.md#prefill-at-client). Esto ayuda a combinar los datos únicos de cada instancia del formulario prerrellenado.

### Consideraciones para almacenar en caché formularios adaptables en un despachante {#considerations}

* Cuando utilice la caché de formularios adaptables, utilice el AEM [!DNL Dispatcher] para almacenar en caché las bibliotecas de cliente (CSS y JavaScript) de un formulario adaptable.
* Durante el desarrollo de componentes personalizados, en el servidor utilizado para el desarrollo, mantenga deshabilitada la caché de formularios adaptables.
* Las URL sin extensión no se almacenan en caché. Por ejemplo, las URL con el patrón `/content/forms/[folder-structure]/[form-name].html` se almacenan en caché, y el almacenamiento en caché ignora las URL con el patrón `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Por lo tanto, utilice URL con extensiones para aprovechar las ventajas del almacenamiento en caché.
* Consideraciones para formularios adaptables localizados:
   * Usar formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar una versión localizada de un formulario adaptable en lugar de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [Deshabilite el uso de la configuración regional del explorador ](supporting-new-language-localization.md#how-localization-of-adaptive-form-works)para URL con el formato `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Cuando se usa el formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`y **[!UICONTROL Usar configuración regional del explorador]** en configuration manager está desactivado, se proporciona la versión no localizada del formulario adaptable. El idioma no localizado es el idioma utilizado al desarrollar el formulario adaptable. No se tiene en cuenta la configuración regional configurada para el explorador (configuración regional del explorador) y se proporciona una versión no localizada del formulario adaptable.
   * Cuando se usa el formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`y **[!UICONTROL Usar configuración regional del explorador]** en configuration manager está habilitado, se proporciona una versión localizada del formulario adaptable, si está disponible. El idioma del formulario adaptable localizado se basa en la configuración regional configurada para el explorador (configuración regional del explorador). Puede llevar a [almacenamiento en caché solo primera instancia de un formulario adaptable]. Para evitar que este problema se produzca en la instancia, consulte [Solución de problemas](#only-first-insatnce-of-adptive-forms-is-cached).

### Habilitar el almacenamiento en caché en Dispatcher

Siga los pasos que se indican a continuación para habilitar y configurar el almacenamiento en caché de los formularios adaptables en Dispatcher:

1. Abra la siguiente URL para cada instancia de publicación de su entorno y [habilitar el agente de vaciado para publicar instancias de su entorno](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance):
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Agregue lo siguiente al archivo dispatcher.any](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files):

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   Cuando haya agregado lo anterior:

   * Un formulario adaptable permanece en la caché hasta que no se publique una versión actualizada del formulario.

   * Cuando se publica una versión más reciente del recurso al que se hace referencia en un formulario adaptable, los formularios adaptables afectados se invalidan automáticamente. Existen algunas excepciones a la hora de invalidar automáticamente los recursos a los que se hace referencia. Para obtener más información sobre las excepciones, consulte la sección [Solución de problemas](#troubleshooting).
1. [Añada las siguientes reglas: dispatcher.any o un archivo de reglas personalizadas](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache). Esto excluirá las URL que no admitan el almacenamiento en caché; por ejemplo, comunicaciones interactivas.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [Añada los siguientes parámetros a la lista de los parámetros de URL ignorados](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

El entorno de AEM está configurado para almacenar en caché los formularios adaptables. Almacena en caché todos los tipos de formularios adaptables. Si tiene que comprobar los permisos de acceso de los usuarios de una página antes de enviar la página almacenada en caché, consulte [Almacenar contenido protegido en caché](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/permissions-cache.html).

## Solución de problemas {#troubleshooting}

### Algunos formularios adaptables que contienen imágenes o vídeos no se invalidan automáticamente desde la caché de Dispatcher {#videos-or-images-not-auto-invalidated}

#### Problema {#issue1}

Cuando selecciona y añade imágenes o vídeos a través del navegador de recursos a un formulario adaptable y estas imágenes y vídeos se editan en el editor de Assets, los formularios adaptables que contienen dichas imágenes no se invalidan automáticamente desde la caché del distribuidor.

#### Solución {#Solution1}

Después de publicar las imágenes y el vídeo, cancele la publicación y los formularios adaptables que hacen referencia a estos recursos de forma explícita.

### Solo se almacena en caché la primera instancia de un formulario adaptable {#only-first-instance-of-adaptive-forms-is-cached}

#### Problema {#issue3}

Cuando la dirección URL del formulario adaptable no tiene información de localización, y **[!UICONTROL Usar configuración regional del explorador]** en configuration manager está habilitado, se proporciona una versión localizada del formulario adaptable y solo la primera instancia del formulario adaptable se almacena en caché y se entrega a todos los usuarios subsiguientes.

#### Solución {#Solution3}

Siga estos pasos para resolver el problema:

1. Abra conf.d/httpd-dispatcher.conf o cualquier otro archivo de configuración configurado para cargarse durante la ejecución.

1. Agregue el siguiente código al archivo y guárdelo. Es un código de ejemplo, puede modificarlo para adaptarlo a su entorno.

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
