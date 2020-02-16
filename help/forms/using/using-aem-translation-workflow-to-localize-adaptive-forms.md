---
title: Uso del flujo de trabajo de traducción de AEM para localizar formularios adaptables y documentos de registro
seo-title: Uso del flujo de trabajo de traducción de AEM para localizar formularios adaptables y documentos de registro
description: Aprenda a utilizar los flujos de trabajo de traducción de AEM para localizar formularios adaptables y documentos de registro.
seo-description: Aprenda a utilizar los flujos de trabajo de traducción de AEM para localizar formularios adaptables y documentos de registro.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# Uso del flujo de trabajo de traducción de AEM para localizar formularios adaptables y documentos de registro {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Los formularios localizados le ayudan a ofrecer una audiencia más amplia en todas las regiones geográficas. El flujo de trabajo de traducción de Adobe Experience Manager le ayuda a localizar formularios adaptables y sus documentos de registro. Puede utilizar **traducción** automática o traductores **** humanos para localizar un formulario adaptable.

En este artículo se explica el proceso para utilizar el flujo de trabajo de traducción de AEM con formularios adaptables y documentos de registro.

## Localización de un formulario adaptable y un documento de registro mediante traducción automática {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

El servicio de traducción automática traduce inmediatamente el contenido en forma adaptable y documento de registro. AEM Forms está preconfigurado para utilizar una versión de prueba de Microsoft Translator para la traducción automática. Realice los siguientes pasos para habilitar la traducción automática para los formularios adaptables y el documento de registro:

1. En la interfaz de usuario de AEM Forms, seleccione un formulario y toque la opción **Agregar diccionario** .
1. En la pantalla **Agregar diccionario al proyecto** de traducción, seleccione la opción **Crear un nuevo proyecto** de traducción o **Agregar a un proyecto** de traducción existente.
1. En el campo Título **** del proyecto, especifique el título. Por ejemplo, `Government Reference Site - German locale.`
1. En el campo Idiomas **de** destino, especifique una configuración regional (por ejemplo, `German(de)`) y haga clic en **Hecho**. Puede especificar varias configuraciones regionales. El formulario se traduce a todas las configuraciones regionales especificadas en el campo Idiomas **de** destino.
1. En el cuadro de diálogo Diccionario agregado, haga clic en **Abrir proyectos**. En la pantalla Proyectos, abra el proyecto recién creado.
1. Haga clic en las **elipses** en la parte inferior del mosaico Resumen **de** traducción. Se abre la pantalla Resumen de traducción.
1. Haga clic en el icono **Editar** en la parte superior de la pantalla Resumen **de** traducción. Abra la ficha **Traducción** y seleccione Traducción automática en la pantalla Método **de** traducción. Seleccione el proveedor **de** traducción y la configuración **de** nube correspondientes. Click the **Done** icon at the top of the screen.
1. En el mosaico Trabajo **de** traducción, haga clic en el icono ![aem62forms_downarrow](assets/aem62forms_downarrow.png) y, a continuación, haga clic en **Iniciar**. El estado del mosaico cambia a Borrador. Una vez finalizada la traducción, el estado cambia a **Listo para revisión**. Actualice la página después de unos minutos y compruebe el estado.
1. Después de que el estado cambie a **Listo para revisión** en el mosaico Trabajo **de** traducción, abra el formulario en una ventana del explorador. Se muestra una versión localizada del formulario.

   >[!NOTE]
   >
   >* Antes de abrir la versión localizada del formulario en la ventana del explorador, asegúrese de que la configuración regional del explorador está configurada para coincidir con la configuración regional del formulario. Por ejemplo, si el formulario se traduce al idioma alemán(de), defina la configuración regional del explorador en alemán(de).
   >* Los componentes de formulario adaptables no admiten idiomas de derecha a izquierda (RTL). Por ejemplo, hebreo.


   Junto con el formulario adaptable, también se localiza el documento de registro generado automáticamente.

   Para obtener más información sobre la configuración y la configuración del documento de registro, consulte:

   [Configuración del documento de plantilla de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Configuración de documento de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalice la información de marca del documento del registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) y asegúrese de que la configuración regional del explorador se establece en el mismo idioma en el que ha localizado el formulario adaptable mediante el lenguaje del equipo. La configuración regional del explorador ayuda a localizar la información de marca en el documento del registro.
1. Para ver el documento localizado del registro, toque Generar vista previa. El documento del archivo PDF se genera y abre en una nueva ficha del explorador.

## Localización de un formulario adaptable y su documento de registro mediante Traducción humana {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

En Traducción humana el contenido se envía a un proveedor de traducción y es traducido por traductores profesionales. Una vez completado, el contenido traducido se devuelve e importa a AEM. Cuando el proveedor de traducción está integrado con AEM, el contenido se envía automáticamente entre AEM y el proveedor de traducción.

Para la traducción, un diccionario que contiene archivos en formato XLIFF se comparte con los traductores profesionales. El diccionario incluye un archivo XLIFF independiente para cada configuración regional. Cada archivo XLIFF contiene texto que se mostrará a los usuarios finales y a los marcadores de posición del texto localizado correspondiente.

Realice los siguientes pasos para localizar un formulario y su documento de registro mediante Traductores humanos:

1. [Conecte AEM con su proveedor](/help/sites-administering/tc-tic.md) de servicios de traducción y [cree configuraciones](/help/sites-administering/tc-tic.md)del marco de integración de traducción.

1. [Asocie las páginas del maestro](/help/sites-administering/tc-tic.md) de idioma con el servicio de traducción y las configuraciones del marco.

1. [Identifique el tipo de contenido](/help/sites-administering/tc-rules.md) que traducir.

1. [Para preparar el contenido para la traducción](/help/sites-administering/tc-prep.md) , cree el maestro de idioma y las páginas raíz de las copias de idioma.

1. [Cree proyectos](/help/sites-administering/tc-manage.md) de traducción para reunir el contenido que traducir y preparar el proceso de traducción.

1. Utilice los proyectos de traducción para [administrar el proceso](/help/sites-administering/tc-manage.md)de traducción de contenido.

>[!NOTE]
>
>* Los componentes de formulario adaptables no admiten idiomas de derecha a izquierda (RTL). Por ejemplo, hebreo.
>



