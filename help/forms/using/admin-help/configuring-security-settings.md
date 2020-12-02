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
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 0%

---


# Configuración de la configuración de seguridad{#configuring-security-settings}

Puede limitar el acceso a los documentos PDF estableciendo contraseñas y restringiendo determinadas funciones, como la impresión y la edición. Cuando un documento PDF tiene funciones restringidas, las herramientas y los elementos de menú relacionados con dichas funciones aparecen atenuados. También puede utilizar otros métodos para crear documentos seguros, como cifrar o certificar un documento. Una configuración de seguridad contiene la contraseña y las opciones específicas que se utilizarán para determinadas conversiones de PDF.

En la página Configuración de seguridad, puede realizar las siguientes tareas:

## Crear o editar una configuración de seguridad {#create-or-edit-a-security-setting}

Una *configuración de seguridad* controla la seguridad y los permisos de los archivos convertidos con esa configuración de seguridad.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de seguridad.
1. Haga clic en Nuevo o en el nombre de una configuración de seguridad.
1. En la página Nueva/Editar configuración de seguridad, complete la información necesaria para la configuración de seguridad. (Consulte [Configuración del tipo de archivo](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings).)
1. Haga clic en Guardar y, en el cuadro de diálogo que aparece, escriba un nombre para la configuración y, a continuación, haga clic en Aceptar.

### Configuración de seguridad {#security-settings}

Estas opciones configuran la compatibilidad y el cifrado. Para obtener instrucciones sobre cómo acceder a la configuración de fuentes, consulte [Creación o edición de una configuración de seguridad](configuring-security-settings.md#create-or-edit-a-security-setting).

**Compatibilidad:** establece el tipo de codificación para abrir un documento protegido con contraseña. La opción Acrobat 3.0 y posterior utiliza un nivel de codificación bajo, pero las demás opciones utilizan un nivel de codificación alto:

**Acrobat 3.0 Y Posterior:** Utiliza codificación baja (RC4 de 40 bits).

**Acrobat 5.0 Y Posteriores:** Utiliza Encriptación Alta (RC4 de 128 bits).

**Acrobat 6.0 Y Posteriores:** Utiliza Encriptación Alta (RC4 de 128 bits). Esta opción le permite habilitar los metadatos para la búsqueda.

**Acrobat 7.0 Y Posteriores:** Utiliza Encriptación Alta (AES de 128 bits). Esta opción le permite activar metadatos para buscar y codificar sólo archivos adjuntos.

**Acrobat 9.0 Y Posteriores:** Utiliza Encriptación Alta (AES de 256 bits). Esta opción le permite activar metadatos para buscar y codificar sólo archivos adjuntos.

Una versión anterior de Acrobat no puede abrir un documento PDF con una configuración de compatibilidad más alta. Por ejemplo, si selecciona la opción Acrobat 7.0 y posterior, no podrá abrir el documento en Acrobat 6.0 ni en versiones anteriores.

Asegúrese de que el nivel de compatibilidad sea coherente con el nivel de compatibilidad de PDF para el mismo origen. Por ejemplo, si tiene una carpeta vigilada configurada para utilizar la configuración de PDF estándar, que es compatible con Acrobat 5.0 o posterior, el nivel de compatibilidad de seguridad no debe ser mayor que Acrobat 5.0.

**Restricción de documento:** las restricciones de documento disponibles dependen de la opción Compatibilidad seleccionada.

**Sin cifrado:** no cifra ninguna parte del documento.

**Codificar todo el contenido del Documento:** Codifica el documento y los metadatos del documento. Cuando se selecciona esta opción, los motores de búsqueda no pueden acceder a los metadatos de documento.

**Codificar todo el contenido del Documento excepto los metadatos (Compatible con Acrobat 6 y versiones posteriores):** Codifica el contenido de un documento, pero aún permite que los motores de búsqueda accedan a los metadatos del documento. Esta opción solo está disponible cuando la opción Compatibilidad está establecida en Acrobat 6.0 o posterior, Acrobat 7.0 o posterior, o Acrobat 9.0 o posterior.

**Codificar sólo archivos adjuntos (compatibles con Acrobat 7 y versiones posteriores):** los usuarios pueden abrir el documento sin contraseña, pero deben introducir una contraseña para abrir los archivos adjuntos. Esta opción solo está disponible cuando la opción Compatibilidad está establecida en Acrobat 7.0 o posterior o en Acrobat 9.0 o posterior.

Estas opciones configuran la seguridad de la contraseña:

>[!NOTE]
>
>Si olvida una contraseña, no podrá recuperarla del documento. Se recomienda almacenar contraseñas en otra ubicación segura en caso de olvidarlas. Además, mantenga una copia de seguridad del documento que no esté protegido con contraseña.

**Requerir una contraseña para abrir el Documento:** activa las opciones de contraseña.

**Contraseña de apertura de documento:** evita que los usuarios abran el documento a menos que escriban la contraseña especificada. Las contraseñas distinguen entre mayúsculas y minúsculas. Acrobat utiliza el método de seguridad RC4 de RSA Security Inc. para proteger documentos PDF con contraseña. Si restringe la impresión y la edición, se recomienda agregar una contraseña de apertura de documento para mejorar la seguridad.

**Vuelva a escribir la contraseña de apertura de Documento:** garantiza que la contraseña de apertura de documento sea correcta.

**Requerir una contraseña para abrir archivos adjuntos:** activa las opciones de contraseña. Esta opción solo está disponible cuando la opción Compatibilidad está establecida en Acrobat 7.0 o posterior o en Acrobat 9.0 o posterior, y la opción de restricción de Documento está establecida en Codificar sólo archivos adjuntos.

**Contraseña de apertura de archivo adjunto:** garantiza que se requiere una contraseña para abrir un archivo adjunto. Los usuarios pueden abrir el documento sin contraseña. Esta opción solo está disponible cuando la opción Compatibilidad está establecida en Acrobat 7.0 o posterior o en Acrobat 9.0 o posterior, y la opción de restricción de Documento está establecida en Codificar sólo archivos adjuntos.

**Volver a escribir Archivo adjunto:** garantiza que la contraseña sea correcta. Esta opción solo está disponible cuando la opción Compatibilidad está establecida en Acrobat 7.0 o posterior o en Acrobat 9.0 o posterior, y la opción de restricción de Documento está establecida en Codificar sólo archivos adjuntos.

Estas opciones configuran los permisos:

**Utilice Una Contraseña Para Restringir La Impresión Y Edición Del Documento Y Su Configuración De Seguridad:** Habilita Las Restricciones De Permisos.

**Contraseña de permisos:** impide que los usuarios impriman y editen. Los usuarios no pueden cambiar esta configuración de seguridad a menos que escriban la contraseña especificada. No puede utilizar la misma contraseña que se usa para la contraseña de apertura de Documento. Cuando se establece una contraseña de permisos, solo las personas que escriben esa contraseña pueden cambiar la configuración de seguridad. Si el documento PDF tiene ambos tipos de contraseñas, se abrirá cualquiera de ellas. Sin embargo, un usuario solo puede establecer o cambiar las funciones restringidas con la contraseña de permisos. Si el documento PDF solo tiene la contraseña de permiso o si un usuario abre el documento con la contraseña de apertura de documento, aparecerá el mensaje de contraseña cuando el usuario intente cambiar la configuración de seguridad.

**Vuelva a escribir la contraseña de permisos:** garantiza que la contraseña de permisos sea correcta.

**Impresión permitida:** especifica la calidad de impresión del documento PDF:

**Ninguno:** evita que los usuarios impriman el documento.

**Baja resolución (150 ppp):** permite a los usuarios imprimir el documento con una resolución no superior a 150 ppp. La impresión puede ser más lenta porque cada página se imprime como una imagen de mapa de bits. Esta opción solo está disponible si se selecciona un nivel de cifrado alto (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Alta resolución:** permite a los usuarios imprimir con cualquier resolución, dirigiendo la salida vectorial de alta calidad a PostScript y otras impresoras que admiten funciones de impresión de alta calidad avanzadas.

**Cambios permitidos:** define qué acciones de edición están permitidas en el documento PDF:

**Ninguno:** evita que los usuarios cambien el documento, incluido el rellenado de campos de formulario y de firma.

**Inserción, eliminación y rotación de páginas:** permite a los usuarios insertar, eliminar y rotar páginas, así como crear marcadores y páginas en miniatura. Esta opción solo está disponible si se selecciona un nivel de cifrado alto (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Rellenar campos de formulario y firmar campos de firma existentes:** permite a los usuarios rellenar formularios y agregar firmas digitales. Sin embargo, los usuarios no pueden agregar comentarios ni crear campos de formulario. Esta opción solo está disponible si se selecciona un nivel de cifrado alto (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Comentarios, Rellenado de campos de formulario y Firma de campos de firma existentes:** permite a los usuarios rellenar formularios y agregar firmas y comentarios digitales.

**Diseño de página, retoque, rellenado de campos de formulario y firma de campos de firma existentes:** permite a los usuarios insertar, rotar o eliminar páginas y crear marcadores o imágenes en miniatura, rellenar formularios y agregar firmas digitales. Esta opción no permite a los usuarios crear campos de formulario. Esta opción solo está disponible si se selecciona un nivel de codificación bajo (Acrobat 3.0).

**Cualquiera excepto extraer páginas:** permite a los usuarios cambiar el documento mediante cualquier método de la Lista de permitidos Cambios, excepto eliminar páginas.

**Activar copia de texto, imágenes y otro contenido:** permite a los usuarios seleccionar y copiar el contenido del documento PDF. También permite que las utilidades que necesitan acceder al contenido de un archivo PDF, como Acrobat Catalog, accedan a dicho contenido. Esta opción solo está disponible si se selecciona un nivel de codificación alto.

**Activar el acceso al texto de los dispositivos de Reader de pantalla para personas con problemas visuales:** permite a los usuarios con problemas visuales leer el documento mediante lectores de pantalla. Sin embargo, los usuarios no pueden copiar ni extraer el contenido del documento. Esta opción solo está disponible si se selecciona un nivel de codificación alto.

## Eliminar una configuración de seguridad {#delete-a-security-setting}

Puede eliminar una configuración de seguridad si ya no es necesaria. Sin embargo, no se puede eliminar la configuración de seguridad preconfigurada.

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > Generador de PDF > Configuración de seguridad]**.
1. Seleccione la casilla de verificación situada junto a la configuración que desee eliminar. Puede seleccionar varios ajustes.
1. Haga clic en **[!UICONTROL Eliminar]** y, en la página **[!UICONTROL Eliminar confirmación]**, haga clic nuevamente en **[!UICONTROL Eliminar]**.

