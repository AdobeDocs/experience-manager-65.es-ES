---
title: Implementación de referencia de We.Retail
seo-title: Implementación de referencia de We.Retail
description: We.Retail es una vista previa de tecnología de una implementación de referencia que ilustra la forma recomendada de configurar una presencia en línea con AEM
seo-description: We.Retail es una vista previa de tecnología de una implementación de referencia que ilustra la forma recomendada de configurar una presencia en línea con AEM
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 12%

---

# Implementación de referencia de We.Retail{#we-retail-reference-implementation}

## Introducción {#introduction}

We.Retail es una implementación de referencia y contenido de muestra que ilustra la forma recomendada de configurar una presencia en línea con Adobe Experience Manager.

We.Retail utiliza las últimas tecnologías de AEM, como HTL, diseños interactivos, plantillas editables, componentes principales y mucho más.

Aunque ilustra un vertical minorista, la forma en que se configura el sitio se puede aplicar a cualquier vertical y solo el catálogo de productos y las funciones del carro de compras son específicas del minorista.

## Características {#features}

Como implementación AEM referencia estándar, We.Retail muestra algunas de las funciones más potentes de AEM.

| **Función** | **Descripción** | **¿Interesado?** |
|---|---|---|
| [Estructura global del sitio](/help/sites-administering/tc-bp.md) | We.Retail incluye maestros de idiomas que se copian en vivo en sitios específicos de países. | [¡Pruébelo!](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [Diseño interactivo](/help/sites-authoring/responsive-layout.md) | Todas las páginas tienen un diseño interactivo para adaptarse de forma dinámica a la pantalla y al tamaño del dispositivo. | [¡Pruébelo!](/help/sites-developing/we-retail-responsive-layout.md) |
| [Plantillas editables](/help/sites-developing/page-templates-editable.md) | Todas las páginas se basan en plantillas editables, lo que permite a los usuarios que no son desarrolladores adaptar y personalizar las plantillas. | [¡Pruébelo!](/help/sites-developing/we-retail-editable-templates.md) |
| [Lenguaje de plantilla HTML](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html) | Todos los componentes se basan en HTL |  |
| [Capacidades del comercio electrónico](/help/commerce/cif-classic/developing/ecommerce.md) | Incluye un catálogo de productos |  |
| [Sitios de comunidades](/help/communities/overview.md) | Permitir que los visitantes participen en discusiones de la comunidad, lean blogs y mucho más |  |
| [Componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) | Todos los componentes se basan en los nuevos componentes principales y son más utilizables y configurables por el usuario | [¡Pruébelo!](/help/sites-developing/we-retail-core-components.md) |
| [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) | La sección Experiencias de We.Retail muestra la potencia de reutilizar contenido mediante fragmentos de contenido. | [¡Pruébelos!](/help/sites-developing/we-retail-content-fragments.md) |
| [Fragmentos de experiencias](/help/sites-authoring/experience-fragments.md) | Un fragmento de experiencias es un grupo de uno o varios componentes que incluye contenido y diseño que se puede consultar dentro de las páginas. | [¡Pruébelos!](/help/sites-developing/we-retail-experience-fragments.md) |

## Introducción {#getting-started}

We.Retail se entrega como contenido AEM ejemplo. Para usar, simplemente [inicie AEM como lo haría normalmente](/help/sites-deploying/deploy.md#getting-started), asegurándose de que el contenido de muestra no esté deshabilitado.

>[!CAUTION]
>
>We.Retail no debe instalarse en instancias de producción. Las instancias de producción deben iniciarse en `nosamplecontent` [runmode](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>We.Retail se basa en la última tecnología de AEM y, por lo tanto, no admite la creación de [IU clásica](/help/sites-classic-ui-authoring/home.md).

### Última versión {#latest-version}

Aunque We.Retail se distribuye con la versión de AEM, es posible que se actualicen el contenido y sus funciones después de la versión. Por lo tanto, es posible [descargar la última versión de GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) y luego [cargarla](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) e [instalarla](/help/sites-administering/package-manager.md#installing-packages) como un paquete en la instancia de AEM.

### Primeros pasos {#first-steps}

1. Una vez iniciado el AEM (o cuando We.Retail esté instalado), el sitio **We.Retail** está disponible en la [consola Sitios](/help/sites-authoring/basic-handling.md#global-navigation).
1. Por ejemplo, se puede abrir la siguiente página y debe tener el aspecto que se muestra en el [apéndice](#appendix) siguiente:

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail y Geometrixx {#we-retail-geometrixx}

Geometrixx y sus muchas encarnaciones sirvieron como contenido de muestra en versiones anteriores de AEM. Desde la versión 6.3, We.Retail ha sido el contenido de muestra AEM y sirve como la nueva implementación de referencia estándar.

We.Retail es técnicamente más robusto y aprovecha la última tecnología de AEM para ser más flexible y escalable, a la vez que muestra las características más recientes del producto.

### Comparación de características {#feature-comparison}

La siguiente tabla ofrece una descripción general de las principales funciones disponibles en We.Retail en comparación con Geometrixx.

* **** Disponibilidad significa que se encuentran ejemplos de la función en el contenido de ejemplo.
* **No está** disponible significa que los ejemplos de la función no están disponibles en el contenido de ejemplo, pero no significa que la función en sí no lo esté.

| **Función** | **We.Retail** | **Geometrixx** |
|---|---|---|
| Estructura global del sitio | Los maestros de idiomas se copian en vivo en sitios específicos de países | No disponible |
| Fragmentos de contenido | Disponible | No disponible |
| Fragmentos de experiencias | Disponible | No disponible |
| Diseño adaptable  | Para todas las páginas | Solo Geometrixx Medias |
| Plantillas editables | Para todas las páginas | No disponible |
| HTL | Todos los componentes | Limitada |
| Direccionamiento | Para todas las páginas | Solo Geometrixx Outdoors |
| Pantallas | Disponible | No disponible |
| Móvil | No disponible | Disponible |
| Manuscritos | No disponible | Disponible |
| Carrusel, descargar, crear gráficos de componentes | No disponible | Disponible |
| Control de columna | Se ha reemplazado por un contenedor de diseño | Disponible |
| Forms | No disponible | Disponible |
| Campaign | No hay ejemplos de correo electrónico | Disponible |

>[!NOTE]
>
>Esta lista se esfuerza por ser completa, pero no debe considerarse exhaustiva.

## Contribute {#contribute}

We.Retail se ha lanzado como un proyecto de código abierto y la última versión del código fuente se puede descargar desde GitHub.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra el proyecto aem-sample-we-retail en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

La última versión también puede [descargarse directamente](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) como paquete instalable.

Si tiene problemas, presente [problemas de GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

Siéntase libre de ramificar o contribuir con [solicitudes de extracción](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## Vista previa {#preview}

Vista previa de la página de bienvenida de We.Retail:

![screencaptura-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
