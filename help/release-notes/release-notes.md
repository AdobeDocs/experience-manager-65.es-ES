---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6.5
description: Encuentra información de la versión, novedades, instrucciones de instalación y una lista detallada de cambios para  [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 07f45107bceee9e793a39f4167985da91fb51e4a
workflow-type: tm+mt
source-wordcount: '6161'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager] 6.5 Últimas notas de la versión del paquete de servicio {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.22.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión del paquete de servicio |
| Fecha | Jueves, 21 de noviembre de 2024 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Qué se incluye en [!DNL Experience Manager] 6.5.22.0 {#what-is-included-in-aem-6522}

[!DNL Experience Manager] 6.5.22.0 incluye nuevas características, mejoras clave solicitadas por el cliente y correcciones de errores. También incluye mejoras de rendimiento, estabilidad y seguridad publicadas desde el lanzamiento inicial de la versión 6.5 en abril de 2019. [Instalar este Service Pack](#install) en [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## Funciones principales y mejoras

### Formularios {#forms-sp22}

Las funciones y mejoras clave de esta versión son las siguientes:

#### Nuevas funciones de GA en AEM Forms {#ga-aem-forms-sp22}

* Se ha agregado compatibilidad para habilitar la incrustación de fuentes en las [API por lotes de comunicaciones interactivas](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel). Las comunicaciones interactivas ahora admiten la incrustación de fuentes Adobe Ming y Adobe Myungjo en archivos PDF generados mediante la API por lotes. Esta mejora garantiza una representación precisa del texto en los documentos generados, incluso cuando se utilizan subconjuntos de fuentes, lo que proporciona una compatibilidad mejorada con el contenido multilingüe en las salidas de PDF.

* [Tabla de API de contenido para accesibilidad de PDF](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api): AEM Forms en OSGi ahora es compatible con la nueva API de etiquetas de TDC para mejorar PDF en cuanto a estándares de accesibilidad. Hace que los archivos PDF sean más accesibles para los usuarios con tecnología de asistencia.

* [Resolución XDP del fragmento](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository): AEM Forms en OSGi ahora resuelve los XDP del fragmento a los que se hace referencia en los XDP principales y se almacenan en el repositorio de CRX de AEM.

* [Mejoras en el cumplimiento de PDF/A](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents): Ahora los usuarios pueden convertir archivos PDF a formatos PDF/A (1a, 2a, 3a) para fines de archivo, al tiempo que garantizan la accesibilidad y verifican el cumplimiento de estos estándares.

* **Compatibilidad con el cambio de tamaño automático de la fuente para documentos estáticos de PDF**: AEM Forms Designer, OutputService y FormsService ahora admiten el cambio de tamaño automático de fuentes para PDF estáticos. Si el usuario establece el tamaño de fuente 0 para los campos de texto, numéricos, de contraseña o de fecha y hora, el tamaño de fuente se ajusta automáticamente dentro de estos campos sin alterar el tamaño general del campo. Para utilizar la función, los usuarios pasan un indicador en el XCI personalizado: `<behaviorOverride>patch-LC-3921991:1</behaviorOverride>`.

#### Nuevas funciones de Beta en AEM Forms {#beta-aem-forms-sp22}

La función beta ofrece una oportunidad única para obtener acceso exclusivo a innovaciones de vanguardia y ayudar a dar forma a su desarrollo. ¿Quiere activar una función beta para sus entornos? Envíe un correo electrónico desde su dirección oficial a aem-forms-ea@adobe.com con la lista de funciones que le interesan.

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md) y [servicios de CAPTCHA de torniquete de Cloudflare](/help/forms/using/integrate-adaptive-forms-turnstile.md): AEM Forms admite los siguientes servicios de Captcha:
   * Captcha protege los formularios de bots, spam y abusos automatizados al desafiar a los usuarios con un widget de casilla de verificación. Garantiza que solo los usuarios humanos procedan, mejorando la seguridad de las transacciones en línea.
   * Cloudflare Turnstile ofrece una medida de seguridad que tiene como objetivo proteger los formularios de bots automatizados, ataques maliciosos, spam y tráfico automatizado no deseado. Presenta una casilla de verificación en el envío del formulario para verificar que son humanos, antes de permitirles enviar el formulario.

* Versiones de formulario adaptable:
   * [Crear varias versiones de un formulario adaptable](/help/forms/using/add-versioning-reviews-comments.md): Ahora los usuarios pueden administrar fácilmente las variaciones de los formularios existentes. Este proceso simplifica el control de versiones y facilita la comparación para la optimización de formularios, todo ello dentro de un único flujo de trabajo optimizado.
   * [Comparar Forms adaptable](/help/forms/using/compare-forms-core-components.md): Ahora los usuarios pueden comparar fácilmente dos formularios para identificar diferencias. Facilita una colaboración fluida ya que permite a los miembros del equipo comparar revisiones y discutir cambios de forma eficaz.

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

### Sites {#sites}

[El editor universal](/help/sites-developing/universal-editor/introduction.md) ya está disponible en AEM 6.5 para casos de uso remoto con la aplicación de un paquete de funciones.

### [!DNL Assets]

La pestaña IPTC ahora admite los campos de texto [!UICONTROL Texto alternativo] y [!UICONTROL Descripción extendida]. (ASSETS-34918)

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Se han corregido problemas en el Service Pack 22 {#fixed-issues}


### [!DNL Sites]{#sites-6522}


#### Accesibilidad {#sites-accessibility-6522}

* Faltaba un nombre accesible en el botón del selector de muestras de anotación. Es decir, con un lector de pantalla, no hay ningún nombre comprensible para que el botón seleccione después de introducir un nuevo valor hexadecimal. (SITES-11992)
* Los siguientes elementos del menú del carril izquierdo aparecen como una lista, pero no están marcados como tales en el lector de pantalla:

   * Sitio
   * Live Copy
   * Iniciar
   * Copia de idioma
   * Carpeta
   * Informe CSV (SITES-2874)

* La Administración de contenido web principal de AEM requiere una etiqueta de accesibilidad para los hipervínculos en el Editor de texto enriquecido. Cuando se utiliza un hipervínculo en el componente de texto, la etiqueta de anclaje debe incluir el atributo `aria-label` para garantizar que los lectores de pantalla puedan leer y transmitir el texto del vínculo con precisión por motivos de accesibilidad. (SITES-11511)
* En AEM, los elementos interactivos del encabezado de tabla de la vista de lista no tienen la función de &quot;botón&quot; requerida. Como tal, el lector de pantalla NVDA no anuncia las funciones de botón esperadas para los siguientes encabezados de tabla: Título, Nombre, Modificado, Publicado, Vista previa, Plantilla, Operación, Flujo de trabajo. A cada elemento interactivo del encabezado de la tabla se le debe asignar una función de &quot;botón&quot; para garantizar la compatibilidad con tecnologías de asistencia como NVDA. (SITES-10962)


#### Interfaz de usuario de administrador{#sites-adminui-6522}

* En algunos casos de AEM, las funcionalidades de vista previa y comparación de versiones no funcionaban según lo esperado en varias páginas. Específicamente:

   * **Problema de vista previa:** Al intentar obtener una vista previa de la versión de una página, aparece inicialmente un error. Después de volver a intentarlo, la vista previa genera una página en blanco.
   * **Problema de comparación de versiones:** La característica &quot;Comparar con actual&quot; sólo mostraba la versión actual, sin resaltar las diferencias entre versiones. (SITES-23988)

* Aparece una etiqueta `<br>` inesperada en el campo Editor de texto enriquecido (RTE) al utilizar `defaultPasteMode` establecido en `plaintext` durante una acción de copiar y pegar. Este problema causa un marcado diferente para el mismo contenido, lo que da como resultado que el mismo contenido de texto se traduzca dos veces en la memoria de traducción de un cliente. (SITES-23606)
* En AEM 6.5.20.0, se encontró un problema de funcionalidad con la característica **Administrar publicación**. Al seleccionar un nodo y programarlo para su publicación futura, podría aparecer un mensaje de error &quot;Error al recuperar los recursos secundarios de los elementos seleccionados&quot; al intentar incluir nodos secundarios. Este problema bloqueaba el uso de la opción **Incluir elementos secundarios**, lo que impedía la publicación completa de la jerarquía de contenido deseada. (SITES-23000)
* La marca de tiempo &quot;Publicado&quot; de una plantilla no se actualizaba en el entorno de creación, aunque la plantilla se replicara correctamente en las instancias de publicación. El comportamiento esperado era que la marca de tiempo de la instancia de autor reflejara la última publicación, pero esta actualización no se estaba produciendo según lo previsto. (SITES-21585)
* Se ha producido una discrepancia en el recuento de vínculos entrantes en el entorno de creación de AEM. El carril izquierdo mostraba menos vínculos en comparación con la IU clásica. Además, algunos vínculos entrantes legítimos no funcionan. (SITES-24837)
* Se comunicaban tiempos de carga extremadamente largos al ver las versiones de la página en la vista Cronología de AEM. Se tardaba hasta 19 minutos en mostrar las versiones. Este problema continuaba desde la actualización de AEM 6.4.8 a 6.5.18, lo que afectaba significativamente a la eficacia del flujo de trabajo. (SITES-22468 Y SITES-22467)

<!-- #### Classic UI{#sites-classicui-6522} 

* A -->


#### [!DNL Content Fragments]{#sites-contentfragments-6522}

* En la versión actualizada de AEM 6.5.17, al guardar los fragmentos de contenido, se produjo el siguiente error: *ERROR: No se pudo guardar el fragmento de contenido.* (SITES-22993)
* Se identificó un problema con una resolución de recursos sin cerrar en `ContentFragmentModelOmniSearchHandler` en el editor de AEM. (SITES-24903)


#### [!DNL Content Fragments] - Administrador{#sites-admin-6522}

Al hacer clic en el vínculo en la notificación por correo electrónico, se dirige al usuario al visor o editor de recursos predeterminado. Lo hace en lugar del editor de fragmentos de contenido, incluso cuando el recurso del flujo de trabajo está determinado como un fragmento de contenido. (SITES-24338)


#### [!DNL Content Fragments] - API de GraphQL {#sites-graphql-api-6522}

Al utilizar fragmentos de contenido con elementos de campo de texto multilínea, el marcado generado al consultar con GraphQL no conservaba el formato especificado en HTML. Por ejemplo, faltaba una nueva línea después de la lista. Esto tuvo como consecuencia que el último párrafo pasara a formar parte de la lista. (SITES-23233)


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6522}

* A


#### [!DNL Content Fragments] - REST API{#sites-restapi-6522}

* A -->

#### Servidor principal{#sites-core-backend-6522}

* Se notificaron `SegmentNotFoundException` errores recurrentes en una instancia de autor de AEM. Al reiniciar el autor, se resolvió temporalmente el problema, pero se necesitaba una corrección a largo plazo para evitar que se produjeran más casos. (SITES-22573)
* Se planteó un problema con respecto a la funcionalidad de la cronología en AEM Sites, específicamente en relación con la administración de las propiedades de `cq:lastModified` que faltan en las anotaciones. Después de aplicar AEM 6.5.20, había incertidumbre sobre si el contenido existente necesitaba una corrección para la propiedad que faltaba o si la cronología se actualizaba para funcionar correctamente sin él. (SITES-21861)


#### Componentes principales{#sites-core-components-6522}

* Después de una actualización de AEM 6.5.18 a 6.5.21, se identificó un problema con la funcionalidad que comprueba el uso activo de los componentes. Al intentar desplazarse para obtener elementos adicionales en la página Uso de Live, la tabla no cargaba más resultados a pesar de que se veía &quot;Cargando más elementos&quot; en la interfaz de usuario. (SITES-23919)
* Se ha notificado un problema con la validación de campos obligatorios en un cuadro de diálogo de componentes de AEM que contenía dos pestañas. La pestaña 1 incluía un Editor de texto enriquecido (RTE) y campos de texto, mientras que la pestaña 2 tenía campos de ruta y campos de texto. Aunque todos los campos están marcados como obligatorios (`required=true`), las notificaciones de error persisten incorrectamente en la ficha 1, incluso después de rellenar todos los campos obligatorios. Por el contrario, los errores de la pestaña 2 se borran según lo esperado. (SITES-23243)
* Después de migrar a AEM 6.5.21, la instrucción de lenguaje de plantilla de HTML `data-sly-include` ya no funcionaba como se esperaba, específicamente no admitía expresiones `appendPath` y `prependPath`. Como resultado, el resultado del recurso incluido no se representó correctamente, aunque funcionaba correctamente antes de la migración. Este problema provocaba errores de procesamiento en los recursos que dependen de estas expresiones para la manipulación de rutas. (GRANITE-52970)


<!-- #### Campaign integration{#sites-campaign-integration-6522}

* A -->


#### Fragmentos de experiencias{#sites-experiencefragments-6522}

* Los fragmentos de experiencias no se ordenan por título como se esperaba cuando se hace clic en el encabezado de columna **Title** en la vista de lista. Se observa un parpadeo rápido en la pantalla, pero no se ordena. (SITES-23706)

* En AEM 6.5.17, se ha producido un problema al convertir un componente de página en un fragmento de experiencia mediante la función predeterminada. Después de la conversión, el fragmento de experiencia aparecía vacío durante la edición, a pesar de mostrarse correctamente en la página en la que se utilizó. El problema se debía a una creación de nodo incorrecta: el nodo de componente se colocaba fuera del nodo raíz/contenedor, violando la estructura de la plantilla. Necesitaba mover manualmente el nodo de componente al nodo raíz/contenedor correcto para restaurar la editabilidad del fragmento. (SITES-22974)

* Después de migrar de AEM 6.5.11 a 6.5.20, las configuraciones en la nube en los fragmentos de experiencias no se guardaban correctamente. Aunque las configuraciones parecían guardarse en `crx/de`, no se mostraban al volver a abrir la consola de configuraciones, lo que indica un problema de persistencia. (SITES-22287)


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6522}

* A -->


#### Lanzamientos{#sites-launches-6522}

Al agregar recursos del fragmento de experiencia usando el filtro de etiquetado en la producción de AEM, el usuario podía seleccionarlo, pero luego encontró un error después de seleccionar **Crear copia de idioma**. El comportamiento esperado era que el recurso de fragmento de experiencia seleccionado del filtro de etiquetado se suponía que se agregaría al proyecto de traducción. (SITES-24152)

#### Verificador de vínculos{#sites-link-checker-6522}

LinkCheckerTask no puede autenticarse porque el cliente HTTP intenta NTLM antes de la autenticación básica, lo que provoca que el proxy bloquee a los usuarios después de varios intentos fallidos. En su lugar, el sistema debe utilizar la autenticación básica para autenticarse con el proxy, lo que permite que los servicios LinkCheckerTask funcionen correctamente. (SITES-25034)


#### MSM: Live Copies{#sites-msm-live-copies-6522}

* Cuando se aplican etiquetas SEO Robots a la copia principal y se despliegan en páginas de Live Copy, los valores aparecían correctamente en `crx/de`. Sin embargo, los valores no se reflejaban en la interfaz de usuario en Propiedades de página de las páginas de Live Copy. (SITES-23475)
* Los errores relacionados con los lanzamientos aparecían cuando se intentaba promocionar un lanzamiento a través de la interfaz de usuario. El asistente Promocionar lanzamiento permanecía vacío, lo que impedía completar el proceso de promoción. (SITES-19718)
* Se han producido problemas con los fragmentos de experiencias en AEM tras varios intentos de crear Live Copies y realizar despliegues. El problema se produjo cuando los usuarios encontraron un error de `NotFound` al intentar volver a la pantalla de administración de Fragmentos de experiencias desde la pantalla de Despliegue. (SITES-21933)


#### Editor de página{#sites-pageeditor-6522}

* El botón Deshacer cambió la posición del componente además de cambiar el texto a la última versión. (SITES-17465)
* Cuando se pegaba un componente de contenedor copiado, aparecía visualmente dos veces, lo que daba como resultado tres instancias en la página. Sin embargo, después de actualizar la página, el duplicado desapareció, lo que sugiere que el problema era probablemente un error visual temporal. (SITES-21890)
* Al navegar por el panel izquierdo Componentes con las teclas Tab o Mayús+Tab del teclado, varios elementos de texto no estaban claramente visibles, tanto visualmente como en el modo de pestaña. Este problema afectaba a la accesibilidad, lo que dificultaba la identificación o interacción con estos componentes durante la navegación mediante el teclado. (SITES-2266)

#### Replicación{#sites-replication-6522}

En AEM 6.5.18 y 6.5.19, al desactivar una página principal, se generaban varias solicitudes de desactivación para cada página secundaria. Este problema también provocó la cancelación masiva de la publicación de los extremos de GraphQL. (NPR-42075 Y NPR42010)


### [!DNL Assets]{#assets-6522}

* Al utilizar la función Assets conectado, las actualizaciones realizadas en AEM Assets no se reflejan en el entorno de AEM Sites. (ASSETS-42344)
* Problemas con el estado de publicación de recursos al mover recursos de una ubicación a otra en Experience Manager. (ASSETS-41158)
* La carga de recursos mediante la API genera `unclosed resource resolver` mensaje de error. (ASSETS-41049)
* Problemas con la consulta de referencia `AssetReferenceResolverImpl` después de actualizar a Adobe Experience Manager, Service Pack 21. (ASSETS-40384)
* En la versión 6.5.19 de AEM, al eliminar una opción de los resultados del panel de búsqueda, también desmarca todas las demás casillas de verificación disponibles. (ASSETS-37335)
* Los valores no deseados se muestran en la salida de Excel mientras se realiza la operación de exportación masiva de metadatos. (ASSETS-37260)
* En la versión 6.5.19 de AEM, cuando se carga un archivo SVG en formato UTF-8, el resultado es borroso. (ASSETS-36616)
* Falta la opción `Fetch original rendition for Dynamic Media Connected Assets` en la configuración de Assets conectado. (ASSETS-41726)
* Las propiedades de recurso se guardan incluso si no se define un valor para los campos obligatorios. (ASSETS-37914)
* Si el estado de procesamiento de un recurso es Error o Error de metadatos, la IU de los subtítulos y las pistas de audio no funciona correctamente. (ASSETS-37281)
* Al guardar los metadatos de un recurso e intentar editarlos, no se muestra el nombre del idioma. (ASSETS-37281)

#### [!DNL Dynamic Media]{#assets-dm-6522}

Un problema de producción interrumpió el proceso de migración cuando se producía un error en la carga de vídeo a Dynamic Media, que mostraba un error de error de proceso en la interfaz de usuario. (ASSETS-36038)

<!--

### [!DNL Forms]{#forms-6522}

Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.22.0 Forms add-on package release is scheduled for Thursday, November 28, 2024. A list of Forms fixes and enhancements is added to this section post the release.

-->

### Formularios {#forms-bug-fixes-sp22}

* Las direcciones URL generadas para los archivos adjuntos en los borradores guardados en AEM Forms no reflejan las asignaciones configuradas de Apache Sling Resource Resolver Factory. (FORMS-16949)
* Cuando un usuario del Service Pack 19 de AEM Forms (6.5.19.0) obtiene una vista previa de una carta, el contenido no se alinea correctamente, ya que los espacios parecen no estar y el carácter `x` aparece en algunas ubicaciones. (FORMS-16670)
* Cuando un usuario que usa AEM Forms Service Pack 18 (6.5.18.0) intenta imprimir los archivos mediante el protocolo CIFS, se produce el siguiente error: (FORMS-16629)
  `ALC-OUT-001-401: Unknown error while printing using CIFS on the Printer: \\\\\\\\NSMVPLUETEST01\\\\TH_Test`.
* Cuando un usuario actualiza del paquete de servicio 17 de AEM Forms (6.5.17.0) al paquete de servicio 20 de AEM Forms (6.5.20.0), el icono del editor de reglas no aparece en el nivel del contenedor de formularios. (FORMS-16430)
* Cuando un usuario actualiza del paquete de servicio 17 de AEM Forms (6.5.17.0) al paquete de servicio 21 de AEM Forms (6.5.21.0), la ruta de URL de envío del formulario adaptable modificado no funciona. (FORMS15894)
* En AEM Forms Service Pack 19 (6.5.19.0), la validación de AEM Forms 6.5 PDF/A falla en determinados archivos con el error `creation date and modification date mismatch with timezone`, mientras que se ejecuta sin problemas en la validación de Acrobat Pro PDF/A para una comprobación de compatibilidad. (FORMS-15840)
* Cuando un usuario elimina borradores de formularios utilizando el componente &quot;Borradores y envíos&quot; en una página de sitio del paquete de servicio 15 de AEM Forms (6.5.15.0) en OSGi, se produce un error en la eliminación. (FORMS-15755)
* Cuando un usuario tiene una lista de SharePoint con más de 999 entradas y el formulario incluye un archivo adjunto, el envío del formulario falla. (FORMS-15057)
* Se agrega una regla de validación para garantizar que la fecha de finalización no sea anterior a la fecha de inicio, junto con una secuencia de comandos personalizada para el mensaje de validación. Sin embargo, la validación no entra en déclencheur cuando la fecha de finalización es anterior a la fecha de inicio. (FORMS-14757)
* Cuando un usuario utiliza la funcionalidad de mostrar/ocultar en una tabla de un formulario adaptable, el tamaño del campo se reduce. El tamaño del campo se corrige al agregar y quitar una fila. (FORMS-14756)
* Cuando un usuario imprime formularios en AEM Forms Service Pack 19 (6.5.19.0), algunos formularios no se representan correctamente en el servidor, lo que provoca errores durante el proceso de impresión. (FORMS14734)
* Cuando un usuario actualiza del Service Pack 15 (6.5.15.0) de AEM Forms al Service Pack 19 (6.5.19.0), se produce un problema. Un patrón de visualización personalizado establecido como `num{$zzz,zz9.99}` no se representa correctamente en la vista previa y la interfaz de usuario del agente. (FORMS-14694)
* Cuando un usuario obtiene una vista previa de una carta en una comunicación interactiva con un XML de datos guardado, la carta se queda atascada en el estado &quot;Cargando&quot; en la interfaz de usuario de AEM. La vista previa de la carta de nuevo con el mismo XML funciona bien. (FORMS-14521)
* En AEM Forms Service Pack 20 (6.5.20.0), los usuarios que envían correos electrónicos con archivos adjuntos mediante el botón &quot;Enviar correo electrónico&quot; en formularios adaptables advierten de un problema. El nombre del archivo adjunto aparece en la línea siguiente en lugar de en línea. (FORMS-14426)
* Cuando un usuario genera un PDF en AEM Forms con listas con viñetas establecidas en el estilo predeterminado &quot;Disco&quot;, el PDF no supera la comprobación de accesibilidad en la herramienta de accesibilidad de Adobe Acrobat. La lista con los estilos &quot;Viñeta&quot; y &quot;Cuadrado&quot; pasa la comprobación de accesibilidad. (FORMS-13802, LC-3922179)
* Cuando un usuario se actualiza de AEMForms-6.5.0-0065 a AEMForms-6.5.0-0087 en la configuración independiente RHEL8 JBoss®, no se conecta con el contenedor del servicio LiveCycle. (FORMS-15907) *
* En AEM Forms en JEE, en AEM Workspace, seleccionar un formulario enviado anteriormente para iniciar un nuevo proceso de formulario provoca un problema. Forms con datos rellenados previamente sobrescribe todos los datos enviados anteriormente, eliminando los campos rellenados manualmente. (FORMS-15376)
* En AEM Forms Service Pack 20 (6.5.20.0), cuando un usuario convierte el archivo Tiff a PDF mediante el servicio PDFG, se produce el siguiente error: (FORMS-14879) ALC-PDG-011-028-Error al convertir el archivo de imagen de entrada a PDF. com/sun/image/codec/jpeg/JPEGCodec
* Actualizar en AEM Forms en archivos jar JEE: La biblioteca `commons-collections:commons-collections:jar` ahora se incluye para mejorar la resolución de dependencias y la funcionalidad en varios trabajos JEE de AEM Forms, como:
   * Mejora del trabajo del ensamblador para mejorar el procesamiento del trabajo y la gestión de errores.
   * Mejora del trabajo de PDF Generator (PDFG) para garantizar operaciones más fluidas para la generación y conversión de documentos.
   * LC-Upgrade Mejora del trabajo para mejorar el proceso de actualización a la vez que se garantiza una transición estable entre versiones.
   * Mejora del trabajo de Rights Management para proteger la gestión de documentos y funciones mejoradas de Rights Management.
   * Mejora de trabajos para un procesamiento de trabajos y una administración del sistema más fiables.
* A partir de AEM Forms OSGi 6.5.22, la operación renderPDFForm del servicio Forms no ejecutará scripts solo de cliente (runAt=client) en el servidor, solo aquellos marcados runAt=server o runAt=both se ejecutarán como se describe en la tabla siguiente. (FORMS-16564)

  | Script marcado como runAt | Ejecutado en el servidor |
  |---------------------|-------------------------|
  | servidor | sí |
  | ambos | sí |
  | cliente | no |

#### XMLFM {#forms-xmlfm-sp22}

* En AEM Forms Service Pack 21 (6.5.21.0), cuando un usuario agrega etiquetas no estándar a archivos PDF mediante XMLFM, el documento no cumple los requisitos de especificación de PDF. (LC-3922484)
* Cuando un usuario genera un PDF utilizando el Servicio de salida en el Service Pack 20 de AEM Forms (6.5.20.0), se produce un error con CORBA.COMM_FAILURE y se muestra el error: `15:04:35,973 ERROR [com.adobe.formServer.PA.XMLFormAgentWrapper] (default task-14) ALCOUT-002-013: XMLFormFactory, PAexecute failure: "org.omg.CORBA.COMM_FAILURE"`. El servicio se pasa correctamente cuando la función de accesibilidad &quot;Referencia&quot; se excluye del subformulario de la plantilla XDP. sin embargo, esta función es necesaria para el cumplimiento 508. (LC-3922402)
* Cuando un usuario convierte un formulario XFA en una PDF de AcroForm, se produce un error. (LC-3922363)
* En AEM Forms Service Pack 19 (6.5.19.0), cuando un usuario crea un XDP con los subformularios sin nombre, FS_DATA_SOM aparece vacío para los subformularios sin nombre. (LC-3922034)

#### Forms Designer {#forms-designer-sp22}

* Cuando un usuario abre una biblioteca de fragmentos seleccionando una carpeta de fragmentos en AEM Forms Designer versión 6.5.21.0, se bloquea. (LC-3922439)
* Cuando un usuario desinstala la versión de AEM Forms Designer de 32 bits 6.5.20.0 e instala la versión de AEM Forms Designer 6.5.21.0, Forms Designer no se inicia. Los registros de errores muestran una asignación de memoria insuficiente para el entorno de tiempo de ejecución de Java (JRE). (LC-3922404)
* Una vez que un usuario instala AEM Forms Designer versión 6.5.20.0, la opción Macros no aparece en el menú, sólo aparece la macro predeterminada &#39;Comprobador de accesibilidad&#39; y no se puede ejecutar. (LC-3922321)
* Cuando un usuario agrega una nueva ubicación de plantilla para crear XDP en la versión 6.5.20.0 de AEM Forms Designer, Forms Designer se bloquea. (LC-3922316)
* Cuando un usuario genera resultados mediante el método ExportData en el OSGI del paquete de servicio 15 (6.5.15.0) de AEM Forms 6.5, produce datos incompletos e incorrectos. (LC-3922340)


<!-- #### [!DNL Adaptive Forms] {#forms-6522}

* A


#### [!DNL Forms Designer] {#forms-designer-6522}

* A -->


### Foundation {#foundation-6522}

En la consola de AEM Assets, se ha producido un problema al intentar reordenar documentos DITA. La ruta de exploración situada en la parte superior del cuadro de diálogo del explorador de rutas muestra incorrectamente el nombre del nodo en lugar del título del nodo para el nodo principal raíz. El título del nodo correcto solo aparece después de seleccionar un elemento dentro de la ruta de exploración, lo que indica un error de visualización temporal. (NPR-42106)


<!-- #### Apache Felix {#foundation-apachefelix-6522}


* A

#### Campaign{#foundation-campaign-6522}

* A


#### Cloud Services{#foundation-cloudservices-6522}

* A -->


#### Comunidades {#foundation-communities-6522}

Después de actualizar de AEM 6.5.19 a 6.5.20, surgió un problema en el cual `Connection evic` subprocesos no se cerraron correctamente después de las llamadas a `UgcSearch`. Este problema, observado en el entorno de producción, hace que estos subprocesos persistan y se acumulen con el tiempo, lo que podría afectar al rendimiento. (NPR-42019)


<!-- #### Content distribution{#foundation-content-distribution-6522}

* A -->


#### CRX {#foundation-crx-6522}

* La ordenación no funcionaba de acuerdo con **Grupos** del menú del lado izquierdo del Administrador de paquetes de CRX. (GRANITE-53277)
* El Administrador de paquetes de AEM restringe la instalación de versiones de paquetes más bajas de forma predeterminada, pero permite realizar instalaciones potentes de versiones anteriores. Sin embargo, el uso de la opción de instalación forzada puede interferir con futuras instalaciones a través de la canalización estándar. Por ejemplo, si está instalada la versión 1.21 de y se agrega la versión 1.24, la instalación se realiza correctamente e incluye ambas versiones. Sin embargo, al intentar instalar la versión 1.22 sobre 1.24, se produce un error en la canalización, pero funciona si se instala a la fuerza, enumerando todas las versiones. Del mismo modo, la instalación de la versión 1.23 se bloquea si la versión 1.24 ya está presente, ya que la canalización no permite las actualizaciones posteriores. (GRANITE-53263)


#### Granite{#foundation-granite-6522}

* Los paquetes de instantáneas se instalaban en AEM mediante comandos CURL. Durante la instalación, el instalador JCR analizó los paquetes mediante el instalador OSGI para asegurarse de que no se requieran paquetes o configuraciones OSGI adicionales. Si la versión de un paquete contenía &quot;SNAPSHOT&quot;, el instalador de OSGI activaba VLT para crear un paquete de instantáneas correspondiente. Sin embargo, dado que cada instancia de autor de AEM ejecuta su propio instalador OSGI, ambas instancias pueden intentar generar la instantánea simultáneamente, lo que provoca conflictos de sesión dentro del repositorio. (NPR-42003)
* Existía una contención de bloqueo en `ScriptDependencyResolver` con AEM 6.5.21. (GRANITE-53181)
* Después de actualizar AEM a 6.5.21, surgieron problemas cuando se usaban rutas relativas en la sintaxis de Sightly (HTL), como `data-sly-use`. (GRANITE-53080)


#### Integraciones{#foundation-integrations-6522}

* Se ha agregado una declaración de atribución legal para la interfaz de usuario de Cloud Services. (FORMS-16373)
* Adición de permisos de lectura para que el usuario **fd-cloudservice** acceda a las configuraciones de hCaptcha y Turnstile, lo que le permite recuperar el ID de cliente y el secreto de cliente necesarios para la validación y el procesamiento de captcha. Además, se implementó un modelo de Lista de control de acceso para administrar el acceso a estas configuraciones. (FORMS-16360)


#### Localización{#foundation-localization-6522}

En ![Icono de martillo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) Herramientas > **Seguridad** > ![Icono de usuario](https://spectrum.adobe.com/static/icons/workflow_18/Smock_User_18_N.svg) **Usuarios**, en la página Administración de usuarios, los datos de la columna **Estado** de la tabla se mostraban verticalmente. (GRANITE-48304)


<!-- #### Oak {#foundation-oak-6522}

* A -->


#### Plataforma{#foundation-platform-6522}

* El seguimiento de Enterprise Information Management introducido en AEM 6.5.18 provocó anomalías en el cálculo de las puntuaciones de adopción del producto. La biblioteca de métricas de Adobe provocó este problema al sobrescribir los datos de usuario proporcionados por la biblioteca de seguimiento de Omega. Como resultado, las puntuaciones de adopción de muchos clientes de AEM Sites y AEM Assets cayeron a cero a partir de febrero de 2024. (CQ-4358438)
* Se ha identificado un problema crítico en el entorno de producción en el que el recolector de elementos no utilizados gestionaba las etiquetas de forma incorrecta. Específicamente, cuando se movió una etiqueta o se le cambió el nombre, el recolector de elementos no utilizados no pudo actualizar la propiedad `cq:MovedTo`, lo que provocó que la etiqueta desapareciera de las páginas. (CQ-4358293)
* Un problema con ContextHub en AEM 6.5.19 hacía que los segmentos se resolvieran incorrectamente cuando se agregaba una ruta de contexto a una instancia de AEM. El problema afectaba específicamente al campo URL dentro de los objetos de JavaScript generados por el componente de página, donde faltaba el prefijo de ruta de contexto requerido. Esta omisión impedía que los segmentos funcionaran según lo esperado. (SITES-21852)
* Se ha actualizado AEM Quickstart para que utilice la biblioteca `commons-collections-3.2.2-adobe-2`. La actualización garantiza que la aplicación se pueda seguir ejecutando sin problemas. (NPR-42150)
* La configuración de OAuth2 de SMTP en AEM 6.5 difiere considerablemente de lo que se utiliza en AEM as a Cloud Service. Para optimizar la configuración y garantizar la coherencia, la configuración de AEM 6.5 debía estar alineada con los estándares utilizados en AEM as a Cloud Service. (GRANITE-53273)
* Se encontró un problema al hacer clic en ![Icono de brújula](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Compass_18_N.svg) > ![Icono del proyecto](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Project_18_N.svg) Proyectos y, a continuación, al pasar el puntero del ratón sobre ![Icono de carril izquierdo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![Icono de cheurón hacia abajo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg), apareció un acento grave antes de la información sobre herramientas &quot;Solo contenido&quot;. (CQ-4356633)

#### Seguridad{#foundation-security-6522}

* Se han encontrado problemas con una biblioteca criptográfica JSAFE (versión 6.0.0) obsoleta en AEM. Se incluye un paquete parcheado con JSAFE versión 6.2.5 en AEM 6.5.22. (NPR-42006)
* Al validar los protocolos permitidos durante las comprobaciones XSS, los controladores se comparan con &quot;http&quot; y &quot;https&quot;. Sin embargo, la propiedad `protocol` de un objeto URL devolvió estos valores con dos puntos finales, como `http:` y `https:`. Esta discrepancia causó problemas de validación. Para garantizar un análisis preciso, la comprobación de protocolo necesaria para tener en cuenta los dos puntos o ajustar la lógica de comparación en consecuencia.  (NPR-42119)
* Después de instalar AEM 6.5.21 (la versión anterior era AEM 6.5.19) en IBM® WebSphere® Liberty Profile y Semeru Java 8.0, no se pudo abrir ninguna página. Los registros de errores indicaron problemas relacionados con las versiones de servlet que requerían diferentes paquetes. Para solucionar este problema, se tuvo que revertir la dependencia de `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` porque estaba relacionada con el problema. (NPR-42116)
* Varios exploradores están eliminando gradualmente la compatibilidad con las cookies **SameSite=None**, que se utilizan para permitir el acceso entre sitios a las cookies. Como alternativa, se están introduciendo **cookies particionadas**. Estas cookies aíslan el almacenamiento según el contexto en el que se utilizan, lo que mejora la privacidad y seguridad al impedir el seguimiento entre sitios, al tiempo que permite que las cookies funcionen dentro de particiones específicas, como contenido de terceros incrustado. (GRANITE-51953)


<!-- #### Sling{#foundation-sling-6522}

* A -->


#### Traducción{#foundation-translation-6522}

* Se ha agregado compatibilidad con los cambios recientes en los componentes principales en las reglas de traducción predeterminadas. (NPR-42029)
* Se ha identificado un problema con la exportación de archivos XLIFF en AEM Forms. Al usar la opción **Exportar selección como XLIFF (solo cadenas)**, la secuencia de componentes no se mantenía de forma coherente. Sin embargo, la secuencia sigue siendo correcta al exportar XLIFF para un idioma específico. Se proporcionaron dos archivos para demostrar el problema: **DE-CH_Export.xliff** (secuencia correcta) y **String_Export.xliff** (secuencia incorrecta). (NPR-42118)


#### Interfaz de usuario{#foundation-ui-6522}

* `coralui-component-dialog` estaba modificando la ubicación de `cq-dialog-actions`, lo que podría afectar al diseño o al comportamiento de los botones de acción en los cuadros de diálogo de AEM. (NPR-42294)
* La funcionalidad del selector de color en AEM no funcionaba correctamente. Cuando se accede a él, muestra un modal en blanco, lo que impide la selección de color. Este problema comenzó después de instalar AEM 6.5.20 en el entorno de ensayo. El selector de color funcionó correctamente *antes* de la actualización. (NPR-42163)
* En ![Icono de martillo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **Herramientas** > **Flujo de trabajo** > **Modelos** > seleccione cualquier modelo > **Iniciar flujo de trabajo**, faltaba el icono Examinar en el campo Carga útil del cuadro de diálogo **Ejecutar flujo de trabajo**. (NPR-42162)


<!-- #### WCM{#foundation-wcm-6522}

* A


#### Workflow{#foundation-workflow-6522}

* A -->


## Instalar [!DNL Experience Manager] 6.5.22.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.22.0 requiere [!DNL Experience Manager] 6.5. Consulte [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del Service Pack está disponible en Adobe [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip).
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.22.0 en una de las instancias de creación mediante el Administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe no recomienda quitar ni desinstalar el paquete [!DNL Experience Manager] 6.5.22.0. Como tal, antes de instalar el paquete, debe crear una copia de seguridad de `crx-repository` en caso de que deba revertirla. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Instalar el Service Pack en [!DNL Experience Manager] 6.5{#install-service-pack}

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de realizar la instalación, realice una instantánea o una copia de seguridad nueva de la instancia de [!DNL Experience Manager].

1. Descargar el Service Sack de [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el Administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y luego seleccione **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de la instalación del Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacén de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo de la interfaz de usuario del administrador de paquetes a veces se cierra durante la instalación del paquete de servicio. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete actualizador antes de asegurarse de que la instalación se haya realizado correctamente. Normalmente, este problema se produce en el explorador [!DNL Safari], pero puede ocurrir de forma intermitente en cualquier explorador.

**Instalación automática**

Existen dos métodos diferentes que puede utilizar para instalar [!DNL Experience Manager] 6.5.22.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en la carpeta `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.
* Use la API [HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que se instalen los paquetes anidados.

>[!NOTE]
>
>Experience Manager 6.5.22.0 no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar la instalación**

Para conocer las plataformas que están certificadas para funcionar con esta versión, consulte los [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.22.0)` en [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos los paquetes OSGi están **[!UICONTROL ACTIVOS]** o **[!UICONTROL FRAGMENTOS]** en la consola OSGi (use la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es de la versión 1.22.20 o posterior (utilice la consola web: `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Instalar Service Pack para [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Para obtener instrucciones para instalar el Service Pack en Experience Manager Forms, consulte [Instrucciones de instalación del Service Pack de Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La funcionalidad Formularios adaptables, disponible en [AEM 6.5 Inicio rápido](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), está diseñada únicamente para la exploración y la evaluación. Para su uso en producción, es esencial obtener una licencia válida para AEM Forms, ya que la funcionalidad Formularios adaptables requiere una licencia adecuada.

### Instalación del paquete de índice de GraphQL para fragmentos de contenido de Experience Manager{#install-aem-graphql-index-add-on-package}

Los clientes que usen GraphQL deben instalar el [fragmento de contenido de Experience Manager con el paquete de índice 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip) de GraphQL.

Al hacerlo, puede añadir la definición de índice necesaria en función de las funciones que utilizan realmente.

Si no se instala este paquete, las consultas de GraphQL pueden ser lentas o dar error.

>[!NOTE]
>
>Instale este paquete solo una vez por instancia; no es necesario reinstalarlo con cada Service Pack.

### UberJar{#uber-jar}

UberJar para [!DNL Experience Manager] 6.5.22.0 está disponible en el [repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar UberJar en un proyecto de Maven, consulta [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluye la siguiente dependencia en el POM de tu proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.22</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar y los demás artefactos relacionados están disponibles en el repositorio de Maven Central en lugar del repositorio Maven público de Adobe (`repo.adobe.com`). Se cambió el nombre del archivo principal de UberJar a `uber-jar-<version>.jar`. Por lo tanto, no hay `classifier`, con `apis` como valor, para la etiqueta `dependency`.


## Funciones en desuso y eliminadas{#removed-deprecated-features}

Ver [funciones obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md/).

## Problemas conocidos{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->


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

* Actualice las consultas de GraphQL que puedan haber utilizado un nombre de API personalizado para el modelo de contenido para utilizar el nombre predeterminado del modelo de contenido en su lugar.

* Una consulta GraphQL puede utilizar el índice `damAssetLucene` en lugar del índice `fragments`. Esta acción puede dar como resultado consultas de GraphQL que fallan o que tardan mucho tiempo en ejecutarse.

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

* Al intentar mover, eliminar o publicar fragmentos de contenido, sitios o páginas, hay un problema cuando se recuperan las referencias de fragmentos de contenido. La consulta en segundo plano falla. Es decir, la funcionalidad no funciona.
Para garantizar el funcionamiento correcto, debe agregar las siguientes propiedades al nodo de definición de índice `/oak:index/damAssetLucene` (no se requiere la reindexación):

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si actualiza la instancia de [!DNL Experience Manager] de la versión 6.5.0 a la 6.5.4 al Service Pack más reciente de Java™ 11, verá `RRD4JReporter` excepciones en el archivo `error.log`. Para detener las excepciones, reinicie la instancia de [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Los usuarios pueden cambiar el nombre de una carpeta en una jerarquía de [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Durante la instalación de [!DNL Experience Manager] 6.5.x.x se pueden mostrar los siguientes errores y mensajes de advertencia:
   * &quot;Cuando la integración de Adobe Target se configura en [!DNL Experience Manager] mediante la API de Target Standard (autenticación IMS) y, a continuación, se exportan fragmentos de experiencias a Target, se crean tipos de ofertas incorrectos. En lugar de &quot;Fragmento de experiencia&quot;/fuente &quot;Adobe Experience Manager&quot;, Target crea varias ofertas con el tipo &quot;HTML&quot;/fuente &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en `granite/operations/maintenance`.
   * La validación del lado del servidor de formularios adaptables falla cuando se utilizan funciones de agregado como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : no se encontraron ventanas de mantenimiento en `granite/operations/maintenance`.
   * El punto interactivo de una imagen interactiva de Dynamic Media no está visible al obtener una vista previa del recurso a través del visor de titulares de ventas.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : tiempo de espera agotado para completar el cambio de registro sin registrar.

* A partir de AEM 6.5.15, el motor Rhino JavaScript proporcionado por el paquete ```org.apache.servicemix.bundles.rhino``` presenta un nuevo comportamiento de elevación. Los scripts que utilizan el modo estricto (```use strict;```) deben declarar sus variables correctas. De lo contrario, no se ejecutan y terminan generando un error de tiempo de ejecución.

* La instalación del contenido listo para usar relacionado con el etiquetado mediante un paquete de actualización oficial restablece la propiedad de idiomas del nodo `/content/cq:tags` de forma predeterminada. Esta acción se aplica a los paquetes de servicio, los paquetes de servicio de seguridad, los paquetes de funciones ampliadas, los paquetes de funciones acumulativas, los parches, etc. Por lo tanto, es necesario agregarlo desde las propiedades antes de la instalación.

### Problema conocido de AEM Sites {#known-issues-aem-sites-6522}

* Fragmentos de contenido: la previsualización falla debido a la protección DoS para un gran árbol de fragmentos. Consulte el artículo de [KB sobre las opciones de configuración predeterminadas de GraphQL Query Executor](https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934)


### Problemas conocidos de AEM Forms {#known-issues-aem-forms-6522}

* Si la conversión de HTML a PDF falla en el servidor SUSE® Linux® (SLES 15 SP6 o posterior) con el error: `Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57`.
Siga estos pasos para resolver el problema:
   1. Inicie el servidor y establezca la variable de entorno `OPENSSL_CONF` mediante el siguiente comando:
      `export OPENSSL_CONF=/etc/ssl`
También puede establecer la variable de entorno al iniciar el servidor:
      `-e OPENSSL_CONF=/etc/ssl`
   1. Reinicie el servidor.
* Después de instalar AEM Forms JEE Service Pack 21 (6.5.21.0), si encuentra entradas duplicadas de Jars Geode `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` en la carpeta `<AEM_Forms_Installation>/lib/caching/lib` (FORMS-14926), realice los siguientes pasos para resolver el problema:

   1. Detenga los localizadores, si están en funcionamiento.
   1. Detenga el servidor de AEM.
   1. Vaya a `<AEM_Forms_Installation>/lib/caching/lib`.
   1. Quite todos los archivos de revisión de Geode excepto `geode-*-1.15.1.2.jar`. Confirme que solo están presentes los jars Geode con `version 1.15.1.2`.
   1. Abra el símbolo del sistema en modo de administrador.
   1. Instale el parche de Geode mediante el archivo `geode-*-1.15.1.2.jar`.

* Si un usuario intenta obtener una vista previa de un borrador de carta con datos XML guardados, se queda atascado en el estado `Loading` para algunas cartas específicas. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-14521)

* Después de actualizar a AEM Forms Service Pack 6.5.21.0, el servicio `PaperCapture` no puede realizar operaciones de OCR (reconocimiento óptico de caracteres) en archivos PDF. El servicio no genera resultados en forma de PDF o de archivo de registro. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (CQDOC-21680)

* Cuando los usuarios actualizaban de AEM 6.5 Forms Service Pack 18 o 19 a Service Pack 20 o 21, encontraban un error de compilación de JSP. Este error les impedía abrir o crear formularios adaptables. También causó problemas con otras interfaces de AEM. Estas interfaces incluían el editor de páginas, la interfaz de usuario de AEM Forms, el editor de flujos de trabajo y la interfaz de usuario de Información general del sistema. (FORMS-15256)

  Si tiene un problema de este tipo, realice los siguientes pasos para resolverlo:
   1. Vaya al directorio `/libs/fd/aemforms/install/` en CRXDE.
   1. Elimine el paquete con el nombre `com.adobe.granite.ui.commons-5.10.26.jar`.
   1. Reinicie el servidor de AEM.

* Después de actualizar al paquete de servicio 20 de AEM Forms (6.5.20.0) con el complemento de Forms, las configuraciones que dependen del servicio de Adobe Analytics Cloud heredado mediante autenticación basada en credenciales dejan de funcionar. Este problema impedía que las reglas de Analytics se ejecutaran correctamente. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (FORMS-15428)

* Cuando un usuario actualiza al Service Pack 20 de AEM Forms (6.5.20.0) en el servidor JEE y genera archivos PDF mediante los servicios de salida, los archivos PDF se representan con problemas de accesibilidad. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922112)
* Cuando un usuario genera archivos PDF etiquetados mediante el servicio de salida en JEE, muestra la &quot;Advertencia de estructura inadecuada&quot;. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922038)
* Cuando se envía un formulario en AEM Forms JEE, las instancias de un elemento XML repetitivo se eliminan de los datos. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3922017)
* Cuando un usuario en un entorno Linux® procesa un formulario adaptable (en JEE) en HTML, no se procesa correctamente. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921957)
* Cuando un usuario convierte un archivo XTG al formato PostScript mediante el servicio Output en AEM Forms JEE, se produce el siguiente error: `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921720)
* Después de actualizar al paquete de servicio 18 de AEM Forms (6.5.18.0) en el servidor JEE, cuando un usuario envía un formulario, no se puede procesar HTML5 o PDF forms y XMLFM se bloquea. Para descargar e instalar la revisión, consulte el artículo [Revisiones de Adobe Experience Manager Forms](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms). (LC-3921718)
* En la Vista previa de impresión de la interfaz de usuario de Interactive Communications Agent, el símbolo de moneda (como el signo de dólar $) se muestra de forma incoherente para todos los valores de campo. Aparece para valores de hasta 999, pero falta para valores de 1000 y superiores. (FORMS-16557)
* Las modificaciones realizadas en el XDP de los fragmentos de diseño anidados en una comunicación interactiva no se reflejan en el editor de CI. (FORMS-16575)
* En la Vista preliminar de la interfaz de usuario de Interactive Communications Agent, algunos valores calculados no se muestran correctamente. (FORMS-16603)
* Cuando la carta se ve en la Vista previa de impresión, el contenido cambia. Es decir, algunos espacios desaparecen y ciertas letras se sustituyen por &quot;x&quot;. (FORMS-15681)
* Cuando un usuario configura una instancia de WebLogic 14c, el servicio PDFG en AEM Forms Service Pack 21 (6.5.21.0) en JEE que se ejecuta en JBoss® falla debido a conflictos del cargador de clases que implican la biblioteca SLF4J. El error se muestra de la siguiente manera (CQDOC-22178):

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature
  ```

## Paquetes de contenido y paquetes OSGi incluidos{#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en esta versión del paquete de servicio [!DNL Experience Manager] 6.5:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.22.0](/help/release-notes/assets/65220-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.22.0](/help/release-notes/assets/65220-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos{#restricted-sites}

Estos sitios web solo están disponibles para los clientes de. Si es cliente de y necesita acceso, póngase en contacto con el administrador de cuentas de Adobe.

* [Descarga de producto en Licensing.adobe.com](https://licensing.adobe.com/)
* [Póngase en contacto con Atención al cliente de Adobe](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de producto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html?lang=es)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [Suscribirse a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)
