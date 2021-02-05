---
title: Configuración de la caché de formularios adaptables
seo-title: Configuración de la caché de formularios adaptables
description: 'La caché de formularios adaptables está diseñada específicamente para formularios y documentos adaptables. Almacena en caché formularios adaptables y documentos adaptables con el objetivo de reducir el tiempo necesario para presentar una forma adaptable o un documento en el cliente. '
seo-description: 'La caché de formularios adaptables está diseñada específicamente para formularios y documentos adaptables. Almacena en caché formularios adaptables y documentos adaptables con el objetivo de reducir el tiempo necesario para presentar una forma adaptable o un documento en el cliente. '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
translation-type: tm+mt
source-git-commit: 2d54d115529126162c92e9943a188d05159535f9
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 1%

---


# Configurar la caché de formularios adaptables {#configure-adaptive-forms-cache}

Una caché es un mecanismo para reducir los tiempos de acceso a los datos, reducir la latencia y mejorar las velocidades de entrada y salida (E/S). La caché de formularios adaptables almacena solo el contenido HTML y la estructura JSON de un formulario adaptable sin guardar datos precargados. Ayuda a reducir el tiempo necesario para procesar un formulario adaptable en el cliente. Está diseñado específicamente para formularios adaptables.

## Configurar la caché de formularios adaptables en instancias de creación y publicación {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Vaya a AEM administrador de configuración de consola web en `https://[server]:[port]/system/console/configMgr`.
1. Haga clic en **[!UICONTROL Configuración del Canal Web de comunicación interactiva y formulario adaptable]** para editar sus valores de configuración.
1. En el cuadro de diálogo [!UICONTROL editar valores de configuración], especifique el número máximo de formularios o documentos que una instancia del servidor AEM [!DNL Forms] puede almacenar en caché en el campo **[!UICONTROL Número de Forms adaptable]**. El valor predeterminado es 100.

   >[!NOTE]
   >
   >Para deshabilitar la caché, establezca el valor en el campo Número de Forms adaptable en **0**. La caché se restablece y todos los formularios y documentos se eliminan de la caché cuando se deshabilita o cambia la configuración de la caché.

   ![Cuadro de diálogo de configuración para la caché HTML de formularios adaptables](assets/cache-configuration-edit.png)

1. Haga clic en **[!UICONTROL Guardar]** para guardar la configuración.

El entorno está configurado para utilizar formularios adaptables de caché y recursos relacionados.


## (Opcional) Configure la caché de formularios adaptables en el despachante {#configure-the-cache}

También puede configurar el procesamiento en caché de formularios adaptables en el despachante para un aumento adicional del rendimiento.

### Requisitos previos {#pre-requisites}

* Habilite la opción [combinando o prefiriendo datos en el cliente](prepopulate-adaptive-form-fields.md#prefill-at-client). Ayuda a combinar datos únicos para cada instancia de un formulario precumplimentado.

### Consideraciones para almacenar en caché formularios adaptables en un despachante {#considerations}

* Cuando utilice la caché de formularios adaptables, utilice la AEM [!DNL Dispatcher] para almacenar en caché las bibliotecas de cliente (CSS y JavaScript) de un formulario adaptable.
* Al desarrollar componentes personalizados, en el servidor utilizado para el desarrollo, mantenga deshabilitada la caché de formularios adaptables.
* Las direcciones URL sin extensión no se almacenan en caché. Por ejemplo, la dirección URL con patrón`/content/forms/[folder-structure]/[form-name].html` se almacena en caché y el almacenamiento en caché omite las direcciones URL con patrón `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Por lo tanto, utilice direcciones URL con extensiones para aprovechar las ventajas del almacenamiento en caché.
* Consideraciones para formularios adaptables localizados:
   * Utilice el formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar una versión localizada de un formulario adaptable en lugar de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [Deshabilite el uso de ](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) localizaciones de explorador para direcciones URL con formato  `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Cuando se utiliza Formato de URL `http://host:port/content/forms/af/<adaptivefName>.html` y **[!UICONTROL Usar configuración regional del explorador]** en el administrador de configuración, se muestra la versión no localizada del formulario adaptable. El idioma no localizado es el idioma utilizado al desarrollar el formulario adaptable. La configuración regional configurada para el explorador (configuración regional del explorador) no se tiene en cuenta y se proporciona una versión no localizada del formulario adaptable.
   * Cuando se utiliza Formato de URL `http://host:port/content/forms/af/<adaptivefName>.html` y **[!UICONTROL Usar configuración regional del explorador]** en el administrador de configuración está habilitado, se muestra una versión localizada del formulario adaptable, si está disponible. El idioma del formulario adaptable localizado se basa en la configuración regional configurada para el explorador (configuración regional del explorador). Puede llevar a [almacenar en caché sólo la primera instancia de un formulario adaptable]. Para evitar que el problema se produzca en su instancia, consulte [solución de problemas](#only-first-insatnce-of-adptive-forms-is-cached).

### Habilitar la caché en el despachante

Siga los pasos que se indican a continuación para habilitar y configurar la caché de formularios adaptables en el despachante:

1. Abra la siguiente URL para cada instancia de publicación de su entorno y [habilite el agente de vaciado para las instancias de publicación de su entorno](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance):
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Añada lo siguiente en el archivo](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files) dispatcher.any:

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

   Al agregar lo anterior:

   * Un formulario adaptable permanece en la caché hasta que no se publica una versión actualizada del formulario.

   * Cuando se publica una versión más reciente del recurso al que se hace referencia en un formulario adaptable, los formularios adaptables afectados se invalidan automáticamente. Existen algunas excepciones a la invalidación automática de los recursos a los que se hace referencia. Para ver la solución alternativa a las excepciones, consulte la sección [solución de problemas](#troubleshooting).
1. [Añada el siguiente archivo](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache) de reglas dispatcher.any o custom rules. Excluye las direcciones URL que no admiten el almacenamiento en caché. Por ejemplo, Comunicación interactiva.

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

1. [Añada los siguientes parámetros en la lista](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters) de parámetros de URL omitidos:

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

El entorno de AEM está configurado para almacenar en caché formularios adaptables. Almacena en caché todos los tipos de formularios adaptables. Si necesita comprobar los permisos de acceso de los usuarios para una página antes de entregar la página en caché, consulte [almacenamiento en caché de contenido seguro](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/permissions-cache.html).

## Solución de problemas {#troubleshooting}

### Algunos formularios adaptables que contienen imágenes o vídeos no se invalidan automáticamente desde la caché del despachante {#videos-or-images-not-auto-invalidated}

#### Problema {#issue1}

Al seleccionar y agregar imágenes o vídeos mediante el navegador de recursos a un formulario adaptable y estas imágenes y vídeos se editan en el editor de recursos, los formularios adaptables que contengan dichas imágenes no se invalidan automáticamente desde la caché del despachante.

#### Solución {#Solution1}

Después de publicar las imágenes y el vídeo, anule explícitamente la publicación y publique los formularios adaptables que hacen referencia a estos recursos.

### Solo se almacena en caché la primera instancia de un formulario adaptable {#only-first-instance-of-adaptive-forms-is-cached}

#### Problema {#issue3}

Cuando la dirección URL del formulario adaptable no tiene información de localización y **[!UICONTROL Usar configuración regional del explorador]** en el administrador de configuración está activada, se proporciona una versión localizada del formulario adaptable y solo se almacena en caché la primera instancia del formulario adaptable y se entrega a todos los usuarios subsiguientes.

#### Solución {#Solution3}

Siga los pasos siguientes para resolver el problema:

1. Abra conf.d/httpd-dispatcher.conf o cualquier otro archivo de configuración configurado para cargarse durante la ejecución.

1. Añada el siguiente código en el archivo y guárdelo. Es un código de muestra modificarlo para adaptarlo a su entorno.

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
