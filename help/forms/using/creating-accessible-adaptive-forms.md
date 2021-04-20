---
title: Creación de formularios adaptables accesibles
seo-title: Creación de formularios adaptables accesibles
description: AEM Forms proporciona herramientas y para crear formularios adaptables accesibles, y ayuda a cumplir con los estándares de accesibilidad.
seo-description: AEM Forms proporciona herramientas y para crear formularios adaptables accesibles, y ayuda a cumplir con los estándares de accesibilidad.
uuid: 6472bc2d-47ca-4883-88b7-5de0b758fd00
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1e95c66b-d132-4c44-a1dc-31fd09af8113
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 7a3f54d90769708344e6751756b2a12ac6c962d7
workflow-type: tm+mt
source-wordcount: '2078'
ht-degree: 1%

---


# Creación de formularios adaptables accesibles{#creating-accessible-adaptive-forms}

## Introducción {#introduction}

Un formulario accesible es un formulario que todos pueden utilizar, incluidos los usuarios con necesidades especiales. Forms adaptable incluye una serie de funciones y capacidades que mejoran la capacidad de uso de los usuarios con diferentes capacidades. Crear la accesibilidad en formularios adaptables no solo permite la mayor audiencia posible para el contenido, sino que también es un requisito al proporcionar documentos en áreas geográficas en las que se exige el cumplimiento de los estándares de accesibilidad. AEM Forms ayuda a los desarrolladores de formularios a cumplir con los estándares de accesibilidad.

Durante la creación de un formulario adaptable, el autor debe tener en cuenta los siguientes puntos para crear un formulario adaptable accesible:

* Compruebe el formulario con la herramienta de prueba de accesibilidad Nombre accesible y Inspector de descripción (ANDI)
* Proporcionar etiquetas adecuadas para los controles de formulario
* Proporcionar equivalentes de texto para imágenes
* Proporcionar suficiente contraste de color
* Asegúrese de que los controles de formulario son accesibles mediante el teclado

## Requisitos previos

Se necesita una herramienta de accesibilidad como **Accessible Name and Description Inspector (ANDI)** y un **tema del formulario adaptable desarrollado para solucionar problemas relacionados con la accesibilidad** para crear un formulario adaptable accesible.

### Descargar e instalar la herramienta de prueba de accesibilidad

La herramienta Inspector de nombres y descripciones accesibles (ANDI) ayuda a identificar y corregir los problemas relacionados con el cumplimiento de la accesibilidad en el contenido web. Es la herramienta recomendada bajo las directrices de Trusted Tester v5 del Departamento de Seguridad Nacional. El Departamento de &#x200B; de la Administración de Seguridad Social de los Estados Unidos lo desarrolla para comprobar que la Sección 508 cumpla con el contenido de la Web. La herramienta:

* Ayuda a detectar problemas de accesibilidad &#x200B; en una página web
* Proporciona sugerencias para mejorar la accesibilidad &#x200B;
* Detecta problemas de accesibilidad del teclado y contraste de color
* Identifica claramente el contenido del lector de pantalla de acuerdo con los estándares

ANDI trabaja con los principales navegadores de Internet. Consulte la [documentación de ANDI](https://www.ssa.gov/accessibility/andi/help/install.html) para obtener instrucciones detalladas sobre cómo configurar y utilizar la herramienta.

### Descargue e instale el tema Ultramarine-Accessible

El tema Ultramarine-Accessible es un tema de referencia. Ayuda a demostrar cómo corregir el contraste de color y otros problemas relacionados con la accesibilidad de forma adaptativa. Adobe recomienda crear un tema personalizado para el entorno de producción en función de los estilos aprobados por su organización. Siga estos pasos para cargar el tema en la instancia de AEM:

1. Descargue el paquete de temas.
1. Vaya a **[!UICONTROL Experience Manager]** > **[!UICONTROL Navegación]** ![Navegación](assets/Smock_Compass_18_N.svg) > **[!UICONTROL Forms]** en la instancia de AEM.
1. Pulse **[!UICONTROL Crear]** > **[!UICONTROL Cargar archivo]**. Seleccione y cargue el archivo x Ultramarine-Accessible-Theme.zip. Carga el tema en la instancia de AEM.

## Conversión de un formulario adaptable en accesible

Debe centrarse en cuatro aspectos clave: navegación mediante el teclado, contraste de color, texto alternativo significativo para imágenes y etiquetas adecuadas para controles de formulario para que un formulario adaptable sea accesible. Siga estos pasos para que los formularios adaptables existentes sean accesibles:

### 1. Aplique un tema accesible y realice correcciones adicionales

Aplique el tema Ultramarine-Accessible a su forma adaptativa existente. Para aplicar el tema:

1. Abra el formulario adaptable para editarlo.
1. Seleccione un componente y pulse el icono principal. En el menú contextual, pulse **[!UICONTROL Contenedor de formulario adaptable]** y, a continuación, pulse el icono de configuración.
1. Seleccione el tema Ultramarine-Accessible en el navegador de propiedades y pulse el icono **[!UICONTROL Guardar]**.
1. Actualice la ventana del explorador. El tema se aplica al formulario adaptable.

Después de aplicar un tema accesible, realice las siguientes correcciones adicionales. Las correcciones se añaden a las correcciones de accesibilidad que se tratan en el tema accesible:

1. Agregue un texto alternativo significativo para la imagen del logotipo en el formulario adaptable.

   Proporcione un texto alternativo significativo para las imágenes de los componentes de encabezado y pie de página de la plantilla de formulario adaptable. Al corregir la plantilla y utilizarla para crear un formulario adaptable, los formularios adaptables heredan todas las correcciones relacionadas con la accesibilidad aplicadas al encabezado y al pie de página de la plantilla.  Para un formulario adaptable existente, realice cambios a nivel de formulario adaptable. Los cambios realizados en una plantilla de formulario adaptable no fluyen automáticamente a un formulario adaptable existente.

1. Agregue un componente de encabezado que contenga el nombre del formulario al formulario adaptable. Si el diseño de formulario especifica un nombre de empresa, agregue también un componente de encabezado independiente para el nombre de empresa.

   La mayoría de las herramientas de accesibilidad informan a los usuarios sobre la jerarquía del contenido para ayudarles a comprender la estructura de la página web. Defina distintos niveles de encabezado para el nombre de organización y el texto del nombre del formulario en el formulario adaptable para proporcionar una estructura jerárquica a este texto. Además, utilice un componente Texto antes de cada panel y sección con un nivel de encabezado adecuado para crear una jerarquía.

   ![Aplicación de un estilo de encabezado](assets/apply-style.gif)

1. Cambie el color de fondo del pie de página para utilizar el contraste adecuado de acuerdo con los estándares de accesibilidad para mejorar la visibilidad y legibilidad del texto. Puede utilizar ANDI para encontrar problemas de contraste de color en el formulario. Además, no utilice fuentes muy pequeñas. Las fuentes pequeñas son difíciles de leer.

1. Reemplace los componentes switch y de elección de imagen del formulario adaptable existente por el componente de opción (radio).

1. Reemplace el componente de paso numérico del formulario adaptable existente por el componente de cuadro numérico.

1. Reemplace el campo de entrada de fecha con el campo selector de fecha.

1. Establezca los patrones de visualización, validación y edición para el componente selector de fechas. Asimismo, configure un mensaje de error de validación personalizado. Por ejemplo, ha especificado una fecha no válida. El formato correcto de la fecha es AAAA-MM-DD.

1. Establezca el texto de accesibilidad personalizado para el componente selector de fechas. Por ejemplo, introduzca la fecha de nacimiento. Los lectores de pantalla leen estos textos de accesibilidad personalizados.

1. Utilice una descripción breve en lugar de una descripción larga para los componentes del formulario adaptable. Una descripción larga agrega el botón de ayuda. Asegúrese de que el formulario adaptable no tenga ningún botón de ayuda.

1. Agregue texto de accesibilidad personalizado a todas las celdas de solo lectura de las tablas. Además, deshabilite todas las celdas de solo lectura de las tablas.

1. Elimine los campos de firma de anotaciones, si los hubiera, en el formulario adaptable. Configure el formulario adaptable para que utilice Adobe Sign para una experiencia de firma digital perfecta.

### 2. Proporcione etiquetas adecuadas para los controles de formulario {#provide-proper-labels-for-form-controls}

La etiqueta o el título de un componente identifica lo que representa el componente de formulario. Por ejemplo, el texto &quot;Nombre&quot; indica a los usuarios que deben introducir su nombre en un campo de texto. Para que puedan acceder los lectores de pantalla, la etiqueta está asociada programáticamente a un componente de formulario. Como alternativa, el control de formulario se configura con información de accesibilidad adicional.

La etiqueta que perciben los lectores de pantalla no necesariamente debe ser la misma que el rótulo visual. En algunos casos, es posible que desee ser más específico sobre el propósito del control. Para cada objeto de campo de un formulario, las opciones de accesibilidad se pueden utilizar para especificar lo que anuncia el lector de pantalla para identificar el campo de formulario específico.

Para utilizar la opción Accesibilidad, siga estos pasos:

1. Seleccione un componente y pulse ![cmppr](assets/cmppr.png).
1. Haga clic en **[!UICONTROL Accesibilidad]** en la barra lateral para elegir la opción de accesibilidad deseada.

### Opciones de accesibilidad en componentes de formulario {#accessibility-options-in-form-components}

![Opciones de accesibilidad en componentes de formulario](assets/accessibility-options.png)

**Los** autores de formularios de texto personalizados proporcionan el contenido de la opción de accesibilidad Campo de texto personalizado. La tecnología de asistencia, como los lectores de pantalla, utiliza este texto personalizado. El uso de la configuración Título es la mejor opción en la mayoría de los casos. Considere la posibilidad de crear Texto personalizado del Reader de pantalla solo cuando utilice el Título o una breve descripción no sea posible.

**Breve** descripciónPara la mayoría de los componentes, la breve descripción aparece durante la ejecución cuando el usuario sitúa el puntero sobre el componente. Puede establecer esta opción en el campo de descripción breve, en la opción de contenido de ayuda.

**** TítuloUtilice esta opción para permitir que AEM Forms utilice la etiqueta visual asociada al campo de formulario como texto del lector de pantalla.

**** NombrePuede especificar un valor en el campo Nombre de la ficha Enlace. El nombre no puede contener espacios.

**** NoneAl seleccionar None, el objeto de formulario no tiene nombre en el formulario publicado. Ninguno no es una configuración recomendada para los controles de formulario.

>[!NOTE]
>
>* El botón de opción y la casilla de verificación solo pueden tener dos opciones para la accesibilidad, a saber, Texto personalizado y Título.
>* Para los formularios adaptables basados en XFA, la opción de accesibilidad se hereda de las opciones de accesibilidad establecidas en el XDP. La información del objeto de XDP se asigna a la Descripción corta y el rótulo se asigna al título. Las otras opciones funcionan tal cual.


### 3. Proporcione equivalentes de texto para imágenes {#provide-text-equivalents-for-images}

Las imágenes pueden ayudar a mejorar la comprensión de algunos usuarios. Sin embargo, para los usuarios que utilizan lectores de pantalla, las imágenes reducen la accesibilidad del formulario. Si decide utilizar imágenes, proporcione descripciones de texto para todas las imágenes.

Asegúrese de que el texto describe el objeto y su propósito en el formulario. Un lector de pantalla lee este texto alternativo cuando encuentra una imagen. Una imagen siempre debe tener un texto alternativo especificado.

Seleccione un componente de imagen y pulse ![cmppr](assets/cmppr.png). En la barra lateral, en Propiedades, especifique el texto alternativo de una imagen.

![Texto alternativo de una imagen](assets/image-properties.png)

### 4. Proporcione suficiente contraste de color {#provide-sufficient-color-contrast}

El diseño de accesibilidad implica considerar directrices adicionales para el uso del color. Los autores de formularios pueden utilizar colores para mejorar el aspecto de los formularios, resaltando los distintos componentes del formulario. Sin embargo, un uso inapropiado del color puede hacer que una forma sea difícil o imposible de leer para personas con capacidades diferentes.

Los usuarios con deficiencias visuales dependen de un alto contraste entre el texto y el fondo para leer contenido digital. Sin un contraste suficiente, una forma puede resultar difícil, si no imposible, de leer para algunos usuarios.

Se recomienda utilizar la fuente y los colores de fondo predeterminados, contenido en color negro sobre fondo blanco. Si cambia los colores predeterminados, elija un color de primer plano oscuro en un color de fondo claro o viceversa.

Consulte [Creación de temas personalizados para formularios adaptables](/help/forms/using/creating-custom-adaptive-form-themes.md) para obtener más información sobre cómo cambiar el color de contraste y el tema para los formularios adaptables.

### 5. Asegúrese de que los controles de formulario sean accesibles mediante el teclado {#ensure-that-form-controls-are-keyboard-accessible}

Un formulario accesible se puede rellenar por completo utilizando solo el teclado o un dispositivo de entrada equivalente. Los usuarios con movilidad reducida o visión reducida pueden no tener más opción que utilizar el teclado y muchos usuarios que pueden utilizar el ratón prefieren la entrada del teclado. Al permitir los distintos métodos de entrada, no solo se crean formularios accesibles, sino que también se crean formularios que se adaptan mejor a las preferencias de todos los usuarios.

Los siguientes métodos abreviados del teclado están disponibles en AEM Forms.

| Acción | Métodos abreviados del teclado |
|---|---|
| Mover el cursor hacia adelante a través de un formulario | Ficha |
| Mover el cursor hacia atrás a través de un formulario | Mayús + Tab |
| Mover al panel siguiente | Alt+Flecha derecha |
| Mover al panel anterior | Alt+Flecha izquierda |
| Restablecer los datos rellenados en un formulario | Alt + R |
| Enviar un formulario | Alt + S |

Además, hay varias teclas de método abreviado de teclado disponibles para el componente **[!UICONTROL Selector de fecha]** en Forms adaptable. Para habilitar las teclas de método abreviado, pulse el componente **[!UICONTROL Selector de fecha]** y pulse ![Configurar](assets/configure-icon.svg) para abrir las propiedades. En la sección **[!UICONTROL Patrones]**, seleccione un patrón de visualización mediante las listas desplegables **[!UICONTROL Type]** y **[!UICONTROL Pattern]**. Guarde las propiedades para habilitar el uso de teclas de método abreviado para el componente **[!UICONTROL Selector de fecha]**.

Las siguientes teclas de método abreviado de teclado están disponibles para el componente Selector de fecha en Forms adaptable:

| Acción | Métodos abreviados del teclado |
|---|---|
| <ul><li>Mostrar las opciones del componente Selector de fecha cuando el tab focus resalta el icono de calendario</li><li>Suceso click cuando el tab focus resalte una opción</li> | Espacio o Entrar |
| Ocultar las opciones del componente Selector de fecha | Esc |
| <ul><li>Mueva el cursor hacia adelante por las opciones disponibles en el componente Selector de fecha .</li><li>Definir el enfoque de la pestaña en el icono del calendario cuando el campo de entrada de fecha está activo</li> | Ficha |
| Mover el cursor hacia atrás a través de las opciones disponibles en el componente Selector de fecha | Mayús + Tab |
| <ul><li>Mostrar las opciones del componente Selector de fecha cuando el tab focus resalta el campo de entrada de fecha</li><li>Mover el cursor hacia abajo en el calendario disponible en el componente Selector de fecha</li> | Flecha hacia abajo |
| Mover el cursor hacia arriba en el calendario disponible en el componente Selector de fecha | Flecha hacia arriba |
| Mover el cursor hacia atrás en el calendario disponible en el componente Selector de fecha | Flecha izquierda |
| Mover el cursor hacia adelante en el calendario disponible en el componente Selector de fecha | Flecha derecha |
| Realice la acción del rótulo disponible entre las flechas de navegación derecha e izquierda del calendario | Mayús + flecha arriba |
| Realice la acción para el icono de flecha de navegación derecha ![flecha derecha](assets/right-navigation-icon.svg) disponible en el calendario | Mayús + flecha izquierda |
| Realice la acción del icono de flecha de navegación izquierda ![flecha izquierda](assets/left-navigation-icon.svg) disponible en el calendario | Mayús + flecha derecha |

## Utilice la herramienta de accesibilidad para encontrar los problemas de accesibilidad restantes

El Inspector de nombres y descripciones accesibles (ANDI) le ayuda a identificar y corregir los problemas relacionados con el cumplimiento de la accesibilidad de forma adaptativa. Utilizar la herramienta ANDI para encontrar los problemas de accesibilidad de forma adaptativa:

1. Abra el formulario adaptable en modo de vista previa.
1. Haga clic en el icono de herramienta ANDI marcado. La herramienta ANDI analiza el formulario adaptable y muestra los problemas de accesibilidad. Para obtener más información sobre cómo utilizar la herramienta, consulte la [documentación de ANDI](https://www.ssa.gov/accessibility/andi/help/howtouse.html).
1. Revise y corrija los problemas notificados por ANDI.