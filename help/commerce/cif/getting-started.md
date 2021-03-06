---
title: Introducción a Contenido y comercio AEM
description: Obtenga información sobre cómo implementar un proyecto de Contenido y comercio AEM.
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 6%

---

# Introducción a Contenido y comercio AEM {#start}

Para comenzar con AEM Contenido y comercio, debe instalar el complemento Contenido y comercio de AEM para AEM 6.5.

## Requisito mínimo de software

[Paquete de servicio de AEM 6.5](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html) Se requiere 7 o posterior.

## Incorporación {#onboarding}

La incorporación para AEM contenido y comercio es un proceso de dos pasos:

1. Instalación del complemento de contenido y comercio de AEM para AEM 6.5

2. Conectar AEM con su solución de comercio

### Instalación del complemento de contenido y comercio de AEM para AEM 6.5 {#install-add-on}

Descargue e instale el complemento de AEM Commerce para AEM 6.5 desde el [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) portal.

Inicie e instale el Service Pack AEM 6.5 requerido. Se recomienda instalar el último Service Pack disponible.

>[!NOTE]
>
>Esto lo hará el CSE para AEM clientes de Managed Service.

### Conectar AEM a su sistema de comercio {#connect}

AEM se puede conectar a cualquier sistema de comercio que tenga un extremo de GraphQL accesible para AEM. Estos extremos generalmente están disponibles para el público o pueden conectarse a través de VPN privada o conexiones locales dependiendo de la configuración individual del proyecto.

Opcionalmente, se puede proporcionar un encabezado de autenticación para utilizar funciones de CIF adicionales que requieran autenticación.

Proyectos generados por el [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)y [Tienda de referencia de Venia AEM](https://github.com/adobe/aem-cif-guides-venia) que ya se incluye en la variable [configuración predeterminada](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) debe ajustarse.

Reemplace el valor de la variable `url` en `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` con el extremo GraphQL del sistema comercial. Esta configuración se puede realizar a través de la consola OSGI o implementando la configuración OSGI a través del proyecto. Se admiten diferentes configuraciones para sistemas de ensayo y producción utilizando distintos modos AEM ejecución.

Los componentes principales AEM Content and Commerce Add-On y CIF utilizan conexiones AEM del lado del servidor y del lado del cliente. Los componentes principales del CIF del lado del cliente y las herramientas de creación del complemento CIF se conectan de forma predeterminada a `/api/graphql`. Esto se puede ajustar mediante la configuración del Cloud Service del CIF si es necesario (consulte a continuación).

El complemento CIF proporciona un servlet proxy de GraphQL en `/api/graphql` que se pueden usar opcionalmente para [desarrollo local](develop.md). Para implementaciones de producción, se recomienda configurar un proxy inverso al extremo de comercio GraphQL mediante el AEM Dispatcher o en otras capas de red (como CDN).

## Configuración de tiendas y catálogos {#catalog}

El complemento y la variable [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components) se puede utilizar en varias estructuras AEM sitio conectadas a diferentes tiendas de comercio (o vistas de tiendas, etc.). De forma predeterminada, el complemento CIF se implementa con una configuración predeterminada que se conecta al catálogo y almacén predeterminados de Adobe Commerce.

Esta configuración se puede ajustar para el proyecto mediante la configuración del Cloud Service del CIF siguiendo estos pasos:

1. En AEM vaya a Herramientas -> Cloud Services -> Configuración del CIF

2. Seleccione la configuración de comercio que desee cambiar

3. Abra las propiedades de configuración mediante la barra de acciones

![Configuración de Cloud Services del CIF](/help/commerce/cif/assets/cif-cloud-service-config.png)

Se pueden configurar las siguientes propiedades:

- Cliente de GraphQL: seleccione el cliente de GraphQL configurado para la comunicación de back-end de comercio. Esto suele permanecer de forma predeterminada.
- Vista de almacén: el identificador de vista de tienda. Si está vacía, se utilizará la vista de tienda predeterminada.
- Ruta de proxy de GraphQL: la ruta de URL del proxy GraphQL AEM usar para solicitudes de proxy al extremo de comercio back-end GraphQL.
   >[!NOTE]
   >
   > En la mayoría de las configuraciones, el valor predeterminado `/api/graphql` no debe cambiarse. Solo la configuración avanzada que no utilice el proxy de GraphQL proporcionado debe cambiar esta configuración.
- Habilitar compatibilidad con UID de catálogo : habilite la compatibilidad con UID en lugar de con ID en las llamadas de GraphQL de comercio back-end.
   >[!NOTE]
   >
   > La compatibilidad con UID se ha introducido en Adobe Commerce 2.4.2. Solo debe habilitarse si el back-end de comercio admite un esquema de GraphQL de la versión 2.4.2 o posterior.
- Identificador de categoría raíz del catálogo: el identificador (UID o ID) de la raíz del catálogo del almacén
   >[!CAUTION]
   >
   > A partir de la versión 2.0.0 de los componentes principales de CIF, la compatibilidad con `id` se ha eliminado y se ha reemplazado por `uid`. Si su proyecto utiliza los componentes principales del CIF versión 2.0.0, debe activar la compatibilidad con el UID del catálogo y utilizar un UID de categoría válido como &quot;Identificador de categoría raíz del catálogo&quot;.

La configuración que se muestra arriba es para referencia. Los proyectos deben proporcionar sus propias configuraciones.

Para obtener configuraciones más complejas que utilizan varias estructuras de sitios de AEM combinadas con distintos catálogos de comercio, consulte la [Configuración de varias tiendas de comercio](configuring/multi-store-setup.md) tutorial.

## Recursos adicionales {#additional-resources}

- [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
- [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
- [Configuración de varias tiendas de comercio](configuring/multi-store-setup.md)
