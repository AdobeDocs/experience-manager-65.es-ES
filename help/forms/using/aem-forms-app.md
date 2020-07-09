---
title: Aplicación AEM Forms
seo-title: Aplicación AEM Forms
description: La aplicación AEM Forms permite a los trabajadores de campo utilizar formularios adaptables en sus dispositivos móviles.
seo-description: La aplicación AEM Forms permite a los trabajadores de campo utilizar formularios adaptables en sus dispositivos móviles.
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
translation-type: tm+mt
source-git-commit: aaedec7314b0fa8551df560eef2574a53c20d1c5
workflow-type: tm+mt
source-wordcount: '2418'
ht-degree: 0%

---


# Introduction to AEM Forms app {#aem-forms-app}

## Información general {#overview}

La aplicación AEM Forms permite sincronizar formularios adaptables, formularios móviles y conjuntos de formularios en dispositivos móviles, según el servidor. Puede definir flujos de trabajo que sean flujos de trabajo centrados en [Forms en OSGi](/help/forms/using/aem-forms-workflow.md) o flujos de trabajo de [Forms en JEE](/help/forms/using/finance-reference-site-walkthrough.md#approving-the-application). Por ejemplo, se ejecuta una empresa bancaria y se utilizan AEM Forms para administrar las aplicaciones y comunicaciones de los clientes. Sus clientes rellenan un formulario y lo envían para su verificación. Si activa el formulario en dispositivos móviles, los clientes pueden rellenarlo en la aplicación AEM Forms. También puede administrar el flujo de trabajo de verificación activando el formulario de verificación en dispositivos móviles. El trabajador de campo puede llevar un dispositivo móvil al cliente, comprobar los detalles y enviar el formulario. La aplicación AEM Forms se sincroniza con el servidor AEM Forms y obtiene los formularios habilitados para dispositivos móviles. Si la aplicación está sin conexión, almacena datos localmente.

El código fuente de la aplicación AEM Forms está disponible para los clientes a través del uso compartido de paquetes. El paquete de código fuente del recurso compartido de paquetes está disponible como: `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

La aplicación AEM Forms es compatible con dispositivos iOS, Android y Windows. Puede instalar la aplicación AEM Forms para Android desde Google Play, iOS desde App Store y Windows desde la tienda Windows.

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

Para instalar, personalizar y distribuir la aplicación en dispositivos iOS, Android o Windows, consulte [Personalización, compilación y distribución de la aplicación](#customize-build-distribute)AEM Forms.

## Requisitos previos {#prerequisites}

La aplicación AEM Forms requiere un servidor AEM Forms. Los usuarios pueden procesar formularios creados en AEM Forms Server, rellenarlos, guardarlos como borradores y enviarlos. La aplicación se conecta al servidor y obtiene de él los formularios habilitados. La aplicación AEM Forms se sincroniza con el servidor y, tan pronto como se cargan los formularios en la aplicación, los usuarios pueden trabajar sin conexión. Si la aplicación está sin conexión, los datos se guardan en el dispositivo y los datos se sincronizan con el servidor cuando la aplicación está en línea.

### Aplicación de AEM Forms con servidores que utilizan el flujo de trabajo de AEM Forms {#aem-forms-app-with-servers-using-aem-forms-workflow}

Si tiene un servidor de flujo de trabajo de AEM Forms, puede procesar formularios como tareas en la aplicación de AEM Forms. Por ejemplo, se ejecuta una empresa bancaria y el cliente rellena una aplicación para utilizar los servicios. La aplicación es un formulario adaptable que acepta información de sus clientes y la almacena como envío para revisión. El administrador revisa una aplicación y envía una solicitud de verificación al trabajador sobre el terreno. La aplicación reenviada activa un formulario de verificación en la aplicación del trabajador de campo como tarea. El trabajador de campo lleva el dispositivo móvil al cliente y verifica los detalles.

### Aplicación para AEM Forms con servidores que utilizan un flujo de trabajo centrado en Forms en OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

Si tiene un servidor AEM Forms, puede procesar formularios adaptables como aplicación AEM Inbox y tareas en la aplicación AEM Forms. Por ejemplo, se ejecuta una empresa bancaria y el cliente rellena una aplicación para utilizar los servicios. La aplicación está asociada a un formulario adaptable que acepta información de sus clientes y la almacena como un envío para revisión. El administrador revisa la tarea y aprueba la solicitud de verificación al trabajador de campo. El trabajador de campo lleva el dispositivo móvil al cliente y verifica los detalles.

### Aplicación de formularios o AEM Forms independientes con servidores sin flujo de trabajo de AEM Forms {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

Un servidor de AEM Forms que no utiliza Flujo de trabajo de AEM Forms es un AEM Forms en OSGi o un formulario móvil independiente o un formulario adaptable. La aplicación AEM Forms funciona con la implementación de AEM Forms en [OSGi](/help/sites-deploying/configuring-osgi.md). Los formularios que activa y publica para la aplicación AEM Forms están disponibles en la aplicación.

Los formularios se descargan en la aplicación y están disponibles sin conexión. Por ejemplo: está ejecutando una empresa bancaria y un cliente rellena una aplicación en el sitio. La aplicación es un formulario adaptable que acepta información de sus clientes y la almacena para su revisión. El administrador revisa el formulario y crea un formulario de verificación en la instancia de creación de AEM. El administrador habilita la sincronización del formulario con la aplicación AEM Forms y la publica. Si el formulario de verificación está disponible en la aplicación AEM Forms, el agente de campo puede utilizar un dispositivo móvil para comprobar los detalles del cliente. El dispositivo móvil se sincroniza con el servidor y el formulario de verificación se carga en la aplicación. El agente de campo puede visitar a su cliente, verificar los detalles, guardar los datos como borrador o enviar el formulario de verificación. El formulario se sincroniza con el servidor siempre que la aplicación esté en línea.

Para sincronizar el formulario en la aplicación AEM Forms:

1. En la instancia de autor, seleccione un formulario y haga clic en Propiedades **[!UICONTROL de Vista]**.

1. En la página de propiedades, haga clic en **[!UICONTROL Avanzadas]**.
1. En Avanzadas, active la opción: **[!UICONTROL Sincronice con la aplicación]** AEM Forms y toque **[!UICONTROL Guardar]**.

Cuando se publica el formulario, la aplicación se sincroniza con el servidor y lo recupera. Para sincronizar varios formularios, en la instancia de creación, seleccione varios formularios en el administrador de formularios y toque **[!UICONTROL Sincronizar con la aplicación]** AEM Forms.

## Compatibilidad con dispositivos móviles {#mobile-device-support}

Consulte la aplicación [AEM Forms (anteriormente denominada Mobile Workspace)](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## Funciones principales de la aplicación AEM Forms {#key-features-of-aem-forms-app}

### Aplicación AEM Forms con servidores AEM Forms {#aem-forms-app-with-aem-forms-servers}

Puede sincronizar la aplicación con el servidor AEM Forms y trabajar con formularios en el dispositivo móvil.

Con el servidor de flujo de trabajo de AEM Forms, un formulario se puede asociar con un punto de partida en un proceso de área de trabajo y con la aplicación Bandeja de entrada de AEM. Una aplicación AEM Inbox puede tener asociado un formulario adaptable. Un punto de partida puede tener asociado un formulario adaptable, HTML5 o un conjunto de formularios. Un punto de partida se puede enviar como tarea o la tarea se puede guardar como borrador. Para obtener más información sobre las diferencias entre una aplicación AEM Inbox y un punto de partida, consulte [Acciones y funciones de los Flujos de trabajo AEM centrados en el formulario en los flujos de trabajo](capabilities-osgi-jee-workflows.md)OSGi y JEE de AEM Forms.

Con el servidor AEM Forms sin flujo de trabajo de AEM Forms, se procesa un formulario habilitado para la sincronización en la aplicación en la aplicación AEM Forms. Los formularios están disponibles en la ficha Formularios de la aplicación y se pueden enviar o guardar como borrador. La aplicación admite formularios adaptables y formularios móviles.

1. **Guardar una tarea o un formulario como borrador**

   La opción Guardar como borrador guarda una instantánea de una tarea o formulario junto con los datos rellenados y los archivos adjuntos en el formulario asociado. Los borradores se guardan en el dispositivo móvil y se sincronizan con el servidor de AEM Forms para una recuperación posterior.

   Consulte [Guardado de una tarea o formulario como borrador](/help/forms/using/save-as-draft.md).

1. **Guardar formulario como plantilla**

   A veces, cuando los usuarios rellenan un formulario, las entradas de algunos campos siguen siendo las mismas. En estos casos, puede rellenar los campos que requieren valores idénticos en cada instancia y guardar el formulario o borrador como plantilla. Ahora, cada vez que crea una instancia de la plantilla, los campos especificados ya se rellenan con los valores especificados en la plantilla. Le ayuda a ahorrar tiempo y esfuerzo para rellenar el formulario.

   Consulte [Guardar formularios como plantillas](/help/forms/using/save-forms-and-start-points-as-templates.md).

### Uso de tareas y formularios {#working-with-tasks-and-forms}

Puede sincronizar la aplicación con el servidor de flujo de trabajo de AEM Forms y trabajar con tareas y formularios en su dispositivo móvil.

Una tarea en el dispositivo móvil contiene un formulario adaptable, un formulario HTML5 o un conjunto de formularios, y también puede contener archivos adjuntos y una dirección URL [de](/help/forms/using/getting-task-variables-summary-url.md)resumen. De forma predeterminada, las tareas asignadas se colocan en la carpeta **[!UICONTROL Tareas]** . Al trabajar en una tarea, puede cambiar la tarea y guardar una copia de borrador de la tarea en el servidor de AEM Forms.

Un formulario del dispositivo móvil puede ser un formulario adaptable o un formulario móvil. Los formularios habilitados para la sincronización en la aplicación de formularios están disponibles en la carpeta Forms. Puede sincronizar formularios habilitados en el servidor de AEM Forms sin el flujo de trabajo de AEM Forms (AEM Forms en OSGi).

Consulte:

* [Apertura de una tarea](/help/forms/using/open-task.md)
* [Uso de un formulario](/help/forms/using/working-with-form.md)

### Trabajar sin conexión {#working-offline}

Puede trabajar en el dispositivo móvil en modo sin conexión. Puede iniciar sesión en la aplicación incluso si no hay conectividad de red y puede trabajar en todos los formularios sincronizados con el dispositivo cuando estuvo en línea por última vez. Para obtener más información sobre cómo sincronizar los formularios, consulte [Sincronización de la aplicación](/help/forms/using/sync-app.md). Si decide sincronizar los datos adjuntos asociados a un formulario, también puede abrirlos en modo sin conexión. Puede editar el formulario, agregar anotaciones y enviar o guardar un formulario en modo sin conexión. El formulario se sincroniza con el servidor de AEM Forms la próxima vez que esté en línea.

Para obtener más información, consulte [Trabajo en modo](/help/forms/using/work-offline-mode.md)sin conexión.

### Adding annotations {#adding-annotations}

Puede agregar los siguientes datos adjuntos a un formulario en el dispositivo móvil

* **Notas**: Puede utilizar la función Notas para agregar un garabato a mano alzada o una nota de texto en el formulario. Para obtener más información, consulte [Añadir una nota](/help/forms/using/add-attachments.md#adding-a-note).

* **Imagen**: la aplicación AEM Forms incluye una función que utiliza la funcionalidad de cámara o la galería del dispositivo móvil. Con el archivo adjunto de la fotografía, puede añadir una fotografía con el formulario asociado. Para obtener más información, consulte [Añadir una fotografía](/help/forms/using/add-attachments.md#adding-a-photograph).

### Autoguardar {#autosave}

Cuando un usuario introduce datos en la aplicación AEM Forms, la función de guardado automático los guarda a intervalos regulares. La función de guardado automático de la aplicación AEM Forms le ayuda a evitar la pérdida de datos si la aplicación se cierra debido a condiciones como la batería baja.

Consulte [Uso del guardado automático en la aplicación](/help/forms/using/autosave-data-app.md)AEM Forms.

## Diferencias entre la bandeja de entrada de AEM y las funciones de la aplicación AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Dos de las principales formas de iniciar un flujo de trabajo centrado en formularios son utilizar la bandeja de entrada [y la aplicación AEM Forms de](/help/forms/using/manage-applications-inbox.md) AEM. Sin embargo, las funciones de la bandeja de entrada y la aplicación de AEM Forms de AEM difieren. La bandeja de entrada de AEM solo funciona con flujos de trabajo [centrados en](/help/forms/using/aem-forms-workflow.md) formularios, mientras que la aplicación AEM Forms funciona tanto con flujos de trabajo centrados en formularios como con la administración de procesos. Para obtener más información sobre las diferencias entre las funciones de la aplicación AEM Inbox y AEM Forms, consulte [Acciones y funciones de los Flujos de trabajo de AEM centrados en formularios en OSGi y flujos de trabajo](capabilities-osgi-jee-workflows.md)JEE de AEM Forms.

## Formularios admitidos {#supported-forms}

Tipos de formularios admitidos en la aplicación AEM Forms:

### Formulario adaptable {#adaptive-form}

La aplicación AEM Forms admite un formulario adaptable que se adapta dinámicamente a las entradas del usuario. También se admiten formularios adaptables cargados de forma diferida.

### Formulario móvil {#mobile-form}

Puede crear formularios para dispositivos móviles en AEM Forms. Los formularios móviles se representan como formularios HTML en dispositivos móviles que se adaptan según los dispositivos de visualización.

### Conjunto de formularios {#formset}

Con los conjuntos de formularios, se pueden agrupar varios formularios relacionados con un servicio o proceso para automatizar un proceso empresarial y presentarlos a los usuarios finales. En este escenario, los usuarios pueden rellenar todo el conjunto como uno y no es necesario archivar, enviar y rastrear formularios o procesos individuales.

>[!NOTE]
>
>Requiere flujo de trabajo de AEM Forms (AEM Forms en JEE).

## Funcionamiento de la aplicación AEM Forms {#how-aem-forms-app-works}

La aplicación AEM Forms proporciona una solución móvil para que los trabajadores de campo trabajen en formularios asignados a ellos. La aplicación almacena en caché todos los datos del servidor y proporciona una experiencia de usuario eficaz al guardar todo el trabajo localmente. Los datos del disco se envían al servidor mediante actualizaciones de sincronización oportunas.

La aplicación AEM Forms es una aplicación basada en PhoneGap 5.0 en la que el modelo Backbone se utiliza de forma eficaz para presentar los datos almacenados en los modelos mediante vistas. Todas las operaciones nativas se realizan a través de los complementos PhoneGap.

## Personalización, compilación y distribución de la aplicación AEM Forms {#customize-build-distribute}

>[!NOTE]
>
>Aplicable solo si utiliza el código fuente de la aplicación AEM Forms para crear la aplicación.

La aplicación AEM Forms es fácil de personalizar para las necesidades específicas de la organización. El código fuente de la aplicación se proporciona junto con AEM Forms. Puede cambiar el código fuente y crear su propia solución de mano de obra móvil. También puede firmar la aplicación con su propia clave de empresa.

### Personalizar {#customize}

Puede personalizar la aplicación para:

**Marca**: Cambie el icono de la aplicación, el nombre de la aplicación, las imágenes de inicio y las páginas en la aplicación AEM Forms. También puede cambiar el texto para localizar la aplicación en una región específica. Para obtener más información sobre la personalización de la marca en la aplicación AEM Forms, consulte Personalización [de la marca](/help/forms/using/branding-customization.md).

**Tema**: Cambie estilos como colores, fuentes y espaciado en la interfaz de usuario de la aplicación AEM Forms. Para obtener más información, consulte Personalización [de temas](/help/forms/using/theme-customization.md).

**Gesto**: Cambie los gestos, como el barrido a la derecha y el barrido a la izquierda, en la interfaz de usuario de la aplicación AEM Forms. Para obtener más información, consulte Personalización [de gestos](/help/forms/using/gesture-customization.md).

Para obtener más información sobre la configuración de un proyecto de aplicación para AEM Forms con fines de personalización, consulte:

* [Configuración de la aplicación entorno para AEM Forms](/help/forms/using/setup-environment-mobile-workspace.md)
* [Configuración del proyecto de Visual Studio y creación de una aplicación de Windows](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Configuración del proyecto Xcode y creación de una aplicación de iOS](/help/forms/using/setup-xcode-project-build-installer.md)
* [Configure el proyecto de Eclipse y cree una aplicación de Android](/help/forms/using/setup-eclipse-project-build-installer.md)

### Generar y distribuir {#build-and-distribute}

El código fuente de la aplicación AEM Forms se puede extraer de adobe-lc-mobileWorkspace-src.zip, que está disponible como parte del paquete de origen de la aplicación AEM Forms en el uso compartido de paquetes.

Para obtener el origen de la aplicación AEM Forms, realice los siguientes pasos:

1. Navegar al recurso compartido de paquetes

   URL: `https://<server>:<port>/crx/packageshare`.

1. Descargue el paquete de origen. Al descargar el paquete, se agrega en el administrador de paquetes de AEM Forms.
1. Después de descargarlo, navegue a: `https://<server>:<port>/crx/packmgr/index.jsp`e instalar `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

1. Para descargar el paquete, ábralo `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` en el navegador.

   El paquete de origen se descarga en el dispositivo.

**Para iOS**:

Para obtener más información sobre cómo crear una aplicación de iOS (.ipa), consulte [Configuración del proyecto Xcode y compilación de la aplicación](/help/forms/using/setup-xcode-project-build-installer.md)de iOS.

Para obtener más información sobre cómo firmar la aplicación AEM Forms con el perfil de aprovisionamiento, consulte Configuración, proceso y resolución de problemas [de firma de código de](https://developer.apple.com/support/code-signing/)iOS.

**Para Android**:

Para obtener más información sobre cómo crear una aplicación de Android (.apk), consulte [Configuración del proyecto Eclipse y creación de la aplicación](/help/forms/using/setup-eclipse-project-build-installer.md)de Android.

Para obtener más información sobre cómo firmar la aplicación AEM Forms, consulte [Firma de aplicaciones](https://developer.android.com/tools/publishing/app-signing.html).

**Para Windows**:

Para obtener más información sobre cómo crear una aplicación de Windows (.appx), consulte [Configuración del proyecto de Visual Studio y compilación de la aplicación](/help/forms/using/setup-visual-studio-project-build-installer.md)de Windows.

Para obtener más información sobre cómo distribuir la aplicación a través de MDM, consulte [Distribución de aplicaciones](/help/forms/using/distribute-mobile-workspace-app.md)de AEM Forms. La distribución de aplicaciones mediante MDM solo se aplica a iOS y Android.

## Recomendaciones para actualizar Mobile Workspace a la aplicación AEM Forms {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

Si está actualizando a la versión más reciente de la aplicación AEM Forms, asegúrese de leer los siguientes puntos:

* **Si ha instalado una versión anterior de la aplicación desde la tienda de reproducción en Android**, puede actualizar la aplicación directamente desde la tienda de reproducción.

* **Si la versión anterior de la aplicación se crea e instala con el código fuente (aplicable para iOS y Android)**:

   Antes de instalar la nueva aplicación, sincronice todos los datos con el servidor de AEM Forms. Después de sincronizar los datos, desinstale la versión anterior de la aplicación e instale la nueva aplicación.

