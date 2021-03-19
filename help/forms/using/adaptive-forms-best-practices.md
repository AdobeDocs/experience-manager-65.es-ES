---
title: 'Prácticas recomendadas para usar formularios adaptables '
seo-title: 'Prácticas recomendadas para usar formularios adaptables '
description: Explica las prácticas recomendadas para configurar un proyecto de AEM Forms, desarrollar formularios adaptables y optimizar el rendimiento del sistema AEM Forms.
seo-description: Explica las prácticas recomendadas para configurar un proyecto de AEM Forms, desarrollar formularios adaptables y optimizar el rendimiento del sistema AEM Forms.
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
feature: Formularios adaptables
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '4298'
ht-degree: 0%

---


# Prácticas recomendadas para usar formularios adaptables{#best-practices-for-working-with-adaptive-forms} 

## Información general {#overview}

Los formularios de Adobe Experience Manager (AEM) pueden ayudarle a transformar transacciones complejas en experiencias digitales simples y atractivas. Sin embargo, requiere un esfuerzo concertado para implementar, construir, ejecutar y mantener un ecosistema AEM Forms eficiente y productivo.

Este documento proporciona directrices y recomendaciones de las que pueden beneficiarse el administrador de formularios, los autores y los desarrolladores al trabajar con AEM Forms, especialmente con el componente de formularios adaptables. Se tratan las prácticas recomendadas, desde la configuración de un proyecto de desarrollo de formularios hasta la configuración, personalización, creación y optimización de AEM Forms. Estas prácticas recomendadas contribuyen colectivamente al rendimiento general del ecosistema de AEM Forms.

Además, estas son algunas lecturas recomendadas para prácticas recomendadas generales AEM:

* [Prácticas recomendadas: Implementación y mantenimiento de AEM](/help/sites-deploying/best-practices.md)
* [Prácticas recomendadas: Creación de contenido](/help/sites-authoring/best-practices.md)
* [Prácticas recomendadas: Administración de AEM](/help/sites-administering/administer-best-practices.md)
* [Prácticas recomendadas: Desarrollo de soluciones](/help/sites-developing/best-practices.md)

## Configuración de AEM Forms {#set-up-and-configure-aem-forms}

### Configuración del proyecto de desarrollo de formularios {#setting-up-forms-development-project}

Una estructura de proyecto simplificada y estandarizada puede reducir considerablemente los esfuerzos de desarrollo y mantenimiento. Apache Maven es una herramienta de código abierto recomendada para la creación de AEM proyectos.

* Utilice Apache Maven `aem-project-archetype` para crear y administrar la estructura de AEM proyecto. Crea plantillas y estructura recomendadas para el proyecto de AEM. Además, proporciona automatización de la compilación y sistemas de control de cambios para ayudar a administrar el proyecto.

   * Utilice el comando maven `archetype:generate` para generar la estructura inicial.
   * Utilice el comando maven `eclipse:eclipse` para generar los archivos de proyecto eclipse e importar el proyecto en eclipse.

Para obtener más información, consulte [Cómo crear proyectos AEM utilizando Apache Maven](/help/sites-developing/ht-projects-maven.md).

* La herramienta FileVault o VLT le ayuda a asignar el contenido de una instancia CRX o AEM a su sistema de archivos. Proporciona operaciones de administración del control de cambios, como el registro y la salida del contenido del proyecto AEM. Consulte [Cómo utilizar la herramienta VLT](/help/sites-developing/ht-vlttool.md).

* Si utiliza el entorno de desarrollo integrado en Eclipse, puede utilizar AEM herramientas de desarrollo para la integración perfecta de Eclipse IDE con instancias de AEM para crear aplicaciones de AEM. Para obtener más información, consulte [AEM herramientas para desarrolladores de Eclipse](/help/sites-developing/aem-eclipse.md).

* No almacene ningún contenido ni realice ninguna modificación en la carpeta /libs. Cree superposiciones en carpetas /app para ampliar o sobrescribir las funcionalidades predeterminadas.

* Cuando cree paquetes para mover contenido, asegúrese de que las rutas de filtro de paquetes sean correctas y solo se mencionen las rutas requeridas.

* No almacene ningún contenido ni realice ninguna modificación en la carpeta /libs. Cree superposiciones en carpetas /app para ampliar o sobrescribir las funcionalidades predeterminadas.

* Defina las dependencias correctas para que los paquetes obliguen a un orden o secuencia de instalación predeterminados.

* No cree ningún nodo referenciable en /libs o /apps.

### Planificación del entorno de creación {#planning-for-authoring-environment}

Una vez configurado el proyecto AEM, defina una estrategia para crear y personalizar plantillas y componentes de formularios adaptables.

* Una plantilla de formulario adaptable es una página AEM especializada que define la estructura y la información de encabezado y pie de página de un formulario adaptable. Una plantilla tiene diseños, estilos y estructura básicos preconfigurados para un formulario adaptable. AEM Forms proporciona plantillas y componentes integrados que puede utilizar para crear formularios adaptables. Sin embargo, puede crear plantillas y componentes personalizados según sus necesidades. Se recomienda recopilar los requisitos para plantillas y componentes adicionales que necesite en los formularios adaptables. Para obtener más información, consulte [Personalización de formularios y componentes adaptables](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* AEM Forms permite crear formularios adaptables basados en los siguientes modelos de formulario. Los modelos de formulario actúan como interfaz para el intercambio de datos entre un formulario y AEM sistema y proporcionan una estructura basada en XML para el flujo de datos dentro y fuera de un formulario adaptable. Además, los modelos de formulario imponen reglas y restricciones en los formularios adaptables en forma de restricciones de esquema y XFA.

   * **Ninguno**: Los formularios adaptables creados con esta opción no utilizan ningún modelo de formulario. El XML de datos generado a partir de estos formularios tiene una estructura plana con campos y valores correspondientes.
   * **Esquema** XML o JSON: Los esquemas XML y JSON representan la estructura en la que el sistema back-end de su organización produce o consume los datos. Puede asociar un esquema a un formulario adaptable y utilizar sus elementos para agregar contenido dinámico al formulario adaptable. Los elementos del esquema están disponibles en la ficha Objeto del modelo de datos del navegador de contenido para la creación de formularios adaptables. Puede arrastrar y soltar los elementos de esquema para crear el formulario.
   * **Plantilla** de formulario XFA: Es un modelo de formulario ideal si tiene inversiones en formularios HTML5 basados en XFA. Proporciona una forma directa de convertir los formularios basados en XFA en formularios adaptables. Cualquier regla XFA existente se conserva en los formularios adaptables asociados. Los formularios adaptables resultantes admiten construcciones XFA, como validaciones, eventos, propiedades y patrones.
   * **Modelo** de datos de formulario: Es un modelo de formulario preferido si desea integrar sistemas backend como bases de datos, servicios web y AEM perfil de usuario para rellenar previamente formularios adaptables y escribir datos de formulario enviados de nuevo en los sistemas backend. Un editor del Modelo de datos de formulario permite definir y configurar entidades y servicios en un modelo de datos de formulario que se puede utilizar para crear formularios adaptables. Para obtener más información, consulte [Integración de datos de AEM Forms](/help/forms/using/data-integration.md).

Es importante elegir cuidadosamente el modelo de datos que no solo se adapte a sus necesidades, sino que amplíe sus inversiones existentes en activos XFA y XSD, si las hay. Se recomienda utilizar el modelo XSD para crear plantillas de formulario porque el XML generado contiene datos según XPATH definido por el esquema. El uso del modelo XSD como opción predeterminada para el modelo de datos de formulario también es útil porque desvincula el diseño de formulario del sistema back-end que procesa y consume datos y mejora el rendimiento del formulario debido a que se asigna de uno a uno el campo de formulario. Además, BindRef del campo puede convertirse en el XPATH de su valor de datos en XML.

Para obtener más información, consulte [Creación de un formulario adaptable](/help/forms/using/creating-adaptive-form.md).

* Hay algunas secciones comunes en los formularios adaptables. Puede identificarlos y definir una estrategia para promover la reutilización del contenido. Los formularios adaptables permiten crear fragmentos independientes y reutilizarlos en todos los formularios. También puede guardar un panel en un formulario adaptable como un fragmento. Cualquier cambio en un fragmento se refleja en todos los formularios asociados. Ayuda a reducir el tiempo de creación y garantiza la coherencia en todos los formularios. Además, el uso de fragmentos hace que los formularios adaptables sean ligeros, lo que mejora la experiencia de creación, especialmente de formularios grandes. Para obtener más información, consulte [Fragmentos de formulario adaptables](/help/forms/using/adaptive-form-fragments.md).

### Personalización de formularios y componentes adaptables {#customize-components}

* AEM Forms proporciona plantillas de formulario adaptables integradas que puede utilizar para crear formularios adaptables. También puede crear sus propias plantillas. AEM proporciona plantillas estáticas y editables.

   * Los desarrolladores definen y configuran las plantillas estáticas.
   * Los autores crean plantillas editables mediante el editor de plantillas. El editor de plantillas permite definir una estructura básica y contenido inicial en una plantilla. Cualquier modificación en la capa de estructura se refleja en todos los formularios que utilizan esa plantilla. El contenido inicial puede incluir un tema preconfigurado, un servicio de relleno previo, una acción de envío, etc. Sin embargo, esta configuración se puede modificar para un formulario con el editor de formularios. Para obtener más información, consulte [Plantillas de formulario adaptables](/help/forms/using/template-editor.md).

* Para aplicar estilo a un campo o panel específico, utilice [estilos en línea](/help/forms/using/inline-style-adaptive-forms.md). Como alternativa, puede definir una clase en un archivo CSS y especificar el nombre de la clase en la propiedad Clase CSS del componente.
* Incluya una biblioteca de cliente en un componente para aplicar estilos de forma coherente en todos los formularios adaptables o fragmentos que utilicen ese componente. Para obtener más información, consulte [Creación de un componente de página de formulario adaptable](/help/forms/using/custom-adaptive-forms-templates.md).
* Aplique estilos definidos en una biblioteca de cliente para seleccionar formularios adaptables especificando la ruta a la biblioteca de cliente en el campo de ruta del archivo CSS en las propiedades del contenedor de formularios adaptables.
* Para crear una biblioteca de cliente de los estilos, puede configurar el archivo CSS personalizado en la clientlib base del Editor de temas o en las propiedades del contenedor de formularios.
* Los formularios adaptables proporcionan diseños de panel, como capacidad de respuesta, tabulación, acordeones y asistente, para controlar cómo se distribuyen los componentes de formulario en un panel. Puede crear diseños de panel personalizados y ponerlos a disposición de los autores de formularios para su uso. Para obtener más información, consulte [Creación de componentes de diseño personalizados para formularios adaptables](/help/forms/using/custom-layout-components-forms.md).
* También puede personalizar componentes de formulario adaptables específicos, como campos y diseño de panel.

   * Utilice la funcionalidad [Overlay](/help/sites-developing/overlays.md) de AEM para modificar una copia de un componente. No se recomienda modificar los componentes predeterminados.
   * Para personalizar el diseño de los componentes de formulario adaptables listos para usar en /libs, [cree componentes de diseño personalizados](/help/forms/using/custom-layout-components-forms.md) además de los [diseños predeterminados](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * Introduzca interactividades personalizadas mediante la creación de widgets o apariciones personalizados. No se recomienda modificar los componentes predeterminados. Para obtener más información, consulte [Aspecto framework](/help/forms/using/introduction-widgets.md).

* Consulte [Gestión de información de identificación personal](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) para ver las recomendaciones sobre la gestión de datos PII.

## Creación de formularios adaptables {#author-adaptive-forms}

### Uso de la IU táctil para la creación {#using-touch-optimized-ui-for-authoring}

* Utilice el explorador de objetos de la barra lateral para acceder rápidamente a los campos situados en la parte inferior de la jerarquía del formulario. Puede utilizar el cuadro de búsqueda para buscar objetos en el árbol de objetos o formularios y navegar de un objeto a otro.
* Para ver y editar las propiedades de un componente en el navegador de componentes de la barra lateral, seleccione el componente y haga clic en ![cmppr-1](assets/cmppr-1.png). También puede hacer doble clic en un componente para ver sus propiedades en el navegador de propiedades.
* Utilice los métodos abreviados del teclado para realizar acciones rápidas en los formularios. Consulte [Atajos de teclado de AEM Forms](/help/forms/using/keyboard-shortcuts.md).

* Se recomiendan los componentes de formulario adaptables para su uso únicamente en páginas de formulario adaptables. Los componentes dependen de su jerarquía principal. Por lo tanto, no los utilice en una página AEM.

Además, consulte las descripciones de los componentes y las prácticas recomendadas en [Introducción a la creación de formularios adaptables](/help/forms/using/introduction-forms-authoring.md).

### Uso de reglas en formularios adaptables {#using-rules-in-adaptive-forms}

AEM Forms proporciona un [editor de reglas](/help/forms/using/rule-editor.md) que le permite crear reglas para agregar comportamiento dinámico a los componentes del formulario adaptable. Con estas reglas, se pueden evaluar condiciones y acciones de déclencheur en componentes como mostrar u ocultar campos, calcular valores, cambiar listas desplegables de forma dinámica, etc.

El editor de reglas proporciona un editor visual y un editor de código para escribir reglas. Tenga en cuenta lo siguiente al escribir reglas mediante el modo de editor de código:

* Utilice nombres significativos y únicos para los campos y componentes de formulario para evitar posibles conflictos al escribir reglas.
* Utilice el operador `this` para que un componente se haga referencia a sí mismo en una expresión de regla. Garantiza que la regla siga siendo válida incluso si cambia el nombre del componente. Por ejemplo, `field1.valueCommit script: this.value > 10`.

* Utilice nombres de componentes cuando haga referencia a otros componentes del formulario. Utilice la propiedad `value` para recuperar el valor de un campo o componente. Por ejemplo, `field1.value`.

* Consulte los componentes por jerarquía única relativa para evitar conflictos. Por ejemplo, `parentName.fieldName`.

* Cuando gestione reglas complejas o comúnmente utilizadas, considere la posibilidad de escribir lógica empresarial como funciones en una biblioteca de cliente independiente que puede especificar y reutilizar en formularios adaptables. La biblioteca cliente debe ser una biblioteca independiente y no debe tener dependencias externas, excepto jQuery y Underscore.js. También puede utilizar la biblioteca de cliente para aplicar la [revalidación del lado del servidor](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) de los datos de formulario enviados.
* Los formularios adaptables proporcionan un conjunto de API que puede utilizar para comunicarse con los formularios adaptables y realizar acciones en ellos. Algunas de las API clave son las siguientes: Para obtener más información, consulte [Referencia de la API de la biblioteca JavaScript para Forms adaptable](https://adobe.com/go/learn_aemforms_documentation_63).

   * `guideBridge.reset()`: Restablece un formulario.
   * `guideBridge.submit()`: Envía un formulario.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`: Define el enfoque en un campo.
   * `guideBridge.validate(errorList, somExpression, focus)`: Valida un formulario.
   * `guideBridge.getDataXML(options)`: Obtiene los datos de formulario como XML.
   * `guideBridge.resolveNode(somExpression)`: Obtiene un objeto de formulario.
   * `guideBridge.setProperty(somList, propertyName, valueList)`: Define la propiedad de un objeto de formulario.
   * Además, puede utilizar las siguientes propiedades de campo:

      * `field.value` para cambiar el valor de un campo.
      * f `ield.enabled` para habilitar/deshabilitar un campo.
      * `field.visible` para cambiar la visibilidad de un campo.

* Es posible que los autores de formularios adaptables tengan que escribir código JavaScript para crear lógica empresarial en un formulario. Aunque JavaScript es potente y eficaz, es probable que pueda comprometer las expectativas de seguridad. Por lo tanto, debe asegurarse de que el autor del formulario es una persona de confianza y de que hay procesos para revisar y aprobar el código JavaScript antes de que se ponga en producción un formulario. El administrador puede restringir el acceso al editor de reglas a los grupos de usuarios en función de su función o función. Consulte [Conceder acceso al editor de reglas a grupos de usuarios seleccionados](/help/forms/using/rule-editor-access-user-groups.md).
* Puede utilizar expresiones en reglas para hacer dinámicos los formularios adaptables. Todas las expresiones son expresiones de JavaScript válidas y utilizan API de modelos de secuencias de comandos de formularios adaptables. Estas expresiones devuelven valores de ciertos tipos. Para obtener más información sobre las expresiones y las prácticas recomendadas a su alrededor, consulte [expresiones de formulario adaptables](/help/forms/using/adaptive-form-expressions.md).

### Trabajo con temas {#working-with-themes}

La adaptación para los temas le permite crear estilos reutilizables que se pueden aplicar en todos los formularios para conseguir un aspecto y un estilo coherentes. Se recomienda utilizar Temas para definir el estilo de los componentes y paneles del formulario. Algunas prácticas recomendadas relacionadas con los temas son las siguientes:

* Utilice la biblioteca de recursos para aplicar rápidamente estilos de texto, fondo e imágenes. Cuando se añade un estilo en la biblioteca de recursos, está disponible para otros temas y en el modo de estilo del editor de formularios.
* Aplique la configuración global como fuente y fondo de página mediante el selector de nivel de página.
* Utilice bibliotecas de cliente para importar estilos existentes o avanzados en sus temas.
* Puede anular el estilo de campos, paneles o botones específicos de una capa de estilo de formulario.
* Si un tema no cumple los requisitos de estilo, puede utilizar clases predefinidas como guideFieldNode, guideFieldLabel, guideFieldWidget y guidePanelNode para aplicar un estilo común a todos los formularios.

Para obtener más información, consulte [Temas](/help/forms/using/themes.md).

### Optimización del rendimiento de formularios grandes y complejos {#optimizing-performance-of-large-and-complex-forms}

Los autores de formularios y los usuarios finales suelen tener problemas de rendimiento al cargar formularios grandes en modo de creación o durante la ejecución. A medida que aumenta el número de objetos (campos y paneles) en el formulario, la experiencia de creación y ejecución comienza a degradarse. También evita que varios autores colaboren y creen un formulario simultáneamente.

Tenga en cuenta las siguientes prácticas recomendadas para superar los problemas de rendimiento con formularios grandes:

* Se recomienda crear formularios adaptables utilizando el modelo de datos de formulario XSD incluso cuando sea posible convertir un XFA a un formulario adaptable.
* Incluir solo los campos y paneles en formularios adaptables que capturan información del usuario. Considere la posibilidad de mantener el contenido estático como mínimo o utilice direcciones URL para abrirlo en una ventana independiente.
* Aunque cada formulario está diseñado para un propósito específico, hay algunos segmentos comunes en la mayoría de los formularios. Por ejemplo: detalles personales, dirección, detalles de empleo, etc. Cree [fragmentos de formulario adaptables](/help/forms/using/adaptive-form-fragments.md) para elementos de formulario y secciones comunes y utilícelos en todos los formularios. También puede guardar un panel en un formulario existente como fragmento. Cualquier cambio en un fragmento se refleja en todos los formularios adaptables asociados. Promueve la creación colaborativa, ya que varios autores pueden trabajar simultáneamente en diferentes fragmentos que conforman un formulario.

   * De forma similar a los formularios adaptables, se recomienda que todos los estilos específicos de fragmento y las secuencias de comandos personalizadas se definan en la biblioteca de cliente mediante el cuadro de diálogo contenedor de fragmentos. Además, intente crear fragmentos autosuficientes que no dependan de objetos externos.
   * Evite utilizar secuencias de comandos entre fragmentos. Si hay algún objeto fuera del fragmento al que deba hacer referencia, intente que dicho objeto forme parte del formulario principal. Si el objeto debe seguir residiendo en otro fragmento, consulte con él por su nombre en la secuencia de comandos.

* Utilice Guardar y reanudar con el guardado automático para guardar el formulario adaptable periódicamente y permitir que los usuarios vuelvan más tarde para completar el formulario.
* Configure los fragmentos para que se carguen de forma diferida. Durante el tiempo de ejecución, los fragmentos marcados para cargarse de forma diferida solo se representan cuando son necesarios. Reduce significativamente el tiempo de carga de los formularios grandes. También se admite en fragmentos con paneles repetibles. Para obtener más información, consulte [Configuración de carga diferida](/help/forms/using/lazy-loading-adaptive-forms.md).

   * No configure la carga diferida en fragmentos en un diseño de cuadrícula adaptable o en el primer panel.
   * Los componentes de archivo adjunto y Términos y condiciones no son compatibles con los fragmentos cargados de forma diferida.
   * Marque un valor en un panel cargado de forma diferida como Usar valor globalmente si ese valor se utiliza en alguna otra parte del formulario, de modo que el valor esté disponible para su uso cuando se descargue el panel que lo contiene.
   * Considere la posibilidad de escribir reglas de visibilidad para fragmentos que deban mostrarse u ocultarse según una condición.

### Rellenado previo de formularios adaptables {#prefilling-adaptive-forms}

Puede rellenar previamente los campos de formulario adaptables con datos recuperados del servidor para ayudar a los usuarios a rellenar rápidamente el formulario y evitar errores de escritura.

* AEM Forms proporciona un servicio de cumplimentación previa para leer datos de un archivo XML de datos predefinido y rellenar previamente los campos de un formulario adaptable con el contenido del archivo XML de relleno previo.
* El XML de datos de relleno previo debe ser compatible con el esquema del modelo de formulario asociado al formulario adaptable.
* Incluya las secciones `afBoundedData` y `afUnBoundedData` en el XML de relleno previo para rellenar previamente los campos enlazados y no enlazados en un formulario adaptable.

* Para los formularios adaptables basados en el modelo de datos de formulario, AEM Forms proporciona el servicio de rellenado previo del modelo de datos de formulario integrado. El servicio de relleno previo consulta los orígenes de datos de los objetos del modelo de datos en el formulario adaptable y prefiere los valores de campo al procesar el formulario.
* También puede utilizar los protocolos de archivo, crx, servicio o http para rellenar previamente los formularios adaptables.
* AEM Forms admite servicios de relleno previo personalizados que se pueden insertar como servicio OSGi para rellenar previamente formularios adaptables.

Para obtener más información, consulte [Relleno previo de campos de formulario adaptables](/help/forms/using/prepopulate-adaptive-form-fields.md).

### Firma y envío de formularios adaptables {#signing-and-submitting-adaptive-forms}

Los formularios adaptables requieren Enviar acciones para procesar los datos especificados por el usuario. Una acción Enviar determina la tarea realizada en los datos enviados mediante un formulario adaptable.

* Hay varias acciones de envío disponibles de forma predeterminada en los formularios adaptables. Para obtener más información, consulte [Configuración de la acción de envío](/help/forms/using/configuring-submit-actions.md).
* Puede escribir una acción de envío personalizada si las acciones de envío predeterminadas no cumplen con su caso de uso. Para obtener más información, consulte [Escritura de acción de envío personalizada para formularios adaptables](/help/forms/using/custom-submit-action-form.md).
* Incluya validaciones del lado del servidor para evitar el envío de datos no válidos.

Puede aprovechar la experiencia de varios signos de Adobe Sign en los formularios adaptables. Tenga en cuenta lo siguiente al configurar Adobe Sign en formularios adaptables. Para obtener más información, consulte [Uso de Adobe Sign en un formulario adaptable](/help/forms/using/working-with-adobe-sign.md).

* El formulario adaptable habilitado para Adobe Sign solo se envía después de que todos los firmantes hayan firmado el formulario. Forms aparece en estado de firma pendiente hasta que todos los firmantes firman el formulario.
* Puede configurar la experiencia de firma en el formulario o redirigir a los firmantes a una página de firma en el envío.
* Configure la experiencia de firma secuencial o paralela, según corresponda.

### Generación del documento de registro {#generating-document-of-record}

Un documento de registro (DoR) es una versión PDF aplanada de un formulario adaptable que se puede imprimir, firmar o archivar.

* Según el modelo de datos de formulario en el que se base un formulario adaptable, puede configurar una plantilla para DoR de la siguiente manera:

   * **Plantilla** de formulario XFA: Utilice el archivo XDP asociado como plantilla de DoR.
   * **Esquema** XSD: Utilice la plantilla XFA asociada que utilice el mismo esquema XML utilizado por el formulario adaptable.
   * **Ninguno**: Utilizar el DoR generado automáticamente.

* Configure el encabezado, pie de página, imágenes, color, fuente, etc. a la derecha de la ficha Documento de registro del editor de formularios adaptables.
* Utilice `DoRService` para generar el DoR mediante programación.
* Excluir campos ocultos del documento de trabajo.
* Utilice el parámetro de solicitud `afAcceptLang` para ver el DoR en otra configuración regional.

### Depuración y prueba de formularios adaptables {#debugging-and-testing-adaptive-forms}

[AEM complemento de Chrome ](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) es una extensión de explorador para Google Chrome que proporciona herramientas para depurar formularios adaptables. Los creadores y desarrolladores de formularios pueden utilizar estas herramientas para:

* Identificar cuellos de botella y optimizar el rendimiento de la renderización del formulario
* Depurar palabras clave y errores bindRef en el formulario
* Habilitar y configurar registros
* Depuración de reglas y secuencias de comandos en el formulario
* Explorar y obtener más información sobre las API de guideBridge

Para obtener más información, consulte [AEM Complemento de Chrome: Formulario adaptable](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

El SDK de Calvin es una API de utilidad para que los desarrolladores de Forms adaptables prueben el Forms adaptable. El SDK de Calvin se basa en el [marco de pruebas Hobbes.js](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/test-api/index.html). Puede utilizar el marco para probar lo siguiente:

* Experiencia de representación de un formulario adaptable
* Experiencia de cumplimentación previa de un formulario adaptable
* Enviar experiencia de un formulario adaptable
* Reglas de expresión
* Validaciones
* Carga diferida

Para obtener más información, consulte [Automatización de la prueba de formularios adaptables](/help/forms/using/calvin.md).

### Validación de formularios adaptables en AEM servidor {#validating-adaptive-forms-on-aem-server}

Las validaciones del lado del servidor son necesarias para evitar cualquier intento de omitir las validaciones en el cliente y cualquier posible compromiso de los envíos de datos y las violaciones de reglas comerciales. Las validaciones del lado del servidor se ejecutan en el servidor cargando la biblioteca de cliente necesaria.

* Incluya funciones en una biblioteca de cliente para validar expresiones en formularios adaptables y especifique la biblioteca de cliente en el cuadro de diálogo contenedor de formularios adaptables. Para obtener más información, consulte [Revalidación del lado del servidor](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* La validación del lado del servidor valida el modelo de formulario. Se recomienda crear una biblioteca de cliente independiente para las validaciones y no mezclarla con otras cosas como el estilo HTML y la manipulación DOM en la misma biblioteca de cliente.

### Localización de formularios adaptables {#localizing-adaptive-forms}

AEM proporciona flujos de trabajo de traducción que puede utilizar para localizar formularios adaptables. Para obtener más información, consulte [Uso de AEM flujo de trabajo de traducción para localizar formularios adaptables](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

Algunas prácticas recomendadas al localizar formularios adaptables son las siguientes:

* Utilice fragmentos de formulario adaptables para elementos comunes en todos los formularios y localice fragmentos. Garantiza que localice un fragmento una vez y refleja en todos los formularios en los que se utiliza el fragmento localizado.
* Las modificaciones como la adición de un componente nuevo o la aplicación de una secuencia de comandos en un formulario localizado no se localizan automáticamente. Por lo tanto, debe finalizar un formulario antes de localizarlo para evitar múltiples ciclos de localización.
* Utilice el parámetro de solicitud `afAcceptLang` para anular la configuración regional del explorador y procesar el formulario en la configuración regional especificada. Por ejemplo, la siguiente URL obligará a procesar el formulario en la configuración regional de japonés, independientemente de la configuración regional especificada en la configuración del explorador:

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms admite actualmente la localización de contenido de formularios adaptables en las configuraciones regionales de inglés (en), español (es), francés (fr), italiano (it), alemán (de), japonés (ja), portugués-brasileño (pt-BR), chino (zh-CN), chino-taiwanés (zh-TW) y coreano (ko-KR). Sin embargo, se puede agregar compatibilidad con nuevas configuraciones regionales para formularios adaptables en tiempo de ejecución. Para obtener más información, consulte [Compatibilidad con nuevas configuraciones regionales para la localización de formularios adaptables](/help/forms/using/supporting-new-language-localization.md).

## Preparar el proyecto de formularios para producción {#prepare-forms-project-for-production}

### Adición de un servidor de procesamiento de formularios {#adding-forms-processing-server}

Puede configurar una instancia adicional del servidor de AEM Forms que reside detrás del cortafuegos en una zona segura. Puede utilizar esta instancia para:

* **Procesamiento** por lotes: trabajos que son recurrentes o programados en lotes con una carga pesada. Por ejemplo, imprimir instrucciones, generar correspondencias y utilizar servicios de documentos como PDF Generator, Output y Assembler.
* **Almacenamiento de datos** PII: Guarde los datos PII en el servidor de procesamiento. No es obligatorio si ya está utilizando un proveedor de almacenamiento personalizado para almacenar datos PII.

### Mover el proyecto a otro entorno {#moving-project-to-another-environment}

A menudo, debe mover los proyectos de AEM de un entorno a otro. Algunas de las cosas clave que hay que recordar al moverse son las siguientes:

* Haga una copia de seguridad de las bibliotecas de cliente, el código personalizado y las configuraciones existentes.
* Implemente paquetes de productos y parches manualmente y en el orden especificado en el nuevo entorno.
* Implemente paquetes de código específicos del proyecto y paquetes manualmente y como paquete o paquete separado en el nuevo servidor de AEM.
* (*AEM Forms en JEE solamente*) Implemente LCA y DSC manualmente en el servidor de Forms Workflow.
* Utilice la funcionalidad [Export-Import](/help/forms/using/import-export-forms-templates.md) para mover recursos al nuevo entorno. También puede configurar el agente de replicación y publicar los recursos.
* Al actualizar, reemplace todas las API y características obsoletas con nuevas API y características.

### Configuración de AEM {#configuring-aem}

Algunas prácticas recomendadas para configurar AEM para mejorar el rendimiento general son las siguientes:

* Habilite la compresión de la biblioteca de cliente HTML para JavaScript y CSS desde la consola Felix. Consulte [Clientlibs explicados por ejemplo](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/).
* Almacene en caché todas las bibliotecas de cliente en `/etc.clientlibs/fd` y cualquier biblioteca de cliente personalizada adicional en AEM Dispatcher para aumentar la capacidad de respuesta y seguridad de los formularios publicados. Para obtener más información, consulte [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* No almacene en caché las rutas `/content/forms/af/` y `/content/dam/formsanddocuments/*`. para obtener información detallada sobre la configuración del almacenamiento en caché de formularios adaptables, consulte [Almacenamiento en caché de formularios adaptables](/help/forms/using/configure-adaptive-forms-cache.md).

* Habilite HTML mediante el módulo de compresión del servidor web. Para obtener más información, consulte [Ajuste de rendimiento del servidor AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Aumente las llamadas por configuración de solicitud para formularios grandes. Consulte [Optimización del rendimiento de formularios grandes y complejos](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* Cree [páginas de error personalizadas que se muestran mediante el controlador de error](https://helpx.adobe.com/experience-manager/6-2/sites-developing/customizing-errorhandler-pages.html).
* Servidor AEM Forms seguro.

   * Utilice el modo de ejecución `nosamplecontent` para asegurarse de que no hay contenido de muestra ni usuarios de muestra implementados en el servidor de producción. Consulte [Ejecución de AEM en modo preparado para producción](/help/sites-administering/production-ready.md).

* Mantenga el tamaño de pila a un mínimo de 8 GB. Para otras configuraciones, consulte [Ajuste de rendimiento del servidor AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Utilice sesiones de usuario de servicio en lugar de sesiones de administración para ejecutar tareas de nivel de servicio. Para obtener más información, consulte [Autenticación de servicio](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### Configuración del almacenamiento externo para borradores y datos de formularios enviados {#external-storage}

En un entorno de producción, se recomienda no almacenar los datos de formulario enviados en AEM repositorio. La implementación predeterminada de las acciones de envío de Forms Portal Store, Store Content y Store PDF almacena datos de formulario en AEM repositorio. Estas acciones de envío solo están pensadas para fines de demostración. Además, las funciones Guardar y reanudar y Guardar automáticamente utilizan el almacenamiento del portal de forma predeterminada. Por lo tanto, considere las siguientes recomendaciones:

* **Almacenamiento de datos** de borrador: Si utiliza la función Borrador de los formularios adaptables, debe implementar una interfaz de proveedor de servicios (SPI) personalizada para almacenar los datos en borrador en un almacenamiento más seguro, como la base de datos. Para obtener más información, consulte [Ejemplo para integrar borradores y componentes de envío con la base de datos](/help/forms/using/integrate-draft-submission-database.md).

* **Almacenamiento de datos** de envío: Si utiliza el almacén de envío del portal de formularios, debe implementar un SPI personalizado para almacenar los datos de envío en una base de datos. Consulte [Ejemplo para integrar borradores y componentes de envío con la base de datos](/help/forms/using/integrate-draft-submission-database.md) para obtener una integración de ejemplo.

   También puede escribir una acción de envío personalizada que almacene datos de formulario y datos adjuntos en un almacenamiento seguro. Consulte [Escritura de acción de envío personalizada para formularios adaptables](/help/forms/using/custom-submit-action-form.md) para obtener más información.

* **Longitud del ID** de borrador: Al guardar un formulario adaptable como borrador, se genera un ID de borrador para identificar el borrador de forma exclusiva. El valor mínimo de la longitud del campo de ID de borrador es de 26 caracteres. Adobe recomienda establecer la longitud del ID de borrador en 26 caracteres o más.

### Administración de información de identificación personal {#handling-personally-identifiable-information}

Uno de los desafíos clave para las organizaciones es cómo manejar los datos de identificación personal (PII). A continuación se indican algunas prácticas recomendadas que le ayudarán a gestionar estos datos:

* Utilice un almacenamiento externo seguro como la base de datos para almacenar datos de formularios en borrador y enviados. Consulte [Configuración del almacenamiento externo para borradores y datos de formularios enviados](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* Utilice el componente de formulario Términos y condiciones para obtener el consentimiento explícito del usuario antes de activar el guardado automático. En este caso, habilite el guardado automático solo cuando el usuario acepte las condiciones del componente Términos y condiciones .

