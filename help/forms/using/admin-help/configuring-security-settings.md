---
title: Configuración de la configuración de seguridad
seo-title: Configuración de la configuración de seguridad
description: Obtenga información sobre cómo configurar los ajustes de seguridad.
seo-description: Obtenga información sobre cómo configurar los ajustes de seguridad.
uuid: 9747f268-3551-4064-8dba-e1de4a577843
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a89ab508-173f-4b1c-88d9-ef944af4d9ae
feature: PDF Generator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 0%

---


# Configuración de seguridad{#configuring-security-settings}

Puede limitar el acceso a los documentos PDF estableciendo contraseñas y restringiendo ciertas funciones, como la impresión y la edición. Cuando un documento PDF tiene características restringidas, las herramientas y los elementos de menú relacionados con esas características se ven atenuados. También puede utilizar otros métodos para crear documentos seguros, como codificar o certificar un documento. Una configuración de seguridad contiene la contraseña y las opciones específicas que se deben usar para ciertas conversiones de PDF.

En la página Configuración de seguridad, puede realizar las siguientes tareas:

## Crear o editar una configuración de seguridad {#create-or-edit-a-security-setting}

Una *configuración de seguridad* controla la seguridad y los permisos de los archivos convertidos con esa configuración de seguridad.

1. En la consola de administración, haga clic en Servicios > Generador de PDF > Configuración de seguridad.
1. Haga clic en Nuevo o en el nombre de una configuración de seguridad.
1. En la página Nueva/Editar configuración de seguridad , complete la información necesaria para la configuración de seguridad. (Consulte [Configuración del tipo de archivo](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings)).
1. Haga clic en Guardar y, en el cuadro de diálogo que aparece, escriba un nombre para la configuración y, a continuación, haga clic en Aceptar.

### Configuración de seguridad {#security-settings}

Estos ajustes configuran la compatibilidad y el cifrado. Para obtener instrucciones sobre el acceso a la configuración de fuentes, consulte [Crear o editar una configuración de seguridad](configuring-security-settings.md#create-or-edit-a-security-setting).

**Compatibilidad:** establece el tipo de cifrado para abrir un documento protegido con contraseña. La opción Acrobat 3.0 y posteriores utiliza un nivel de codificación bajo, pero las demás opciones utilizan un nivel de codificación alto:

**Acrobat 3.0 Y Posteriores:** Utiliza un cifrado bajo (RC4 de 40 bits).

**Acrobat 5.0 Y Posteriores:** Utiliza un cifrado alto (RC4 de 128 bits).

**Acrobat 6.0 Y Posteriores:** Utiliza un cifrado alto (RC4 de 128 bits). Esta opción permite activar los metadatos para la búsqueda.

**Acrobat 7.0 Y Posteriores:** Utiliza un cifrado alto (AES de 128 bits). Esta opción permite activar metadatos para buscar y cifrar solo archivos adjuntos.

**Acrobat 9.0 Y Posteriores:** Utiliza un cifrado alto (AES de 256 bits). Esta opción permite activar metadatos para buscar y cifrar solo archivos adjuntos.

Una versión anterior de Acrobat no puede abrir un documento PDF que tenga una configuración de compatibilidad superior. Por ejemplo, si selecciona la opción Acrobat 7.0 y posteriores, no podrá abrir el documento en Acrobat 6.0 o versiones anteriores.

Asegúrese de que el nivel de compatibilidad sea coherente con el nivel de compatibilidad de PDF para el mismo origen. Por ejemplo, si tiene una carpeta de visualización configurada para utilizar la configuración de PDF estándar, que es compatible con Acrobat 5.0 o posterior, el nivel de compatibilidad de seguridad no debe ser superior al de Acrobat 5.0.

**Restricción de documento:** las restricciones de documento disponibles dependen de la opción Compatibilidad seleccionada.

**Sin codificación:** no cifra ninguna parte del documento.

**Codificar todo el contenido del documento:** codifica el documento y los metadatos del documento. Cuando se selecciona esta opción, los motores de búsqueda no pueden acceder a los metadatos del documento.

**Codificar todo el contenido del documento excepto los metadatos (compatible con Acrobat 6 y versiones posteriores):** codifica el contenido de un documento, pero sigue permitiendo que los motores de búsqueda accedan a los metadatos del documento. Esta opción solo está disponible cuando la opción Compatibilidad está definida en Acrobat 6.0 o posterior, Acrobat 7.0 o posterior, o Acrobat 9.0 o posterior.

**Codificar solo archivos adjuntos (compatibles con Acrobat 7 y versiones posteriores):**  los usuarios pueden abrir el documento sin contraseña, pero deben introducir una contraseña para abrir los archivos adjuntos. Esta opción solo está disponible cuando la opción Compatibilidad está definida en Acrobat 7.0 o posterior o en Acrobat 9.0 o posterior.

Estos ajustes configuran la seguridad de la contraseña:

>[!NOTE]
>
>Si olvida una contraseña, no se puede recuperar del documento. Se recomienda almacenar contraseñas en otra ubicación segura en caso de que las olvide. Además, mantenga una copia de seguridad del documento que no esté protegido con contraseña.

**Requerir una contraseña para abrir el documento:** activa las opciones de contraseña.

**Contraseña de apertura de documento:** evita que los usuarios abran el documento a menos que escriban la contraseña especificada. Las contraseñas distinguen entre mayúsculas y minúsculas. Acrobat utiliza el método de seguridad RC4 de RSA Security Inc. para proteger con contraseña los documentos PDF. Si restringe la impresión y la edición, se recomienda agregar una contraseña de apertura de documento para mejorar la seguridad.

**Volver a escribir la contraseña de apertura del documento:**  garantiza que la contraseña de apertura del documento sea correcta.

**Requerir una contraseña para abrir archivos adjuntos:** activa las opciones de contraseña. Esta opción solo está disponible cuando la opción Compatibilidad está definida en Acrobat 7.0 o posterior o en Acrobat 9.0 o posterior, y la opción Restricción de documento está establecida en Codificar solo archivos adjuntos.

**Archivo adjunto Abrir contraseña:** garantiza que se necesita una contraseña para abrir un archivo adjunto. Los usuarios pueden abrir el documento sin contraseña. Esta opción solo está disponible cuando la opción Compatibilidad está definida en Acrobat 7.0 o posterior o en Acrobat 9.0 o posterior, y la opción Restricción de documento está establecida en Codificar solo archivos adjuntos.

**Volver a escribir archivo adjunto:** garantiza que la contraseña sea correcta. Esta opción solo está disponible cuando la opción Compatibilidad está definida en Acrobat 7.0 o posterior o en Acrobat 9.0 o posterior, y la opción Restricción de documento está establecida en Codificar solo archivos adjuntos.

Estas opciones configuran los permisos:

**Utilice Una Contraseña Para Restringir La Impresión Y Edición Del Documento Y Su Configuración De Seguridad:** Habilita Las Restricciones En Los Permisos.

**Contraseña de permisos:** restringe a los usuarios de la impresión y la edición. Los usuarios no pueden cambiar esta configuración de seguridad a menos que escriban la contraseña especificada. No puede utilizar la misma contraseña que se usa para la contraseña de apertura de documento. Cuando establece una contraseña de permisos, solo las personas que escriben esa contraseña pueden cambiar la configuración de seguridad. Si el documento PDF tiene ambos tipos de contraseñas, se abrirá cualquiera de ellas. Sin embargo, un usuario solo puede establecer o cambiar las funciones restringidas con la contraseña de permisos. Si el documento PDF solo tiene la contraseña de permiso o si un usuario abre el documento utilizando la contraseña de apertura del documento, la solicitud de contraseña aparecerá cuando el usuario intente cambiar la configuración de seguridad.

**Volver a escribir la contraseña de permisos:** garantiza que la contraseña de permisos sea correcta.

**Impresión permitida:** especifica la calidad de impresión del documento PDF:

**Ninguno:** evita que los usuarios impriman el documento.

**Baja resolución (150 ppp):** permite a los usuarios imprimir el documento con una resolución no superior a 150 ppp. La impresión puede ser más lenta porque cada página se imprime como una imagen de mapa de bits. Esta opción solo está disponible si se ha seleccionado un nivel de cifrado alto (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Alta resolución:** permite a los usuarios imprimir a cualquier resolución, dirigiendo la salida vectorial de alta calidad a PostScript y otras impresoras que admiten características de impresión avanzadas de alta calidad.

**Cambios permitidos:** define qué acciones de edición se permiten en el documento PDF:

**Ninguno:** evita que los usuarios cambien el documento, lo que incluye rellenar los campos de firma y formulario.

**Inserción, eliminación y rotación de páginas:** permite a los usuarios insertar, eliminar y rotar páginas, así como crear marcadores y páginas en miniatura. Esta opción solo está disponible si se ha seleccionado un nivel de cifrado alto (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Rellenar campos del formulario y firmar campos de firma existentes:** permite a los usuarios rellenar formularios y agregar firmas digitales. Sin embargo, los usuarios no pueden agregar comentarios ni crear campos de formulario. Esta opción solo está disponible si se ha seleccionado un nivel de cifrado alto (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Comentarios, rellenado de campos de formulario y firma de campos de firma existentes:** permite a los usuarios rellenar formularios y agregar firmas y comentarios digitales.

**Diseño de página, toque, rellenado de campos de formulario y firma de campos de firma existentes:** permite a los usuarios insertar, rotar o eliminar páginas, así como crear marcadores o imágenes en miniatura, rellenar formularios y agregar firmas digitales. Esta opción no permite a los usuarios crear campos de formulario. Esta opción solo está disponible si se ha seleccionado un nivel de codificación bajo (Acrobat 3.0).

**Cualquier excepto Extracción de páginas:** permite a los usuarios cambiar el documento utilizando cualquier método de la Lista de permitidos Cambios, excepto eliminar páginas.

**Activar la copia de texto, imágenes y otro contenido:** permite a los usuarios seleccionar y copiar el contenido del documento PDF. También permite que las utilidades que necesitan acceder al contenido de un archivo PDF, como Acrobat Catalog, accedan a dicho contenido. Esta opción solo está disponible si se ha seleccionado un nivel de codificación alto.

**Habilitar el acceso al texto de los dispositivos del Reader de pantalla para los discapacitados visuales:** permite a los usuarios con deficiencias visuales leer el documento utilizando lectores de pantalla. Sin embargo, los usuarios no pueden copiar ni extraer el contenido del documento. Esta opción solo está disponible si se ha seleccionado un nivel de codificación alto.

## Eliminar una configuración de seguridad {#delete-a-security-setting}

Puede eliminar una configuración de seguridad si ya no es necesaria. Sin embargo, la configuración de seguridad preconfigurada no se puede eliminar.

1. En la consola de administración, haga clic en **[!UICONTROL Services > PDF Generator > Security Settings]**.
1. Seleccione la casilla de verificación situada junto a la configuración que desea eliminar. Puede seleccionar varias opciones de configuración.
1. Haga clic en **[!UICONTROL Eliminar]** y, en la página **[!UICONTROL Confirmación de eliminación]**, vuelva a hacer clic en **[!UICONTROL Eliminar]**.

