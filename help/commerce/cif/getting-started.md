---
title: Introducción a AEM Content y Commerce
description: AEM Obtenga información sobre cómo implementar un proyecto de Contenido y Commerce de.
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 4%

---

# Introducción a AEM Content y Commerce {#start}

AEM Para empezar a usar Contenido de la y Commerce AEM, debe instalar el complemento Contenido de la y Commerce AEM para la versión 6.5 de la misma.

## Requisito mínimo de software

AEM Se requiere [Paquete de servicio 6.5](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html) 7 o posterior.

## Incorporación {#onboarding}

AEM La incorporación de Contenido de la y Commerce es un proceso de dos pasos:

1. AEM Instalación del complemento Contenido de la y Commerce AEM para la versión 6.5 de la versión

2. AEM Conéctese con su solución de comercio de

### AEM Instalación del complemento Contenido de la y Commerce AEM para la versión 6.5 de la versión {#install-add-on}

AEM Descargue e instale el complemento de Commerce AEM para la versión 6.5 de desde el portal de [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html).

AEM Inicie e instale el paquete de servicio necesario de 6.5 de. Se recomienda instalar el último Service Pack disponible.

>[!NOTE]
>
>AEM Esto lo hará el CSE para los clientes de Managed Service de la.

### AEM Conéctese a su sistema de Commerce {#connect}

AEM Se puede conectar a cualquier sistema de comercio que tenga un punto final de GraphQL AEM accesible para su. Estos extremos suelen estar disponibles públicamente o pueden conectarse a través de conexiones privadas VPN o locales, según la configuración individual del proyecto.

CIF Opcionalmente, se puede proporcionar un encabezado de autenticación para utilizar funciones de autenticación adicionales que requieran autenticación.

AEM AEM Se deben ajustar los proyectos generados por el [tipo de archivo del proyecto &#x200B;](https://github.com/adobe/aem-project-archetype) y el [Almacén de referencia de Venia de](https://github.com/adobe/aem-cif-guides-venia) que ya está incluido en la [configuración predeterminada](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json).

Reemplace el valor de `url` en `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` por el extremo GraphQL de su sistema de comercio. Esta configuración se puede realizar a través de la consola OSGI o implementando la configuración OSGI a través del proyecto. AEM Se admiten diferentes configuraciones para sistemas de ensayo y producción utilizando diferentes modos de ejecución de la.

AEM Los componentes principales y del complemento de Commerce CIF AEM y de contenido de la utilizan conexiones tanto del lado del servidor como del lado del cliente. CIF CIF Las herramientas de creación de complementos de componentes principales y de componentes principales de la del lado del cliente se conectan de forma predeterminada a `/api/graphql`. CIF Esto se puede ajustar a través de la configuración del Cloud Service de si es necesario (consulte a continuación).

CIF El complemento de proporciona un servlet proxy de GraphQL en `/api/graphql` que se puede usar opcionalmente para [desarrollo local](develop.md). Para implementaciones de producción, se recomienda encarecidamente configurar un proxy inverso al extremo de Commerce GraphQL AEM a través de Dispatcher o en otras capas de red (como CDN).

## Configuración de tiendas y catálogos {#catalog}

CIF AEM El complemento y los [Componentes principales](https://github.com/adobe/aem-core-cif-components) se pueden usar en varias estructuras de sitio conectadas a varias tiendas de comercio (o vistas de tiendas, etc.) y en varias estructuras de sitio que se han conectado a diferentes tiendas de comercio. CIF De forma predeterminada, el complemento de se implementa con una configuración predeterminada que se conecta a la tienda y al catálogo predeterminados de Adobe Commerce.

CIF Esta configuración se puede ajustar para el proyecto mediante la configuración del Cloud Service de la siguiendo estos pasos:

1. AEM En la página de inicio, vaya a Herramientas > Cloud Service CIF > Configuración de la

2. Seleccione la configuración de comercio que desee cambiar

3. Abra las propiedades de configuración a través de la barra de acciones

CIF ![Configuración de Cloud Service de](/help/commerce/cif/assets/cif-cloud-service-config.png)

Se pueden configurar las siguientes propiedades:

- Cliente de GraphQL: seleccione el cliente de GraphQL configurado para la comunicación back-end comercial. Esto debería permanecer en modo predeterminado.
- Vista de tienda: el identificador de la vista de tienda. Si está vacía, se utiliza la vista de tienda predeterminada.
- Ruta del proxy de GraphQL: la ruta URL del proxy de GraphQL AEM que se utiliza para las solicitudes de proxy al extremo de GraphQL backend de comercio.

  >[!NOTE]
  >
  >En la mayoría de las configuraciones, no se debe cambiar el valor predeterminado `/api/graphql`. Solo la configuración avanzada que no utiliza el proxy de GraphQL proporcionado debe cambiar esta configuración.

- Habilitar compatibilidad con UID de catálogo: habilite la compatibilidad con UID en lugar de con ID en las llamadas comerciales de GraphQL back-end.

  >[!NOTE]
  >
  >La compatibilidad con UID se ha introducido en Adobe Commerce 2.4.2. Habilite esta opción solo si el backend de Commerce admite un esquema GraphQL de la versión 2.4.2 o posterior.

- Identificador de categoría raíz del catálogo: el identificador (UID o ID) de la raíz del catálogo de la tienda

  >[!CAUTION]
  >
  >CIF A partir de la versión 2.0.0 de los componentes principales de la, se quitó la compatibilidad con `id` y se reemplazó con `uid`. CIF Si el proyecto utiliza componentes principales de la versión 2.0.0 de la, debe habilitar la compatibilidad con UID de catálogo y utilizar un UID de categoría válido como &quot;Identificador de categoría raíz de catálogo&quot;.

La configuración que se muestra arriba es como referencia. Los proyectos deben proporcionar sus propias configuraciones.

AEM Para obtener configuraciones más complejas que utilicen varias estructuras de sitio de la combinadas con distintos catálogos de comercio, consulte el tutorial [Configuración de varias tiendas de Commerce](configuring/multi-store-setup.md).

## Recursos adicionales {#additional-resources}

- [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
- [Tienda de referencia de Venia de AEM](https://github.com/adobe/aem-cif-guides-venia)
- [Configuración de varias tiendas de Commerce](configuring/multi-store-setup.md)
