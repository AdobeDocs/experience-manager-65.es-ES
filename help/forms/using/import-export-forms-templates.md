---
title: Importación y exportación de recursos a AEM Forms
seo-title: Importing and exporting assets to AEM Forms
description: Puede importar y exportar formularios y plantillas adaptables desde y hacia AEM instancias. Esto ayuda a migrar formularios o a moverlos a través de sistemas.
seo-description: You can import and export adaptive forms and templates from and in to AEM instances. This helps in migrating forms or moving them across systems.
uuid: 937daedd-56f3-4e02-b695-b194b494d9bf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 69210727-dde3-495a-87b7-2e8173e6b664
docset: aem65
role: Admin
exl-id: b5f6a54e-92d1-4631-a1d1-184f37d174b6
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2516'
ht-degree: 39%

---

# Importación y exportación de recursos a AEM Forms{#importing-and-exporting-assets-to-aem-forms}

Puede mover formularios y recursos relacionados, temas, diccionarios de datos, fragmentos de documentos y letras entre distintas instancias de AEM Forms. Este movimiento es necesario cuando se migran sistemas o se mueven formularios de un servidor de etapa a un servidor de producción. Para los recursos para los que se admite la carga y la importación mediante la interfaz de usuario de AEM Forms, el uso de la interfaz de usuario de Forms es la forma recomendada de exportar o importar. No se recomienda utilizar el administrador de paquetes de AEM para exportar o importar estos recursos.

>[!NOTE]
>
>* En AEM 6.4 Forms, la estructura y las rutas del repositorio crx han cambiado. Si importa recursos de una versión anterior a AEM 6.4 Forms y el formulario tiene algunas dependencias con la estructura anterior, debe exportar manualmente las dependencias. Para obtener detalles de los cambios en la estructura y las rutas del repositorio, consulte [Reestructuración del repositorio en AEM](/help/sites-deploying/repository-restructuring.md).
>


## Descargar o cargar recursos de formularios y documentos {#download-or-upload-forms-amp-documents-assets}

La interfaz de usuario de AEM Forms permite exportar recursos desde una instancia de AEM descargándolos como paquete CRX de AEM o archivos binarios. A continuación, puede importar el paquete CRX de AEM descargado o el archivo binario en otra instancia de AEM.

La exportación e importación a través de la interfaz de usuario de AEM Forms es compatible con todos los recursos, excepto con las plantillas de formulario adaptable y las directivas de contenido de formulario adaptable. Por lo tanto, al exportar un formulario adaptable desde la interfaz de usuario de AEM Forms, la plantilla de formulario adaptable y las políticas de contenido relacionadas no se exportan automáticamente como otros recursos relacionados.

Para estos tipos de recursos, debe utilizar el administrador de paquetes de AEM para crear un paquete CRX en el servidor de AEM fuente e instalar el paquete en el servidor de destino. Para obtener información sobre cómo crear e instalar paquetes, consulte [Uso de paquetes](/help/sites-administering/package-manager.md).

### Descargar recursos de formularios y documentos {#download-forms-amp-documents-assets}

Para descargar recursos de formularios y documentos:

1. Inicie sesión en la instancia de AEM Forms.
1. Pulse en el icono de Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > Navegación ![icono de brújula](assets/compass.png) > Formularios > Formularios y documentos.
1. Seleccione los recursos de los formularios y pulse en el icono **Descargar**.
1. En Descargar recursos, elija una de las siguientes opciones y pulse **Descargar**.

   * **Descargar como paquete CRX:** Utilice la opción para descargar y mover todos los recursos seleccionados y las dependencias relacionadas de una instancia de AEM Forms a otra. Descarga todos los recursos y carpetas como un paquete crx. Cualquier recurso de formulario, incluidos los formularios creados en AEM (formularios adaptables, comunicaciones interactivas y fragmentos de formulario adaptables), conjuntos de formularios, plantillas de formulario, documentos de PDF y recursos (XSD, XFS, imágenes) se puede descargar como paquete desde la interfaz de usuario de AEM Forms.
La ventaja de descargar recursos como un paquete es que también descarga recursos que el recurso seleccionado para descargar ha utilizado. Por ejemplo, si tiene un formulario adaptable que utiliza una plantilla de formulario, XSD y una imagen. Al seleccionar este formulario adaptable y descargarlo como paquete, el paquete descargado también contiene la plantilla de formulario, XSD y la imagen. También se descargan todas las propiedades de metadatos (incluidas las propiedades personalizadas) asociadas al recurso.

   * **Descargar recursos como archivos binarios:** Utilice la opción para descargar solo plantillas de formulario (XDP), PDF forms (PDF), documento (PDF) y recursos (imágenes, esquemas, hojas de estilo). Puede editar estos recursos con aplicaciones externas. Descarga los recursos de formularios que poseen binarios, como XSD, XDP, imágenes, PDF y XDP como un archivo .zip. 
No puede descargar formularios adaptables, comunicaciones interactivas, fragmentos de formularios adaptables, temas y conjuntos de formularios con **Descargar recursos como archivos binarios** . Para descargar estos recursos, debe utilizar la opción **Descargar como paquete CRX**.

   Los recursos seleccionados se descargan como un archivo (archivo .zip).

   >[!NOTE]
   >
   >Tanto el paquete de AEM como los archivos binarios se descargan como un archivo (archivo .zip). Las plantillas de los recursos no se descargan junto con los recursos. Debe exportar las plantillas de recursos por separado.

### Cargar recursos de Forms y documentos {#upload-forms-amp-documents-assets}

Para cargar recursos de formularios y documentos:

>[!VIDEO](https://vimeo.com/)

1. Inicie sesión en la instancia de AEM Forms.
1. Pulse en el icono de Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > Navegación ![icono de brújula](assets/compass.png) > Formularios > Formularios y documentos.
1. Pulse **Crear** > **Cargar archivo**. Aparecerá un cuadro de diálogo para cargar formularios o paquetes.
1. En el cuadro de diálogo, examine y seleccione el paquete o el archivo que desea importar. También puede seleccionar documentos PDF, XSD, imágenes, hojas de estilo y formularios XDP. Pulse **Abrir**. La carpeta o el nombre de archivo que seleccione no deben incluir caracteres especiales.

   En el cuadro de diálogo, compruebe los detalles de los recursos que se están cargando y pulse **Cargar**.

   En caso de que cargue un recurso de formularios existente, este se actualizará.

   >[!NOTE]
   >
   >La carga de un paquete no reemplaza la jerarquía de carpetas existente. Por ejemplo, si tiene un formulario adaptable llamado &quot;Formación&quot; en la ubicación /content/dam/formsanddocuments en un servidor. El formulario adaptable se descarga y se carga en otro servidor. El segundo servidor también tiene una carpeta llamada “Aprendizaje” en la misma ubicación /content/dam/formsanddocuments. La carga falla.

## Descargar o cargar una temática {#downloading-or-uploading-a-theme}

Con AEM Forms, puede crear, descargar o cargar temas. Se crea una temática como otros recursos, como formularios, documentos y cartas. Puede crear una temática, descargarla y cargarla en una instancia independiente para reutilizarla. Para obtener más información sobre los temas, consulte [Temas en AEM Forms](../../forms/using/themes.md).

### Descargar una temática {#downloading-a-theme}

Puede exportar temas en AEM Forms que puede usar en otros proyectos o instancias. AEM le permite descargar una temática como archivo zip, que puede cargar en la instancia.

Para descargar una temática:

1. Inicie sesión en la instancia de AEM Forms.
1. Pulse en el icono de Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > Navegación ![icono de brújula](assets/compass.png) > Formularios > Temáticas.
1. Seleccione la temática y pulse **Descargar**. La temática se descarga como archivo (archivo .zip).

### Cargar una temática {#uploading-a-theme}

Puede utilizar las temáticas creadas con ajustes preestablecidos de estilo en su proyecto. Puede importar paquetes de temáticas que otros creen cargándolos en su proyecto.

Para cargar una temática:

1. En Experience Manager, vaya a **Formularios > Temáticas**.
1. En la página Temáticas, haga clic en **Crear > Cargar archivo**.
1. En la solicitud de carga de archivos, examine y seleccione un paquete de temáticas en el equipo y haga clic en **Cargar**. 
La temática cargada está disponible en la página de temáticas.

1. Inicie sesión en la instancia de AEM Forms.
1. Pulse en el icono de Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > Navegación ![icono de brújula](assets/compass.png) > Formularios > Temáticas.
1. click **Crear** > **Carga de archivo**. En la solicitud de carga de archivos, examine y seleccione un paquete de temáticas en el equipo y haga clic en **Cargar**. Se carga la temática.

## Importar y exportar recursos en la gestión de correspondencia {#import-and-export-assets-in-correspondence-management}

Para compartir recursos, como diccionarios de datos, cartas y fragmentos de documentos, entre dos implementaciones diferentes de Gestión de correspondencia, puede crear y compartir archivos .cmp. Un archivo .cmp puede incluir uno o más diccionarios de datos, letras, fragmentos de documento y formularios.

### Exportar fragmentos de documento, letras y/o diccionarios de datos {#export-document-fragments-letters-and-or-data-dictionaries}

1. En las páginas letras, fragmentos de documento o diccionario de datos, pulse y seleccione los recursos que desea exportar a un solo paquete y, a continuación, pulse Cola para descarga. Los recursos están alineados para su exportación.
1. Si es necesario, repita el paso anterior para agregar letras, fragmentos de documento y diccionarios de datos.
1. Toque **Descargar**.
1. La gestión de correspondencia muestra el cuadro de diálogo Descargar recursos con una lista de recursos de la lista de exportación.

   ![exportar](assets/export.png)

1. Para ver las dependencias que se exportan, pulse Resolver. O pase al siguiente paso. Incluso si no toca la resolución, las dependencias se exportan.
1. Para descargar el archivo .cmp, pulse **OK**.
1. Correspondence Management descarga un archivo .cmp en el equipo.

   El archivo .cmp incluye los recursos exportados. Puede compartir el archivo .cmp con otros usuarios. Otros usuarios pueden importar el archivo .cmp en un servidor diferente para obtener todos los recursos en el nuevo servidor.

### Exportar todos los recursos de la gestión de correspondencia como un paquete {#export-all-the-correspondence-management-assets-as-a-package}

Utilice esta opción para descargar todos los recursos de Gestión de correspondencia y dependencias relacionadas como paquete desde una instancia de formularios AEM.

Por ejemplo, si Gestión de Correspondencia tiene una carta que utiliza una imagen y un texto, el paquete descargado también contiene la imagen y el texto relacionados con la carta. También se descargan todas las propiedades de metadatos (incluidas las propiedades personalizadas) asociadas al recurso. Una vez que haya descargado el paquete (.cmp), puede [importar el paquete a otra instancia de AEM Forms](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

Para descargar todos los recursos de Gestión de Correspondencia y las dependencias relacionadas como paquete, complete los siguientes pasos:

1. Inicie sesión en el servidor de AEM Forms como usuario de formularios.
1. Toque **Adobe Experience Manager** en la barra de navegación global.
1. Toque las herramientas ( ![herramientas](assets/tools.png)) y, a continuación, toque **Forms**.
1. Toque **Exportar recursos de gestión de correspondencia**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( &quot;La página Exportar todos los activos de gestión de correspondencia aparece y muestra la información sobre la última vez que se intentó el proceso de exportación y un vínculo para descargar el último paquete exportado correctamente.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Toque **Exportar** y, en el mensaje de confirmación, pulse **OK**.

   Una vez completado un proceso por lotes, se actualizan los detalles de la última ejecución y el vínculo para descargar el paquete. Incluye información como el inicio de sesión del administrador y si el lote se ejecuta correctamente o no. Los recursos se exportan a un paquete y aparece el vínculo Descargar paquete exportado .

   >[!NOTE]
   >
   >El proceso Exportar todos los recursos no se puede cancelar una vez iniciado. Además, mientras la operación de exportación está en curso, no cree, elimine, modifique ni publique ningún recurso ni inicie el proceso Publicar todos los recursos.a

1. Toque . **Descargar paquete exportado** para descargar el archivo del paquete.

   Para añadir los activos del paquete a otra instancia de Gestión de Correspondencia, [importar el paquete a una instancia de AEM Forms](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

### Importar fragmentos de documento, letras y/o diccionarios de datos en la gestión de correspondencia {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

Puede importar recursos que se exporten a un archivo .cmp. Un archivo .cmp puede tener una o más letras, diccionarios de datos, fragmentos de documentos y recursos dependientes.

>[!NOTE]
>
>Al importar recursos antiguos de la gestión de correspondencia para la migración, inicie sesión con una cuenta de administrador. Para obtener más información sobre la migración de activos antiguos de la administración de correspondencia, consulte [Migración de recursos de Gestión de correspondencia a formularios AEM 6.1](/help/forms/using/migration-utility.md).

1. En la página del diccionario de datos, letras o fragmentos de documento, pulse **Crear > Carga de archivo** y seleccione el archivo .cmp.
1. La gestión de correspondencia muestra el cuadro de diálogo Importar recursos con la lista de recursos que se importan. Toque **Importar**.

   Después de importar los recursos, las siguientes propiedades de los recursos se actualizan, mientras que las demás propiedades siguen siendo las mismas:

   * Autor: Muestra el ID del usuario que importó el recurso al servidor
   * Modificado: Hora a la que se importó el recurso al servidor

   >[!NOTE]
   >
   >Para poder cargar XDP (como parte del archivo cmp o de otro modo), debe formar parte del grupo de usuarios avanzados de formularios. Para obtener derechos de acceso, póngase en contacto con el administrador.

## Exportar una aplicación de flujo de trabajo {#export-a-workflow-application}

Puede utilizar el administrador de paquetes de AEM para exportar aplicaciones de flujo de trabajo. El procedimiento es el siguiente:

1. Abra el administrador de paquetes de AEM Forms. La URL del gestor de paquetes es https://&lt;server>:&lt;port>/crx/packmgr.
1. Haga clic en **[!UICONTROL Crear paquete]**. Se abre el cuadro de diálogo **[!UICONTROL Nuevo paquete]**.
1. Especifique el nombre, la versión y el grupo para el paquete. Haga clic en **[!UICONTROL Aceptar]**.
1. Haga clic en **[!UICONTROL Editar]** y abra la pestaña **[!UICONTROL Filtros]**. Haga clic en **[!UICONTROL Añadir filtro]**. Especifique la ruta de la aplicación de flujo de trabajo. Por ejemplo: /etc/fd/dashboard/startpoints/homemortgage. Haga clic en **[!UICONTROL Añadir regla]**.

1. Abra la pestaña **[!UICONTROL Avanzado]**. Seleccione **[!UICONTROL Combinar]** o **[!UICONTROL Sobrescribir]** en el campo Administrar ACL. Haga clic en **[!UICONTROL Guardar]**.
1. Haga clic en **[!UICONTROL Generar]** para crear el paquete.

   Una vez generado el paquete, puede descargarlo e importarlo al otro servidor. La aplicación de flujo de trabajo aparece en el servidor donde se carga el paquete.

   >[!NOTE]
   >
   >Para que la aplicación de flujo de trabajo funcione correctamente, exporte también el formulario adaptable y el modelo de flujo de trabajo correspondientes con la aplicación de trabajo.

## Carpetas y organización de recursos {#folders-and-organizing-assets}

La interfaz de usuario de AEM Forms utiliza carpetas para organizar los recursos. Estas carpetas se utilizan para organizar los recursos creados en la interfaz de usuario de AEM Forms. Puede cambiar el nombre, crear subcarpetas y almacenar recursos y documentos en estas carpetas. La organización de documentos y recursos en una carpeta permite agrupar los archivos para facilitar la administración. Puede seleccionar una carpeta y elegir descargarla o eliminarla.

Para crear una carpeta, complete los siguientes pasos:

### Cree una carpeta. {#create-a-folder}

1. Inicie sesión en la interfaz de usuario de AEM Forms en `https://<server>:<port>/aem/forms.html`.
1. Vaya a la ubicación en la que desea crear una carpeta.
1. Pulse Crear > Carpeta.
1. Introduzca la siguiente información:

   * **Título:** Nombre para mostrar de la carpeta
   * **Nombre:** *(Obligatorio)* El nombre del nodo en el que desea almacenar la carpeta en el repositorio

   >[!NOTE]
   >
   >De forma predeterminada, el valor del campo de nombre se rellena automáticamente a partir del título. El nombre solo puede contener caracteres alfanuméricos o los caracteres especiales guion (-) y guion bajo (_). Cualquier otro carácter especial especificado en el título se reemplaza automáticamente por un guion y se le solicita que confirme el nuevo nombre. Puede elegir continuar con el nombre sugerido o editarlo más adelante.

1. Se muestra una nueva carpeta con el título que haya definido en la ubicación actual de la lista de recursos.

   Si existe una carpeta con el nombre especificado, el envío falla con un error. Puede ver el mensaje de error pasando el puntero sobre el icono de error ![aem6forms_error_alert](assets/aem6forms_error_alert.png) que aparece junto al campo de nombre.

   Puede pulsar la carpeta recién creada para entrar en ella y crear recursos o carpetas dentro de la carpeta. Además, puede seleccionar una carpeta y elegir colocarla en la cola para descargarla, eliminarla o editar su nombre.

   ![editdeletedownloadafolder](assets/editdeletedownloadafolder.png)

### Crear copias de uno o varios recursos o letras {#create-copies-of-one-or-more-assets-or-letters}

Puede utilizar recursos y letras existentes para crear rápidamente recursos y letras con propiedades, contenido y recursos heredados similares. Puede copiar y pegar diccionarios de datos, fragmentos de documento y letras.

Complete los siguientes pasos para crear copias de recursos y cartas:

1. En la página Recursos o Cartas correspondiente, seleccione uno o varios recursos o letras. La interfaz de usuario muestra el icono Copiar .
1. Pulse Copiar. La interfaz de usuario muestra el icono Pegar . También puede elegir ir/navegar dentro de una carpeta antes de pegar. Las distintas carpetas pueden contener recursos con los mismos nombres. Para obtener más información sobre las carpetas, consulte [Carpetas y organización de recursos](#folders-and-organizing-assets).
1. Pulse Pegar. Aparecerá el cuadro de diálogo Pegar. El sistema genera automáticamente nombres y títulos a las nuevas copias de recursos/letras, pero puede editar los títulos y nombres de los recursos/letras.

   Si está copiando y pegando los recursos o las letras en el mismo lugar, se añade un sufijo &quot;-CopyXX&quot; al nombre existente del recurso o la carta. Si no existe título para el recurso o la carta copiados, el campo de título generado automáticamente permanece en blanco.

1. Si es necesario, edite el Título y el Nombre con los que desea guardar la copia del recurso o la carta.
1. Pulse Pegar. Se crean nuevas copias de los recursos copiados.

## Búsqueda {#search-forms}

La interfaz de usuario de AEM Forms le permite buscar su contenido. Con la barra superior, puede pulsar Buscar **[A]** para buscar recursos como recursos y documentos en el contenido.

Al buscar recursos, AEM Forms muestra el panel lateral. También puede tocar ![assets-browser-content-only](assets/assets-browser-content-only.png) > Filtro **[B]** para invocar el panel lateral. Con los distintos filtros del panel lateral, puede limitar la búsqueda. El panel lateral también le permite guardar sus búsquedas.

![search_topbar](assets/search_topbar.png)

**A.** Buscar **B.** Filtro

![Panel lateral: Filtros](assets/search_sidepanel.png)

Panel lateral: Filtros

En el panel lateral, puede utilizar lo siguiente para reducir los resultados de búsqueda:

* Directorio de búsqueda
* Etiquetas
* Criterios de búsqueda; por ejemplo, fechas de modificación, estado de publicación o estado de Live Copy

El panel lateral también le permite guardar la configuración de búsqueda con los nombres que elija.

Para obtener más información e instrucciones sobre el uso de la búsqueda, los filtros, la búsqueda guardada y el panel lateral, consulte [Buscar](/help/sites-authoring/search.md).
