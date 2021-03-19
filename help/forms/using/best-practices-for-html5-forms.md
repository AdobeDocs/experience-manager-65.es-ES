---
title: Prácticas recomendadas para formularios HTML5
seo-title: Prácticas recomendadas para formularios HTML5
description: Ajuste su Forms HTML5 basado en XFA para obtener el mejor rendimiento.
seo-description: Aprenda a ajustar su Forms HTML5 basado en XFA para obtener el mejor rendimiento.
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 1%

---


# Prácticas recomendadas para formularios HTML5{#best-practices-for-html-forms}

## Información general {#overview}

AEM Forms tiene un componente llamado formularios HTML5. Ayuda a procesar PDF forms existentes basados en XFA (archivos XDP) en formato HTML5. Este documento proporciona directrices y recomendaciones para reducir el tiempo de carga y mejorar el rendimiento de los formularios HTML5 en dispositivos móviles.

La mayoría de los dispositivos móviles tienen una potencia de procesamiento y capacidades de memoria limitadas. Ayuda a mejorar el tiempo de espera de los dispositivos móviles. Los exploradores web que se ejecutan en un dispositivo móvil tienen acceso a recursos limitados (memoria limitada y capacidades de procesamiento). Una vez alcanzado el límite, el comportamiento del explorador se vuelve lento. Este documento proporciona recomendaciones para mantener el tamaño de un formulario HTML5 bajo control. Un formulario más pequeño no infringe los límites de memoria y potencia de procesamiento de un dispositivo y proporciona una experiencia suave.

Sin embargo, las recomendaciones que se tratan en este artículo están dirigidas a formularios HTML5, pero son igualmente aplicables a los PDF forms basados en XFA. Estas prácticas recomendadas contribuyen de forma colectiva al rendimiento general de los formularios HTML5. Requiere una planificación cuidadosa para desarrollar formas eficientes y productivas. Empecemos:

## Los nodos son la moneda de los formularios HTML5, ingréselos sabiamente {#nodes-are-currency-of-html-forms-spend-them-wisely}

Por lo general, un formulario XFA tiene varios elementos. Por ejemplo, tabla, campo de texto e imágenes. Cada elemento tiene una serie de propiedades para controlar el comportamiento y el aspecto del elemento. Cuando se procesa un formulario XFA en formato HTML5, todos los elementos XFA y las propiedades correspondientes se convierten en nodos DOM de modelo o HTML. Estos nodos aumentan el tamaño y la complejidad de un DOM. Lentos en la representación del formulario HTML5.

Es más fácil para los exploradores renderizar un DOM más ligero. Por lo tanto, puede realizar las siguientes optimizaciones en un formulario XFA para reducir el número de nodos. Por lo tanto, genere una estructura DOM delgada:

* Utilice la propiedad caption para añadir una etiqueta a un campo. No utilice un elemento Texto independiente para añadir una etiqueta. Ayuda a reducir el peso adicional, lo que lleva a mejoras en el rendimiento. También ayuda a evitar problemas de diseño.
* Mantenga el número mínimo de elementos de texto Dibujar en un formulario. Los elementos de dibujo son útiles para mejorar la legibilidad y la apariencia, pero no tienen ninguna capacidad de almacenamiento de información. Se recomienda combinar varios elementos de texto de Dibujar en un solo elemento de texto de Dibujar. No deje piedra sin girar para hacer un formulario más ligero.

## Los formularios Lite funcionan mejor, mantenga los recursos comprimidos {#lite-forms-perform-better-keep-the-resources-compressed}

Un formulario HTML5 puede contener varios recursos externos, como archivos de imagen, JavaScript y CSS. Cada vez que un explorador solicita un formulario, los recursos externos se envían a través de la red. El tiempo necesario para viajar por la red es directamente proporcional al tamaño de los archivos.

Por lo tanto, reducir el tamaño de los recursos externos y utilizar sólo los recursos absolutamente necesarios es el método preferido para mejorar el rendimiento de los formularios. Puede realizar las siguientes optimizaciones en un formulario XFA para reducir el tamaño de los recursos externos de un formulario:

* Utilice [imágenes comprimidas](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md). Reduce la actividad de red y la cantidad de memoria necesaria para procesar un formulario. Por lo tanto, el tiempo de carga del formulario disminuye sustancialmente.
* Utilice la opción minificar de AEM Configuration Manager (Day CQ HTML Library Manager) para comprimir archivos JavaScript y CSS. Para obtener más información, consulte [Configuración de OSGi](/help/sites-deploying/osgi-configuration-settings.md).
* Habilite la compresión web. Reduce el tamaño de las solicitudes y respuestas originadas desde un formulario. Para obtener más información, consulte [Ajuste de rendimiento de AEM servidor de formularios](https://helpx.adobe.com/es/aem-forms/6-3/performance-tuning-aem-forms.html).

## Mantenga el interés vivo, muestre solo los campos obligatorios {#keep-the-interest-alive-show-only-required-fields}

Un formulario HTML5 se puede ejecutar en cientos de páginas. Un formulario con un gran número de campos es lento de cargar en el explorador. Puede realizar las siguientes optimizaciones en un formulario XFA para optimizar los formularios con un gran número de campos y páginas:

* Evalúe la división de los formularios grandes en varios formularios. También puede utilizar un conjunto de formularios para agrupar todos los formularios más pequeños y presentarlos como una sola unidad. Un conjunto de formularios sólo carga los formularios necesarios. Además, en un conjunto de formularios, se pueden configurar campos comunes en distintos formularios para compartir enlaces de datos. Los enlaces de datos ayudan a los usuarios a rellenar la información común solo una vez; la información se rellena automáticamente en formularios posteriores, lo que supone mejoras sustanciales del rendimiento. Para obtener más información sobre los conjuntos de formularios, consulte [Conjunto de formularios en AEM](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).
* Considere la posibilidad de dividir secciones y mover cada sección a una página diferente. Los formularios HTML5 se cargan dinámicamente en cada página en la solicitud de desplazamiento de la página. Solo la página desplazada (la página que se muestra y las páginas que la preceden) se almacenan en la memoria; el resto de las páginas se cargan bajo demanda. Por lo tanto, dividir y mover una sección en una página por su cuenta reduce el tiempo necesario para cargar un formulario. También puede utilizar la primera página del formulario como página de aterrizaje. Es similar a la tabla de contenido (TOC) de un libro. Una página de aterrizaje del formulario solo contiene vínculos a las demás secciones del formulario. Mejora significativamente el tiempo de carga de la primera página del formulario y mejora la experiencia del usuario.
* Mantenga las secciones condicionales ocultas de forma predeterminada. Consiga que estas secciones solo estén visibles cuando se cumpla una determinada condición. Ayuda a reducir al mínimo el tamaño de DOM. También puede utilizar la navegación con pestañas para mostrar solo una sección a la vez.

## Menos es más, reducir el número de páginas {#less-is-more-reduce-the-number-of-pages}

Los formularios HTML5 pueden contener campos impulsados por datos (tablas y subformularios). Estos campos amplían el tamaño del formulario en tiempo de ejecución. Por ejemplo, una tabla controlada por datos de un formulario HTML5 puede abarcar miles de filas. Estas tablas pueden causar una degradación del diseño y del rendimiento. Las optimizaciones sugeridas a continuación pueden ayudarle a reducir el tiempo de carga de los formularios HTML5 con campos impulsados por datos:

* Utilice secuencias de comandos XFA para lograr la navegación por páginas para mostrar campos impulsados por datos (tablas y subformularios). En la navegación por páginas, solo se muestran datos específicos en una página. Limita la operación de pintura del explorador a los campos que se muestran a la vez y facilita el desplazamiento por un formulario. Además, los usuarios de los dispositivos móviles solo están interesados en un subconjunto de datos. Le ayuda a ofrecer una buena experiencia de usuario y a reducir el tiempo necesario para cargar los datos necesarios. Se obtienen dos soluciones por el precio de una.  Tenga en cuenta también que la navegación por páginas no está disponible de forma predeterminada. Puede utilizar secuencias de comandos XFA para desarrollar la navegación por páginas.

* Evalúe la combinación de varias columnas de solo lectura en una sola columna. Reduce la memoria necesaria para mostrar el formulario. Además, evite mostrar las columnas que no requieran ninguna entrada de los usuarios.
* Evalúe dividir el formulario basado en datos en un [conjunto de formularios](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html), si las sugerencias anteriores no arrojan muchas mejoras. Por ejemplo, si una tabla tiene más de 1000 filas, mueva cada 100 filas a un formulario diferente. Ayudaría a mejorar el tiempo de carga y el rendimiento de los formularios.  Tenga en cuenta también que un conjunto de formularios genera un XML de envío consolidado para todos los formularios. Para diferenciar los datos de cada formulario, utilice diferentes orígenes de datos. Para obtener más información, consulte [Conjunto de formularios en AEM Forms](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).

## Potencia de dos para el documento de registro (DOR) {#power-of-two-for-document-of-record-dor}

Un formulario XFA puede tener un gran número de secciones dedicadas únicamente a Documento de registro (DOR). Para reducir el número de nodos y mejorar el rendimiento de un formulario de este tipo, puede mantener diferentes copias del formulario: una copia para rellenar el formulario y otra para generar el documento de registro en el servidor. En la copia para rellenar el formulario XFA, se muestran los campos requeridos solo para capturar datos. En el formulario Generar documento de registro XFA, mantenga los campos requeridos solamente en la salida impresa del formulario. Antes de elegir el enfoque sugerido, evalúe la ganancia de rendimiento y la sobrecarga de mantenimiento.

## Lecturas recomendadas {#recommended-reads}

Los formularios de Adobe Experience Manager (AEM) pueden ayudarle a transformar transacciones complejas en experiencias digitales simples y atractivas. Sin embargo, requiere un esfuerzo concertado para desarrollar formas eficientes y productivas. Además de HTML5 Forms, estas son algunas lecturas recomendadas para prácticas recomendadas generales AEM:

* [Prácticas recomendadas para implementar y mantener AEM](/help/sites-deploying/best-practices.md)
* [Prácticas recomendadas para la creación de contenido](/help/sites-authoring/best-practices.md)
* [Prácticas recomendadas para la administración de AEM](/help/sites-administering/administer-best-practices.md)
* [Prácticas recomendadas para el desarrollo de soluciones](/help/sites-developing/best-practices.md)
* [Prácticas recomendadas para usar formularios adaptables](/help/forms/using/adaptive-forms-best-practices.md) 
* [El servidor de AEM Forms no incrusta fuentes en un formulario PDF dinámico](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## Tarjeta de referencia rápida {#quick-reference-card}

Puede imprimir la siguiente tarjeta (haga clic en tarjeta para descargar una versión de alta resolución) y mantenerla en su escritorio para una referencia rápida:
[ ![Tarjeta de referencia rápida de las prácticas recomendadas de Forms HTML5](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
