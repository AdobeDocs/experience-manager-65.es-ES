---
title: Encabezados HTTP personalizados
description: Obtenga información sobre cómo configurar encabezados HTTP personalizados en Adobe Experience Manager Commerce.
exl-id: 834aadac-c3be-4e7a-a3cb-349608810b40
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 3%

---

# Encabezados HTTP personalizados {#custom-http-headers}

## Información general {#overview}

CIF Para obtener más control sobre su back-end, los autores pueden configurar encabezados HTTP personalizados que se envían al motor de comercio, junto con los que ya envía el usuario Los casos de uso comunes incluyen configuraciones de varias tiendas en las que puede utilizar encabezados HTTP para controlar la respuesta del back-end de comercio.

>[!NOTE]
>
>Los desarrolladores siempre pueden configurar encabezados HTTP personalizados mediante la configuración del cliente de GraphQL.
>

## Configuración {#configuration}

Para configurar los encabezados HTTP personalizados, primero debe definirlos. Los encabezados HTTP personalizados deben definirse primero agregándolos a la configuración del servicio `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` mediante una configuración OSGi.

Puede configurar los valores de los encabezados HTTP en la página Configuración de Cloud Service de su proyecto:

1. Vaya a la página de configuración del Cloud Service en Herramientas > Cloud Services CIF > Configuración de la.
1. Abra una configuración existente o cree una.
1. Vaya a la pestaña &quot;Avanzado&quot; y busque el campo múltiple &quot;Encabezados HTTP personalizados&quot;. Puede seleccionar los encabezados definidos anteriormente y asignarles valores.

Los componentes que utilizan la configuración de servicio en la nube anterior envían estos encabezados HTTP con cada solicitud de GraphQL.

## Restricciones {#restrictions}

Aunque el servicio permite definir cualquier nombre de encabezado, incluidos los estándar, no están disponibles para su configuración. En otras palabras, no se pueden anular los encabezados HTTP estándar con esta función. Se puede encontrar una lista de nombres de encabezados restringidos [aquí](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). Además de estos, hay dos encabezados más que no se pueden utilizar:

* CIF &quot;Almacén&quot;: utilizado por los usuarios para identificar la tienda de Adobe Commerce.
* CIF &quot;Preview-Version&quot;: utilizado por los usuarios para recuperar productos clasificados.
