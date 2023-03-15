---
title: Implementación de referencia de We.Retail
seo-title: We.Retail Reference Implementation
description: AEM We.Retail es una previsualización tecnológica de una implementación de referencia que ilustra la forma recomendada de configurar una presencia en línea con las soluciones de
seo-description: We.Retail is a technology preview of a reference implementation that illustrates the recommended way of setting up an online presence with AEM
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 11%

---

# Implementación de referencia de We.Retail{#we-retail-reference-implementation}

## Introducción {#introduction}

We.Retail es una implementación de referencia y contenido de muestra que ilustra la forma recomendada de configurar una presencia en línea con Adobe Experience Manager.

AEM We.Retail utiliza las últimas tecnologías en materia de diseño, como HTL, los diseños adaptables, las plantillas editables, los componentes principales y mucho más, entre otras.

Aunque ilustra un vertical minorista, la forma en que se configura el sitio se puede aplicar a cualquier vertical y solo las funciones del catálogo de productos y del carro de compras son específicas del minorista.

## Características {#features}

AEM AEM Como implementación de referencia estándar de, We.Retail muestra algunas de las funciones más potentes de las soluciones de de de.

| **Función** | **Descripción** | **¿Interesado?** |
|---|---|---|
| [Estructura del sitio globalizada](/help/sites-administering/tc-bp.md) | We.Retail incluye formatos de idioma que se copian en tiempo real en sitios específicos de cada país. | [¡Pruébalo!](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [Diseño interactivo](/help/sites-authoring/responsive-layout.md) | Todas las páginas tienen un diseño interactivo para adaptarse dinámicamente a la pantalla y al tamaño del dispositivo. | [¡Pruébalo!](/help/sites-developing/we-retail-responsive-layout.md) |
| [Plantillas editables](/help/sites-developing/page-templates-editable.md) | Todas las páginas se basan en plantillas editables, lo que permite a los usuarios que no son desarrolladores adaptar y personalizar las plantillas. | [¡Pruébalo!](/help/sites-developing/we-retail-editable-templates.md) |
| [Lenguaje de plantilla HTML ](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | Todos los componentes se basan en HTL |  |
| [Funcionalidades de eCommerce](/help/commerce/cif-classic/developing/ecommerce.md) | Incluye un catálogo de productos |  |
| [Sitios de comunidades](/help/communities/overview.md) | Permite a los visitantes unirse a las discusiones de la comunidad, leer blogs y mucho más |  |
| [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) | Todos los componentes se basan en los nuevos componentes principales y son más utilizables y configurables por el usuario de forma predeterminada | [¡Pruébalo!](/help/sites-developing/we-retail-core-components.md) |
| [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) | La sección Experiencias de We.Retail muestra la potencia de reutilizar contenido mediante fragmentos de contenido. | [¡Pruébelos!](/help/sites-developing/we-retail-content-fragments.md) |
| [Fragmentos de experiencias](/help/sites-authoring/experience-fragments.md) | Un fragmento de experiencias es un grupo de uno o varios componentes que incluye contenido y diseño que se puede consultar dentro de las páginas. | [¡Pruébelos!](/help/sites-developing/we-retail-experience-fragments.md) |

## Introducción {#getting-started}

AEM We.Retail se entrega como contenido de muestra de la. Para utilizar, simplemente [AEM Empiece como lo haría normalmente.](/help/sites-deploying/deploy.md#getting-started), asegurándose de que el contenido de la muestra no esté deshabilitado.

>[!CAUTION]
>
>We.Retail no debe instalarse en instancias de producción. Las instancias de producción deben iniciarse en `nosamplecontent` [modo de ejecución](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>AEM We.Retail se basa en la tecnología más reciente de la red de distribución de productos de la industria de la y, por lo tanto, no es compatible [creación de IU clásica](/help/sites-classic-ui-authoring/home.md).

### Última versión {#latest-version}

AEM Aunque We.Retail se distribuye con el lanzamiento de la versión de la, es posible que se actualicen el contenido y sus funciones después del lanzamiento. Por lo tanto, es posible [descargue la última versión de GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) y luego [cargar](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) y [instalar](/help/sites-administering/package-manager.md#installing-packages) AEM funciona como un paquete en la instancia de su.

### Primeros pasos {#first-steps}

1. AEM Una vez que se haya iniciado la aplicación de la versión (y/o se haya instalado We.Retail), el sitio web se abrirá en la siguiente ubicación: **We.Retail** está disponible en la [consola sitios](/help/sites-authoring/basic-handling.md#global-navigation).
1. Por ejemplo, la siguiente página se puede abrir y debe tener el aspecto que se muestra en la [apéndice](#appendix) a continuación:

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail y Geometrixx {#we-retail-geometrixx}

El Geometrixx AEM y sus muchas encarnaciones servían como contenido de muestra en versiones anteriores de la. AEM Desde la versión 6.3, We.Retail ha sido el contenido de muestra entregado con la implementación de y sirve como la nueva implementación de referencia estándar de.

AEM We.Retail es técnicamente más robusta y aprovecha la tecnología más avanzada para ser más flexible y escalable, a la vez que muestra las nuevas características del producto.

### Comparación de funciones {#feature-comparison}

La siguiente tabla ofrece información general sobre las principales funciones disponibles en We.Retail en comparación con Geometrixx.

* **Disponible** significa que los ejemplos de la función se encuentran en el contenido de muestra.
* **No disponible** significa que los ejemplos de la función no están disponibles en el contenido de muestra, pero no significa que la función en sí no lo esté.

| **Función** | **We.Retail** | **Geometrixx** |
|---|---|---|
| Estructura del sitio globalizada | Los formatos de idiomas se copian en tiempo real en sitios específicos de cada país | No disponible |
| Fragmentos de contenido | Disponible | No disponible |
| Fragmentos de experiencias | Disponible | No disponible |
| Diseño adaptable | Para todas las páginas | Solo Geometrixx Medias |
| Plantillas editables | Para todas las páginas | No disponible |
| HTL | Todos los componentes | Limitado |
| Direccionamiento | Para todas las páginas | Solo Geometrixx Outdoors |
| Screens | Disponible | No disponible |
| Móvil | No disponible | Disponible |
| Manuscritos | No disponible | Disponible |
| Componentes de carrusel, descarga y gráfico | No disponible | Disponible |
| Control de columna | Reemplazado por el contenedor de diseño | Disponible |
| Forms | No disponible | Disponible |
| Campaign | No hay ejemplos de correo electrónico | Disponible |

>[!NOTE]
>
>Esta lista trata de ser completa, pero no debe considerarse exhaustiva.

## Contribute {#contribute}

We.Retail se ha lanzado como un proyecto de código abierto y la última versión del código fuente se puede descargar desde GitHub.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra el proyecto aem-sample-we-retail en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

La última versión también puede ser [descargado directamente](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) como paquete instalable.

Si tiene problemas, presente un [Problemas de GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

Siéntase libre de ramificar o contribuir con [solicitudes de extracción](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## Vista previa {#preview}

Vista previa de la página de bienvenida de We.Retail:

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
