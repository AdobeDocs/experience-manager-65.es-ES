---
title: Uso del espacio de trabajo de AEM Forms
seo-title: Working with AEM Forms workspace
description: Empiece con el espacio de trabajo de AEM Forms con esta breve descripción general de los flujos de trabajo de proceso.
seo-description: Get started with AEM Forms workspace with this quick overview of the process workflows.
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
exl-id: 0bedcbd9-2cf8-47da-9440-c773982e550c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Uso del espacio de trabajo de AEM Forms{#working-with-aem-forms-workspace}

## Introducción {#introduction}

El espacio de trabajo de AEM Forms forma parte de AEM Forms. Workspace facilita la representación de Forms HTML además de los PDF forms. Ahora puede participar en procesos empresariales desde interfaces móviles y aplicaciones web.

Además, el espacio de trabajo de AEM Forms es altamente personalizable mediante el HTML estándar y las metodologías de desarrollo de JavaScript™ . Es un software basado en componentes que se integra fácilmente con sus otras aplicaciones web.

Para obtener más información, consulte [Introducción al espacio de trabajo de AEM Forms](/help/forms/using/introduction-html-workspace.md).

## Familiarizarse {#getting-familiar}

Para familiarizarse con el proceso completo de creación de una aplicación de formularios para automatizar un proceso empresarial, siga el tutorial. Puede crear, administrar y probar una aplicación mediante Workbench, Designer y el espacio de trabajo de AEM Forms después de seguir el tutorial. Para obtener más información sobre la implementación, consulte [Creación de la primera aplicación de AEM Forms](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html).

## Información general funcional {#functional-overview}

Puede utilizar el espacio de trabajo de AEM Forms para realizar las siguientes tareas:

**Iniciar un proceso empresarial:** El espacio de trabajo de AEM Forms clasifica los procesos según se han diseñado y configurado en la organización. Puede marcar como favorito las categorías más utilizadas para acceder rápidamente a las categorías. Cuando se inicia un proceso, normalmente se rellena un formulario para iniciar un proceso empresarial que controla el flujo de trabajo de formularios. Para obtener más información, consulte [Inicio de procesos](/help/forms/using/starting-processes.md).

**Ver y actuar en función de las tareas:** Cuando vea las listas de tareas pendientes, verá las tareas de un proceso empresarial que esté asignado a usted, a cualquier grupo al que pertenezca o que sean las tareas compartidas de otros usuarios. Puede abrir, trabajar y completar las tareas según sea necesario. Normalmente, completar una tarea implica proporcionar información, aprobar un formulario o rechazar un formulario. Para obtener más información, consulte [Uso de listas de tareas pendientes](/help/forms/using/todo-lists.md).

**Seguimiento de tareas**: Para realizar el seguimiento de sus tareas, utilice la pestaña Tracking del espacio de trabajo de AEM Forms. Puede buscar procesos activos o completados que haya iniciado o en los que haya participado. Puede ver las tareas, asignaciones y formularios que formaban parte del proceso. También puede iniciar nuevos procesos utilizando los datos de formulario de un proceso que haya iniciado anteriormente. Para obtener más información, consulte [Seguimiento de procesos](/help/forms/using/tracking-processes.md).

## Nueva oferta de espacio de trabajo de AEM Forms {#new-offering-of-aem-forms-workspace}

**Soporte para la aprobación masiva de tareas**:

Puede aprobar varias tareas del mismo tipo. Una vez que seleccione una tarea para su aprobación, solo permanecerán habilitadas las tareas con el mismo proceso, con los mismos nombres de tareas y las mismas opciones de ruta. Consulte [Uso de listas de tareas pendientes](/help/forms/using/todo-lists.md) para obtener más información sobre la implementación.

## Migración de Flex Workspace a AEM Forms Workspace {#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex Workspace no es compatible con los clientes de AEM Forms. Todos los clientes que utilicen Flex Workspace deben pasar a AEM Forms Workspace.

En el espacio de trabajo de AEM Forms, los servicios de procesamiento y envío predeterminados, en el perfil de acción predeterminado, asociados a los formularios XDP, han cambiado y se han introducido nuevos servicios. Para obtener más información, consulte [Nuevo servicio de renderización y envío](/help/forms/using/new-render-submit-service.md). Para migrar los procesos existentes, que funcionan con formularios XDP, para utilizar estos servicios, puede seguir [estos pasos](new-render-submit-service.md).

**Asignación de las personalizaciones de Flex Workspace con el espacio de trabajo de AEM Forms**

La asignación entre varios tipos de personalizaciones en ambos espacios de trabajo es la siguiente:

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de personalización </strong></td>
   <td><strong>Personalizaciones cubiertas </strong></td>
   <td><strong>Situación de personalización del espacio de trabajo de AEM Forms correspondiente</strong></td>
  </tr>
  <tr>
   <td>Personalización de la localización</td>
   <td>
    <ol>
     <li>Cambio de la configuración regional de Workspace</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">Cambio de la configuración regional del espacio de trabajo de AEM Forms</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalización de temas</td>
   <td>
    <ol>
     <li>Reemplazo de imágenes</li>
     <li>Modificación de colores</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">Cambio del logotipo de la organización</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">Cambio del esquema de color</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalización del diseño</td>
   <td>
    <ol>
     <li>Simplificación de la interfaz de usuario de Workspace<br /> </li>
     <li>Creación de una nueva pantalla de inicio de sesión</li>
     <li>Creación de un contenedor de aprobación personalizado</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">Uso de componentes reutilizables</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">Creación de una nueva pantalla de inicio de sesión</a></li>
     <li>El contenedor de aprobación está obsoleto.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Algunas de las funciones de Flex Workspace que no están disponibles en el espacio de trabajo de AEM Forms son: mensajes y notificaciones, página de bienvenida, contenedor de aprobación y opción para administrar encabezados de columna. Para obtener una lista completa, consulte [Funciones de Flex Workspace no disponibles en AEM Forms Workspace](/help/forms/using/features-flex-workspace-available-html.md).

## Desarrollo con el espacio de trabajo de AEM Forms {#developing-with-aem-forms-workspace}

### Arquitectura {#architecture}

AEM Forms workspace es una aplicación web basada en HTML y JavaScript™ alojada en CRX™. Cuando se abre la URL de Workspace en un explorador, se accede a un recurso CRX™ y la aplicación se representa como una página HTML en el explorador. Las bibliotecas de JavaScript y el código personalizado de JavaScript administran el comportamiento interno y externo de la aplicación, como la interfaz de usuario, la interacción del usuario y la comunicación con el servidor de AEM Forms. Para obtener más información, consulte Espacio de trabajo de AEM Forms [arquitectura](/help/forms/using/html-workspace-architecture.md).

### Personalización del espacio de trabajo de AEM Forms {#aem-forms-workspace-customization}

El espacio de trabajo de AEM Forms admite una amplia variedad de personalizaciones para actualizar el diseño de la interfaz de usuario, su apariencia, funcionalidad y mucho más. Las personalizaciones implican actualizar una o más de las siguientes opciones:

* Aspectos visuales de la interfaz de usuario
* Funcionalidad mediante personalizaciones semánticas
* Reutilización de componentes de HTML en otras aplicaciones web

La variable [personalización](introduction-customizing-html-workspace.md#types-of-customizations) explica los tipos de dichas personalizaciones.

### Configuración del entorno de desarrollo {#set-up-the-developer-environment}

Los resultados del espacio de trabajo de AEM Forms incluyen un paquete CRX implementado en CRX, un archivo SDK que contiene el código fuente completo, bibliotecas JavaScript de terceros y scripts de compilación del espacio de trabajo de AEM Forms. Utilícelos para configurar el entorno de desarrollo y realizar las personalizaciones mencionadas anteriormente. Para obtener más información, consulte [Creación del código de espacio de trabajo de AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

Puede personalizar una parte importante de la interfaz y la funcionalidad principal, como fuentes, combinación de colores, logotipo, pantalla de inicio de sesión, diálogos de error, integración con aplicaciones de terceros y reutilización de componentes en aplicaciones de terceros. También puede mejorar el contenido mostrado en la página Resumen de tareas, mostrar imágenes para acciones de ruta de tareas e incluso modificar las vistas y los modelos de estructura básica de bajo nivel que crean la aplicación de espacio de trabajo de AEM Forms.

### Renderización del HTML de XDP Forms {#html-rendering-of-xdp-forms}

De forma predeterminada, para un nuevo proceso, un formulario XDP se procesa en formato PDF en un equipo de escritorio y en formato HTML en una tableta. Es posible procesar siempre un formulario XDP en formato HTML. Para obtener más información, consulte [Nuevos servicios de procesamiento y envío](/help/forms/using/new-render-submit-service.md).

[Forms móvil](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) que funciona con [perfiles](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html), habilita la representación HTML de formularios XDP. De forma predeterminada, la opción &quot;Renderizar nuevo formulario de HTML&quot; utiliza `default.html` que puede cambiar. También puede agregar cambios personalizados que se produzcan antes de procesar un formulario XDP en formato de HTML.

## aplicación de espacio de trabajo de AEM Forms {#aem-forms-workspace-app}

Para trabajar en los procesos empresariales en un dispositivo móvil, puede utilizar la oferta de aplicación de espacio de trabajo de AEM Forms de AEM Forms. Para obtener más información, consulte la [Información general de la aplicación del espacio de trabajo de AEM Forms](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html).
