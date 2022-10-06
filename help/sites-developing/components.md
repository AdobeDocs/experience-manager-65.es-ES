---
title: Información general sobre componentes
seo-title: Components
description: Los componentes son unidades modulares que implementan una funcionalidad específica para presentar el contenido en su sitio web
seo-description: Components are modular units which realize specific functionality to present your content on your website
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
exl-id: 9e30c969-2692-4380-943a-b022ee900ce8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 10%

---

# Información general sobre componentes{#components-overview}

Esta página proporciona información general sobre los componentes de Adobe Experience Manager (AEM), como los [se utiliza para la creación de páginas](/help/sites-authoring/default-components-foundation.md).

## ¿Qué son los componentes? {#what-exactly-is-a-component}

* Unidades modulares que implementan funcionalidades específicas para presentar el contenido en su sitio web.
* Reutilizable.
* Se desarrolla como unidades independientes dentro de una carpeta del repositorio.
* No tienen archivos de configuración ocultos.
* Puede contener otros componentes.
* Puede ejecutarse en cualquier lugar dentro de cualquier sistema AEM. También se pueden limitar para que se ejecuten en componentes específicos.
* Disponen de una interfaz de usuario estandarizada.
* Tenga un comportamiento de edición que se pueda configurar.
* Utilizar cuadros de diálogo creados con subelementos basados en componentes de la interfaz de usuario de Granite
* Se desarrollan utilizando [HTL](https://docs.adobe.com/content/help/es-ES/experience-manager-htl/using/overview.html) (recomendado) o JSP.
* Se puede desarrollar para crear componentes personalizados que amplíen la funcionalidad predeterminada.

Como los componentes son modulares, puede:

* Desarrolle un nuevo componente en la instancia local.
* Implíquela en el entorno de prueba.
* Implíquela en su entorno de creación activo, donde permiten a los autores o administradores añadir y configurar contenido.
* Implemente en los entornos de publicación activos, donde se utilizan para representar contenido para los visitantes del sitio web. Algunos componentes, por ejemplo para Comunidades, también aceptan la entrada de los usuarios.

Cada componente AEM:

* Es un tipo de recurso.
* Es una colección de scripts que realizan completamente una función específica.
* Puede funcionar en *aislamiento*, es decir, dentro de AEM o un portal.

## Componentes listos para usar dentro de AEM {#out-of-the-box-components-within-aem}

AEM viene con una variedad de [componentes integrados](/help/sites-authoring/default-components.md) que proporcionan una amplia funcionalidad, que incluye:

* Sistema de párrafos ( `parsys`)
* Página ( `responsivegrid` - solo IU táctil)
* Texto
* Imagen con texto acompañante
* Barra de herramientas

Los componentes proporcionados y su uso dentro de la variable [sitios web de We.Retail de muestra](/help/sites-developing/we-retail.md) se proporciona una ilustración de cómo implementar y utilizar componentes. Los componentes se proporcionan con todo el código fuente y se pueden utilizar tal cual o como puntos de partida para los componentes modificados o ampliados.

### Componentes principales y componentes básicos {#core-components-and-foundation-components}

Hay dos conjuntos de componentes de AEM proporcionados por el Adobe disponibles:

* [Componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html)
* [Componentes de base](/help/sites-authoring/default-components-foundation.md)

**Componentes principales** se han introducido con AEM 6.3 y ofrecen funciones flexibles y personalizables de creación de contenido. La variable [Sitio de referencia de We.Retail](/help/sites-developing/we-retail.md) ilustra cómo se pueden utilizar los componentes principales y representa las prácticas recomendadas actuales del desarrollo de componentes.

**Componentes básicos** han estado disponibles con AEM para muchas versiones y están disponibles de forma predeterminada en una instalación de AEM estándar. Aunque aún es compatible, la mayoría de ellos han quedado obsoletos, ya no se mejoran y se basan en tecnologías heredadas.

>[!NOTE]
>
>[Componentes principales](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) representan las prácticas recomendadas actuales para el diseño y desarrollo de componentes y sirven como implementaciones de referencia.
>
>[Herramientas de modernización AEM](modernization-tools.md) puede ayudar a migrar a componentes principales.

### Visualización de componentes disponibles {#viewing-available-components}

Para obtener una descripción general de todos los componentes disponibles en la instancia de AEM, utilice la variable [Consola Componentes](/help/sites-authoring/default-components-console.md).

Como alternativa, también puede utilizar CRXDE Lite para obtener una lista de todos los componentes disponibles en el repositorio.

1. En **[!UICONTROL CRXDE Lite]**, seleccione **[!UICONTROL Herramientas]** en la barra de herramientas y, a continuación, **[!UICONTROL Consulta]**, que abre el **[!UICONTROL Consulta]** pestaña .

1. En el **[!UICONTROL Consulta]** , seleccione `XPath` como **[!UICONTROL Tipo]**.

1. En el campo de entrada **[!UICONTROL Consulta]**, escriba la cadena siguiente:

   `//element(*, cq:Component)`

1. Haga clic en **[!UICONTROL Ejecutar]** y se muestran los componentes.

## Recursos adicionales {#further-reading}

Las páginas siguientes proporcionan información más detallada sobre el desarrollo de estos y otros componentes:

* [Componentes AEM: conceptos básicos](/help/sites-developing/components-basics.md)
* [Desarrollo de componentes AEM](/help/sites-developing/developing-components.md)
* [Desarrollo de componentes de AEM: ejemplos de código](/help/sites-developing/developing-components-samples.md)
* [Configuración de varios editores in situ](/help/sites-developing/multiple-inplace-editors.md)
* [Modo de desarrollador](/help/sites-developing/developer-mode.md)
* [Prueba de la interfaz de usuario](/help/sites-developing/hobbes.md)
* [Componentes para fragmentos de contenido](/help/sites-developing/components-content-fragments.md)
* [Obtención de información de página en formato JSON](/help/sites-developing/pageinfo.md)
* [Internacionalización de componentes](/help/sites-developing/i18n.md)
* [Componentes principales](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [Uso de Ocultar condiciones](/help/sites-developing/hide-conditions.md)
* IU clásica

   * [Componentes AEM (IU clásica)](/help/sites-developing/developing-components-classic.md)
   * [Uso y ampliación de utilidades (IU clásica)](/help/sites-developing/widgets.md)
   * [Uso de xtype (IU clásica)](/help/sites-developing/xtypes.md)
   * [Desarrollo de Forms (IU clásica)](/help/sites-developing/developing-forms.md)
