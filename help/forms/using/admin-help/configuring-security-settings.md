---
title: Configuración de la configuración de seguridad
seo-title: Configuración de la configuración de seguridad
description: Obtenga información sobre cómo configurar las opciones de seguridad.
seo-description: Obtenga información sobre cómo configurar las opciones de seguridad.
uuid: 9747f268-3551-4064-8dba-e1de4a577843
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a89ab508-173f-4b1c-88d9-ef944af4d9ae
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de la configuración de seguridad{#configuring-security-settings}

Puede limitar el acceso a los documentos PDF estableciendo contraseñas y restringiendo determinadas funciones, como la impresión y la edición. Cuando un documento PDF tiene funciones restringidas, las herramientas y los elementos de menú relacionados con dichas funciones aparecen atenuados. También puede utilizar otros métodos para crear documentos seguros, como cifrar o certificar un documento. Una configuración de seguridad contiene la contraseña y las opciones específicas que se utilizarán para determinadas conversiones de PDF.

En la página Configuración de seguridad, puede realizar las siguientes tareas:

## Crear o editar una configuración de seguridad {#create-or-edit-a-security-setting}

Una configuración *de* seguridad controla la seguridad y los permisos de los archivos convertidos con esa configuración de seguridad.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de seguridad.
1. Haga clic en Nuevo o en el nombre de una configuración de seguridad.
1. En la página Nueva/Editar configuración de seguridad, complete la información necesaria para la configuración de seguridad. (Consulte [Configuración del tipo de archivo](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings)).
1. Haga clic en Guardar y, en el cuadro de diálogo que aparece, escriba un nombre para la configuración y, a continuación, haga clic en Aceptar.

### Configuración de seguridad {#security-settings}

Estas opciones configuran la compatibilidad y el cifrado. Para obtener instrucciones sobre cómo acceder a la configuración de fuentes, consulte [Creación o edición de una configuración](configuring-security-settings.md#create-or-edit-a-security-setting)de seguridad.

**** Compatibilidad: Define el tipo de codificación para abrir un documento protegido con contraseña. La opción Acrobat 3.0 y posterior utiliza un nivel de codificación bajo, pero las demás opciones utilizan un nivel de codificación alto:

**** Acrobat 3.0 Y Posterior: Utiliza codificación baja (RC4 de 40 bits).

**** Acrobat 5.0 Y Posteriores: Utiliza cifrado alto (RC4 de 128 bits).

**** Acrobat 6.0 Y Posteriores: Utiliza cifrado alto (RC4 de 128 bits). Esta opción le permite habilitar los metadatos para la búsqueda.

**** Acrobat 7.0 Y Posteriores: Utiliza cifrado alto (AES de 128 bits). Esta opción le permite activar metadatos para buscar y codificar sólo archivos adjuntos.

**** Acrobat 9.0 Y Posteriores: Utiliza cifrado alto (AES de 256 bits). Esta opción le permite activar metadatos para buscar y codificar sólo archivos adjuntos.

Una versión anterior de Acrobat no puede abrir un documento PDF con una configuración de compatibilidad más alta. Por ejemplo, si selecciona la opción Acrobat 7.0 y posterior, no podrá abrir el documento en Acrobat 6.0 o anterior.

Asegúrese de que el nivel de compatibilidad sea coherente con el nivel de compatibilidad de PDF para el mismo origen. Por ejemplo, si tiene una carpeta vigilada configurada para utilizar la configuración de PDF estándar, que es compatible con Acrobat 5.0 o posterior, el nivel de compatibilidad de seguridad no debe ser mayor que Acrobat 5.0.

**** Restricción de documento: Las restricciones de documento disponibles dependen de la opción Compatibilidad seleccionada.

**** Sin cifrado: No cifra ninguna parte del documento.

**** Cifrar todo el contenido del documento: Codifica el documento y los metadatos del documento. Cuando se selecciona esta opción, los motores de búsqueda no pueden acceder a los metadatos del documento.

**** Codificar Todo El Contenido Del Documento Excepto Los Metadatos (Compatible Con Acrobat6 Y Posteriores): Codifica el contenido de un documento pero aún permite que los motores de búsqueda accedan a los metadatos del documento. Esta opción solo está disponible cuando la opción Compatibilidad está definida en Acrobat 6.0 o posterior, Acrobat 7.0 o posterior, o Acrobat 9.0 o posterior.

**** Codificar sólo archivos adjuntos (Compatible Con Acrobat 7 Y Posteriores): Los usuarios pueden abrir el documento sin contraseña, pero deben introducir una contraseña para abrir los archivos adjuntos. Esta opción solo está disponible cuando la opción Compatibilidad está definida en Acrobat 7.0 o posterior o en Acrobat 9.0 o posterior.

Estas opciones configuran la seguridad de la contraseña:

***Nota **: Si olvida una contraseña, no podrá recuperarla del documento. Se recomienda almacenar contraseñas en otra ubicación segura en caso de olvidarlas. Además, mantenga una copia de seguridad del documento que no esté protegido con contraseña.*

**** Requerir Una Contraseña Para Abrir El Documento: Habilita las opciones de contraseña.

**** Contraseña de apertura de documento: Impide que los usuarios abran el documento a menos que escriban la contraseña especificada. Las contraseñas distinguen entre mayúsculas y minúsculas. Acrobat utiliza el método de seguridad RC4 de RSA Security Inc. para proteger los documentos PDF con contraseña. Si está restringiendo la impresión y edición, se recomienda agregar una contraseña de apertura de documento para mejorar la seguridad.

**** Vuelva a escribir la contraseña de apertura del documento: Garantiza que la contraseña de apertura del documento sea correcta.

**** Requerir una contraseña para abrir archivos adjuntos: Habilita las opciones de contraseña. Esta opción solo está disponible cuando la opción Compatibilidad está definida en Acrobat 7.0 o posterior o en Acrobat 9.0 o posterior, y la opción de restricción Documento está establecida en Codificar sólo archivos adjuntos.

**** Contraseña de apertura de archivo adjunto: Garantiza que se necesita una contraseña para abrir un archivo adjunto. Los usuarios pueden abrir el documento sin contraseña. Esta opción solo está disponible cuando la opción Compatibilidad está definida en Acrobat 7.0 o posterior o en Acrobat 9.0 o posterior, y la opción de restricción Documento está establecida en Codificar sólo archivos adjuntos.

**** Volver a escribir archivo adjunto: Garantiza que la contraseña sea correcta. Esta opción solo está disponible cuando la opción Compatibilidad está definida en Acrobat 7.0 o posterior o en Acrobat 9.0 o posterior, y la opción de restricción Documento está establecida en Codificar sólo archivos adjuntos.

Estas opciones configuran los permisos:

**** Utilice Una Contraseña Para Restringir La Impresión Y Edición Del Documento Y Su Configuración De Seguridad: Habilita las restricciones de permisos.

**** Contraseña de permisos: Restringe la impresión y edición a los usuarios. Los usuarios no pueden cambiar esta configuración de seguridad a menos que escriban la contraseña especificada. No puede utilizar la misma contraseña que se utiliza para la contraseña de apertura de documento. Cuando se establece una contraseña de permisos, solo las personas que escriben esa contraseña pueden cambiar la configuración de seguridad. Si el documento PDF tiene ambos tipos de contraseñas, se abrirá cualquiera de ellas. Sin embargo, un usuario solo puede establecer o cambiar las funciones restringidas con la contraseña de permisos. Si el documento PDF solo tiene la contraseña de permiso o si un usuario abre el documento con la contraseña de apertura del documento, la solicitud de contraseña aparecerá cuando el usuario intente cambiar la configuración de seguridad.

**** Vuelva a escribir la contraseña de permisos: Garantiza que la contraseña de permisos sea correcta.

**** Impresión permitida: Especifica la calidad de impresión del documento PDF:

**** Ninguno: Impide que los usuarios impriman el documento.

**** Baja resolución (150 ppp): Permite a los usuarios imprimir el documento con una resolución no superior a 150 ppp. La impresión puede ser más lenta porque cada página se imprime como una imagen de mapa de bits. Esta opción solo está disponible si se selecciona un nivel de codificación alto (Acrobat 5.0, 6.0, 7.0 o 9.0).

**** Alta resolución: Permite a los usuarios imprimir con cualquier resolución, dirigiendo la salida vectorial de alta calidad a PostScript y otras impresoras que admiten funciones de impresión de alta calidad avanzadas.

**** Cambios permitidos: Define qué acciones de edición se permiten en el documento PDF:

**** Ninguno: Impide que los usuarios cambien el documento, incluso rellenando campos de formulario y firma.

**** Inserción, Eliminación Y Rotación De Páginas: Permite a los usuarios insertar, eliminar y rotar páginas, así como crear marcadores y páginas en miniatura. Esta opción solo está disponible si se selecciona un nivel de codificación alto (Acrobat 5.0, 6.0, 7.0 o 9.0).

**** Rellenado de campos de formulario y firma de campos de firma existentes: Permite a los usuarios rellenar formularios y agregar firmas digitales. Sin embargo, los usuarios no pueden agregar comentarios ni crear campos de formulario. Esta opción solo está disponible si se selecciona un nivel de codificación alto (Acrobat 5.0, 6.0, 7.0 o 9.0).

**** Comentarios, Rellenado De Campos De Formulario Y Firma De Campos De Firma Existentes: Permite a los usuarios rellenar formularios y agregar firmas y comentarios digitales.

**** Diseño De Página, Retocar, Rellenar Campos De Formulario Y FirmarCampos De Firma Existentes: Permite a los usuarios insertar, rotar o eliminar páginas y crear marcadores o imágenes en miniatura, rellenar formularios y agregar firmas digitales. Esta opción no permite a los usuarios crear campos de formulario. Esta opción solo está disponible si se selecciona un nivel de codificación bajo (Acrobat 3.0).

**** Cualquiera excepto extracción de páginas: Permite a los usuarios cambiar el documento mediante cualquier método de la lista Cambios permitidos, excepto eliminar páginas.

**** Habilite La Copia De Texto, Imágenes Y Otro Contenido: Permite a los usuarios seleccionar y copiar el contenido del documento PDF. También permite que las utilidades que necesiten acceder al contenido de un archivo PDF, como Acrobat Catalog, accedan a dicho contenido. Esta opción solo está disponible si se selecciona un nivel de codificación alto.

**** Habilite El Acceso Al Texto De Los Dispositivos Lectores De Pantalla Para Las Personas Con Problemas Visuales: Permite a los usuarios con deficiencias visuales leer el documento mediante lectores de pantalla. Sin embargo, los usuarios no pueden copiar ni extraer el contenido del documento. Esta opción solo está disponible si se selecciona un nivel de codificación alto.

## Eliminar una configuración de seguridad {#delete-a-security-setting}

Puede eliminar una configuración de seguridad si ya no es necesaria. Sin embargo, no se puede eliminar la configuración de seguridad preconfigurada.

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > Generador de PDF > Configuración]** de seguridad.
1. Seleccione la casilla de verificación situada junto a la configuración que desee eliminar. Puede seleccionar varios ajustes.
1. Haga clic en **[!UICONTROL Eliminar]** y, en la página **[!UICONTROL Eliminar confirmación]** , vuelva a hacer clic en **[!UICONTROL Eliminar]** .

