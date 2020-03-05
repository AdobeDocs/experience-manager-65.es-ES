---
title: Novedades de Adobe Experience Manager 6.5 Service Pack 4
description: Novedades de Adobe Experience Manager 6.5 Service Pack 4
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 1d867ee46ca9cd5945c7413d42fc002b90332c3c

---


# Novedades de Adobe Experience Manager 6.5 Service Pack 4 {#aem-whats-new-service-pack-4}

En 2020, para Adobe Experience Manager (AEM) 6.5, las nuevas funciones y mejoras se entregan en Service Packs trimestrales. Los clientes se benefician de este nuevo enfoque a medida que adoptan las innovaciones con mayor rapidez.

El último Service Pack 4 de AEM (6.5.4.0) está disponible el 5 **de marzo de 2020**. En este artículo se destacan las funciones que ofrece el Service Pack más reciente para enriquecer el viaje de AEM.

## AEM Sites {#aem-sites}

### Mejoras en el rendimiento en diversas esferas {#performance-improvements}

* Reduzca el tiempo para cargar e inicializar ContextHub dentro de un sitio (contexthub.kernel.js). Genera una carga más rápida de la primera página durante una visita al sitio.

* En el Editor de páginas, reduzca el tiempo que se actualiza la página después de arrastrar y soltar fragmentos de experiencia en el lienzo de la página.

* En Live Copy Overview, reduzca el tiempo de carga de las entradas cuando el sitio tenga muchas Live Copies (+200).

* En el Editor de plantillas, mejore el manejo de las direcciones URL incompletas o no válidas que podrían activar el Editor de plantillas para que se ralentice.

Además, a partir de AEM 6.5 SP4, el sistema de estilos se ha mejorado, los estilos también se pueden seleccionar dentro de un cuadro de diálogo de componentes.

## AEM Assets {#aem-assets}

### Integración con Brand Portal a través de la consola de Adobe I/O {#assets-integration-bp}

Recursos AEM ahora se configura con Brand Portal a través de Adobe I/O, que obtiene un testigo IMS para la autorización del inquilino de Brand Portal. Anteriormente, se configuraba en la IU clásica mediante OAuth Gateway heredado.

Las nuevas integraciones con OAuth heredado no serán compatibles a partir del 6 de abril de 2020 y cambiarán a la consola de Adobe I/O. Si no modifica la integración, las configuraciones existentes seguirán funcionando.

Puede crear una nueva integración o actualizar la configuración de integración a la consola de Adobe I/O.

### Accessibility enhancements {#accessibility-enhancements}

* Las casillas de verificación de estado mixto ahora tienen un atributo de marcado con aria con un valor &quot;mixto&quot;, para exponer su estado mixto a los lectores de pantalla.

* Ahora se admiten controles basados en el teclado, aparte de gestos basados en rutas, para desplazarse por imágenes con zoom.

* Se han proporcionado restricciones de formato de fecha en etiquetas de campo para que los usuarios que utilizan sólo el teclado introduzcan manualmente la fecha.

* El atributo Alt se ha agregado a los iconos decorativos y se ha eliminado el atributo role=img, de modo que dichos iconos e imágenes no se exponen a los usuarios del lector de pantalla.

* Se ha agregado el atributo Alt a los iconos de cierre para indicar a los usuarios del lector de pantalla que deben pasar el tabulador por encima.

## Formularios AEM {#aem-forms}

### Generar resultados imprimibles en flujos de trabajo de AEM Forms {#generate-printable-output}

Si desea que una solución imprima varias copias de un archivo de plantilla de origen y lo integre con un archivo de datos con numerosos registros, hay un nuevo paso de flujo de trabajo Generar salida imprimible disponible en AEM Forms. Por ejemplo, si desea imprimir un formulario de origen con un nombre diferente cada vez que se imprima, puede tener esos nombres en el archivo de datos e integrarlo con un archivo de plantilla estándar.

Aproveche esta función con **Herramientas** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]** > **[!UICONTROL Crear]** y, a continuación, busque el paso de flujo de trabajo **[!UICONTROL Generar salida]** imprimible.

![Generar salida imprimible](assets/generate-print-output-demo.gif)

Para obtener más información sobre esta función, consulte Flujo de trabajo centrado en [formularios en OSGi - Referencia](../forms/using/aem-forms-workflow-step-reference.md)de pasos.

### Compatibilidad con varias columnas para formularios adaptables y comunicaciones interactivas en el modo Diseño {#multi-column-adaptive-forms}

Ahora puede definir el número de columnas para un panel en formularios adaptables y comunicaciones interactivas.

Puede encontrar la nueva opción si cambia al modo Diseño, toca el panel que desea convertir a un formato de varias columnas, selecciona su elemento principal y toca el icono de varias columnas, como se muestra en la siguiente figura, para definir el número de columnas para el panel.

![Diseño de varias columnas](assets/multi-column-layout.gif)

Para obtener más información, consulte [Uso del modo Diseño para cambiar el tamaño de los componentes](../forms/using/resize-using-layout-mode.md).

### Personalizaciones de la bandeja de entrada de AEM {#aem-inbox}

¿Alguna vez siente la necesidad de personalizar las opciones disponibles en el encabezado de AEM? Ahora es posible con nuestra nueva versión de Service Pack con la introducción de una opción de control **[!UICONTROL de]** administración.

**Personalizar el texto del encabezado**

Los usuarios que pertenecen al grupo de administradores **del** flujo de trabajo ahora pueden personalizar el texto del encabezado disponible en la parte superior con el texto que prefiera para reemplazar el texto existente de **[!UICONTROL Adobe Experience Manager]** .

Puede encontrar la nueva opción **[!UICONTROL Personalizar texto]** de encabezado en el selector de vista (disponible en la parte superior derecha de la barra de herramientas) > Control **** de administración.

**Personalización del logotipo**

Al igual que al personalizar el texto del encabezado, los usuarios que pertenecen al grupo de administradores **de** flujo de trabajo ahora pueden personalizar el logotipo disponible en la parte superior con el logotipo que prefiera.

Puede encontrar la nueva opción **[!UICONTROL Personalizar logotipo]** en el selector de vista > Control **[!UICONTROL de administración]**.

Para obtener más información sobre esta función, consulte [Su bandeja de entrada](../sites-authoring/inbox.md).

### Control de navegación del usuario {#user-navigation-control}

Los usuarios que pertenecen al grupo de administradores **de** flujo de trabajo tienen la opción de hacer que los usuarios trabajen en AEM en un modo restringido según su función. Los administradores pueden controlar la visualización de las opciones de navegación disponibles en el encabezado y restringir el acceso de los usuarios al modo de creación de flujo de trabajo o navegar a la Ayuda u otros vínculos de soluciones.

Consulte las nuevas **[!UICONTROL opciones]** de navegación Ocultar en Selector de vista > Control **[!UICONTROL de administración]**.

Para obtener más información sobre esta función, consulte [Su bandeja de entrada](../sites-authoring/inbox.md).

### Compatibilidad con texto enriquecido en formularios HTML5 {#rich-text-support}

El campo de texto ahora puede mostrar una lista de opciones de formato en el formulario HTML5 procesado. Debe definir un formato de campo para el campo de texto en Forms Designer para aplicar la configuración adecuada al campo.

Para utilizar esta función, toque el campo de texto en la vista **** Diseño de Forms Designer. En la ficha **[!UICONTROL Campo]** , seleccione Texto **** enriquecido en la lista desplegable Formato **[!UICONTROL de]** campo para aplicar la configuración. El campo de texto ahora muestra las opciones de formato cuando se procesa en un formulario HTML5.

Para obtener más información, consulte [Diseño de plantillas de formulario para formularios](../forms/using/designing-form-template.md)HTML5.

## Puntos destacados

Además de las nuevas funciones, AEM 6.5 Service Pack 4 incluye los siguientes aspectos destacados:

* Ahora solo se pueden sincronizar subárboles de contenido selectivo con Scene7 en lugar de todo `content/dam`.

* La integración del modelo de datos de formulario mediante el servicio web SOAP ahora admite grupos de opciones o atributos en los elementos.

* La entrada o salida de SOAP y las estructuras de datos complejas ahora admiten la sustitución dinámica de grupos.

## Funciones principales de los Service Packs anteriores de AEM 6.5

### Imágenes inteligentes para Dynamic Media {#smart-imaging}

Las imágenes inteligentes aprovechan las características de visualización únicas de cada usuario para ofrecer automáticamente las imágenes correctas optimizadas para su experiencia, lo que mejora el rendimiento y la participación. Las imágenes inteligentes funcionan con los ajustes preestablecidos de imagen existentes y utilizan la inteligencia en el último milisegundo de la publicación para reducir aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red o del navegador. Consulte Imágenes [inteligentes](../assets/imaging-faq.md).

### Búsqueda visual de Recursos AEM {#visual-search}

Los usuarios de recursos pueden buscar imágenes visualmente similares. AEM muestra las imágenes con etiquetas inteligentes del repositorio de DAM similares a una imagen seleccionada por el usuario. See [Visual search](../assets/search-assets.md).

### Compartir y solicitar acceso a los elementos de la Bandeja de entrada de un usuario {#share-request-access}

Puede compartir los elementos de la Bandeja de entrada con otro usuario. Una vez que otro usuario tiene acceso a los elementos de la Bandeja de entrada, el usuario puede reclamar y realizar las acciones correspondientes en los elementos compartidos. Del mismo modo, puede solicitar acceso a los elementos de la Bandeja de entrada a otros usuarios. Consulte [Uso compartido y solicitud de acceso a elementos de la Bandeja de entrada de un usuario](../forms/using/configure-shared-queues-osgi.md).

### Configuración de la configuración fuera de la oficina para los elementos de la Bandeja de entrada {#configure-out-of-office}

Si planea salir de la oficina, puede especificar lo que sucede con los artículos que se le han asignado para ese período.
Tiene la opción de especificar una fecha y hora de inicio y una fecha y hora de finalización para que la configuración fuera de la oficina esté en vigor. Puede establecer una persona predeterminada a la que se enviarán todos los elementos. Consulte [Configuración fuera de la oficina](../forms/using/configure-out-of-office-settings.md).

### Generar varias comunicaciones interactivas mediante la API por lotes {#generate-multiple-ic}

Puede utilizar la API por lotes para generar varias comunicaciones interactivas a partir de una plantilla. La plantilla es una comunicación interactiva sin datos. La API de lote combina datos con una plantilla para generar una comunicación interactiva. La API es útil en la producción masiva de comunicaciones interactivas. Por ejemplo: facturas telefónicas, extractos de tarjetas de crédito para varios clientes. Consulte [Generación de varias comunicaciones interactivas mediante la API](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)por lotes.

### Mensajes de error de validación estándar para formularios adaptables {#standard-validation}

Los formularios adaptables ahora se pueden integrar con servicios personalizados para realizar validaciones de datos. Si los valores de entrada no cumplen los criterios de validación y el mensaje de error de validación que devuelve el servidor está en el formato de mensaje estándar, los mensajes de error se muestran en el campo del formulario. Si los valores de entrada no cumplen los criterios de validación y el mensaje de error de validación del servidor no está en el formato de mensaje estándar, los formularios adaptables proporcionan un mecanismo para transformar los mensajes de error de validación en un formato estándar de modo que se muestren en el campo del formulario. Consulte Mensajes de error de validación [estándar para formularios](../forms/using/standard-validation-error-messages-adaptive-forms.md)adaptables.

## Versiones clave desde AEM 6.5 SP3

Entre el 12 de diciembre de 2019 y el 5 de marzo de 2020, Adobe lanzó las siguientes funciones que están fuera del paquete principal de AEM:

* Mejoras mensuales de AEM Cloud Manager 2020.1.0 y 2020.2.0Las dos últimas versiones se centraron en mejorar el estado de la canalización y la capacidad de descargar registros para los distintos pasos. Lea las notas completas de la versión aquí:
   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)

   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* Actualizaciones de CLI de AEM Cloud ManagerAutomatice las tareas de Cloud Manager mediante la herramienta de línea de comandos. Estamos ampliando continuamente la CLI: únete a [GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases).

* Sitios AEM: Project Archetype 23La mejor manera de iniciar un nuevo proyecto de AEM. Con Archetype 23 estamos [fusionando el Arquetipo de Proyecto para SPA y sitios regulares en uno](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23), proporcionando además un tema predeterminado para poner en marcha su desarrollo front-end.

* Sitios AEM: Sitio de referencia de WKND Todos los [nuevos proyectos](https://www.wknd.site/) de referencia, acompañados de las prácticas recomendadas para crear sitios con AEM. Obtenga más información leyendo el tutorial [](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html) WKND completamente actualizado y obtenga el código de [GitHub](https://github.com/adobe/aem-guides-wknd/releases).

* Sitios AEM: Commerce CIF Core Components 0.7.0 y 0.9.0Integración de AEM Sites y Magento Commerce. Estamos [extendiendo continuamente componentes principales dedicados y un arquetipo de proyecto con énfasis en comercio](https://github.com/adobe/aem-core-cif-components/releases).

* Recursos AEM: Desktop App 2.0.1.1
   [Obtener acceso de escritorio a los recursos](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)

* AEM Screens: Feature Pack 202001Digital Signage directamente desde AEM. Tome las últimas mejoras con el último Feature Pack; esta vez estamos [habilitando la reproducción sincrónica en varios reproductores](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)multimedia.

## Recursos útiles

* [Guías de usuario de AEM 6.5](../user-guide/capabilities.md)

* [Notas de versión específicas de Adobe Experience Manager 6.5](release-notes.md)

* [Notas de la versión de Service Pack para Adobe Experience Manager 6.5](sp-release-notes.md)
