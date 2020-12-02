---
title: Uso del espacio de trabajo de AEM Forms
seo-title: Uso del espacio de trabajo de AEM Forms
description: Comience con el espacio de trabajo de AEM Forms con esta rápida descripción general de los flujos de trabajo de proceso.
seo-description: Comience con el espacio de trabajo de AEM Forms con esta rápida descripción general de los flujos de trabajo de proceso.
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
translation-type: tm+mt
source-git-commit: 21efe30c6a69d04c737bc523aeaab504db8f605b
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---


# Uso del espacio de trabajo de AEM Forms{#working-with-aem-forms-workspace}

## Introducción {#introduction}

El espacio de trabajo de AEM Forms forma parte de AEM Forms. Workspace facilita la representación de HTML Forms además de PDF forms. Ahora puede participar en procesos empresariales desde interfaces móviles y aplicaciones web.

Además, el espacio de trabajo de AEM Forms es altamente personalizable mediante las metodologías de desarrollo estándar de HTML y JavaScript™. Es un software basado en componentes que se integra fácilmente con sus otras aplicaciones web.

Para obtener más información, consulte [Introducción al espacio de trabajo de AEM Forms](/help/forms/using/introduction-html-workspace.md).

## Familiarizarse {#getting-familiar}

Para familiarizarse con el proceso completo de creación de una aplicación de formularios para automatizar un proceso empresarial, siga el tutorial. Puede crear, administrar y probar una aplicación mediante el espacio de trabajo Workbench, Designer y AEM Forms después de seguir el tutorial. Para obtener más información sobre la implementación, consulte [Creación de la primera aplicación de AEM Forms](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html).

## Información general funcional {#functional-overview}

Puede utilizar el espacio de trabajo de AEM Forms para realizar las siguientes tareas:

**Inicio de un proceso empresarial:el espacio de trabajo de** AEM Forms categoría los procesos según lo diseñado y configurado por su organización. Puede marcar como favoritas las categorías usadas con frecuencia para acceder rápidamente a las categorías. Cuando se inicio un proceso, normalmente se rellena un formulario para inicio de un proceso empresarial que realiza controles de flujo de trabajo de formularios. Para obtener más información, consulte [Procesos de inicio](/help/forms/using/starting-processes.md).

**Vista y actuar en función de tareas:** cuando realiza la vista de sus listas de tareas pendientes, verá tareas de un proceso empresarial que se le hayan asignado, o de cualquier grupo al que pertenezca o que sean tareas compartidas de otros usuarios. Puede abrir, trabajar y completar las tareas según sea necesario. Normalmente, completar una tarea implica proporcionar información, aprobar un formulario o rechazar un formulario. Para obtener más información, consulte [Uso de listas de tareas pendientes](/help/forms/using/todo-lists.md).

**Tareas** de seguimiento: Para realizar el seguimiento de sus tareas, utilice la ficha Seguimiento del espacio de trabajo de AEM Forms. Puede buscar los procesos activos o completados que inició o en los que participó. Puede realizar la vista de las tareas, asignaciones y formularios que formaban parte del proceso. También puede inicio nuevos procesos mediante datos de formulario de un proceso que haya iniciado anteriormente. Para obtener más información, consulte [Procesos de seguimiento](/help/forms/using/tracking-processes.md).

## Nueva oferta de espacio de trabajo de AEM Forms {#new-offering-of-aem-forms-workspace}

**Compatibilidad para la aprobación masiva de tareas**:

Puede aprobar varias tareas del mismo tipo. Una vez seleccionada una tarea para aprobación, solo permanecerán habilitadas las tareas con el mismo proceso, con los mismos nombres de tarea y las mismas opciones de ruta. Consulte [Uso de listas pendientes](/help/forms/using/todo-lists.md) para obtener detalles de implementación.

## Migración desde Flex Workspace al área de trabajo de AEM Forms {#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex Workspace no es compatible con los clientes de AEM Forms. Todos los clientes que utilicen Flex Workspace deben mudarse a AEM Forms Workspace.

En el espacio de trabajo de AEM Forms, los servicios de procesamiento y envío predeterminados, en el perfil de acción predeterminado, asociados a los formularios XDP, han cambiado y se han introducido nuevos servicios. Para obtener más información, consulte [Nuevo servicio de procesamiento y envío](/help/forms/using/new-render-submit-service.md). Para migrar los procesos existentes, que funcionan con formularios XDP, para utilizar estos servicios, puede seguir [estos pasos](new-render-submit-service.md).

**Asignación de personalizaciones de Flex Workspace con el espacio de trabajo de AEM Forms**

La asignación entre varios tipos de personalizaciones en ambos espacios de trabajo es la siguiente.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de personalización </strong></td>
   <td><strong>Personalizaciones cubiertas </strong></td>
   <td><strong>Escenario de personalización del espacio de trabajo de AEM Forms correspondiente</strong></td>
  </tr>
  <tr>
   <td>Personalización de localizaciones</td>
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
     <li>Sustitución de imágenes</li>
     <li>Modificación de colores</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">Cambio del logotipo de organización</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">Cambio de la combinación de colores</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalización del diseño</td>
   <td>
    <ol>
     <li>Simplificación de la interfaz de usuario de Workspace<br /> </li>
     <li>Creación de una nueva pantalla de inicio de sesión</li>
     <li>Creación de un Contenedor de aprobación personalizado</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">Uso de componentes reutilizables</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">Creación de una nueva pantalla de inicio de sesión</a></li>
     <li>El Contenedor de aprobación está obsoleto.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Algunas de las funciones de Flex Workspace que no están disponibles en el espacio de trabajo de AEM Forms incluyen: mensajes y notificaciones, página de bienvenida, contenedor de aprobación y opción para administrar encabezados de columna. Para obtener una lista completa, consulte [Funciones de Flex Workspace no disponibles en el área de trabajo de AEM Forms](/help/forms/using/features-flex-workspace-available-html.md).

## Desarrollo con el espacio de trabajo de AEM Forms {#developing-with-aem-forms-workspace}

### Arquitectura {#architecture}

El espacio de trabajo de AEM Forms es una aplicación web basada en HTML y JavaScript™ alojada en CRX™. Cuando se abre la URL del espacio de trabajo en un navegador, se accede a un recurso CRX™ y la aplicación se representa como una página HTML en el navegador. Las bibliotecas de JavaScript y el código JavaScript personalizado administran el comportamiento interno y externo de la aplicación, como la interfaz de usuario, la interacción del usuario y la comunicación con el servidor de AEM Forms. Para obtener más información, consulte Espacio de trabajo de AEM Forms [arquitectura](/help/forms/using/html-workspace-architecture.md).

### Personalización del espacio de trabajo de AEM Forms {#aem-forms-workspace-customization}

El espacio de trabajo de AEM Forms admite una amplia variedad de personalizaciones para actualizar el diseño de la interfaz de usuario, su apariencia, funcionalidad y mucho más. Las personalizaciones implican actualizar una o varias de las siguientes opciones:

* Aspectos visuales de la interfaz de usuario
* Funcionalidad mediante personalizaciones semánticas
* Reutilización de componentes HTML en otras aplicaciones web

El artículo [personalización](introduction-customizing-html-workspace.md#types-of-customizations) explica los tipos de dichas personalizaciones.

### Configure el entorno de programadores {#set-up-the-developer-environment}

Los elementos que se pueden entregar en el espacio de trabajo de AEM Forms incluyen un paquete CRX implementado en CRX, un archivo SDK que contiene el código fuente completo, bibliotecas JavaScript de terceros y secuencias de comandos de compilación del espacio de trabajo de AEM Forms. Utilícelos para configurar el entorno del desarrollador para realizar las personalizaciones mencionadas anteriormente. Para obtener más información, consulte [Generación del código del espacio de trabajo de AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

Puede personalizar una parte importante de la interfaz y la funcionalidad básica, como fuentes, combinación de colores, logotipo, pantalla de inicio de sesión, diálogos de error, integración con aplicaciones de terceros y reutilización de componentes en aplicaciones de terceros. También puede mejorar el contenido mostrado en la página Resumen de Tarea, mostrar imágenes para acciones de ruta de tarea e incluso modificar los modelos y Vistas de red troncal de bajo nivel que crean la aplicación de espacio de trabajo de AEM Forms.

### Representación HTML de XDP Forms {#html-rendering-of-xdp-forms}

De forma predeterminada, para un nuevo proceso, un formulario XDP se procesa en formato PDF en un escritorio y en formato HTML en una tablet. Siempre es posible procesar un formulario XDP en formato HTML. Para obtener más información, consulte [Nuevos servicios de procesamiento y envío](/help/forms/using/new-render-submit-service.md).

[La función ](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) Formularios móviles, que funciona con  [perfiles](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html), habilita la representación HTML de formularios XDP. De forma predeterminada, el perfil &#39;Representar nuevo formulario HTML&#39; utiliza `default.html`, que puede cambiar. También puede agregar cambios personalizados que se producen antes de procesar un formulario XDP en formato HTML.

## Aplicación de espacio de trabajo de AEM Forms {#aem-forms-workspace-app}

Para trabajar en los procesos empresariales en un dispositivo móvil, puede utilizar la oferta de aplicaciones de espacio de trabajo de AEM Forms de AEM Forms. Para obtener más información, consulte la [descripción general de la aplicación del espacio de trabajo de AEM Forms](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html).
