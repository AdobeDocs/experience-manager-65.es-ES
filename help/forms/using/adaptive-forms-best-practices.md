---
title: 'Prácticas recomendadas para usar formularios adaptables '
seo-title: 'Prácticas recomendadas para usar formularios adaptables '
description: Explica las prácticas recomendadas para configurar un proyecto de AEM Forms, desarrollar formularios adaptables y optimizar el rendimiento del sistema AEM Forms.
seo-description: Explica las prácticas recomendadas para configurar un proyecto de AEM Forms, desarrollar formularios adaptables y optimizar el rendimiento del sistema AEM Forms.
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
translation-type: tm+mt
source-git-commit: 615b0db6da0986d7a74c42ec0d0e14bad7ede168
workflow-type: tm+mt
source-wordcount: '4296'
ht-degree: 0%

---


# Prácticas recomendadas para usar formularios adaptables{#best-practices-for-working-with-adaptive-forms} 

## Información general {#overview}

Los formularios de Adobe Experience Manager (AEM) pueden ayudarle a transformar transacciones complejas en experiencias digitales sencillas y atractivas. Sin embargo, requiere un esfuerzo concertado para implementar, construir, ejecutar y mantener un ecosistema AEM Forms eficiente y productivo.

Este documento proporciona directrices y recomendaciones de las que pueden beneficiarse los administradores, autores y desarrolladores de formularios al trabajar con AEM Forms, especialmente con el componente de formularios adaptables. Se analizan las prácticas recomendadas desde la configuración de un proyecto de desarrollo de formularios hasta la configuración, personalización, creación y optimización de AEM Forms. Estas prácticas recomendadas contribuyen colectivamente al rendimiento general del ecosistema de AEM Forms.

Además, se recomiendan algunas lecturas para prácticas recomendadas generales AEM:

* [Prácticas recomendadas: Implementación y mantenimiento de AEM](/help/sites-deploying/best-practices.md)
* [Prácticas recomendadas: Creación de contenido](/help/sites-authoring/best-practices.md)
* [Prácticas recomendadas: Administración de AEM](/help/sites-administering/administer-best-practices.md)
* [Prácticas recomendadas: Desarrollo de soluciones](/help/sites-developing/best-practices.md)

## Configurar y configurar AEM Forms {#set-up-and-configure-aem-forms}

### Configuración del proyecto de desarrollo de formularios {#setting-up-forms-development-project}

Una estructura de proyectos simplificada y estandarizada puede reducir considerablemente los esfuerzos de desarrollo y mantenimiento. Apache Maven es una herramienta de código abierto recomendada para construir proyectos AEM.

* Utilice Apache Maven `aem-project-archetype` para crear y administrar la estructura de AEM proyecto. Crea plantillas y estructura recomendadas para el proyecto de AEM. Además, proporciona automatización de la compilación y sistemas de control de cambios para ayudar a administrar el proyecto.

   * Utilice el comando maven `archetype:generate` para generar la estructura inicial.
   * Utilice el comando maven `eclipse:eclipse` para generar los archivos de proyecto eclipse e importar el proyecto en eclipse.

Para obtener más información, consulte [Cómo compilar AEM proyectos con Apache Maven](/help/sites-developing/ht-projects-maven.md).

* La herramienta FileVault o VLT le ayuda a asignar el contenido de una instancia de CRX o AEM al sistema de archivos. Proporciona operaciones de administración de control de cambios, como ingreso y salida del contenido del proyecto AEM. Consulte [Cómo utilizar la herramienta VLT](/help/sites-developing/ht-vlttool.md).

* Si utiliza el entorno de desarrollo integrado por Eclipse, puede utilizar AEM herramientas de desarrollador para la integración sin fisuras del IDE de Eclipse con instancias AEM para crear aplicaciones AEM. Para obtener más información, consulte [AEM herramientas para desarrolladores de Eclipse](/help/sites-developing/aem-eclipse.md).

* No almacene contenido ni realice modificaciones en la carpeta /libs. Cree superposiciones en las carpetas /app para ampliar o sobrescribir las funciones predeterminadas.

* Cuando cree paquetes para mover contenido, asegúrese de que las rutas de filtro del paquete son correctas y solo se mencionan las rutas requeridas.

* No almacene contenido ni realice modificaciones en la carpeta /libs. Cree superposiciones en las carpetas /app para ampliar o sobrescribir las funciones predeterminadas.

* Defina las dependencias correctas para los paquetes para forzar un orden o secuencia de instalación predeterminados.

* No cree ningún nodo referenciable en /libs o /apps.

### Planificación del entorno de creación {#planning-for-authoring-environment}

Una vez configurado el proyecto AEM, defina una estrategia para la creación y personalización de plantillas y componentes de formularios adaptables.

* Una plantilla de formulario adaptable es una página AEM especializada que define la estructura y la información de encabezado y pie de página de un formulario adaptable. Una plantilla tiene diseños, estilos y estructura básicos preconfigurados para un formulario adaptable. AEM Forms proporciona plantillas integradas y componentes que puede utilizar para crear formularios adaptables. Sin embargo, puede crear plantillas y componentes personalizados según sus necesidades. Se recomienda recopilar requisitos para plantillas y componentes adicionales que necesitará en los formularios adaptables. Para obtener más información, consulte [Personalización de formularios y componentes adaptables](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* AEM Forms permite crear formularios adaptables basados en los siguientes modelos de formulario. Los modelos de formulario actúan como interfaz para el intercambio de datos entre un formulario y AEM sistema y proporcionan una estructura basada en XML para el flujo de datos dentro y fuera de un formulario adaptable. Además, los modelos de formulario imponen reglas y restricciones a los formularios adaptables en forma de restricciones de esquema y XFA.

   * **Ninguno**: Los formularios adaptables creados con esta opción no utilizan ningún modelo de formulario. El XML de datos generado a partir de estos formularios tiene una estructura plana con campos y valores correspondientes.
   * **ESQUEMA** XML o JSON: Los esquemas XML y JSON representan la estructura en la que el sistema back-end de la organización produce o consume los datos. Puede asociar un esquema a un formulario adaptable y utilizar sus elementos para agregar contenido dinámico al formulario adaptable. Los elementos del esquema están disponibles en la ficha Objeto del modelo de datos del navegador de contenido para la creación de formularios adaptables. Puede arrastrar y soltar los elementos de esquema para crear el formulario.
   * **Plantilla** de formulario XFA: Es un modelo de formulario ideal si tiene inversiones en formularios HTML5 basados en XFA. Proporciona una forma directa de convertir los formularios basados en XFA en formularios adaptables. Las reglas XFA existentes se conservan en los formularios adaptables asociados. Los formularios adaptables resultantes admiten construcciones XFA, como validaciones, eventos, propiedades y patrones.
   * **Modelo** de datos de formulario: Es un modelo de formulario preferido si desea integrar sus sistemas de back-end como bases de datos, servicios Web y AEM perfil del usuario para rellenar formularios adaptables y escribir datos de formulario enviados en los sistemas de back-end. Un editor del modelo de datos de formulario permite definir y configurar entidades y servicios en un modelo de datos de formulario que se puede utilizar para crear formularios adaptables. Para obtener más información, consulte [Integración de datos de AEM Forms](/help/forms/using/data-integration.md).

Es importante elegir cuidadosamente el modelo de datos que no sólo se adapte a sus necesidades, sino que amplíe sus inversiones existentes en activos XFA y XSD, si los hay. Se recomienda utilizar el modelo XSD para crear plantillas de formulario porque el XML generado contiene datos según XPATH definido por esquema. El uso del modelo XSD como opción predeterminada para el modelo de datos de formulario también ayuda porque desvincula el diseño de formulario del sistema back-end que procesa y consume datos y mejora el rendimiento del formulario debido a la asignación de uno a uno del campo de formulario. Además, BindRef del campo puede convertirse en XPATH de su valor de datos en XML.

Para obtener más información, consulte [Creación de un formulario adaptable](/help/forms/using/creating-adaptive-form.md).

* Existen algunas secciones comunes en los formularios adaptables. Puede identificarlos y definir una estrategia para promover la reutilización del contenido. Los formularios adaptables permiten crear fragmentos independientes y reutilizarlos en distintos formularios. También puede guardar un panel en un formulario adaptable como un fragmento. Cualquier cambio en un fragmento se refleja en todos los formularios asociados. Ayuda a reducir el tiempo de creación y garantiza la coherencia entre los formularios. Además, el uso de fragmentos hace que los formularios adaptables sean livianos, lo que mejora la experiencia de creación, especialmente en formularios grandes. Para obtener más información, consulte [Fragmentos de formulario adaptables](/help/forms/using/adaptive-form-fragments.md).

### Personalización de formularios y componentes adaptables {#customize-components}

* AEM Forms proporciona plantillas de formulario adaptables integradas que puede utilizar para crear formularios adaptables. También puede crear sus propias plantillas. AEM proporciona plantillas estáticas y editables.

   * Los desarrolladores definen y configuran las plantillas estáticas.
   * Las plantillas editables las crean los autores mediante el editor de plantillas. El editor de plantillas permite definir una estructura básica y un contenido inicial en una plantilla. Cualquier modificación en la capa de estructura se refleja en todos los formularios que utilicen esa plantilla. El contenido inicial puede incluir tema preconfigurado, servicio de relleno previo, acción de envío, etc. Sin embargo, esta configuración se puede modificar para un formulario con el editor de formularios. Para obtener más información, consulte [Plantillas de formulario adaptables](/help/forms/using/template-editor.md).

* Para aplicar estilo a un campo o instancia de panel específicos, utilice [estilo en línea](/help/forms/using/inline-style-adaptive-forms.md). También puede definir una clase en un archivo CSS y especificar el nombre de la clase en la propiedad Clase CSS del componente.
* Incluya una biblioteca de cliente en un componente para aplicar estilos de forma coherente en todos los formularios adaptables o fragmentos que utilicen dicho componente. Para obtener más información, consulte [Creación de un componente de página de formulario adaptable](/help/forms/using/custom-adaptive-forms-templates.md).
* Aplique estilos definidos en una biblioteca de cliente para seleccionar formularios adaptables especificando la ruta de acceso a la biblioteca de cliente en el campo de ruta del archivo CSS en las propiedades del contenedor de formulario adaptable.
* Para crear una biblioteca de cliente de sus estilos, puede configurar el archivo CSS personalizado en la clientlib base del Editor de temas o en las propiedades del Contenedor de formularios.
* Los formularios adaptables proporcionan diseños de panel, como interactivos, tabuladores, acordeones y asistentes, para controlar cómo se distribuyen los componentes de un formulario en un panel. Puede crear diseños de panel personalizados y hacerlos disponibles para su uso por los autores de formularios. Para obtener más información, consulte [Creación de componentes de diseño personalizados para formularios adaptables](/help/forms/using/custom-layout-components-forms.md).
* También puede personalizar componentes de formulario adaptables específicos, como campos y presentación del panel.

   * Utilice la funcionalidad [Overlay](/help/sites-developing/overlays.md) de AEM para modificar una copia de un componente. No se recomienda modificar los componentes predeterminados.
   * Para personalizar la presentación de los componentes de formulario adaptables listos para usar en /libs, [cree componentes de diseño personalizados](/help/forms/using/custom-layout-components-forms.md) además de los [diseños predeterminados](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * Introduzca interactividades personalizadas mediante la creación de utilidades o apariencias personalizadas. No se recomienda modificar los componentes predeterminados. Para obtener más información, consulte [Entorno de apariencia](/help/forms/using/introduction-widgets.md).

* Consulte [Administración de información de identificación personal](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) para obtener recomendaciones sobre el manejo de datos de PII.

## Crear formularios adaptables {#author-adaptive-forms}

### Uso de la IU táctil para la creación {#using-touch-optimized-ui-for-authoring}

* Utilice el navegador de objetos de la barra lateral para acceder rápidamente a los campos de la jerarquía del formulario. Puede utilizar el cuadro de búsqueda para buscar objetos en el formulario o en el árbol de objetos y desplazarse de un objeto a otro.
* Para vista y edición de las propiedades de un componente en el navegador de componentes de la barra lateral, seleccione el componente y haga clic en ![cmppr-1](assets/cmppr-1.png). También puede hacer clic con el botón doble en un componente para vista de sus propiedades en el navegador de propiedades.
* Utilice los métodos abreviados de teclado para realizar acciones rápidas en los formularios. Consulte [Métodos abreviados de teclado de AEM Forms](/help/forms/using/keyboard-shortcuts.md).

* Se recomienda utilizar componentes de formulario adaptables solo en páginas de formulario adaptables. Los componentes dependen de su jerarquía principal. Por lo tanto, no los use en una página AEM.

Consulte también las descripciones de los componentes y las prácticas recomendadas en [Introducción a la creación de formularios adaptables](/help/forms/using/introduction-forms-authoring.md).

### Uso de reglas en formularios adaptables {#using-rules-in-adaptive-forms}

AEM Forms proporciona un [editor de reglas](/help/forms/using/rule-editor.md) que permite crear reglas para agregar comportamiento dinámico a los componentes de formularios adaptables. Mediante estas reglas, puede evaluar condiciones y acciones de déclencheur en componentes, como mostrar u ocultar campos, calcular valores, cambiar dinámicamente la lista desplegable, etc.

El editor de reglas proporciona un editor visual y un editor de código para escribir reglas. Tenga en cuenta lo siguiente al escribir reglas con el modo de editor de código:

* Utilice nombres significativos y únicos para los campos y componentes de formulario para evitar posibles conflictos al escribir reglas.
* Utilice el operador `this` para que un componente haga referencia a sí mismo en una expresión de regla. Garantiza que la regla siga siendo válida incluso si cambia el nombre del componente. Por ejemplo, `field1.valueCommit script: this.value > 10`.

* Utilice los nombres de componentes al hacer referencia a otros componentes del formulario. Utilice la propiedad `value` para recuperar el valor de un campo o componente. Por ejemplo, `field1.value`.

* Consulte los componentes por jerarquía única relativa para evitar conflictos. Por ejemplo, `parentName.fieldName`.

* Al gestionar reglas complejas o comúnmente utilizadas, considere la posibilidad de escribir la lógica empresarial como funciones en una biblioteca de cliente independiente que puede especificar y reutilizar en formularios adaptables. La biblioteca de cliente debe ser una biblioteca independiente y no debe tener dependencias externas, excepto en jQuery y Underscore.js. También puede utilizar la biblioteca del cliente para exigir [revalidación del lado del servidor](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) de los datos de formulario enviados.
* Los formularios adaptables proporcionan un conjunto de API que puede utilizar para comunicarse con los formularios adaptables y realizar acciones en ellos. Algunas de las API clave son las siguientes. Para obtener más información, consulte [Referencia de la API de la biblioteca JavaScript para Forms adaptable](https://adobe.com/go/learn_aemforms_documentation_63).

   * `guideBridge.reset()`:: Restablece un formulario.
   * `guideBridge.submit()`:: Envía un formulario.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`:: Define el enfoque en un campo.
   * `guideBridge.validate(errorList, somExpression, focus)`:: Valida un formulario.
   * `guideBridge.getDataXML(options)`:: Obtiene los datos del formulario como XML.
   * `guideBridge.resolveNode(somExpression)`:: Obtiene un objeto de formulario.
   * `guideBridge.setProperty(somList, propertyName, valueList)`:: Define la propiedad de un objeto de formulario.
   * Además, puede utilizar las siguientes propiedades de campo:

      * `field.value` para cambiar el valor de un campo.
      * f `ield.enabled` para habilitar/deshabilitar un campo.
      * `field.visible` para cambiar la visibilidad de un campo.

* Es posible que los autores de formularios adaptables necesiten escribir código JavaScript para generar lógica empresarial en un formulario. Aunque JavaScript es potente y eficaz, es probable que pueda comprometer las expectativas de seguridad. Por lo tanto, debe asegurarse de que el autor del formulario es una persona de confianza y de que existen procesos para revisar y aprobar el código JavaScript antes de que un formulario se ponga en producción. El administrador puede restringir el acceso al editor de reglas a los grupos de usuarios en función de su función o función. Consulte [Conceder acceso al editor de reglas para seleccionar grupos de usuarios](/help/forms/using/rule-editor-access-user-groups.md).
* Puede utilizar expresiones en las reglas para hacer dinámicos los formularios adaptables. Todas las expresiones son expresiones JavaScript válidas y utilizan API de modelos de secuencias de comandos de formularios adaptables. Estas expresiones devuelven valores de ciertos tipos. Para obtener más información acerca de las expresiones y las prácticas recomendadas a su alrededor, consulte [expresiones de formularios adaptables](/help/forms/using/adaptive-form-expressions.md).

### Uso de temáticas {#working-with-themes}

Adaptable para temáticas le permite crear estilos reutilizables que se pueden aplicar en todos los formularios para obtener un aspecto y un estilo coherentes. Se recomienda utilizar Temáticas para definir el estilo de los componentes y paneles de formularios. Algunas de las prácticas recomendadas en relación con las temáticas son las siguientes:

* Utilice la biblioteca de recursos para aplicar rápidamente estilos de texto, fondo e imágenes. Cuando se agrega un estilo a la biblioteca de recursos, está disponible para otras temáticas y en el modo de estilo del editor de formularios.
* Aplique la configuración global como fuente y fondo de página mediante el selector de nivel de página.
* Utilice las bibliotecas cliente para importar estilos existentes o avanzados en sus temáticas.
* Puede anular el estilo de campos, paneles o botones específicos en una capa de estilo de formulario.
* Si un tema no cumple los requisitos de estilo, puede utilizar clases predefinidas como guideFieldNode, guideFieldLabel, guideFieldWidget y guidePanelNode para aplicar un estilo común a todos los formularios.

Para obtener más información, consulte [Temáticas](/help/forms/using/themes.md).

### Optimización del rendimiento de formularios grandes y complejos {#optimizing-performance-of-large-and-complex-forms}

Los autores de formularios y los usuarios finales suelen tener problemas de rendimiento al cargar formularios grandes en modo de creación o en tiempo de ejecución. A medida que aumenta el número de objetos (campos y paneles) en el formulario, la creación y la experiencia en tiempo de ejecución resultan inicios degradantes. También evita que varios autores colaboren y creen un formulario simultáneamente.

Considere las siguientes optimizaciones para superar problemas de rendimiento con formularios grandes:

* Se recomienda crear formularios adaptables con el modelo de datos de formulario XSD incluso cuando se convierte un XFA a un formulario adaptable, si es posible.
* Incluya solo los campos y paneles en formularios adaptables que capturan información del usuario. Considere mantener el contenido estático en un nivel mínimo o utilice direcciones URL para abrirlo en una ventana separada.
* Aunque cada formulario está diseñado para un propósito específico, hay algunos segmentos comunes en la mayoría de los formularios. Por ejemplo: detalles personales, dirección, detalles de empleo, etc. Cree [fragmentos de formulario adaptables](/help/forms/using/adaptive-form-fragments.md) para elementos y secciones de formulario comunes y utilícelos en todos los formularios. También puede guardar un panel en un formulario existente como un fragmento. Cualquier cambio en un fragmento se refleja en todos los formularios adaptables asociados. Promueve la creación en colaboración, ya que varios autores pueden trabajar simultáneamente en distintos fragmentos que conforman un formulario.

   * De forma similar a los formularios adaptables, se recomienda que todos los estilos y secuencias de comandos personalizados específicos de fragmentos se definan en la biblioteca del cliente mediante el cuadro de diálogo contenedor de fragmentos. Además, intente crear fragmentos autosuficientes que no dependan de objetos que se encuentren fuera de él.
   * Evite el uso de secuencias de comandos entre fragmentos. Si hay algún objeto fuera del fragmento al que debe hacer referencia, intente que dicho objeto forme parte del formulario principal. Si el objeto debe seguir residiendo en otro fragmento, consulte por su nombre en la secuencia de comandos.

* Utilice Guardar y reanudar con el guardado automático para guardar el formulario adaptable periódicamente y permitir que los usuarios puedan volver a intentarlo más tarde para completar el formulario.
* Configure los fragmentos para que se carguen de forma diferida. En tiempo de ejecución, el fragmento marcado para cargarse de forma diferida solo se procesa cuando es necesario. Reduce significativamente el tiempo de carga de los formularios grandes. También se admite en fragmentos con paneles repetitivos. Para obtener más información, consulte [Configuración de la carga diferida](/help/forms/using/lazy-loading-adaptive-forms.md).

   * No configure la carga diferida en fragmentos en un diseño de cuadrícula adaptable o en el primer panel.
   * El archivo adjunto y los componentes Términos y condiciones no se admiten en fragmentos cargados de forma diferida.
   * Marque un valor en un panel flotante cargado como Usar valor globalmente si ese valor se utiliza en alguna otra parte del formulario de modo que el valor esté disponible para su uso cuando se descargue el panel que lo contiene.
   * Considere la posibilidad de escribir reglas de visibilidad para fragmentos que deberían mostrarse u ocultarse en función de una condición.

### Cumplimentación previa de formularios adaptables {#prefilling-adaptive-forms}

Puede rellenar previamente los campos de formulario adaptables con datos recuperados del servidor para ayudar a los usuarios a rellenar rápidamente el formulario y evitar errores al escribir.

* AEM Forms proporciona un servicio de rellenado previo para leer datos de un archivo XML de datos predefinido y rellenar los campos de un formulario adaptable con el contenido del archivo XML de relleno previo.
* El XML de datos de relleno previo debe ser compatible con el esquema del modelo de formulario asociado al formulario adaptable.
* Incluya las secciones `afBoundedData` y `afUnBoundedData` en el XML de relleno previo para rellenar previamente los campos enlazados y no enlazados en un formulario adaptable.

* Para los formularios adaptables basados en el modelo de datos de formulario, AEM Forms proporciona el servicio de cumplimentación previa del modelo de datos de formulario incorporado. El servicio de cumplimentación previa consulta orígenes de datos para objetos del modelo de datos en el formulario adaptable y prefiere valores de campo al procesar el formulario.
* También puede utilizar los protocolos file, crx, service o http para rellenar formularios adaptables.
* AEM Forms admite servicios de cumplimentación previa personalizados que se pueden conectar como un servicio OSGi para rellenar formularios adaptables.

Para obtener más información, consulte [Rellenar campos de formulario adaptables](/help/forms/using/prepopulate-adaptive-form-fields.md).

### Firma y envío de formularios adaptables {#signing-and-submitting-adaptive-forms}

Los formularios adaptables requieren acciones de envío para procesar los datos especificados por el usuario. Una acción Enviar determina la tarea que se realiza en los datos que se envían mediante un formulario adaptable.

* Existen varias acciones de envío listas para usar en formularios adaptables. Para obtener más información, consulte [Configuración de la acción Enviar](/help/forms/using/configuring-submit-actions.md).
* Puede escribir una acción de envío personalizada si las acciones de envío predeterminadas no cumplen con su caso de uso. Para obtener más información, consulte [Escritura de una acción Enviar personalizada para formularios adaptables](/help/forms/using/custom-submit-action-form.md).
* Incluya validaciones del lado del servidor para evitar el envío de datos no válidos.

Puede aprovechar la experiencia con varios signos de Adobe Sign en formularios adaptables. Tenga en cuenta lo siguiente al configurar Adobe Sign en formularios adaptables. Para obtener más información, consulte [Uso de Adobe Sign en un formulario adaptable](/help/forms/using/working-with-adobe-sign.md).

* El formulario adaptable habilitado para Adobe Sign solo se envía después de que todos los firmantes hayan firmado el formulario. Forms aparece en el estado Firma pendiente hasta que todos los firmantes firman el formulario.
* Puede configurar la experiencia de firma en el formulario o redirigir a los firmantes a una página de firma en el momento del envío.
* Configure la experiencia de firma secuencial o paralela, según corresponda.

### Generando documento del registro {#generating-document-of-record}

Un documento de registro (DoR) es una versión PDF acoplada de un formulario adaptable que se puede imprimir, firmar o archivar.

* Según el modelo de datos de formulario en el que se base un formulario adaptable, puede configurar una plantilla para el documento de trabajo de la siguiente manera:

   * **Plantilla** de formulario XFA: Utilice el archivo XDP asociado como plantilla de DoR.
   * **Esquema** XSD: Utilice la plantilla XFA asociada que utilice el mismo esquema XML que utiliza el formulario adaptable.
   * **Ninguno**: Usar DoR generado automáticamente.

* Configure el encabezado, pie de página, imágenes, color, fuente, etc. a la derecha desde la ficha Documento de registro del editor de formularios adaptables.
* Utilice `DoRService` para generar el DoR mediante programación.
* Excluir campos ocultos del documento de trabajo.
* Utilice el parámetro de solicitud `afAcceptLang` para la vista de DoR en otra configuración regional.

### Depuración y prueba de formularios adaptables {#debugging-and-testing-adaptive-forms}

[AEM Chrome Plug-](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) inis es una extensión de navegador para Google Chrome que proporciona herramientas para depurar formularios adaptables. Los creadores y desarrolladores de formularios pueden utilizar estas herramientas para:

* Identifique los cuellos de botella y optimice el rendimiento del procesamiento de formularios
* Depurar palabras clave y errores bindRef en el formulario
* Habilitar y configurar registros
* Depurar reglas y secuencias de comandos en el formulario
* Explore y conozca las API de guideBridge

Para obtener más información, consulte [AEM Complemento Chrome - Formulario adaptable](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

Calvin SDK es una API de utilidad para desarrolladores de Forms adaptable para probar Forms adaptable. El SDK de Calvin está construido sobre el [marco de pruebas de Hobbes.js](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/test-api/index.html). Puede utilizar la estructura para probar lo siguiente:

* Experiencia de representación de un formulario adaptable
* Experiencia de cumplimentación previa de un formulario adaptable
* Enviar experiencia de un formulario adaptable
* Reglas de expresión
* Validaciones
* Carga diferida

Para obtener más información, consulte [Automatización de pruebas de formularios adaptables](/help/forms/using/calvin.md).

### Validación de formularios adaptables en AEM servidor {#validating-adaptive-forms-on-aem-server}

Las validaciones del lado del servidor son necesarias para evitar cualquier intento de omitir las validaciones en el cliente y cualquier posible compromiso de envíos de datos y violaciones de reglas comerciales. Las validaciones del lado del servidor se ejecutan en el servidor cargando la biblioteca de cliente requerida.

* Incluya funciones en una biblioteca de cliente para validar expresiones en formularios adaptables y especifique la biblioteca de cliente en el cuadro de diálogo contenedor de formularios adaptables. Para obtener más información, consulte [Revalidación del lado del servidor](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* La validación del lado del servidor valida el modelo de formulario. Se recomienda crear una biblioteca de cliente independiente para las validaciones y no mezclarla con otros elementos como el estilo HTML y la manipulación DOM en la misma biblioteca de cliente.

### Localización de formularios adaptables {#localizing-adaptive-forms}

AEM proporciona flujos de trabajo de traducción que puede utilizar para localizar formularios adaptables. Para obtener más información, consulte [Uso de AEM flujo de trabajo de traducción para localizar formularios adaptables](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

Algunas prácticas recomendadas para localizar formularios adaptables son las siguientes:

* Utilice fragmentos de formulario adaptables para elementos comunes en distintos formularios y localice fragmentos. Garantiza que se localice un fragmento una vez y que se refleje en todos los formularios en los que se utilice el fragmento localizado.
* Las modificaciones como la adición de un componente nuevo o la aplicación de una secuencia de comandos en un formulario localizado no se localizan automáticamente. Por lo tanto, debe finalizar un formulario antes de localizarlo para evitar varios ciclos de localización.
* Utilice el parámetro de solicitud `afAcceptLang` para anular la configuración regional del explorador y procesar el formulario en la configuración regional especificada. Por ejemplo, la siguiente URL obligará a procesar el formulario en la configuración regional japonesa, independientemente de la configuración regional especificada en la configuración del explorador:

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* Actualmente, AEM Forms admite la localización de contenido de formularios adaptables en inglés (en), español (es), francés (fr), italiano (it), alemán (de), japonés (ja), portugués-brasileño (pt-BR), chino (zh-CN), chino-Taiwán (zh-TW) y coreano (ko-KR). Sin embargo, puede añadir compatibilidad con nuevas configuraciones regionales para formularios adaptables en tiempo de ejecución. Para obtener más información, consulte [Compatibilidad con nuevas configuraciones regionales para la localización de formularios adaptables](/help/forms/using/supporting-new-language-localization.md).

## Preparar proyecto de formularios para producción {#prepare-forms-project-for-production}

### Añadiendo servidor de procesamiento de formularios {#adding-forms-processing-server}

Puede configurar una instancia adicional del servidor de AEM Forms que resida detrás del servidor de seguridad en una zona segura. Puede utilizar esta instancia para:

* **Procesamiento** por lotes: trabajos que se repiten o programan en lotes con una carga pesada. Por ejemplo, imprima sentencias, genere correspondencias y utilice servicios de documento como PDF Generator, Output y Ensamblador.
* **Almacenamiento de datos** PII: Guarde los datos PII en el servidor de procesamiento. No es necesario si ya está utilizando un proveedor de almacenamiento personalizado para almacenar datos PII.

### Mover proyecto a otro entorno {#moving-project-to-another-environment}

A menudo necesita mover sus proyectos AEM de un entorno a otro. Algunas de las cosas clave que hay que recordar al mover son las siguientes:

* Realice copias de seguridad de sus bibliotecas de cliente, código personalizado y configuraciones existentes.
* Implemente paquetes de productos y parches manualmente y en el orden especificado en el nuevo entorno.
* Implemente paquetes de código específicos del proyecto y paquetes manualmente y como paquete o paquete independiente en el nuevo servidor de AEM.
* (*AEM Forms en JEE solamente*) Implemente LCA y DSC manualmente en el servidor Forms Workflow.
* Utilice la funcionalidad [Export-Import](/help/forms/using/import-export-forms-templates.md) para mover los recursos al nuevo entorno. También puede configurar el agente de replicación y publicar los recursos.
* Al actualizar, reemplace todas las API y funciones obsoletas por nuevas API y funciones.

### Configuración de AEM {#configuring-aem}

Algunas prácticas recomendadas para configurar AEM para mejorar el rendimiento general son las siguientes:

* Habilite la compresión de biblioteca de cliente HTML para JavaScript y CSS desde la consola Felix. Consulte [Clientlibs explicados por ejemplo](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/).
* Almacene en caché todas las bibliotecas de cliente en `/etc.clientlibs/fd` y todas las bibliotecas de cliente personalizadas adicionales en AEM despachante para aumentar la capacidad de respuesta y la seguridad de los formularios publicados. Para obtener más información, consulte [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* No almacene en caché las rutas `/content/forms/af/` y `/content/dam/formsanddocuments/*`. para obtener información detallada sobre la configuración de la caché de formularios adaptables, consulte [Almacenamiento en caché de formularios adaptables](/help/forms/using/configure-adaptive-forms-cache.md).

* Habilite HTML mediante el módulo de compresión de servidor web. Para obtener más información, consulte [Ajuste del rendimiento del servidor de AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Aumentar la configuración de llamadas por solicitud para formularios grandes. Consulte [Optimización del rendimiento de formularios grandes y complejos](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* Cree [páginas de error personalizadas mostradas por el controlador de errores](https://helpx.adobe.com/experience-manager/6-2/sites-developing/customizing-errorhandler-pages.html).
* Servidor AEM Forms seguro.

   * Utilice el modo de ejecución `nosamplecontent` para asegurarse de que no hay contenido de muestra y usuarios de muestra implementados en el servidor de producción. Consulte [Ejecución de AEM en modo listo para la producción](/help/sites-administering/production-ready.md).

* Mantenga el tamaño del montón a un mínimo de 8 GB. Para obtener más información sobre la configuración, consulte [Ajuste del rendimiento del servidor de AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Utilice sesiones de usuario de servicio en lugar de sesiones de administración para ejecutar tareas de nivel de servicio. Para obtener más información, consulte [Autenticación de servicio](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### Configuración del almacenamiento externo para borradores y datos de formularios enviados {#external-storage}

En un entorno de producción, se recomienda no almacenar los datos del formulario enviados en AEM repositorio. La implementación predeterminada de las acciones de envío de Forms Portal Store, Store Content y Store PDF almacena datos de formulario en AEM repositorio. Estas acciones de envío están destinadas únicamente a fines de demostración. Además, las funciones Guardar y reanudar y Guardar automáticamente utilizan el almacenamiento del portal de forma predeterminada. Por lo tanto, considere las siguientes recomendaciones:

* **Almacenamiento de datos** de borrador: Si está utilizando la función Borrador de formularios adaptables, debe implementar una interfaz de proveedor de servicios (SPI) personalizada para almacenar los datos borrador en almacenamientos más seguros como la base de datos. Para obtener más información, consulte [Ejemplo para integrar los borradores y el componente de envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md).

* **Almacenamiento de datos** de envío: Si utiliza el almacén de envío de Form Portal, debe implementar un SPI personalizado para almacenar los datos de envío en una base de datos. Consulte [Ejemplo para integrar los borradores y el componente de envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md) para obtener una integración de muestra.

   También puede escribir una acción de envío personalizada que almacene datos de formulario y datos adjuntos en un almacenamiento seguro. Consulte [Escritura de la acción Enviar personalizada para formularios adaptables](/help/forms/using/custom-submit-action-form.md) para obtener más información.

* **Duración del ID** de borrador: Al guardar un formulario adaptable como borrador, se genera un ID de borrador para identificar de forma exclusiva el borrador. El valor mínimo de la longitud del campo de ID de borrador es de 26 caracteres. Adobe recomienda definir la longitud del ID de borrador en 26 caracteres o más.

### Manejo de información personal identificable {#handling-personally-identifiable-information}

Uno de los desafíos clave para las organizaciones es cómo manejar datos de identificación personal (PII). Algunas prácticas recomendadas que le ayudarán a administrar estos datos son las siguientes:

* Utilice un almacenamiento externo seguro como una base de datos para almacenar datos de formularios de borrador y enviados. Consulte [Configuración del almacenamiento externo para borradores y datos de formularios enviados](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* Utilice el componente de formulario Términos y condiciones para obtener el consentimiento explícito del usuario antes de activar el guardado automático. En este caso, habilite el guardado automático solo cuando el usuario acepte las condiciones del componente Términos y condiciones.

