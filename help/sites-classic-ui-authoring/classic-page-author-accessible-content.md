---
title: Crear contenido accesible (Conformidad con WCAG 2.0)
seo-title: Crear contenido accesible (Conformidad con WCAG 2.0)
description: WCAG 2.0 consiste en un conjunto de directrices tecnológicas independientes y criterios de éxito para ayudar a crear contenido web accesible para, y utilizable por, personas con discapacidades.
seo-description: WCAG 2.0 consiste en un conjunto de directrices tecnológicas independientes y criterios de éxito para ayudar a crear contenido web accesible para, y utilizable por, personas con discapacidades.
page-status-flag: de-activated
uuid: c2c0cac0-2a9f-478d-8261-e8cc894aae34
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 378bc33d-ab6c-4651-9688-102c961561fc
translation-type: tm+mt
source-git-commit: df992fc0204519509c4662a7d4315939af2fc92c
workflow-type: tm+mt
source-wordcount: '9241'
ht-degree: 94%

---


# Crear contenido accesible (Conformidad con WCAG 2.0){#creating-accessible-content-wcag-conformance}

>[!CAUTION]
>
>Dado que la IU clásica quedó obsoleta en AEM 6.4, el contenido de esta página no se ha actualizado para WCAG 2.1.
>
>Consulte las páginas siguientes para obtener más información sobre AEM y WCAG 2.1:
>
>* [AEM y las directrices de accesibilidad web](/help/managing/web-accessibility.md) 
>* [Guía rápida de WCAG 2.1](/help/managing/qg-wcag.md)
>* [Crear contenido accesible (Conformidad con WCAG 2.1)](/help/sites-authoring/creating-accessible-content.md)


WCAG 2.0 consiste en un conjunto de directrices tecnológicas independientes y criterios de éxito para ayudar a crear contenido web accesible para, y utilizable por, personas con discapacidades.

>[!NOTE]
>
>Consulte también:
>
>* nuestra [Guía rápida para WCAG 2.0](/help/managing/qg-wcag.md) si desea más información
>* [Configurar el Editor de texto enriquecido para producir contenido accesible](/help/sites-administering/rte-accessible-content.md)

>



Se clasifican según tres niveles de conformidad: Nivel A (el más bajo), Nivel AA y Nivel AAA (el más alto). Brevemente, los niveles se definen de la siguiente manera:

* **Nivel A:** El sitio alcanza un nivel básico y mínimo de accesibilidad. Para alcanzar este nivel, se cumplen todos los criterios de éxito del nivel A.
* **Nivel AA:** Se trata de un nivel ideal de accesibilidad en el que su página alcanza un nivel mejorado de accesibilidad, por lo que resulta accesible para mucha gente, en muchas situaciones y utilizando distintas tecnologías. Para alcanzar este nivel, se deben cumplir todos los criterios de éxito de los niveles A y niveles AA.
* **Nivel AAA:** Su sitio alcanza un nivel muy alto de accesibilidad. Para alcanzar este nivel, se cumplen todos los criterios de éxito de los niveles A, AA y AAA.

Al crear su sitio, debe determinar el nivel general en el que desea que se ajuste.

La siguiente sección presenta las [directrices WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines) con criterios de éxito vinculados a los [niveles de conformidad](https://www.w3.org/TR/UNDERSTANDING-WCAG20/conformance.html) de los niveles A y AA.

>[!NOTE]
>
>Como no se pueden satisfacer todos los criterios de éxito del Nivel AAA para ciertos tipos de contenido, no es recomendable pedir este nivel de conformidad como política general.

>[!NOTE]
>
>En este documento utilizamos:
>
>* Nombres abreviados para las [directrices WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines)
>* Numeración utilizada en las [directrices WCAG 2.0](https://www.w3.org/TR/WCAG20/#guidelines) para apoyar las referencias cruzadas en la página web de WCAG

>



## Principio 1: perceptible  {#principle-perceivable}

[Principio 1: perceptible. Los componentes de la interfaz de usuario y de la información se deben presentar a los usuarios de forma perceptible.](https://www.w3.org/TR/WCAG20/#perceivable)

### Alternativas de texto (1.1)      {#text-alternatives}

[Directrices 1.1 Alternativas de texto: proporciona alternativas de texto para cualquier contenido no textual para cambiarlo por otras formas según sea necesario, como letras grandes, braille, voz, símbolos o lenguaje más sencillo.](https://www.w3.org/TR/WCAG20/#text-equiv)

### Contenido no textual (1.1.1)      {#non-text-content}

* Criterios de éxito 1.1.1
* Nivel A
* Contenido no textual: todo contenido no textual que se presenta al usuario tiene una alternativa de texto que cumple el objetivo equivalente, excepto para las situaciones que se detallan a continuación

#### Objetivo: Contenido no textual (1.1.1) {#purpose-non-text-content}

La información en una página web se puede proporcionar en muchos formatos no textuales distintos, como fotografías, vídeos, animaciones, tablas y gráficos. Las personas ciegas o con deficiencias visuales graves no pueden ver el contenido no textual, pero pueden acceder al contenido textual si lo lee en voz alta un lector de pantalla o si se presenta en un formato táctil a través de un dispositivo de visualización braille. Por ello, al proporcionar alternativas textuales para el contenido en formato gráfico, quienes no puedan ver el contenido gráfico podrán acceder a una versión equivalente de la información que proporcione el contenido.

Un beneficio útil adicional es que las alternativas textuales permiten indexar contenido no textual mediante una tecnología de buscadores.

#### Cómo cumplir: Contenido no textual (1.1.1)      {#how-to-meet-non-text-content}

Para gráficos estáticos, el requisito principal es proporcionar una alternativa textual equivalente para el gráfico. Esto se puede llevar a cabo en el campo **Texto alternativo:**

>[!NOTE]
>
>Algunos componentes listos para usar, como **Carrusel** y **Presentación de diapositivas,** no proporcionan los medios para añadir descripciones de texto alternativas a las imágenes. Cuando se implementan versiones de estos componentes para su instancia de AEM, su equipo de desarrollo debe configurarlos para dar soporte al atributo `alt`[ y para que así los autores puedan añadirlo al contenido (consulte Añadir soporte para elementos y atributos HTML adicionales](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

El campo **Texto alternativo** se encuentra disponible en la pestaña de propiedades de la imagen **Avanzado** del cuadro de diálogo del componente **Imagen:**

![Cuadro de diálogo de edición del componente Imagen en la IU clásica; muestra el campo Texto alternativo.](assets/chlimage_1-17a.png)

AEM añade un **Texto alternativo** a sus imágenes por defecto. Para la IU clásica, existen dos escenarios distintos para crear el atributo por defecto (aunque puede que el valor por defecto no sea suficiente como alternativa y se deba editar en la pestaña **Avanzado** en propiedades de la imagen):

* Archivo:

   Se carga una imagen desde el disco duro del usuario. Si agrega un componente de imagen a una página y luego elige una imagen de su disco duro u otra fuente, el valor predeterminado para **Texto alternativo** es `file`. Se deberá cambiar en la pestaña **Avanzado** en propiedades de la imagen. De nuevo, este valor no se mostrará en el campo **Texto alternativo** pero, cuando se cambie el valor, el nuevo aparecerá en el campo.

* Recurso:

   Se agrega una imagen desde el repositorio de recursos digitales. Si arrastra una imagen del repositorio de recursos digital hasta la página web, los valores de **Título** y **Texto alternativo** para dicha imagen se tomarán de los metadatos de la misma.

>[!NOTE]
>
>En ambos casos, el valor predeterminado **Texto alternativo** no está visible en la ficha **Propiedades avanzadas de la imagen**. Para cambiar el valor predeterminado, simplemente introduzca un nuevo valor en el campo **Texto alternativo**.

>[!NOTE]
>
>Si la imagen es puramente decorativa (consulte [Crear buenas alternativas de texto](#creating-good-text-alternatives)), puede introducir un espacio en blanco en el campo **Texto alternativo** utilizando la barra espaciadora. Esto creará un atributo `alt` vacío, que solicitará a un lector de pantalla que ignore la imagen.

#### Crear buenas alternativas de texto {#creating-good-text-alternatives}

Existen distintos tipos de contenido no textual, por lo que el valor de la alternativa textual depende del papel que juegue el elemento gráfico en la página web. Algunas de las normas generales a seguir incluyen:

* Las alternativas textuales deben ser precisas pero también deben recoger con claridad la información esencial proporcionada por el contenido no textual. 
* Deben evitarse las descripciones demasiado largas (que superen los 100 caracteres). Si una alternativa textual requiere más detalle:

   * proporcione una breve descripción en el texto alternativo
   * y añada una descripción más larga en el texto en cualquier otra parte, en la misma página o en una página web aparte. Cree un vínculo a esta descripción en la imagen o a través de un texto vinculante adyacente a la imagen.

* El texto alternativo no debe repetir el contenido proporcionado en el texto de la misma página. Muchas imágenes son ilustraciones de puntos que ya se han cubierto en el texto de la página, por lo que puede que ya exista una alternativa textual detallada.
* Si el contenido no textual es un vínculo a otra página o documento y no hay otro texto que forme parte del mismo vínculo, entonces el texto alternativo para la imagen debe indicar el destino del vínculo en lugar de describir la imagen.
* Si el contenido no textual está contenido en un botón y no hay texto que forme parte del mismo botón, entonces el texto alternativo de la imagen debe indicar la funcionalidad del botón, en lugar de describir la imagen.
* Es perfectamente aceptable que se dé a una imagen un texto alternativo vacío (nulo), pero solo si la imagen no tiene texto alternativo (por ejemplo, si es un elemento gráfico puramente decorativo) o si el texto equivalente ya existe en la página textual.

El borrador [W3C: HTML5 Técnicas para proporcionar alternativas textuales útiles](https://dev.w3.org/html5/alt-techniques/) contiene más detalles y ejemplos de provisiones de texto alternativo apropiado para imágenes de distintos tipos.

Los tipos específicos de contenido no textual que requieren alternativas textuales pueden incluir:

* Fotos ilustrativas:

   Son imágenes de personas, objetos o lugares. Piensen en el papel de la foto en la página; es probable que un equivalente textual adecuado sea *Foto de [objeto]*, pero puede depender del texto que lo rodea.

* Iconos:

   Estos son pequeños pictogramas (gráficos) que transmiten información específica. Se deben utilizar de manera consistente en una página o sitio. Todos los ejemplos del icono en una página o sitio deben contener el mismo texto alternativo, corto y preciso, a menos que se duplique innecesariamente el texto adyacente.

* Gráficos y gráficos:

   Normalmente representan datos numéricos. Una opción para proporcionar una alternativa textual podría ser incluir un breve resumen de las tendencias principales que se muestran en la tabla o en el gráfico. Si es necesario, proporcione también una descripción más detallada en el texto mediante el campo **Descripción** de la ficha **Propiedades de imagen avanzadas**. Además, puede proporcionar los datos de origen en formato tabulado en cualquier otra parte de la página o sitio.

   ![Ejemplo de gráfico. Debajo se representa el mejor enfoque para proporcionar una alternativa.](assets/chlimage_1-2a.jpeg)

   Para proporcionar una alternativa para este gráfico de ejemplo, agregue un texto conciso `alt` a la propia imagen y, a continuación, siga la imagen con una alternativa textual completa.

   ```xml
   <p><img src="figure1.gif" alt="Figure 1" ></p>
   <p> Figure 1. Distribution of Articles by Journal Category.
   Pie chart: Language=68%, Education=14% and Science=18%.</p>
   ```

   >[!NOTE]
   >
   >El fragmento anterior solo se utiliza para ilustrar el orden. Se recomienda utilizar el componente **Imagen** (en lugar de la referencia `img src` utilizada anteriormente.

   Esto se puede hacer en AEM mediante la combinación de los campos **Texto alternativo** y **Descripción** en el cuadro de diálogo de configuración de la imagen, como en [Contenido no textual (1.1.1)](#how-to-meet-non-text-content).

* Mapas, diagramas, diagramas de flujo:

   Para gráficos que proporcionan datos espaciales (por ejemplo, para admitir la descripción de relaciones entre objetos o un proceso), compruebe que el mensaje clave se proporciona en formato de texto.  En el caso de los mapas, es probable que no sea práctico proporcionar un equivalente textual completo, pero si el mapa se proporciona como una forma de ayudar a las personas a encontrar su camino a una ubicación determinada, el texto alternativo de la imagen del mapa puede indicar brevemente *Mapa de X* y, a continuación, proporcionar direcciones a esa ubicación en texto en cualquier parte de la página o a través del campo **Descripción** en la pestaña **Avanzado** del componente **Imagen**.

* CAPTCHA:

   CAPTCHA es una *prueba de Turing pública completamente automatizada para distinguir entre ordenadores y humanos*. Es una medida de seguridad que se utiliza en páginas web para distinguir a humanos de software maligno, pero que puede originar barreras de accesibilidad. Se trata de imágenes que requieren que los usuarios describan lo que ven para pasar una prueba de seguridad. Como obviamente no es posible proporcionar una alternativa textual para la imagen, en lugar de ello tendrá que considerar una solución alternativa que no sea gráfica.‪


   W3C proporciona varias sugerencias como: Cada uno de estos enfoques tiene sus propias ventajas e inconvenientes.‪

   * Rompecabezas de lógica
   * Salida de sonido en lugar de imágenes
   * Cuentas de uso limitado y filtros de spam

* Imágenes de fondo:

   Se consiguen utilizando hojas de estilo en cascada (CSS) en lugar de HTML. Esto quiere decir que no se puede especificar un valor de texto alternativo. Por lo tanto, las imágenes de fondo no deben proporcionar información textual importante; si lo hacen, esta información también debe proporcionarse en el texto de la página.

   Sin embargo, es importante que se muestre un fondo alternativo cuando la imagen no se pueda mostrar.

   >[!NOTE]
   >
   >Debe haber un nivel adecuado de contraste entre el fondo y el texto en primer plano; este es un tema que se analiza en detalle en [Contraste (Mínimo) (1.4.3)](#contrast-minimum).

#### Más información: Contenido no textual (1.1.1)      {#more-information-non-text-content}

* [Entender los criterios de éxito 1.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html)
* [Cumplir los criterios de éxito 1.1.1](https://www.w3.org/WAI/WCAG20/quickref/#text-equiv)
* [W3C: Técnicas HTML5 para proporcionar alternativas textuales de éxito (borrador)](https://dev.w3.org/html5/alt-techniques/)
* [Explicación de W3C y alternativas para CAPTCHA](https://www.w3.org/TR/turingtest/)

### Medios basados en el tiempo (1.2)      {#time-based-media}

[Directrices 1.2 Medios basados en el tiempo: proporcionar alternativas para medios basados en el tiempo.](https://www.w3.org/TR/WCAG20/#text-equiv)

Trata el contenido de la página web *basado en el tiempo*. Abarca el contenido que puede reproducir el usuario (como vídeos, audios y contenido animado) y se puede pregrabar o reproducir en vivo.

### Solo audio y solo vídeo (pregrabado) (1.2.1)   {#audio-only-and-video-only-pre-recorded}

* Criterios de éxito 1.2.1
* Nivel A
* Solo audio y Solo vídeo (pregrabado): para medios de solo audio y solo vídeo pregrabado, la siguiente información es cierta, excepto cuando el audio o el vídeo es una alternativa para texto y se etiqueta claramente como:

   * Solo audio pregrabado: se proporciona una alternativa para medios basados en el tiempo que presenta información equivalente para contenido de solo audio pregrabado.
   * Solo vídeo pregrabado: se proporciona una alternativa para medios basados en el tiempo o una pista de audio que presenta información equivalente para contenido de solo vídeo pregrabado.

#### Objetivo: solo audio y Solo vídeo (pregrabado) (1.2.1)   {#purpose-audio-only-and-video-only-pre-recorded}

Se pueden dar problemas de accesibilidad para vídeo y audio a través de:

* Personas con discapacidades visuales cuando no hay banda sonora o cuando la banda sonora no basta para informar de lo que está sucediendo en el vídeo o animación;
* Personas con discapacidades auditivas o sordera, que no pueden oír la banda sonora;
* Personas que pueden oír la banda sonora, pero que no entienden lo que se dice (por ejemplo, porque está en un idioma que no entienden).

También puede que el vídeo o el audio no se encuentre disponible para las personas que utilizan navegadores o dispositivos en los que no se puede reproducir contenido en formatos específicos, como Adobe Flash.

Proporcionar esta información en un formato diferente, como texto (o audio para vídeo sin audio) puede ser una manera accesible para personas que no pueden acceder al contenido original.

#### Cómo cumplir: Solo audio y solo vídeo (pregrabado) (1.2.1)   {#how-to-meet-audio-only-and-video-only-pre-recorded}

* Si el contenido es audio pregrabado sin vídeo (como podcast):

   * Proporcione un enlace inmediatamente antes o después del contenido para una transcripción textual del contenido del audio.

      La transcripción debe ser una página HTML con un texto equivalente a todo el contenido hablado o no hablado importante, además de una indicación de quién habla, una descripción del escenario, expresiones vocales y una descripción de cualquier otro audio significativo.

* Si el contenido es una animación o un vídeo pregrabado sin audio:

   * Proporcione un vínculo inmediatamente antes o después del contenido para una descripción textual equivalente de la información proporcionada por el vídeo.
   * O bien, una descripción de audio equivalente en un formato de audio comúnmente utilizado, como un MP3.

>[!NOTE]
>
>Si el contenido del audio o vídeo se proporciona como una alternativa que ya existe en otro formato en una página web, no es necesario seguir los requisitos descritos anteriormente. Por ejemplo, si un vídeo ilustra una lista de instrucciones textuales, este vídeo no requiere ninguna alternativa ya que las instrucciones del texto funcionan ya como alternativa para el vídeo.

Insertar contenido multimedia, en concreto contenido Flash, en sus páginas web AEM es parecido a insertar una imagen. Sin embargo, como el contenido multimedia es mucho mayor que una imagen estática, existe una gran variedad de opciones y escenarios para controlar cómo se reproduce el contenido multimedia.

>[!NOTE]
>
>Al utilizar contenido multimedia con contenido informativo, también se deben crear vínculos a opciones alternativas. Por ejemplo, para incluir una transcripción textual, cree una página HTML para reproducir la transcripción y añada un vínculo debajo o junto al contenido del audio.

#### Más información: Solo audio y solo vídeo (pregrabado) (1.2.1) {#more-information-audio-only-and-video-only-pre-recorded}

* [Entender los criterios de éxito 1.2.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html)
* [Cumplir los criterios de éxito 1.2.1](https://www.w3.org/WAI/WCAG20/quickref/#media-equiv)

### Subtítulos (pregrabados) (1.2.2)   {#captions-pre-recorded}

* Criterios de éxito 1.2.2
* Nivel A
* Subtítulos (pregrabados): se proporcionan los subtítulos para todo el contenido de audio pregrabado en medios sincronizados, excepto cuando los medios son una alternativa para el texto y se etiquetan claramente como tal.

#### Objetivo: subtítulos (pregrabados) (1.2.2)   {#purpose-captions-pre-recorded}

Las personas sordas o con dificultades auditivas no podrán acceder, o tendrán grandes dificultades para acceder, al contenido de audio. Los subtítulos son equivalentes textuales para audio verbal y no verbal que se muestran en la pantalla en el momento apropiado durante el vídeo. Permiten entender lo que está ocurriendo a las personas que no pueden oír el audio.

>[!NOTE]
>
>No se requieren subtítulos donde los equivalentes textuales o no textuales (que directamente proporcionan información equivalente) se muestran disponibles en la misma página que el vídeo o la animación.

#### Cómo cumplir: Subtítulos (pregrabados) (1.2.2)   {#how-to-meet-captions-pre-recorded}

Los subtítulos pueden ser:

* Abiertos: siempre visibles cuando se reproduce el vídeo)
* Cerrados: el usuario puede activar o desactivar los subtítulos

Utilice subtítulos cerrados siempre que sea posible, ya que proporciona a los usuarios la opción de verlos o de no verlos.

Para los subtítulos cerrados necesitará crear y proporcionar un archivo de subtítulos sincronizados en un formato adecuado (como [SMIL](https://www.w3.org/AudioVideo/)) a lo largo del archivo de vídeo (los detalles de cómo hacerlo van más allá de esta guía, pero hemos proporcionado enlaces a varios tutoriales en [Más información: Subtítulos (pregrabados) (1.2.2)](#more-information-captions-pre-recorded)). Proporcione una nota a los usuarios para que sepan que los subtítulos están disponibles para el vídeo.

Si necesita utilizar subtítulos abiertos, incorpore el texto en la pista de vídeo. Esto se puede conseguir utilizando aplicaciones de edición de vídeo que permiten superponer títulos en el vídeo.

#### Más información: Subtítulos (pregrabados) (1.2.2)   {#more-information-captions-pre-recorded}

* [Entender los criterios de éxito 1.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html):
* [Cumplir los criterios de éxito 1.2.2](https://www.w3.org/WAI/WCAG20/quickref/#media-equiv)
* [W3C: Medios multimedia sincronizados](https://www.w3.org/AudioVideo/)
* [Subtítulos, transcripciones y descripciones de audio: por WebAIM](https://webaim.org/techniques/captions/)

### Descripción del audio o medios alternativos (pregrabados) (1.2.3)   {#audio-description-or-media-alternative-pre-recorded}

* Criterios de éxito 1.2.3
* Nivel A
* Descripción del audio o medios alternativos (pregrabados): se proporciona una alternativa para medios basados en el tiempo o descripción del audio del contenido de vídeo pregrabado para medios sincronizados, excepto cuando el medio es una alternativa para el texto y se etiqueta claramente como tal

#### Objetivo: Descripción del audio o medios alternativos (pregrabados) (1.2.3)   {#purpose-audio-description-or-media-alternative-pre-recorded}

Las personas ciegas o con dificultades de visión experimentarán barreras de accesibilidad si la información en un vídeo o animación solo se proporciona de manera visual, o si la banda sonora no proporciona información suficiente para poder entender lo que está pasando visualmente.

#### Cómo cumplir: Descripción del audio o medios alternativos (pregrabados) (1.2.3)   {#how-to-meet-audio-description-or-media-alternative-pre-recorded}

Se pueden adoptar dos métodos para cumplir este criterio de éxito. Cualquiera de los dos es aceptable:

1. Incluir una descripción de audio adicional para el contenido del vídeo. Esto se puede lograr de una de las tres maneras siguientes:

   * Durante pausas en el diálogo existente, proporcionando información sobre los cambios en la escena que no se presentan como parte de la pista de audio existente;
   * Proporcionando una pista de audio nueva, adicional y optativa, que contenga la banda sonora original, pero incluyendo también información de audio adicional sobre los cambios en la escena.

      * Esto permitirá a los usuarios cambiar de la pista de audio existente (que *no* contiene una descripción del audio) a la nueva pista de audio (que *sí* contiene una descripción del audio).
      * Evita interrupciones a los usuarios que no necesitan la descripción adicional.
   * Creando una segunda versión del contenido del vídeo que permita descripciones de audio extendidas. Reduce las dificultades que se asocian al proporcionar descripciones de audio detalladas en los huecos entre el diálogo existente, mediante pausas temporales en el audio y en el vídeo en puntos adecuados. El resultado es una descripción del audio mucho más larga antes de que se retomen las acciones. Como en el ejemplo anterior, esta opción resulta mejor como una pista de audio adicional y opcional para prevenir interrupciones a los usuarios que no necesitan la descripción adicional.


1. Proporcionar una transcripción del texto que sea adecuada al equivalente textual del audio y a los elementos visuales del vídeo o animación. Donde resulte necesario se deberá incluir una indicación de quién está hablando, una descripción del entorno y de las expresiones vocales. Según la longitud, se puede colocar la transcripción en la misma página del vídeo o de la animación o en una página aparte; si se elige esta última opción, se debe proporcionar un vínculo a la transcripción adyacente al vídeo o animación.

Los detalles exactos de cómo crear vídeos descritos por audio quedan fuera del alcance de esta guía. Crear descripciones de vídeo y audio puede llevar mucho tiempo, pero otros productos de Adobe pueden ayudarle a realizar estas tareas. Al crear contenido con Adobe Flash Professional, también se debe crear un guión para recordar al usuario que puede descargar el programa adicional adecuado y proporcionar una alternativa textual a través del elemento `<noscript>`.

#### Más información: Descripción del audio o medios alternativos (pregrabados) (1.2.3) {#more-information-audio-description-or-media-alternative-pre-recorded}

* [Entender los criterios de éxito 1.2.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html)
* [Cumplir los criterios de éxito 1.2.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-audio-desc)
* [Adobe Encore CS5](https://helpx.adobe.com/es/premiere-pro/using/whats-new.html)

### Subtítulos (en vivo) (1.2.4)    {#captions-live}

* Criterios de éxito 1.2.4
* Nivel AA
* Subtítulos (en vivo): se proporcionan subtítulos para todo el contenido de audio en vivo en medios sincronizados.

#### Objetivo: Subtítulos (en vivo) (1.2.4)      {#purpose-captions-live}

Este criterio de éxito es idéntico al de [Subtítulos (pregrabados)](#captions-pre-recorded) puesto que se enfrenta a las barreras de accesibilidad que experimentan las personas sordas o que sufren deficiencias auditivas, excepto por el hecho de que este criterio de éxito trata las presentaciones en vivo tales como retransmisiones vía Internet.

#### Cómo cumplir: Subtítulos (en vivo) (1.2.4) {#how-to-meet-captions-live}

Siga las directrices proporcionadas para [Subtítulos (pregrabados)](#captions-pre-recorded) descritas arriba. Debido a la naturaleza del medio, la provisión de subtítulos se tiene que crear tan rápido como sea posible y como respuesta a lo que está sucediendo. Por eso es necesario considerar la posibilidad de utilizar subtítulos a tiempo real o herramientas de función de voz a texto.

Las instrucciones detalladas van más allá del alcance de este documento, pero los siguientes recursos proporcionan información útil:

* [WebAIM: Subtítulos a tiempo real](https://www.webaim.org/techniques/captions/realtime.php)
* [AccessIT (Universidad de Washington): ¿Se pueden generar subtítulos de manera automática utilizando el reconocimiento de voz?](https://www.washington.edu/accessit/articles?1209)

#### Más información: Subtítulos (en vivo) (1.2.4)      {#more-information-captions-live}

* [Entender los criterios de éxito 1.2.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html)
* [Cumplir los criterios de éxito 1.2.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-real-time-captions)

### Descripción del audio (pregrabado) (1.2.5)           {#audio-description-pre-recorded}

* Criterios de éxito 1.2.5
* Nivel AA
* Descripción del audio (pregrabado): la descripción del audio se proporciona para todos los contenidos de vídeo pregrabados en medios sincronizados

#### Objetivo: Descripción del audio (pregrabado) (1.2.5)      {#purpose-audio-description-pre-recorded}

Este criterio de éxito es idéntico al de [Descripción del audio o medios alternativos (pregrabados)](#audio-description-or-media-alternative-pre-recorded), excepto por el hecho de que los autores deben proporcionar una descripción del audio mucho más detallada para ajustarse al Nivel AA.

#### Cómo cumplir: Descripción del audio (pregrabado) (1.2.5)   {#how-to-meet-audio-description-pre-recorded}

Siga las directrices que se proporcionan para la [Descripción del audio o medios alternativos (pregrabados)](#audio-description-or-media-alternative-pre-recorded).

#### Más información: Descripción del audio (pregrabado) (1.2.5)      {#more-information-audio-description-pre-recorded}

* [Entender los criterios de éxito 1.2.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html)
* [Cumplir los criterios de éxito 1.2.5](https://www.w3.org/WAI/WCAG20/quickref/#qr-media-equiv-audio-desc-only)

### Adaptable (1.3)      {#adaptable}

[Directrices 1.3 Adaptable: crear contenido que se pueda presentar de distintas maneras (por ejemplo en un diseño sencillo) sin que pierda información o estructura.](https://www.w3.org/TR/WCAG20/#content-structure-separation)

Estas directrices engloban los requisitos necesarios para apoyar a quienes:

* no pueden acceder a la información de la manera en que la presenta el autor, con un diseño estándar de dos dimensiones, varias columnas y en una página web a color;

* utilizan una representación de solo audio o una alternativa visual, como un texto largo o un gran contraste.

### Información y relaciones (1.3.1)     {#info-and-relationships}

* Criterios de éxito 1.3.1
* Nivel A
* Información y relaciones: la información, estructura y relaciones en presentaciones se puede determinar mediante un programa o puede estar disponible en formato texto

#### Objetivo: Información y relaciones (1.3.1)      {#purpose-info-and-relationships}

Muchas tecnologías de asistencia que utilizan las personas con discapacidades cuentan con información estructural para que se pueda reproducir el contenido de salida de manera eficaz. Esta información estructural se puede presentar en forma de titulares de página, titulares en tablas o columnas y en lista. Por ejemplo, un lector de pantalla permite a un usuario navegar por una página de titular en titular. Sin embargo, cuando el contenido de una página solo parece contener una estructura a través de un estilo visual, en lugar de un formato HTML subyacente, quiere decir que no existe ninguna información estructural disponible para tecnologías de asistencia, lo que limita su capacidad de proporcionar una búsqueda más sencilla.

Este criterio de éxito pretende asegurar que esta información estructural se proporciona a través de HTML para que los buscadores y las tecnologías de asistencia puedan acceder a la información y aprovecharla.

#### Cómo cumplir: Información y relaciones (1.3.1)   {#how-to-meet-info-and-relationships}

AEM facilita construir páginas web utilizando los elementos HTML adecuados. Abra el contenido de su página en RTE (un componente de texto) y utilice el menú **Formato** para especificar el elemento estructural adecuado (por ejemplo, párrafos, titulares, etc.).

La imagen siguiente muestra el texto que se ha diseñado en párrafos; el código fuente que se utiliza muestra que contiene las etiquetas correctas de apertura y cierre &lt;p> y &lt;/p>.

![Ejemplo del elemento Párrafo que se muestra en el modo de edición de la fuente (IU clásica).](assets/chlimage_1-18a.png)

Puede comprobar que sus páginas web contienen la estructura adecuada mediante:

* **Uso de encabezados:**

   Siempre que tenga habilitadas las características de accesibilidad del RTE (consulte [AEM y accesibilidad](/help/sites-administering/rte-accessible-content.md)), AEM ofertas 3 niveles de encabezado de página. Puede utilizarlas para identificar secciones y subsecciones de contenido. El encabezado 1 es el nivel más alto, mientras que el encabezado 3 es el más bajo. El administrador del sistema puede configurar el sistema para permitir el uso de más niveles de encabezado.

   La imagen siguiente muestra un ejemplo de los distintos tipos de encabezados.

   ![Los Encabezados H1 hasta H3 que se muestran en el selector desplegable (IU clásica).](assets/chlimage_1-19a.png)

* **Texto enfatizado**:

   Utilice el elemento &lt;strong> o &lt;em> para dar énfasis. No utilice encabezados o texto enfatizado en los párrafos.

   * Enfatice el texto que quiera remarcar;
   * Haga clic en el icono **B** (para &lt;strong>) o en el icono **I** (para &lt;em>) que se muestra en el panel **Propiedades** (asegúrese de que HTML está seleccionado).

   >[!NOTE]
   >
   >RTE en una instalación AEM estándar está configurada para utilizar:
   >
   >* &lt;b> para &lt;strong>
   * &lt;i> para &lt;em>

   Aunque son igual de eficaces, &lt;strong> y &lt;em> son preferibles porque son HTML semánticamente correctos. Su equipo de desarrollo puede configurar el RTE para utilizar &lt;strong> y &lt;em> (en lugar de &lt;b> y &lt;i>) cuando desarrolle su proyecto.

* **Utilizar listas**:
Es posible utilizar HTML para especificar tres tipos de listas distintas.

   * El elemento `<ul>` se utiliza para listas *sin ordenar* listas (con viñetas). Los elementos de listas individuales se identifican utilizando el elemento `<li>`.

      en RTE, utilice el icono **Lista con viñetas**.

   * El elemento `<ol>` se utiliza para listas *numeradas*. Los elementos de listas individuales se identifican utilizando el elemento `<li>`.

      En RTE, utilice el icono **Lista numerada** .
   Si desea cambiar contenido existente por un tipo de lista específica, remarque el texto adecuado y seleccione el tipo de lista adecuado. Como en el ejemplo anterior, en el que se mostraba cómo se introducía texto en formato párrafo, los elementos de la lista adecuada se añaden automáticamente a tu HTML, pero puede verlo en la vista de editor de la fuente.

   >[!NOTE]
   `<dl>` no funciona para RTE.

* **Utilizar tablas**:

   Las tablas de datos deben identificarse utilizando elementos de tablas HTML:

   * un elemento `<table>`
   * un elemento `<tr>` para cada fila de la tabla
   * un elemento `<th>` para cada titular de fila y columna
   * un elemento `<td>` para cada celda de datos

   >[!NOTE]
   Las tablas se deben crear con el componente **Tabla.** Aunque las tablas se pueden crear en el componente Texto, no es recomendable.

   Además, las tablas accesibles utilizan los siguientes elementos y atributos:

   * El elemento `<caption>` se utiliza para proporcionar un subtítulo visible para la tabla. Los subtítulos por defecto aparecen centrados debajo de la tabla, pero se pueden posicionar de cualquier otra manera adecuada utilizando CSS. El subtítulo está asociado programáticamente con la tabla, por lo que se trata de un método útil para proporcionar una introducción al contenido.
   * El elemento `<h3 class="summary">` ayuda a los usuarios que carecen de visión para que entiendan con mayor facilidad la información que se presenta en la tabla mediante una sinopsis de lo que el usuario puede ver. Resulta particularmente útil cuando se utilizan diseños de la tabla complejos o poco convencionales (este atributo no se muestra en el buscador, solo se lee en voz alta para tecnologías de asistencia).
   * El atributo `scope` del elemento `<th>` se utiliza para indicar si una celda representa el encabezado de una fila en concreto o de una columna en concreto. Un enfoque similar es el de utilizar el encabezado y los atributos de identificación en tablas complejas, donde las celdas de datos se pueden asociar con uno o más encabezados.

   >[!NOTE]
   Por defecto, estos elementos y atributos no se encuentran disponibles directamente, aunque es posible que el administrador del sistema añada cierta ayuda para estos valores en el cuadro de diálogo **Propiedades de la tabla**[ (consulte Agregar ayuda para elementos y atributos HTML adicionales](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

   Cuando se añade una **Tabla** se pueden configurar las **Propiedades de la tabla** utilizando el cuadro de diálogo.

   * **Subtítulo** apropiado.
   * Idealmente, elimine los valores predeterminados de **anchura**, **altura**, **borde**, **relleno de celda** y **espaciado de celda**, ya que estas propiedades se pueden definir en una hoja de estilo global.

   ![Cuadro de diálogo de Propiedades de la tabla.](assets/chlimage_1-20a.png)

   A continuación, puede utilizar las **propiedades de celda** para elegir si la celda es una celda de datos o de encabezado y, si es una celda de encabezado, si se relaciona con una fila o columna o ambas:

   ![Cuadro de diálogo de Propiedades de la celda; configurar una fila (normalmente la primera) como encabezado.](assets/chlimage_1-21a.png)

* **Tablas de datos complejos:**

   En algunos casos en los que hay tablas complejas con dos o más niveles de encabezados, las Propiedades de la tabla básicas pueden no ser suficientes para proporcionar toda la información estructural necesaria. Para este tipo de tablas complejas es necesario crear relaciones directas entre los encabezados y sus celdas utilizando el **encabezado** y **atributos de identificación**. Por ejemplo, en la tabla siguiente, los encabezados y las identificaciones se comparan para crear una asociación programática para los usuarios de tecnología de asistencia.

   >[!NOTE]
   El atributo de identificación no se encuentra disponible en una instalación lista para usar. Se puede activar configurando las normas HTML y el serializador en RTE.

   >[!NOTE]
   Las tablas se deben crear con el componente **Tabla.** Aunque las tablas se pueden crear en el componente Texto, no es recomendable.

   ```xml
   <table>
      <tr>
        <th rowspan="2" id="h">Homework</th>
        <th colspan="3" id="e">Exams</th>
        <th colspan="3" id="p">Projects</th>
      </tr>
      <tr>
        <th id="e1" headers="e">1</th>
        <th id="e2" headers="e">2</th>
        <th id="ef" headers="e">Final</th>
        <th id="p1" headers="p">1</th>
        <th id="p2" headers="p">2</th>
        <th id="pf" headers="p">Final</th>
      </tr>
      <tr>
       <td headers="h">15%</td>
       <td headers="e e1">15%</td>
       <td headers="e e2">15%</td>
       <td headers="e ef">20%</td>
       <td headers="p p1">10%</td>
       <td headers="p p2">10%</td>
       <td headers="p pf">15%</td>
      </tr>
     </table>
   ```

   Para conseguirlo en AEM, añada las especificaciones directamente utilizando el modo de edición de la fuente.

   >[!NOTE]
   Esta funcionalidad no se encuentra disponible de inmediato en una instalación estándar. Requiere una configuración de RTE; normas HTML y serializador.

#### Más información: Información y relaciones (1.3.1) {#more-information-info-and-relationships}

* [Entender los criterios de éxito 1.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html)
* [Cumplir los criterios de éxito 1.3.1](https://www.w3.org/WAI/WCAG20/quickref/#qr-content-structure-separation-programmatic)

### Características sensoriales (1.3.3)           {#sensory-characteristics}

* Criterios de éxito 1.3.3
* Nivel A
* Características sensoriales: las instrucciones que se proporcionan para entender el contenido y operar con él no se basan solo en características sensoriales de componentes como la forma, el tamaño, la ubicación visual, la orientación o el sonido

#### Objetivo: Características sensoriales (1.3.3)      {#purpose-sensory-characteristics}

Los diseñadores normalmente se centran en características de diseño visuales tales como el color, la forma, el estilo del texto o una parte de la ubicación absoluta o relativa del contenido donde se presenta la información. Estas pueden ser técnicas de diseño muy poderosas para transmitir información, pero las personas ciegas o con limitaciones de visión puede que no consigan acceder a la información que requiere identificación visual de atributos como la ubicación, el color o la forma.

De la misma manera, la información que requiere distinguir entre sonidos distintos (como contenido cuya voz es masculina o femenina) presentará barreras de accesibilidad para las personas que sufran limitaciones auditivas si el contenido del audio no se refleja en un texto alternativo.

>[!NOTE]
Para los requisitos relativos a las alternativas de color, consulte [Uso del color](#use-of-color).

#### Cómo cumplir: Características sensoriales (1.3.3)      {#how-to-meet-sensory-characteristics}

Asegúrese de que cualquier información relativa a las características visuales del contenido de una página se presente también en un formato alternativo.

* Es importante no basarse en la posición visual para dar información. Por ejemplo, para dirigir a los usuarios hacia un menú a la derecha de la página para que accedan a más información, no se debe hacer referencia al *menú de la derecha*; en lugar de eso, es preferible nombrar el menú (por ejemplo mediante un encabezado) y hacer referencia a ese nombre en el texto.
* También es importante no basarse en el estilo del texto (por ejemplo si se trata de texto en negrita o en cursiva) como la única manera de transmitir la información.

>[!NOTE]
El uso de términos descriptivos se puede considerar aceptable si estos se entienden por su significado en un contexto no visual. Por ejemplo, utilizar *arriba* y *abajo* generalmente estaría aceptado, porque respectivamente implican contenido antes y después de un elemento particular del contexto; tendría sentido cuando el contenido se lee en voz alta.

#### Más información: Características sensoriales (1.3.3)      {#more-information-sensory-characteristics}

* [Entender los criterios de éxito 1.3.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html)
* [Cumplir los criterios de éxito 1.3.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-content-structure-separation-understanding)

### Distinguible (1.4)      {#distinguishable}

[Directrices 1.4 Distinguible: Facilitar a los usuarios ver y oír el contenido incluyendo la posibilidad de separar el primer plano del fondo.](https://www.w3.org/TR/WCAG20/#visual-audio-contrast)

### Uso del color (1.4.1)           {#use-of-color}

* Criterios de éxito 1.4.1
* Nivel A
* Uso del color: el color no es el único medio visual para transmitir información, indicar una acción, una respuesta o distinguir un elemento visual

>[!NOTE]
Este criterio de éxito se dirige específicamente a la percepción del color. Otras formas de percepción se tratan en [Adaptable (1.3)](#adaptable); incluyendo el acceso programático al color y otros códigos de presentación visual.

#### Objetivo: Uso del color (1.4.1)      {#purpose-use-of-color}

El color es, obviamente, una manera efectiva de resaltar el atractivo estético de las páginas web y también resulta útil para transmitir información. Sin embargo, existe una variedad de impedimentos visuales, desde la ceguera hasta la deficiencia de la percepción del color, que supone que hay personas que no pueden distinguir entre ciertos colores. Esto hace que la codificación de colores sea una manera poco fiable de transmitir información.

Por ejemplo, una persona con una deficiencia de la percepción entre el color rojo y el verde no podrá distinguir entre las gamas de verdes y las gamas de rojos. Puede que esta persona vea ambos colores como un tercer color (por ejemplo, marrón), en cuyo caso no podrá distinguir entre el verde, el rojo y el marrón.

Además, las personas que utilizan navegadores de solo texto, dispositivos de pantallas monocromáticas o páginas en blanco y negro no pueden percibir el color.

#### Cómo cumplir: Uso del color (1.4.1)   {#how-to-meet-use-of-color}

En todos los casos donde el color se utilice para transmitir información, es importante asegurarse de que la información se encuentra disponible sin necesidad de ver el color.

Por ejemplo, asegúrese de que la información que proporciona el color también esté explícita en el texto. La siguiente ilustración muestra cómo el color y el texto indican la disponibilidad de asientos en una actuación:

<table>
 <tbody>
  <tr>
   <td><p><strong>Actuación</strong></p> </td>
   <td><p><strong>Disponibilidad</strong></p> </td>
  </tr>
  <tr>
   <td><p>Martes, 16 de marzo<sup></sup></p> </td>
   <td><p>ASIENTOS DISPONIBLES</p> </td>
  </tr>
  <tr>
   <td><p>Miércoles, 17 de marzo</p> </td>
   <td><p>ASIENTOS DISPONIBLES</p> </td>
  </tr>
  <tr>
   <td><p>Jueves, 18 de marzo<sup></sup></p> </td>
   <td><p>AGOTADOS</p> </td>
  </tr>
 </tbody>
</table>

Si el color se utiliza como señal para proporcionar información, debe proporcionar una señal visual adicional, como un cambio de estilo (por ejemplo, negrita, cursiva) o de fuente. Esto ayuda a las personas con problemas de visión o a la hora de percibir el color a identificar la información. Sin embargo, no se puede confiar en esta medida totalmente puesto que no ayudaría a aquellos que no puedan ver la página.

#### Más información: Uso del color (1.4.1) {#more-information-use-of-color}

* [Entender los criterios de éxito 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [Cumplir los criterios de éxito 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [Directrices para cumplir la relación de contraste 3:1 que contiene una lista de colores &quot;seguros para la web&quot;](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)

### Contraste (mínimo) (1.4.3)      {#contrast-minimum}

* Criterios de éxito 1.4.3
* Nivel AA
* Contraste (mínimo): la presentación visual del texto y las imágenes de texto tiene una relación de contraste de al menos 4.5:1, excepto los siguientes:

   * Texto grande: el texto y las imágenes de texto a gran escala mantienen una relación de contraste de al menos 3:1.
   * Secundario: el texto o las imágenes de texto que forman parte de un componente de interfaz de usuario inactivo, que son puramente decorativos, que no son visibles para nadie o que forman parte de una fotografía que contiene otro contenido visual significativo, no tienen requisitos de contraste.
   * Logotipos: El texto que forma parte de un logotipo o del nombre de una marca no cuenta con un requisito mínimo de contraste.

#### Objetivo: Contraste (mínimo) (1.4.3)   {#purpose-contrast-minimum}

Las personas con ciertas deficiencias visuales quizá no puedan distinguir entre ciertas parejas de colores de poco contraste. Estas personas pueden sufrir problemas de accesibilidad si:

* El texto contrasta poco con el color del fondo.
* El código de color del texto (como el texto con vínculo y el texto sin vínculo) es importante para distinguir la información.

>[!NOTE]
El texto que se utiliza con fines puramente decorativos se excluye de estos criterios de éxito.

#### Cómo cumplir: Cumplir los criterios de contraste (Mínimo) (1.4.3)      {#how-to-meet-contrast-minimum}

Asegúrese de que el texto contrasta lo suficiente con el fondo. Las relaciones de contraste dependen del tamaño y del estilo del texto en cuestión:

* Para los textos cuyo tamaño es menor de 18 puntos (o 14 puntos en negrita), la relación de contraste entre el texto o las imágenes del texto y el fondo debería ser de al menos 4.5:1.
* Para los textos cuyo tamaño es de al menos 18 puntos (o 14 puntos en negrita), la relación de contraste debería ser de al menos 3:1.
* Ante un fondo estampado, el fondo alrededor de cualquier texto debería estar sombreado para que la relación 4.5:1 o 3:1 se mantenga.

Para comprobar los niveles de contraste, utilice una herramienta de contraste de color como el programa [Paciello Group Color Contrast Analyser](https://www.paciellogroup.com/resources/contrast-analyser.html) o el [verificador de contraste de color WebAIM](https://www.webaim.org/resources/contrastchecker/). Estas herramientas permiten comprobar las parejas de color e informar de cualquier problema de contraste.

Alternativamente, si no le preocupa especificar la apariencia de su página, puede optar por no especificar el color del fondo o del texto en primer plano. No es necesario comprobar el contraste, ya que el navegador del usuario determinará los colores del texto y del fondo.

Si no se pueden cumplir los niveles de contraste recomendados tendrá que proporcionar un vínculo a una versión alternativa y equivalente de la página (que no presente problemas de contraste de color) o permitir al usuario ajustar el contraste del esquema de color de la página bajo su propio criterio.

#### Más información: Contraste (mínimo) (1.4.3)      {#more-information-contrast-minimum}

* [Entender los criterios de éxito 1.4.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)
* [Cumplir los criterios de éxito 1.4.3](https://www.w3.org/WAI/WCAG20/quickref/#qr-visual-audio-contrast-contrast)

### Imágenes de texto (1.4.5)      {#images-of-text}

* Criterios de éxito 1.4.5
* Nivel AA
* Imágenes de texto: si las tecnologías que se utilizan consiguen la presentación visual, el texto se utiliza para proporcionar información (y no las imágenes de texto), excepto en los casos siguientes:

   * Personalizable: la imagen de texto se puede personalizar visualmente bajo los requisitos del usuario;
   * Esencial: una presentación de texto en concreto resulta esencial para que se transmita la información.

>[!NOTE]
Logotipos (texto que forma parte de un logotipo o del nombre de la marca) se consideran esenciales.

#### Objetivo: Imágenes de texto (1.4.5)           {#purpose-images-of-text}

Las imágenes de texto normalmente se utilizan cuando se prefiere un tipo de texto en particular; por ejemplo un logotipo, o si un texto se ha generado desde otra fuente (por ejemplo un documento físico escaneado). Sin embargo, comparadas con el texto presentado en HTML y cuyo estilo utiliza CSS, las imágenes de texto carecen de la flexibilidad de cambiar su tamaño o apariencia que podría resultar necesaria para las personas con deficiencias visuales o dificultades de lectura.

#### Cómo cumplir: Imágenes de texto (1.4.5)        {#how-to-meet-images-of-text}

Si es necesario utilizar imágenes de texto, utilice CSS para reemplazar las imágenes de texto con texto equivalente en HTML y así el texto estará disponible en un modo personalizable. Para mostrar un ejemplo de cómo se puede conseguir, consulte [C30: Utilizar CSS para reemplazar texto con imágenes de texto y proporcionar al usuario controles de interfaz que pueda cambiar](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### Más información: Imágenes de texto (1.4.5)           {#more-information-images-of-text}

* [Entender los criterios de éxito 1.4.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html)
* [Cumplir los criterios de éxito 1.4.5](https://www.w3.org/WAI/WCAG20/quickref/#qr-visual-audio-contrast-text-presentation)

## Principio 2: operable           {#principle-operable}

[Principio 2: operable. Los componentes y la navegación de interfaz de usuario deben ser operables.](https://www.w3.org/TR/WCAG20/#operable)

### Pausar, parar, ocultar (2.2.2)           {#pause-stop-hide}

* Criterios de éxito 2.2.2
* Nivel A
* Pausar, parar, ocultar: Para mover, cerrar, desplazar o actualizar automáticamente la información, los siguientes criterios son verdaderos:  

   * Mover, cerrar, desplazar: Para mover, cerrar o desplazar cualquier tipo de información que (a) empiece de manera automática, (b) dure más de cinco segundos y (c) se presente en paralelo con otro contenido, existe un mecanismo que el usuario puede utilizar para pausar, parar u ocultar la información, a menos que mover, cerrar o desplazar dicha información forme parte de una actividad en la que sea esencial;
   * Actualizar automáticamente: Para actualizar de manera automática cualquier tipo de información que (a) empiece de manera automática y (b) se presente en paralelo con otro contenido, existe un mecanismo que el usuario puede utilizar para pausar, parar u ocultar la información, o para controlar la frecuencia de la actualización, a menos que actualizar automáticamente dicha información forme parte de una actividad en la que sea esencial.

Puntos que se deben tener en cuenta:

1. Para ver los requisitos relacionados con contenidos que parpadean, consulte [No diseñar contenido de manera que cause parpadeos (2.3)](#seizures).
1. Ya que cualquier contenido que no cumpla estos criterios de éxito puede interferir en la capacidad de un usuario para utilizar toda una página, todo el contenido de la página web (tanto si se utiliza para cumplir otros criterios como si no) debe cumplir este criterio de éxito. Consulte [Requisito de conformidad 5: no interferencia](https://www.w3.org/TR/WCAG20/#cc5).
1. El contenido que se actualiza periódicamente a través del software o que se transmite al usuario no necesita preservar o presentar la información que se genera o se recibe entre la iniciación de la pausa y la reanudación de la presentación, puesto que puede no ser técnicamente posible y en muchas situaciones podría ser engañoso.
1. Una animación en una fase de precarga o en una situación similar se consideraría esencial si la interacción no se pudiera dar durante dicha fase para todos los usuarios, y si no indicara el progreso podría confundirlos o llevarles a pensar que el contenido se ha congelado o se ha estropeado.

#### Objetivo: Pausar, parar, ocultar (2.2.2)      {#purpose-pause-stop-hide}

Algunos usuarios pueden considerar que el contenido que se mueve les distrae o les dificulta a la hora de concentrarse en otras partes de la página. Además, dicho contenido puede ser difícil de leer para quienes tienen problemas para seguir un texto que se mueve.

#### Cómo cumplir: Pausar, parar, ocultar (2.2.2)      {#how-to-meet-pause-stop-hide}

Según la naturaleza del contenido, se puede aplicar una o varias de las siguientes sugerencias al crear páginas web con contenido que se mueve o parpadea:

* Proporcionar la manera de pausar el movimiento del contenido y dar a los usuarios tiempo suficiente para leerlo. Por ejemplo, lectores de noticias o texto que se actualiza de manera automática.
* Asegúrese de que el contenido que parpadea deja de hacerlo tras cinco segundos.
* Utilizar tecnologías adecuadas para mostrar el contenido parpadeante que se puede mostrar en el navegador. Por ejemplo, archivos de Formato de intercambio de gráficos (GIF) o Gráficos de red portátiles animados (APNG).
* Proporcionar un formulario de control en la página web para permitir a los usuarios desactivar cualquier contenido que parpadee en la página.
* Si no es posible ninguno de los anteriores, proporcionar un vínculo a la página que contenga todo el contenido pero sin parpadeos.

#### Más información: Pausar, parar, ocultar (2.2.2)   {#more-information-pause-stop-hide}

* [Entender los criterios de éxito 2.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html)
* [Cumplir los criterios de éxito 2.2.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-time-limits-pause)

### Parpadeos (2.3)      {#seizures}

[Directrices 2.3 Parpadeos: No diseñar contenido de manera que cause parpadeos.](https://www.w3.org/TR/WCAG20/#seizure)

### Tres parpadeos o por debajo de los límites (2.3.1)      {#three-flashes-or-below-threshold}

* Criterios de éxito 2.3.1
* Nivel A
* Tres parpadeos o Por debajo de los límites: las páginas web no contienen ningún elemento que parpadee más de tres veces en el período de un segundo o que esté por debajo del parpadeo general y los indicadores del parpadeo rojo

>[!NOTE]
Ya que cualquier contenido que no cumpla estos criterios de éxito puede interferir en la capacidad de un usuario para utilizar toda una página, todo el contenido de la página web (tanto si se utiliza para cumplir otros criterios como si no) debe cumplir este criterio de éxito. Consulte [Requisito de conformidad 5: no interferencia](https://www.w3.org/TR/WCAG20/#cc5).

#### Objetivo: Tres parpadeos o Por debajo de los límites (2.3.1) {#purpose-three-flashes-or-below-threshold}

En ciertos casos, el contenido que parpadea puede causar parpadeos fotosensibles. Este criterio de éxito permite a los usuarios acceder y experimentar todo el contenido sin tener que preocuparse por el contenido parpadeante.

#### Cómo cumplir: Tres parpadeos o por debajo del umbral (2.3.1)      {#how-to-meet-three-flashes-or-below-threshold}

Siga estos pasos para asegurarse de que se aplican las siguientes técnicas:

* Asegúrese de que los componentes no parpadean más de tres veces durante el período de un segundo;
* Si no se cumple la condición anterior, muestre el contenido parpadeante en una zona *pequeña y segura* en píxeles en la pantalla. Esta zona se calcula utilizando una fórmula compleja que se recoge en [G176: Hacer que la zona parpadeante sea lo suficientemente reducida](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176), por lo que esta técnica solo se debe utilizar si el contenido que parpadea es *absolutamente* necesario.

#### Más información: Tres parpadeos o por debajo de los límites (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [Entender los criterios de éxito 2.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html)
* [Cumplir los criterios de éxito 2.3.1](https://www.w3.org/WAI/WCAG20/quickref/#seizure)

### Página titulada (2.4.2)           {#page-titled}

* Criterios de éxito 2.4.2
* Nivel A
* Página titulada: las páginas web tienen títulos que describen el tema o el objetivo de estas

#### Objetivo: Página titulada (2.4.2)      {#purpose-page-titled}

Este criterio de éxito ayuda a todo el mundo, independientemente de cualquier discapacidad en concreto, a identificar de manera rápida el contenido de una página web sin tener que leerla entera. Es particularmente útil cuando se abren varias páginas web en pestañas del navegador, ya que el título de la página se muestra en la pestaña y por eso se puede localizar rápidamente.

#### Cómo cumplir: Página titulada (2.4.2)      {#how-to-meet-page-titled}

Al crear una página HTML nueva en AEM, se puede especificar el título de la página. Asegúrese de que el título describe adecuadamente el contenido de la página para que los usuarios puedan identificar rápidamente si el contenido es relevante o no para sus necesidades.

También puede editar el título de la página al editar una página, a la que se puede acceder desde la ficha **Página** - **Página** - **Propiedades de la página...**

#### Más información: Página titulada (2.4.2) {#more-information-page-titled}

* [Entender los criterios de éxito 2.4.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html)
* [Cumplir los criterios de éxito 2.4.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-title)

### Objetivo del vínculo (en contexto) (2.4.4)           {#link-purpose-in-context}

* Criterios de éxito 2.4.4
* Nivel A
* Objetivo del vínculo (en contexto): el objetivo de cada vínculo se puede determinar por el texto del vínculo en sí o por el texto del vínculo junto al contexto del vínculo determinado programáticamente, excepto cuando el objetivo del vínculo sea ambiguo para los usuarios en general

#### Objetivo: Objetivo del vínculo (en contexto) (2.4.4)           {#purpose-link-purpose-in-context}

Es muy importante indicar claramente la dirección del vínculo a través del texto del vínculo adecuado para todos los usuarios, independientemente de cualquier discapacidad. Esto ayuda a los usuarios a decidir si quieren seguir el vínculo o no. Para los usuarios con visión normal, un texto para el vínculo con sentido es extremadamente útil cuando hay varios vínculos en una página (particularmente si la página está muy cargada de texto), ya que el texto del vínculo proporciona una indicación más clara de la función del destino de la página. Mientras que los usuarios que utilizan tecnologías de asistencia, que pueden generar una lista de todos los vínculos en una misma página, pueden entender más fácilmente el texto del vínculo por el contexto.

#### Cómo cumplir: Objetivo del vínculo (en contexto) (2.4.4)     {#how-to-meet-link-purpose-in-context}

Sobre todo, es importante asegurarse de que el objetivo de un vínculo se describe con claridad en el texto del vínculo.

* Ejemplo incorrecto:

   * Texto: para obtener más información sobre las clases nocturnas de otoño de 2010, haga clic aquí.
   * Motivo: no indica el destino claramente y resulta ambiguo.

* Ejemplo correcto:

   * Texto: Clases nocturnas de otoño de 2010, más información.
   * Motivo: ajustando ligeramente el texto y la posición del vínculo se puede mejorar el texto del vínculo.

Los vínculos se tienen que redactar con coherencia en todas las páginas, especialmente en las barras de navegación. Por ejemplo, si un vínculo a una página en concreto se nombra como **Publicaciones** en una página, utilice ese mismo texto en otras páginas para mantener la coherencia.

Sin embargo, en el momento de escribir, existen varios problemas en cuanto al uso de los títulos:

* El texto del atributo en el título generalmente se encuentra disponible solamente para los usuarios que utilizan el ratón como un consejo de herramienta emergente y no se puede acceder a él mediante el teclado. 
* Los lectores de pantalla pueden leer en voz alta los atributos de título, pero esta funcionalidad puede que no se permita por defecto, por lo que los usuarios pueden no estar al tanto de que existe un atributo de título.
* Es difícil cambiar la apariencia del texto del título, lo que quiere decir que puede resultar difícil o imposible de leer para algunas personas.

Por eso, mientras el atributo del título se puede utilizar para proporcionar contenido adicional a un vínculo, es importante tener en cuenta las limitaciones y no utilizarlo como alternativa para un texto de vínculo adecuado.

Cuando el vínculo esté formado por una imagen, asegúrese de que el texto alternativo de la imagen describe el destino del vínculo. Por ejemplo, si la imagen de una estantería es el vínculo a las publicaciones de una persona, el texto alternativo debería ser algo como **Publicaciones de John Smith** y no **Estantería**.

Alternativamente, si el anclaje del vínculo contiene texto que describe el objetivo del vínculo además de la imagen (y por ello el texto aparece junto a la imagen), utilice un atributo alternativo vacío para la imagen:

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
El fragmento anterior representa una ilustración; es recomendable utilizar el componente **Imagen**.

Aunque es aconsejable proporcionar un texto para el vínculo que identifique su objetivo sin necesidad de contexto adicional, no siempre es posible. Los vínculos de contexto libre se pueden utilizar en los casos siguientes, cuyos ejemplos HTML se pueden encontrar en [Cumplir los criterios de éxito 2.4.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-refs).

* Cuando el texto del vínculo forme parte de una lista de vínculos relacionados y cuando el elemento de la lista que incluye el vínculo proporcione contexto suficiente.
* Cuando el objetivo del vínculo se pueda identificar claramente gracias al párrafo *anterior* (y no gracias al siguiente).
* Cuando el vínculo aparezca incluido en una tabla de datos y el objetivo se pueda identificar claramente en los encabezados asociados.
* Cuando una lista de vínculos esté incluida en un conjunto de encabezados y el encabezado mismo proporcione un contexto adecuado.
* Cuando una lista de vínculos esté incluida en un vínculo alojado y el elemento de la lista superior encima del vínculo alojado proporcione un contexto adecuado.

En algunos casos en los que hay varios vínculos en una misma página (cada uno de los cuales proporciona la dirección de un vínculo con detalles complejos pero necesarios), puede resultar adecuado proporcionar una versión alternativa de la página web que muestre exactamente el mismo contenido pero donde el texto del vínculo no se detalle tanto.

Alternativamente, los guiones se pueden utilizar para proporcionar una cantidad mínima de texto en el vínculo, pero al activar un control adecuado orientado hacia la parte superior de la página, el texto del vínculo se *expande* hacia más detalles. Un enfoque similar sería utilizar CSS para *ocultar* el vínculo de la vista del usuario, pero imprimirlo en su totalidad para los usuarios del lector de pantalla. Esta cuestión queda fuera del ámbito de este documento, pero existe más información sobre cómo conseguirlo en la sección [Más información: Objetivo del vínculo (en contexto) (2.4.4)](#more-information-link-purpose-in-context).

#### Más información: Objetivo del vínculo (en contexto) (2.4.4) {#more-information-link-purpose-in-context}

* [Entender los criterios de éxito 2.4.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html)
* [Cumplir los criterios de éxito 2.4.4](https://www.w3.org/WAI/WCAG20/quickref/#qr-navigation-mechanisms-refs)
* [C7: Utilizar CSS para ocultar una parte del texto del vínculo](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)

## Principio 3: comprensible      {#principle-understandable}

[Principio 3: Comprensible: la información y el funcionamiento de la interfaz del usuario deben ser comprensibles.](https://www.w3.org/TR/WCAG20/#understandable)

### Hacer que el contenido del texto sea legible y comprensible (3.1)           {#make-text-content-readable-and-understandable}

[Directrices 3.1 Legible: hacer que el contenido del texto sea legible y comprensible.](https://www.w3.org/TR/WCAG20/#meaning)

### Idioma de la página (3.1.1)           {#language-of-page}

* Criterios de éxito 3.1.1
* Nivel A
* Idioma de la página: el lenguaje humano por defecto de cada página web se puede determinar programáticamente

#### Objetivo: Idioma de la página (3.1.1)           {#purpose-language-of-page}

El objetivo de este criterio de éxito es asegurarse de que el texto y cualquier otro contenido lingüístico se introduce de manera correcta. Para los usuarios de lectores de pantalla, esto garantiza que el contenido se pronuncia de manera correcta, mientras que los navegadores visuales tienden a mostrar ciertos conjuntos de caracteres de manera correcta.

#### Cómo cumplir: Idioma de la página (3.1.1)        {#how-to-meet-language-of-page}

Para cumplir este criterio de éxito, el idioma por defecto de una página web se puede identificar utilizando el atributo `lang` en el elemento `<html>` en la parte superior de la página. Por ejemplo:

* Si una página está escrita en inglés británico, el elemento `<html>` debería ser:

   `<html lang = “en-gb”>`

* Mientras que una página en inglés americano debería adoptar el estándar siguiente:

   `<html lang = “en-us”>`

En AEM, el idioma predeterminado de la página se define al crear la página, pero también se puede cambiar al editarla. Puede hacerlo desde la **barra de tareas** - pestaña **Página** - **Propiedades de página…** - pestaña **Avanzadas**.

#### Más información: Idioma de la página (3.1.1) {#more-information-language-of-page}

* [Entender los criterios de éxito 3.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html)
* [Cumplir los criterios de éxito 3.1.1](https://www.w3.org/WAI/WCAG20/quickref/#qr-meaning-doc-lang-id)
* Los códigos se basan en ISO 639-1. Encontrará una lista más extensa de códigos para cada idioma en [W3 Schools](https://www.w3schools.com/tags/ref_language_codes.asp).

### Idioma de las partes (3.1.2)       {#language-of-parts}

* Criterios de éxito 3.1.2
* Nivel AA
* Idioma de las partes: se puede determinar programáticamente el idioma de cada pasaje o frase en el contenido excepto en casos de nombres propios, términos técnicos, palabras de lenguaje indeterminado y palabras o expresiones que hayan formado parte de la lengua vernácula del texto que lo rodea

#### Objetivo: Idioma de las partes (3.1.2)    {#purpose-language-of-parts}

El objetivo de este criterio de éxito es parecido al del criterio de éxito del [Idioma de la página](#language-of-page), excepto por el hecho de que se refiere a páginas web con contenido en idiomas múltiples en una misma página (por ejemplo, por las citas o préstamos poco frecuentes).

Las páginas que aplican este criterio de éxito permiten:

* Software de transición en braille para insertar caracteres acentuados.
* Lectores de pantalla para pronunciar las palabras que no aparecen en el idioma por defecto de manera correcta.
* Herramientas de traducción como Google Translate para traducir el contenido de manera correcta de un idioma a otro.

#### Cómo cumplir: Idioma de las partes (3.1.2)    {#how-to-meet-language-of-parts}

El atributo `lang` se puede utilizar para identificar los cambios en el idioma del contenido. Por ejemplo, una cita en alemán (ISO 639-1 código “de”) se puede mostrar de la manera siguiente:

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
Los bloques de citas no funcionan en una situación fácil de usar. Se podría desarrollar un componente personalizado para admitir el atributo.

De manera similar, el navegador puede mostrar un préstamo poco común o una expresión correcta si el elemento `span` se utiliza de la manera siguiente:

```xml
<p>The only French phrase I know is <span lang = “fr”>je ne sais quoi</span>.</p>
```

>[!NOTE]
No es necesario seguir este criterio de éxito cuando se incluyen nombres o ciudades en distintos idiomas, o cuando se utilizan préstamos o expresiones que ya son comunes en el idioma por defecto (como *schadenfreude* en inglés).

Para añadir el elemento “span” (extensión), con un idioma adecuado, puede editar manualmente sus especificaciones HTML en el modo de edición de la fuente de RTE para que se lea como puede ver arriba. Alternativamente, el atributo `lang`[ se puede incluir en RTE a través de un administrador del sistema (consulte Añadir ayuda para elementos y atributos HTML adicionales](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

#### Más información: Idioma de las partes (3.1.2) {#more-information-language-of-parts}

* [Entender los criterios de éxito 3.1.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html)
* [Cumplir los criterios de éxito 3.1.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-meaning-other-lang-id)

### Ayudar a los usuarios a evitar y corregir errores (3.3)      {#help-users-avoid-and-correct-mistakes}

[Directrices 3.3 Asistencia de la entrada: ayudar a los usuarios a evitar y corregir errores.](https://www.w3.org/TR/WCAG20/#minimize-error)

### Etiquetas o instrucciones (3.3.2)      {#labels-or-instructions}

* Criterios de éxito 3.3.2
* Nivel A
* Etiquetas o instrucciones: las etiquetas o instrucciones se proporcionan cuando el contenido requiere entradas de usuarios

#### Objetivo: Etiquetas o instrucciones (3.3.2)    {#purpose-labels-or-instructions}

Proporcionar instrucciones para ayudar a los usuarios a completar formularios es una parte fundamental para la buena práctica en la funcionalidad de la interfaz. Hacer esto es particularmente beneficioso para quienes sufren discapacidades visuales o cognitivas, ya que de otra manera experimentarían dificultades para entender la estructura de un formulario y el tipo de datos que se proporcionan en un campo del formulario en concreto.

En AEM, se añade una etiqueta por defecto al añadir un componente de formulario, como **Cuadro de texto**, a la página. Este título por defecto depende del tipo de componente, puede añadir su propio título en la pestaña **Título y texto** del diálogo de edición para ese campo. Es importante asegurarse de que las etiquetas ayudan a los usuarios a entender los datos que se asocian con cada componente del formulario.

![Pestaña Título y texto (cuadro de diálogo de edición); se ha añadido el título &quot;Descripción&quot;.](assets/chlimage_1-22a.png)

El campo **Título** se debe utilizar para elementos de campo porque proporciona una etiqueta disponible para la tecnología de asistencia. No basta con escribir una etiqueta en el texto, al lado del campo.

Para algunos componentes de formulario también se pueden ocultar las etiquetas utilizando la casilla **Ocultar título**. Las etiquetas ocultas de esta forma siguen estando disponibles para la tecnología de asistencia, pero no se muestran en la pantalla. Aunque puede ser una medida adecuada en algunas situaciones, normalmente es mejor incluir una etiqueta que sea visual siempre que se pueda, ya que posiblemente algunos usuarios se fijen en una sección muy pequeña de la pantalla (que miren los campos uno por uno) y necesiten las etiquetas para identificar el campo de manera correcta.

#### Botones de imagen {#image-buttons}

Cuando se utilizan botones de imagen (por ejemplo, el componente **Botón de imagen**) el campo **Título** en la pestaña **Título y texto** del cuadro de diálogo de edición, proporciona el texto alternativo para la imagen, en lugar de la etiqueta. Por eso, en el ejemplo siguiente, la imagen con el texto `Submit` contiene el texto alternativo `Submit`, que se ha añadido utilizando el campo **Título** en el diálogo de edición.

![Botón de imagen con el texto alternativo configurado en el campo Título (cuadro de diálogo de edición).](assets/chlimage_1-23a.png)

#### Grupos de campos de formulario {#groups-of-form-fields}

Cuando hay un grupo de controles relacionados, como el **Grupo de radio**, puede ser necesario un título para el grupo, así como controles individuales. Al añadir un conjunto de botones de opción en AEM, el campo **Título** proporciona el título del grupo, mientras que se especifican títulos individuales cuando los botones de opción (**elementos**) se crean.

![Añadir elementos al grupo de radio. El título del grupo es &quot;Contactar mediante&quot;, que se define en el campo Título.](assets/chlimage_1-24a.png)

Sin embargo, no existe una asociación programática entre el título del grupo y los botones de opción. Los editores de plantillas necesitarían rodear el título en los `fieldset` necesarios y las etiquetas `legend` para crear esta asociación, que solo se puede hacer editando el código fuente de la página. Alternativamente, un administrador del sistema puede añadir soporte a estos elementos para que aparezcan en el diálogo **Propiedades del campo**[ (consulte Añadir ayuda para elementos y atributos HTML adicionales](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)).

#### Consideraciones adicionales para Formularios {#additional-considerations-for-forms}

Si se introducen datos en un formato concreto, especifíquelo en el texto de la etiqueta. Por ejemplo, si se tiene que introducir una fecha en formato `DD-MM-YYYY`, especifíquelo como parte de la etiqueta. Esto significa que cuando los usuarios de los lectores de pantalla se encuentren con este campo, la etiqueta se anunciará automáticamente junto con la información adicional sobre el formato.

Si es obligatorio introducir datos en un campo de formulario, especifíquelo utilizando la palabra obligatorio como parte de la etiqueta. AEM añade un asterisco cuando un campo es obligatorio, pero sería ideal incluir la palabra `required` en la etiqueta (en el campo **Título** del diálogo de edición).

![Añadir información adicional (la palabra obligatorio) para los usuarios de lector de pantalla en el campo &quot;Título&quot;.](assets/chlimage_1-25a.png)

La colocación de las etiquetas también es importante ya que ayuda a localizar campos adecuados. Esto es de particular importancia cuando el usuario se encuentra con un formulario complejo. Siga la convención siguiente:

* Casillas de verificación o botones de radio:

   Las etiquetas se colocan inmediatamente a la derecha del campo.

* Todos los demás componentes del formulario (por ejemplo, cuadros de texto, cuadros combinados):

   Las etiquetas se colocan inmediatamente encima o inmediatamente a la izquierda del campo.

En formularios simples con una funcionalidad muy limitada, etiquetar de manera correcta un botón de `Submit` puede actuar como una etiqueta para el campo adyacente (por ejemplo: `Search`). Resulta útil cuando puede ser difícil encontrar espacio para el texto de una etiqueta.

#### Más información: Etiquetas o instrucciones (3.3.2)    {#more-information-labels-or-instructions}

* [Entender los criterios de éxito 3.3.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html)
* [Cumplir los criterios de éxito 3.3.2](https://www.w3.org/WAI/WCAG20/quickref/#qr-minimize-error-cues)

