---
title: Prácticas recomendadas para formularios HTML5
seo-title: Prácticas recomendadas para formularios HTML5
description: Ajuste los formularios HTML5 basados en XFA para obtener el mejor rendimiento.
seo-description: Aprenda a ajustar los formularios HTML5 basados en XFA para obtener el mejor rendimiento.
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
translation-type: tm+mt
source-git-commit: 3e83611f6b30cee774b72194bee1d03e323a6a57

---


# Best practices for HTML5 forms{#best-practices-for-html-forms}

## Información general {#overview}

AEM Forms tiene un componente llamado formularios HTML5. Ayuda a procesar formularios PDF existentes basados en XFA (archivos XDP) en formato HTML5. Este documento proporciona directrices y recomendaciones para reducir el tiempo de carga y mejorar el rendimiento de los formularios HTML5 en dispositivos móviles.

La mayoría de los dispositivos móviles tienen una capacidad de procesamiento y memoria limitadas. Ayuda a mejorar el tiempo de espera de los dispositivos móviles. Los navegadores web que se ejecutan en un dispositivo móvil tienen acceso a recursos limitados (memoria limitada y capacidades de procesamiento). Una vez alcanzado el límite, el comportamiento del explorador se torna lento. Este documento proporciona recomendaciones para mantener el tamaño de un formulario HTML5 en control. Un formulario más pequeño no infringe los límites de memoria y potencia de procesamiento de un dispositivo y proporciona una experiencia suave.

Sin embargo, las recomendaciones analizadas en este artículo están dirigidas a formularios HTML5, pero son igualmente aplicables a formularios PDF basados en XFA. Estas prácticas recomendadas contribuyen de forma colectiva al rendimiento general de los formularios HTML5. Requiere una planificación cuidadosa para desarrollar formas eficientes y productivas. Comencemos:

## Los nodos son la moneda de los formularios HTML5 y se invierten con prudencia {#nodes-are-currency-of-html-forms-spend-them-wisely}

Generalmente, un formulario XFA tiene varios elementos. Por ejemplo, tabla, campo de texto e imágenes. Cada elemento tiene una serie de propiedades para controlar el comportamiento y la apariencia del elemento. Cuando un formulario XFA se procesa en formato HTML5, todos los elementos XFA y las propiedades correspondientes se convierten en nodos DOM de modelo o HTML. Estos nodos aumentan el tamaño y la complejidad de un DOM. ralentizar el procesamiento del formulario HTML5.

Es más fácil para los navegadores procesar un DOM más delgado. Por lo tanto, puede realizar las siguientes optimizaciones en un formulario XFA para reducir el número de nodos. Por lo tanto, genere una estructura DOM delgada:

* Utilice la propiedad caption para agregar una etiqueta a un campo. No utilice un elemento Texto independiente para agregar una etiqueta. Ayuda a eliminar el peso adicional, lo que lleva a un aumento del rendimiento. También ayuda a evitar problemas de diseño.
* Mantenga el número mínimo de elementos de texto Dibujar en un formulario. Los elementos de dibujo son útiles para mejorar la legibilidad y la apariencia, pero no tienen ninguna capacidad de almacenamiento de información. Se recomienda combinar varios elementos de texto Dibujar en un solo elemento de texto Dibujar. No deje ninguna piedra sin girar para hacer un formulario más delgado.

## Los formularios Lite funcionan mejor, los recursos se mantienen comprimidos {#lite-forms-perform-better-keep-the-resources-compressed}

Un formulario HTML5 puede contener varios recursos externos, como archivos de imagen, JavaScript y CSS. Cada vez que un explorador solicita un formulario, los recursos externos se envían a través de la red. El tiempo necesario para viajar por la red es directamente proporcional al tamaño de los archivos.

Por lo tanto, reducir el tamaño de los recursos externos y utilizar únicamente los recursos absolutamente necesarios es el método preferido para mejorar el rendimiento de los formularios. Puede realizar las siguientes optimizaciones en un formulario XFA para reducir el tamaño de los recursos externos de un formulario:

* Utilice imágenes [](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md)comprimidas. Reduce la actividad de red y la cantidad de memoria necesaria para procesar un formulario. Por lo tanto, el tiempo de carga del formulario disminuye sustancialmente.
* Utilice la opción Minify en AEM Configuration Manager (Day CQ HTML Library Manager) para comprimir archivos JavaScript y CSS. Para obtener más información, consulte Configuración de [OSGi](/help/sites-deploying/osgi-configuration-settings.md).
* Habilite la compresión web. Reduce el tamaño de las solicitudes y respuestas originadas en un formulario. Para obtener más información, consulte Ajuste [del rendimiento del servidor](https://helpx.adobe.com/aem-forms/6-3/performance-tuning-aem-forms.html)de formularios AEM.

## Mantener vivo el interés, mostrar solo los campos obligatorios {#keep-the-interest-alive-show-only-required-fields}

Un formulario HTML5 se puede ejecutar en cientos de páginas. Un formulario con un gran número de campos es lento de cargar en el explorador. Puede realizar las siguientes optimizaciones en un formulario XFA para optimizar los formularios con un gran número de campos y páginas:

* Evalúe la división de los formularios grandes en varios formularios. También puede utilizar un conjunto de formularios para agrupar todos los formularios más pequeños y presentarlos como una sola unidad. Un conjunto de formularios solo carga los formularios necesarios. Además, en un conjunto de formularios, puede configurar campos comunes en diferentes formularios para compartir enlaces de datos. Los enlaces de datos ayudan a los usuarios a rellenar la información común una sola vez; la información se rellena automáticamente en formularios posteriores, lo que produce mejoras sustanciales en el rendimiento. Para obtener más información sobre los conjuntos de formularios, consulte Conjunto [de formularios en formularios](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)AEM.
* Considere dividir secciones y mover cada sección a una página diferente. Los formularios HTML5 cargan cada página de forma dinámica en la solicitud de desplazamiento de la página. Solo se almacenan en la memoria las páginas con desplazamiento (la página que se muestra y las páginas que las preceden); el resto de las páginas se cargan a petición. De este modo, dividir y mover una sección en una página por sí misma reduce el tiempo necesario para cargar un formulario. También puede utilizar la primera página del formulario como página de aterrizaje. Es similar a la tabla de contenido (TOC) de un libro. Una página de aterrizaje del formulario sólo contiene vínculos a las demás secciones del formulario. Mejora significativamente el tiempo de carga de la primera página del formulario y mejora la experiencia del usuario.
* De forma predeterminada, las secciones condicionales se mantienen ocultas. Convierta estas secciones en visibles únicamente cuando se cumpla una determinada condición. Ayuda a reducir al mínimo el tamaño del DOM. También puede utilizar la navegación con fichas para mostrar solo una sección a la vez.

## Menos es más, reducir el número de páginas {#less-is-more-reduce-the-number-of-pages}

Los formularios HTML5 pueden contener campos basados en datos (tablas y subformularios). Estos campos expanden el tamaño del formulario en tiempo de ejecución. Por ejemplo, una tabla basada en datos en un formulario HTML5 puede abarcar miles de filas. Estas tablas pueden causar una degradación del diseño y del rendimiento. Las optimizaciones sugeridas a continuación pueden ayudarle a reducir el tiempo de carga de los formularios HTML5 con campos basados en datos:

* Utilice secuencias de comandos XFA para lograr la navegación por páginas y mostrar campos basados en datos (tablas y subformularios). En la navegación por páginas, solo se muestran datos específicos en una página. Limita la operación de pintura del navegador a los campos que se muestran a la vez y facilita la navegación por un formulario. Además, los usuarios de dispositivos móviles solo están interesados en un subconjunto de datos. Le ayuda a ofrecer una excelente experiencia al usuario y reduce el tiempo necesario para cargar los datos necesarios. Se obtienen dos soluciones por el precio de una.  Además, tenga en cuenta que la navegación por páginas no está disponible de forma predeterminada. Puede utilizar secuencias de comandos XFA para desarrollar la navegación por páginas.

* Evalúe la combinación de varias columnas de solo lectura en una sola columna. Reduce la memoria necesaria para mostrar el formulario. Además, evite mostrar las columnas que no requieran ninguna entrada de los usuarios.
* Evaluar la división del formulario basado en datos en un conjunto [de](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)formularios, si las sugerencias anteriores no producen muchas mejoras. Por ejemplo, si una tabla tiene más de 1000 filas, mueva cada 100 filas a un formulario diferente. Ayudaría a mejorar el tiempo de carga y el rendimiento de los formularios.  Además, tenga en cuenta que un conjunto de formularios produce un archivo XML de envío consolidado para todos los formularios. Para diferenciar los datos de cada formulario, utilice orígenes de datos diferentes. Para obtener más información, consulte Conjunto [de formularios en AEM Forms](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).

## Potencia de dos para el documento de registro (DOR) {#power-of-two-for-document-of-record-dor}

Un formulario XFA puede tener un gran número de secciones dedicadas únicamente al documento de registro (DOR). Para reducir el número de nodos y mejorar el rendimiento de un formulario de este tipo, puede mantener diferentes copias del formulario: una copia para rellenar el formulario y otra para generar el documento de registro en el servidor. En la copia para rellenar el formulario XFA, se muestran los campos requeridos solamente para capturar datos. En el formulario Generar documento de registro XFA desde, mantenga los campos requeridos solamente en la salida impresa del formulario. Antes de elegir el enfoque sugerido, evalúe la ganancia de rendimiento y la sobrecarga de mantenimiento.

## Lecturas recomendadas {#recommended-reads}

Los formularios de Adobe Experience Manager (AEM) pueden ayudarle a transformar transacciones complejas en experiencias digitales sencillas y atractivas. Sin embargo, requiere un esfuerzo concertado para desarrollar formas eficientes y productivas. Además de los formularios HTML5, se recomiendan algunas lecturas para las prácticas recomendadas generales de AEM:

* [Prácticas recomendadas para implementar y mantener AEM](/help/sites-deploying/best-practices.md)
* [Prácticas recomendadas para la creación de contenido](/help/sites-authoring/best-practices.md)
* [Prácticas recomendadas para la administración de AEM](/help/sites-administering/administer-best-practices.md)
* [Prácticas recomendadas para desarrollar soluciones](/help/sites-developing/best-practices.md)
* [Prácticas recomendadas para usar formularios adaptables](/help/forms/using/adaptive-forms-best-practices.md) 

## Tarjeta de referencia rápida {#quick-reference-card}

Puede imprimir la siguiente tarjeta (haga clic en tarjeta para descargar una versión de alta resolución) y mantenerla en su escritorio para obtener una referencia rápida:
Tarjeta de referencia rápida de prácticas recomendadas de formularios[ ![HTML5](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
