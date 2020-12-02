---
title: AEM Sites - Preparación para RGPD
seo-title: AEM Sites - Preparación para RGPD
description: Conozca los detalles de la preparación para el RGPD para AEM Sites.
seo-description: Conozca los detalles de la preparación para el RGPD para AEM Sites.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---


# AEM Sites - Preparación para RGPD{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones que figuran a continuación, pero los detalles abarcados son aplicables a todas las normas de protección de datos y privacidad; como el RGPD, la CCPA, etc.

El Reglamento general de protección de datos de la Unión Europea sobre derechos de privacidad de datos entrará en vigor en mayo de 2018.

AEM Sites está preparado para ayudar a los clientes con sus obligaciones de cumplimiento de RGPD. Esta página guía a los clientes a través de los procedimientos para gestionar solicitudes de RGPD en AEM Sites. Describe la ubicación de los datos privados almacenados y cómo eliminarlos manualmente o con código.

Para obtener más información, consulte la página [RGPD en el Centro de privacidad de Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte [Preparación para el RGPD AEM](/help/managing/data-protection-and-privacy.md) para obtener más información.

## Author Server {#author-server}

Las cuentas de usuario y el contenido UGC en el servidor de creación se tratan en la [documentación del RGPD de la plataforma](/help/managing/data-protection-and-privacy.md).

## Servidor de publicación {#publish-server}

Las cuentas de usuario utilizadas para autenticar visitantes en el sitio y el contenido de UGC en el servidor de publicación se tratan en la [documentación de GDPR de la plataforma](/help/managing/data-protection-and-privacy.md).

De forma predeterminada, los componentes de AEM Sites no almacenan datos de formulario introducidos por visitantes en el servidor de publicación. Se recomienda reenviar los datos a un sistema de terceros o a Adobe Campaign para un procesamiento posterior.

## Inclusión/exclusión {#opt-in-opt-out}

AEM tiene un [servicio de exclusión de cookies](/help/sites-developing/cookie-optout.md) que puede utilizarse para administrar la inclusión/exclusión para los usuarios.

## Perspectivas mejoradas de Analytics {#enhanced-insights-by-analytics}

AEM Sites incluye una integración opcional con Perspectivas mejoradas de Analytics, que utiliza la funcionalidad del servicio a petición de Adobe Analytics.

Para obtener más información sobre la administración de las solicitudes de temas de datos del RGPD relacionadas con Adobe Analytics, consulte [Adobe Analytics y el RGPD](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html).

## Personalización mejorada por Destinatario {#enhanced-personalization-by-target}

AEM Sites incluye una integración opcional con Personalización mejorada por Destinatario que utiliza la funcionalidad dentro del servicio a petición de Adobe Target.

Para obtener más información sobre la administración de solicitudes de datos del RGPD relacionadas con Adobe Target, consulte [Adobe Target - Privacy and General Data Protection Regulation](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html).

## ContextHub {#contexthub}

AEM proporciona una capa de datos opcional con [ContextHub](/help/sites-developing/contexthub.md). Esto mantiene los datos específicos del visitante en el navegador, para utilizarlos en la personalización basada en reglas.

De forma predeterminada, estos datos de visitante no se almacenan en AEM; AEM envía reglas a la capa de datos para tomar decisiones de personalización en el explorador.

>[!NOTE]
>
>Antes de Adobe CQ 5.6, el ClientContext (una versión anterior de ContextHub) enviaba los datos al servidor, pero no los almacenaba.
>
>Adobe CQ 5.5 y versiones anteriores son ahora EOL y no están cubiertos por esta documentación.

### Implementación de la inclusión/exclusión {#implementing-opt-in-opt-out}

El propietario del sitio debe implementar un componente de exclusión según las siguientes directrices.

Estas directrices implementan la inclusión como opción predeterminada. Por lo tanto, un visitante de un sitio web debe estar claramente de acuerdo, antes de que cualquier dato personal se almacene en la persistencia (del lado del cliente) del navegador.

* El componente de exclusión debe incluirse cada vez que se incluya el componente ContextHub.
* Los términos y condiciones que se relacionan con el RGPD para el sitio web deben mostrarse en el visitante del sitio web, permitiéndoles:

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

Para obtener la previsualización de la resistencia utilizada en ContextHub, un usuario puede:

* Utilice la consola del navegador; por ejemplo:

   * Chrome:

      * Abra Herramientas de desarrollador > Aplicación > Almacenamiento:

         * Almacenamiento local > (sitio web) > ContextHubPersistence
         * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
         * Cookies > (sitio web) > SessionPersistence
   * Firefox:

      * Abra Herramientas de desarrollador > Almacenamiento:

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

      El almacén de ContextHub define qué capa de persistencia se utilizará, por lo que se debe comprobar la vista del estado actual de la persistencia.


Por ejemplo, para vista de datos almacenados en localStorage:

Para obtener la previsualización de la resistencia utilizada en ContextHub, un usuario puede:

* Utilice la consola del explorador:

   * Chrome: abra Herramientas para desarrolladores > Aplicación > Almacenamiento:

      * Almacenamiento local > (sitio web) > ContextHubPersistence
      * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
      * Cookies > (sitio web) > SessionPersistence
   * Firefox: abra Herramientas de desarrollador > Almacenamiento:

      * Almacenamiento local > (sitio web) > ContextHubPersistence
      * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
      * Cookies > (sitio web) > SessionPersistence


* Utilice la API de ContextHub, en la consola del navegador:

   * ContextHub proporciona las siguientes capas de persistencia de datos:

      * ContextHub.Utils.Persistence.Modes.LOCAL (predeterminado)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      El almacén de ContextHub define qué capa de persistencia se utilizará, por lo que se debe comprobar la vista del estado actual de la persistencia.


Por ejemplo, para vista de datos almacenados en localStorage:

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

