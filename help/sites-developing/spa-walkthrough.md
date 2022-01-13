---
title: Introducción y tutorial de SPA
seo-title: SPA Introduction and Walkthrough
description: Este artículo presenta los conceptos de un SPA y explica cómo utilizar una aplicación de SPA básica para la creación, mostrando cómo se relaciona con el AEM SPA Editor subyacente.
seo-description: This article introduces the concepts of a SPA and walks through using a basic SPA application for authoring, showing how it relates to the underlying AEM SPA Editor.
uuid: 4b0a9e53-3892-4d60-8bd3-7ff740d2f137
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 0478afcb-b029-4ce6-b3e6-cee4bb5408ce
docset: aem65
exl-id: 95990112-2afc-420a-a7c7-9613f40d4c4a
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '1968'
ht-degree: 1%

---

# Introducción y tutorial de SPA{#spa-introduction-and-walkthrough}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios mediante marcos de SPA y los autores quieren editar contenido sin problemas dentro de AEM para un sitio creado con dichos marcos.

El SPA Editor ofrece una solución completa para admitir SPA dentro de AEM. Este artículo recorre mediante una aplicación de SPA básica para la creación y muestra cómo se relaciona con el AEM SPA Editor subyacente.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren SPA procesamiento del lado del cliente basado en el marco de trabajo (por ejemplo, React o Angular).

## Introducción {#introduction}

### Objetivo del artículo {#article-objective}

Este artículo presenta los conceptos básicos de SPA antes de guiar al lector a través de un tutorial del editor de SPA utilizando una sencilla aplicación SPA para demostrar la edición básica del contenido. A continuación, se profundiza en la construcción de la página y en cómo se relaciona la aplicación SPA con el AEM SPA Editor y cómo interactúa con ella.

El objetivo de esta introducción y tutorial es demostrar a un desarrollador AEM por qué los SPA son relevantes, cómo funcionan en general, cómo el editor de SPA gestiona un SPA y cómo es diferente de una aplicación AEM estándar.

El tutorial se basa en la funcionalidad de AEM estándar y en la aplicación de diario We.Retail de ejemplo. Deben cumplirse los siguientes requisitos:

* [AEM versión 6.4 con Service Pack 2 o posterior](/help/release-notes/release-notes.md)
* [Instale la aplicación de muestra de We.Retail Journal disponible en GitHub aquí.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

>[!CAUTION]
>
>Este documento utiliza la variable [Aplicación de diario We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) únicamente con fines de demostración. No debe utilizarse para ningún trabajo de proyecto.
>
>Cualquier proyecto AEM debería aprovechar el [Tipo de archivo del proyecto AEM](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/developing/archetype/overview.html), que admite SPA proyectos que utilizan React o Angular y aprovecha el SDK de SPA.

### ¿Qué es un SPA? {#what-is-a-spa}

Una aplicación de una sola página (SPA) difiere de una página convencional en que se procesa en el lado del cliente y principalmente está dirigida por JavaScript, y se basa en llamadas Ajax para cargar datos y actualizar la página de forma dinámica. La mayoría o todo el contenido se recupera una vez en una única carga de página con recursos adicionales cargados asincrónicamente según sea necesario en función de la interacción del usuario con la página.

Esto reduce la necesidad de actualizar la página y presenta al usuario una experiencia que es fluida, rápida y se parece más a una experiencia nativa de la aplicación.

El AEM SPA Editor permite a los desarrolladores de front-end crear SPA que se pueden integrar en un sitio AEM, lo que permite a los autores de contenido editar el contenido SPA tan fácilmente como cualquier otro contenido AEM.

### ¿Por qué un SPA? {#why-a-spa}

Al ser más rápido, fluido y más parecido a una aplicación nativa, una SPA se convierte en una experiencia muy atractiva no solo para el visitante de la página web, sino también para los especialistas en marketing y desarrolladores debido a la naturaleza de cómo SPA funciona.

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**Visitantes**

* Los visitantes desean experiencias nativas cuando interactúan con el contenido.
* Hay datos claros de que cuanto más rápida sea una página, más probable será que se produzca una conversión.

**Especialistas en marketing**

* Los especialistas en marketing desean ofrecer experiencias ricas y nativas para atraer visitantes a fin de que participen plenamente en el contenido.
* La personalización puede hacer que estas experiencias sean aún más atractivas.

**Desarrolladores**

* Los desarrolladores quieren una separación clara de las preocupaciones entre el contenido y la presentación.
* La separación limpia hace que el sistema sea más extensible y permite el desarrollo independiente del front-end.

### ¿Cómo funciona un SPA? {#how-does-a-spa-work}

La idea principal de una SPA es que las llamadas y la dependencia de un servidor se reducen para minimizar los retrasos causados por las llamadas al servidor de modo que el SPA se aproxime a la capacidad de respuesta de una aplicación nativa.

En una página web secuencial tradicional, solo se cargan los datos necesarios para la página inmediata. Esto significa que cuando el visitante se mueve a otra página, se llama al servidor para obtener los recursos adicionales. Pueden ser necesarias llamadas adicionales, ya que el visitante interactúa con los elementos de la página. Estas llamadas múltiples pueden dar una sensación de retraso o retraso, ya que la página tiene que estar al día con las solicitudes del visitante.

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

Para una experiencia más fluida, que se acerca a lo que un visitante espera de las aplicaciones móviles nativas, un SPA carga todos los datos necesarios para el visitante en la primera carga. Aunque esto puede tardar un poco más al principio, elimina la necesidad de realizar llamadas al servidor adicionales.

Al realizar el procesamiento en el lado del cliente, el elemento de página reacciona más rápido y las interacciones con la página por parte del visitante son inmediatas. Cualquier dato adicional que se necesite se llama asincrónicamente para maximizar la velocidad de la página.

>[!NOTE]
>
>Para obtener detalles técnicos sobre cómo SPA funciona en AEM, consulte el artículo [Introducción a SPA en AEM](/help/sites-developing/spa-getting-started-react.md).
>
>Para obtener más información sobre el diseño, la arquitectura y el flujo de trabajo técnico del Editor de SPA, consulte el artículo [Información general del Editor de SPA](/help/sites-developing/spa-overview.md).

## Experiencia de edición de contenido con SPA {#content-editing-experience-with-spa}

Cuando se crea un SPA para aprovechar el AEM SPA Editor, el autor del contenido no observa ninguna diferencia al editar y crear contenido. La funcionalidad de AEM común está disponible y no se requieren cambios en el flujo de trabajo del autor.

>[!NOTE]
>
>El tutorial se basa en la funcionalidad de AEM estándar y en la aplicación de diario We.Retail de ejemplo. Deben cumplirse los siguientes requisitos:
>
>* [AEM versión 6.4 con Service Pack 2](/help/release-notes/release-notes.md)
>* [Instale la aplicación de muestra de We.Retail Journal disponible en GitHub aquí.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

>


1. Edite la aplicación de diario We.Retail en AEM.

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at142533](assets/screen_shot_2018-06-07at142533.png)

1. Seleccione un componente de encabezado y observe que aparece una barra de herramientas como cualquier otro componente. Seleccione **Editar**.

   ![screen_shot_2018-06-07at142937](assets/screen_shot_2018-06-07at142937.png)

1. Edite el contenido como de costumbre dentro de AEM y tenga en cuenta que los cambios se mantienen.

   ![screen_shot_2018-06-07at143419](assets/screen_shot_2018-06-07at143419.png)

   >[!NOTE]
   >Consulte la [Información general del Editor de SPA](spa-overview.md#requirements-limitations) para obtener más información sobre el editor de texto in situ y el SPA.

1. Utilice el navegador de recursos para arrastrar y soltar una nueva imagen en un componente de imagen.

   ![screen_shot_2018-06-07at143530](assets/screen_shot_2018-06-07at143530.png)

1. El cambio se mantiene.

   ![screen_shot_2018-06-07at143732](assets/screen_shot_2018-06-07at143732.png)

Se admiten herramientas de creación adicionales, como arrastrar y soltar componentes adicionales en la página, reorganizar componentes y modificar el diseño, como en cualquier aplicación que no sea de SPA.

>[!NOTE]
>
>El Editor de SPA no modifica el DOM de la aplicación. El propio SPA es responsable del DOM.
>
>Para ver cómo funciona esto, continúe con la siguiente sección de este artículo. [Aplicaciones SPA y el AEM SPA Editor](/help/sites-developing/spa-walkthrough.md#spa-apps-and-the-aem-spa-editor).

## Aplicaciones SPA y el AEM SPA Editor {#spa-apps-and-the-aem-spa-editor}

Experimentar cómo se comporta un SPA para el usuario final y luego inspeccionar la página SPA ayuda a comprender mejor cómo funciona una aplicación SAP con el SPA Editor en AEM.

### Uso de una aplicación SPA {#using-an-spa-application}

1. Cargue la aplicación de diario We.Retail en el servidor de publicación o utilice la opción **Ver tal y como aparece publicado** de la variable **Información de la página** en el editor de páginas.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-08at102650](assets/screen_shot_2018-06-08at102650.png)

   Tenga en cuenta la estructura de las páginas, incluida la navegación a páginas secundarias, widget meteorológico y artículos.

1. Vaya a una página secundaria mediante el menú y vea que la página se carga inmediatamente sin necesidad de actualizar.

   ![screen_shot_2018-06-08at102815](assets/screen_shot_2018-06-08at102815.png)

1. Abra las herramientas de desarrollador integradas del explorador y supervise la actividad de red a medida que navega por las páginas secundarias.

   ![screen_shot_2018-06-08at103922](assets/screen_shot_2018-06-08at103922.png)

   Hay muy poco tráfico a medida que se mueve de página en página en la aplicación. La página no se vuelve a cargar y solo se solicitan las imágenes nuevas.

   El SPA administra el contenido y el enrutamiento por completo en el lado del cliente.

Por lo tanto, si la página no se vuelve a cargar al navegar por las páginas secundarias, ¿cómo se carga?

La siguiente sección, [Carga de una aplicación SPA](/help/sites-developing/spa-walkthrough.md#loading-an-spa-application), profundiza en la mecánica de carga del SPA y en cómo se puede cargar el contenido sincrónica y asincrónicamente.

### Carga de una aplicación SPA {#loading-an-spa-application}

1. Si aún no se ha cargado, cargue la aplicación We.Retail Journal en el servidor de publicación o utilizando la opción **Ver tal y como aparece publicado** de la variable **Información de la página** en el editor de páginas.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at144736](assets/screen_shot_2018-06-07at144736.png)

1. Utilice la herramienta integrada del navegador para ver el origen de la página.
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

   La página no tiene contenido dentro de su cuerpo. Se compone principalmente de hojas de estilo y una llamada a un script React, `we-retail-journal-react.js`.

   Este script React es el controlador principal de esta aplicación y es responsable de procesar todo el contenido.

1. Utilice las herramientas integradas del explorador para inspeccionar la página. Consulte el contenido del DOM completamente cargado.

   ![screen_shot_2018-06-07at151848](assets/screen_shot_2018-06-07at151848.png)

1. Cambie a la ficha Red (Network) en el Inspector y vuelva a cargar la página.

   Ignorando las solicitudes de imagen, tenga en cuenta que los recursos principales cargados para la página son la página en sí, CSS, React Javascript, sus dependencias, así como los datos JSON de la página.

   ![screen_shot_2018-06-07at152155](assets/screen_shot_2018-06-07at152155.png)

1. Cargue el `react.model.json` en una pestaña nueva.

   `/content/we-retail-journal/react.model.json`

   ![screen_shot_2018-06-07at152636](assets/screen_shot_2018-06-07at152636.png)

   El AEM SPA Editor aprovecha [Servicios de contenido AEM](/help/assets/content-fragments/content-fragments.md) para entregar todo el contenido de la página como un modelo JSON.

   Al implementar interfaces específicas, los modelos Sling proporcionan la información necesaria para el SPA. El envío de los datos JSON se delega hacia abajo en cada componente (de página, párrafo, componente, etc.).

   Cada componente elige lo que expone y cómo se procesa (lado del servidor con HTL o lado del cliente con React). Por supuesto, este artículo se centra en la renderización del lado del cliente con React.

1. El modelo también puede agrupar las páginas de forma que se carguen sincrónicamente, lo que reduce el número de recargas de página necesarias.

   En el ejemplo de We.Retail Journal, la variable `home`, `blog`y `aboutus` las páginas se cargan sincrónicamente, ya que los visitantes suelen visitar todas esas páginas. Sin embargo, la variable `weather` se carga de forma asíncrona, ya que es menos probable que los visitantes la visiten.

   Este comportamiento no es obligatorio y es totalmente definible.

   ![screen_shot_2018-06-07at153945](assets/screen_shot_2018-06-07at153945.png)

1. Para ver esta diferencia de comportamiento, vuelva a cargar la página y borre la actividad de red del inspector. Vaya al blog y a las páginas de uso en el menú de página y vea que no hay actividad de red reportada.

   Vaya a la página del tiempo y compruebe que la variable `weather.model.json` se llama asincrónicamente.

   ![screen_shot_2018-06-07at155738](assets/screen_shot_2018-06-07at155738.png)

### Interacción con el SPA Editor {#interaction-with-the-spa-editor}

Con la aplicación de ejemplo We.Retail Journal, está claro cómo se comporta y se carga la aplicación cuando se publica, aprovechando los servicios de contenido para la entrega de contenido JSON, así como la carga asincrónica de recursos.

Además, para el autor del contenido, la creación de contenido mediante un editor de SPA es perfecta dentro de AEM.

En la siguiente sección analizaremos el contrato que permite al Editor de SPA relacionar componentes dentro del SPA con componentes de AEM y lograr esta experiencia de edición sin problemas.

1. Cargue la aplicación de diario We.Retail en el editor y cambie a **Vista previa** en el menú contextual.

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

1. Con las herramientas de desarrollador incorporadas del navegador, inspeccione el contenido de la página. Con la herramienta de selección, seleccione un componente editable en la página y vea los detalles del elemento.

   Tenga en cuenta que el componente tiene un nuevo atributo de datos `data-cq-data-path`.

   ![screen_shot_2018-06-08at095124](assets/screen_shot_2018-06-08at095124.png)

   Por ejemplo

   `data-cq-data-path="root/responsivegrid/paragraph_1`

   Estas rutas permiten la recuperación y asociación del objeto de configuración de contexto de edición de cada componente.

   Este es el único atributo de marcado necesario para que el editor reconozca este componente como editable dentro del SPA. En función de este atributo, el SPA Editor determinará qué configuración editable está asociada al componente, de modo que el marco, la barra de herramientas, etc. correctos. se carga.

   También se agregan algunos nombres de clase específicos para marcar marcadores de posición y para la funcionalidad de arrastrar y soltar recursos.

   >[!NOTE]
   >
   >Este es un cambio en el comportamiento de las páginas procesadas del lado del servidor en AEM, donde hay un `cq` elemento insertado para cada componente editable.
   >
   >
   >Este método en SPA elimina la necesidad de insertar elementos personalizados, basándose únicamente en un atributo de datos adicional, lo que simplifica el marcado para el desarrollador de front-end.

## Siguientes pasos {#next-steps}

Ahora que comprende la SPA experiencia de edición en AEM y cómo se relaciona un SPA con el Editor de SPA, profundiza en la comprensión de cómo se crea un SPA.

* [Introducción a SPA en AEM](/help/sites-developing/spa-getting-started-react.md) muestra cómo se crea una SPA básica para trabajar con el Editor de SPA en AEM
* [Información general del Editor de SPA](/help/sites-developing/spa-overview.md) profundiza en el modelo de comunicación entre AEM y el SPA.
* [Desarrollo de SPA para AEM](/help/sites-developing/spa-architecture.md) describe cómo involucrar a los desarrolladores de front-end para que desarrollen un SPA para AEM, así como cómo SPA interactúan con AEM arquitectura.
