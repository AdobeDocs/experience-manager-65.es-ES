---
title: '[!DNL Adobe Experience Manager] Notas de la versión de Service Pack 6.5.'
description: Release notes specific to [!DNL Adobe Experience Manager] 6.5 Service Pack 6.
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '4530'
ht-degree: 6%

---


# [!DNL Adobe Experience Manager] Notas de la versión de Service Pack 6.5 {#aem-service-pack-release-notes}

## Información de la versión {#release-information}

| Productos | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.6.0 |
| Tipo | Versión de Service Pack |
| Fecha | 3 de septiembre de 2020 |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.6-1.0.zip) |

## Qué incluye Adobe Experience Manager 6.5.6.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.6.0 es una actualización importante que incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras de rendimiento, estabilidad y seguridad, que se han publicado desde la disponibilidad general de la versión 6.5 en **abril de 2019**. Se puede instalar sobre Adobe Experience Manager 6.5.

Las principales funciones y mejoras introducidas en Adobe Experience Manager 6.5.6.0 incluyen:

* La publicación de las carpetas de contribución de recursos desde Brand Portal a Recursos Experience Manager ahora también se admite a través del servidor proxy.

* Los grupos de carpetas privadas autogenerados ahora se limpian al eliminar la carpeta privada en [!DNL Experience Manager Assets].

* Las descripciones de los modificadores en el editor de ajustes preestablecidos de [!UICONTROL visor] de vídeo se han actualizado en [!DNL Dynamic Media].

* Se proporciona una nueva configuración de compañía para reflejar el estado del [!DNL Dynamic Media] conector.

* Las opciones predeterminadas para `test` y `aiprocess` se actualizan a `Thumbnail`, desde `Rasterize` antes en Dynamic Media, para garantizar que los usuarios solo tengan que crear miniaturas y omitir la extracción de página y la extracción de palabras clave.

* [Rellene previamente un formulario adaptable en el cliente](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client).

* [Integración del modelo de datos de formulario con las API de RESTful en un servidor con implementación](../../help/forms/using/configure-data-sources.md)SSL bidireccional.

* [Se mejoró el almacenamiento en caché para páginas](../../help/forms/using/configure-adaptive-forms-cache.md)de formularios adaptables traducidas.

* Compatibilidad con etiquetas de texto de [Adobe Sign en el servicio](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html)de conversión automatizada de Forms.

* Compatibilidad para [convertir formularios de color en formularios](https://docs.adobe.com/content/help/en/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html) adaptables mediante [!DNL Automated Forms Conversion service].

* Compatibilidad con los protocolos SMB 2 y SMB 3.

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.22.4.

Para obtener una lista completa de las funciones y mejoras introducidas en Experience Manager 6.5.6.0, consulte [Novedades de Adobe Experience Manager 6.5 Service Pack 6](new-features-latest-service-pack.md).

A continuación se muestra la lista de correcciones que se proporcionan en la versión [!DNL Experience Manager] 6.5.6.0.

### [!DNL Sites] {#sites-6560}

* En [!DNL Sites] o [!DNL Screens], seleccione un proyecto y haga clic en [!UICONTROL Administración Publicaciones]. Los usuarios no pueden avanzar en el asistente [!UICONTROL Administrar publicación] debido a errores de interfaz de usuario. Específicamente, la opción [!UICONTROL Publicar] no funciona (NPR-34099).
* La posición de iParsys (Sistema de párrafos heredado) no se vuelve a su posición predeterminada original después de anular la selección de las opciones [!UICONTROL Cancelar herencia] o [!UICONTROL Deshabilitar herencia] (NPR-34097).
* Si el `RolloutConfigManagerFactoryImpl` no puede cargar una configuración de despliegue, no intenta cargar las configuraciones que faltan. Devuelve las configuraciones almacenadas en caché (NPR-34092).
* En el componente de núcleo de texto, después de utilizar la opción de edición HTML de origen, se elimina la clase de la `em` etiqueta (NPR-34081).
* Después de actualizar de Experience Manager 6.3.3 a Experience Manager 6.5.3, el proceso de implementación tarda mucho más y la implementación falla con un error de tiempo de espera (NPR-34049).
* El `htmlwriter` no codifica los valores de atributo. El marcado que está presente en el marcado XF se exporta con valores de atributos descodificados (es decir, `"` en lugar de `&#34`). Provoca problemas en el lado del Destinatario con el Compositor de experiencias visuales que utiliza el XF exportado (NPR-34048).
* Al mover páginas en [!DNL Experience Manager Sites], mejore el registro para capturar el error de creación de versiones con el motivo (NPR-34014).
* En [!DNL Rich Text Editor] caso de que se elimine todo el texto, también se eliminará la etiqueta de párrafo (NPR-33976).
* Cuando se abre o actualiza la `siteadmin` página (en la IU clásica), las opciones del `New` menú están desactivadas (NPR-33949).

   ![Captura de pantalla que ilustra el problema de falta de menú en la IU clásica](assets/33949_missing_menu.png)

* Un [!DNL Content Fragment] no se puede usar como un `TemplatedResource` , ya que falla en `ContentFragmentUsePojo` (NPR-33911).
* Las operaciones de movimiento sincrónico y asíncrono pueden provocar errores debido a transferencias simultáneas. Las operaciones de movimiento de página están restringidas a movimiento sincrónico solamente. Evita el movimiento simultáneo de páginas (NPR-33875).
* [!UICONTROL La operación Administrar publicación] para replicar contenido de la instancia Autor a Publicación falla y genera un error de JavaScript (NPR-33872).
* Cuando se seleccionan varias páginas o recursos para crear versiones, la nueva versión se crea solo para la última página o recurso seleccionado (NPR-33866).
* Mueva una página de modelo con copias en vivo a otra carpeta. Al moverlo a la carpeta original, la operación de movimiento falla sin ningún error (NPR-33864).
* Cuando se utiliza la acción de mover para cambiar el nombre de una página web en la [!DNL Sites] consola, se muestran dos cuadros de diálogo superpuestos en el último paso del asistente (NPR-33831).

   ![Captura de pantalla que ilustra el problema del NPR-33831 con el diálogo de movimiento superpuesto](assets/33831_rename_dialog.png)

* Las propiedades `cq:acLinks` y `cq:acUUID` de [!DNL Adobe Campaign] la copia se eliminan durante la operación de copiar y pegar (NPR-33794).
* Al intentar un despliegue en una página secundaria de una Live Copy principal independiente, [!DNL Experience Manager] genera una excepción de puntero nulo (NPR-33676).
* Los [!DNL RTE] componentes de un contenedor de diseño no están visibles cuando el contenedor de diseño se copia y se vuelve a pegar en la página. Los [!DNL RTE] componentes no son editables, pero se muestran al actualizar la página (NPR-33662).
* Al cambiar el tamaño de un componente de diseño para diferentes puntos de interrupción (medio y grande), el diseño no se comporta como se espera (NPR-33608).
* En el modo de edición en línea de [!DNL RTE], arrastrar una imagen no funciona para el componente Texto (NPR-33602).
* Es posible crear un componente en una página de modelo con el mismo nombre que el nombre de la página. Durante el despliegue, `_msm_moved` se suprime para cambiar el nombre del componente. El componente se mueve al final del sistema [!UICONTROL de] párrafos (NPR-33535).
* Cuando offTime o onTime están configurados en muchas páginas o recursos, consumen muchos recursos y ralentizan el sistema durante el inicio y el cierre (NPR-33482).
* Un usuario con permisos CRUD activado no `/content/experience-fragment` puede eliminar una carpeta (NPR-33436).
* Puede seleccionar [!UICONTROL HTML y JSON] como opción para el formato [!UICONTROL de exportación de] Adobe Target en una carpeta principal de la [!DNL Experience Fragments] sección. Las mismas propiedades se muestran en la IU táctil para las subcarpetas de esta carpeta principal. Sin embargo, en CRXDE, por `cq:adobeTargetExportFormat`ejemplo, solo muestra HTML en lugar de mostrar `html,json` (NPR-33423).
* No se admite Publicar o Cancelar la publicación desde un alias de página. Elimine la opción que parece indicar lo contrario (NPR-33415).
* Una etiqueta específica se puede mover de una ubicación a otra en [!DNL Experience Manager]. También se puede aplicar a diferentes páginas antes y después de moverse. Al editar las propiedades de las páginas, la etiqueta no se muestra para su edición aunque la etiqueta sea la misma (NPR-33353).
* Una plantilla de página no se representa correctamente cuando se elimina un contenedor de diseño de una plantilla que contiene varios contenedores de diseño (NPR-33347).
* En el editor de plantillas, intente eliminar una plantilla que se utilice en más de 100000 páginas debajo `/content/`. Se muestra un error sin ningún mensaje de error (NPR-33312).
* El redireccionamiento a [!DNL Experience Manager] página con anclaje no funciona en la instancia Autor, ya que `PageRedirectServlets` coloca la cadena de consulta después de un fragmento de URL o un anclaje (NPR-34288).
* La creación de una marca en `/content/campaign` resulta en una estructura que no permite crear campañas. [!UICONTROL La opción Crear marca] deja a la marca recién creada sin capacidad para crear [!UICONTROL Ofertas y Actividades] , ya que no hay ninguna opción [!UICONTROL Crear] (NPR-34113).
* Puede suspender la creación [!DNL Live Copy] de una página y la herencia se interrumpe como se ve en el modo Editor. En las propiedades de página, el icono que representa la herencia indica incorrectamente que la herencia existe y no está rota (NPR-34017).
* Las páginas con muchas referencias no se pueden mover asincrónicamente y, en ocasiones, la operación de movimiento falla (CQ-4297969).
* Una página web con `/` caracteres en la URL deja de responder durante la creación. Cuando se agrega un componente durante la creación, aumenta el uso de la CPU y el explorador deja de responder (CQ-4295749).
* En el modo de exploración, NVDA no narra un valor seleccionado en la opción de menú Tipo/Tamaño. El enfoque visual no está en el elemento seleccionado. Los usuarios que dependen de un lector de pantalla no pueden utilizar el modo de exploración (CQ-4294993).
* Al crear una página web, los usuarios pueden seleccionar la plantilla [!UICONTROL de página] de contenido. En la ficha Medios  sociales, los usuarios seleccionan una variación de XF [!UICONTROL preferida]. Para seleccionar un fragmento de experiencia en el modo de exploración NVDA, los usuarios no pueden utilizar las teclas del teclado (CQ-4292669).
* Se ha actualizado la biblioteca de controladores a la versión 4.7.3 más segura (NPR-34484).

### [!DNL Assets] {#assets-6560}

**Mejoras de accesibilidad en Recursos Experience Manager**

* Con las teclas del teclado, los usuarios ahora pueden acceder a las opciones interactivas de la interfaz de usuario y centrarse en ellas en la lista de [!UICONTROL referencias] de los recursos (NPR-34115).

* El lector de pantalla ahora anuncia la acción prevista de los predicados en la página de búsqueda (NPR-34104).

* La página de búsqueda y la página de resultados de búsqueda ahora tienen títulos más informativos para comprender mejor a los usuarios de lectores de pantalla (NPR-34093).

* Los lectores de pantalla ahora anuncian las opciones para eliminar las etiquetas seleccionadas en la ficha [!UICONTROL Básico] de la página [!UICONTROL Propiedades] del recurso (NPR-33972).

* Los elementos de cada fila de la vista de lista ahora son anunciados como los elementos de la misma fila por los lectores de pantalla (NPR-33932).

* El enfoque del usuario al navegar con `Tab` la tecla pasa ahora a la opción de cierre en la previsualización de la versión (NPR-33863).

* El enfoque del usuario ahora se mueve al icono de búsqueda después de que Omniture esté cerrado (NPR-33705).

* Las opciones de interfaz de usuario procesables ahora tienen un enfoque visual más prominente y un mayor contraste al navegar con las teclas del teclado. Los usuarios del teclado pueden identificar las áreas enfocadas (NPR-33542).

* La funcionalidad de arrastrar mediante el teclado ahora funciona en el Editor [!UICONTROL de Esquemas de] metadatos en el modo de exploración del lector de pantalla (CQ-4296326).

* En el cuadro de diálogo de uso compartido de vínculos, al navegar en el modo de exploración, un lector de pantalla,

   * No narra la información de la tabla en cuanto se carga el cuadro de diálogo.

   * Puede navegar a todas las sugerencias automáticas de la lista.

   * Narra las sugerencias automáticas mostradas para [!UICONTROL Añadir dirección de correo electrónico/búsqueda] (CQ-4294232).

* El uso de la `Esc` tecla para eliminar los iconos de acción rápida de la vista de tarjeta ya no elimina el enfoque del teclado del último elemento seleccionado (CQ-4293554).

* Para las opciones interactivas en la interfaz de usuario, el lector de pantalla ahora anuncia su propósito en lugar de los nombres literales de los iconos (CQ-4272943).

* Ahora, el enfoque del teclado se mueve correctamente a [!UICONTROL las opciones Flotante], [!UICONTROL InlineZoom], [!UICONTROL Shoppable_Banner], [!UICONTROL Zoom_dark], [!UICONTROL Zoom_light]  [!DNL Dynamic Media] , ZoomVertical_oscuroZoom y ZoomVerticalLightal navegar con la tecla Tab en el recurso VistaPrevia en la página (CQ-4299999999955552555255525525555555552555555555555555525555555555555555555555555 0605).

* [!UICONTROL Ahora se puede acceder a la opción Guardar y cerrar] en la página [!UICONTROL Propiedades] del recurso con las teclas del teclado (NPR-34107).

* Los mensajes de error debido a combinaciones incorrectas de nombre de usuario y contraseña en la página de inicio de sesión ahora los lectores de pantalla anuncian cada vez que se produce el error (NPR-33722).

* En la sección [!DNL Experience Manager] de encabezado, al navegar en el modo Examinar, el lector de pantalla ahora anuncia:

   * Sugerencias de edición automática en [!UICONTROL Tipo para buscar] en Omniture.

   * El estado se expande o contrae para [!UICONTROL las opciones Soluciones], [!UICONTROL Ayuda], [!UICONTROL Bandeja de entrada]y [!UICONTROL Usuario] .

   * Mensaje de estado de la Ayuda [!UICONTROL de] búsqueda que se muestra cuando el usuario introduce una cadena de búsqueda en el campo [!UICONTROL Buscar ayuda] , en la opción [!UICONTROL Ayuda] .

   ![Menú Ayuda en el encabezado](assets/Help_aem_header.png)

   *Figura: [!UICONTROL Busque Ayuda] en el menú [!UICONTROL Ayuda] .*

   * El mensaje de error si se introduce un valor incorrecto en [!UICONTROL Suplantar como] campo en la opción [!UICONTROL Usuario] y el enfoque se mueve correctamente al campo de texto (NPR-33804).

   ![Menú Usuario en el encabezado](assets/User_aem_header.png)

   *Figura: [!UICONTROL Suplantar como] campo en el menú [!UICONTROL Usuario] en el encabezado.*

* Ahora el usuario puede cambiar el enfoque mediante el teclado:

   * [!UICONTROL Busque/Añada la dirección] de correo electrónico en el cuadro de diálogo [!UICONTROL Vínculo compartido] .

   * [!UICONTROL Añada el campo Usuario o Grupo] en Grupo [!UICONTROL de usuarios] cerrado en la ficha [!UICONTROL Permisos] de [!UICONTROL Propiedades] de la carpeta (NPR-34452).

**Problemas solucionados en Experience Manager Assets**

[!DNL Adobe Experience Manager] 6.5.6.0 [!DNL Assets] proporciona correcciones a los siguientes problemas:

* Las anotaciones no se resaltan cuando se seleccionan en la línea de tiempo del recurso (CQ-4302422).

* La previsualización de activos de garantía de marketing (como Folleto, Volante y Tarjeta de presentación) creada con [!DNL Adobe InDesign] plantilla no muestra saltos de línea ni saltos de párrafo (NPR-34268).

* La extracción de texto y, por lo tanto, la búsqueda de texto completo de los archivos PDF cargados no funciona (NPR-34164). Para solucionarlo, reinicie la implementación [!DNL sAdobe Experience Manager] después de instalar Service Pack 6.

* La línea de tiempo de los recursos de varias páginas muestra las anotaciones aplicadas a todos los subrecursos al explorar el recurso en la vista de la línea de tiempo, en lugar de mostrar las anotaciones específicas de los subrecursos específicos (NPR-34100).

* Las carpetas de recursos no se publican con la opción [!UICONTROL Administrar publicación] si las carpetas contienen recursos en los formatos de archivo JavaScript, CSS o JSON (NPR-34090).

* Al anular la selección o eliminar las etiquetas o filtros aplicados en Omniture, se ejecuta la consulta de búsqueda varias veces, lo que aumenta el tiempo de búsqueda (NPR-34078).

* En la vista de tarjetas cuando un flujo de trabajo (en un recurso de una carpeta) está en curso o pendiente, la página se vuelve a cargar hasta que se completa o finaliza el flujo de trabajo. Por lo tanto, los autores no pueden trabajar en los recursos de la carpeta para la que tienen que desplazarse hacia abajo (NPR-33986).

* Si el usuario mueve un recurso publicado a una nueva ubicación, el recurso se vuelve a publicar aunque la opción [!UICONTROL Volver a publicar] no esté seleccionada. Esto provoca que muchos recursos huérfanos se encuentren en la instancia de publicación. Sin embargo, el comportamiento predeterminado es que la operación de movimiento de un recurso publicado la anula de forma automática; este recurso se vuelve a publicar si el autor selecciona la opción [!UICONTROL Volver a publicar] al mover el recurso (NPR-33934).

* La página [!UICONTROL Mover recursos] para los recursos de las colecciones no carga todo el contenido HTML, como la opción [!UICONTROL Ajustar/volver a publicar] . Por lo tanto, los usuarios no pueden completar la operación de movimiento (NPR-33860).

* Al mover un recurso y añadir caracteres especiales en el nombre y el título de los recursos movidos, se crea una carpeta adicional (con el mismo nombre) en la nueva ubicación del recurso (NPR-33826).

* [!UICONTROL El botón Descargar] de un recurso se desactiva cuando se selecciona la opción [!UICONTROL Correo electrónico] en el cuadro de diálogo [!UICONTROL Descargar] (NPR-33730).

* El error &quot;Solicitar URI demasiado largo&quot; se observa al realizar operaciones masivas en recursos, como la edición masiva de metadatos (NPR-33723).

* Se observa un error de JavaScript y los usuarios no pueden seleccionar ni eliminar las opciones generadas en el campo [!UICONTROL Desplegable] [!UICONTROL Añadiendo mediante la funcionalidad de ruta] JSON en el Editor [!UICONTROL de formularios de Esquema de metadatos de]carpeta, si el archivo JSON cargado tiene un valor de espacio o caracteres especiales (NPR-33712).

* Las representaciones estáticas de recursos no se actualizan cuando el recurso se actualiza mediante la opción [!UICONTROL Abrir] en [!DNL desktop app] o [!DNL Adobe Asset Link] y se sincronizan de nuevo en [!DNL Adobe Experience Manager] (CQ-4296279).

* En la vista de columnas, la operación de movimiento de un conjunto de recursos también mueve los recursos seleccionados antes de utilizar la opción [!UICONTROL Filtrar] . Tenga en cuenta que el uso de la opción [!UICONTROL Filtro] anula la selección anterior (NPR-34018).

* Las barras invertidas se agregan antes que los caracteres especiales en las sugerencias de búsqueda de recursos, que tienen caracteres especiales en su nombre (NPR-33834).

* Al crear reglas para la lista desplegable en el formulario [!UICONTROL de Esquema de metadatos de]carpeta, el usuario no puede seleccionar valores en la columna Opciones [!UICONTROL de] campo (CQ-4297530).

* La copia en tiempo de ejecución del modelo de flujo de trabajo personalizado de recursos (creado en `/var/workflow/models/dam`) se elimina al instalar [!DNL Experience Manager] 6.5 Service Pack 5 o una versión anterior en [!DNL Experience Manager] 6.5 (NPR-34532). Para recuperar la copia en tiempo de ejecución, sincronice la copia en tiempo de diseño del modelo de flujo de trabajo con la copia en tiempo de ejecución mediante la API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

**Problemas solucionados en Dynamic Media**

* Si el usuario define la configuración de codificación en las ediciones después de crear el perfil de vídeo, la configuración de recorte inteligente se elimina de los perfiles de vídeo (CQ-4299177).

* Los recursos parpadean al cargarse la página cuando el usuario cambia entre las opciones de carril lateral (por ejemplo, [!UICONTROL Información general], [!UICONTROL Línea de tiempo], [!UICONTROL Visores]) en la página de detalles del recurso (NPR-34235).

* Se observan los siguientes problemas con el trabajo de reprocesamiento:

   * Falta el identificador de trabajo en el identificador de trabajo devuelto por el trabajo de reprocesamiento.

   * El trabajo de reprocesamiento para los registros de vídeo solo tiene que ver con el nombre del archivo y no con la ruta completa.

   * El trabajo de reprocesamiento no tiene la opción de establecer el tipo de recurso como estático.

   * `ExcludeFromAVS` no se proporciona (CQ-4298401).

* La funcionalidad de recorte inteligente falla cuando se agrega perfil de imagen a una carpeta con varias proporciones de aspecto (por ejemplo, 11) (NPR-34082).

* El flujo de trabajo de recursos de actualización de DAM se activa cuando el usuario se desplaza hacia abajo en la página Archivo [!UICONTROL de] flujo de trabajo en la ficha [!UICONTROL Flujo de trabajo] de [!UICONTROL Herramientas] en [!DNL Adobe Experience Manager] la configuración de Dynamic Media Scene7 (CQ-4299727).

* Los símbolos de la ficha [!UICONTROL Comportamiento] del Editor [!UICONTROL de ajustes preestablecidos de] visor no están localizados (CQ-4299026).

* La vista principal muestra la imagen con una presentación incorrecta que no cabe en el visor, si el visor está en modo interactivo (CQ-4298293).

* Los cambios en los ajustes preestablecidos de imagen en [!UICONTROL Adobe Experience Manager] no se sincronizan con Scene7 Publishing System (CQ-4299713).

### [!DNL Commerce] {#commerce-6560}

* Los vínculos a recursos de productos no se vuelven a factorizar cuando se mueven recursos (NPR-34098).

### Plataforma {#platform-6560}

* No se pueden descargar registros con la herramienta Diagnóstico en una instancia de Experience Manager actualizada (NPR-34336).
* La actualización falla con un error debido a las dependencias en una versión específica del paquete de `cq-wcm-api` base (CQ-4300520).
* No se especifican los valores predeterminados para los ajustes de tiempo de espera **[!UICONTROL y tiempo de espera]** de **[!UICONTROL socket de]** Connect para la configuración del agente predeterminado (publicación) (NPR-33707).
* Las actualizaciones de la configuración de asignación en `/etc/map.publish` no se reflejan en las páginas del sitio (NPR-34015).
* [La documentación](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) de referencia de API no incluye la documentación del `com.day.cq.tagging` paquete (CQ-4295864).

### Interfaz de usuario {#ui-6560}

* La interfaz del explorador de descarga no muestra todos los temas de trabajo (NPR-34308).
* La interfaz [del navegador](/help/sites-administering/configurations.md) de configuración no muestra todas las configuraciones (NPR-33644).
* Al pulsar la `Esc` tecla cuando se busca que los usuarios suplanten, se cierra el cuadro de diálogo **[!UICONTROL Usuario]** en lugar de la lista del usuario (NPR-34084).

### Integraciones {#integrations-6560}

* Las actividades con nombres largos no se sincronizan con [!DNL Adobe Target] (NPR-34254).

### Proyectos de traducción {#translation-6560}

* No se crea un proyecto de traducción si el usuario `authorizableID` incluye caracteres especiales (NPR-33828).

### Sling {#sling-6560}

* La comprobación de estado y el detector de patrones tienen una funcionalidad superpuesta. Como resultado, la comprobación de estado de salud se elimina del producto (NPR-33928).

### WCM {#wcm-6560}

* Componentes de base: cuando se agrega un componente de imagen de base a una página y se hace referencia a una imagen, la operación no `Undo` funciona (NPR-34516).

* No se puede utilizar la operación de desplazamiento de página (CQ-4303028).

### [!DNL Communities] {#communities-6560}

* Compartir una publicación en medios sociales muestra una opción obsoleta de Google+ (NPR-33877).

* El miembro de la comunidad no puede modificar la plantilla de grupo ni otros ajustes de la función de grupo (NPR-33530).

* Las etiquetas de hipervínculo de las imágenes no se generan correctamente en una publicación de foro (NPR-33464).

* Los errores de accesibilidad se identifican en la función Asignación de comunidad (NPR-33442).

* Los usuarios existentes de un grupo de comunidad agregados a través de la consola de administración se eliminan de la lista de usuario en cualquier modificación de la consola de grupo de comunidad (NPR-34315).

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack no incluye correcciones para [!DNL Forms]. They are delivered using a separate [!DNL Forms] add-on package. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

Después de instalar el paquete del complemento [!DNL Experience Manager Forms] 6.5.6.0:

* Detenga la [!DNL Experience Manager Forms] instancia.

* Elimine `bcpkix-1.51`los archivos `bcmail-1.51`y `bcprov-1.51` JAR del `crx-repository\launchpad\ext` directorio.

* Eliminar` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider` propiedad del `sling.properties` archivo.

* Reinicie la [!DNL Experience Manager Forms] instancia.

**Formularios adaptables**

* Cuando falta un fragmento de formulario adaptable, el formulario adaptable no se procesa (NPR-34302).

* La descripción del contenido de la ayuda de los campos de formulario adaptables muestra una etiqueta HTML de párrafo (NPR-34116).

* Al seleccionar la propiedad **[!UICONTROL Revalidate en el servidor]** , el formulario adaptable no se puede enviar (NPR-33876).

* La acción **[!UICONTROL Enviar a envío de extremo]** REST no funciona para un formulario adaptable (CQ-4299044).

* Accesibilidad: Al intentar enviar un formulario adaptable sin cargar un archivo adjunto para un campo obligatorio, el enfoque no se desplaza automáticamente al campo adjunto (CQ-4298065).

* Al agregar filas a una tabla de un formulario adaptable, las opciones **[!UICONTROL Añadir al principio]** y **[!UICONTROL Añadir al final]** no muestran los resultados adecuados (CQ-4297511).

* La secuencia de comandos de confirmación [!UICONTROL de] valor se activa incorrectamente, lo que provoca la pérdida de datos en un formulario adaptable (CQ-4296874).

* El selector de fechas no funciona correctamente en formularios adaptables localizados (NPR-34333).

* Cuando hay un subrayado o espacio en el nombre del archivo, no se puede adjuntar el archivo a un formulario adaptable (CQ-4301001).

* Cuando un panel repetible anidado tiene más apariciones que su principal, todas las ocurrencias de dicho panel repetible anidado no se pueden rellenar previamente (NPR-33666).

* Los formularios adaptables tienen algunos resueltores de recursos abiertos. Esto lleva a errores de envío. El problema se produce de forma intermitente (CQ-4299407).

* Al abrir la configuración de campo por primera vez, no se muestra el icono de propiedades (CQ-4296284).

**Flujo de trabajo**

* Cuando un aprobador de flujo de trabajo carga un archivo adjunto, se cambia su nombre a `undefined` (NPR-33699).

* [!DNL Experience Manager] Error en la operación de depuración de flujo de trabajo y muestra el siguiente mensaje de error (NPR-33575):

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] para dejar de [!DNL Windows] responder después de enviar un formulario (NPR-34409).

* Al instalar AEM Service Pack, la lista **Para hacer** de elementos no se muestra como vínculos. El texto de los elementos **Por hacer** incluye etiquetas HTML (NPR-34317).

**Comunicación interactiva**

* Cuando se incluye un fragmento de documento de texto con componentes repetibles anidados, la comunicación interactiva no se guarda (NPR-34095).

**Administración de correspondencia**

* Al modificar un fragmento de documento de texto que incluye valores de diccionario de datos, la interfaz de usuario del agente deja de responder (NPR-33930).

* Copiar y pegar contenido de un [!DNL Microsoft Word] documento en un fragmento de documento de texto en una carta genera problemas de formato (NPR-33536).

**Servicios de documentos**

* Cuando se genera un archivo PDF a partir de un archivo XDP mediante los servicios Output y Forms, el resultado es que falta texto y se superpone (NPR-34237, CQ-4299331).

* Al convertir un archivo HTML a PDF, el `MaxReuseCount` atributo no se puede configurar (NPR-33470).

* Cuando se descarga un archivo PDF que incluye funciones interactivas de Extensiones de Reader, no se puede agregar un archivo adjunto al archivo PDF mediante [!DNL Adobe Reader] (NPR-33729).

**:Seguridad de los documentos**

* No se puede ejecutar la operación de firma con certificados basados en HSM en un archivo PDF después de instalar [!DNL Experience Manager] Service Pack (NPR-34310).

**Diseñador**

* No se pueden abrir XForms en Designer versión 6.5.x (CQ-4295322).

* Al abrir Designer, la pantalla de bienvenida muestra un año incorrecto (CQ-4295289).

* Cuando se instala [!DNL Acrobat DC] en el servidor, la opción **[!UICONTROL Distribuir formulario]** está inactiva (CQ-4296304).

Para obtener información sobre las actualizaciones de seguridad, consulte la página [de boletines de seguridad de](https://helpx.adobe.com/security/products/experience-manager.html)Experience Manager.

## Install 6.5.6.0 {#install}

**Requisitos de configuración**

* AEM 6.5.6.0 requires AEM 6.5. See [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* La descarga del Service Pack está disponible en Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* En una implementación con MongoDB y varias instancias, instale AEM 6.5.6.0 en una de las instancias de creación mediante el Administrador de paquetes.
* Antes de realizar la instalación, realice una instantánea o una copia de seguridad nueva de la instancia de AEM.
* Reinicie la instancia antes de la instalación. Aunque esto solo es necesario cuando la instancia sigue en modo de actualización (y este es el caso cuando la instancia se actualizó desde una versión anterior), se recomienda si la instancia se ejecutó durante un período más largo.

>[!NOTE]
>
>Adobe no recomienda quitar o desinstalar el paquete Adobe Experience Manager 6.5.6.0.

### Instalación de Service Pack {#install-service-pack}

Siga los pasos siguientes para instalar Service Pack en una instancia de Adobe Experience Manager 6.5 existente:

1. Descargue el Service Pack desde [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.6-1.0.zip).

1. Abra el Administrador de paquetes y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener información sobre cómo utilizarla, consulte Administrador [de paquetes](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html).

1. Select the package and click **[!UICONTROL Install]**.

>[!NOTE]
>
>Debido a un problema conocido, hay disponible un paquete de Service Pack actualizado. Se recomienda instalar el paquete.

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda que espere a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que la instalación se realiza correctamente. Typically, this happens on [!DNL Safari] but can intermittently happen on any browser.

**Instalación automática**

Existen dos formas de instalar automáticamente Adobe Experience Manager 6.5.6.0 en una instancia de trabajo:

A. Coloque el paquete en la `../crx-quickstart/install` carpeta cuando el servidor esté disponible en línea. El paquete se instala automáticamente.

B. Utilice la API [HTTP del Administrador](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html)de paquetes. Utilícelo `cmd=install&recursive=true` para instalar los paquetes anidados.

>[!NOTE]
>
>Adobe Experience Manager 6.5.6.0 no admite la instalación de Bootstrap.

**Validar la instalación**

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.6.0)` en Productos instalados.

1. All OSGi bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.3 o posterior (utilice la consola web: `/system/console/bundles`).

Para conocer las plataformas certificadas para trabajar con esta versión, consulte los requisitos [técnicos](/help/sites-deploying/technical-requirements.md).

### Instalación del paquete de complementos de Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms. Las correcciones en Adobe Experience Manager Forms se entregan a través de un paquete adicional independiente.

1. Asegúrese de que ha instalado Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Instalar Adobe Experience Manager Forms en JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms en JEE. Las correcciones en Adobe Experience Manager Forms en JEE se entregan a través de un instalador independiente.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes for patch 0018](jee-patch-installer-65.md).

### UberJar {#uber-jar}

UberJar para Experience Manager 6.5.6.0 está disponible en el repositorio [de](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.6-1.0/)Maven Central.

Para usar UberJar en un proyecto Maven, vea [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.6-1.0</version>  
      <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>A partir de esta versión, UberJar y otros artefactos relacionados están disponibles en el repositorio de Maven Central en lugar del repositorio de Maven Público de Adobe (repo.adobe.com). Se cambia el nombre del archivo principal de UberJar a `uber-jar-<version>.jar`. Como resultado, no hay ningún `classifier`valor, con `apis` como valor, para la `dependency` etiqueta.

## Funciones en desuso {#removed-deprecated-features}

Esta sección lista las funciones y funciones que se han marcado como obsoletas con Experience Manager 6.5.6.0. Las funciones que se planea eliminar en una versión futura se definen como obsoletas en primer lugar, con una opción alternativa para su uso.

Se aconseja a los clientes que revisen si utilizan la función o la capacidad en su implementación actual y que planifiquen cambiar su implementación para utilizar la opción alternativa.

| Área | Función | Reemplazo |
|---|---|---|
| Integraciones | La pantalla de inclusión **[!UICONTROL de servicios de nube de]** AEM ya no se utiliza. Con la integración de AEM y Destinatario actualizada en AEM 6.5 para admitir la API de Target Standard, que utiliza la autenticación mediante IMS y E/S de Adobe, y el creciente papel de Inicio de Adobe para instrumentar páginas AEM para análisis y personalización, el asistente para la inclusión se ha vuelto funcionalmente irrelevante. | Configure las conexiones del sistema, la autenticación IMS de Adobe y las integraciones de E/S de Adobe mediante los respectivos servicios de nube de AEM. |
| Conectores | El conector JCR de Adobe para Microsoft SharePoint 2010 y Microsoft SharePoint 2013 está en desuso para AEM 6.5. | N/D |

## Problemas conocidos {#known-issues}

* Si la comprobación de estado de seguridad no funciona y el sistema muestra el siguiente mensaje de error:
   `message: Could not verify users and could not test system account logins.`
Siga los pasos siguientes para resolver el problema:
   1. Vaya a https://&lt;*hostname*>:&lt;*port*>/system/console/configMgr.

   1. Buscar `hc.impl`.

   1. En Asignaciones [!UICONTROL de servicio], haga clic en `+` y especifique `com.adobe.granite.repository.hc.impl=[user-reader-service]`.

   1. Click [!UICONTROL Save] to save the configuration.

* Si instala [!DNL Experience Manager] 6.5 Service Pack 5 o un Service Pack anterior en [!DNL Experience Manager] 6.5, se eliminará la copia en tiempo de ejecución del modelo de flujo de trabajo personalizado de recursos (creado en `/var/workflow/models/dam`).
Para recuperar la copia en tiempo de ejecución, Adobe sugiere sincronizar la copia en tiempo de diseño del modelo de flujo de trabajo personalizado con su copia en tiempo de ejecución mediante la API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Póngase en contacto con la asistencia de Adobe si se producen problemas al editar y crear reglas en cascada en el Esquema de metadatos de [!UICONTROL carpeta Editor] de Forms y el Editor [!UICONTROL de Forms de] metadatos mediante el cuadro de diálogo [!UICONTROL Definir regla] . Tenga en cuenta que las reglas que ya se han creado y guardado funcionan correctamente.

* Si se cambia el nombre de una carpeta en la jerarquía [!DNL Experience Manager Assets] y se publica en la carpeta anidada que contiene un recurso, [!DNL Brand Portal]el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el navegador de propiedades. Si selecciona configurar otro campo del formulario adaptable en el mismo editor, se resuelve el problema.

* Si [!UICONTROL el asistente para la configuración] de recursos conectados devuelve un mensaje de error 404 después de la instalación, vuelva a instalar manualmente los paquetes `cq-remotedam-client-ui-content` y `cq-remotedam-client-ui-components` mediante el Administrador de paquetes.

* Durante la instalación de AEM 6.5.x.x pueden aparecer los siguientes errores y mensajes de advertencia:
   * &quot;Cuando la integración de Target se configura en AEM mediante la API de Target Standard (autenticación IMS), la exportación de fragmentos de experiencia a Target provoca la creación de tipos de ofertas incorrectos. En lugar de tener que escribir &quot;Fragmento de experiencias&quot;/origen &quot;Adobe Experience Manager&quot;, Destino, se crean varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor de Formulario adaptable falla cuando se utilizan funciones acumuladas como SUM, MAX y MIN. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al obtener una vista previa del recurso a través del visor de pancarta de ventas.

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en AEM 6.5.6.0:

* [Lista de paquetes OSGi incluidos en AEM 6.5.6.0](assets/6560_bundles.txt)

* [Lista de paquetes de contenido incluidos en AEM 6.5.6.0](assets/6560_packages.txt)

## Restricted sites {#restricted-sites}

Estos sitios solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* [Póngase en contacto con el servicio de asistencia](https://docs.adobe.com/content/help/en/customer-one/using/home.html)al cliente Para obtener más información sobre el acceso al portal de asistencia técnica, consulte [Acceso al portal](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)de asistencia técnica.

>[!MORELIKETHIS]
>
>* [Notas de la versión de AEM 6.5](/help/release-notes/release-notes.md)
>* [Página de productos AEM](https://www.adobe.com/es/marketing/experience-manager.html)
>* [Documentación de AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

