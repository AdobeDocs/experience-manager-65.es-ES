---
title: SPA Introducción y Tutorial
seo-title: SPA Introducción y Tutorial
description: En este artículo se introducen los conceptos de SPA y se pasa por una aplicación básica de SPA para la creación, mostrando cómo se relaciona con el AEM SPA Editor subyacente.
seo-description: En este artículo se introducen los conceptos de SPA y se pasa por una aplicación básica de SPA para la creación, mostrando cómo se relaciona con el AEM SPA Editor subyacente.
uuid: 4b0a9e53-3892-4d60-8bd3-7ff740d2f137
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 0478afcb-b029-4ce6-b3e6-cee4bb5408ce
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '2000'
ht-degree: 0%

---


# Introducción a SPA y tutoriales{#spa-introduction-and-walkthrough}

Las aplicaciones de una sola página (SPA) pueden oferta de experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido dentro de AEM sin problemas para un sitio creado con dichos marcos.

El Editor SPA oferta una solución integral para admitir SPA dentro de AEM. En este artículo se explica el uso de una aplicación de SPA básica para la creación y se muestra cómo se relaciona con el editor de SPA de AEM subyacente.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren SPA procesamiento del lado del cliente basado en el marco de trabajo (por ejemplo, React o Angular).

## Introducción {#introduction}

### Objetivo del artículo {#article-objective}

Este artículo presenta los conceptos básicos de SPA antes de guiar al lector a través de un tutorial del editor de SPA mediante una aplicación SPA sencilla para mostrar la edición básica del contenido. A continuación, profundiza en la construcción de la página y en cómo se relaciona la aplicación SPA con el Editor de SPA de AEM y cómo interactúa con él.

El objetivo de esta introducción y tutorial es demostrar a un desarrollador AEM por qué SPA son relevantes, cómo funcionan en general, cómo gestiona un SPA el Editor AEM y cómo es diferente de una aplicación AEM estándar.

El tutorial se basa en la funcionalidad AEM estándar y en la aplicación de Historial We.Retail de muestra. Deben cumplirse los siguientes requisitos:

* [AEM versión 6.4 con Service Pack 2 o posterior](/help/release-notes/sp-release-notes.md)
* [Instale la aplicación de Historial We.Retail de muestra disponible en GitHub aquí.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

>[!CAUTION]
>
>Este documento utiliza la aplicación de Historial [We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) únicamente con fines de demostración. No debe utilizarse para ningún trabajo de proyecto.
>
>Cualquier proyecto AEM debe aprovechar el [AEM Arquetipo de proyecto](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html), que admite SPA proyectos usando React o Angular y aprovecha el SDK SPA.

### ¿Qué es un SPA? {#what-is-a-spa}

Una aplicación de una sola página (SPA) difiere de una página convencional en que se procesa en el lado del cliente y se dirige principalmente a JavaScript, y depende de las llamadas de Ajax para cargar datos y actualizar la página de forma dinámica. La mayor parte o la totalidad del contenido se recupera una vez en una única carga de página con recursos adicionales cargados asincrónicamente según sea necesario según la interacción del usuario con la página.

Esto reduce la necesidad de actualizar la página y presenta al usuario una experiencia que es fluida, rápida y se parece más a una experiencia nativa de la aplicación.

El Editor de SPA de AEM permite a los desarrolladores de front-end crear SPA que se pueden integrar en un sitio AEM, permitiendo a los autores de contenido editar el contenido SPA tan fácilmente como cualquier otro contenido AEM.

### ¿Por qué un SPA? {#why-a-spa}

Al ser más rápido, fluido y más parecido a una aplicación nativa, una SPA se convierte en una experiencia muy atractiva no sólo para el visitante de la página web, sino también para los especialistas en mercadotecnia y desarrolladores debido a la naturaleza de SPA trabajo.

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**Visitantes**

* Los visitantes desean experiencias nativas cuando interactúan con el contenido.
* Hay datos claros de que cuanto más rápida sea una página, más probabilidad habrá de producirse una conversión.

**Especialistas en mercadotecnia**

* Los especialistas en marketing desean oferta de experiencias ricas y nativas para atraer a visitantes a fin de que se comprometan plenamente con el contenido.
* La personalización puede hacer que estas experiencias sean aún más atractivas.

**Desarrolladores**

* Los desarrolladores quieren una clara separación de las preocupaciones entre el contenido y la presentación.
* La separación limpia hace que el sistema sea más extensible y permite el desarrollo independiente del front-end.

### ¿Cómo funciona un SPA? {#how-does-a-spa-work}

La idea principal detrás de una SPA es que las llamadas y la dependencia en un servidor se reducen para minimizar los retrasos causados por las llamadas al servidor de modo que el SPA se aproxime a la capacidad de respuesta de una aplicación nativa.

En una página web secuencial tradicional, solo se cargan los datos necesarios para la página inmediata. Esto significa que cuando el visitante se mueve a otra página, se llama al servidor para obtener los recursos adicionales. Es posible que sean necesarias llamadas adicionales a medida que el visitante interactúa con los elementos de la página. Estas llamadas múltiples pueden dar una sensación de retraso o retraso, ya que la página tiene que responder a las solicitudes del visitante.

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

Para una experiencia más fluida, que se aproxima a lo que espera un visitante de las aplicaciones móviles nativas, un SPA carga todos los datos necesarios para el visitante en la primera carga. Aunque esto puede tardar un poco más al principio, elimina la necesidad de realizar llamadas al servidor adicionales.

Al realizar el procesamiento en el lado del cliente, el elemento de página reacciona más rápido y las interacciones con la página por parte del visitante son inmediatas. Cualquier dato adicional que se necesite se llama de forma asíncrona para maximizar la velocidad de la página.

>[!NOTE]
>
>Para obtener detalles técnicos sobre cómo SPA trabajar en AEM, consulte el artículo [Introducción a SPA en AEM](/help/sites-developing/spa-getting-started-react.md).
>
>Para obtener una vista más detallada del diseño, la arquitectura y el flujo de trabajo técnico del Editor de SPA, consulte el artículo [Información general del editor de SPA](/help/sites-developing/spa-overview.md).

## Experiencia de edición de contenido con SPA {#content-editing-experience-with-spa}

Cuando se crea un SPA para aprovechar el Editor de SPA de AEM, el autor del contenido no observa ninguna diferencia al editar y crear contenido. La funcionalidad de AEM común está disponible y no se requieren cambios en el flujo de trabajo del autor.

>[!NOTE]
>
>El tutorial se basa en la funcionalidad AEM estándar y en la aplicación de Historial We.Retail de muestra. Deben cumplirse los siguientes requisitos:
>
>* [AEM versión 6.4 con Service Pack 2](/help/release-notes/sp-release-notes.md)
>* [Instale la aplicación de Historial We.Retail de muestra disponible en GitHub aquí.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

>



1. Edite la aplicación de Historial We.Retail en AEM.

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at142533](assets/screen_shot_2018-06-07at142533.png)

1. Seleccione un componente de encabezado y observe que aparece una barra de herramientas como cualquier otro componente. Seleccione **Editar**.

   ![screen_shot_2018-06-07at142937](assets/screen_shot_2018-06-07at142937.png)

1. Edite el contenido como si fuera normal dentro de AEM y tenga en cuenta que los cambios se mantienen.

   ![screen_shot_2018-06-07at143419](assets/screen_shot_2018-06-07at143419.png)

   >[!NOTE]
   >Consulte la [Información general del editor de SPA](spa-overview.md#requirements-limitations) para obtener más información sobre el editor de texto y el SPA in situ.

1. Utilice el navegador de recursos para arrastrar y soltar una imagen nueva en un componente de imagen.

   ![screen_shot_2018-06-07at143530](assets/screen_shot_2018-06-07at143530.png)

1. El cambio se mantiene.

   ![screen_shot_2018-06-07at143732](assets/screen_shot_2018-06-07at143732.png)

Se admiten herramientas de creación adicionales como arrastrar y soltar componentes adicionales en la página, reorganizar componentes y modificar el diseño, como en cualquier aplicación que no sea de SPA.

>[!NOTE]
>
>El Editor de SPA no modifica el DOM de la aplicación. El propio SPA es responsable del DOM.
>
>Para ver cómo funciona esto, continúe con la siguiente sección de este artículo [Aplicaciones de SPA y el AEM Editor SPA](/help/sites-developing/spa-walkthrough.md#spa-apps-and-the-aem-spa-editor).

## Aplicaciones SPA y el Editor de SPA de AEM {#spa-apps-and-the-aem-spa-editor}

La experiencia de cómo se comporta un SPA para el usuario final y, a continuación, la inspección de la página de SPA ayuda a comprender mejor cómo funciona una aplicación SAP con el Editor de SPA en AEM.

### Uso de una aplicación SPA {#using-an-spa-application}

1. Cargue la aplicación de Historial We.Retail en el servidor de publicación o utilizando la opción **Vista tal y como se publica** del menú **Información de página** del editor de páginas.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-08at102650](assets/screen_shot_2018-06-08at102650.png)

   Tenga en cuenta la estructura de las páginas, incluida la navegación a páginas secundarias, utilidades meteorológicas y artículos.

1. Navegue a una página secundaria mediante el menú y observe que la página se carga inmediatamente sin necesidad de actualizar.

   ![screen_shot_2018-06-08at102815](assets/screen_shot_2018-06-08at102815.png)

1. Abra las herramientas de desarrollador integradas de su navegador y supervise la actividad de red a medida que navega por las páginas secundarias.

   ![screen_shot_2018-06-08at103922](assets/screen_shot_2018-06-08at103922.png)

   Hay muy poco tráfico a medida que se mueve de una página a otra en la aplicación. La página no se vuelve a cargar y solo se solicitan las imágenes nuevas.

   El SPA administra el contenido y el enrutamiento por completo en el lado del cliente.

Por lo tanto, si la página no se recarga al navegar por las páginas secundarias, ¿cómo se carga?

La siguiente sección, [Carga de una aplicación SPA](/help/sites-developing/spa-walkthrough.md#loading-an-spa-application), explora en profundidad la mecánica de cargar la SPA y cómo se puede cargar el contenido sincrónica y asincrónicamente.

### Cargando una aplicación SPA {#loading-an-spa-application}

1. Si aún no se ha cargado, cargue la aplicación de Historial We.Retail en el servidor de publicación o utilizando la opción **Vista tal y como se publica** del menú **Información de página** del editor de páginas.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at144736](assets/screen_shot_2018-06-07at144736.png)

1. Utilice la herramienta integrada de su navegador para vista del origen de la página.
1. Tenga en cuenta que el contenido de la fuente es extremadamente limitado.

   ```
   <!DOCTYPE HTML>
   <html lang="en-CH">
       <head>
       <meta charset="UTF-8">
       <title>We.Retail Journal</title>
   
       <meta name="template" content="we-retail-react-template"/>
   
   <link rel="stylesheet" href="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.css" type="text/css">
   
   <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
   
   </head>
       <body class="page basicpage">
   
   <div id="page"></div>
   
   <script type="text/javascript" src="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.js"></script>
   
       </body>
   </html>
   ```

   La página no tiene contenido dentro de su cuerpo. Se compone principalmente de hojas de estilo y una llamada a una secuencia de comandos React, `we-retail-journal-react.js`.

   Esta secuencia de comandos de React es el controlador principal de esta aplicación y es responsable de procesar todo el contenido.

1. Utilice las herramientas integradas del explorador para inspeccionar la página. Consulte el contenido del DOM completamente cargado.

   ![screen_shot_2018-06-07at151848](assets/screen_shot_2018-06-07at151848.png)

1. Cambie a la ficha Red del Inspector y vuelva a cargar la página.

   Al omitir las solicitudes de imagen, tenga en cuenta que los recursos principales cargados para la página son la propia página, CSS, React Javascript, sus dependencias y los datos JSON de la página.

   ![screen_shot_2018-06-07at152155](assets/screen_shot_2018-06-07at152155.png)

1. Cargue `react.model.json` en una nueva ficha.

   `/content/we-retail-journal/react.model.json`

   ![screen_shot_2018-06-07at152636](assets/screen_shot_2018-06-07at152636.png)

   El Editor de SPA de AEM aprovecha [Servicios de contenido de AEM](/help/assets/content-fragments/content-fragments.md) para entregar todo el contenido de la página como un modelo JSON.

   Al implementar interfaces específicas, los modelos Sling proporcionan la información necesaria para el SPA. El envío de los datos de JSON se delega hacia abajo en cada componente (de página, párrafo, componente, etc.).

   Cada componente elige lo que expone y cómo se procesa (lado del servidor con HTL o lado del cliente con React). Por supuesto, este artículo se centra en la representación del lado del cliente con React.

1. El modelo también puede agrupar las páginas para que se carguen sincrónicamente, reduciendo el número de recargas de página necesarias.

   En el ejemplo de Historial We.Retail, las páginas `home`, `blog` y `aboutus` se cargan sincrónicamente, ya que los visitantes suelen visitar todas esas páginas. Sin embargo, la página `weather` se carga asincrónicamente, ya que es menos probable que los visitantes la visiten.

   Este comportamiento no es obligatorio y es totalmente definible.

   ![screen_shot_2018-06-07at153945](assets/screen_shot_2018-06-07at153945.png)

1. Para vista de esta diferencia de comportamiento, vuelva a cargar la página y borre la actividad de red del inspector. Navegue al blog y a las páginas de acerca de nosotros en el menú de la página y vea que no hay ningún informe de actividad de red.

   Vaya a la página del clima y vea que la `weather.model.json` se llama asincrónicamente.

   ![screen_shot_2018-06-07at155738](assets/screen_shot_2018-06-07at155738.png)

### Interacción con el Editor de SPA {#interaction-with-the-spa-editor}

Con la aplicación de Historial We.Retail de muestra, queda claro cómo se comporta y se carga la aplicación cuando se publica, aprovechando los servicios de contenido para el envío de contenido JSON así como la carga asincrónica de recursos.

Además, para el autor del contenido, la creación de contenido mediante un editor de SPA es perfecta dentro de AEM.

En la siguiente sección analizaremos el contrato que permite al Editor de SPA relacionar componentes dentro del SPA con AEM componentes y lograr esta experiencia de edición sin problemas.

1. Cargue la aplicación de Historial We.Retail en el editor y cambie al modo **Previsualización**.

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

1. Con las herramientas de desarrollador integradas del explorador, inspeccione el contenido de la página. Con la herramienta de selección, seleccione un componente editable en la página y vista los detalles del elemento.

   Tenga en cuenta que el componente tiene un nuevo atributo de datos `data-cq-data-path`.

   ![screen_shot_2018-06-08at095124](assets/screen_shot_2018-06-08at095124.png)

   Por ejemplo

   `data-cq-data-path="root/responsivegrid/paragraph_1`

   Esta ruta permite recuperar y asociar el objeto de configuración de contexto de edición de cada componente.

   Este es el único atributo de marcado necesario para que el editor reconozca este componente como un componente editable dentro del SPA. Según este atributo, el Editor de SPA determinará qué configuración editable está asociada al componente, de modo que el marco, la barra de herramientas, etc. correctos. está cargado.

   Algunos nombres de clase específicos también se agregan para marcar marcadores de posición y para la funcionalidad de arrastrar y soltar recursos.

   >[!NOTE]
   >
   >Se trata de un cambio en el comportamiento de las páginas procesadas del lado del servidor en AEM, donde hay un elemento `cq` insertado para cada componente editable.
   >
   >
   >Este método en SPA elimina la necesidad de inyectar elementos personalizados, confiando solamente en un atributo de datos adicional, lo que simplifica el marcado para el desarrollador de front-end.

## Próximos pasos {#next-steps}

Ahora que comprende la experiencia de edición SPA en AEM y cómo se relaciona un SPA con el Editor de SPA, indíquese más profundamente en la comprensión de cómo se crea un SPA.

* [Introducción a SPA en ](/help/sites-developing/spa-getting-started-react.md) AEMmuestra cómo se crea un SPA básico para trabajar con el Editor de SPA en AEM
* [SPA ](/help/sites-developing/spa-overview.md) Información general del editor profundiza en el modelo de comunicación entre AEM y el SPA.
* [Desarrollo de SPA para ](/help/sites-developing/spa-architecture.md) AEMdescribe cómo involucrar a los desarrolladores de front-end para desarrollar un SPA para AEM, así como cómo SPA interactuar con la arquitectura AEM.
