---
title: 'Sitios AEM: preparación para RGPD'
seo-title: 'Sitios AEM: preparación para RGPD'
description: Obtenga información sobre la preparación para el RGPD en los sitios de AEM.
seo-description: Obtenga información sobre la preparación para el RGPD en los sitios de AEM.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# Sitios AEM: preparación para RGPD{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones que figuran a continuación, pero los detalles abarcados son aplicables a todas las normas de protección de datos y privacidad; como el RGPD, la CCPA, etc.

El Reglamento general de protección de datos de la Unión Europea sobre derechos de privacidad de datos entrará en vigor en mayo de 2018.

AEM Sites está preparado para ayudar a los clientes a cumplir sus obligaciones de cumplimiento de GDPR. Esta página guía a los clientes a través de los procedimientos para gestionar solicitudes GDPR en sitios AEM. Describe la ubicación de los datos privados almacenados y cómo eliminarlos manualmente o con código.

Para obtener más información, consulte la página del [RGPD en el Centro](https://www.adobe.com/privacy/general-data-protection-regulation.html)de privacidad de Adobe.

>[!NOTE]
>
>Consulte Preparación para [AEM GDPR](/help/managing/data-protection-and-privacy.md) para obtener más información.

## Author Server {#author-server}

Las cuentas de usuario y el contenido UGC en el servidor de creación se tratan en la documentación [del RGPD de la](/help/managing/data-protection-and-privacy.md)plataforma.

## Servidor de publicación {#publish-server}

Las cuentas de usuario utilizadas para autenticar a los visitantes en el sitio y el contenido UGC en el servidor de publicación se tratan en la documentación [de GDPR de la](/help/managing/data-protection-and-privacy.md)plataforma.

De forma predeterminada, los componentes de AEM Sites no almacenan los datos de formulario introducidos por los visitantes en el servidor de publicación. Se recomienda reenviar los datos a un sistema de terceros o a Adobe Campaign para un procesamiento posterior.

## Inclusión/exclusión {#opt-in-opt-out}

AEM cuenta con un servicio [de exclusión de](/help/sites-developing/cookie-optout.md) cookies que se puede utilizar para administrar la inclusión y la exclusión de los usuarios.

## Perspectivas mejoradas de Analytics {#enhanced-insights-by-analytics}

AEM Sites incluye una integración opcional con Perspectivas mejoradas de Analytics, que utiliza funciones dentro del servicio a petición de Adobe Analytics.

Para obtener más información sobre la administración de solicitudes de asunto de datos GDPR relacionadas con Adobe Analytics, consulte [Adobe Analytics y GDPR](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/).

## Personalización mejorada por Target {#enhanced-personalization-by-target}

AEM Sites incluye una integración opcional con Personalización mejorada por Target que utiliza funciones dentro del servicio a petición de Adobe Target.

Para obtener más información sobre la administración de solicitudes de datos del RGPD relacionadas con Adobe Target, consulte [Adobe Target - Privacy and General Data Protection Regulation](https://marketing.adobe.com/resources/help/en_US/target/target/privacy-and-general-data-protection-regulation.html).

## ContextHub {#contexthub}

AEM proporciona una capa de datos opcional con [ContextHub](/help/sites-developing/contexthub.md). Esto mantiene los datos específicos del visitante en el explorador, para utilizarlos en la personalización basada en reglas.

De forma predeterminada, los datos de visitante no se almacenan en AEM; AEM envía reglas a la capa de datos para tomar decisiones de personalización en el navegador.

>[!NOTE]
>
>Antes de Adobe CQ 5.6, ClientContext (una versión anterior de ContextHub) enviaba los datos al servidor, pero no los almacenaba.
>
>Adobe CQ 5.5 y versiones anteriores ahora son EOL y no están cubiertos por esta documentación.

### Implementación de la inclusión/exclusión {#implementing-opt-in-opt-out}

El propietario del sitio debe implementar un componente de exclusión según las siguientes directrices.

Estas directrices implementan la inclusión como opción predeterminada. Por lo tanto, el visitante de un sitio web debe aceptar claramente antes de que cualquier dato personal se almacene en la persistencia (del lado del cliente) del navegador.

* El componente de exclusión debe incluirse cada vez que se incluya el componente ContextHub.
* Los términos y condiciones que se relacionan con el RGPD para el sitio web deben mostrarse al visitante del sitio web, permitiéndole:

   * aceptar
   * rechazar
   * cambiar la opción anterior

* Si un visitante del sitio acepta los términos y condiciones del sitio, se debe eliminar la cookie de exclusión de ContextHub:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* Si un visitante del sitio no acepta los términos y condiciones del sitio, se debe configurar la cookie de exclusión de ContextHub:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* Para comprobar si ContextHub se está ejecutando en modo de exclusión, se debe realizar la siguiente llamada en la consola del explorador:

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### Vista previa de la persistencia de ContextHub {#previewing-persistence-of-contexthub}

Para obtener una vista previa de la persistencia utilizada por ContextHub, un usuario puede:

* Utilice la consola del navegador; por ejemplo:

   * Chrome:

      * Abra Herramientas para desarrolladores > Aplicación > Almacenamiento:

         * Almacenamiento local > (sitio web) > ContextHubPersistence
         * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
         * Cookies > (sitio web) > SessionPersistence
   * Firefox:

      * Abra Herramientas para desarrolladores > Almacenamiento:

         * Almacenamiento local > (sitio web) > ContextHubPersistence
         * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
         * Cookies > (sitio web) > SessionPersistence
   * Safari:

      * Abra Preferencias > Avanzadas > Mostrar menú Desarrollar en la barra de menús
      * Abra Desarrollar > Mostrar consola de JavaScript

         * Consola > Almacenamiento > Almacenamiento local > (sitio web) > ContextHubPersistence
         * Consola > Almacenamiento > Almacenamiento de sesión > (sitio web) > ContextHubPersistence
         * Consola > Almacenamiento > Cookies > (sitio web) > ContextHubPersistence
   * Internet Explorer:

      * Abrir Herramientas para desarrolladores > Consola

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* Utilice la API de ContextHub, en la consola del navegador:

   * ContextHub proporciona las siguientes capas de persistencia de datos:

      * ContextHub.Utils.Persistence.Modes.LOCAL (predeterminado)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW
      El almacén de ContextHub define qué capa de persistencia se utilizará, por lo que se debe comprobar el estado actual de la persistencia en todas las capas.


Por ejemplo, para ver los datos almacenados en localStorage:

Para obtener una vista previa de la persistencia utilizada por ContextHub, un usuario puede:

* Utilice la consola del explorador:

   * Chrome: abra Herramientas para desarrolladores > Aplicación > Almacenamiento:

      * Almacenamiento local > (sitio web) > ContextHubPersistence
      * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
      * Cookies > (sitio web) > SessionPersistence
   * Firefox: abra Herramientas para desarrolladores > Almacenamiento:

      * Almacenamiento local > (sitio web) > ContextHubPersistence
      * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
      * Cookies > (sitio web) > SessionPersistence


* Utilice la API de ContextHub, en la consola del navegador:

   * ContextHub proporciona las siguientes capas de persistencia de datos:

      * ContextHub.Utils.Persistence.Modes.LOCAL (predeterminado)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW
      El almacén de ContextHub define qué capa de persistencia se utilizará, por lo que se debe comprobar el estado actual de la persistencia en todas las capas.


Por ejemplo, para ver los datos almacenados en localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Borrado de la persistencia de ContextHub {#clearing-persistence-of-contexthub}

Para borrar la persistencia de ContextHub:

* Para borrar la persistencia de los almacenes cargados actualmente:

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* Para borrar una capa de persistencia específica; por ejemplo, sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* Para borrar todas las capas de persistencia de ContextHub, se debe llamar al código adecuado para todas las capas:

   * ContextHub.Utils.Persistence.Modes.LOCAL (predeterminado)
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW

