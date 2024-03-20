---
title: Introducción a AEM Content y Commerce
description: AEM Obtenga información sobre cómo implementar un proyecto de Contenido y comercio de.
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 4%

---

# Introducción a AEM Content y Commerce {#start}

AEM AEM AEM Para empezar a usar Contenido y comercio de, debe instalar el complemento de Contenido y comercio de para 6.5.

## Requisito mínimo de software

[AEM Paquete de servicio de.5](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html) Se requiere 7 o posterior.

## Incorporación {#onboarding}

AEM La incorporación para Contenido y comercio de es un proceso de dos pasos:

1. AEM AEM Instale el complemento de contenido y comercio de la para 6.5

2. AEM Conéctese con su solución de comercio de

### AEM AEM Instale el complemento de contenido y comercio de la para 6.5 {#install-add-on}

AEM AEM Descargue e instale el complemento de comercio de la para 6.5 desde el [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html) portal.

AEM Inicie e instale el paquete de servicio necesario de 6.5 de. Se recomienda instalar el último Service Pack disponible.

>[!NOTE]
>
>AEM Esto lo hará el CSE para los clientes de Managed Service de la.

### AEM Conexión a su sistema de comercio de {#connect}

AEM Se puede conectar a cualquier sistema de comercio que tenga un punto final de GraphQL AEM accesible para su. Estos extremos suelen estar disponibles públicamente o pueden conectarse a través de conexiones privadas VPN o locales, según la configuración individual del proyecto.

CIF Opcionalmente, se puede proporcionar un encabezado de autenticación para utilizar funciones de autenticación adicionales que requieran autenticación.

Proyectos generados por el [AEM Tipo de archivo del proyecto](https://github.com/adobe/aem-project-archetype), y el [AEM Tienda de referencia de Venia en](https://github.com/adobe/aem-cif-guides-venia) que ya se incluye en la [configuración predeterminada](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) debe ajustarse.

Reemplace el valor del `url` in `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` con el extremo GraphQL de su sistema de comercio. Esta configuración se puede realizar a través de la consola OSGI o implementando la configuración OSGI a través del proyecto. AEM Se admiten diferentes configuraciones para sistemas de ensayo y producción utilizando diferentes modos de ejecución de la.

AEM CIF AEM Los componentes principales y del complemento de contenido y comercio de la utilizan conexiones del lado del servidor y del lado del cliente de la aplicación de la forma más sencilla posible. CIF CIF Las herramientas de creación de complementos de componentes principales y de componentes de cliente se conectan de forma predeterminada a `/api/graphql`. CIF Esto se puede ajustar a través de la configuración del Cloud Service de si es necesario (consulte a continuación).

CIF El complemento de proporciona un servlet proxy de GraphQL en `/api/graphql` que se puede utilizar de forma opcional para [desarrollo local](develop.md). Para implementaciones de producción, se recomienda encarecidamente configurar un proxy inverso al extremo de GraphQL AEM de comercio a través de la instancia de Dispatcher de o en otras capas de red (como CDN).

## Configuración de tiendas y catálogos {#catalog}

El complemento y el [CIF Componentes principales](https://github.com/adobe/aem-core-cif-components) AEM se puede utilizar en varias estructuras de sitio de la conectadas a diferentes tiendas comerciales (o vistas de tiendas, etc.). CIF De forma predeterminada, el complemento de se implementa con una configuración predeterminada que se conecta a la tienda y al catálogo predeterminados de Adobe Commerce.

CIF Esta configuración se puede ajustar para el proyecto mediante la configuración del Cloud Service de la siguiendo estos pasos:

1. AEM En la página de inicio, vaya a Herramientas > Cloud Service CIF > Configuración de la

2. Seleccione la configuración de comercio que desee cambiar

3. Abra las propiedades de configuración a través de la barra de acciones

![CIF Configuración de Cloud Service de](/help/commerce/cif/assets/cif-cloud-service-config.png)

Se pueden configurar las siguientes propiedades:

- Cliente de GraphQL: seleccione el cliente de GraphQL configurado para la comunicación back-end comercial. Esto debería permanecer en modo predeterminado.
- Vista de tienda: el identificador de la vista de tienda. Si está vacía, se utiliza la vista de tienda predeterminada.
- Ruta del proxy de GraphQL: la ruta URL del proxy de GraphQL AEM que se utiliza para las solicitudes de proxy al extremo de GraphQL backend de comercio.

  >[!NOTE]
  >
  >En la mayoría de las configuraciones, el valor predeterminado `/api/graphql` no se debe cambiar. Solo la configuración avanzada que no utiliza el proxy de GraphQL proporcionado debe cambiar esta configuración.

- Habilitar compatibilidad con UID de catálogo: habilite la compatibilidad con UID en lugar de con ID en las llamadas comerciales de GraphQL back-end.

  >[!NOTE]
  >
  >La compatibilidad con UID se ha introducido en Adobe Commerce 2.4.2. Habilite esta opción solo si el backend de Commerce admite un esquema GraphQL de la versión 2.4.2 o posterior.

- Identificador de categoría raíz del catálogo: el identificador (UID o ID) de la raíz del catálogo de la tienda

  >[!CAUTION]
  >
  >CIF A partir de la versión 2.0.0 de los componentes principales de, la compatibilidad con `id` se ha eliminado y reemplazado por `uid`. CIF Si el proyecto utiliza componentes principales de la versión 2.0.0 de la, debe habilitar la compatibilidad con UID de catálogo y utilizar un UID de categoría válido como &quot;Identificador de categoría raíz de catálogo&quot;.

La configuración que se muestra arriba es como referencia. Los proyectos deben proporcionar sus propias configuraciones.

AEM Para obtener configuraciones más complejas que utilicen varias estructuras de sitio de la combinadas con diferentes catálogos de comercio, consulte la [Configuración de varias tiendas de Commerce](configuring/multi-store-setup.md) tutorial.

## Recursos adicionales {#additional-resources}

- [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
- [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
- [Configuración de varias tiendas de Commerce](configuring/multi-store-setup.md)
