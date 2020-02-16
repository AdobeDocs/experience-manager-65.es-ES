---
title: Uso del espacio de trabajo de AEM Forms
seo-title: Uso del espacio de trabajo de AEM Forms
description: Empiece a trabajar con el espacio de trabajo de AEM Forms con esta rápida descripción general de los flujos de trabajo del proceso.
seo-description: Empiece a trabajar con el espacio de trabajo de AEM Forms con esta rápida descripción general de los flujos de trabajo del proceso.
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Working with AEM Forms workspace{#working-with-aem-forms-workspace}

## Introducción {#introduction}

El espacio de trabajo de AEM Forms forma parte de AEM Forms. Workspace facilita la representación de formularios HTML además de los formularios PDF. Ahora puede participar en procesos empresariales desde interfaces móviles y aplicaciones web.

Además, el espacio de trabajo de AEM Forms es altamente personalizable mediante las metodologías de desarrollo estándar HTML y JavaScript™. Es un software basado en componentes que se integra fácilmente con sus otras aplicaciones web.

Para obtener más información, consulte [Introducción al espacio de trabajo](/help/forms/using/introduction-html-workspace.md)de AEM Forms.

## Familiarizarse {#getting-familiar}

Para familiarizarse con el proceso completo de creación de una aplicación de formularios para automatizar un proceso empresarial, siga el tutorial. Puede crear, administrar y probar una aplicación mediante el espacio de trabajo Workbench, Designer y AEM Forms después de seguir el tutorial. Para obtener más información sobre la implementación, consulte [Creación de la primera aplicación](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html)de AEM Forms.

## Información general funcional {#functional-overview}

Puede utilizar el espacio de trabajo de AEM Forms para realizar las siguientes tareas:

**** Iniciar un proceso comercial: El espacio de trabajo de AEM Forms clasifica los procesos tal como los diseñó y configuró su organización. Puede marcar como favoritas las categorías que se utilizan con frecuencia para acceder a ellas rápidamente. Cuando se inicia un proceso, normalmente se rellena un formulario para iniciar un proceso empresarial que formulario controles de flujo de trabajo. Para obtener más información, consulte [Inicio de procesos](/help/forms/using/starting-processes.md).

**** Ver y actuar según las tareas: Cuando ve las listas de tareas pendientes, ve las tareas de un proceso empresarial que están asignadas a usted, a cualquier grupo al que pertenezca o que sean tareas compartidas de otros usuarios. Puede abrir, trabajar y completar las tareas según sea necesario. Normalmente, completar una tarea implica proporcionar información, aprobar un formulario o rechazar un formulario. Para obtener más información, consulte [Uso de listas](/help/forms/using/todo-lists.md)de tareas pendientes.

**Tareas** de seguimiento: Para realizar el seguimiento de las tareas, utilice la ficha Seguimiento del espacio de trabajo de AEM Forms. Puede buscar los procesos activos o completados que inició o en los que participó. Puede ver las tareas, las asignaciones y los formularios que formaban parte del proceso. También puede iniciar nuevos procesos utilizando datos de formulario de un proceso que haya iniciado anteriormente. Para obtener más información, consulte [Seguimiento de procesos](/help/forms/using/tracking-processes.md).

## Nueva oferta de espacio de trabajo de AEM Forms {#new-offering-of-aem-forms-workspace}

**Compatibilidad con la aprobación masiva de tareas**:

Puede aprobar varias tareas del mismo tipo. Una vez seleccionada una tarea para aprobación, solo permanecerán habilitadas las tareas con el mismo proceso, con los mismos nombres de tareas y las mismas opciones de ruta. Consulte [Uso de listas](/help/forms/using/todo-lists.md) de tareas pendientes para obtener detalles de implementación.

## Migración de Flex Workspace al espacio de trabajo de AEM Forms {#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex Workspace no es compatible con los clientes de AEM Forms. Todos los clientes que utilicen Flex Workspace deben pasar a AEM Forms Workspace.

En el espacio de trabajo de AEM Forms, los servicios de procesamiento y envío predeterminados, en el perfil de acción predeterminado, asociados a formularios XDP, han cambiado y se han introducido nuevos servicios. Para obtener más información, consulte [Nuevo servicio](/help/forms/using/new-render-submit-service.md)de procesamiento y envío. Para migrar los procesos existentes, que funcionan con formularios XDP, y utilizar estos servicios, puede seguir [estos pasos](/help/forms/using/new-render-submit-service.md#main-pars-faq).

**Asignación de las personalizaciones de Flex Workspace con el espacio de trabajo de AEM Forms**

La asignación entre varios tipos de personalizaciones en ambos espacios de trabajo es la siguiente.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de personalización </strong></td>
   <td><strong>Personalizaciones cubiertas </strong></td>
   <td><strong>Escenario de personalización del espacio de trabajo de AEM Forms correspondiente</strong></td>
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

Algunas de las funciones de Flex Workspace que no están disponibles en el espacio de trabajo de AEM Forms son: mensajes y notificaciones, página de bienvenida, contenedor de aprobación y opción para administrar encabezados de columna. Para obtener una lista completa, consulte [Funciones de Flex Workspace no disponibles en el espacio de trabajo](/help/forms/using/features-flex-workspace-available-html.md)de AEM Forms.

## Desarrollo con el espacio de trabajo de AEM Forms {#developing-with-aem-forms-workspace}

### Arquitectura {#architecture}

El espacio de trabajo de AEM Forms es una aplicación web basada en HTML y JavaScript™ alojada en CRX™. Cuando se abre la URL del espacio de trabajo en un navegador, se accede a un recurso CRX™ y la aplicación se representa como una página HTML en el navegador. Las bibliotecas de JavaScript y el código JavaScript personalizado administran el comportamiento interno y externo de la aplicación, como la interfaz de usuario, la interacción del usuario y la comunicación con el servidor de AEM Forms. Para obtener más información, consulte [Arquitectura](/help/forms/using/html-workspace-architecture.md)del espacio de trabajo de AEM Forms.

### Personalización del espacio de trabajo de AEM Forms {#aem-forms-workspace-customization}

El espacio de trabajo de AEM Forms admite una amplia variedad de personalizaciones para actualizar el diseño de la interfaz de usuario, su apariencia, funcionalidad y mucho más. Las personalizaciones implican actualizar una o varias de las siguientes opciones:

* Aspectos visuales de la interfaz de usuario
* Funcionalidad mediante personalizaciones semánticas
* Reutilización de componentes HTML en otras aplicaciones web

El artículo de [personalización](/help/forms/using/introduction-customizing-html-workspace.md#main-pars-heading-0) explica los tipos de personalizaciones.

### Configuración del entorno de desarrollo {#set-up-the-developer-environment}

Los elementos que se pueden entregar en el espacio de trabajo de AEM Forms incluyen un paquete CRX implementado en CRX, un archivo SDK que contiene el código fuente completo, bibliotecas JavaScript de terceros y secuencias de comandos de compilación del espacio de trabajo de AEM Forms. Utilícelos para configurar el entorno de desarrollo para realizar las personalizaciones mencionadas anteriormente. Para obtener más información, consulte [Creación del código](/help/forms/using/introduction-customizing-html-workspace.md#main-pars-heading-3)del espacio de trabajo de AEM Forms.

Puede personalizar una parte importante de la interfaz y la funcionalidad básica, como fuentes, combinación de colores, logotipo, pantalla de inicio de sesión, diálogos de error, integración con aplicaciones de terceros y reutilización de componentes en aplicaciones de terceros. También puede mejorar el contenido mostrado en la página Resumen de tareas, mostrar imágenes para acciones de ruta de tareas e incluso modificar las vistas y los modelos de red troncal de bajo nivel que crean la aplicación de espacio de trabajo de AEM Forms.

### Representación HTML de formularios XDP {#html-rendering-of-xdp-forms}

De forma predeterminada, para un nuevo proceso, un formulario XDP se procesa en formato PDF en un escritorio y en formato HTML en una tablet. Siempre es posible procesar un formulario XDP en formato HTML. Para obtener más información, consulte [Nuevo servicio](/help/forms/using/new-render-submit-service.md)de procesamiento y envío.

[La función de formularios](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) móviles, que funciona con [perfiles](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html), activa la representación HTML de formularios XDP. De forma predeterminada, &#39;Representar nuevo formulario HTML&#39; utiliza `default.html` un perfil que puede cambiar. También puede agregar cambios personalizados que se producen antes de procesar un formulario XDP en formato HTML.

## Aplicación del espacio de trabajo de AEM Forms {#aem-forms-workspace-app}

Para trabajar en los procesos empresariales en un dispositivo móvil, puede utilizar la aplicación de espacio de trabajo de AEM Forms que ofrece AEM Forms. Para obtener más información, consulte Descripción general [de la aplicación del espacio de trabajo de](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html)AEM Forms.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
