---
title: Información general de componentes
seo-title: Componentes
description: Los componentes son unidades modulares que cuentan con una funcionalidad específica para presentar el contenido en el sitio web
seo-description: Los componentes son unidades modulares que cuentan con una funcionalidad específica para presentar el contenido en el sitio web
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# Información general de componentes{#components-overview}

En esta página se ofrece una descripción general de los componentes de Adobe Experience Manager (AEM), como los [utilizados para la creación](/help/sites-authoring/default-components-foundation.md)de páginas.

## ¿Qué son los componentes? {#what-exactly-is-a-component}

* Unidades modulares que proporcionan una funcionalidad específica para presentar el contenido en el sitio web.
* Reutilizable.
* Desarrollado como unidades independientes dentro de una carpeta del repositorio.
* No tiene archivos de configuración ocultos.
* Puede contener otros componentes.
* Puede ejecutarse en cualquier lugar dentro de cualquier sistema AEM. También pueden limitarse a ejecutarse en componentes específicos.
* Tener una interfaz de usuario estandarizada.
* Tener un comportamiento de edición que se pueda configurar.
* Utilizar cuadros de diálogo creados con subelementos basados en componentes Granite UI
* Se desarrollan con [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) (recomendado) o JSP.
* Se puede desarrollar para crear componentes personalizados que extiendan la funcionalidad predeterminada.

Debido a que los componentes son modulares, puede:

* Desarrolle un nuevo componente en la instancia local.
* Implementarlo en el entorno de prueba.
* Implementarla en el entorno de creación activo, donde permite a los autores y administradores agregar y configurar contenido.
* Implementarlo en los entornos de publicación activa, donde se utilizan para representar contenido para los visitantes del sitio web. Ciertos componentes, por ejemplo para Comunidades, también aceptan datos introducidos por los usuarios.

Cada componente de AEM:

* Es un tipo de recurso.
* Es una colección de secuencias de comandos que realizan completamente una función específica.
* Puede funcionar de *forma aislada*, es decir, en AEM o en un portal.

## Componentes integrados en AEM {#out-of-the-box-components-within-aem}

AEM comes with a variety of [out-of-the-box components](/help/sites-authoring/default-components.md) that provide comprehensive functionality including:

* Sistema de párrafos ( `parsys`)
* Página ( `responsivegrid` - solo IU táctil)
* Texto
* Imagen, con texto adjunto
* Barra de herramientas

Los componentes proporcionados y su uso dentro de los sitios web [We.Retail de](/help/sites-developing/we-retail.md) muestra ilustran cómo implementar y utilizar los componentes. Los componentes se proporcionan con todo el código fuente y pueden utilizarse tal cual o como puntos de partida para componentes modificados o ampliados.

### Componentes principales y componentes básicos {#core-components-and-foundation-components}

Existen dos conjuntos de componentes de AEM proporcionados por Adobe disponibles:

* [Componentes principales](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [Componentes de base](/help/sites-authoring/default-components-foundation.md)

**Los componentes** principales se introdujeron con AEM 6.3 y ofrecen una funcionalidad de creación flexible y rica en funciones. El sitio [de referencia](/help/sites-developing/we-retail.md) We.Retail ilustra cómo se pueden utilizar los componentes principales y representa las optimizaciones actuales del desarrollo de componentes.

**Foundation Components** ha estado disponible con AEM para muchas versiones y está disponible de forma predeterminada en una instalación estándar de AEM. Aunque aún se admite, la mayoría de ellas han quedado obsoletas, ya no se mejoran y se basan en tecnologías heredadas.

>[!NOTE]
>
>[Los componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) principales representan las prácticas recomendadas actuales para el diseño y el desarrollo de componentes y sirven como implementaciones de referencia.
>
>[Las herramientas](modernization-tools.md) de modernización de AEM pueden ayudar a migrar a los componentes principales.

### Visualización de componentes disponibles {#viewing-available-components}

Para obtener una descripción general de todos los componentes disponibles en la instancia de AEM, utilice la consola [](/help/sites-authoring/default-components-console.md)Componentes.

También puede utilizar CRXDE Lite para obtener una lista de todos los componentes disponibles en el repositorio.

1. En **[!UICONTROL CRXDE Lite]**, seleccione **[!UICONTROL Herramientas]** en la barra de herramientas y, a continuación, **[!UICONTROL Consulta]**, que abre la ficha **[!UICONTROL Consulta]** .

1. En la ficha **[!UICONTROL Consulta]** , seleccione `XPath` como **[!UICONTROL Tipo]**.

1. En el campo de entrada **[!UICONTROL Consulta]**, escriba la cadena siguiente:

   `//element(*, cq:Component)`

1. Haga clic en **[!UICONTROL Ejecutar]** y se enumerarán los componentes.

## Recursos adicionales {#further-reading}

Las páginas siguientes proporcionan información más detallada sobre el desarrollo de estos (y otros) componentes:

* [Componentes de AEM: conceptos básicos](/help/sites-developing/components-basics.md)
* [Desarrollo de componentes de AEM](/help/sites-developing/developing-components.md)
* [Desarrollo de componentes de AEM: ejemplos de código](/help/sites-developing/developing-components-samples.md)
* [Configuración de varios editores in situ](/help/sites-developing/multiple-inplace-editors.md)
* [Modo de desarrollador](/help/sites-developing/developer-mode.md)
* [Prueba de la IU](/help/sites-developing/hobbes.md)
* [Componentes para fragmentos de contenido](/help/sites-developing/components-content-fragments.md)
* [Obtención de información de la página en formato JSON](/help/sites-developing/pageinfo.md)
* [Internacionalización de componentes](/help/sites-developing/i18n.md)
* [Componentes principales](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [Uso de Ocultar condiciones](/help/sites-developing/hide-conditions.md)
* IU clásica

   * [Componentes de AEM (IU clásica)](/help/sites-developing/developing-components-classic.md)
   * [Uso y ampliación de utilidades (IU clásica)](/help/sites-developing/widgets.md)
   * [Uso de xtypes (IU clásica)](/help/sites-developing/xtypes.md)
   * [Desarrollo de formularios (IU clásica)](/help/sites-developing/developing-forms.md)

