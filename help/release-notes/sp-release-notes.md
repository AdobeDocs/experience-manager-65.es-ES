---
title: '[!DNL Experience Manager] Notas de la versión de service pack 6.5'
description: Notas de versión específicas de [!DNL Adobe Experience Manager] 6.5 service pack 8
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: fb1423b7ae110b8a3cf8e0e389394e9266157a9f
workflow-type: tm+mt
source-wordcount: '3360'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager] Notas de la versión de service pack 6.5  {#aem-service-pack-release-notes}

## Información de la versión {#release-information}

| Productos | [!DNL Adobe Experience Manager] 6,5 |
| -------- | ---------------------------- |
| Versión | 6.5.8.0 |
| Tipo | Versión de Service Pack |
| Fecha | 11 de marzo de 2021 |
| Descargar URL | [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## Qué incluye [!DNL Adobe Experience Manager] 6.5.8.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.8.0 incluye nuevas funciones, mejoras clave solicitadas por los clientes y mejoras de rendimiento, estabilidad y seguridad, que se han publicado desde la publicación de la versión 6.5 en abril de 2019. El Service Pack se instala en [!DNL Adobe Experience Manager] 6.5.

Las funciones y mejoras clave introducidas en [!DNL Adobe Experience Manager] 6.5.8.0 son:

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* Al utilizar la funcionalidad [Recursos conectados](/help/assets/use-assets-across-connected-assets-instances.md), ahora puede ver una lista de todas las páginas [!DNL Sites] que utilizan el recurso. Estas referencias a un recurso están disponibles en la página [!UICONTROL Propiedades] de un recurso. Esto permite a los administradores, especialistas en marketing y bibliotecarios obtener una vista completa del uso de los recursos, lo que permite un mejor seguimiento, administración y coherencia de marca.

* Al eliminar un recurso al que se hace referencia en una página web, [!DNL Experience Manager] [muestra una advertencia](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references). Puede forzar la eliminación de un recurso al que se hace referencia o comprobar y modificar las referencias que se muestran en la página [!DNL Properties] del recurso. Al hacer clic en las referencias, se abren las páginas [!DNL Sites] local y remota.

* Ordenar las páginas de Live Copy disponibles para el lanzamiento con las propiedades [!UICONTROL Name], [!UICONTROL Last modified date,] y [!UICONTROL Last rollout date].

* El repositorio integrado (Apache Jackrabbit Oak) se ha actualizado a 1.22.6. <!-- TBD: Mention the version -->

Para obtener una lista completa de las funciones y mejoras introducidas en [!DNL Experience Manager] 6.5.8.0, consulte [novedades en [!DNL Adobe Experience Manager] 6.5 Service Pack 8](new-features-latest-service-pack.md).

La siguiente es la lista de correcciones que se proporcionan en la versión [!DNL Experience Manager] 6.5.8.0.

### [!DNL Sites] {#sites-6580}

* Cuando una página se mueve al modelo, el destino de los vínculos no se actualiza (NPR-35724).
* El reproductor basado en Tizen no se autentica en determinados navegadores. El problema ocurre con los exploradores que no admiten el atributo samesite=none (NPR-35589).
* Un contenedor interactivo desbloqueado no muestra los componentes permitidos (NPR-35565).
* Cuando se crea una Live Copy de una página recién agregada, el maestro de idioma crea dos copias para cada dominio (NPR-35545).
* Bloqueo en el Registro de componentes de SCR cuando muchos subprocesos están bloqueados debido al temporizador `org.apache.felix.scr.impl.ComponentRegistry`. Como resultado, [!DNL Experience Manager] deja de responder por un tiempo indefinido (GRANITE-33125,FELIX-6252).
* Al buscar un recurso específico en el carril lateral, el resultado contiene algunos recursos que no se buscaron (NPR-35524).
* Al habilitar SSL para una instancia de Experience Manager, se elimina la ruta de contexto (NPR-35477).
* Cuando cree una lista, añada texto como primer elemento, añada una tabla como segundo elemento y añada una lista dentro de la tabla, la lista principal distorsiona (NPR-35465).
* Cuando se utilizan distintos complementos en elementos de lista consecutivos, se agrega una etiqueta <br> adicional a los elementos de lista (NPR-35464).
* Cuando una lista se coloca entre dos párrafos, no se puede añadir una tabla a la lista (NPR-35356).
* Cuando se inicia una actualización de AEM instancia de AEM 6.3 a AEM 6.5, la instancia de actualización tarda más en iniciarse (NPR-35323).
* Cuando se replica un recurso AEM que incluye un corchete (). en el nombre, la replicación falla (GRANITE-27004, NPR-35315).
* Cuando se agregan encabezados a un Editor de texto enriquecido, el botón de párrafo está desactivado (NPR-35256).
* Cuando se agrega un elemento a una lista existente, se elimina la lista contraíble o de alternancia (NPR-35206).
* Cuando se selecciona la opción Desplegar página, aparece un cuadro de diálogo con todas las Live Copies disponibles y se produce el despliegue automático. Las Live Copies de páginas se implementan en todas las regiones geográficas sin la acción del usuario (NPR-35138).
* Cuando se utiliza la opción incluir elementos secundarios, la opción Administrar publicación no enumera todas las páginas. Solo se muestran 22 páginas (NPR-35086).
* Cuando se edita una política, el componente de texto no conserva los cambios de política (NPR-35070).
* Al aplicar sangría a algunos elementos de una lista numerada, todos los elementos mantienen el mismo número, aunque la numeración debe comenzar desde 1 para los elementos con la misma sangría (CQ-4313011).
* Cuando la minificación está activada, no se puede editar ninguna página o componente. Los problemas se iniciaron después de instalar AEM Service Pack 7 6.5 (CQ-4311133).
* Los filtros de recursos y búsqueda de Omni devuelven resultados irrelevantes o inexistentes (CQ-4312322, NPR-35793).
* Cuando varias páginas acceden simultáneamente a una biblioteca de cliente, el administrador de bibliotecas HTML no carga la biblioteca de cliente. Produce una representación incorrecta de las páginas (NPR-35538).
* La ruta de contexto se elimina automáticamente al configurar un SSL en [!DNL Experience Manager] (NPR-35294).
* El administrador de paquetes no cierra la sesión de los usuarios después de hacer clic en la opción Cerrar sesión (NPR-35160).

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0  [!DNL Assets] corrige los problemas siguientes y proporciona las siguientes mejoras.

* Al restaurar una versión anterior de un recurso, el evento DamEvent.Type RESTARED no se activa en la consola OSGi (NPR-35789).
* `IndexWriter.merge` causa  `OutOfMemoryError` error, ya que la funcionalidad de etiquetado inteligente crea grandes  `/oak:index/lucene` e  `/oak:index/ntBaseLucene` índices (NPR-35651).
* Aparece un mensaje de error al intentar guardar una carpeta de tipo [!UICONTROL Contribución de recursos] con caracteres multibyte en el nombre (NPR-35605).
* Cuando se utilizan campos de subtipo de metadatos en cascada, se produce un error &quot;Por favor, rellene este campo&quot; incorrecto (NPR-35643).
* Cuando se arrastra un recurso existente en la interfaz de usuario [!DNL Assets] y se crea una versión nueva, los cambios en los metadatos no son persistentes (NPR-34940).
* Al crear reglas en el editor de esquemas de metadatos para un menú en cascada, la opción [!UICONTROL Dependiente de] repite el mismo nombre (NPR-35596).
* La búsqueda por similitudes no funciona después de editar [!UICONTROL Carril de búsqueda de administración de recursos] (NPR-35588).
* Desde una carpeta, si abre la búsqueda de recursos en el carril izquierdo haciendo clic en [!UICONTROL Filter], el filtro en [!UICONTROL Status] > [!UICONTROL Checkout] > [!UICONTROL Checked out] no funciona (NPR-35530).
* Si intenta eliminar todas las etiquetas inteligentes de un recurso y guardar los cambios, las etiquetas no se eliminarán. Sin embargo, la interfaz de usuario indica que los cambios se han guardado (NPR-35519).
* Los usuarios no pueden reorganizar u ordenar los recursos en la vista de lista en una carpeta ordenable (NPR-35516).
* Si edita el esquema de metadatos predeterminado, el campo de etiquetas de la página [!UICONTROL Properties] del recurso cambia a un campo de texto. El cambio permite que los usuarios no conscientes agreguen etiquetas bajo demanda y las etiquetas se almacenan como una cadena en el repositorio (NPR-35478).
* Al descargar un recurso, si proporciona un nombre que no tiene una dirección de correo electrónico válida, la opción de descarga no está disponible. Sin embargo, si se selecciona otra opción en el cuadro de diálogo de descarga, el botón está habilitado, pero no se envía un correo electrónico (NPR-35365).
* Los usuarios no pueden proteger los recursos después de editarlos en [!DNL Adobe InDesign] y reciben un error por falta de permisos (NPR-35341).
* La biblioteca JavaScript de controladores se actualiza a la versión 4.7.6 (NPR-35333).
* La interfaz del editor de metadatos deja de funcionar correctamente cuando se comienza con la edición de metadatos masivos y se anula la selección de elementos hasta que se mantiene seleccionado un solo elemento (NPR-35144).
* La navegación global no abre la consola correcta cuando se hace clic desde la página `assets.html` (CQ-4312311).
* [!DNL Assets] no muestra la representación RGB para un recurso que tiene representación RGB (CQ-4310190).
* La opción [!UICONTROL Relate] del menú no se muestra correctamente en la página [!UICONTROL Propiedades] (CQ-4310188).
* Si se utiliza el filtro de tipo de archivo para documentos para buscar recursos y crear una colección inteligente, el filtro no se aplica cuando se accede a la colección. En su lugar, todos los tipos de recursos se muestran en la búsqueda (NPR-35759).
* No puede arrastrar y agregar recursos en un Lightbox desde la interfaz de usuario [!DNL Assets] (NPR-35901).
* Cuando se crea una nueva versión de un recurso existente después de resolver el conflicto de nombres, los metadatos del recurso original se sobrescriben (CQ-4313594).
* Al filtrar la búsqueda de recursos mediante un filtro de búsqueda o un predicado, abrir un recurso para verlo o editarlo y volver a la página de resultados de la búsqueda, el filtro no funciona. Todos los recursos buscados aparecen sin filtrar (NPR-35913).

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* La opción URL del ajuste preestablecido de imagen RESS está habilitada en la página de detalles del recurso. Ahora, las opciones URL y RESS están disponibles en la página de detalles del recurso cuando se selecciona el ajuste preestablecido de imagen RESS en la sección representaciones dinámicas . (CQ-4311241)
* Componente de medios interactivo: el vídeo interactivo no funciona si el usuario tiene [!DNL Experience Manager] con configuración de publicación selectiva (CQ-4311054).
* Si mueve recursos entre carpetas, la sincronización entre [!DNL Experience Manager] y [!DNL Dynamic Media–Scene7] mediante API es muy lenta (CQ-4310001).
* Al utilizar Omnisearch, el tamaño de los registros aumenta significativamente (CQ-4309153).
* Cuando la sincronización selectiva está habilitada y un recurso se copia (no se mueve) en una carpeta de sincronización, no se sincroniza como se espera (CQ-4307122).
* Para los recursos cargados que se publican automáticamente en DM, el estado no se muestra Publicado en AEM. Además, la columna de estado Publicar de Dynamic Media no muestra el estado de publicación correcto (CQ-4306415).
* Si un recurso se publica en [!DNL Experience Manager] y se configura para publicar en [!DNL Dynamic Media] en la activación, el valor de metadatos `scene7FileStatus` no se actualiza según lo esperado (CQ-4308269).
* Al editar el perfil de vídeo, [!DNL Experience Manager] no muestra los valores de altura y velocidad de bits establecidos para el ajuste preestablecido de vídeo. Los campos aparecen en blanco (CQ-4311828).

### [!DNL Commerce] {#commerce-6580}

* No se puede crear una etiqueta personalizada para todos los productos en Commerce (CQ-4310682).

* La actualización de referencia de recursos de producto hace que los subprocesos de replicación estén en estado de espera hasta que el subproceso ProductAssetListener complete sus confirmaciones para el JCR (NPR-35269).

### Plataforma {#platform-6580}

* Cuando se utiliza un componente Vista de ficha de Coral sin pestañas y, a continuación, se déclencheur un validador de Foundation, se produce el siguiente error (NPR-35636):

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* La replicación de reenvío de SCD falla en los eventos de eliminación de nodos que incluyen una coma en el nombre (NPR-35191).

* Después de actualizar a AEM 6.5.7, las compilaciones empiezan a fallar. La razón es que una versión antigua o ningún jackson-core está incrustado en el uber-jar (GRANITE-33006).

### Interfaz de usuario {#ui-6580}

* Cuando se cambia de la vista de tarjeta a la vista de lista para documentos de una carpeta de la consola Recursos, la ordenación no funciona correctamente (NPR-35842).

* Cuando se crea un hipervínculo de texto en un componente de texto, la función de búsqueda no muestra los resultados adecuados (NPR-35849).

* Cuando no se proporciona un valor a un campo oculto que está marcado como obligatorio, le impide guardar un componente (NPR-35219).

### Integraciones {#integrations-6580}

* Cuando se utilizan valores diferentes para el ID del inquilino de IMS y el código del cliente de Target, [!DNL Experience Manager] no se integra con [!DNL Adobe Target] (NPR-35342).

### Proyectos de traducción {#translation-6580}

* Problemas al exportar o importar un trabajo de traducción en [!DNL Experience Manager] (NPR-35259).

### Campaign {#campaign-6580}

* Cuando crea una página de campaña utilizando una plantilla predeterminada en la interfaz de usuario táctil y abre la pestaña Correo electrónico en el cuadro de diálogo de propiedades de la página, la variable de personalización para los campos de asunto y cuerpo permanece deshabilitada (CQ-4312388).

### [!DNL Communities] {#communities-6580}

* Al agregar una estructura de página a un grupo de comunidad, el título [!UICONTROL Grupo] de la ruta de exploración se cambia al título de la primera [!UICONTROL Página] (NPR-35803).
* A diferencia de los moderadores, un miembro estándar de la comunidad no puede acceder ni editar ningún borrador del anuncio (NPR-35339).
* Se han roto el control de acceso y la denegación de servicio con DSRPReindexServlet, lo que hace que el sitio de las comunidades caiga hasta que se complete la indexación (NPR-35591).
* Al eliminar [!UICONTROL Todos los usuarios] del campo [!UICONTROL Administradores], estos no se eliminan del back-end (NPR-35592, NPR-35611).
* El componente [!UICONTROL Componer mensaje] no devuelve ningún resultado cuando el texto introducido coincide parcialmente (NPR-35666).

### [!DNL Brand Portal] {#brandportal-6580}

* Al agregar un miembro a una carpeta de tipo [!UICONTROL Contribución de recursos] , se muestra [!UICONTROL Agregar usuario o grupo] en la interfaz de usuario, aunque solo se admiten los usuarios activos de Brand Portal y no los grupos (NPR-35332).

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] lanza los paquetes de complementos una semana después de la fecha de lanzamiento programada del paquete de servicio de [!DNL Experience Manager].

**Formularios adaptables**

* Cuando inserta una tabla con una fila repetible en un panel repetible que tiene varias instancias en un formulario adaptable, la tabla siempre se añade a la primera instancia del panel (NPR-35635).

* Cuando el tab focus vuelve a alcanzar el componente CAPTCHA después de verificarlo correctamente una vez en un formulario adaptable, [!DNL Experience Manager Forms] muestra el mensaje de error `Provide Captcha phrase to proceed` (NPR-35539).

**Comunicación interactiva**

* Cuando envía un formulario traducido, los mensajes de envío se muestran en inglés y no se traducen al idioma correspondiente (NPR-35808).

* Cuando se incluye una condición de ocultado en los fragmentos de documento o XDP adjuntos, la comunicación interactiva no se carga (NPR-35745).

**Administración de correspondencia**

* Cuando edita una carta, los módulos con condiciones tardan más en cargarse (NPR-35325).

* Cuando selecciona un recurso del panel de navegación izquierdo que no está incluido en una carta y, a continuación, selecciona el siguiente recurso, el resaltado azul no se elimina del recurso seleccionado anteriormente (NPR-35851).

* Cuando edita campos de texto en una carta, [!DNL Experience Manager Forms] muestra el mensaje de error `Text Edit Failed` (CQ-4313770).

**Flujo de trabajo**

* Cuando intenta abrir un formulario adaptable en una aplicación móvil [!DNL Experience Manager Forms] para iOS, la aplicación se detiene para responder (CQ-4314825).

* La pestaña [!UICONTROL To-do] del espacio de trabajo HTML muestra caracteres HTML (NPR-35298).

**XMLFM**

* Cuando se genera un documento XML utilizando el servicio de salida, se produce el error `OutputServiceException` para algunos de los archivos XML (CQ-4311341, CQ-4313893).

* Cuando se aplica la propiedad superíndice al primer carácter de la viñeta, el tamaño de la viñeta se reduce (CQ-4306476).

* Los PDF forms generados mediante el servicio de salida no incluyen bordes (CQ-4312564).

**Diseñador**

* Al abrir un archivo XDP en [!DNL Experience Manager Forms] Designer, se genera un archivo designer.log en la misma carpeta que el archivo XDP (CQ-4309427, CQ-4310865).

**Formularios HTML5**

* Cuando selecciona una casilla de verificación en un formulario adaptable en el explorador web [!DNL Safari] para [!DNL iOS 14.1 or 14.2], no se muestran los campos adicionales (NPR-35652).

**Administración de Forms**

* No hay ningún mensaje de confirmación que indique la carga masiva correcta de archivos XDP en el repositorio CRX (NPR-35546).

**Seguridad de los documentos**

* Se han notificado varios problemas para la opción [!UICONTROL Editar directiva] en AdminUI (NPR-35747).

Para obtener información sobre las actualizaciones de seguridad, consulte la [página de boletines de seguridad del Experience Manager](https://helpx.adobe.com/security/products/experience-manager.html).

## Instalar 6.5.8.0 {#install}

**Requisitos de configuración y más información**

* El Experience Manager 6.5.8.0 requiere el Experience Manager 6.5. Consulte [documentación de actualización](/help/sites-deploying/upgrade.md) para obtener instrucciones detalladas.
* La descarga del Service Pack está disponible en el Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* En una implementación con MongoDB y varias instancias, instale el Experience Manager 6.5.8.0 en una de las instancias de autor mediante el Administrador de paquetes.

>[!NOTE]
>
>Adobe no recomienda quitar o desinstalar el paquete [!DNL Adobe Experience Manager] 6.5.8.0.

### Instale el Service Pack {#install-service-pack}

Para instalar el Service Pack en una instancia [!DNL Adobe Experience Manager] 6.5, siga estos pasos:

1. Reinicie la instancia antes de la instalación si la instancia está en modo de actualización (y este es el caso cuando la instancia se actualizó desde una versión anterior). Adobe también recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.

1. Antes de la instalación, tome una instantánea o una copia de seguridad nueva de su instancia [!DNL Experience Manager].

1. Descargue el Service Pack desde [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip).

1. Abra Administrador de paquetes y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).

1. Seleccione el paquete y haga clic en **[!UICONTROL Install]**.

1. Para actualizar el conector S3, detenga la instancia después de instalar el Service Pack, sustituya el conector existente por un nuevo archivo binario proporcionado en la carpeta de instalación y reinicie la instancia. Consulte [Almacenamiento de datos de Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>El cuadro de diálogo en la interfaz de usuario del Administrador de paquetes a veces se cierra durante la instalación del Service Pack. Adobe recomienda esperar a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete de actualización antes de asegurarse de que las instalaciones se realizan correctamente. Normalmente, esto sucede en [!DNL Safari] pero puede suceder de forma intermitente en cualquier explorador.

**Instalación automática**

Existen dos maneras de instalar automáticamente Adobe Experience Manager 6.5.8.0 en una instancia de trabajo:

A. Coloque el paquete en la carpeta `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala automáticamente.

B. Utilice la API [HTTP del Administrador de paquetes](/help/sites-administering/package-manager.md#package-share). Utilice `cmd=install&recursive=true` para instalar los paquetes anidados.

>[!NOTE]
>
>Adobe Experience Manager 6.5.8.0 no es compatible con la instalación del Bootstrap.

**Validar la instalación**

1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (6.5.8.0)` en [!UICONTROL Installed Products].

1. Todos los paquetes OSGi son **[!UICONTROL ACTIVE]** o **[!UICONTROL FRAGMENT]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

1. El paquete OSGi `org.apache.jackrabbit.oak-core` es la versión 1.22.3 o posterior (utilice la consola web: `/system/console/bundles`).

Para saber cuáles son las plataformas certificadas para funcionar con esta versión, consulte los [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

### Instalación del paquete de complementos de Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Omita este paso si no utiliza Experience Manager Forms. Las correcciones en Experience Manager Forms se entregan mediante un paquete de complementos independiente una semana después de la versión programada del Service Pack [!DNL Experience Manager].

1. Asegúrese de que ha instalado el Service Pack de Adobe Experience Manager.
1. Descargue el paquete de complementos de Forms correspondiente que aparece en las [versiones de AEM Forms](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) para su sistema operativo.
1. Instale el paquete de complementos de Forms como se describe en [Instalación de paquetes de complementos de AEM Forms](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>AEM 6.5.8.0 incluye una nueva versión de [Paquete de compatibilidad de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases). Si utiliza una versión anterior del paquete de compatibilidad de AEM Forms y actualiza a AEM 6.5.8.0, instale la versión más reciente del paquete tras la instalación del paquete de complementos de Forms.

### Instalar Adobe Experience Manager Forms en JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Omita este paso si no utiliza AEM Forms en JEE. Las correcciones en Adobe Experience Manager Forms en JEE se entregan mediante un instalador independiente.

Para obtener información sobre la instalación del instalador acumulativo para Forms Experience Manager en JEE y la configuración posterior a la implementación, consulte las [notas de la versión](jee-patch-installer-65.md).

>[!NOTE]
>
>Después de instalar el instalador acumulativo para Experience Manager Forms en JEE, instale el último paquete de complementos de Forms, elimine el paquete de complementos de Forms de la carpeta `crx-repository\install` y reinicie el servidor.

### UberJar {#uber-jar}

UberJar para Experience Manager 6.5.8.0 está disponible en el [repositorio Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.8/).

Para usar UberJar en un proyecto de Maven, consulte [cómo usar UberJar](/help/sites-developing/ht-projects-maven.md) e incluya la siguiente dependencia en el POM de su proyecto:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.8</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar y los otros artefactos relacionados están disponibles en el Repositorio Central de Maven en lugar del Repositorio de Maven Público de Adobe (`repo.adobe.com`). El nombre del archivo principal de UberJar cambia a `uber-jar-<version>.jar`. Por lo tanto, no hay `classifier`, con `apis` como valor, para la etiqueta `dependency`.

## Funciones en desuso {#removed-deprecated-features}

A continuación se muestra una lista de funciones y capacidades que están marcadas como obsoletas con [!DNL Experience Manager] 6.5.7.0. Las funciones se marcan como obsoletas inicialmente y luego se eliminan en una versión futura. Normalmente se proporciona una opción alternativa.

Revise si utiliza una función o una capacidad en una implementación. Además, planifique cambiar la implementación para utilizar una opción alternativa.

| Área | Función | Reemplazo |
|---|---|---|
| Integraciones | La pantalla de inclusión **[!UICONTROL AEM Cloud Services]** está en desuso. Con la integración de Experience Manager y Adobe Target actualizada en Experience Manager 6.5 para admitir la API de Adobe Target Standard, que utiliza la autenticación mediante IMS y E/S de Adobe, y el creciente papel de Launch de Adobe para instrumentar páginas de Experience Manager para el análisis y la personalización, el asistente de inclusión se ha vuelto funcionalmente irrelevante. | Configure las conexiones del sistema, la autenticación IMS de Adobe y las integraciones [!DNL Adobe I/O] a través de los respectivos servicios de nube de Experience Manager. |
| Conectores | El conector JCR de Adobe para Microsoft SharePoint 2010 y Microsoft SharePoint 2013 está en desuso para Experience Manager 6.5. | N/D |

## Problemas conocidos {#known-issues}

* Si está actualizando la instancia [!DNL Experience Manager] de la versión 6.5 a la versión 6.5.8.0, puede ver `RRD4JReporter` excepciones en el archivo `error.log`. Reinicie la instancia para resolver el problema.

* Si instala [!DNL Experience Manager] 6.5 Service Pack 5 o un Service Pack anterior en [!DNL Experience Manager] 6.5, se eliminará la copia de tiempo de ejecución del modelo de flujo de trabajo personalizado de recursos (creado en `/var/workflow/models/dam`).
Para recuperar la copia de tiempo de ejecución, Adobe recomienda sincronizar la copia en tiempo de diseño del modelo de flujo de trabajo personalizado con su copia de tiempo de ejecución mediante la API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Póngase en contacto con el Servicio de atención al cliente de Adobe si tiene problemas al editar y crear reglas en cascada en el [!UICONTROL Editor de Forms de Esquemas de metadatos de carpeta] y en el [!UICONTROL Editor de Forms de esquemas de metadatos] mediante el cuadro de diálogo [!UICONTROL Definir regla]. Las reglas que ya se han creado y guardado funcionan según lo esperado.

* Si se cambia el nombre de una carpeta de la jerarquía en [!DNL Experience Manager Assets] y la carpeta anidada que contiene un recurso se publica en [!DNL Brand Portal], el título de la carpeta no se actualiza en [!DNL Brand Portal] hasta que se vuelva a publicar la carpeta raíz.

* Cuando un usuario selecciona configurar un campo por primera vez en un formulario adaptable, la opción para guardar una configuración no se muestra en el Explorador de propiedades. Si se selecciona para configurar otro campo del formulario adaptable en el mismo editor, se resuelve el problema.

* Si el asistente de [!UICONTROL Configuración de recursos conectados] devuelve un mensaje de error 404 después de la instalación, vuelva a instalar manualmente los paquetes `cq-remotedam-client-ui-content` y `cq-remotedam-client-ui-components` mediante el Administrador de paquetes.

* Durante la instalación del Experience Manager 6.5.x.x pueden aparecer los siguientes errores y mensajes de advertencia:
   * &quot;Cuando la integración de Adobe Target se configura en Experience Manager mediante la API de Target Standard (autenticación IMS), la exportación de fragmentos de experiencias a Target provoca la creación de tipos de ofertas incorrectos. En lugar de tener que escribir &quot;Fragmento de experiencias&quot;/origen &quot;Adobe Experience Manager&quot;, Destino, se crean varias ofertas con el tipo &quot;HTML&quot;/origen &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La validación del lado del servidor del formulario adaptable falla cuando se utilizan funciones agregadas como SUM, MAX y MIN (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: no se encontraron ventanas de mantenimiento en granite/operations/maintenance.
   * La zona interactiva de una imagen interactiva de Dynamic Media no está visible al previsualizar el recurso mediante el visor de banners de ventas.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tiempo de espera de que el cambio de registro se complete sin registrar.

## Los paquetes OSGi y los paquetes de contenido están incluidos {#osgi-bundles-and-content-packages-included}

Los siguientes documentos de texto enumeran los paquetes OSGi y los paquetes de contenido incluidos en [!DNL Experience Manager] 6.5.8.0:

* [Lista de paquetes OSGi incluidos en Experience Manager 6.5.8.0](assets/6580_bundles.txt)

* [Lista de paquetes de contenido incluidos en Experience Manager 6.5.8.0](assets/6580_packages.txt)

## Sitios web restringidos {#restricted-sites}

Estos sitios web solo están disponibles para los clientes. Si es un cliente y necesita obtener acceso, póngase en contacto con su administrador de cuentas de Adobe.

* [Descarga de productos en licensing.adobe.com](https://licensing.adobe.com/)
* Consulte [cómo ponerse en contacto con el Servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notas de la versión 6.5](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] página de producto](https://www.adobe.com/es/marketing/experience-manager.html)
>* [[!DNL Experience Manager] Documentación de 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es)
>* [Suscripción a las actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html)

