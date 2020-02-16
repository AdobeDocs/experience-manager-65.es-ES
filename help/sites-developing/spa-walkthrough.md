---
title: Introducción y tutoriales de SPA
seo-title: Introducción y tutoriales de SPA
description: Este artículo introduce los conceptos de SPA y analiza el uso de una aplicación SPA básica para la creación, mostrando cómo se relaciona con el editor de SPA de AEM subyacente.
seo-description: Este artículo introduce los conceptos de SPA y analiza el uso de una aplicación SPA básica para la creación, mostrando cómo se relaciona con el editor de SPA de AEM subyacente.
uuid: 4b0a9e53-3892-4d60-8bd3-7ff740d2f137
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 0478afcb-b029-4ce6-b3e6-cee4bb5408ce
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# Introducción y tutoriales de SPA{#spa-introduction-and-walkthrough}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios del sitio web. Los desarrolladores quieren poder crear sitios con marcos de SPA y los autores quieren editar contenido dentro de AEM sin problemas para un sitio creado con dichos marcos.

El Editor de SPA ofrece una solución completa para admitir SPA dentro de AEM. En este artículo se explica cómo se relaciona con el Editor de SPA de AEM subyacente mediante una aplicación de SPA básica para la creación.

>[!NOTE]
>
>El Editor de SPA es la solución recomendada para proyectos que requieren procesamiento del cliente basado en el marco de SPA (por ejemplo, React o Angular).

## Introducción {#introduction}

### Objetivo del artículo {#article-objective}

Este artículo introduce los conceptos básicos de las SPA antes de guiar al lector a través de un tutorial del editor de SPA mediante una sencilla aplicación de SPA para mostrar la edición básica del contenido. A continuación, profundiza en la construcción de la página y en cómo se relaciona la aplicación SPA con el editor de AEM SPA y cómo interactúa con él.

El objetivo de esta introducción y este tutorial es demostrar a un desarrollador de AEM por qué los SPA son relevantes, cómo funcionan en general, cómo gestiona un SPA el Editor de AEM SPA y cómo difiere de una aplicación estándar de AEM.

El tutorial se basa en la funcionalidad estándar de AEM y en la aplicación de muestra We.Retail Journal. Deben cumplirse los siguientes requisitos:

* [AEM versión 6.4 con Service Pack 2 o posterior
   ](/help/release-notes/sp-release-notes.md)
* [Instale la aplicación de muestra We.Retail Journal disponible en GitHub aquí.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

### ¿Qué es un SPA? {#what-is-a-spa}

Una aplicación de una sola página (SPA) difiere de una página convencional en que se procesa en el lado del cliente y principalmente está dirigida por JavaScript, y depende de las llamadas de Ajax para cargar datos y actualizar la página de forma dinámica. La mayor parte o la totalidad del contenido se recupera una vez en una única carga de página con recursos adicionales cargados asincrónicamente según sea necesario según la interacción del usuario con la página.

Esto reduce la necesidad de actualizar la página y presenta al usuario una experiencia que es fluida, rápida y se parece más a una experiencia nativa de la aplicación.

El editor de SPA de AEM permite a los desarrolladores de front-end crear SPA que se pueden integrar en un sitio de AEM, lo que permite a los autores de contenido editar el contenido de SPA con la misma facilidad que cualquier otro contenido de AEM.

### ¿Por qué un SPA? {#why-a-spa}

Al ser más rápido, fluido y más parecido a una aplicación nativa, un SPA se convierte en una experiencia muy atractiva no sólo para el visitante de la página web, sino también para los especialistas en mercadotecnia y desarrolladores debido a la naturaleza del funcionamiento de los SPA.

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**Visitantes**

* Los visitantes desean experiencias nativas cuando interactúan con el contenido.
* Hay datos claros de que cuanto más rápida sea una página, más probabilidad habrá de producirse una conversión.

**Especialistas en mercadotecnia**

* Los especialistas en mercadotecnia desean ofrecer experiencias ricas y nativas para atraer visitantes a fin de que se involucren plenamente con el contenido.
* La personalización puede hacer que estas experiencias sean aún más atractivas.

**Desarrolladores**

* Los desarrolladores quieren una clara separación de las preocupaciones entre el contenido y la presentación.
* La separación limpia hace que el sistema sea más extensible y permite el desarrollo independiente del front-end.

### ¿Cómo funciona un SPA? {#how-does-a-spa-work}

La idea principal de un SPA es que las llamadas y la dependencia de un servidor se reducen para minimizar los retrasos causados por las llamadas al servidor de modo que el SPA se aproxime a la capacidad de respuesta de una aplicación nativa.

En una página web secuencial tradicional, solo se cargan los datos necesarios para la página inmediata. Esto significa que cuando el visitante se mueve a otra página, se llama al servidor para obtener los recursos adicionales. Es posible que sea necesario realizar llamadas adicionales a medida que el visitante interactúa con los elementos de la página. Estas llamadas múltiples pueden dar una sensación de retraso o retraso, ya que la página tiene que ponerse al día con las solicitudes del visitante.

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

Para una experiencia más fluida, que se aproxima a lo que un visitante espera de las aplicaciones móviles nativas, un SPA carga todos los datos necesarios para el visitante en la primera carga. Aunque esto puede tardar un poco más al principio, elimina la necesidad de llamadas al servidor adicionales.

Al realizar el procesamiento en el lado del cliente, el elemento de página reacciona más rápido y las interacciones con la página por parte del visitante son inmediatas. Cualquier dato adicional que se necesite se llama de forma asíncrona para maximizar la velocidad de la página.

>[!NOTE]
>
>Para obtener información técnica sobre cómo funcionan los SPA en AEM, consulte el artículo [Introducción a los SPA en AEM](/help/sites-developing/spa-getting-started-react.md).
>
>Para obtener una vista más detallada del diseño, la arquitectura y el flujo de trabajo técnico del Editor de SPA, consulte el artículo Información general [del Editor de](/help/sites-developing/spa-overview.md)SPA.

## Experiencia de edición de contenido con SPA {#content-editing-experience-with-spa}

Cuando se crea un SPA para aprovechar el Editor de SPA de AEM, el autor del contenido no observa ninguna diferencia al editar y crear contenido. La funcionalidad común de AEM está disponible y no se requieren cambios en el flujo de trabajo del autor.

>[!NOTE]
>
>El tutorial se basa en la funcionalidad estándar de AEM y en la aplicación de muestra We.Retail Journal. Deben cumplirse los siguientes requisitos:
>
>* [AEM versión 6.4 con Service Pack 2](/help/release-notes/sp-release-notes.md)
>* [Instale la aplicación de muestra We.Retail Journal disponible en GitHub aquí.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)
>



1. Edite la aplicación We.Retail Journal en AEM.

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at142533](assets/screen_shot_2018-06-07at142533.png)

1. Seleccione un componente de encabezado y observe que aparece una barra de herramientas como cualquier otro componente. Seleccione **Editar**.

   ![screen_shot_2018-06-07at142937](assets/screen_shot_2018-06-07at142937.png)

1. Edite el contenido como de costumbre en AEM y tenga en cuenta que los cambios se mantienen.

   ![screen_shot_2018-06-07at143419](assets/screen_shot_2018-06-07at143419.png)

1. Utilice el navegador de recursos para arrastrar y soltar una imagen nueva en un componente de imagen.

   ![screen_shot_2018-06-07at143530](assets/screen_shot_2018-06-07at143530.png)

1. El cambio se mantiene.

   ![screen_shot_2018-06-07at143732](assets/screen_shot_2018-06-07at143732.png)

Se admiten herramientas de creación adicionales como arrastrar y soltar componentes adicionales en la página, reorganizar componentes y modificar el diseño, como en cualquier aplicación que no sea de SPA.

>[!NOTE]
>
>El Editor de SPA no modifica el DOM de la aplicación. La SPA misma es responsable del DOM.
>
>Para ver cómo funciona, continúe con la sección siguiente de este artículo Aplicaciones de [SPA y con el Editor](/help/sites-developing/spa-walkthrough.md#spa-apps-and-the-aem-spa-editor)de AEM SPA.

## Aplicaciones de SPA y el Editor de SPA de AEM {#spa-apps-and-the-aem-spa-editor}

La experiencia de cómo se comporta un SPA para el usuario final y, a continuación, la inspección de la página de SPA ayuda a comprender mejor cómo funciona una aplicación SAP con el Editor de SPA en AEM.

### Uso de una aplicación SPA {#using-an-spa-application}

1. Cargue la aplicación We.Retail Journal en el servidor de publicación o con la opción **Ver como publicado** del menú Información **de** página del editor de páginas.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-08at102650](assets/screen_shot_2018-06-08at102650.png)

   Tenga en cuenta la estructura de las páginas, incluida la navegación a páginas secundarias, utilidades meteorológicas y artículos.

1. Navegue a una página secundaria mediante el menú y observe que la página se carga inmediatamente sin necesidad de actualizar.

   ![screen_shot_2018-06-08at102815](assets/screen_shot_2018-06-08at102815.png)

1. Abra las herramientas de desarrollador integradas de su navegador y supervise la actividad de la red a medida que navega por las páginas secundarias.

   ![screen_shot_2018-06-08at103922](assets/screen_shot_2018-06-08at103922.png)

   Hay muy poco tráfico a medida que se mueve de una página a otra en la aplicación. La página no se vuelve a cargar y solo se solicitan las imágenes nuevas.

   El SPA administra el contenido y el enrutamiento por completo en el lado del cliente.

Por lo tanto, si la página no se recarga al navegar por las páginas secundarias, ¿cómo se carga?

La siguiente sección, [Carga de una aplicación](/help/sites-developing/spa-walkthrough.md#loading-an-spa-application)SPA, explora en profundidad la mecánica de carga del SPA y cómo se puede cargar el contenido sincrónica y asincrónicamente.

### Carga de una aplicación SPA {#loading-an-spa-application}

1. Si aún no se ha cargado, cargue la aplicación We.Retail Journal en el servidor de publicación o con la opción **Ver como publicado** del menú Información **de** página del editor de páginas.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at144736](assets/screen_shot_2018-06-07at144736.png)

1. Utilice la herramienta integrada de su navegador para ver el origen de la página.
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

   Esta secuencia de comandos de React es el controlador principal de esta aplicación y es responsable de procesar todo el contenido.

1. Utilice las herramientas integradas del explorador para inspeccionar la página. Consulte el contenido del DOM completamente cargado.

   ![screen_shot_2018-06-07at151848](assets/screen_shot_2018-06-07at151848.png)

1. Cambie a la ficha Red del Inspector y vuelva a cargar la página.

   Al omitir las solicitudes de imagen, tenga en cuenta que los recursos principales cargados para la página son la página misma, CSS, React Javascript, sus dependencias y los datos JSON de la página.

   ![screen_shot_2018-06-07at152155](assets/screen_shot_2018-06-07at152155.png)

1. Cargue el `react.model.json` en una nueva ficha.

   `/content/we-retail-journal/react.model.json`

   ![screen_shot_2018-06-07at152636](assets/screen_shot_2018-06-07at152636.png)

   El Editor de SPA de AEM aprovecha los servicios [de contenido de](/help/assets/content-fragments.md) AEM para ofrecer todo el contenido de la página como un modelo JSON.

   Al implementar interfaces específicas, los modelos Sling proporcionan la información necesaria para el SPA. El envío de los datos de JSON se delega hacia abajo en cada componente (de página, párrafo, componente, etc.).

   Cada componente elige lo que expone y cómo se procesa (lado del servidor con HTL o lado del cliente con React). Por supuesto, este artículo se centra en la representación del lado del cliente con React.

1. El modelo también puede agrupar las páginas para que se carguen sincrónicamente, reduciendo el número de recargas de página necesarias.

   En el ejemplo de We.Retail Journal, las páginas `home`, `blog`y `aboutus` se cargan sincrónicamente, ya que los visitantes suelen visitar todas esas páginas. Sin embargo, la página `weather` se carga asincrónicamente, ya que es menos probable que los visitantes la visiten.

   Este comportamiento no es obligatorio y es totalmente definible.

   ![screen_shot_2018-06-07at153945](assets/screen_shot_2018-06-07at153945.png)

1. Para ver esta diferencia de comportamiento, vuelva a cargar la página y borre la actividad de red del inspector. Vaya al blog y a las páginas de uso en el menú de la página y vea que no se ha informado de ninguna actividad de red.

   Vaya a la página del tiempo y vea que la llamada `weather.model.json` se realiza de forma asíncrona.

   ![screen_shot_2018-06-07at155738](assets/screen_shot_2018-06-07at155738.png)

### Interacción con el Editor de SPA {#interaction-with-the-spa-editor}

Con la aplicación de muestra We.Retail Journal, queda claro cómo se comporta y se carga la aplicación cuando se publica, aprovechando los servicios de contenido para la entrega de contenido JSON, así como la carga asincrónica de recursos.

Además, para el autor del contenido, la creación de contenido mediante un editor de SPA es perfecta dentro de AEM.

En la siguiente sección analizaremos el contrato que permite al Editor de SPA relacionar componentes dentro de SPA con componentes de AEM y lograr esta experiencia de edición sin problemas.

1. Cargue la aplicación We.Retail Journal en el editor y cambie al modo de **vista previa** .

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

1. Con las herramientas de desarrollador integradas del explorador, inspeccione el contenido de la página. Con la herramienta de selección, seleccione un componente editable en la página y vea los detalles del elemento.

   Tenga en cuenta que el componente tiene un nuevo atributo de datos `data-cq-data-path`.

   ![screen_shot_2018-06-08at095124](assets/screen_shot_2018-06-08at095124.png)

   Por ejemplo

   `data-cq-data-path="root/responsivegrid/paragraph_1`

   Esta ruta permite recuperar y asociar el objeto de configuración de contexto de edición de cada componente.

   Este es el único atributo de marcado necesario para que el editor reconozca este componente como un componente editable dentro del SPA. Según este atributo, el Editor de SPA determinará qué configuración editable está asociada al componente, de modo que el marco, la barra de herramientas, etc. correctos. está cargado.

   Algunos nombres de clase específicos también se agregan para marcar marcadores de posición y para la funcionalidad de arrastrar y soltar recursos.

   >[!NOTE]
   >
   >Se trata de un cambio en el comportamiento de las páginas procesadas del lado del servidor en AEM, donde hay un `cq` elemento insertado para cada componente editable.
   >
   >
   >Este enfoque en SPA elimina la necesidad de inyectar elementos personalizados, confiando solamente en un atributo de datos adicional, lo que simplifica el marcado para el desarrollador de front-end.

## Próximos pasos {#next-steps}

Ahora que comprende la experiencia de edición de SPA en AEM y cómo se relaciona un SPA con el Editor de SPA, puede comprender mejor cómo se crea un SPA.

* [Introducción a los SPA en AEM](/help/sites-developing/spa-getting-started-react.md) muestra cómo se crea un SPA básico para trabajar con el Editor de SPA en AEM
* [La descripción general](/help/sites-developing/spa-overview.md) del Editor de SPA profundiza en el modelo de comunicación entre AEM y SPA.
* [Developing SPAs for AEM](/help/sites-developing/spa-architecture.md) describe cómo interactuar con los desarrolladores de front-end para desarrollar un SPA para AEM, así como cómo interactúan los SPA con la arquitectura de AEM.
