---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6.5
description: Encuentre información de la versión, novedades, instrucciones de instalación y una lista de cambios detallada para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
contentOwner: Rick Brough
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ed762d86-a04b-452b-a08f-86359bb8ff27
    internal-label: Configuration and operations
subfeature_v2:
  - id: c21ccc2b-e0c8-4853-bf41-f12259ed93f8
    internal-label: Release information
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 56b13809475a59f188750b86503e316e69171fe1
workflow-type: tm+mt
source-wordcount: '7273'
ht-degree: 15%
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
| Versión | 6.5.26.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del Service Pack |
| Fecha | 12 de noviembre de 2026 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |


<!-- REWRITE AI GENERATED SUMMARY OF NOTES BELOW FOR EACH NEW SERVICE PACK RELEASE -->

Experience Manager 6.5.26.0 incluye nuevas características, mejoras clave solicitadas por el cliente y correcciones de errores. También incluye mejoras de accesibilidad, localización, rendimiento, estabilidad y seguridad basadas en la versión 6.5 disponible desde abril de 2019.

Los aspectos destacados del Service Pack 26 son los siguientes:

* Seguridad. Dos correcciones esenciales cierran una vulnerabilidad de inyección de plantillas del lado del servidor en el Editor de metadatos y violaciones de scripts en sitios múltiples (XSS) en los servlets de la IU de Coral.
* Cumplimiento de C2PA. Assets ahora detecta las credenciales de C2PA y firma las representaciones que genera el flujo de trabajo de actualización de recursos. La firma se ejecuta localmente en cada instancia y no se admite la infraestructura de firma dedicada o propiedad del cliente.
* Accesibilidad. Más de 25 correcciones ayudan al editor de páginas y a la consola Sites a cumplir los requisitos de contraste, teclado y lector de pantalla de WCAG.
* Localización. Docenas de correcciones traducen cadenas y corrigen problemas de diseño en Sites, Assets, Seguridad y Operaciones.
* Fiabilidad. Corrige la contención del bloqueo de GraphQL de la dirección en las instancias de publicación, los despliegues de MSM, las acciones de la barra de herramientas del Editor de texto enriquecido y la activación de páginas en la IU clásica.
* Analytics. La integración de Launch utiliza la API de Adobe Analytics 2.0 antes de que Analytics 1.4 finalice su vida útil el 31 de agosto de 2026.


<!-- UPDATE FOR EACH NEW RELEASE -->

## Se han corregido problemas, mejoras y mejoras en el Service Pack 26 {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6526}

#### Accesibilidad {#sites-accessibility-6526}

* Los autores pueden agregar, mover y quitar componentes únicamente mediante el teclado. La interacción de arrastrar y soltar requería un puntero, por lo que no cumplía el criterio de teclado WCAG 2.1.1. El editor ahora proporciona las opciones emergentes Insertar componente, Cortar y pegar y Eliminar como equivalentes operables mediante el teclado. (SITES-25359)

* Los autores ahora pueden ver el botón Formato activo (&quot;T&quot;) en el menú en línea del componente Texto. Después de aplicar formato de negrita o cursiva, el icono del botón permaneció oscuro sobre un fondo gris oscuro y no se alcanzó la relación de contraste mínima de WCAG 2.1 AA de 4.5:1. El CSS actualizado ilumina el icono, que restaura el contraste que proporcionaban los paquetes de servicio anteriores. (SITES-51864)

* La pestaña Assets del Editor de páginas ahora muestra una cadena traducida en la lista desplegable Seleccionar componentes después de elegir Párrafos en la lista desplegable Imágenes. Anteriormente, la cadena &quot;OTHER&quot; aparecía en inglés porque los recursos de localización no lo tenían. El diccionario actualizado proporciona la traducción en todas las configuraciones regionales. (SITES-24525)




* El iframe de ContextHub en el editor de páginas ahora tiene un atributo de título descriptivo. Anteriormente, el elemento `contexthub-ui-iframe` no tenía título, por lo que los usuarios del lector de pantalla no pudieron identificarlo cuando el enfoque se movió a él. El título ahora aparece en todas las páginas y vistas del editor, incluido Lienzo, Carril lateral y Vista previa del diseño. (SITES-24650)
* El botón Filtros del carril del filtro de la consola Sitios no agrega etiquetas visibles encima de los campos Búsquedas guardadas y Seleccionar directorio de búsqueda. Una auditoría informó de que las etiquetas aparecían cuando el foco salía del botón, cuando se presionaba una tecla o cuando se hacía clic en el botón. Las pruebas no reprodujeron el comportamiento, por lo que no fue necesario realizar ningún cambio. (SITES-24706)
* Los vínculos de la consola Sitios y la navegación de la aplicación ahora se destacan con mayor claridad. El texto del vínculo cumplía la relación de contraste de 4.5:1, pero el grosor de fuente delgada y el tamaño pequeño dificultaban la visualización de los vínculos. Un mayor peso de fuente y un tamaño mayor facilitan la lectura del texto a los usuarios con deficiencias visuales. (SITES-24723)
* Los lectores de pantalla ya no anuncian &quot;en blanco&quot; antes del contenido de información sobre herramientas en el modal Preferencias de usuario. Anteriormente, el icono de información usaba `role="tooltip"` con una referencia de `aria-labelledby`, por lo que NVDA leía primero una etiqueta vacía. El icono ahora utiliza `role="button"` y un `aria-label` de &quot;información&quot;, y el cambio se aplica a los componentes del formulario de Coral que comparten el patrón. (SITES-24732)
* El botón Eliminar del modal Delete ahora cumple el requisito de contraste 4.5:1 de WCAG 1.4.3. Anteriormente, el texto en blanco sobre fondo rojo proporcionaba una relación de 3,9:1 después de que los autores seleccionaran un elemento y hicieran clic en Eliminar en la barra de herramientas de acciones. El color más oscuro del botón hace que la etiqueta sea legible para autores con deficiencias visuales. (SITES-24772)
* El encabezado Referencias de la consola Sitios del carril Referencias ahora utiliza un elemento de encabezado en lugar de `div`. Anteriormente, los lectores de pantalla no anunciaban el texto como un encabezado, por lo que los usuarios no podían navegar por encabezados. El encabezado también aparece en la parte superior de la vista Referencias inicial. (SITES-24967)
* El indicador de enfoque de los botones de acordeón en el carril del filtro de la consola Sites ahora cumple el requisito de contraste 3:1 de WCAG 1.4.11. Anteriormente, el indicador azul mostraba una relación de 2,3:1 en el fondo, lo que hacía que el botón de acordeón Etiquetas fuera difícil de encontrar para los usuarios del teclado. El color actualizado proporciona a los usuarios de teclado una señal de enfoque clara. (SITES-24986)
* El indicador de enfoque de los botones de opción del carril del filtro de la consola Sites ahora cumple el requisito de contraste 3:1 de WCAG 1.4.11. Anteriormente, el indicador azul claro mostraba una relación de 1,7:1 contra el fondo. Los usuarios del teclado ahora pueden rastrear su posición en el acordeón de fecha Modificado. (SITES-24987)
* El botón Seleccionar situado junto a los campos Ruta y Etiquetas en el carril lateral del Editor de páginas ya no utiliza un icono de casilla de verificación. Anteriormente, el icono sugería un conmutador, pero al activar el botón se abría un modal que contenía el Directorio de árbol. El botón Seleccionar ahora comunica correctamente su función, y lo mismo se aplica a los modelos Imagen y Teaser. (SITES-25210)
* Los lectores de pantalla ahora omiten las imágenes en miniatura de los recursos en el carril lateral del Editor de páginas. Anteriormente, cada imagen llevaba un texto alternativo que duplicaba el nombre del recurso visible, por lo que los usuarios escuchaban el mismo texto dos veces. Un atributo `alt` vacío marca la imagen como decorativa y mantiene el nombre en el título de la tarjeta. (SITES-25213)
* Los lectores de pantalla reconocen la lista Componentes del carril lateral como una lista. Una auditoría informó de los elementos como elementos no relacionados, pero la prueba confirmó que el marcado utiliza un elemento de lista y elementos de lista. No fue necesario ningún cambio de código. (SITES-25214)
* Los iconos de información de los componentes del carril lateral del Editor de páginas son más grandes y fáciles de ver. Anteriormente, los iconos utilizaban el tamaño extra pequeño de unos 12 píxeles, que los usuarios con deficiencias visuales encontraban difícil de ver. Los iconos ahora utilizan el tamaño medio.(SITES-25217)
* El indicador de enfoque del botón Muestra en el modal Anotación ahora se destaca del botón. Anteriormente, el indicador coincidía con el color de la muestra. Esto dificultaba a los usuarios del teclado ver qué botón estaba enfocado. Un desplazamiento proporciona al indicador suficiente contraste con el fondo y lo mantiene claramente visible. (SITES-25253)
* El campo Fecha del modal Deformación de tiempo ya no lleva `aria-haspopup="dialog"`. Anteriormente, los lectores de pantalla anunciaban que el campo abría un cuadro de diálogo, aunque no fuera así. La eliminación del atributo proporciona a los usuarios del lector de pantalla información precisa. (SITES-25263)
* Las etiquetas de texto de la barra de herramientas Demografía, como &quot;Recomendado&quot;, ahora cumplen el requisito de contraste 4.5:1 de WCAG 1.4.3. Anteriormente, el texto gris sobre un fondo gris oscuro proporcionaba una relación de 2,8:1 en el modo de vista previa. El texto más oscuro o más claro, según el fondo, hace que cada etiqueta sea legible. (SITES-25307)
* El indicador de enfoque de los botones Commerce, Persona y Dispositivo de la barra de herramientas Demografía ahora cumple el requisito de contraste WCAG 1.4.11 de 3:1. Anteriormente, el indicador mostraba una relación de 1,9:1 con respecto al fondo de la barra de herramientas. Los usuarios del teclado ahora pueden rastrear su posición. (SITES-25308)
* El texto que los autores escriben en los campos de texto de la barra de herramientas Demografía ahora cumple el requisito de contraste 4.5:1 de WCAG 1.4.3. Anteriormente, el texto blanco sobre fondo gris producía una relación de 2,9:1 en campos como, por ejemplo, el campo desplegable Perfil `displayName` en modo de vista previa. Los colores actualizados hacen que los valores escritos sean legibles para los autores con deficiencias visuales. (SITES-25318)
* Los lectores de pantalla ahora leen la información del objeto de descripción cuando el enfoque alcanza las casillas de verificación en los cuadros de diálogo Teaser, Imagen y Carrusel. Anteriormente, el texto no estaba asociado mediante programación con la casilla de verificación, por lo que los usuarios no podían oír la instrucción. Un atributo `aria-describedby` ahora vincula cada casilla de verificación con su descripción. (SITES-25364)
* Los lectores de pantalla ahora anuncian qué botón Formatos de párrafo está activo en el Editor de texto enriquecido. Anteriormente, al seleccionar una opción de la lista, la tecnología de asistencia no indicaba la opción actual. El botón activo ahora lleva `aria-current="true"`, y la opción Destino de hipervínculo activo lleva `aria-selected="true"`. (SITES-25367)
* Los botones Ordenar del encabezado de tabla de la vista de lista de la consola Sitios ahora cumplen el requisito de contraste 3:1 de WCAG 1.4.11. Anteriormente, los iconos de color gris claro mostraban una relación de 1,5:1 frente al fondo del encabezado. El color más oscuro del icono hace que los botones sean visibles para los autores con deficiencias visuales. (SITES-25372)
* La pestaña Assets del carril lateral del Editor de páginas ya no se vuelve a cargar cuando el enfoque se mueve al campo Filtro. Anteriormente, al tabular en el campo vacío, se activaba una recarga y los lectores de pantalla anunciaban un mensaje de carga cada vez. La pestaña ahora solo se vuelve a cargar después de cambiar el valor del filtro y pulsar Intro. (SITES-25377)
* El icono de muestra seleccionado en el modal Anotación ahora cumple el requisito de contraste WCAG 1.4.11 de 3:1. Anteriormente, la marca de verificación blanca mostraba una proporción tan baja como 1,58:1 frente a las muestras amarillas, naranjas y verdes. El icono actualizado ofrece a los autores con deficiencias visuales un indicador claro. (SITES-25523)
* La lista Componentes del panel lateral del Editor de páginas ya no utiliza el foco del teclado. Los usuarios del teclado seleccionan y mueven componentes con los controles de la ventana de contenido, por lo que la lista del panel lateral repite la función. Una nota bajo el filtro de componentes informa a los usuarios del teclado dónde encontrar los controles. (SITES-40752)


#### Interfaz de usuario de administración{#sites-adminui-6526}


#### IU clásica{#sites-classicui-6526}

* Los autores pueden volver a activar las páginas en la consola Sitios de la IU clásica (`siteadmin.html`). Anteriormente, el botón Activar página mostraba un control de número &quot;Cargando&quot; indefinidamente y nunca activaba la replicación, porque un script de seguimiento fallido detenía el controlador de clics. El controlador de clics ahora se ejecuta sin errores y completa la activación. (SITES-52165)
* El código de idioma indonesio ahora se muestra como ID en las propiedades de la copia de idioma. Anteriormente, el carril Referencias mostraba el código heredado en para páginas bajo la raíz del idioma indonesio. La actualización del paquete cq-wcm-core corrige el valor, por lo que el código coincide con el estándar ISO. (SITES-4491)

<!--
#### Component Console{#sites-component-console-6526}



#### [!DNL Content Fragments]{#sites-contentfragments-6526}



#### [!DNL Content Fragments] - Admin{#sites-admin-6526}
-->


#### [!DNL Content Fragments] - Editor de fragmentos{#sites-fragments-editor-6526}

* El botón Editar fragmento de contenido aparece inmediatamente para cada referencia de varios campos en el editor de fragmentos de contenido. Anteriormente, el botón permanecía oculto hasta que los autores guardaban el fragmento principal y no hacía nada después de abrir el Explorador de rutas. El editor ahora crea la lista de acciones en el primer procesamiento, de modo que los autores abren los fragmentos a los que se hace referencia sin pasos adicionales. (SITES-43733)

* Los caracteres chinos, japoneses y coreanos ya no se muestran en cursiva en el marcador de posición del cuadro de diálogo Crear fragmento de contenido. Anteriormente, el estilo en cursiva se aplicaba a los caracteres CJK en **Assets** > **Archivos**, lo que dificultaba la lectura del texto. Los estilos actualizados omiten la cursiva para los idiomas CJK. (SITES-43548)
* El editor de fragmentos de contenido valida los campos correctamente después de actualizar la interfaz de usuario de Granite. Un cambio reciente en la interfaz de usuario de Granite provocó una regresión, por lo que las bibliotecas de cliente del editor ya no coincidían con el nuevo comportamiento de validación. Las bibliotecas y pruebas adaptadas resuelven la discrepancia. (SITES-46650)


#### [!DNL Content Fragments]: API GraphQL {#sites-graphql-api-6526}

* Las consultas de GraphQL sobre fragmentos de contenido ahora reconocen las referencias de RemoteRef a Dynamic Media con OpenAPI Assets. Anteriormente, las consultas fallaban con un &quot;Error de validación de consulta persistente&quot; y no devolvían datos de recursos cuando AEM 6.5 Sites consumía AEM as a Cloud Service Assets. Las respuestas ahora incluyen el ID del repositorio y el ID del recurso, de modo que los clientes pueden crear direcciones URL de envío. (SITES-48507)

* Las instancias de publicación siguen respondiendo durante el tráfico intenso de GraphQL. Bloquear la contención en `GraphQLServiceImpl` subprocesos de procesamiento de solicitudes retrasados en los métodos de esquema, lo que ralentiza las solicitudes y requiere reinicios. La sincronización mejorada resuelve la restricción de rendimiento y mantiene la disponibilidad de los sitios y las aplicaciones móviles. (SITES-48699)

* El mensaje de la página Puntos finales de GraphQL permanece localizado después de volver a cargar la página. Anteriormente, el mensaje &quot;No se encontraron puntos de conexión&quot; aparecía en su idioma cuando creaba y eliminaba puntos de conexión, pero volvió a inglés después de una recarga. La página ahora carga la cadena traducida en cada visita. (SITES-43586)


<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6526}
-->


#### [!DNL Content Fragments]: editor de modelos y modelos{#sites-models-model-editor-6526}

* Las miniaturas de los modelos de fragmentos de contenido se muestran en **Herramientas** > **General** > **Modelos de fragmentos de contenido** cuando el nombre de la configuración contiene caracteres localizados, como &quot;español テスト&quot;. Anteriormente, la miniatura cargada no aparecía porque los caracteres provocaban un error en la ruta. La gestión actualizada codifica el nombre correctamente. (SITES-39242)

* La cadena Etiqueta de campo del lienzo del Editor del modelo de fragmentos de contenido ahora aparece en el idioma del usuario. Anteriormente, la etiqueta permanecía en inglés después de que los autores arrastraran un componente al lienzo y se traducía solo después de que guardaban y reabrían el modelo. La etiqueta ahora se traduce inmediatamente, haciendo coincidir el panel Propiedades. (SITES-45383)


<!--
#### [!DNL Content Fragments] - REST API{#sites-restapi-6526}

#### ContextHub{#sites-contexthub-6526}
-->


#### Backend principal{#sites-core-backend-6526}

* La activación programada de la página mediante Tiempo de activación/desactivación ahora se ejecuta solo cuando es necesario. `OnOffTriggerProcessor` activó anteriormente la replicación y la invalidación de caché con demasiada frecuencia, lo que obligó a los autores a volver a publicar el contenido manualmente. La corrección adaptada elimina el procesamiento innecesario y restaura la publicación programada fiable. (SITES-48483)

* La carga de archivos funciona para recursos remotos desde la administración de recursos de próxima generación en un campo múltiple. Anteriormente, la carga fallaba cuando los autores elegían un recurso remoto para un campo dentro de un campo múltiple. La actualización de los componentes principales restaura el flujo de carga, por lo que el campo acepta el recurso. (SITES-44266)


#### Componentes principales{#sites-core-components-6526}

* El Selector de recursos remoto mantiene la imagen de cada elemento multicampo separada. Anteriormente, al seleccionar una imagen en un elemento de varios campos se aplicaba a todos los elementos y la referencia de recurso remoto no se guardaba. Cada elemento contiene ahora su propia selección, y la referencia persiste después de guardar el cuadro de diálogo. (SITES-42376)

* Esta versión incluye correcciones de portada para Commerce, componentes principales, componentes de base (heredados), lanzamientos y Live Copies de MSM. Las correcciones abordan las vulnerabilidades de seguridad, las infracciones de scripts entre sitios (XSS), el comportamiento de carga de archivos y el comportamiento de Live Copy. Los backports alinean AEM 6.5 y AEM 6.5 LTS con las correcciones enviadas anteriormente en AEM as a Cloud Service. (SITES-43738)


<!--
#### Campaign integration{#sites-campaign-integration-6526}

#### ContentHub {#sites-contenthub-6526}

#### Crosswalk {#sites-crosswalk-6526}

#### Experience Fragments{#sites-experiencefragments-6526}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-6526}
-->


#### Sin encabezado: administrador {#sites-headless-admin-6526}

Mejora: La vista Previsualización del administrador sin encabezado ahora pasa la ruta de variación seleccionada al componente de vista previa. Este cambio garantiza que las previsualizaciones de fragmentos de contenido con varias variaciones carguen contenido desde la variación correcta. La matriz `draftFragmentIds` incluye el parámetro de variación. (SITES-42714)


#### Lanzamientos{#sites-launches-6526}

* Las entradas de la cronología para los lanzamientos promocionados ahora se muestran en el idioma del usuario. Anteriormente, las cadenas &quot;Created version of&quot; y &quot;antes de promocionar el lanzamiento&quot; permanecían en inglés después de que los autores promocionaran un lanzamiento y abrieran la cronología del sitio en Sites. Los recursos actualizados proporcionan las traducciones en todas las configuraciones regionales. (SITES-13389)
* El marcador de posición Seleccionar ruta de Launch Source en el panel de filtros Lanzamientos se muestra en su totalidad. Anteriormente, el texto se cortaba en interfaces localizadas, como francés, italiano y portugués, porque no se ajustaba al campo. El diseño actualizado muestra el marcador de posición completo. (SITES-42792)
* La columna Fecha de lanzamiento en Herramientas > Sitios > Lanzamientos ya no muestra AM ni PM en las configuraciones regionales de alemán, francés, español, italiano, portugués de Brasil y chino tradicional. Anteriormente, la columna utilizaba un formato de 12 horas que no coincide con esas configuraciones regionales. La columna ahora muestra el formato de 24 horas. (SITES-43178)


<!--
#### Link Checker{#sites-link-checker-6526}
-->


#### Localización{#sites-localization-6526}

* Ahora se muestran en el idioma del usuario las cadenas de las páginas de Informes de estado en **Herramientas** > **Operaciones**. Anteriormente, los mensajes de Ruta de búsqueda de recursos, Mantenimiento, Cola de replicación, Errores de registro, Paquetes activos y Rendimiento de las solicitudes permanecían en inglés. Los recursos i18n actualizados proporcionan las traducciones y un archivo de reserva mantiene las cadenas disponibles. (NPR-44279)

* El mensaje de error &quot;La configuración de &#39;Ruta JSON&#39; se omite cuando se marca la opción &#39;Agregar manualmente&#39;&quot; ahora se muestra en el idioma del usuario en la consola **Herramientas** > **Assets** > **Esquemas de metadatos**. Anteriormente, el mensaje permanecía en inglés después de que los autores agregaran un elemento desplegable, seleccionaran Agregar a través de la ruta JSON y cambiaran a Agregar manualmente. Los recursos actualizados proporcionan las traducciones. (ASSETS-31575)
* La cadena &quot;promocionada&quot; en las etiquetas **Assets** > **Manage** ahora se muestra en el idioma del usuario. Anteriormente, la cadena permanecía en inglés cuando se pasaba el ratón sobre una etiqueta inteligente después de seleccionar Promocionar. Los recursos actualizados proporcionan la traducción en todas las configuraciones regionales. (ASSETS-36070)
* La etiqueta del botón Agregar ya no se superpone con el botón de **Propiedades de carpeta** > **Contribución de recursos**. Anteriormente, el texto entraba en conflicto con el botón de las interfaces alemán, italiano y portugués brasileño después de crear una carpeta con la configuración &quot;Contribución de recursos&quot;. Los estilos actualizados dan a las etiquetas traducidas más largas espacio suficiente. (ASSETS-36746)
* Los títulos de columna de la vista de lista de Assets ahora se muestran horizontalmente en la interfaz japonesa. Anteriormente, los títulos aparecían verticalmente en la vista de lista en **Assets** > **Archivos** y en la vista de tarjeta del editor de fragmentos de contenido. El paquete `cq-dam-content` actualizado corrige la dirección del texto. (ASSETS-43105)
* El estado de publicación &quot;Programado para más tarde&quot; en la vista de columna de Assets ahora aparece en el idioma del usuario. Anteriormente, la cadena permanecía en inglés después de que los autores seleccionaran un recurso, eligieran **Administrar publicación**, seleccionaran la opción **Más tarde**, agregaran una fecha y publicaran. El paquete `cq-dam-content` actualizado proporciona las traducciones de todas las configuraciones regionales. (ASSETS-43307)
* Las cadenas de la ficha **Configuración de etiquetas inteligentes** ahora se muestran en su totalidad para francés y portugués brasileño. Anteriormente, el texto se cortaba después de hacer clic en **Crear** en **Herramientas** > **Cloud Services** > **Etiqueta inteligente**. Para leer el texto sin información sobre herramientas, utilice la actualización de CSS que proporciona espacio suficiente. (ASSETS-68045)
* La cadena &quot;Predicado de propiedad de valores de rutas múltiples&quot; en el carril de búsqueda del administrador de Assets ahora se muestra en el idioma del usuario. Anteriormente, la cadena permanecía en inglés cuando los administradores editaban el formulario de búsqueda en **Herramientas** > **General** > **Buscar** formularios y arrastraban el predicado al formulario. El paquete `cq-dam-content` actualizado proporciona las traducciones. (CQ-4336103)
* Las etiquetas Aria de la vista Proyectos ahora se muestran en el idioma del usuario. Anteriormente, el botón Acciones de cada mosaico del proyecto no tenía un nombre accesible y la acción Configurar mosaico utilizaba una etiqueta inglesa predefinida mientras que las etiquetas del mismo nivel se localizaban. El script de mosaico actualizado proporciona una etiqueta localizada para ambas acciones. (CQ-4352359)
* Las colecciones inteligentes con caracteres chinos, japoneses o coreanos en el nombre ahora se guardan correctamente. Anteriormente, al guardar una colección de **Assets** > **Archivos** > **Filter** se producía el error &quot;Error al guardar la búsqueda: solicitud no válida, no se permite la colección duplicada&quot; cuando el nombre contenía caracteres CJK. La comprobación de duplicados ahora compara los títulos de las colecciones en lugar de los nombres de los nodos, por lo que las colecciones con diferentes títulos CJK ya no entran en conflicto. (GRANITE-62592)
* El menú desplegable País o región en **Seguridad** > **Usuarios** > **Crear** ahora ordena los nombres alfabéticamente en el idioma del usuario. Anteriormente, la lista ordenaba los nombres en orden inglés mientras mostraba nombres localizados, por lo que los países aparecían desordenados en configuraciones regionales como el japonés. El paquete `com.adobe.granite.security.content` actualizado ordena con reglas según la configuración regional. (GRANITE-67789)
* La exención de responsabilidad de la tarea de mantenimiento de AuditLog en **Herramientas** > **Operaciones** > **Mantenimiento** ahora se muestra en el idioma del usuario. Anteriormente, la advertencia sobre la depuración de registros de auditoría y los requisitos de cumplimiento permanecían en inglés después de que los usuarios hicieran clic en el icono de exención de responsabilidad en la ventana Mantenimiento semanal. Los recursos actualizados proporcionan la traducción en todas las configuraciones regionales. (NPR-44189)
* Los nombres de permisos en **Security** > **Permissions** > **Audit View** ahora se muestran en el idioma del usuario. Anteriormente, los nombres aparecían en inglés porque faltaban las traducciones. El paquete `com.adobe.granite.platform.i18n` actualizado los suministra. (NPR-44477)
* El cuadro de diálogo Comprobar estado en **Seguridad** > **Configuraciones de Adobe IMS** ahora se muestra en el idioma del usuario. Anteriormente, el cuadro de diálogo mostraba cadenas en inglés en interfaces localizadas porque faltaban las traducciones. El paquete `com.adobe.granite.platform.i18n` actualizado los suministra. (NPR-44479)
* Las cadenas de la herramienta Diagnóstico de sincronización de usuarios en **Herramientas** > **Operaciones** > **Diagnóstico** ahora se muestran en el idioma del usuario. Anteriormente, la herramienta mostraba texto en inglés en interfaces localizadas. El paquete `com.adobe.granite.platform.i18n` actualizado proporciona las traducciones. (NPR-44481)
* Los flujos de configuración ahora muestran mensajes de error descriptivos en el idioma del usuario. Anteriormente, los errores en las páginas de configuración de AEM producían texto técnico o no traducido. El paquete `com.adobe.granite.ui.content` actualizado administra los errores y proporciona mensajes localizados. (NPR-44840)
* El mensaje de error que aparece al cambiar las propiedades de un grupo eliminado en **Seguridad** > **Grupos** ahora se muestra en el idioma del usuario. Anteriormente, el mensaje permanecía en inglés para interfaces localizadas. El paquete `com.adobe.granite.security.content` actualizado proporciona las traducciones. (NPR-44841)
* El mensaje de error &quot;¡Se ha producido un error al guardar los cambios del grupo!&quot; ahora se muestra en el idioma del usuario en la consola **Seguridad** > **Grupos** > **Editar grupo**. Anteriormente, el mensaje permanecía en inglés para interfaces localizadas. El paquete `com.adobe.granite.security.content` actualizado proporciona las traducciones. (NPR-44842)
* Los caracteres chinos, japoneses y coreanos ya no aparecen en cursiva en el mensaje de error del icono de la bandeja de entrada. Anteriormente, el estilo en cursiva distorsionaba los caracteres y dificultaba la lectura del texto. El paquete `com.adobe.granite.ui.coralui3` actualizado quita el estilo para esos idiomas. (NPR-44843)
* Los números de **Operaciones** > **Supervisión** ahora siguen el formato de configuración regional del usuario. Anteriormente, la página mostraba números en un formato fijo independientemente del idioma de la interfaz. El paquete `com.adobe.granite.monitoring.dashboard` actualizado aplica los separadores y el formato correctos. (NPR-44844)
* La pestaña Explicar consulta ahora muestra la &quot;Herramienta de depuración de Query Builder&quot;. en el idioma del usuario. Anteriormente, faltaba el texto del vínculo en las interfaces localizadas porque la cadena no estaba externalizada. El paquete `com.adobe.granite.monitoring.dashboard` actualizado lo restaura. (NPR-44845)
* El texto del cuadro de diálogo de la herramienta de depuración de Query Builder ahora se muestra en el idioma del usuario en la pestaña Explicar consulta. Anteriormente, varias cadenas permanecían en inglés porque no estaban externalizadas. El paquete `cq-platform-content` actualizado proporciona las traducciones. (NPR-44846)
* El texto de la página de resultados de la comprobación de coherencia ahora se muestra en el idioma del usuario. Anteriormente, varias cadenas aparecían en inglés porque no estaban externalizadas. El paquete `com.adobe.granite.operations.ui.core` actualizado proporciona las traducciones. (NPR-44847)
* El gráfico de monitorización ahora muestra las etiquetas de mes y semana en el idioma del usuario. Anteriormente, las etiquetas estaban codificadas en inglés, por lo que el gráfico ignoraba la configuración regional de la interfaz. El paquete `com.adobe.granite.monitoring.dashboard` actualizado externaliza las cadenas y ahora aparecen las traducciones. (NPR-44848)
* El menú desplegable País o región en **Seguridad** > **Usuarios** > **Crear** ahora ordena las entradas correctamente. Anteriormente, los nombres de países localizados aparecían en el orden incorrecto para algunos idiomas. El paquete `com.adobe.granite.security.content` actualizado aplica la ordenación según la configuración regional. (NPR-44942)
* La información del objeto en el cuadro de diálogo del componente Botón ahora se muestra en el idioma del usuario. Anteriormente, el texto de información de los campos Texto de botón, Vínculo, Icono, HTML ID y `aria-label` permanecía en inglés aunque las cadenas existían en el servicio de localización. El diccionario actualizado proporciona las traducciones de todas las configuraciones regionales admitidas. (SITES-7579)
* Ahora, la información del objeto en la sección Propiedades del componente Lista de fragmentos de contenido se muestra en el idioma del usuario. Anteriormente, el texto de información de los campos Modelo de fragmento de contenido, Etiquetas, Número máximo de elementos, Ruta principal, Orden y Ordenar por permanecía en inglés. El diccionario actualizado proporciona traducciones para todas las configuraciones regionales admitidas. (SITES-14969)
* Los vínculos de ayuda para los componentes principales del Editor de plantillas ahora conducen a páginas de documentación localizadas. Anteriormente, al seleccionar Ayuda en el cuadro de diálogo de configuración de componentes, se abría la página en inglés independientemente del idioma de la interfaz. Las direcciones URL actualizadas ahora dirigen a los usuarios a la página para su configuración regional. (SITES-15058)
* La información sobre herramientas del cuadro de diálogo Fragmento de contenido ahora se muestra en el idioma del usuario. Anteriormente, el texto de la información de objeto para los modos Elemento de texto único y Varios elementos y para la ruta del fragmento de contenido permanecía en inglés. Un diccionario actualizado proporciona traducciones para todas las configuraciones regionales. (SITES-17333)
* Los mensajes de error en el editor de la directiva de componentes del editor de plantillas ahora aparecen en el idioma del usuario. Anteriormente, los mensajes &quot;El recurso {} no se puede modificar&quot; y &quot;No se puede crear el nodo en&quot; permanecían en inglés cuando los autores editaban una directiva de componente o creaban una nueva. Los recursos actualizados proporcionan traducciones para todas las configuraciones regionales compatibles. (SITES-17475)
* La pestaña Assets del Editor de páginas ahora muestra una cadena traducida en la lista desplegable Seleccionar componentes después de elegir Párrafos en la lista desplegable Imágenes. Anteriormente, la cadena &quot;OTHER&quot; aparecía en inglés porque los recursos de localización no lo tenían. El diccionario actualizado proporciona la traducción en todas las configuraciones regionales. (SITES-21481)
* La información sobre herramientas de la información del cuadro de diálogo Configurar componente del Editor de páginas ya no muestra un salto de línea adicional. Anteriormente, la información de herramientas de componentes, como el visor de PDF y la barra de progreso, se agrupaba de forma extraña en varias configuraciones regionales. Ahora, la información sobre herramientas se ajusta correctamente y la división de palabras funciona según lo esperado. (SITES-38567)
* La información del objeto &quot;para salir del editor de texto, pulse la tecla Esc&quot; ahora aparece en el idioma del usuario en el cuadro de diálogo de configuración del componente Texto. Anteriormente, la cadena se mostraba en inglés porque los recursos de localización no lo tenían. La información sobre herramientas ahora se traduce en todas las configuraciones regionales. (SITES-43186)
* La etiqueta ESTRUCTURA del Editor de plantillas ahora aparece en el idioma del usuario. Anteriormente, la etiqueta permanecía en inglés cuando los autores abrían una plantilla de formulario adaptable, porque la cadena no aparecía en los recursos de localización. La etiqueta ahora se traduce en todas las configuraciones regionales. (SITES-43599)


#### MSM: Live Copy{#sites-msm-live-copies-6526}

* El cuadro de diálogo Despliegue de MSM carga de nuevo la lista de Live Copy después de una actualización. Anteriormente, un `NullPointerException` de `AsyncOperationServlet.doGet` detuvo el cuadro de diálogo en un control de número, por lo que los autores no pudieron seleccionar configuraciones regionales de destino ni iniciar el despliegue. Un paquete `com.adobe.granite.jobs.async` actualizado administra los datos de trabajo que faltan y finaliza la solicitud. (SITES-43116)
* El despliegue desde la barra de herramientas editable en una página de modelo funciona de nuevo. Error en la acción de la barra de herramientas con &quot;No se pueden leer las propiedades de undefined (reading &#39;doRollout&#39;)&quot; porque la biblioteca de cliente `MSM.Rollout` no se cargó. La página actualizada ahora carga la biblioteca, por lo que el trabajo de despliegue se inicia y los cambios llegan a las Live Copies. (SITES-46052)

* La desactivación por lotes de una página de modelo y sus páginas secundarias ya no envía eventos de despliegue duplicados. Cuando se desactivan un elemento principal y sus elementos secundarios en una solicitud, el sistema de replicación emite cinco eventos en lugar de tres, y cada página secundaria se despliega dos veces. La deduplicación en el administrador de despliegue ahora envía un despliegue por página, por lo que las Live Copies no reciben paquetes redundantes. (SITES-44988)


#### Editor de páginas{#sites-pageeditor-6526}

* El estilo seleccionado permanece resaltado en el cuadro de diálogo de selección de estilos del Editor de páginas después de desplazarse por la lista. Anteriormente, un estilo se resaltaba cuando lo elegía, pero el resaltado desaparecía al hacer clic en la barra de desplazamiento. Esta regresión comenzó después de SP22 y el cuadro de diálogo ahora mantiene visible el estado seleccionado. (SITES-30874)

* Los autores pueden editar páginas en el modo Diseño cuando los componentes principales y secundarios definen diferentes puntos de interrupción adaptables. Anteriormente, la función getResponsiveCssClasses producía un error con TypeError en los componentes que omitían el ancho cq:responsive/phone. La función ahora vuelve a los valores disponibles y continúa el procesamiento. (SITES-46681)
* Las relaciones de recorte personalizadas ahora se cargan en modo de edición en línea híbrido para componentes con varios destinos de colocación de imágenes. Anteriormente, el Editor de imágenes inicializaba un ipeConfig genérico para todos los destinos de colocación, por lo que el editor solo mostraba las relaciones predeterminadas e ignoraba las relaciones de aspecto de cada destino. El editor ahora lee la configuración del destino de colocación seleccionado y el recorte se aplica tanto en vistas en línea como en vistas de pantalla completa. (SITES-45771)
* Al presionar Retroceso en el Editor de texto enriquecido no se agregan estilos en línea adicionales al texto. Un cliente informó que al quitar un salto de línea después de un texto en negrita se agregó style=&quot;font-size: 0.8125rem; background-color: transparent;&quot; a la etiqueta en negrita. No se pudo reproducir el comportamiento al probar el Service Pack más reciente, por lo que no fue necesario realizar ningún cambio. (SITES-15883)


<!--
#### Replication{#sites-replication-6526}
-->


#### Editor de texto enriquecido{#sites-rte-6526}

* Los botones de la barra de herramientas del Editor de texto enriquecido funcionan en la vista adaptable y en el modo Diseño. Anteriormente, los botones se resaltaban al hacer clic, pero la selección permanecía sin cambios y no se abría ningún cuadro de diálogo. El script del editor actualizado aplica el formato, coincidiendo con el comportamiento en el modo de edición. (SITES-44233)
* Los autores pueden agregar símbolos de moneda y marcas comerciales a los componentes de texto sin perderlos. El complemento Caracteres especiales insertaba los símbolos, pero se mostraban como espacios en blanco en el editor y en la salida publicada. La gestión corregida procesa cada símbolo tal como se ha introducido. (SITES-46532)
* El icono Pantalla completa de la barra de herramientas del Editor de texto enriquecido vuelve a expandir el editor. Anteriormente, al hacer clic en el icono del componente Texto principal no se hacía nada y el editor se mantenía en el tamaño en línea. Los autores ahora tienen un espacio de trabajo centrado para el contenido de formulario largo en la edición en línea y en la edición de cuadros de diálogo. (SITES-46396)


#### IU de administración del sitio{#sites-admin-ui-6526}

Al revertir un recurso a una versión anterior, ahora se actualiza la miniatura de su tarjeta. Un cambio en la codificación de la URL en la biblioteca de cliente de la cronología provocaba una discrepancia en la ruta, por lo que la búsqueda de la tarjeta fallaba y la miniatura permanecía obsoleta. La coincidencia de las rutas codificadas y sin procesar restaura la actualización. (SITES-46590)

<!--
#### Universal editor {#sites-universal-editor-6526}
-->

#### Extensiones de flujo de trabajo {#sites-workflow-extensions-6526}

Ver carga útil ahora abre el editor de paquetes de la IU táctil para los flujos de trabajo que Administrar publicación inicia para varias páginas. Anteriormente, la acción abría el editor del paquete de la IU clásica, aunque los autores iniciaban el flujo de trabajo en la IU táctil. Los autores ahora inspeccionan la carga útil sin salir de la IU táctil. (SITES-40928)


### [!DNL Assets] {#assets-6526}

* Mejora: AEM Assets 6.5 incluye compatibilidad con la Coalición para la procedencia y autenticidad de contenido (C2PA) para el contenido de IA generativo. El flujo de trabajo Actualizar recursos detecta las credenciales de C2PA, extrae los metadatos y firma las representaciones que regenera el flujo de trabajo. La firma se ejecuta localmente en cada instancia de AEM, por lo que los clientes no necesitan una infraestructura de firma dedicada. (ASSETS-75868)

* Mejora de la documentación: La nueva documentación pública explica cómo personalizar la canalización de procesamiento de recursos y, al mismo tiempo, mantener el cumplimiento de C2PA. La documentación explica cómo colocar el paso Detectar credencial de C2PA antes de los pasos de representación y cómo la firma se ejecuta localmente en cada instancia de AEM. La documentación también indica la limitación de la infraestructura de firma dedicada o propiedad del cliente. (ASSETS-76100)
* La lista desplegable Ayuda del encabezado del shell ahora permanece abierta cuando pasa el ratón por encima de sus vínculos en entornos de AEM 6.5 SP26. Anteriormente, la lista desplegable se cerraba cuando el puntero entraba en la lista, por lo que los autores no hacían clic en los vínculos Documentación, Comunidad o Asistencia. El paquete `com.adobe.granite.ui.content` actualizado aplaza la comprobación de enfoque, por lo que el menú se cierra únicamente cuando el enfoque realmente se desplaza. (ASSETS-65676)

<!--
#### [!DNL Dynamic Media]{#assets-dm-6526}
-->

### [!DNL Forms]{#forms-6526}

* Nueva función: Compatibilidad con etiquetas de accesibilidad en listas de texto enriquecido. Anteriormente, las etiquetas de lista solo aparecían en el árbol de etiquetas de accesibilidad cuando la plantilla seguía una estructura específica. La solicitud se cerró como duplicado de un ticket relacionado que ofrece la función. (LC-3923202)


<!--
#### Forms JEE {#forms-jee-6526}

#### Forms Designer {#forms-designer-6526}
-->


### Foundation {#foundation-6526}

* La cadena &quot;País o región&quot; en el cuadro de diálogo **Seguridad** > **Usuarios** > **Crear** usuario ahora aparece en el idioma del usuario. Anteriormente, la etiqueta permanecía en inglés para interfaces localizadas. El paquete `com.adobe.granite.security.content` actualizado proporciona las traducciones. (NPR-43882)
* La lista desplegable Ayuda del encabezado del shell ahora permanece abierta cuando pasa el ratón por encima de sus vínculos en entornos de AEM 6.5 SP26. Anteriormente, la lista desplegable se cerraba cuando el puntero entraba en la lista, por lo que los autores no hacían clic en los vínculos Documentación, Comunidad o Asistencia. El paquete `com.adobe.granite.ui.content` actualizado aplaza la comprobación de enfoque, por lo que el menú se cierra únicamente cuando el enfoque realmente se desplaza. (NPR-44686)
* Mejora: La consulta `HtmlLibraryManagerImpl` ahora incluye una etiqueta de tipo de nodo para que la consulta siempre use el índice esperado. El servicio también registra un ERROR cuando no encuentra ninguna biblioteca de cliente, lo que alerta a los administradores del problema. La actualización interrumpe la versión del paquete `com.adobe.granite.clientlibs` en el Service Pack. (NPR-44698)


<!--
#### Apache Felix {#foundation-apachefelix-6526}
-->


#### Autenticación {#foundation-authentication-6526}

Guardar y cerrar en el editor de usuarios ahora vuelve a los resultados de búsqueda de la búsqueda actual. Anteriormente, después de que los autores buscaran un segundo usuario en Omnisearch, editaran las propiedades y hicieran clic en Guardar y cerrar, la página abría las propiedades del primer usuario en su lugar. El script UserProperties.js actualizado restaura la navegación esperada. (NPR-44774)

<!--
#### Campaign{#foundation-campaign-6526}

#### Cloud Services{#foundation-cloudservices-6526}

#### Communities {#foundation-communities-6526}

#### Content distribution{#foundation-content-distribution-6526}

#### Adobe CRX {#foundation-crx-6526}
-->


#### Granite{#foundation-granite-6526}

* El marcador de posición &quot;Modelo de fragmento de contenido&quot; en el filtro Omnisearch de Assets ahora se muestra en su totalidad. Anteriormente, el texto se cortaba después de ir a Assets, hacer clic en el icono Filtros o Buscar y expandir el campo Modelo de fragmento de contenido. El estilo actualizado proporciona al marcador de posición espacio suficiente. (GRANITE-54387)
* El menú desplegable Ayuda en el encabezado del shell ahora permanece abierto cuando mueve el puntero sobre sus vínculos. Anteriormente, la lista desplegable se cerraba en cuanto el puntero entraba en la lista de vínculos de documentación, comunidad y soporte técnico, lo que hacía que no se pudiera acceder a los vínculos con un ratón. El controlador de enfoque ahora aplaza la comprobación al siguiente fotograma de animación, por lo que el desplazamiento ya no cuenta como el enfoque que sale del menú. (GRANITE-70978)

<!--
#### Jetty{#foundation-jetty-6526}
-->

#### Integraciones de Launch{#foundation-launch-integrations-6526}

Mejora: La integración de Adobe Analytics con Adobe Experience Manager Launch utiliza la API de Analytics 2.0. La API de Analytics 1.4 llega al final de su vida útil el 31 de agosto de 2026. La migración mantiene el funcionamiento de las integraciones de informes y Launch después de esa fecha. (CQ-4365074, CQ-4365080)

<!--
#### Localization{#foundation-localization-6526}

#### Oak {#foundation-oak-6526}
-->

#### Plataforma{#foundation-platform-6526}

* El vínculo de Ayuda situado en el pie de página de la página de inicio de sesión de AEM ahora abre una página de trabajo. Anteriormente, el vínculo apuntaba a una dirección URL de marketing.adobe.com que ya no existe. La configuración del pie de página ahora usa la URL [Adobe Experience Manager documentation](https://experienceleague.adobe.com/en/docs/experience-manager). (NPR-44388)
* Mejora: Una solicitud del cliente pedía la API de Microsoft Graph como alternativa a SMTP cuando AEM envía correos electrónicos. El ticket se ha resuelto como duplicado porque otro ticket ya implementa el flujo de API de Graph. SMTP con OAuth 2.0 sigue estando disponible para los clientes que necesitan dejar de utilizar la autenticación básica SMTP. (GRANITE-57478)

* Las cadenas del cuadro de diálogo Permisos efectivos ahora se alinean correctamente en **Herramientas** > **General** > Explorador **Configuración**. Anteriormente, se mostraba una cadena sin conexión después de seleccionar una carpeta, hacer clic en Propiedades y hacer clic en Permisos efectivos. Las reglas de diseño actualizadas restauran la alineación. (CQ-4359166)


#### Proyectos {#foundation-projects-6526}

La cadena &quot;Seleccionar directorio raíz&quot; del cuadro de diálogo Seleccionar diccionario i18n ahora se muestra en su totalidad. Anteriormente, el texto se cortaba en varias interfaces localizadas después de crear un proyecto de traducción y agregar un diccionario i18n. El paquete `cq-projects-translation-content` actualizado proporciona suficiente espacio a la cadena. (CQ-4355405)

<!--
#### Security{#foundation-security-6526}

#### Sling{#foundation-sling-6526}

#### SPA editor {#foundation-spa-editor-6526}
-->


#### Traducción{#foundation-translation-6526}

Las opciones de estilo del componente Lista ahora se muestran en el idioma del usuario. Anteriormente, cadenas como Bloque y Cuadrícula permanecían en inglés en el menú Estilos después de que los autores agregaran el componente Lista a un fragmento de experiencia. Los recursos actualizados proporcionan las traducciones, incluidas las interfaces en coreano, chino simplificado y chino tradicional. (CQ-4349666)

<!--
#### User interface{#foundation-ui-6526}

#### WCM{#foundation-wcm-6526}
-->

#### Flujo de trabajo{#foundation-workflow-6526}

Mejora: El editor de páginas de IU táctil ahora procesa el árbol de contenido y admite la edición de componentes de definición de recursos en páginas de paquetes de flujo de trabajo. Anteriormente, las páginas de `/etc/workflow/packages/` que **Administrar publicación** > **Publicar posteriormente** creaba no mostraban ningún árbol de contenido en el panel izquierdo y los autores no podían editar los componentes de Definición de recurso. Los aprobadores ahora inspeccionan páginas y recursos dentro de una carga útil de flujo de trabajo en la IU táctil, según el comportamiento de la IU clásica. (GRANITE-65620)

## Instalación de [!DNL Experience Manager] 6.5.26.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.26.0 requiere [!DNL Experience Manager] 6.5. Consulte [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del Service Pack está disponible en [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip) de Adobe.
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.26.0 en una de las instancias de autor mediante el administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe recomienda no quitar ni desinstalar el paquete [!DNL Experience Manager] 6.5.26.0. Para revertir si es necesario, cree una copia de seguridad de `crx-repository` antes de instalar el paquete. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Instalar el Service Pack en [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie la instancia antes de la instalación si está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de realizar la instalación, realice una instantánea o una copia de seguridad nueva de la instancia de [!DNL Experience Manager].

1. Descargar el Service Pack desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de la instalación del Service Pack, sustituya el conector existente por un nuevo archivo binario, proporcionado en la carpeta de instalación, y reinicie la instancia. Consulte [Almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo de la interfaz de usuario del administrador de paquetes a veces se cierra durante la instalación del paquete de servicio. Adobe recomienda esperar a que los registros de errores dejen de cambiar antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de confirmar que la instalación se ha realizado correctamente. Este problema se produce en el explorador [!DNL Safari], pero puede ocurrir ocasionalmente en cualquier explorador.

**Instalación automática**

Existen dos métodos diferentes que puede utilizar para instalar [!DNL Experience Manager] 6.5.26.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en la carpeta `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.
* Use la [API HTTP del administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que se instalen los paquetes anidados.

>[!NOTE]
>
>Experience Manager 6.5.26.0 no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validación de la instalación**

Para las plataformas que están certificadas para trabajar con esta versión, vea los [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.26.0)` en [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos los paquetes OSGi tienen el valor **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es de la versión 1.22.20 o posterior (utilice la consola web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Instalar Service Pack para [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obtener instrucciones para instalar el Service Pack en Experience Manager Forms, consulte [Instrucciones de instalación del Service Pack de Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funcionalidad Formularios adaptables, disponible en [AEM 6.5 Inicio rápido](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), está diseñada únicamente para la exploración y la evaluación. Para su uso en producción, es esencial obtener una licencia válida para AEM Forms, ya que la funcionalidad Formularios adaptables requiere una licencia adecuada.

### Instalación del paquete de índice de GraphQL para fragmentos de contenido de Experience Manager{#install-aem-graphql-index-add-on-package}

Los clientes que usen GraphQL deben instalar el [fragmento de contenido de Experience Manager con el paquete de índice 1.1.1 de GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Esto permite añadir la definición de índice necesaria en función de las funciones utilizadas.

Si no se instala este paquete, las consultas de GraphQL serán lentas o fallidas.

>[!NOTE]
>
>Instale este paquete solo una vez por instancia; no es necesario reinstalarlo con cada Service Pack.

### UberJar{#uber-jar}

UberJar para [!DNL Experience Manager] 6.5.26.0 está disponible en el [repositorio de Maven Central](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.26/). <!-- CHECK FOR UPDATE EACH NEW RELEASE FROM MADHULIKA SINGH -->

Para utilizar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.26</version>
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

  1. Instalar el Service Pack o reiniciar Experience Manager as a Cloud Service.
     Las nuevas carpetas para `cache` y `diff-cache` se crean automáticamente y ya no experimenta una excepción relacionada con `mvstore` en `error.log`.

* Actualice las consultas de GraphQL que utilizaron un nombre de API personalizado para el modelo de contenido para utilizar el nombre predeterminado del modelo de contenido en su lugar.

* Una consulta de GraphQL utiliza el índice `damAssetLucene` en lugar del índice `fragments`. Esta acción provoca consultas de GraphQL que fallan o tardan mucho tiempo en ejecutarse.

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

  Después de estos pasos, las consultas de GraphQL funcionan con una velocidad mejorada.

* Al intentar mover, eliminar o publicar fragmentos de contenido, sitios o páginas, hay un problema cuando se recuperan las referencias de fragmentos de contenido. La consulta en segundo plano falla; la funcionalidad no funciona.
Para garantizar el funcionamiento correcto, debe añadir las siguientes propiedades al nodo de definición de índice `/oak:index/damAssetLucene` (no se requiere la reindexación):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si actualiza la instancia de [!DNL Experience Manager] de la versión 6.5.0-6.5.4 al Service Pack más reciente de Java™ 11, verá excepciones `RRD4JReporter` en el archivo `error.log`. Para detener las excepciones, reinicie la instancia de [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Los usuarios pueden cambiar el nombre de una carpeta en [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Durante la instalación de [!DNL Experience Manager] 6.5.x.x aparecen los siguientes errores y mensajes de advertencia:
  * “Cuando la integración de Adobe Target se configura en [!DNL Experience Manager] mediante la API de Target Standard (autenticación IMS) y, a continuación, se exportan fragmentos de experiencias a Target, se crean tipos de ofertas incorrectos. En lugar de “Experience Fragment”/source “Adobe Experience Manager”, Target crea varias ofertas con el tipo “HTML”/source “Adobe Target Classic”.
  * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en `granite/operations/maintenance`.
  * La validación del lado del servidor de formularios adaptables falla cuando se utilizan funciones de agregado como SUM, MAX y MIN (CQ-4274424).
  * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en `granite/operations/maintenance`.
  * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al previsualizar el recurso a través del visor de banners a la venta.
  * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`: tiempo de espera agotado para completar el cambio de registro sin registrar.

* A partir de AEM 6.5.15, el motor Rhino JavaScript proporcionado por el paquete `org.apache.servicemix.bundles.rhino` presenta un nuevo comportamiento de hoisting. Los scripts que utilizan el modo estricto (`use strict;`) deben declarar sus variables correctas. De lo contrario, no se ejecutan y terminan generando un error de tiempo de ejecución.

* La instalación del contenido estándar relacionado con el etiquetado mediante un paquete de actualización oficial restablece la propiedad de idiomas del nodo `/content/cq:tags` al valor predeterminado. Esta acción se aplica a los paquetes de servicio, los paquetes de servicio de seguridad, los paquetes de funciones ampliadas, los paquetes de funciones acumulativas, los parches, etc. Por lo tanto, es necesario agregarlo a las propiedades antes de la instalación.

### Problema conocido de AEM Sites {#known-issues-aem-sites-6526}

* **Problema conocido con una revisión disponible para AEM Foundation**

  Después de actualizar desde un Service Pack anterior a Experience Manager 6.5.26.0, el pedido de versiones del paquete de CRXDE Lite puede impedir que Experience Manager seleccione el paquete deseado. Para corregir el pedido de la versión, instale Service Pack 26 y, a continuación, descargue e instale la revisión [`CRXDE Lite hotfix GRANITE-76725`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq660%2Fhotfixes%2Fgranite-76725%2Fcq-6.5.26-hotfix-GRANITE-76725-1.0.zip) desde Distribución de software. La revisión es una actualización de solo versión. No contiene código ni cambios funcionales. (GRANITE-76725)

* Fragmentos de contenido: la previsualización falla debido a la protección DoS para un gran árbol de fragmentos. Consulte el [artículo de KB sobre las opciones de configuración predeterminadas del ejecutor de consultas de GraphQL](https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)

### Problemas conocidos de AEM Forms {#known-issues-aem-forms-6526}

* Cuando un formulario que contiene un campo de **Archivo adjunto** que utiliza `bindref` se envía a un flujo de trabajo de AEM con un paso de **Asignar tarea**, no se muestran los archivos adjuntos. Como resultado, no aparecen cuando la tarea se abre desde la Bandeja de entrada. Los archivos se guardan correctamente en el repositorio, pero la interfaz de usuario del paso Asignar tarea no muestra los archivos adjuntos. (FORMS-23722)

* Cuando se adjunta un PDF firmado digitalmente a una tarea en AEM Forms JEE Workspace, la carga permanece atascada en el estado de carga o falla con un error de &quot;Archivo no válido&quot;. Como resultado, no se pueden agregar a la tarea archivos adjuntos de PDF más grandes y firmados. Este problema se corrigió en una versión posterior. Para obtener una revisión de la versión, póngase en contacto con el Soporte técnico de Adobe. (FORMS-28517)

#### Problemas conocidos con revisiones disponibles {#aem-forms-issues-with-hotfixes}

Los siguientes problemas incluyen una revisión disponible para su descarga e instalación. Puede [descargar e instalar la revisión](/help/release-notes/aem-forms-hotfix.md) para resolver los siguientes problemas:

* Después de instalar AEM Forms JEE Service Pack 21 (6.5.21.0), si encuentra entradas duplicadas de Jars Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` en la carpeta `<AEM_Forms_Installation>/lib/caching/lib`, realice los siguientes pasos para resolver el problema (FORMS-14926):

  1. Detenga los localizadores, si están en funcionamiento.
  1. Detenga el servidor de AEM.
  1. Ir a `<AEM_Forms_Installation>/lib/caching/lib`.
  1. Quite todos los archivos de parche de Geode, excepto `geode-*-1.15.1.2.jar`. Confirme que solo están presentes los Jars Geode con `version 1.15.1.2`.
  1. Abra el símbolo del sistema en modo de administración.
  1. Instale el parche de Geode mediante el archivo `geode-*-1.15.1.2.jar`.

## Paquetes de contenido y paquetes OSGi incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes archivos zip contienen los documentos de texto que enumeran los paquetes OSGi y los paquetes de contenido incluidos en esta versión del paquete de servicio [!DNL Experience Manager] 6.5:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.26.0](/help/release-notes/assets/65260-bundles.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.26.0](/help/release-notes/assets/65260-packages.zip)
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




