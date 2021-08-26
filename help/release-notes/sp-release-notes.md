---
title: '[!DNL Experience Manager] Notas de la versión de service pack 6.5'
description: Notas de versión específicas del  [!DNL Adobe Experience Manager] 6.5 service pack 10
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '3652'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] Notas de la versión de service pack 6.5 {#aem-service-pack-release-notes}

## Información de la versión {#release-information}

| Productos | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.10.0 |
| Tipo | Versión de Service Pack |
| Fecha | 26 de agosto de 2021 |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip) |

## Qué incluye [!DNL Adobe Experience Manager] 6.5.10.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.10.0 incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras de rendimiento, estabilidad y seguridad, que se han publicado desde la publicación de la versión 6.5 en abril de 2019. El Service Pack se instala en [!DNL Adobe Experience Manager] 6.5.

Las funciones y mejoras clave introducidas en [!DNL Adobe Experience Manager] 6.5.10.0 son:

* **Editor y  [!DNL Content Fragment] modelos mejorados**: Ahora puede crear modelos complejos y personalizados para contenido estructurado mediante  [!DNL Content Fragment] modelos anidados. Las estructuras de contenido se modularizan en elementos básicos que se modelan como subfragmentos. Los fragmentos de nivel superior hacen referencia a estos subfragmentos. Más mejoras en el tipo de datos, como las reglas de validación avanzadas, mejoran aún más la flexibilidad del modelado de contenido con [!DNL Content Fragments]. El editor [!DNL Experience Manager] [!DNL Content Fragment] admite estructuras de fragmento anidadas en una sesión de editor común, con mejoras como la vista de árbol de estructura y la navegación con pestañas por las jerarquías de fragmento.

* **API de GraphQL para[!DNL Content Fragments]**: La nueva API de GraphQL es el método estándar para ofrecer contenido estructurado en formato JSON. Las consultas de GraphQL permiten a los clientes solicitar únicamente los elementos de contenido relevantes para procesar una experiencia. Esta selección elimina la entrega excesiva de contenido (posibilidad con las API HTTP REST) que requiere análisis de contenido en el lado del cliente. Los esquemas de GraphQL se derivan de modelos [!DNL Content Fragment] y las respuestas de API se realizan en formato JSON. En [!DNL Experience Manager] como [!DNL Cloud Service], las [consultas de GraphQL persisten](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) y procesan solicitudes de GET fáciles de almacenar en caché. Todavía no es posible en [!DNL Experience Manager] 6.5.

* **Administración de jerarquías y previsualización** futura: Los usuarios ahora tienen una interfaz para acceder a las estructuras de contenido de sus  [!DNL Experience Manager] lanzamientos, incluida la capacidad de agregar y eliminar páginas en un lanzamiento. Esta función mejora la flexibilidad de los [!DNL Experience Manager] lanzamientos para crear versiones de contenido destinadas a futuras publicaciones. [Las ](/help/sites-authoring/working-with-page-versions.md#timewarp) funciones de Deformación de tiempo permiten a los usuarios previsualizar los lanzamientos como estados de contenido futuros.

* **Recursos conectados**:  [!DNL Experience Manager] amplía la  [!DNL Connected Assets] funcionalidad al uso de  [!DNL Dynamic Media] imágenes en los componentes principales correspondientes. Consulte [Uso de recursos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

* **Vincule las opciones de uso compartido para descargar recursos o representaciones**: Al compartir recursos y colecciones como vínculos, los usuarios pueden elegir si permitir la descarga de recursos originales, sus representaciones o ambas opciones utilizando el vínculo compartido. Además, los usuarios que descargan los recursos compartidos con ellos mediante un vínculo obtienen la opción de descargar solo los recursos originales, solo las representaciones o ambos.

* **Limitar subrecursos generados**: Los administradores pueden limitar el número de subrecursos que  [!DNL Experience Manager] generan para recursos compuestos como archivos PDF, PowerPoint, InDesign y Keynote. Consulte [Administrar recursos compuestos](/help/assets/managing-linked-subassets.md#generate-subassets).

* **compatibilidad** Camera Raw: Hay disponible un nuevo  [!DNL Camera Raw] paquete compatible con la versión  [!DNL Adobe Camera Raw] 10.4. Consulte  [Procesamiento de imágenes mediante [!DNL Camera Raw]](/help/assets/camera-raw.md).

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a la versión 1.22.8.

* **Mejoras de accesibilidad**:

   * [!DNL Dynamic Media] proporciona muchas mejoras de accesibilidad para los visualizadores. Consulte [[!DNL Dynamic Media] actualizaciones](#dynamic-media-65100).

   * Platform proporciona algunas mejoras de accesibilidad. Consulte [Actualizaciones de plataforma](#platform-65100).

* **Mejoras** en la experiencia del usuario:

   * [!DNL Experience Manager] muestra directamente una lista de todos los modelos de contenido en una carpeta sin que los autores de contenido tengan que navegar por la estructura de archivos. La función ahora requiere menos clics y mejora la eficacia de la creación.

   * El campo de ruta en el editor [!DNL Sites] permite a los autores arrastrar recursos desde [!DNL Content Finder].

Para obtener una lista de todas las funciones y mejoras introducidas en [!DNL Experience Manager] 6.5.10.0, consulte [novedades en [!DNL Adobe Experience Manager] 6.5 Service Pack 10](new-features-latest-service-pack.md).

La siguiente es la lista de correcciones que se proporcionan en la versión [!DNL Experience Manager] 6.5.10.0.

### [!DNL Sites] {#sites-65100}

* El foco se desplaza a otro campo al escribir en el campo **[!UICONTROL Valor predeterminado]** en la pestaña **[!UICONTROL Propiedades]** del Editor de fragmentos de contenido (NPR-36992).

* Al filtrar los modelos [!DNL Content Fragment] bajo una ruta especificada, la búsqueda [!DNL Experience Manager] devuelve todos los nodos con `cq:Template` en lugar de devolver rutas y nodos solo para el modelo [!DNL Content Fragment] (SITES-1453).
* [!DNL Content Fragments] devuelve  `null` como estado de las carpetas (SITES-1157).
* [!DNL Experience Manager] no permite a los usuarios desactivar y habilitar  [!DNL Content Fragment] modelos (SITES-1088).
* Cuando un usuario mueve, cambia el nombre o elimina [!DNL Content Fragments] o los recursos multimedia, el [!DNL Content Fragments] referenciado no se actualiza automáticamente (SITES-196).
* Al pegar componentes de una página a otra, se producen errores de JavaScript (NPR-37030).
* Cuando las propiedades de página se ven rápidamente, se abren Propiedades de página para una página diferente (NPR-37025).
* El fragmento de contenido permite que el fragmento de contenido se haga referencia a sí mismo. El selector no admite la operación (NPR-36993).
* Después de actualizar al Service Pack 9, algunos usuarios no pueden mover carpetas en el Experience Manager y ver errores en los registros (SITES-1481).
* Al ajustar la anchura del componente en el contenedor de diseño en modo de edición, se observa un parpadeo (NPR-36961).
* Al promocionar un lanzamiento, los cambios en el lanzamiento promocionado se implementan dos veces en los demás lanzamientos. Si un usuario promociona el lanzamiento doble, el contenido duplicado se refleja en la página de origen (NPR-36893).
* [!DNL Experience Manager] añade un borde gris a algunas imágenes PNG con transparencia si agrega las imágenes a una página utilizando el componente principal de imagen o si cambia el tamaño con el componente Imagen base (NPR-36879).
* [!DNL Experience Manager Sites] La interfaz de usuario del administrador con un número elevado de plantillas resulta en una navegación lenta (NPR-36870).
* La actualización al Service Pack 9 impide la creación de algunos componentes. Este problema no permite a los usuarios de [!DNL Sites] crear páginas nuevas (NPR-36857).
* El método `ContextHubImpl` crea un `ResourceResolver` que no está cerrado. Genera mensajes de advertencia sobre los `ResourceResolver` de larga duración y el servicio devuelve a veces resultados inesperados (NPR-36853).
* Al sincronizar una sola Live Copy desde las propiedades de la página de modelo, también se sincronizan todos los demás Live Copies (NPR-36829, NPR-36522).
* Cuando solo se utiliza el tipo MIME XLS, la función de carga de archivos no funciona como se espera (NPR-36785).
* Las nuevas etiquetas con mayúsculas y minúsculas pascal y todas las palabras en mayúsculas no se muestran en el campo de etiqueta dentro de [!DNL Content Fragments] (NPR-36742).
* La opción Elemento de texto único al agregar [!DNL Content Fragment] hace que falte texto y crea un formato impar relacionado con listas y listas anidadas (NPR-36565).
* Cuando un autor realiza anotaciones en cualquier componente de una página, elimina el componente y deshace la operación de eliminación, se produce un error al intentar ver los datos de la línea de tiempo de la página en la consola Sitios (NPR-36528).
* Propiedades de página La opción [!UICONTROL Guardar y cerrar] del Editor por lotes guarda los cambios, pero no cierra el editor (NPR-36527).
* Cuando un usuario intenta arrastrar y soltar un nuevo componente Texto en una página, el componente desaparece inmediatamente (NPR-36442).
* Cuando un usuario escribe una etiqueta bajo demanda que incluye espacio (la etiqueta que no existe en el sistema) y presiona Intro, la etiqueta aparece bajo el campo . Sin embargo, cuando el [!DNL Content Fragment] se guarda y se vuelve a abrir, la etiqueta bajo demanda no aparece (NPR-36441).
* La plantilla no se puede eliminar cuando se accede a la instancia a través de Dispatcher (NPR-36385).
* Cuando se mueve una página, se requiere una actualización manual del explorador para procesar los cambios (NPR-36381).
* Al seleccionar un componente, puede cortarlo o copiarlo con Ctrl+X o Ctrl+C (y Comando+X o Comando+C en Mac). Al hacer clic en otro componente, puede pegar con la barra de herramientas, pero no con el teclado (Ctrl+V o Comando+V) (NPR-36379).
* Cuando un usuario intenta cortar componentes utilizando el icono de tijeras para moverlos a otro lugar, se produce un error de consola. Además, al pegar, solo se mueve un componente (NPR-36378).
* [!DNL Experience Manager] tiene una consulta sin índice en WCM o notificaciones, ralentiza el rendimiento (NPR-36303).
* Cuando un autor restaura la herencia en el componente heredado eliminado, la opción disponible es sincronizar todo el contenido de la página. Los autores de contenido deben sincronizar la página completa aunque la herencia se restaure solo en un componente. Una sincronización completa puede provocar que el contenido no deseado se sincronice (NPR-34456, CQ-4310183).
* Uso activo de un componente en la instancia de autor no muestra todas las ocurrencias. Algunos componentes se utilizan en más de 1000 páginas, pero el informe solo muestra unas 40 páginas (CQ-4323724).
* Cuando hay una estructura de sitio que tiene muchas subpáginas, la carga de las subpáginas en la vista de columna tarda más en el Experience Manager 6.5.8 que en el Experience Manager 6.4.8.2 (CQ-4322766).
* Desmarque &quot;Todo&quot; no funciona en la opción &quot;Despliegue de página&quot; (NPR-37070).
* Al abrir una versión de componente v3 existente de una página, no se abre el cuadro de diálogo Propiedades de la página y se registra un `NullPointerException` (SITES-1830).

### [!DNL Assets] {#assets-65100}

Los siguientes problemas se solucionan en [!DNL Assets]:

* El valor de la propiedad `jcr:title` no se actualiza en la instancia de publicación después de mover una carpeta. Al cambiar el nombre y volver a publicar una carpeta dentro del autor, no se actualiza el valor de la propiedad `jcr:title` de la misma en la instancia de publicación (NPR-36369).

* Si se seleccionan dos o más recursos y se editan uno o más campos de metadatos, la operación de guardado falla con el código de error 500 en el explorador Safari (NPR-36413).

* La importación masiva de metadatos falla debido a un formato de fecha incorrecto (NPR-36428).

* Cuando se realiza una selección en la página [!UICONTROL Properties] para actualizar los metadatos, la interfaz responde con lentitud cuando el esquema proporciona muchas opciones (NPR-36430).

* El filtro de búsqueda que utiliza el predicado [!UICONTROL Estado de caducidad] no funciona (NPR-36436).

* El menú emergente de varios campos de las propiedades [!UICONTROL Metadatos de carpeta] no muestra los últimos valores seleccionados (NPR-36937, CQ-4314429).

* Al buscar archivos y carpetas, si el usuario aplica un filtro y selecciona [!UICONTROL Files &amp; Folders], solo se muestran los archivos pero no la carpeta (CQ-4319543, NPR-36627).

* Las opciones de la barra de herramientas son diferentes cuando se selecciona la misma colección dentro de una carpeta y cuando se selecciona desde un resultado de búsqueda (NPR-36620).

* La opción [!UICONTROL Publicación rápida] no está disponible en la página de resultados de búsqueda (NPR-36904, CQ-4317748).

* Cuando los usuarios crean una Live Copy de un recurso sin especificar su extensión, después de la descarga el archivo de Live Copy no se puede utilizar (NPR-36903, CQ-4326305).

* Cuando se agrega un usuario como propietario de una carpeta secundaria, el usuario obtiene también el permiso de propietario de la carpeta principal y, por lo tanto, de las demás carpetas secundarias del usuario principal. Además, el usuario no se elimina como propietario de la carpeta principal al intentar eliminarla. (NPR-36801, CQ-4323737).

* [!DNL Experience Manager] genera una excepción sin memoria cuando intenta crear subrecursos para recursos compuestos, como una presentación de PowerPoint (NPR-36668).

* Cuando los usuarios mueven un recurso que ya se está utilizando en una página de sitios publicada, la página de sitios se vuelve a publicar aunque la opción de publicación no esté seleccionada (NPR-36636, CQ-4323500).

* Al utilizar la función de detección de tipo MIME de Apache Tika, los recursos cargados con el método `AssetManager.createAsset` dejan un archivo temporal denominado `apache-tika-*.tmp` en el directorio temporal. Este archivo temporal utiliza todo el espacio libre en disco disponible (NPR-36545).

* Todos los recursos protegidos por DRM se descargan y no se sigue la selección del usuario para descargar recursos específicos (CQ-4327422).

* No se pueden arrastrar recursos a `pathfield` en la interfaz de usuario (NPR-36849).

* Al seleccionar un recurso en la vista Columna, desaparece el panel de detalles del recurso (NPR-36667).

### [!DNL Dynamic Media] {#dynamic-media-65100}

**Mejoras de accesibilidad**

Las siguientes mejoras de accesibilidad están disponibles en [!DNL Dynamic Media Viewers].

* Los lectores de pantalla ahora narran el texto del marcador de posición para buscar y agregar la dirección de correo electrónico como un campo requerido en el cuadro de diálogo de recursos compartidos como vínculo, y también anuncian la información de herramientas [!UICONTROL Rellene este campo] (CQ-4327761).

* Los lectores de pantalla ahora narran correctamente los nombres y propósitos de varios campos en el [!UICONTROL Editor de ajustes preestablecidos de imagen] al acceder a los campos de la interfaz de usuario mediante el teclado (CQ-4325677).

* El foco del teclado ahora se mueve correctamente a la pestaña de búsqueda del cuadro de diálogo [!UICONTROL Ajustes preestablecidos de visor] desde el selector de recursos de la opción [!UICONTROL Tipo de medios enriquecidos] (CQ-4324736).

* Al navegar en el modo de formularios utilizando teclas de teclado, los lectores de pantalla narran las etiquetas correspondientes a las opciones de incremento y reducción en la pestaña [!UICONTROL Crear] de [!UICONTROL Ajustes preestablecidos de imagen] (CQ-4323900).

* Los lectores de pantalla ahora anuncian la opción [!UICONTROL Buscar y agregar dirección de correo electrónico] en el cuadro de diálogo Compartir recursos como un vínculo (CQ-4323352).

* El foco del teclado se mantiene en la barra de herramientas al navegar por los recursos con las teclas de teclado (CQ-4322037).

* Los lectores de pantalla ahora narran la información de campo [!UICONTROL Editar] recién añadida después de seleccionar la opción [!UICONTROL Agregar recorte] dentro del [!UICONTROL Recorte de imagen adaptable] en la página [!UICONTROL Editar perfil de procesamiento de imagen] (CQ-4290734).

* En las páginas [!UICONTROL Editar ajuste preestablecido de imagen] y [!UICONTROL Crear vídeo interactivo], los lectores de pantalla ahora anuncian correctamente el encabezado de la página al navegar por las páginas con las teclas de método abreviado del teclado de encabezado (CQ-4290730) (CQ-4290701).

* Los lectores de pantalla ahora pueden reconocer las distintas regiones de la pantalla (como la región del panel derecho, el panel izquierdo, la barra de herramientas de acciones, el punto de referencia de la barra de herramientas del visor y el punto de referencia de la imagen ampliable) mediante las teclas de método abreviado de referencia y región al navegar por las siguientes páginas.

   * [!UICONTROL Editor de ajustes preestablecidos de visualizador]  (CQ-4290729)

   * [!UICONTROL Editor de conjuntos de imágenes]  (CQ-4290710)

   * [!UICONTROL Crear vídeo interactivo]  (CQ-4290702).

* Los lectores de pantalla ahora anuncian el nombre de la opción de uso compartido en el marco del vídeo, al navegar con la tecla de flecha abajo (CQ-4290728).

* Los lectores de pantalla ahora narran los nombres de varias opciones en las pestañas [!UICONTROL Sprite] y [!UICONTROL Background] de la pestaña [!UICONTROL Aspecto] del [!UICONTROL Editor de ajustes preestablecidos de visualizador] (CQ-4290727).

* Los campos obligatorios, como el campo para editar [!UICONTROL Width], de la pestaña [!UICONTROL Básico] de la página [!UICONTROL Editar codificación de vídeo] ahora tienen un símbolo de asterisco (*) (CQ-4290725).

* Los lectores de pantalla ahora anuncian la etiqueta de las opciones en la página [!UICONTROL Perfiles de imagen] (CQ-4290723).

* Los usuarios de Windows ahora pueden salir del editor CSS expandido en [!UICONTROL Editor de ajustes preestablecidos de visualizador] cuando el foco está en el Editor CSS (CQ-4290720).

* En la ficha [!UICONTROL Básico] de [!UICONTROL Editar ajuste preestablecido de imagen] al navegar en el modo Formulario, los lectores de pantalla ahora narran las etiquetas de varios campos y opciones de edición (CQ-4290717).

* Los lectores de pantalla ahora narran la función y el estado (seleccionado o no seleccionado) para las opciones de la interfaz de usuario en la navegación izquierda en la página de detalles de los recursos (CQ-4290709).

* Los lectores de pantalla ahora narran correctamente el estado (seleccionado o no seleccionado) y el vínculo para los toggles de imagen en la pestaña [!UICONTROL Contenido] de la página [!UICONTROL Crear vídeo interactivo] (CQ-4290707).

* Los lectores de pantalla ahora narran correctamente el nombre, la función y el estado de varios segmentos en la escala de tiempo de vídeo al navegar con la tecla de flecha abajo en la página [!UICONTROL Crear vídeo interactivo] (CQ-4290706).

* Los lectores de pantalla ahora narran el nombre, la función y el estado predeterminado (seleccionado o no seleccionado) y la propiedad al navegar por las opciones en la página [!UICONTROL Crear vídeo interactivo] (CQ-4290704).

* Los lectores de pantalla ahora narran el nombre, la función y el estado predeterminado (seleccionado o no seleccionado) de las opciones en las opciones [!UICONTROL Todos los recursos] y [!UICONTROL Todas las colecciones] al navegar por la página [!UICONTROL Publicar] (CQ-4290705).

* Al cargar un formato de vídeo no admitido (que no sea MP4) en la página [!UICONTROL Crear vídeo interactivo], el Experience Manager muestra y anuncia mensajes de error (CQ-4290700).

* El contraste de los números (tiempo en segundos) en la escala de tiempo de la página [!UICONTROL Crear vídeo interactivo] ahora cumple la proporción de luminosidad mínima requerida, de modo que los usuarios con una percepción limitada del color puedan leer fácilmente (CQ-4290699).

* Los lectores de pantalla ahora anuncian la etiqueta del campo [!UICONTROL Product Name] al navegar por la página [!UICONTROL Crear vídeo interactivo] (CQ-4290697).

**Problemas solucionados**

Las siguientes correcciones de errores están disponibles en [!DNL Dynamic Media].

* Los vídeos cargados en [!DNL Experience Manager] muestran `Process failed` después de que `dynamicmedia_scene7` el modo de ejecución esté habilitado y la sincronización esté deshabilitada (CQ-4327791).

### Plataforma {#platform-65100}

En este Service Pack se implementan las siguientes mejoras:

* Cuando un usuario selecciona un elemento en la vista Árbol, los lectores de pantalla anuncian la selección y las opciones de la barra de herramientas mostradas en la parte superior (NPR-36504).
* Algunos nombres de texto y control son más fáciles de leer para los usuarios con problemas de visión, ya que la proporción de luminosidad cumple la proporción mínima requerida de 4,5:1 (NPR-36503).
* Cuando un usuario utiliza los controles de calendario, el lector de pantalla narra la información descriptiva de fecha, mes y día laborable. Cuando un usuario utiliza la tecla de método abreviado del calendario, el lector de pantalla narra el cambio en la fecha, el mes y el año (NPR-36498).
* Compatibilidad proporcionada para ejecutar JavaScript personalizado `Clientlibs` mediante las funciones de ECMAScript 6 sin cumplir con el modo estricto. Específicamente, el indicador `emitUseStrict` se agrega al `GCCScriptProcessor` (NPR-36411).

Las siguientes correcciones de errores son parte de este Service Pack:

* Las comprobaciones de estado personalizadas se ejecutan con mayor frecuencia de la programada (NPR-36985).
* El método `Resourceresolver map` devuelve un resultado incorrecto para las páginas de alias (NPR-36767).
* [!DNL Experience Manager] el inicio se retrasa debido a la carga de flujos de trabajo (NPR-36615).

### Integraciones {#integrations-65100}

* El Experience Manager deja de responder cuando el nodo principal MongoDB cambia a otro nodo (NPR-36566).
* [!DNL Sling content distribution] falla al realizar la operación de eliminación de miembros de la colección (NPR-36521, CQ-4323578).

### Interfaz de usuario {#user-interface-65100}

* El panel lateral **[!UICONTROL References]** no muestra referencias de recursos y sitios (GRANITE-35078, GRANITE-34892).

### Proyectos de traducción {#translation-65100}

* Se eliminan las subpáginas adicionales en una copia de idioma de un proyecto de traducción múltiple (NPR-36622).

### Flujo de trabajo {#workflow-65100}

* Si el servidor recibe un mensaje fuera de la oficina, informa de las alertas de memoria y deja de responder (NPR-36768).

### [!DNL Communities] {#communities-65100}

* Las páginas del sitio de la comunidad se abren en estado `LoggedIn` para usuarios invitados anónimos (NPR-36908).

* Cuando hay más de una página en la página **[!UICONTROL Community]** > **[!UICONTROL Ideas]** > **[!UICONTROL Comentarios]**, la navegación por la página no funciona (NPR-36541).

<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65100}

*
-->

### [!DNL Forms] {#forms-65100}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] lanza los paquetes de complementos una semana después de la fecha de lanzamiento programada del paquete de servicio de [!DNL Experience Manager].


### Comercio {#commerce-65100}

* El valor del campo **[!UICONTROL Published By]** mostrado es incorrecto en la vista Columna (NPR-36902).
* Cuando se despliega un catálogo, los nuevos productos se marcan incorrectamente como productos modificados (NPR-36666).
* Cuando vuelve a crear un producto eliminado, la página del producto no se vuelve a crear (NPR-36665).
* Las páginas modificadas se actualizan, pero los productos vinculados correspondientes no se actualizan en el lanzamiento del catálogo (CQ-4321409, NPR-36422).
* Los flujos de trabajo **[!UICONTROL Publicar posteriormente]** y **[!UICONTROL Cancelar publicación posterior]** no funcionan (CQ-4327679).

Para obtener información sobre las actualizaciones de seguridad, consulte la [[!DNL Experience Manager] página de boletines de seguridad](https://helpx.adobe.com/security/products/experience-manager.html).

## Instalar 6.5.10.0 {#install}

**Requisitos de configuración y más información**

* El Experience Manager 6.5.10.0 requiere el Experience Manager 6.5. Consulte [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas.
* La descarga del Service Pack está disponible en el Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* En una implementación con MongoDB y varias instancias, instale el Experience Manager 6.5.10.0 en una de las instancias de creación mediante el Administrador de paquetes.

>[!NOTE]
>
>Adobe no recomienda quitar o desinstalar el paquete [!DNL Adobe Experience Manager] 6.5.10.0.

### Instalación del Service Pack {#install-service-pack}

Para instalar el Service Pack en una instancia [!DNL Adobe Experience Manager] 6.5, siga estos pasos:

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (cuando la instancia se actualizó desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de la instalación, tome una instantánea o una copia de seguridad nueva de su instancia [!DNL Experience Manager].

1. Descargue el Service Pack desde [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip).

1. Abra Administrador de paquetes y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y haga clic en **[!UICONTROL Install]**.

1. Para actualizar el conector S3, detenga la instancia después de instalar el Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacenamiento de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del Administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que las instalaciones se realizan correctamente. Normalmente, este problema se produce en el explorador [!DNL Safari], pero puede ocurrir de forma intermitente en cualquier explorador.

**Instalación automática**

Existen dos maneras de instalar automáticamente [!DNL Experience Manager] 6.5.10.0 en una instancia de trabajo:

A. Coloque el paquete en la carpeta `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.

B. Utilice la API [HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Utilice `cmd=install&recursive=true` para instalar los paquetes anidados.

>[!NOTE]
>
>Adobe Experience Manager 6.5.10.0 no es compatible con la instalación del Bootstrap.

**Validar la instalación**

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.10.0)` en [!UICONTROL Installed Products].

1. Todos los paquetes OSGi son **[!UICONTROL ACTIVE]** o **[!UICONTROL FRAGMENT]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.3 o posterior (utilice la consola web: `/system/console/bundles`).

Para saber cuáles son las plataformas certificadas para funcionar con esta versión, consulte los [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

<!--

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to Experience Manager 6.5.10.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

UberJar para Experience Manager 6.5.10.0 está disponible en el [repositorio de Maven Central](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.10/).

Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.10.0</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar y los otros artefactos relacionados están disponibles en el Repositorio Central de Maven en lugar del Repositorio de Maven Público de Adobe (`repo.adobe.com`). El nombre del archivo principal de UberJar cambia a `uber-jar-<version>.jar`. Por lo tanto, no hay `classifier`, con `apis` como valor, para la etiqueta `dependency`.

## Funciones en desuso {#removed-deprecated-features}

A continuación se muestra una lista de funciones y capacidades que están marcadas como obsoletas con [!DNL Experience Manager] 6.5.7.0. Las funciones se marcan como obsoletas inicialmente y luego se eliminan en una versión futura. Se proporciona una opción alternativa.

Revise si utiliza una función o una capacidad en una implementación. Además, planifique cambiar la implementación para utilizar una opción alternativa.

| Área | Función | Reemplazo |
|---|---|---|
| Integraciones | La pantalla de inclusión **[!UICONTROL AEM Cloud Services]** está en desuso ya que la integración [!DNL Experience Manager] y [!DNL Adobe Target] se actualiza en Experience Manager 6.5. La integración es compatible con la API de Adobe Target Standard. La API utiliza la autenticación mediante el Adobe IMS y [!DNL Adobe I/O] y admite la función creciente de Adobe Launch para instrumentar páginas [!DNL Experience Manager] para el análisis y la personalización. El asistente de inclusión carece de relevancia funcional. | Configure las conexiones del sistema, la autenticación IMS de Adobe y las integraciones [!DNL Adobe I/O] a través de los respectivos servicios en la nube [!DNL Experience Manager]. |
| Conectores | El conector JCR de Adobe para Microsoft® SharePoint 2010 y Microsoft® SharePoint 2013 está obsoleto para Experience Manager 6.5. | N/D |

## Problemas conocidos {#known-issues}

* Si está actualizando la instancia [!DNL Experience Manager] de la versión 6.5 a la versión 6.5.10.0, puede ver `RRD4JReporter` excepciones en el archivo `error.log`. Para resolver el problema, reinicie la instancia.

* Si instala [!DNL Experience Manager] 6.5 Service Pack 10 o un Service Pack anterior en [!DNL Experience Manager] 6.5, se eliminará la copia de tiempo de ejecución del modelo de flujo de trabajo personalizado de recursos (creado en `/var/workflow/models/dam`).
Para recuperar la copia de tiempo de ejecución, Adobe recomienda sincronizar la copia en tiempo de diseño del modelo de flujo de trabajo personalizado con su copia de tiempo de ejecución mediante la API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Los usuarios pueden cambiar el nombre de una carpeta en una jerarquía en [!DNL Assets] y publicar una carpeta anidada en [!DNL Brand Portal]. Sin embargo, el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelve a publicar la carpeta raíz.

* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el Explorador de propiedades. Si se selecciona para configurar otro campo del formulario adaptable en el mismo editor, se resuelve el problema.

* Durante la instalación del Experience Manager 6.5.x.x pueden aparecer los siguientes errores y mensajes de advertencia:
   * &quot;Cuando la integración de Adobe Target se configura en Experience Manager mediante la API de Target Standard (autenticación IMS), la exportación de fragmentos de experiencias a Target provoca la creación de tipos de ofertas incorrectos. En lugar de tener que escribir &quot;Fragmento de experiencias&quot;/origen &quot;Adobe Experience Manager&quot;, Destino, se crean varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor del formulario adaptable falla cuando se utilizan funciones agregadas como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al previsualizar el recurso mediante el visor de banners de ventas.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tiempo de espera de que el cambio de registro se complete sin registrar.

## Paquetes de contenido y paquetes OSGi incluidos {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.10.0:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.10.0](assets/65100_bundles.txt)

* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.10.0](assets/65100_packages.txt)

## Sitios web restringidos {#restricted-sites}

Estos sitios web solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* Consulte [cómo ponerse en contacto con el Servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notas de la versión 6.5](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] página de producto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es)
>* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)

