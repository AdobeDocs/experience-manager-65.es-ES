---
title: Implementación de referencia de We.Retail
seo-title: Implementación de referencia de We.Retail
description: We.Retail es una previsualización tecnológica de una implementación de referencia que ilustra la manera recomendada de configurar una presencia en línea con AEM
seo-description: We.Retail es una previsualización tecnológica de una implementación de referencia que ilustra la manera recomendada de configurar una presencia en línea con AEM
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
translation-type: tm+mt
source-git-commit: 307a1db2e5bbb72d730c89ba14f5ce02b96c108d
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 12%

---


# Implementación de referencia de We.Retail{#we-retail-reference-implementation}

## Introducción {#introduction}

We.Retail es una implementación de referencia y contenido de muestra que ilustra la manera recomendada de configurar una presencia en línea con Adobe Experience Manager.

We.Retail utiliza las últimas tecnologías de AEM como HTL, diseños adaptables, plantillas editables, componentes principales y mucho más.

Aunque ilustra una vertical de venta minorista, la forma en que se configura el sitio puede aplicarse a cualquier vertical, y sólo el catálogo de productos y las características del carro de compras son específicas del comercio minorista.

## Características {#features}

Como AEM implementación de referencia estándar, We.Retail muestra algunas de las características más poderosas de AEM.

| **Función** | **Descripción** | **¿Interesado?** |
|---|---|---|
| [Estructura global del sitio](/help/sites-administering/tc-bp.md) | We.Retail incluye maestros de idiomas que se copian en directo en sitios específicos de países. | [¡Pruébelo!](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [Diseño adaptable](/help/sites-authoring/responsive-layout.md) | Todas las páginas presentan un diseño interactivo para adaptarse de forma dinámica a la pantalla y al tamaño del dispositivo. | [¡Pruébelo!](/help/sites-developing/we-retail-responsive-layout.md) |
| [Plantillas editables](/help/sites-developing/page-templates-editable.md) | Todas las páginas se basan en plantillas editables, lo que permite a los no desarrolladores adaptar y personalizar las plantillas. | [¡Pruébelo!](/help/sites-developing/we-retail-editable-templates.md) |
| [Lenguaje de plantilla HTML](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html) | Todos los componentes se basan en HTL |  |
| [Capacidades de comercio electrónico](/help/sites-developing/ecommerce.md) | Presenta un catálogo de productos |  |
| [Sitios de comunidades](/help/communities/overview.md) | Permitir que los visitantes se unan a las discusiones de la comunidad, lean blogs y mucho más |  |
| [Componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) | Todos los componentes se basan en los nuevos componentes principales y son más utilizables y configurables por el usuario de forma predeterminada | [¡Pruébelo!](/help/sites-developing/we-retail-core-components.md) |
| [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) | La sección Experiencias de We.Retail muestra el poder de reutilizar contenido mediante fragmentos de contenido. | [¡Pruébelos!](/help/sites-developing/we-retail-content-fragments.md) |
| [Fragmentos de experiencias](/help/sites-authoring/experience-fragments.md) | Un fragmento de experiencias es un grupo de uno o varios componentes que incluye contenido y diseño que se puede consultar dentro de las páginas. | [¡Pruébelos!](/help/sites-developing/we-retail-experience-fragments.md) |

## Introducción {#getting-started}

We.Retail se entrega como AEM contenido de muestra. Para utilizarla, simplemente [AEM de inicio como normalmente lo haría](/help/sites-deploying/deploy.md#getting-started), asegurándose de que el contenido de muestra no está deshabilitado.

>[!CAUTION]
>
>We.Retail no debe instalarse en instancias de producción. Las instancias de producción deben iniciarse en `nosamplecontent` [runmode](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>We.Retail se basa en la tecnología de AEM más reciente y, por lo tanto, no admite [creación de IU clásica](/help/sites-classic-ui-authoring/home.md).

### Última versión {#latest-version}

Aunque We.Retail se distribuye con la versión de AEM, es posible que las actualizaciones del contenido y sus funciones se realicen después de la versión. Por lo tanto, es posible [descargar la última versión de GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) y luego [cargarla](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) e [instalarla](/help/sites-administering/package-manager.md#installing-packages) como un paquete en la instancia de AEM.

### Primeros pasos {#first-steps}

1. Una vez que se inicia AEM (y/o se instala We.Retail), el sitio **We.Retail** está disponible en la [consola de sitios](/help/sites-authoring/basic-handling.md#global-navigation).
1. Por ejemplo: se puede abrir la siguiente página y debe verse como se muestra en el [apéndice](#appendix) siguiente:

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail y Geometrixx {#we-retail-geometrixx}

Geometrixx y sus muchas encarnaciones sirvieron como contenido de muestra en versiones anteriores de AEM. Desde la versión 6.3, We.Retail ha sido el contenido de muestra entregado con AEM y sirve como la nueva implementación de referencia estándar.

We.Retail es técnicamente más robusto y aprovecha la última tecnología de AEM para ser más flexible y escalable, al tiempo que demuestra las nuevas características del producto.

### Comparación de funciones {#feature-comparison}

La siguiente tabla ofrece una visión general de las principales funciones disponibles en We.Retail en comparación con Geometrixx.

* **** Disponible significa que los ejemplos de la función se encuentran en el contenido de muestra.
* **No** disponible significa que los ejemplos de la función no están disponibles en el contenido de muestra, pero no significa que la función en sí no lo esté.

| **Función** | **We.Retail** | **Geometrixx** |
|---|---|---|
| Estructura global del sitio | Maestros de idioma copiados en vivo en sitios específicos de países | No disponible |
| Fragmentos de contenido | Disponible | No disponible |
| Fragmentos de experiencias | Disponible | No disponible |
| Diseño adaptable  | Para todas las páginas | Solo Geometrixx Medias |
| Plantillas editables | Para todas las páginas | No disponible |
| HTL | Todos los componentes | Limitado |
| Direccionamiento | Para todas las páginas | Solo Geometrixx Outdoors |
| Pantallas | Disponible | No disponible |
| Móvil | No disponible | Disponible |
| Manuscritos | No disponible | Disponible |
| Componentes de carrusel, descarga, gráfico | No disponible | Disponible |
| Control de columna | Se sustituye por el contenedor de diseño | Disponible |
| Forms | No disponible | Disponible |
| Campaign | No hay ejemplos de correo electrónico | Disponible |

>[!NOTE]
>
>Esta lista se esfuerza por ser completa, pero no debe considerarse exhaustiva.

## Contribute {#contribute}

We.Retail se ha lanzado como un proyecto de código abierto y la última versión del código fuente se puede descargar desde GitHub.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir un proyecto AEM-sample-we-Retail en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

La última versión también se puede [descargar directamente](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) como un paquete instalable.

Si tiene problemas, presente [problemas de GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

Siéntase libre de hacer fork o contribuir con [solicitudes de extracción](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## Vista previa {#preview}

Previsualización de la página de bienvenida de We.Retail:

![screencapture-localhost-4502-editor-html-content-we-retail-us-es-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)

