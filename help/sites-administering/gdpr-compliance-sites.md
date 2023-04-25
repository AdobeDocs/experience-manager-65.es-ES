---
title: 'AEM Sites: preparación para el RGPD'
seo-title: AEM Sites - GDPR Readiness
description: Obtenga información sobre los detalles de preparación para el RGPD para AEM Sites.
seo-description: Learn about the details of GDPR Readiness for AEM Sites.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
source-git-commit: d8ae63edd71c7d27fe93d24b30fb00a29332658d
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 54%

---

# AEM Sites: preparación para el RGPD{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones siguientes, pero los detalles cubiertos son aplicables a todas las normas de protección de datos y privacidad; como el RGPD, la CCPA, etc.

El Reglamento general de protección de datos de la Unión Europea sobre derechos de privacidad de datos entrará en vigor en mayo de 2018.

AEM Sites está listo para ayudar a los clientes con sus obligaciones de cumplimiento del RGPD. Esta página guía a los clientes a través de los procedimientos para gestionar las solicitudes de RGPD en AEM Sites. Describe la ubicación de los datos privados almacenados y cómo eliminarlos manualmente o mediante programación.

Para obtener más información, consulte [Página del RGPD en el Centro de privacidad de Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte [Preparación AEM RGPD](/help/managing/data-protection-and-privacy.md) para obtener más información.

## Servidor de creación {#author-server}

Las cuentas de usuario y el contenido de UGC en el servidor de creación se tratan en la [Documentación del RGPD de la plataforma](/help/managing/data-protection-and-privacy.md).

## Servidor de publicación {#publish-server}

Las cuentas de usuario utilizadas para autenticar a los visitantes en el sitio y el contenido de UGC en el servidor de publicación se tratan en la sección [Documentación del RGPD de la plataforma](/help/managing/data-protection-and-privacy.md).

De forma predeterminada, los componentes de AEM Sites no almacenan los datos de formulario introducidos por los visitantes en el servidor de publicación. Se recomienda reenviar los datos a un sistema de terceros o a Adobe Campaign para un procesamiento posterior.

## Inclusión/exclusión {#opt-in-opt-out}

AEM tiene un [servicio de exclusión de cookies](/help/sites-developing/cookie-optout.md) que se puede utilizar para administrar la inclusión/exclusión para los usuarios.

## Perspectivas mejoradas de Analytics {#enhanced-insights-by-analytics}

AEM Sites incluye una integración opcional con Perspectivas mejoradas de Analytics que utiliza funcionalidad dentro del servicio bajo demanda de Adobe Analytics.

Para obtener más información sobre la administración de solicitudes de interesados del RGPD relacionadas con Adobe Analytics, consulte [Adobe Analytics y el RGPD](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html).

## Personalización mejorada por Target {#enhanced-personalization-by-target}

AEM Sites incluye una integración opcional con Personalización mejorada de Target que utiliza funcionalidad dentro del servicio bajo demanda de Adobe Target.

Para obtener más información sobre la administración de solicitudes de interesados del RGPD relacionadas con Adobe Target, consulte [Adobe Target: Reglamento general de protección de datos](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en).

## ContextHub {#contexthub}

AEM proporciona una capa de datos opcional con [ContextHub](/help/sites-developing/contexthub.md). Esto mantiene los datos específicos del visitante en el explorador, para usarlos para la personalización basada en reglas.

De forma predeterminada, estos datos de visitante no se almacenan en AEM; AEM envía reglas a la capa de datos para tomar decisiones de personalización en el explorador.

>[!NOTE]
>
>Antes de Adobe CQ 5.6, el ClientContext (una versión anterior de ContextHub) enviaba los datos al servidor, pero no los almacenaba.
>
>Adobe CQ 5.5 y versiones anteriores ahora son EOL y no están cubiertos por esta documentación.

### Implementación de la inclusión/exclusión {#implementing-opt-in-opt-out}

El propietario del sitio debe implementar un componente de exclusión según las siguientes directrices.

Estas directrices implementan la inclusión como predeterminada. Por lo tanto, el visitante de un sitio web debe aceptar claramente antes de que cualquier dato personal se almacene en la persistencia del explorador (del lado del cliente).

* El componente de exclusión debe incluirse cada vez que se incluya el componente ContextHub.
* Los términos y condiciones relacionados con el RGPD para el sitio web deben mostrarse al visitante del sitio web, lo que les permite:

   * Aceptar
   * Rechazar
   * Cambiar su opción anterior

* Si el visitante de un sitio acepta los términos y condiciones del sitio, se debe eliminar la cookie de exclusión de ContextHub:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* Si el visitante de un sitio no acepta los términos y condiciones del sitio, se debe configurar la cookie de exclusión de ContextHub:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* Para comprobar si ContextHub se está ejecutando en modo de exclusión, la siguiente llamada debe realizarse en la consola del explorador:

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### Previsualización de la persistencia de ContextHub {#previewing-persistence-of-contexthub}

Para obtener una vista previa de la persistencia utilizada en ContextHub, un usuario puede:

* Utilizar la consola del explorador; por ejemplo:

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

      * Abra Preferencias > Avanzado > Mostrar el menú Desarrollo en la barra de menús
      * Abra Desarrollo > Mostrar consola de JavaScript

         * Consola > Almacenamiento > Almacenamiento local > (sitio web) > ContextHubPersistence
         * Consola > Almacenamiento > Almacenamiento de sesión > (sitio web) > ContextHubPersistence
         * Consola > Almacenamiento > Cookies > (sitio web) > ContextHubPersistence
   * Internet Explorer:

      * Abra Herramientas para desarrolladores > Consola

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* Utilice la API de ContextHub en la consola del explorador:

   * ContextHub proporciona las siguientes capas de persistencia de datos:

      * ContextHub.Utils.Persistence.Modes.LOCAL (predeterminado)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      El almacén de ContextHub define qué capa de persistencia se utilizará, por lo que para ver el estado actual de la persistencia se deben comprobar todas las capas.


Por ejemplo, para ver los datos almacenados en localStorage:

Para obtener una vista previa de la persistencia utilizada en ContextHub, un usuario puede:

* Utilice la consola del explorador:

   * Chrome: abra Herramientas para desarrolladores > Aplicación > Almacenamiento:

      * Almacenamiento local > (sitio web) > ContextHubPersistence
      * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
      * Cookies > (sitio web) > SessionPersistence
   * Firefox: abra Herramientas para desarrolladores > Almacenamiento:

      * Almacenamiento local > (sitio web) > ContextHubPersistence
      * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
      * Cookies > (sitio web) > SessionPersistence


* Utilice la API de ContextHub en la consola del explorador:

   * ContextHub proporciona las siguientes capas de persistencia de datos:

      * ContextHub.Utils.Persistence.Modes.LOCAL (predeterminado)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      El almacén de ContextHub define qué capa de persistencia se utilizará, por lo que para ver el estado actual de la persistencia se deben comprobar todas las capas.


Por ejemplo, para ver los datos almacenados en localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Eliminación de la persistencia de ContextHub {#clearing-persistence-of-contexthub}

Para borrar la persistencia de ContextHub:

* Para borrar la persistencia de las tiendas cargadas actualmente:

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

* Para borrar todas las capas de persistencia de ContextHub, se debe llamar al código apropiado para todas las capas:

   * ContextHub.Utils.Persistence.Modes.LOCAL (predeterminado)
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
