---
title: Notas de la versión para  [!DNL Adobe Experience Manager]  6.5
description: Encuentre información de la versión, novedades, instrucciones de instalación y una lista de cambios detallada para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 1a73ae15f03a427f33a748ad2c6c789541206579
workflow-type: tm+mt
source-wordcount: '8188'
ht-degree: 20%

---

# Notas de la versión del Service Pack de [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE!      DO NOT DELETE THIS HIDDEN NOTE!
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## Resumen de versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.25.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del Service Pack |
| Fecha | 21 de mayo de 2026 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

Experience Manager 6.5.25.0 incluye nuevas características, mejoras clave solicitadas por el cliente y correcciones de errores. También incluye mejoras de rendimiento, estabilidad y seguridad basadas en la versión 6.5 disponible desde abril de 2019.

Esta versión del Service Pack ofrece 275 puertos posteriores entre Sites, Assets y Foundation, incluidas correcciones de errores críticas y protección de la seguridad. La versión también mejora la accesibilidad en la creación de sitios con una amplia navegación mediante el teclado, administración del enfoque, semántica de ARIA, mejoras en el contraste de color y tamaño de destinatario táctil que se alinean con los estándares WCAG.

Crosswalk está disponible de forma predeterminada en esta versión, lo que elimina la necesidad de tener un paquete o configuración independiente después de la instalación.

Los puertos secundarios de seguridad corrigen las vulnerabilidades XSS y mejoran la administración de metadatos de recursos compartidos.

Los fragmentos de contenido y la API de GraphQL también reciben mejoras de fiabilidad, que abarcan referencias de imagen incrustadas, administración de consultas persistentes y localización del editor.


<!-- UPDATE FOR EACH NEW RELEASE -->

### Funciones y mejoras clave de Forms

* [Conversiones de PDF Generator con subprocesos múltiples](/help/forms/using/install-configure-document-services.md#windows-only-enable-multi-threaded-pdf-generator-conversions): se agregó compatibilidad para ejecutar conversiones simultáneas de Microsoft Word (doc/docx) y Excel (xls/xlsx) cuando AEM Forms se ejecuta como un servicio de Windows con una sola cuenta de usuario configurada.

* [Marcadores jerárquicos para PDF basados en XFA](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf): El servicio Output y AEM Forms Designer ahora generan jerarquías de marcadores estructuradas en PDF estáticos interactivos y planos basados en XFA. Los marcadores siguen a los niveles de encabezado (H1-H6) establecidos en las propiedades de accesibilidad de los cuadros de texto, por lo que las entradas H2-H6 se anidan bajo el elemento principal correcto en lugar de aparecer en paralelo.

* [Detalles de nivel de formulario en registros de transacciones JEE](/help/forms/using/transaction-report-overview-jee.md#form-level-details-transaction-log-jee): AEM Forms en JEE ahora registra detalles de nivel de formulario en `transaction_log.log` para cada transacción, además de la información de servicio y operación existente. Los administradores pueden correlacionar los datos de informes de transacciones con formularios específicos al analizar envíos, representaciones y conversiones. (FORMS-21574)

* [Se ha actualizado la matriz de plataformas compatibles](/help/forms/using/aem-forms-jee-supported-platforms.md): AEM Forms en el paquete de servicio JEE 6.5.25.0 agrega compatibilidad con las siguientes tecnologías más recientes:
   * Plataforma de aplicaciones empresariales JBoss® (EAP) 7.4.23
   * Cliente de IBM® Content Manager 8.7
   * AEM Forms Designer en Microsoft® Windows Terminal Server 2025

  >[!NOTE]
  >
  > Para actualizar JBoss EAP de 7.4.10 a 7.4.23, consulte:
  > * [Actualice JBoss EAP de 7.4.10 a 7.4.23 para AEM Forms en JEE](/help/forms/using/upgrade-jboss-eap-from-7-4-10-to-7-4-23.md) para entornos independientes.
  > * [Actualizar el clúster EAP JBoss de 7.4.10 a 7.4.23 para AEM Forms en JEE](/help/forms/using/upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23.md) para entornos de clúster.

## Se han corregido problemas en el Service Pack 25 {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6525}

#### Accesibilidad {#sites-accessibility-6525}

* Los controles de arrastrar y soltar filas de tabla de la vista de lista Sitios ahora funcionan con la navegación mediante el teclado. Los usuarios del lector de pantalla y del teclado pueden reordenar las filas y recibir comentarios durante la acción. (SITES-24946)

* La barra de herramientas Editar diseño ahora presenta etiquetas de pantalla y tableta más pequeñas en una secuencia de lector de pantalla significativa. Los usuarios escuchan las etiquetas con las mediciones de reglas relacionadas en lugar de escucharlas desordenadas. (SITES-25291)
* El modal de ventana emergente Muestras ahora administra el enfoque correctamente cuando se abre desde el modal de anotación. El enfoque comienza en el encabezado modal en lugar de moverse directamente al botón de muestra seleccionado. (SITES-25275)
* El modo Teaser ahora proporciona una forma accesible de mover el cuadro de diálogo con un teclado. Los usuarios ya no necesitan un ratón para cambiar la posición del modal en la página. (SITES-25226)
* La Vista de tarjeta mejora la accesibilidad al eliminar el comportamiento innecesario de la cuadrícula ARIA. Los usuarios del lector de pantalla reciben información de tarjeta más clara sin controles de navegación de cuadrícula que no coinciden con el diseño visual. (SITES-24933)
* La información del objeto en el modal Eliminar ahora se muestra de forma coherente después de acciones repetidas al pasar el ratón por encima. Los usuarios pueden mover el puntero y volver al icono para volver a leer la información del objeto. (SITES-24778)
* El carril izquierdo ahora recibe el enfoque en el orden esperado después de que los usuarios lo abran desde la página de inicio de Sites. Los usuarios del teclado y del lector de pantalla pueden pasar del botón de configuración al contenido del carril sin omitir el área expandida. (SITES-24754)
* La administración de enfoque ahora funciona de forma coherente en el cuadro de diálogo modal Carrusel. Los usuarios del teclado y del lector de pantalla pueden comenzar en el encabezado modal y volver al control original después de cerrar el cuadro de diálogo. (SITES-24716)
* El cuadro de diálogo Selección de vínculos ahora devuelve el foco al control que lo abrió después de que los usuarios lo cierren. Los usuarios de teclado y lector de pantalla ya no pierden su lugar después de cerrar el cuadro de diálogo. (SITES-24707)
* El modo Imagen ya no mueve el foco a la primera pestaña o al punto de referencia de la página principal cuando los autores abren o cierran el cuadro de diálogo. El enfoque se desplaza primero al encabezado del cuadro de diálogo y, a continuación, vuelve al control que lo abrió. (SITES-24693)
* El carril Referencias ahora gestiona el enfoque correctamente cuando se abre un cuadro de diálogo modal. Los usuarios del teclado y del lector de pantalla permanecen dentro del cuadro de diálogo hasta que lo cierran y, a continuación, continúan la navegación sin perder contexto. (SITES-24683)
* El modal de selección de ruta de hipervínculo ya no mueve el enfoque al campo o control incorrecto cuando los autores lo abren o lo cierran. El enfoque comienza en el encabezado modal y vuelve al botón que abrió el modal. (SITES-24672)
* El modal Teaser ya no mueve el enfoque a la primera pestaña o parte superior de la página cuando los autores la abren o cierran. El enfoque ahora sigue el flujo de cuadro de diálogo esperado y reduce los anuncios innecesarios del lector de pantalla. (SITES-24522)

* El botón de bloqueo del Editor de páginas ahora proporciona comentarios más precisos del lector de pantalla. Los lectores de pantalla utilizan el atributo title cuando está disponible, lo que reduce los anuncios detallados para los autores que utilizan tecnología de asistencia. (SITES-41431)
* La navegación con teclado ahora omite el contenido oculto. Los usuarios pueden moverse por los elementos de interfaz visibles sin que el foco cambie al contenido que no pueden ver. (SITES-41430)
* Ahora, el foco del teclado vuelve al elemento de activación después de que los usuarios cierren una superposición. El editor de páginas ya no envía el enfoque de nuevo a la superposición, lo que mejora la navegación de los usuarios del teclado. (SITES-40819)
* La barra de herramientas del Editor de páginas ahora muestra etiquetas, como información sobre herramientas, cuando los usuarios navegan por los elementos de la barra de herramientas con un teclado. Los usuarios pueden comprender cada acción de la barra de herramientas a medida que el enfoque se mueve de un elemento a otro. (SITES-40751)
* Al pasar el ratón por encima de los elementos del explorador del componente, ya no se elimina el enfoque de un componente de texto activo. Los autores pueden editar el texto sin interrupciones y el foco del teclado sigue siendo predecible. (SITES-35370)
* Los lectores de pantalla ahora anuncian con mayor claridad el botón de dirección de ordenación del modo de búsqueda. La etiqueta del botón ya no repite la misma dirección y describe mejor el comportamiento de alternancia. (SITES-25534)
* El modal de búsqueda ahora muestra un indicador visual para la opción seleccionada en el cuadro de lista Cambiar archivo o carpeta. Los usuarios pueden identificar la opción de ruta de exploración actual sin depender solo del enfoque. (SITES-25532)
* El modal de búsqueda ahora aumenta el contraste para la etiqueta Ordenar por. El texto cumple los requisitos de accesibilidad y mejora la legibilidad para los usuarios con poca visión. (SITES-25531)
* Los botones de selección de dispositivos ahora muestran la información de estado actual correcta en la barra de herramientas Editar diseño. Los usuarios del lector de pantalla pueden identificar el dispositivo activo sin escuchar el estado de alternancia engañoso. (SITES-25524)
* La navegación con teclado y lector de pantalla ahora cierra el menú Bandeja de entrada cuando el enfoque lo abandona. Los usuarios evitan el confuso estado en el que el menú permanece abierto mientras el enfoque se mueve a otra parte. (SITES-25518)
* La navegación con teclado y lector de pantalla ahora cierra el menú Ayuda cuando el enfoque lo abandona. El enfoque ya no se mueve al contenido fuera del menú mientras el menú permanece abierto. (SITES-25517)
* La página de inicio Fragmentos de contenido ahora proporciona una etiqueta accesible coherente para las pestañas de la barra lateral. NVDA anuncia correctamente la etiqueta de la pestaña cuando los usuarios navegan por los controles de la pestaña. (SITES-25509)
* Las opciones específicas del menú Información de página ahora cumplen con los requisitos mínimos de contraste. El contraste mejorado ayuda a los usuarios con problemas de visión a identificar el elemento de menú activo. (SITES-25321)
* La navegación con teclado ahora omite los controles ocultos en la barra de herramientas demográfica contraída. El enfoque permanece en los elementos interactivos visibles, lo que mejora el orden de navegación en la vista previa del diseño. (SITES-25304)
* El botón Rotar dispositivo ahora proporciona comentarios más claros del lector de pantalla en la barra de herramientas Editar diseño. Los lectores de pantalla anuncian la orientación actual y la acción que la cambia. (SITES-25292)
* La barra de herramientas Editar diseño ahora muestra un estado seleccionado de borrado para el botón Escritorio. La opción Escritorio coincide con los demás botones del dispositivo y facilita la identificación de la vista activa. (SITES-25290)
* La barra de herramientas Editar diseño ahora identifica la región de regla para las tecnologías de asistencia. Los usuarios del lector de pantalla ya no encuentran valores de medición sin etiqueta durante la edición del diseño. (SITES-25287)
* La barra de herramientas Editar diseño ahora muestra la etiqueta de botón iPhone 8 Plus completa en el estado sin marcar. La etiqueta ya no se trunca cuando hay suficiente espacio alrededor del botón. (SITES-25284)
* El problema del que se informó describía un indicador de enfoque en la barra de herramientas Editar diseño que aparecía para cubrir varios controles de dispositivo. La preocupación se centraba en los usuarios del teclado que podían perder la noción del control activo cuando el contorno de enfoque incluía botones adyacentes. El problema funcionaba según lo previsto. (SITES-25283)
* El problema del que se informó describía los botones modales de anotación que anunciaban la anotación antes de cada etiqueta de botón. La preocupación se centró en la salida poco clara del lector de pantalla para acciones como Anotar, Muestras y Eliminar. (SITES-25277)
* El texto del botón de anotación ahora utiliza suficiente contraste en el modo de anotación. Esta actualización mejora la legibilidad para los usuarios con visión reducida y admite requisitos de contraste WCAG. (SITES-25267)
* Los lectores de pantalla ahora reciben actualizaciones de estado cuando los usuarios filtran la lista Insertar nuevo componente. El modal anuncia los cambios de resultados para que los usuarios entiendan que la lista cambió mientras escribían. (SITES-25251)
* El problema registrado describía la semántica de encabezado faltante para el título del modal de anotación. La preocupación se centró en la navegación del lector de pantalla y la capacidad de comprender la estructura modal. (SITES-25248)
* Los niveles de encabezado en el carril lateral del Editor de páginas ahora siguen una jerarquía de contenido más clara. La sección Carril izquierdo ya no aparece como el encabezado de la página principal de las tecnologías de asistencia. (SITES-25222)
* El botón Editar del carril izquierdo de Assets ahora tiene un objetivo de contacto más grande. Los usuarios con necesidades de movilidad pueden activar el botón más fácilmente y evitar los controles cercanos. (SITES-25221)
* El carril izquierdo de Assets ahora identifica cuándo se abre el botón Editar una nueva pestaña del explorador. Los usuarios pueden anticipar el cambio de navegación en lugar de perder contexto inesperadamente. (SITES-25220)
* Los títulos de los componentes ahora se muestran correctamente cuando los usuarios aplican un espaciado de texto aumentado. El carril lateral conserva las etiquetas legibles y admite los requisitos de espaciado de texto WCAG. (SITES-25219)
* El campo de filtro en Componentes de raíl lateral ahora expone un nombre accesible correcto. Esta actualización ayuda a los usuarios del lector de pantalla a identificar el campo sin depender del texto del marcador de posición. (SITES-25212)
* El problema del que se informó describía una secuencia de enfoque ilógica en el modo de anotación. Según se informa, los usuarios del teclado no pudieron acceder a la barra de herramientas de anotaciones a menos que usaran Mayús+Tab después de activar el modo. (SITES-24996)
* El lienzo del editor muestra su título de barra superior como un encabezado. Los lectores de pantalla pueden anunciar el título con la estructura correcta, lo que mejora la navegación y la comprensión de la página. (SITES-24993)
* El informe de accesibilidad observó un contraste insuficiente para el mensaje de estado de carga que aparece cuando los usuarios cambian de vista. La preocupación se centró en la legibilidad para los usuarios con poca visión o daltonismo. (SITES-24991)
* El informe de accesibilidad observó que los vínculos de tarjeta incluían texto no descriptivo. La preocupación se centró en ayudar a los usuarios de lectores de pantalla a comprender cada destino de vínculo sin contexto adicional. (SITES-24975)
* La vista de lista Sitios ahora muestra texto de Live Copy con un contraste más fuerte. La actualización mejora la legibilidad para autores con poca visión y para usuarios que trabajan en condiciones de pantalla brillante. (SITES-24956)
* La navegación mediante el teclado ahora desplaza el foco al menú Emulador después de que los usuarios lo amplíen. Este comportamiento ayuda a los usuarios del lector de pantalla y del teclado a acceder a las opciones de menú en el orden esperado. (SITES-24954)
* La vista de lista Sitios ahora mejora la visibilidad de los botones de arrastrar y soltar en las filas de la tabla. Los autores pueden identificar el control más fácilmente cuando reordenan el contenido. (SITES-24951)
* Una tarjeta ya no expone el vínculo de imagen y el vínculo de encabezado como vínculos independientes cuando comparten el mismo destino. La actualización reduce la descripción del lector de pantalla y mejora la eficacia de la navegación. (SITES-24947)
* Los botones del menú Encabezado ahora utilizan atributos de accesibilidad más precisos. Los lectores de pantalla anuncian los botones como controles ampliables en lugar de controles de apertura de cuadros de diálogo. (SITES-24742)
* La bandeja de entrada ahora marca los vínculos relacionados con el marcado de la lista semántica. Los usuarios del lector de pantalla pueden comprender mejor el número y la agrupación de los vínculos de la Bandeja de entrada. (SITES-24730)
* Las etiquetas de botón de encabezado ahora evitan nombres accesibles detallados. Los usuarios del lector de pantalla reciben anuncios más claros sin información de funciones duplicadas del texto del icono. (SITES-24715)
* El botón Informe de CSV ahora proporciona comentarios más claros sobre el comportamiento de las nuevas pestañas. Los usuarios pueden comprender que, al seleccionar el botón, se abre una nueva pestaña del explorador antes de activarlo. (SITES-24704)
* Los cuadros de diálogo modales ahora utilizan marcas de accesibilidad más precisas para los controles de encabezado. Los botones Ayuda y Alternar a pantalla completa siguen siendo controles interactivos y ya no aparecen como encabezados para los lectores de pantalla. (SITES-24696)
* El punto de referencia del carril del filtro ahora utiliza una etiqueta distinta que identifica su propósito. Los usuarios del lector de pantalla pueden navegar con mayor seguridad por páginas con varios hitos similares. (SITES-24686)
* Referencias Los mensajes de carril ahora proporcionan una mejor legibilidad para los usuarios que dependen de un contraste de texto suficiente. El problema del que se informó se refería a mensajes de selección y selección múltiple que parecían demasiado claros en su contexto. (SITES-24666)
* El modal de búsqueda ahora proporciona destinos táctiles más grandes para los botones Eliminar ubicación y Cerrar. Este cambio ayuda a los usuarios con temblores de manos, espasmos o visión reducida a activar el control deseado. (SITES-24530)
* Se ha notificado que el vínculo del encabezado Adobe Experience Manager utiliza un atributo ARIA incorrecto. Las pruebas confirmaron que el vínculo controla el contenido ampliable, por lo que el estado accesible existente sigue siendo apropiado. (SITES-24528)
* El indicador de enfoque del botón Firma ya no aparece cortado en la lista Componentes. El contorno visible ayuda a los usuarios del teclado a realizar un seguimiento de su posición en el editor. (SITES-24503)
* Un problema del que se informó describía una alternativa de texto que faltaba para el icono de información sobre herramientas en el panel Componentes. El problema no se reprodujo, pero la revisión confirmó que los iconos informativos deben exponer un nombre accesible claro. (SITES-24500)
* El editor de páginas ya no expone varios puntos de referencia de región con la misma etiqueta. Cada punto de referencia tiene ahora un nombre accesible único, por lo que los usuarios del lector de pantalla pueden identificar la región actual. (SITES-24497)
* El control Change file or folder ahora separa la etiqueta del control de su información de estado. Los usuarios del lector de pantalla escuchan un nombre más corto y claro cuando navegan por el control de encabezado. (SITES-24496)
* Los controles interactivos de la tabla de administración de fragmentos de contenido ahora admiten la navegación estándar mediante el teclado. Los usuarios del teclado pueden desplazarse hasta los botones y vínculos en lugar de descubrirlos únicamente mediante la navegación con teclas de flecha. (SITES-24285)
* La IU de administración de sitios ahora trata correctamente los iconos decorativos del globo para los lectores de pantalla. Los iconos utilizan texto alternativo vacío para que los usuarios solo escuchen contenido significativo de la interfaz. (SITES-3057)

#### Interfaz de usuario de administración{#sites-adminui-6525}

La consola Sites ahora muestra correctamente la configuración de la columna **Vista de lista** guardada. Las columnas seleccionadas permanecen marcadas cuando los autores vuelven a abrir el cuadro de diálogo de configuración y el recuento de columnas activo permanece preciso. (SITES-38576)

#### IU clásica{#sites-classicui-6525}

Los cuadros de diálogo del componente Texto de la IU clásica ahora muestran el contenido del Editor de texto enriquecido (RTE) como texto con formato en lugar de HTML sin procesar. Los autores pueden editar el texto existente sin cambiar al modo Source ni eliminar manualmente el marcado. (SITES-38709)

#### Consola de componente{#sites-component-console-6525}

* Ahora los usuarios pueden buscar en la consola Componentes con caracteres localizados o multibyte. La consola también muestra una etiqueta **Remove** traducida en lugar de la cadena en inglés sin traducir. (SITES-39747)
* La página Propiedades del componente ahora localiza las cadenas en Herramientas > Componentes > Propiedades del componente. Los usuarios ya no ven etiquetas en inglés sin traducir en interfaces de creación localizadas. (SITES-39745)

#### [!DNL Content Fragments]{#sites-contentfragments-6525}

La búsqueda de Assets ahora responde correctamente cuando los usuarios seleccionan o cambian filtros. El conjunto de resultados filtrado se actualiza según lo esperado, lo que restaura el refinamiento de la búsqueda confiable en la consola de Assets. (SITES-38686)

#### [!DNL Content Fragments]: administración{#sites-admin-6525}

* La vista de lista de Assets ahora muestra información de objeto Extraído por localizada para fragmentos de contenido bloqueados. Esta corrección mejora la coherencia de la localización cuando los autores revisan las filas del flujo de trabajo. (SITES-42531)

* AEM ahora localiza la etiqueta Principal en el cuadro de diálogo de descarga de fragmentos de contenido. La corrección mantiene la coherencia del flujo de trabajo de descarga en las configuraciones regionales que no están en inglés. (SITES-42534)
* AEM ahora traduce la etiqueta de estado `Later` cuando los autores programan la publicación de fragmentos de contenido desde Assets. Esta corrección mantiene la coherencia de la columna Publicado en todas las interfaces localizadas. (SITES-42532)
* La creación de fragmentos de contenido ahora muestra un mensaje de validación localizado cuando los autores introducen caracteres no válidos en el campo Título. El cuadro de diálogo ya no muestra la cadena sin localizar &quot;Nombre no válido proporcionado&quot;. (SITES-19796)
* La página Editar fragmento de contenido ahora utiliza etiquetas localizadas para etiquetas y colecciones. Los autores ven nombres de campo traducidos en lugar de cadenas en inglés no localizadas. (SITES-977)

#### [!DNL Content Fragments]: editor de fragmentos{#sites-fragments-editor-6525}

* El contenido asociado en el editor de fragmentos de contenido ahora muestra la cadena localizada correcta cuando los autores eliminan contenido de una colección. El cuadro de diálogo ya no reemplaza el nombre del contenido por undefined. (SITES-33675)
* El Editor de fragmentos de contenido ahora muestra una etiqueta General traducida para pestañas sin un marcador de posición configurado. Las interfaces localizadas ya no muestran la cadena en inglés sin traducir en ese área del editor. (SITES-30715)
* El selector Referencia de contenido en el Editor de fragmentos de contenido ahora muestra etiquetas localizadas para los tipos de recursos permitidos. Las interfaces localizadas ya no muestran nombres de tipo en inglés para las categorías de recursos admitidas. (SITES-29699)

#### [!DNL Content Fragments]: API GraphQL {#sites-graphql-api-6525}

* Las respuestas JSON de GraphQL ahora incluyen referencias de imagen incrustadas de los campos de texto enriquecido de fragmentos de contenido cuando los nombres de archivo DAM contienen espacios o caracteres no ASCII. Esta corrección ayuda a las aplicaciones a procesar imágenes referenciadas sin que sea necesario que los autores cambien el nombre de los recursos. (SITES-42191)
* Las respuestas de GraphQL para fragmentos de contenido ahora administran las consultas persistentes de forma más fiable. Las actualizaciones corrigen los encabezados de caché duplicados, mejoran la administración de variables codificadas y devuelven respuestas más claras para el contenido que falta o las consultas fallidas. (SITES-40159)
* Las consultas persistentes de GraphQL ahora se ejecutan sin mensajes INNECESARIOS DE ERROR y ADVERTENCIA en los registros. AEM administra correctamente las variables codificadas, por lo que las consultas correctas ya no crean `PersistedQueryServlet` entradas engañosas. (SITES-39354)

* El cuadro de diálogo Editar extremo de GraphQL ahora localiza sus cadenas de interfaz. Los usuarios ya no ven que el esquema de GraphQL sin traducir se toma del mensaje de configuración en interfaces localizadas. (SITES-34018)

#### [!DNL Content Fragments]: Editor de consultas de GraphQL{#sites-graphql-query-editor-6525}

Los usuarios ahora pueden abrir el Editor de consultas de GraphQL cuando el nombre del explorador de configuración seleccionado contenga caracteres CJK o cirílicos. El editor muestra consultas persistentes para el extremo en lugar de mostrar un error. (SITES-31616)

#### [!DNL Content Fragments]: editor de modelos y modelos{#sites-models-model-editor-6525}

* Los usuarios ahora ven un mensaje de validación localizado en el Editor del modelo de fragmentos de contenido cuando un valor seleccionado necesita un tipo de modelo válido. El editor ya no muestra el mensaje en inglés sin traducir en interfaces localizadas. (SITES-41117)
* El panel de filtro del modelo de fragmento de contenido ahora localiza sus cadenas de estado y título. Los usuarios ya no ven etiquetas sin traducir como Título de modelo, Estado, Borrador, Habilitado y Deshabilitado. (SITES-30863)

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6525} -->

#### ContextHub{#sites-contexthub-6525}

ContextHub ahora se carga sin un error de JavaScript que interrumpe la personalización. Los teasers y otras experiencias personalizadas se pueden representar correctamente en las páginas afectadas. (SITES-38430)

<!-- #### Core Backend{#sites-core-backend-6525} -->

#### Componentes principales{#sites-core-components-6525}

* AEM ya no genera errores ThumbnailServlet repetidos cuando una solicitud se dirige a un recurso DAM que falta. El servlet detiene el procesamiento después de la redirección, lo que evita que las entradas NullPointerException inunden el registro de errores. (SITES-41238)
* AEM ya no marca los campos de cuadro de diálogo opcionales como necesarios cuando los autores vuelven a abrir los cuadros de diálogo de componentes. El cuadro de diálogo mantiene la validación centrada en los campos que realmente requieren entrada, lo que evita errores engañosos en el nivel de tabulación. (SITES-40449)

* AEM incluye varias correcciones de seguridad de puertos de seguridad que refuerzan Sites y los componentes de Cloud Services relacionados. Estas correcciones reducen el riesgo de los scripts entre sitios y mejoran la administración de solicitudes en las rutas de creación afectadas. (SITES-38314)
* El cuadro de diálogo de configuración del componente Image v3 ahora localiza las cadenas en el Editor de páginas. Los autores ya no ven etiquetas sin traducir cuando configuran los componentes de imagen en interfaces localizadas. (SITES-38726)

<!-- #### Campaign integration{#sites-campaign-integration-6525} -->

<!-- #### ContentHub {#sites-contenthub-6525} -->

#### Cruce {#sites-crosswalk-6525}

* Crosswalk ya no requiere paquetes separados y configuración después de la instalación. AEM incluye los paquetes necesarios, paquetes de contenido, usuarios del sistema, asignaciones de usuarios de servicio y alternadores de funciones en el paquete predeterminado. (SITES-41417)
* Los flujos de trabajo de CrossSwalk ahora funcionan con la compatibilidad cq-wcm-core necesaria en AEM 6.5. Los autores pueden utilizar las acciones Crear plantilla y Abrir editor universal sin actualizaciones de paquetes principales independientes. (SITES-37666)

#### Fragmentos de experiencias{#sites-experiencefragments-6525}

AEM ahora carga las plantillas correctas cuando los autores crean variaciones de Fragmento de experiencia y se desplazan más allá de los primeros 40 resultados. El Selector de plantilla mantiene la ruta del fragmento de experiencia seleccionado durante la paginación. (SITES-41531)

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6525} -->

#### Lanzamientos{#sites-launches-6525}

* La cronología de Sites ahora localiza el mensaje que aparece cuando AEM crea una versión antes de promocionar un lanzamiento. Los usuarios ya no ven la cadena en inglés sin traducir en interfaces localizadas. (SITES-39157)
* La lista Lanzamientos ahora muestra la descripción correcta de los lanzamientos creados sin herencia de plantilla o Live Copy. Los usuarios ya no ven la etiqueta de plantilla anulada engañosa. (SITES-34229)

<!-- #### Link Checker{#sites-link-checker-6525} -->

#### Localización{#sites-localization-6525}

* Las propiedades de los componentes de texto en los fragmentos de experiencias ahora utilizan etiquetas localizadas. El menú de formato ya no muestra cadenas no localizadas para las opciones de párrafo, encabezado, comillas o texto con formato previo. (SITES-15091)

* El texto del estado de la plantilla ahora se alinea correctamente en **Herramientas** > **General** > **Plantillas**. Las etiquetas de estado actualizado, habilitado y publicado aparecen en una línea horizontal. (SITES-36797)
* El cuadro de diálogo Mover página ahora muestra la etiqueta completa Seleccionar fecha y hora. La etiqueta ya no se trunca en interfaces localizadas como el francés. (SITES-36795)
* La sección Assets del Editor de plantillas ahora muestra una etiqueta de etiquetas traducida. Las interfaces de creación localizadas presentan etiquetas coherentes durante la configuración de la plantilla. (SITES-33770)
* Las descripciones de las directivas de página ahora se representan correctamente en el Editor de plantillas. Los usuarios pueden leer la guía completa de clases CSS predeterminadas sin texto truncado en la pestaña Estilos. (SITES-29724)
* El Editor de plantillas ahora muestra un error localizado cuando un autor intenta arrastrar un componente a una plantilla eliminada. El mensaje ya no aparece como una cadena &quot;mientras se procesa&quot; sin traducir. (SITES-19313)
* La etiqueta &quot;Target&quot; de la ventana Teaser Configure ahora aparece con texto localizado. La sección Hipervínculo ya no muestra la cadena en inglés en configuraciones regionales que no sean en inglés. (SITES-18622)
* El cuadro de diálogo Iniciar flujo de trabajo del Editor de páginas ahora muestra etiquetas de acción de flujo de trabajo localizadas. Los autores ya no ven cadenas en inglés para las opciones de flujo de trabajo. Las opciones incluyen acciones de aprobación, publicación, solicitud y cancelación de publicación. (SITES-18103)
* El menú desplegable Principal del panel de edición Separador ahora muestra cadenas localizadas sin truncamiento. Los autores pueden revisar la etiqueta completa cuando configuren el componente. (SITES-17480)
* El editor de páginas ahora muestra etiquetas localizadas para &quot;Anchura completa&quot; y &quot;Anchura fija&quot; en el menú Estilos del componente Contenedor. Los autores que utilizan configuraciones regionales admitidas ya no ven esas cadenas en inglés. (SITES-17478)
* Los autores ahora pueden leer la información completa del objeto en el área de propiedades de navegación de la consola Plantillas. La IU mantiene la información del objeto alineada y evita el truncamiento del texto durante la edición de la plantilla. (SITES-15480)
* Los autores ahora pueden leer la etiqueta completa &quot;Forms y documentos con plantilla&quot; en el panel lateral Referencias. La consola Plantillas ya no corta la cadena de las configuraciones regionales admitidas. (SITES-13167)
* La vista Referencias ahora utiliza texto localizado para el mensaje de error de actualización. Los autores ven la mensajería traducida cuando AEM no puede actualizar la lista de referencias. (SITES-13102)
* La validación del formulario ahora identifica el campo que contiene un valor de hora no válido. El modal Deformación de tiempo muestra mensajes de error más claros para que los autores puedan corregir el campo Horas o Minutos afectado. (SITES-10980)
* La consola Plantillas ahora muestra una etiqueta Assets localizada en el cuadro de diálogo Seleccionar imagen. La etiqueta aparece correctamente cuando los autores examinan los recursos desde las propiedades de la plantilla. (SITES-8113)

#### MSM: Live Copy{#sites-msm-live-copies-6525}

* La Información general de Live Copy ahora localiza los formatos de fecha en la vista Estado de relación. Los campos L **Última modificación de Live Copy de Source**, **Última modificación de Live Copy** y **Última implementación** muestran fechas que coinciden con la configuración regional del usuario. (SITES-40756)
* MSM ahora registra más detalles para los eventos push-on-modify. La información de evento añadida ayuda a los equipos a rastrear la actividad de despliegue e identificar el origen de los cambios de página inesperados. (SITES-38029)

#### Editor de páginas{#sites-pageeditor-6525}

* Los autores ahora pueden crear etiquetas que incluyan mayúsculas o espacios y aplicarlas durante el primer guardado de Propiedades de página. AEM crea la etiqueta y escribe el valor correcto en los metadatos de la página durante la misma operación. (SITES-42550)

* Los autores ahora pueden crear fragmentos de contenido en carpetas DAM cuyos nombres contengan un apóstrofo. AEM administra correctamente la ruta de la carpeta codificada y ya no almacena en déclencheur una NullPointerException durante la creación. (SITES-38653)

* AEM ahora admite las acciones de copiar y pegar para los componentes de fragmento de contenido configurados en el Editor de páginas. El componente conserva su referencia de fragmento de contenido, para que los autores puedan duplicar el contenido sin volver a crear manualmente. (SITES-41586)
* El Editor de páginas ahora muestra correctamente la información sobre herramientas de descripción de primer campo en los cuadros de diálogo de componentes. Las descripciones largas permanecen visibles, por lo que los autores pueden revisar las instrucciones de los campos sin perder texto en la parte superior de la información del objeto. (SITES-39937)
* Los autores ahora pueden abrir el cuadro de diálogo Vínculo del editor de texto enriquecido cuando utilizan AEM a través de HTTP. La corrección restaura la edición de vínculos para entornos locales que no utilizan HTTPS. (SITES-39467)

<!-- #### Replication{#sites-replication-6525} -->

<!-- #### Rich Text Editor{#sites-rte-6525} -->

#### Editor universal {#sites-universal-editor-6525}

* El editor universal ya no se abre en el modo de vista previa de forma predeterminada. AEM envía a los usuarios al entorno del editor universal de producción a menos que soliciten explícitamente un comportamiento de vista previa. (SITES-37193)
* El editor universal ahora se abre en modo de vista previa para el desarrollo de AEM, el desarrollo rápido y los entornos de ensayo. El comando Abrir utiliza el comportamiento de previsualización correcto para las instancias que no son de producción. (SITES-33839)

### [!DNL Assets] {#assets-6525}

* La biblioteca de cliente Mis recursos compartidos ahora administra de forma segura los datos de título de recursos compartidos antes de agregarlos al marcado de la página. Las páginas compartidas generadas ya no exponen a los usuarios a la inyección de scripts mediante metadatos de recursos manipulados. (ASSETS-60898)

* Las licencias de Adobe Stock ahora funcionan correctamente en la interfaz de usuario de Assets. El botón Licencia ya no permanece desactivado después de que AEM cargue el perfil de recursos de stock y los datos de derechos. (ASSETS-62610)
* La notificación de caducidad de recursos predeterminada ahora gestiona correctamente las fechas de caducidad inminentes. Los correos electrónicos de recordatorio se ejecutan cuando el tiempo restante alcanza el umbral configurado, en lugar de omitir los recursos con una caducidad de ocho días. (ASSETS-57857)

* AEM Assets ahora restaura la navegación mediante el teclado después de que los usuarios elijan una búsqueda guardada. La interfaz permite que los usuarios se alejen de la lista desplegable sin actualizar ni reiniciar la vista de Assets. (ASSETS-52061)

* El flujo de trabajo de descarga de Admin View ahora conserva correctamente los nombres de los archivos ZIP. La descarga de un recurso ZIP ya no produce un nombre de archivo con una extensión .zip doble. (ASSETS-62207)
* El flujo de trabajo de referencia de Assets ahora gestiona correctamente los espacios en los nombres de archivo. Las actualizaciones de recursos relacionadas ya no fallan cuando un nombre de archivo seleccionado incluye uno o más espacios. (ASSETS-56418)

#### [!DNL Dynamic Media]{#assets-dm-6525}

El menú desplegable Subtítulos y Pistas de audio ahora muestra el árabe como idioma admitido en Dynamic Media. Esta actualización permite a los usuarios agregar pistas de subtítulos en árabe sin soluciones personalizadas. (ASSETS-61771)

### [!DNL Forms]{#forms-6525}

* La vista previa de comunicaciones interactivas ahora carga el contenido correctamente después del Service Pack de AEM Forms 6.5.24.0. El texto ya no se carga lentamente con los espacios que faltan, por lo que la vista previa coincide con el contenido creado y sigue siendo más fácil de leer. (FORMS-25346)
* Los detalles de validación ahora aparecen en los componentes principales de Forms adaptable después de configurar un patrón de validación y guardar el formulario. El patrón permanece visible en la interfaz de creación. (FORMS-25236)
* La generación de documentos ahora administra correctamente los fragmentos anidados del lenguaje de descripción extensible de Forms (XDP) en los entornos de AEM Forms 6.5 Service Pack 23 y AEM Forms Service Pack 6.5.24.0. (FORMS-25234)
* El texto localizado fuera de los fragmentos de formulario ahora se muestra en el idioma correcto durante la revalidación del lado del servidor de Forms adaptable mediante el motor Rhino. El texto ya no vuelve al idioma predeterminado después del envío. (FORMS-25224)
* El Servicio de salida ya no se bloquea con un Error de instrucción no válido en Red Hat Enterprise Linux (RHEL) 8 después de actualizar a AEM Forms Service Pack 6.5.24.0. La generación de documentos y el procesamiento de salida de formularios se completan sin interrupciones en el servicio. (FORMS-25192)
* Los paneles y el contenido añadido dinámicamente mediante la función addInstance() en Forms adaptable ahora aparecen cuando el número inicial de instancias se establece en 0. (FORMS-25169, FORMS-25124)
* Las traducciones al chino tradicional (Hong Kong) ahora se muestran correctamente en los entornos de creación y publicación después de actualizar a AEM Forms Service Pack 6.5.24.0. El contenido localizado de zh-HK ya no aparece en el idioma incorrecto o vuelve a las cadenas predeterminadas de forma inesperada. (FORMS-25042)
* La navegación mediante el teclado en el campo Firma manuscrita del Forms adaptable ahora mueve el enfoque de forma consistente dentro y fuera del área de firma al tabular en el formulario. (FORMS-25011)
* Los archivos de Lenguaje de descripción de servicios web (WSDL) ahora se cargan correctamente en el paso Invocar servicio web durante las operaciones de configuración y actualización. (FORMS-24992, FORMS-24789, FORMS-24188)
* Los borradores de cartas ahora conservan los saltos de línea cuando se aplican condiciones a fragmentos de texto. El contenido de varias líneas ya no aparece como una sola línea continua. (FORMS-24602)
* Los flujos de trabajo de Adobe Sign en AEM Forms en Adobe Managed Services (AMS) ya no se detienen cuando la respuesta de estado de firma no se devuelve después de alcanzar el paso de Adobe Sign. (FORMS-24514)
* La conversión de HTML a formato de documento portátil (PDF) ya no agota el tiempo de espera de forma intermitente en AEM Forms Service Pack 6.5.24.0, incluso para trabajos de conversión grandes o complejos. (FORMS-23978)
* La administración del modo de backup seguro en la interfaz de usuario de administración ahora funciona correctamente después de instalar el parche AEMForms-6.5.0-0112. Los usuarios pueden deshabilitar o desactivar el Modo de copia de seguridad segura cuando la opción esté disponible. (FORMS-23976, FORMS-23718)
* La búsqueda de fuentes de datos del modelo de datos de formulario ya no falla o muestra etiquetas de Lenguaje de marcado de hipertexto (HTML) sin procesar en los resultados de búsqueda. Los resultados muestran texto legible. (FORMS-23875)
* Las funciones personalizadas ahora se cargan durante la ejecución cuando el Forms adaptable está incrustado en páginas de Sites que utilizan versiones de componentes principales admitidas en el Service Pack de AEM Forms 6.5.24.0. (FORMS-23802)
* Las reglas numéricas de las comunicaciones interactivas ahora evalúan los valores correctamente al analizar con la biblioteca actualizada de Notación de objetos de JavaScript (JSON) de Sling Commons. Los campos numéricos gestionan los cambios de análisis de BigDecimal de forma coherente. (FORMS-23733)
* El comportamiento del documento de registro ahora es coherente al trabajar con la versión 6.5.0 y versiones posteriores. La salida del formulario y el procesamiento relacionado se alinean con el comportamiento esperado de los entornos más nuevos. (FORMS-23338)

#### Forms JEE {#forms-jee-6525}

* El inicio de la aplicación ya no falla al cargar el componente de registro con un error no se encontró ninguna clase para org.owasp.esapi.reference.JavaLogFactory. Los entornos afectados se inicializan correctamente sin que sea necesario reiniciar o volver a configurar el servicio. (FORMS-25348)
* El inicio se completa correctamente después de aplicar el Service Pack 25. El proceso de arranque del sistema ya no falla antes de que finalice la inicialización. (FORMS-25347)
* Los componentes principales del formato de documento portátil (PDF) (CPDF) ahora se crean y ejecutan correctamente en entornos Linux sin detenerse inesperadamente durante la ejecución. (FORMS-25115)
* La descodificación de códigos de barras ya no falla con errores DecodingException al procesar ciertos archivos de Formato de documento portátil (PDF) durante la extracción de códigos de barras. (FORMS-23534, FORMS-23449)

#### Forms Designer {#forms-designer-6525}

* La salida de ExportData ahora coincide con los datos del formulario al utilizar ExportData en la versión 6.5. Los campos XML (Lenguaje de marcado extensible) exportados se alinean con los valores mostrados en los formularios originales. (LC-3922791)
* El servicio Output ahora genera etiquetas de accesibilidad correctas en los archivos de formato de documento portátil (PDF) creados en el Service Pack de AEM Forms 6.5.22.0. Las tecnologías de asistencia leen el contenido en el orden correcto sin omitir elementos. (LC-3922756)
* El servicio Output ahora refleja correctamente los estados de campo ocultos o deshabilitados al acoplar formularios con formato de documento portátil (PDF) con el etiquetado habilitado. (LC-3922708)
* Los campos con pie de ilustración inferior en Workbench ahora reciben el etiquetado correcto, lo que mejora la coherencia y la accesibilidad en los documentos generados. (LC-3922619)
* Los códigos QR de los formularios se pueden analizar después de actualizar a AEM Forms Service Pack 6.5.20.0. Los escáneres estándar leen de forma fiable los códigos QR generados. (LC-3922551)
* El procesamiento de servicios de Forms ahora produce una salida coherente al utilizar una entrada idéntica en distintos paquetes de servicio. Los valores procesados ya no difieren entre AEM Forms Service Pack 6.5.17.0 y AEM Forms Service Pack 6.5.18.0. (LC-3922461)
* Los documentos de PDF/A generados a partir de plantillas de paquete de datos XML (XDP) ahora representan correctamente los estilos de borde cuadrado hundido. El aspecto del campo de formulario coincide con el diseño diseñado. (LC-3922180)
* Los envíos de formato de documento portátil plano (PDF) ahora conservan los datos en todas las secciones. Los valores introducidos permanecen en el documento aplanado final. (LC-3922008)
* Los archivos estáticos convertidos con formato de documento portátil (PDF) ya no generan varias etiquetas de vínculo a partir de un solo vínculo en la plantilla XDP original. (LC-3921997)
* La exportación de envíos desde AEM Forms ahora incluye todos los campos en los archivos de salida exportados. (LC-3921983)


### Foundation {#foundation-6525}

#### Apache Felix {#foundation-apachefelix-6525}

El inicio ahora conecta correctamente el servicio CredentialsSupport para la autenticación basada en Felix. Esto evita los errores de dependencia que pueden afectar a la autenticación de tokens durante el inicio de AEM. (GRANITE-63186)

<!-- #### Campaign{#foundation-campaign-6525} -->

<!-- #### Cloud Services{#foundation-cloudservices-6525} -->

<!-- #### Communities {#foundation-communities-6525} -->

<!-- #### Content distribution{#foundation-content-distribution-6525} -->

#### CRX {#foundation-crx-6525}

La edición de archivos JSP ahora funciona como se espera en CRXDE Lite después de las actualizaciones de AEM 6.5. El editor de CodeMirror carga el contenido del archivo en lugar de dejar en blanco la pestaña JSP. (GRANITE-64333)

<!-- #### Granite{#foundation-granite-6525} -->

<!-- #### Integrations{#foundation-integrations-6525} -->

<!-- #### Jetty{#foundation-jetty-6525} -->

#### Localización{#foundation-localization-6525}

* El cuadro de diálogo de carga de certificados en Seguridad > Almacén de confianza ahora muestra etiquetas de formato de datos localizadas. Los usuarios ya no ven etiquetas inglesas no localizadas cuando agregan un certificado. (NPR-43412)

* El cuadro de diálogo Crear almacén de claves ahora alinea el botón Cancelar con los demás botones del cuadro de diálogo. El diseño del botón permanece coherente y ya no pasa de la alineación. (NPR-43291)
* El cuadro de diálogo Comprobar en **Seguridad** > A **Configuraciones de Adobe IMS** ahora muestra texto de confirmación localizado. Los mensajes de comprobación y eliminación ya no aparecen como cadenas inglesas no localizadas. (NPR-43289)
* Las etiquetas de IU localizadas ahora aparecen correctamente en los cuadros de diálogo afectados y en la pestaña Almacén de claves. Los valores de Aria-label utilizan cadenas traducidas, y las etiquetas de campo de contraseña se muestran sin truncamiento. (NPR-43285)
* El flujo de trabajo Crear nuevo usuario ahora muestra errores de validación localizados para caracteres no válidos. Los usuarios reciben un mensaje claro y traducido en lugar de una cadena IllegalArgumentException no localizada. (GRANITE-52920)

<!-- #### Oak {#foundation-oak-6525} -->

#### Plataforma{#foundation-platform-6525}

* El botón Mostrar referencias de etiqueta ahora muestra el número de referencias para la etiqueta seleccionada. Esta actualización ayuda a los usuarios a comprender el uso de etiquetas sin navegación adicional. (CQ-4355509)
* El cuadro de diálogo Mover en Etiquetado ahora coloca los mensajes de validación correctamente. El texto de error ya no cubre el icono de ruta de búsqueda cuando los usuarios envían el cuadro de diálogo con un campo obligatorio vacío. (CQ-4353009)

#### Seguridad{#foundation-security-6525}

AEM ahora lista de permitidos palabras clave adicionales que contienen secreto de cliente. La creación de la configuración ya no falla cuando las integraciones admitidas utilizan estos patrones de nomenclatura de secreto de cliente. (GRANITE-66495)

<!-- #### Sling{#foundation-sling-6525} -->

<!-- #### SPA editor {#foundation-spa-editor-6525} -->

#### Traducción{#foundation-translation-6525}

Los recuentos de estado del proyecto de traducción ahora se actualizan correctamente después de la actualización. Los autores pueden revisar los valores en borrador, en curso y completos sin depender de metadatos obsoletos del comportamiento anterior del Service Pack. (NPR-43418)

#### Interfaz de usuario{#foundation-ui-6525}

* Las direcciones URL de consola de Sites introducidas manualmente ahora se resuelven en la página o ruta de carpeta deseada. La jerarquía de contenido permanece coherente después de la actualización y ya no vuelve a la dirección URL base. (NPR-43688)
* El grupo de pruebas del Administrador de paquetes de Adobe CRX ya no falla después de que una instancia de AEM 6.5 LTS SP1 se actualice a LTS SP2. La prueba del servlet de lista de miniaturas ahora se completa según lo esperado. (NPR-43534)

* El árbol de contenido de la consola Sitios ahora se carga de forma coherente después de cada actualización del explorador. Los autores ya no ven un carril izquierdo en blanco ni un mensaje &quot;No hay elemento&quot; cuando existe contenido. (NPR-43442)

<!-- #### WCM{#foundation-wcm-6525} -->

#### Flujo de trabajo{#foundation-workflow-6525}

* El editor del modelo de flujo de trabajo ahora valida correctamente las rutas del modelo de flujo de trabajo específicas del inquilino. Los clientes que almacenan modelos de flujo de trabajo en rutas /conf de nivel de inquilino pueden editarlos sin moverlos a rutas de configuración globales. (GRANITE-65376)

* El editor del modelo de flujo de trabajo ahora normaliza las rutas de archivo de Windows durante la validación de rutas. Los autores pueden editar modelos de flujo de trabajo en servidores de Windows sin errores de acceso que bloquean las actualizaciones de modelos. (GRANITE-63692)
* La creación de tareas ahora incluye la validación del lado del servidor para las fechas de vencimiento. Los usuarios no pueden crear tareas con una fecha de vencimiento anterior a la fecha de inicio, lo que mantiene la coherencia de los datos de tareas de la bandeja de entrada. (CQ-4362253)
* La creación del área de nombres ahora gestiona correctamente el texto localizado. Los usuarios pueden introducir caracteres no latinos en el campo Título y crear el área de nombres sin un error de validación. (CQ-4355587)

## Instalación de [!DNL Experience Manager] 6.5.25.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.25.0 requiere [!DNL Experience Manager] 6.5. Consulte [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del Service Pack está disponible en [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip) de Adobe.
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.25.0 en una de las instancias de creación mediante el Administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe no recomienda quitar ni desinstalar el paquete [!DNL Experience Manager] 6.5.25.0. Como tal, antes de instalar el paquete, debe crear una copia de seguridad de `crx-repository` en caso de que deba revertirla. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Instalar el Service Pack en [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie la instancia antes de la instalación si está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de realizar la instalación, realice una instantánea o una copia de seguridad nueva de la instancia de [!DNL Experience Manager].

1. Descargar el Service Pack desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de la instalación del Service Pack, sustituya el conector existente por un nuevo archivo binario, proporcionado en la carpeta de instalación, y reinicie la instancia. Consulte [Almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo de la IU del administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete actualizador para asegurarse de que la instalación es correcta. Normalmente, este problema se produce en el explorador [!DNL Safari], pero puede ocurrir de forma intermitente en cualquier explorador.

**Instalación automática**

Existen dos métodos diferentes que puede utilizar para instalar [!DNL Experience Manager] 6.5.25.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en la carpeta `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.
* Use la [API HTTP del administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que se instalen los paquetes anidados.

>[!NOTE]
>
>Experience Manager 6.5.25.0 no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validación de la instalación**

Para conocer las plataformas que están certificadas para funcionar con esta versión, consulte los [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.25.0)` en [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos los paquetes OSGi tienen el valor **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es de la versión 1.22.20 o posterior (utilice la consola web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Instalar Service Pack para [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obtener instrucciones para instalar el Service Pack en Experience Manager Forms, consulte [Instrucciones de instalación del Service Pack de Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funcionalidad Formularios adaptables, disponible en [AEM 6.5 Inicio rápido](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), está diseñada únicamente para la exploración y la evaluación. Para su uso en producción, es esencial obtener una licencia válida para AEM Forms, ya que la funcionalidad Formularios adaptables requiere una licencia adecuada.

### Instalación del paquete de índice de GraphQL para fragmentos de contenido de Experience Manager{#install-aem-graphql-index-add-on-package}

Los clientes que usen GraphQL deben instalar el [fragmento de contenido de Experience Manager con el paquete de índice 1.1.1 de GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Al hacerlo, puede añadir la definición de índice necesaria según las funciones que utilizan realmente.

Si no se instala este paquete, las consultas de GraphQL pueden ser lentas o dar error.

>[!NOTE]
>
>Instale este paquete solo una vez por instancia; no es necesario reinstalarlo con cada Service Pack.

### UberJar{#uber-jar}

UberJar para [!DNL Experience Manager] 6.5.25.0 está disponible en el [repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.25/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para utilizar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.25</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar y los demás artefactos relacionados están disponibles en el repositorio de Maven Central, en lugar del repositorio Maven público de Adobe (`repo.adobe.com`). Se ha cambiado el nombre del archivo principal de UberJar a `uber-jar-<version>.jar`. Por lo tanto, no hay `classifier`, con `apis` como valor, para la etiqueta `dependency`.



## Funciones en desuso y eliminadas{#removed-deprecated-features}

Consulte [Funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md) para obtener una lista detallada de todas las funciones obsoletas o eliminadas de AEM 6.5.

### Compatibilidad con fragmentos de contenido en la API REST de AEM Assets {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2 proporciona OpenAPI modernas para la administración de modelos y fragmentos de contenido, por lo que los puntos finales de compatibilidad de fragmentos de contenido más antiguos en la API de REST de AEM Assets ya no se utilizan.

Adobe tiene la intención de mantener estos extremos más antiguos disponibles hasta que se produzca un anuncio de fin de vida útil. Adobe no planea más mejoras para los puntos finales obsoletos.

### Editor de SPA {#spa-editor}

[El editor de SPA](/help/sites-developing/spa-overview.md) ha quedado obsoleto para nuevos proyectos a partir de la versión 6.5.25 de AEM 6.5. El Editor SPA sigue siendo compatible con los proyectos existentes, pero no debe utilizarse para nuevos proyectos.

Los editores preferidos para administrar contenido sin encabezado en AEM ahora son:

* [El editor universal](/help/sites-developing/universal-editor/introduction.md) para la edición visual.
* [El editor de fragmentos de contenido](/help/sites-developing/universal-editor/introduction.md) para la edición de contenido sin encabezado basada en formularios.

## Problemas conocidos{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **Relacionado con Oak**
En Service Pack 13 y versiones posteriores, ha comenzado a aparecer el siguiente registro de errores que afecta a la caché de persistencia:

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  O bien

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  Para resolver esta excepción, haga lo siguiente:

   1. Eliminar las dos carpetas siguientes de `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. Instale el Service Pack o reinicie Experience Manager as a Cloud Service.
Las nuevas carpetas de `cache` y `diff-cache` se crean automáticamente y ya no experimenta una excepción relacionada con `mvstore` en `error.log`.

* Actualice las consultas de GraphQL que puedan haber usado un nombre de API personalizado para el modelo de contenido y utilizará el nombre predeterminado del modelo de contenido en su lugar.

* Una consulta de GraphQL puede emplear el índice `damAssetLucene`, en lugar del índice `fragments`. Esta acción podría provocar que las consultas de GraphQL fallen o tarden mucho en ejecutarse.

  Para corregir el problema, `damAssetLucene` debe estar configurado para incluir las dos propiedades siguientes en `/indexRules/dam:Asset/properties`:

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  Una vez modificada la definición del índice, se requiere una reindexación (`reindex` = `true`).

  Después de estos pasos, las consultas de GraphQL deberían funcionar más rápido.

* Al intentar mover, eliminar o publicar fragmentos de contenido, sitios o páginas, hay un problema cuando se recuperan las referencias de fragmentos de contenido. La consulta en segundo plano falla; la funcionalidad no funciona.
Para garantizar el funcionamiento correcto, debe agregar las siguientes propiedades al nodo de definición de índice `/oak:index/damAssetLucene` (no se requiere la reindexación):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si actualiza la instancia de [!DNL Experience Manager] de la versión 6.5.0-6.5.4 al Service Pack más reciente de Java™ 11, verá excepciones `RRD4JReporter` en el archivo `error.log`. Para detener las excepciones, reinicie la instancia de [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Los usuarios pueden cambiar el nombre de una carpeta en una jerarquía de [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Durante la instalación de [!DNL Experience Manager] 6.5.x.x se pueden mostrar los siguientes errores y mensajes de advertencia:
   * “Cuando la integración de Adobe Target se configura en [!DNL Experience Manager] mediante la API de Target Standard (autenticación IMS) y, a continuación, se exportan fragmentos de experiencias a Target, se crean tipos de ofertas incorrectos. En lugar de “Experience Fragment”/source “Adobe Experience Manager”, Target crea varias ofertas con el tipo “HTML”/source “Adobe Target Classic”.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en `granite/operations/maintenance`.
   * La validación del lado del servidor de formularios adaptables falla cuando se utilizan funciones de agregado como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en `granite/operations/maintenance`.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al previsualizar el recurso a través del visor de banners a la venta.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`: tiempo de espera agotado para completar el cambio de registro sin registrar.

* A partir de AEM 6.5.15, el motor Rhino JavaScript proporcionado por el paquete `org.apache.servicemix.bundles.rhino` presenta un nuevo comportamiento de hoisting. Los scripts que utilizan el modo estricto (`use strict;`) deben declarar sus variables correctas. De lo contrario, no se ejecutan y terminan generando un error de tiempo de ejecución.

* La instalación del contenido listo para usar relacionado con el etiquetado mediante un paquete de actualización oficial restablece la propiedad de idiomas del nodo `/content/cq:tags` a su valor predeterminado. Esta acción se aplica a los paquetes de servicio, los paquetes de servicio de seguridad, los paquetes de funciones ampliadas, los paquetes de funciones acumulativas, los parches, etc. Por lo tanto, es necesario añadirlo desde las propiedades antes de la instalación.

### Problema conocido de AEM Sites {#known-issues-aem-sites-6525}

Fragmentos de contenido: la previsualización falla debido a la protección DoS para un gran árbol de fragmentos. Consulte el [artículo de KB sobre las opciones de configuración predeterminadas del ejecutor de consultas de GraphQL](https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)

### Problemas conocidos de AEM Forms {#known-issues-aem-forms-6525}

* **FORMS-14521** Si un usuario intenta obtener una vista previa de un borrador de carta con datos XML guardados, se queda atascado en el estado `Loading` para algunas cartas específicas.
* **FORMS-16603** En la vista preliminar de la interfaz de usuario de Interactive Communications Agent, algunos valores calculados no se muestran correctamente.
* **FORMS-15681** Cuando la carta se ve en la Vista preliminar, el contenido cambia; algunos espacios desaparecen y ciertas cartas se reemplazan por `x`.
* **FORMS-15428** Después de actualizar a AEM Forms Service Pack 20 (6.5.20.0) con el complemento de Forms, las configuraciones que dependen del servicio heredado de Adobe Analytics Cloud mediante autenticación basada en credenciales dejan de funcionar. Este problema impedía que las reglas de análisis se ejecutaran de forma correcta.
* **FORMS-16557** En la vista preliminar de la interfaz de usuario de Interactive Communications Agent, el símbolo de moneda (como el signo de dólar $) se muestra de manera incoherente en todos los valores de campo. Aparece para valores de hasta 999, pero falta para valores de 1000 y superiores.
* **FORMS-16575** Las modificaciones realizadas en el XDP de los fragmentos de diseño anidados en una comunicación interactiva no se reflejarán en el editor de CI.
* **FORMS-21378**: cuando la validación del lado del servidor (SSV) está habilitada, es posible que se produzcan errores en los envíos de formularios. Si tiene este problema, póngase en contacto con el Soporte técnico de Adobe para obtener ayuda.
* **FORMS-23722** Cuando un formulario que contiene un campo de **Archivo adjunto** que usa `bindref` se envía a un flujo de trabajo de AEM con un paso de **Asignar tarea**, no se muestran los archivos adjuntos. Como resultado, no aparecen cuando la tarea se abre desde la Bandeja de entrada. Los archivos se guardan correctamente en el repositorio, pero la interfaz de usuario del paso Asignar tarea no muestra los archivos adjuntos.
* **FORMS-23802** Las funciones personalizadas no se pueden cargar en la vista previa o en la publicación cuando un formulario adaptable está incrustado en una página de Sites. Este problema se produce cuando la versión de la biblioteca **aem-forms-core-component** es anterior a la 1.1.76. Puede ver un error como `InvalidFormContainerException: No form container found` en los registros. Para resolver este problema, [descargue e instale la revisión](/help/release-notes/aem-forms-hotfix.md) para AEM Forms SP24 (AddOn 6.0.1454).

#### Problemas conocidos con revisiones disponibles {#aem-forms-issues-with-hotfixes}

<!--
>[!NOTE]
>
>Avoid upgrading to Service Pack 6.5.25.0 for issues without an available hotfix. It may lead to unexpected errors. Upgrade to Service Pack 6.5.25.0 only after the required hotfixes are released.
-->

Los siguientes problemas incluyen una revisión disponible para su descarga e instalación. Puede [descargar e instalar la revisión](/help/release-notes/aem-forms-hotfix.md) para resolver los siguientes problemas:

* **FORMS-23881** En implementaciones JEE de AEM Forms configuradas con el instalador completo de 6.5.23.0, el servicio de salida no procesa las solicitudes cuando se proporciona un archivo XCI personalizado en la invocación. Para resolver este problema, instale el Service Pack más reciente de AEM 6.5.25.0 Forms desde el portal [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html).
* **FORMS-23789** (solo AEM Forms en JEE): Los usuarios experimentaron problemas con Log4j en AEM Forms en JEE SP24, lo que provocó interrupciones en el registro y la supervisión de los clientes empresariales. Para resolver este problema, [descargue e instale la revisión](/help/release-notes/aem-forms-hotfix.md) para AEM Forms en el paquete de servicio JEE 6.5.25.0.
* **FORMS-23802** Las funciones personalizadas no se cargan en la vista previa ni en la publicación cuando el formulario está en una página de Sites con una versión anterior de aem-forms-core-component (&lt;1.1.76). Para resolver este problema, instale la revisión [AEM Forms AddOn 6.0.1454](/help/release-notes/aem-forms-hotfix.md) para SP24.
* **FORMS-23789** (solo AEM Forms en JEE): Los usuarios experimentaron problemas con Log4j en AEM Forms en JEE SP24, lo que provocó interrupciones en el registro y la supervisión de los clientes empresariales. Para resolver este problema, [descargue e instale la revisión](/help/release-notes/aem-forms-hotfix.md) para AEM Forms en el paquete de servicio JEE 6.5.25.0.
* **FORMS-23802** Las funciones personalizadas no se cargan en la vista previa ni en la publicación cuando el formulario está en una página de Sites con una versión anterior de aem-forms-core-component (&lt;1.1.76). Para resolver este problema, instale la revisión [AEM Forms AddOn 6.0.1454](/help/release-notes/aem-forms-hotfix.md) para SP24.
* AEM Forms ahora incluye una actualización de la versión de Struts de la 2.5.33 a la 6.x para el componente de formularios. Esta actualización ofrece los cambios de Struts que se omitieron anteriormente y que no se incluyeron en SP24. La compatibilidad se añadió a través de una [revisión](/help/release-notes/aem-forms-hotfix.md) que puede descargar e instalar para añadir compatibilidad con la última versión de Struts.
* **FORMS-14926** Después de instalar AEM Forms JEE Service Pack 21 (6.5.21.0), si encuentra entradas duplicadas de Jars Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` en la carpeta `<AEM_Forms_Installation>/lib/caching/lib`, realice los siguientes pasos para resolver el problema:

   1. Detenga los localizadores, si están en funcionamiento.
   2. Detenga el servidor de AEM.
   3. Ir a `<AEM_Forms_Installation>/lib/caching/lib`.
   4. Quite todos los archivos de parche de Geode, excepto `geode-*-1.15.1.2.jar`. Confirme que solo están presentes los Jars Geode con `version 1.15.1.2`.
   5. Abra el símbolo del sistema en modo de administrador.
   6. Instale el parche de Geode mediante el archivo `geode-*-1.15.1.2.jar`.

* **FORMS-15256** Cuando los usuarios actualizaron desde AEM 6.5 Forms Service Pack 18 o 19 a Service Pack 20 o 21, encontraron un error de compilación de JSP. Este error les impedía abrir o crear formularios adaptables. También causó problemas con otras interfaces de AEM. Estas interfaces incluían el editor de páginas, la IU de AEM Forms, el editor de flujos de trabajo y la IU de información general del sistema.

  Si tiene un problema de este tipo, siga estos pasos para resolverlo:
   1. Vaya al directorio `/libs/fd/aemforms/install/` en CRXDE.
   2. Elimine el paquete con el nombre `com.adobe.granite.ui.commons-5.10.26.jar`.
   3. Reinicie el servidor de AEM.

* **FORMS-23703** Cuando la regla `contains` está configurada sin un valor predeterminado, se produce un error en la validación del lado del servidor para un formulario adaptable. Puede instalar la versión más reciente de [AEM Forms 6.5.25.0 Service Pack](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases) para solucionar el problema.
* **GRANITE-63681** La configuración predeterminada del sistema bloquea las palabras clave y los patrones de regex necesarios, lo que impide que los conectores del modelo de datos de formulario se autentiquen. Para resolver el problema, descargue e instale la revisión desde el [vínculo](/help/release-notes/aem-forms-hotfix.md).
* La conversión de **FORMS-23979** HTML a PDF (PDFG) puede experimentar tiempos de espera intermitentes. Posteriormente se publicó una versión más reciente del complemento de Forms para SP24 que incluye la corrección. Si encuentra este problema, actualice su entorno al [último complemento de Forms publicado para 6.5.25.0](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#aem-65-forms-releases).
* **FORMS-23717** Después de actualizar a **AEM Forms6.5.25.0**, `server.log` y `error.log` se pueden inundar con mensajes WARN repetidos, como *Error al crear la fábrica del analizador seguro* o *No se admite el atributo Security*. Los registros pueden crecer en alrededor de **5-10 líneas por segundo** (cientos de MB por hora), lo que puede llenar el disco y bloquear el despliegue de producción.

Para reducir el volumen de registro, establezca el nivel de registro de `com.adobe.util.XMLSecurityUtil` en `ERROR` en la configuración del servidor de aplicaciones o mediante el argumento de JVM `-Dlogging.level.com.adobe.util.XMLSecurityUtil=ERROR`. Esta funcionalidad solo oculta los mensajes y no corrige la causa subyacente.

* **FORMS-23875** En la búsqueda del modelo de datos de formulario, la interfaz de usuario muestra una etiqueta de HTML aunque falte una entidad relevante. Para resolver el problema, descargue e instale la revisión desde [el vínculo](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bb-expressionmanager-pkg-10.0.48.zip).

## Paquetes de contenido y paquetes OSGi incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes archivos zip contienen los documentos de texto que enumeran los paquetes OSGi y los paquetes de contenido incluidos en esta versión del paquete de servicio [!DNL Experience Manager] 6.5:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.25.0](/help/release-notes/assets/65250-bundles.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.25.0](/help/release-notes/assets/65250-packages.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos{#restricted-sites}

Estos sitios web solo están disponibles para los clientes. Si es cliente y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe.

* [Descarga del producto en licensing.adobe.com](https://licensing.adobe.com/)
* [Póngase en contacto con Atención al cliente de Adobe](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de productos](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html?lang=es)
>* Documentación de [[!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/es/docs/experience-manager-65)
>* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)



