---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6,5
description: Busque información sobre la versión, novedades, procedimientos de instalación y una lista detallada de cambios para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 38227a66-f2a9-4909-9297-1eced4ed6e8c
source-git-commit: a0e9bfd4bcbf7091d5537c6d88025ef4d6046b4d
workflow-type: tm+mt
source-wordcount: '3989'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5 Últimas notas de la versión de Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.15.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versión de Service Pack |
| Fecha | 24 de noviembre de 2022 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## ¿Qué incluye [!DNL Experience Manager] 6.5.15.0 {#what-is-included-in-aem-6515}

[!DNL Experience Manager] 6.5.15.0 incluye nuevas funciones, mejoras clave solicitadas por el cliente, correcciones de errores y mejoras de rendimiento, estabilidad y seguridad, que se han publicado desde la disponibilidad inicial de la versión 6.5 en abril de 2019. [Instalar este Service Pack](#install) en [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6515}

* Si el movimiento de un recurso en el Experience Manager falla, se puede cambiar el nombre del recurso. (NPR-38753)
* Mientras ve los recursos en un [!UICONTROL Vista de lista], faltan algunos títulos. (CQ-4345746)
* El lector de pantalla no anuncia el submenú del [!UICONTROL Relate] en la ficha Básico de la página Propiedades del recurso. (ASSETS-6938)
* El lector de pantalla detecta incorrectamente los iconos de carpeta de la página de navegación Recursos con la lista de carpetas. (ASSETS-6936)
* Al copiar una colección, a la imagen le falta un vacío `alt` attribute o role=&quot;presentation&quot;. Como resultado, la imagen se expone a los usuarios del lector de pantalla. (ASSETS-6932)
* El texto mostrado al anotar un recurso no tiene un 4:5:1 relación de contraste en comparación con el color de fondo. (ASSETS-6931)
* En la ficha IPTC de la página de propiedades del recurso, al ajustar el ancho de la página, el contenido de la página no se ajusta correctamente y da como resultado un desplazamiento horizontal. (ASSETS-6929)
* Al filtrar recursos, filtre el texto de la sección [!UICONTROL min] y [!UICONTROL max] desaparece después de introducir un valor. (ASSETS-6925)
* En Colecciones de Experience Manager, el lector de pantalla no anuncia el [!UICONTROL email] en la pantalla Descargar. (ASSETS-6923)
* Falta un texto alternativo al anotar los elementos. (ASSETS-6922)
* Si el texto está escrito en horas y minutos en el campo selector de fechas, no se muestra ningún mensaje de error de texto. El error solo se identifica con el color rojo. (ASSETS-6852, ASSETS-6921, ASSETS-6920, ASSETS-6907)
* El texto alternativo de `[role='img']` falta en el filtro Archivos . (ASSETS-6919)
* Anuncio incorrecto del lector de pantalla para la variable [!UICONTROL Crear] submenú. (ASSETS-6916)
* En Colecciones de Experience Manager, el botón Quitar `X` no tiene ningún texto que anunciar para los lectores de pantalla. (ASSETS-6912)
* Cuando se utiliza el Analizador de contraste de color en el Experience Manager, no hay diferencia de color entre la fecha actual y la fecha elegida en el selector de fechas del widget de calendario. Carece de una relación de contraste de al menos 3:1 en comparación con sus colores adyacentes. (ASSETS-6911)
* En Archivos de Experience Manager, al seleccionar una de las opciones de [!UICONTROL Programación] en Administrar publicación, el lector de pantalla anuncia el nombre y el estado de las opciones del botón de radio. Sin embargo, la variable **Programación** no se ha anunciado. (ASSETS-6908, ASSETS-6906)
* Falta el texto alternativo para el icono Ordenar. (ASSETS-6904)
* En la página Propiedades del recurso, el nombre del campo `Person` en la extensión IPTC, los lectores de pantalla no anuncian las etiquetas de pestaña. El lector de pantalla solo anuncia campos editables y actualmente en blanco, pero no el nombre de la etiqueta. (ASSETS-6903, ASSETS-6848)
* La herramienta de anotación no se puede mostrar mediante el teclado. Se utiliza un ratón para dibujar una imagen y mostrar la herramienta Anotación. (ASSETS-6899)
* En Colecciones de Experience Manager, un campo vacío en la variable **Avanzadas** muestra una relación de contraste incorrecta entre el límite y el color adyacente. (ASSETS-6895)
* Valores de atributos ARIA incorrectos para algunos de los elementos durante la edición de recursos. (ASSETS-6894)
* El lector de pantalla no identifica correctamente el encabezado al crear un flujo de trabajo. (ASSETS-6892)
* Al copiar una colección, el botón para eliminar la imagen del SVG `X` a role=&quot;img&quot; le falta un role=&quot;presentation&quot;. Como resultado, la imagen se expone a los usuarios del lector de pantalla. (ASSETS-6890)
* En el **Básico** de las propiedades de los recursos, el lector de pantalla no anuncia adecuadamente el estado de expansión o contracción del campo Etiquetas. (ASSETS-6889)
* La variable **Básico** en Propiedades del recurso contiene páginas con ID duplicado. (ASSETS-6888)
* La etiqueta del campo de texto para definir un título mientras se crea un flujo de trabajo desaparece al especificar un valor en el cuadro de texto. (ASSETS-6887)
* La lista de destinatarios que comparten un vínculo se muestra como una tabla de datos con encabezados, pero no se identifica semánticamente como una tabla de datos para los usuarios del lector de pantalla. (ASSETS-6886)
* No se muestra ningún mensaje de error para representar un campo vacío en `Add Email Address` campo . El error solo se representa con un color. (ASSETS-6885, ASSETS-6843)
* Los textos de marcadores de posición, Ruta y Texto alternativo no tienen al menos una relación de contraste 4.5:1 en comparación con su color de fondo. (ASSETS-6884, ASSETS-6865)
* Valores no válidos para algunos de los atributos ARIA mientras se guarda una colección inteligente. (ASSETS-6882)
* Al guardar una colección inteligente, algunas de las etiquetas no se asocian correctamente con el lector de pantalla. (ASSETS-6881)
* En la pestaña IPTC de las propiedades de los recursos, el lector de pantalla no anuncia la etiqueta de los campos de formulario de palabra clave. (ASSETS-6879)
* En las colecciones de Experience Manager, la variable [!UICONTROL Correo electrónico] no se identifica como campo obligatorio y no se muestra ningún mensaje de error si no especifica ningún valor. (ASSETS-6877)
* En los archivos Experience Manager, no hay ningún mensaje de error en **Uso compartido de vínculos** se muestra en `Add Email Address`. El error solo se identifica al usar un color. (ASSETS-6876, ASSETS-6875)
* [!UICONTROL Recorte y mapa] no tienen los nombres programáticos al editar un recurso. (ASSETS-6874)
* El texto Filtro carece de relación contractual 4.5:1 en comparación con el color de fondo. (ASSETS-6873)
* El texto del nombre de la carpeta en la página de navegación principal no tiene una relación de contraste 4.5:1 en comparación con el color de fondo. (ASSETS-6872)
* Mientras realiza el [!UICONTROL Copiar] operación para colecciones, la variable **[!UICONTROL Agregar usuario]** el control de formulario de cuadro combinado no está correctamente asociado con su etiqueta visible. (ASSETS-6870)
* El lector de pantalla no anuncia [!UICONTROL Crear] opciones de submenú del botón. (ASSETS-6869)
* Las opciones Ámbito, Flujos de trabajo y Zona horaria no tienen una relación de contraste de 4,5:1 en comparación con el color de fondo. (ASSETS-6868)
* El lector de pantalla anuncia incorrectamente el estado de colapso del **Cronología** para abrir el Navegador. (ASSETS-6864)
* Faltan elementos secundarios para algunas de las funciones de ARIA al guardar una colección inteligente. (ASSETS-6862)
* Al compartir un recurso, se requerían atributos ARIA para `Search/Add Email Address` no se han especificado. (ASSETS-6860)
* La variable **map** no se puede mostrar mediante el teclado. En su lugar, es necesario hacer clic con el ratón para mostrar el cuadro de diálogo del mapa. (ASSETS-6859)
* Faltan elementos secundarios para algunas de las funciones de ARIA en la pestaña Básico de la página Propiedades del recurso. (ASSETS-6858)
* Los campos de entrada de texto vacío, disponibles en la pestaña IPTC de las propiedades de Asset, no tienen una relación de contraste 3:1 en comparación con sus colores adyacentes. (ASSETS-6854, ASSETS-6847)
* Los iconos de perfil de **Cronología** los lectores de pantalla detectan incorrectamente . (ASSETS-6850)
* El lector de pantalla no anuncia que el cuadro combinado Revisar estado, disponible en la ficha Básico de las propiedades de los recursos, sea de solo lectura. (ASSETS-6849)
* El lector de pantalla no anuncia correctamente la etiqueta de las casillas de verificación Seleccionar todo y Anotación . (ASSETS-6846)
* El foco del teclado omite el `About Adobe Experience Manager` en la **Mostrar ayuda** para abrir el Navegador. (ASSETS-6845)
* Los lectores de pantalla no anuncian correctamente las carpetas seleccionadas al navegar por la lista de carpetas con las teclas de flecha del teclado en la vista de tarjeta. (ASSETS-6844)
* Al cargar un PDF al Experience Manager, el uso de memoria aumenta constantemente. (ASSETS-16889)
* Cuando un flujo de trabajo convierte un archivo .ZIP en un nombre de carpeta en Assets, no conserva la mayúsculas y minúsculas del nombre del archivo .ZIP. (ASSETS-16712)
* Al cambiar de Brand Portal a Experience Manager 6.5, el filtro predicado del usuario no muestra los resultados adecuados al aplicar el filtro por primera vez. (ASSETS-15932)
* No se puede anotar un vídeo. (ASSETS-15217)
* **Administrar publicación** desaparece para un usuario sin acceso de replicación y `READ` y `WRITE` acceso a `ETC` y `VAR`. (ASSETS-15007)
* El tiempo de carga de la página de propiedades aumenta para un recurso con varias referencias. (ASSETS-14182)
* Cuando se cancela la publicación de una imagen desde Brand Portal, el Experience Manager también la cancela de la publicación de Dynamic Media y, como resultado, no se muestra ninguna imagen en el sitio web activo. (ASSETS-14118)
* Problemas XSS en tarjetas de recorte inteligente en Dynamic Media. (ASSETS-14212, ASSETS-14208, ASSETS-13704)
* Problema XSS en Ajustes preestablecidos de visor en Dynamic Media. (ASSETS-13822)
* Valide el acceso de los usuarios al obtener una vista previa de los recursos de DM en AEM. (CQ-4314757)


## Comercio {#commerce-6515}

* Error al crear una página de tienda, lo que detiene el proceso general de implementación del catálogo. (CQ-4347181)

## [!DNL Forms] {#forms-6515}

### Características principales {#keyfeatures}

* AEM Forms Designer ya está disponible en [Configuración regional en español](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es). (LC-3920051)
* Ahora puede usar [OAuth2 para autenticarse con los protocolos de servidor de correo de Microsoft Office 365 (SMTP e IMAP)](/help/forms/using/oauth2-support-for-mail-service.md). (NPR-35177)
* Puede establecer [Revalidate en el servidor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br) a true para identificar los campos ocultos y excluirlos de un documento de registro en el servidor. (NPR-38149)
* AEM Forms Designer requiere una versión de 32 bits de Visual C++ 2019 Redistribuible (x86).  (NPR-36690)

### Correcciones {#fixes}

* Cuando la propiedad de un formulario adaptable desactivada para los datos está activada, el aspecto del botón de radio y de los grupos de casillas de verificación no cambia. (NPR-39368)
* Cuando se traduce un formulario adaptable, se omiten algunas de las traducciones y no se muestran correctamente. (NPR-39367)
* Cuando la propiedad de una página está definida como oculta, la página no se elimina del conjunto de formularios. (NPR-39325)
* En un documento de registro, la sección de nota al pie dinámica al final de la página no está presente. (NPR-39322)
* Cuando se genera un documento de registro para un formulario adaptable, solo se permite la alineación vertical para los botones de opción y las casillas de verificación. El usuario no puede establecer la alineación horizontal para los botones de opción y las casillas de verificación. (NPR-39321)
* Después de implementar la Gestión de Correspondencia, si varios usuarios intentan acceder a un formulario, org.apache.sling.i18n.impl.JcrResourceBundle.loadPotentialLanguageRoots se convertirá en un cuello de botella y la mayoría de los subprocesos se verán afectados. A menudo, varias solicitudes de página de formularios tardaron más de 1 minuto en cargarse cada una incluso cuando el servidor tiene una carga muy baja. (NPR-39176, CQ-4347710)
* En un formulario adaptable, cuando se utiliza un campo de texto enriquecido en un fragmento de formulario adaptable cargado a medida, se experimentan algunos de los siguientes errores:
   * No se puede editar el contenido ni añadir nada al campo Texto enriquecido .
   * No se respeta el patrón de visualización aplicado al texto enriquecido. 
   * El mensaje de error de longitud mínima del campo no se muestra al enviar el formulario.
   * El contenido de este campo de texto enriquecido se incluye varias veces en el submit-XML producido. (NPR-39168)
* Cuando se utiliza la opción Selector de fecha en un formulario adaptable, no se puede convertir el valor al formato correcto. (NPR-39156)
* Al previsualizar un formulario adaptable como formulario HTML, no se procesa correctamente, ya que algunos subformularios se superponen con el formulario principal. (NPR-39046)
* Si el panel tiene una tabla oculta y el formulario adaptable se procesa mediante la vista tabular, los campos de la primera ficha no se muestran correctamente. (NPR-39025)
* La variable `Body` falta la etiqueta de para la plantilla OOTB (predeterminada). (NPR-39022)
* El documento de registro no se genera en el idioma del formulario adaptable. Siempre se genera en inglés. (NPR-39020)
* Cuando un formulario adaptable tiene varios paneles y algunos de los paneles utilizan el **Archivo adjunto** el componente `Error occurred while draft saving` se produce un error . (NPR-38978)
* When `=` se utiliza en los campos de casilla de verificación, lista desplegable o botón de radio de un formulario adaptable y se genera el documento de registro y, a continuación, `=` no está visible en el documento de registro generado.(NPR-38859)
* Hay un aumento múltiple en el número de errores de procesamiento de lotes de notificaciones después de la actualización del Service Pack 6.5.11.0. (NPR-39636)
* Cuando no se proporcionan datos de prueba, las letras de Gestión de Correspondencia no se cargan en la interfaz de usuario del agente. (CQ-4348702)
* Cuando el usuario aplica el AEM Forms Service Pack 14 (SP14) de AEM Forms implementado mediante IBM® WebSphere®, el arranque falla al inicializar una base de datos y la `java.lang.NoClassDefFoundError:org/apache/log4j/Logger` se produce un error.(NPR-39414)
* En un formulario AEM en el servidor OSGi, cuando se utiliza la API del servicio de documentos para certificar el PDF, se produce un error: com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException: AEM-DSS-311-003. (NPR-38855)
* Cuando el usuario intenta utilizar el servicio wrapper para procesar cartas con AEM 6.3 Forms, la variable `java.lang.reflect.UndeclaredThrowableException` se produce un error. (CQ-4347259)
* Cuando un XDP se procesa como formulario HTML5, el contenido de la página de formato se procesa primero independientemente de la colocación de los objetos en un formulario adaptable. (CQ-4345218)
* La configuración de la aplicación en el servidor de destino cambia a la configuración definida en el servidor de origen aunque la variable **Sobrescribir la configuración cuando se complete la importación** no está activada en el momento de importar la aplicación. (NPR-39044)
* Cuando un usuario intenta actualizar la configuración del conector mediante el Administrador de configuración, falla.(CQ-4347077)
* Cuando el usuario intenta ejecutar un parche de AEM Forms en JEE después de cambiar la contraseña predeterminada del usuario administrador, se produce una excepción `com.adobe.livecycle.lcm.core.LCMException[ALC-LCM-200-003]: Failed to whitelist the classes` ocurre. (CQ-4348277)
* En AEM Designer, los campos de formulario sin rótulos se colocan en celdas de tabla, incluidas las casillas de verificación.(LC-3920410)
* Cuando el usuario intenta abrir la Ayuda en el Diseñador de AEM Forms, esta no se muestra correctamente. (CQ-4341996)

## [!DNL Sites] {#sites-6515}

* La consola Lanzamientos de Experience Manager Sites se estaba quedando en blanco. (NPR-39188)
* Las referencias no se ajustaban cuando la página que tenía la referencia también tenía que activarse durante el movimiento de la página. (NPR-39061)
* Cuando se muestra un contenedor de diseño oculto mediante un contenedor principal, los cambios de diseño no se aplican a todos los componentes dentro del contenedor anidado. (NPR-39041)
* El contenido ya no se superpone con otro contenido con una anchura de 320 píxeles. (SITES-8885)
* Se ha agregado enfoque después de cerrar un cuadro de diálogo. (SITES-8885)

### Accesibilidad {#access-6515}

<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The scrollable region of the Page Editor did not have keyboard access. (SITES-2936) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The color input field of the Page Editor is not labeled or visible on the screen. (SITES-2925) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The iframe in the Page Editor is missing a title attribute; it must have an accessible name. (SITES-2894) -->
* La variable **[!UICONTROL Anotación]** falta su nombre de accesibilidad. (SITES-2892)
* El estado de un componente de interfaz de usuario ACTIVO (**[!UICONTROL Cortar]**, **[!UICONTROL Copiar]**, **[!UICONTROL Pegar]**, **[!UICONTROL Insertar componentes]**, **[!UICONTROL Grupo]**, etc.) no tiene al menos una relación de contraste de luminosidad de tres a uno con el fondo adyacente interior o exterior. (SITES-8889, SITES-8756, SITES-8885)
* Mensaje de estado no anunciado automáticamente. (SITES-8889, SITES-8756, SITES-8885)
* El contenido del texto carece de una relación de contraste de 4,5:1. (SITES-8756, SITES-8885)
* El texto del vínculo o del botón carece de la relación de contraste 4.5:1 al pasar el ratón o al centrar la atención. (SITES-8756, SITES-8885)

### [!DNL Content Fragments] {#sites-contentfragments-6515}

* GraphQL plantea una excepción. Por ejemplo, no puede obtener etiquetas de variación de un fragmento de contenido. No hay variación con el nombre &quot;eléctrico&quot;. Este problema se debe a una llamada `getVariationTags` para una variación no existente que produzca una excepción. (SITES-8898)
* Ordenar los pedidos de título en la vista de lista, tanto ascendente como descendente, cómo los títulos con el orden A, C, B. (SITES-7585)
* Se ha agregado compatibilidad con etiquetas para variaciones de fragmentos de contenido. (SITES-8168)
* Se ha identificado y eliminado el código específico de Odin del Experience Manager 6.5 que era innecesario. (SITES-3574)
* Al publicar un fragmento de copia de idioma desde la interfaz de usuario del Editor de fragmentos de contenido, las referencias asociadas se publicaban en la carpeta en inglés. (NPR-39182)
* Los campos de fecha se rellenan previamente con una fecha. (NPR-39124)
* Las etiquetas desaparecen la segunda vez que selecciona la opción de botón de radio. (NPR-39071)

### Fluid XP {#sites-fluidxp-6515}

* Habilitar compatibilidad con la compilación ES6 para la biblioteca de cliente `/libs/cq/gui/components/siteadmin/admin/restoretree/clientlibs/restoretree.js`. (NPR-39067)
* El campo múltiple de un modelo de fragmento de contenido no se puede vaciar ni guardar porque la validación se produce aunque **[!UICONTROL Requerido]** no está seleccionado. (NPR-39063)
* En **[!UICONTROL Copiar]** o **[!UICONTROL Live Copy]** tareas, la variable `cq:targetMetadata` la información se duplicaba incorrectamente. Esta funcionalidad provocaba que dos o más fragmentos de experiencia en el Experience Manager apuntaran a la misma oferta exportada en el destino. (NPR-38970)
* Después de una acción Restaurar árbol, se muestra el mensaje `Un-publication pending. #0 in the queue` aparece en la interfaz de usuario de una página que, en primer lugar, nunca se publicó. (NPR-38847)

### Editor de página {#sites-pageeditor-6515}

* Deshacer no eliminó el último cambio realizado en el texto que se agregó al componente. En su lugar, cuando se actualizó la página, se eliminó todo el componente. (SITES-8597)
* Actualización `jquery-ui` En la versión más reciente, el Editor de páginas no funcionaba correctamente. (NPR-38596)
* El contenido ya no se superpone con otro contenido con una anchura de 320 píxeles. (SITES-8756)
* se ha agregado enfoque después de cerrar el cuadro de diálogo (SITES-8756)

## Sling {#sling-6515}

* `Repoinit` no era compatible con la creación o administración de grupos con espacio en blanco en el nombre principal porque el nombre del grupo se trataba como una cadena y no permitía que se citara. (SLING-10952)
* Los registros se rellenan inadvertidamente con mensajes de error y excepciones. (NPR-39024)

## Proyectos de traducción {#translation-6515}

* La página de destino se agregaba al trabajo de traducción para copias de idioma actualizadas a través del panel Proyectos . la página de origen no se actualizó. (NPR-39278)
* El proceso de traducción fallaba al generar una vista previa de todas las páginas de un proyecto de traducción. (NPR-39059)
* Si la configuración regional de idioma no existe, se sigue creando en una carpeta de configuración regional cuando las reglas de referencia están configuradas para un evento. (NPR-39054)

## Interfaz de usuario {#ui-6515}

* Los errores de JavaScript ocurren dentro del archivo `multifield.js` para determinados campos del modelo Fragmento de contenido en el editor de modelos de fragmento de contenido y también en el editor de fragmentos de contenido. (NPR-39350)

## Flujo de trabajo {#workflow-6515}

* Los flujos de trabajo que se ejecutaron correctamente en el Experience Manager 6.5.11 no se ejecutaban de forma coherente en el Experience Manager 6.5.13. (NPR-39023)

## Instalar [!DNL Experience Manager] 6.5.15.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.15.0 requiere [!DNL Experience Manager] 6.5. Véase [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas. <!-- UPDATE FOR EACH NEW RELEASE -->
* La descarga del Service Pack está disponible en Adobe [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html).
* En una implementación con MongoDB y varias instancias, instale [!DNL Experience Manager] 6.5.15.0 en una de las instancias de autor que utiliza el Administrador de paquetes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
>Adobe no recomienda quitar o desinstalar el [!DNL Experience Manager] Paquete 6.5.15.0. Como tal, antes de instalar el paquete, debe crear una copia de seguridad de la variable `crx-repository` en caso de que necesite revertirla. <!-- UPDATE FOR EACH NEW RELEASE -->

### Instale el Service Pack en [!DNL Experience Manager] 6,5 {#install-service-pack}

>[!NOTE]
>
> Antes de instalar la última versión [Paquete de servicio de AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), realice los pasos siguientes:
> 1. Instale el [org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar](https://jira.corp.adobe.com/secure/attachment/9396977/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) fragmento de servlet.
> 1. Espere a que el servidor de aplicaciones se estabilice.
> 1. Instalar [Paquete de servicio de AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip).



1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se actualizó desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de la instalación, tome una instantánea o una copia de seguridad nueva de su [!DNL Experience Manager] instancia.

1. Descargue el Service Pack desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra el Administrador de paquetes y, a continuación, seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y, a continuación, seleccione **[!UICONTROL Instalar]**.

1. Para actualizar el conector S3, detenga la instancia después de instalar el Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacenamiento de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del Administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que las instalaciones se realizan correctamente. Normalmente, este problema ocurre en [!DNL Safari] pero puede ocurrir de forma intermitente en cualquier explorador.

**Instalación automática**

Hay dos métodos diferentes que puede utilizar para instalar automáticamente [!DNL Experience Manager] 6.5.15.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.
* Utilice la variable [API HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Uso `cmd=install&recursive=true` para que se instalen los paquetes anidados.

>[!NOTE]
>
>El Experience Manager 6.5.15.0 no admite la instalación del Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar la instalación**

Para saber cuáles son las plataformas certificadas para funcionar con esta versión, consulte la [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.15.0)` under [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos los paquetes OSGi son: **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.13 o posterior (utilice la consola web: `/system/console/bundles`). <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

>[!NOTE]
>
>Si instala la última [Paquete de servicio de AEM (6.5.15.0)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), los errores CRX/bundle y la página de inicio muestran que el servicio no está disponible, [haga clic aquí](/help/forms/using/aem-service-pack-installation-solution.md).


### Instalar [!DNL Experience Manager] Paquete de complementos de Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Omitir si no utiliza [!DNL Experience Manager] Forms.

<!-- 
Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.
-->

1. Asegúrese de que ha instalado la variable [!DNL Experience Manager] Service Pack.
1. Descargue el paquete de complementos de Forms correspondiente que aparece en las [versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) para su sistema operativo.
1. Instale el paquete de complementos de Forms como se describe en [Instalación de paquetes de complementos de AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. Si utiliza letras en Experience Manager 6.5 Forms, instale la variable [último paquete de compatibilidad de AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### Instalar [!DNL Experience Manager] Forms en JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms en JEE. Correcciones en [!DNL Experience Manager] Forms en JEE se entrega a través de un instalador independiente.

Para obtener información acerca de la instalación del instalador acumulativo para [!DNL Experience Manager] Forms en JEE y la configuración posterior a la implementación, consulte la [notas de la versión](jee-patch-installer-65.md).

>[!NOTE]
>
>Después de instalar el instalador acumulativo para [!DNL Experience Manager] Forms en JEE, instale el Service Pack más reciente. Después de la instalación correcta de Service Pack, instale el último paquete de complementos de Forms, elimine el paquete de complementos de Forms de la `crx-repository\install` y reinicie el servidor.

### UberJar {#uber-jar}

UberJar para [!DNL Experience Manager] La versión 6.5.15.0 está disponible en la [Repositorio de Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar y los otros artefactos relacionados están disponibles en el Repositorio Central de Maven en lugar del Repositorio de Maven Público de Adobe (`repo.adobe.com`). Se cambia el nombre del archivo UberJar principal a `uber-jar-<version>.jar`. Así que no hay `classifier`, con `apis` como valor, para la variable `dependency` etiqueta.

## Funciones en desuso {#removed-deprecated-features}

A continuación se muestra una lista de funciones y capacidades que están marcadas como obsoletas con [!DNL Experience Manager] 6.5.7.0. Las funciones se marcan como obsoletas inicialmente y después se eliminan en una versión futura. Se proporciona una opción alternativa.

Revise si utiliza una función o una capacidad en una implementación. Además, planifique cambiar la implementación para utilizar una opción alternativa.

| Área | Función | Reemplazo |
|---|---|---|
| Integraciones | La variable **[!UICONTROL Inclusión de AEM Cloud Services]** ya que la función [!DNL Experience Manager] y [!DNL Adobe Target] la integración se actualiza en [!DNL Experience Manager] 6.5. La integración es compatible con la API de Adobe Target Standard. La API utiliza la autenticación mediante Adobe IMS y [!DNL Adobe I/O Runtime]. Apoya el creciente papel de Adobe Launch como instrumento [!DNL Experience Manager] páginas para analytics y personalización, el asistente de inclusión es funcionalmente irrelevante. | Configure las conexiones del sistema, la autenticación IMS de Adobe y [!DNL Adobe I/O Runtime] integraciones a través de las [!DNL Experience Manager] servicios en la nube. |
| Conectores | El conector JCR de Adobe para Microsoft® SharePoint 2010 y Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/D |

## Problemas conocidos {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->

* [AEM fragmento de contenido con el paquete de índice de GraphQL 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
Este paquete es necesario para los clientes que utilizan GraphQL; esto les permite añadir la definición de índice necesaria en función de las funciones que realmente utilizan.

* Como [!DNL Microsoft® Windows Server 2019] no es compatible [!DNL MySQL 5.7] y [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] no admite instalaciones llave en mano para [!DNL AEM Forms 6.5.10.0].

* Si actualiza su [!DNL Experience Manager] de la versión 6.5 a la versión 6.5.10.0, puede ver `RRD4JReporter` las excepciones de `error.log` archivo. Para resolver el problema, reinicie la instancia.

* Si instala [!DNL Experience Manager] 6.5 Service Pack 10 o un Service Pack anterior en [!DNL Experience Manager] 6.5, la copia en tiempo de ejecución del modelo de flujo de trabajo personalizado de recursos (creado en `/var/workflow/models/dam`).
Para recuperar la copia de tiempo de ejecución, Adobe recomienda sincronizar la copia en tiempo de diseño del modelo de flujo de trabajo personalizado con su copia de tiempo de ejecución mediante la API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Los usuarios pueden cambiar el nombre de una carpeta de una jerarquía [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el Explorador de propiedades. Si se selecciona para configurar otro campo del formulario adaptable en el mismo editor, se resuelve el problema.

* Durante la instalación de [!DNL Experience Manager] 6.5.x.x:
   * &quot;Cuando la integración de Adobe Target está configurada en [!DNL Experience Manager] con la API de Target Standard (autenticación IMS) y luego exportar fragmentos de experiencia a Target se crean tipos de oferta incorrectos. En lugar de escribir &quot;Fragmento de experiencia&quot;/origen &quot;Adobe Experience Manager&quot;, Target crea varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor del formulario adaptable falla cuando se utilizan funciones agregadas como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al previsualizar el recurso mediante el visor de banners de ventas.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tiempo de espera de que el cambio del registro se complete sin registrar.

* Al intentar mover, eliminar o publicar fragmentos de contenido o sitios o páginas, hay un problema cuando se recuperan referencias de fragmentos de contenido, ya que la consulta en segundo plano falla; es decir, la funcionalidad no funciona.
Para garantizar la operación correcta, debe añadir las siguientes propiedades al nodo de definición de índice `/oak:index/damAssetLucene` (no se requiere reindexación):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Paquetes de contenido y paquetes OSGi incluidos {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.15.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.15.0](/help/release-notes/assets/65150_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.15.0](/help/release-notes/assets/65150_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sitios web restringidos {#restricted-sites}

Estos sitios web solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* [Contacto con el servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página de producto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es)
>* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)

