---
title: Introducción a la administración de formularios
seo-title: Introducción a la administración de formularios
description: AEM Forms proporciona herramientas para administrar Forms adaptable y recursos relacionados. Este artículo le presenta las funciones clave de administración de formularios y los elementos de la interfaz de usuario.
seo-description: AEM Forms proporciona herramientas para administrar Forms adaptable y recursos relacionados. Este artículo le presenta las funciones clave de administración de formularios y los elementos de la interfaz de usuario.
uuid: 2275a0b6-b31e-4d8e-8154-ccdfff3705aa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: c0e4c9bb-e12a-4f9a-a8fa-1a8ad41d3995
docset: aem65
translation-type: tm+mt
source-git-commit: 8d352255ace00499412a21564f45f61f45060f4d
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 1%

---


# Introducción a la administración de formularios {#introduction-to-managing-forms}

AEM [!DNL Forms] proporciona una interfaz de usuario simplificada pero potente para crear y administrar formularios, documentos, temáticas, letras, fragmentos de documento, diccionarios de datos y recursos relacionados. Ayuda a administrar el ciclo de vida completo de los formularios, documentos y recursos relacionados, desde el escritorio de un desarrollador hasta la oferta en un servidor de portal para usuarios finales. Puede utilizar la interfaz de usuario AEM [!DNL Forms] para:

* Acceso a componentes AEM [!DNL Forms]
* Acceso a AEM [!DNL Forms] configuraciones

>[!NOTE]
>
>Para obtener información detallada sobre otras herramientas y opciones de AEM, consulte [Creación](/help/sites-authoring/author.md).

## Acceso a los componentes de AEM Forms {#access-aem-forms-components}

Junto con las opciones para crear formularios, documentos y recursos relacionados, AEM proporciona opciones para crear sitios, recursos, administrar una instancia de AEM, etc. Puede hacer clic en el logotipo del Experience Manager ![adobeexperimentencemanager](assets/adobeexperiencemanager.png) para navegar a todas las herramientas disponibles. Junto con los vínculos a las consolas de otros componentes, también contiene vínculos para AEM [!DNL Forms]. Para desplazarse a AEM [!DNL Forms], haga clic en el logotipo del Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > ![brújula](assets/compass.png) de navegación > **[!UICONTROL Forms]**. Se muestran los vínculos de las siguientes consolas:

* Formularios y documentos
* Temas
* Cartas
* Fragmentos de documento
* Diccionarios de datos

   ![AEM Forms Console](assets/aem_forms_console_new.png)

### Formularios y documentos  {#forms-documents}

Forms &amp; Documentos proporciona opciones para crear una comunicación interactiva, un formulario adaptable, un fragmento de formulario adaptable y un conjunto de formularios. Solo para AEM [!DNL Forms] en JEE, Forms &amp; Documentos ofrece la opción de importar archivos desde el almacenamiento local y sincronizar AEM [!DNL Forms] recursos con Workbench.

El botón Crear es el punto de partida del proceso de creación o carga de AEM [!DNL Forms] recurso. Proporciona opciones para crear:

* **Comunicación** interactiva: Una comunicación interactiva es una correspondencia digital, una declaración o un documento basados en HTML personalizada, interactiva y compatible con el dispositivo. Las comunicaciones interactivas son de naturaleza interactiva y cambian el diseño y el diseño automáticamente en función del dispositivo y la configuración del usuario. Para obtener información detallada, consulte Información general sobre comunicaciones [interactivas](/help/forms/using/interactive-communications-overview.md)

* **Formulario adaptable:** Un formulario adaptable es un formulario atractivo y adaptable. Puede crear un formulario adaptable para adaptarse dinámicamente a las entradas del usuario agregando o eliminando secciones de formulario basadas en la respuesta del usuario, el dispositivo o el entorno de trabajo. El artículo [Introducción a la creación de formularios](../../forms/using/introduction-forms-authoring.md) adaptables proporciona información detallada sobre los formularios adaptables.

* **Fragmento de formulario adaptable:** Aunque cada formulario está diseñado para un propósito específico, hay algunos segmentos comunes en la mayoría de las formas, como proporcionar detalles personales como nombre y dirección, detalles de familia, detalles de ingresos, etc. Puede crear un recurso individual para estas secciones. Estos segmentos reutilizables independientes se denominan fragmentos de formulario adaptables. Para obtener información detallada, consulte el artículo Fragmentos [de formulario](../../forms/using/adaptive-form-fragments.md) adaptables.

* **Conjunto de formularios:** Un conjunto de formularios es una colección de formularios HTML5 agrupados y presentados como un único conjunto de formularios para los usuarios finales. Cuando los usuarios finales inicio rellenar un conjunto de formularios, estos se pasan sin problemas de un formulario a otro. Al final, un usuario puede enviar todos los formularios, como una sola entidad, con un solo clic. Para obtener información detallada, consulte Conjunto [de formularios en AEM Forms](../../forms/using/formset-in-aem-forms.md).

* **Carpeta:** AEM [!DNL Forms] interfaz de usuario utiliza carpetas para organizar los recursos. Admite dos tipos de carpetas:

   * **Carpeta general:** Estas carpetas se utilizan para los recursos creados en AEM [!DNL Forms] interfaz de usuario. Estas carpetas no tienen una estructura de carpetas estricta. Puede cambiar el nombre, crear subcarpetas y almacenar formularios adaptables, comunicaciones interactivas, fragmentos de formulario adaptables, plantillas de formulario (XDP), PDF forms, Documentos y recursos relacionados en estas carpetas.
   * **Forms Workflow:** Las carpetas de flujo de trabajo de Forms se crean cuando se migran los procesos de Workbench (archivos de LiveCycle) y se sincronizan con AEM interfaz de [!DNL Forms] usuario. No se permite cambiar el nombre, crear una subcarpeta, crear una comunicación interactiva, un fragmento de formulario adaptable o una comunicación interactiva. Tampoco se le permite eliminar una carpeta de versión ni crear y cargar un formulario adaptable, un fragmento de formulario adaptable o una comunicación interactiva en paralelo a la carpeta de la versión.

   ![carpetas](assets/folders.png)

   **A.** Carpeta general **B.** Forms Workflow

El panel Forms y Documento también ofrece opciones para:

* **Importar archivos desde almacenamiento local:** Puede importar PDF forms y Documentos, plantillas de formulario (formularios XFA) y otros recursos (esquema de imagen y XML para XSD). Para obtener instrucciones paso a paso, consulte [Importación y exportación de recursos a AEM Forms](../../forms/using/import-export-forms-templates.md).
* **Sincronizar recursos de AEM Forms con Workbench:** Puede utilizar la opción Archivos de Workbench para sincronizar recursos entre la interfaz de usuario de AEM Forms y Workbench. Garantiza que todos los recursos estén disponibles en AEM [!DNL Forms] interfaz de usuario y en la selección de recursos del repositorio crx de Workbench.

### Temas  {#themes}

Un tema contiene detalles de estilo para componentes y paneles. Las temáticas tienen una identidad independiente. Por lo tanto, puede reutilizar un tema en varios formularios adaptables. Puede especificar estilos para un componente o modificar las propiedades CSS de los distintos componentes utilizados en los formularios. Los estilos incluyen propiedades como colores de fondo, colores de estado, transparencia y tamaño. Puede guardar las personalizaciones en un tema y colocarlas en componentes del formulario como un ajuste preestablecido. Al agregar el tema al formulario, el estilo especificado se refleja en los componentes correspondientes del formulario. Con AEM 6.2 [!DNL Forms], puede crear temáticas y aplicarlas a los formularios.

Para obtener información sobre la creación y el uso de temáticas, consulte [Temáticas en AEM Forms](../../forms/using/themes.md).

### Cartas  {#letters}

Una carta AEM [!DNL Forms] es una correspondencia segura, personalizada e interactiva. Puede utilizar AEM [!DNL Forms] para reunir rápidamente letras (también conocidas como correspondencias) de contenido preaprobado y de creación personalizada en un proceso simplificado.

Para obtener información sobre la creación y el uso de letras, consulte [Creación de cartas](../../forms/using/create-letter.md).

### Fragmentos de documento {#document-fragments}

Los fragmentos de documento son partes reutilizables o componentes de una correspondencia que permite componer letras. Los fragmentos de documento son de tipo texto, lista, condición y fragmento de diseño. Para obtener información sobre la creación y el uso de fragmentos de documento, consulte [Creación de fragmentos](/help/forms/using/document-fragments.md)de documento.

### Diccionarios de datos {#data-dictionaries}

Normalmente, los usuarios empresariales no necesitan conocer las representaciones de metadatos como XSD (esquema XML) y clases Java. Sin embargo, generalmente requieren acceso a estas estructuras y atributos de datos para generar soluciones. AEM [!DNL Forms] utiliza un diccionario de datos que permite a los usuarios comerciales utilizar información de fuentes de datos back-end sin conocer detalles técnicos sobre sus modelos de datos subyacentes.

Para obtener más información sobre la creación y el uso de diccionarios de datos, consulte el artículo Creación de diccionarios [de datos](../../forms/using/data-dictionary.md)

## Acceso a AEM [!DNL Forms] configuraciones {#accessing-aem-forms-configurations}

AEM panel de herramientas contiene herramientas para varios componentes. Para navegar a las herramientas específicas de AEM Forms, haga clic en el logotipo de Experience Manager ![adobeexperience emanager](assets/adobeexperiencemanager.png) > ![martillo](assets/hammer.png) de herramientas > **[!UICONTROL Forms]**. Se muestran las herramientas para realizar las siguientes funciones:

* **Configurar carpeta vigilada:** Un administrador puede configurar una carpeta de red, conocida como carpeta vigilada, para que cuando un usuario coloque un archivo (como un archivo PDF) en la carpeta vigilada, se inicie una operación preconfigurada y se manipule el archivo. Para obtener información detallada, consulte [Creación y configuración de una carpeta](/help/forms/using/creating-configure-watched-folder.md)vigilada.
* **Configurar el servicio sin conexión de la aplicación de Forms:** El servicio sin conexión de la aplicación AEM [!DNL Forms] almacena en caché las rutas o direcciones URL de los recursos utilizados en un formulario. El almacenamiento en caché de rutas o direcciones URL de los recursos utilizados en un formulario mejora el rendimiento en el servidor. Para configurar el componente sin conexión del lado del servidor de la aplicación de AEM Forms, consulte [Trabajo en modo](/help/forms/using/work-offline-mode.md)sin conexión.

   ![Herramientas de AEM Forms](assets/aem_forms_tools_new.png)

* **Configurar generador de PDF:** Un administrador puede configurar AEM [!DNL Forms] generador de PDF, agregar cuentas de usuario e importar o exportar la configuración al generador de PDF.
* **Publicar recursos de gestión de correspondencia:** AEM [!DNL Forms] le permite publicar todas las letras, fragmentos de Documento y diccionarios de datos, así como las dependencias relacionadas, de una instancia de autor a la vez. Los recursos publicados incluyen todos los recursos de Correspondence Management y las dependencias relacionadas. Para obtener información detallada, consulte [Publicación y cancelación de la publicación de formularios y documentos](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets).
* **Exportar recursos de gestión de correspondencia:** Puede descargar todos los recursos de Correspondence Management y las dependencias relacionadas como un paquete desde una [!DNL Forms] instancia de AEM. Para obtener información detallada, consulte [Importación y exportación de recursos a AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## Elementos comunes de la interfaz de usuario {#commonelements}

* **Carril izquierdo:** Puede hacer clic en el icono del carril izquierdo ![Railleftpng](assets/railleftpng.png) para mostrar las capacidades Línea de tiempo y Referencias de AEM [!DNL Forms].

   * **Línea de tiempo:** Puede agregar comentarios y realizar vistas en un recurso que se pueda revisar en la línea de tiempo. Para obtener instrucciones detalladas, consulte [Creación y gestión de revisiones de recursos en formularios](../../forms/using/create-reviews-forms.md).
   * **Referencias:** Un recurso AEM [!DNL Forms] se puede utilizar en varios AEM [!DNL Forms] . Por ejemplo, un fragmento de documento se puede utilizar en varias letras. Referencias es una lista de recursos (otros formularios o recursos) en los que se utiliza el recurso seleccionado y también la lista de otros recursos que utiliza el recurso seleccionado.

* **Rutas de exploración:** Una ruta de exploración representa el título de la consola o carpeta actual. Puede hacer clic en la opción Ruta de exploración para navegar entre el nivel de carpetas que están en una jerarquía superior.
* **Conmutador de vistas:** Puede hacer clic en la ![lista](assets/viewlist.png) de vistas del icono del conmutador de Vistas o en la ![tarjeta](assets/viewcard.png) de visualización para cambiar rápidamente entre la lista y la vista de la tarjeta. Para obtener más información sobre los componentes comunes de la interfaz de usuario, consulte [Creación](/help/sites-authoring/author.md).
* **Buscar:** La ![búsqueda](assets/search.png) de opciones de búsqueda permite encontrar rápidamente y saltar al contenido y las herramientas que necesita. Escriba el nombre del contenido o la capacidad del producto y seleccione entre las sugerencias; por ejemplo, escriba &quot;Documentos&quot; para buscar rápidamente y navegar a la consola **[!UICONTROL Forms &amp; Documentos]** o Fragmentos de Documento. Para obtener más información sobre la búsqueda, consulte AEM artículo de [búsqueda](/help/sites-authoring/search.md) 6.2

* **Barra de herramientas** Acciones: Al seleccionar un recurso, la barra de herramientas de acciones aparece encima de la lista de recursos. Contiene todas las herramientas de administración del recurso seleccionado. Puede situar el cursor sobre un icono de herramienta para vista de la información sobre herramientas que describe su funcionalidad

>[!NOTE]
>
>Cuando un usuario realiza una búsqueda en cualquier consola de Forms y Documentos, el carril solo contiene **Filtros y opciones**. Puede utilizar Filtros y opciones para realizar búsquedas avanzadas.

* **Barra de herramientas** Acciones: Al seleccionar un recurso, la barra de herramientas de acciones aparece encima de la lista de recursos. Contiene todas las herramientas de administración del recurso seleccionado. Puede situar el cursor sobre un icono de herramienta para vista de la información sobre herramientas que describe su funcionalidad

   ![Barra de herramientas de acciones para un formulario adaptable](assets/action_toolbar_new.png)

   Barra de herramientas de acciones para un formulario adaptable
