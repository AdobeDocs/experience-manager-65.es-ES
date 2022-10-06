---
title: Directrices para la resolución de problemas del espacio de trabajo de AEM Forms
seo-title: Troubleshooting guidelines for AEM Forms workspace
description: Habilite los registros y utilice Debugger en el explorador para solucionar problemas del espacio de trabajo de AEM Forms.
seo-description: Enable logs and use debugger in browser to troubleshoot AEM Forms workspace.
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
exl-id: a054b60a-5e89-4c98-87bc-35669988d160
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 1%

---

# Directrices para la resolución de problemas del espacio de trabajo de AEM Forms {#troubleshooting-guidelines-for-aem-forms-workspace}

Este artículo explica cómo depurar el espacio de trabajo de AEM Forms habilitando el registro y utilizando Debugger en un explorador. También se explican algunos problemas comunes que se pueden encontrar al utilizar el espacio de trabajo de AEM Forms y sus soluciones.

## No se puede instalar el paquete de espacio de trabajo de AEM Forms {#unable-to-install-aem-forms-workspace-package}

Después de instalar el parche, abra el espacio de trabajo de AEM Forms. Si encuentra el error No se encontró ningún recurso, abra el Administrador de paquetes CRX y vuelva a instalar el `adobe-lc-workspace-pkg-<version>.zip` paquete.

Al instalar el paquete, si se produce un error `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`, realice los pasos siguientes:

1. Inicie sesión en CRX DE lite. La dirección URL predeterminada es `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. Elimine el siguiente nodo:

   `/home/groups/P/PERM_WORKSPACE_USER`

1. Vaya al Administrador de paquetes. El URL predeterminado es `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. Busque e instale la variable `adobe-lc-workspace-pkg-[version].zip` paquete.
1. Reinicie el servidor de aplicaciones.

## Registro del espacio de trabajo de AEM Forms {#aem-forms-workspace-nbsp-logging}

Puede generar registros en varios niveles para permitir una solución óptima de los errores. Por ejemplo, en una aplicación compleja, el registro en el nivel de componente ayuda a depurar y solucionar problemas de componentes específicos.

En el espacio de trabajo de AEM Forms:

* Para obtener la información de registro sobre un archivo de componente específico, añada `/log/<ComponentFile>/<LogLevel>` en la dirección URL y pulse `Enter`. Toda la información de registro del archivo de componente en el nivel de registro especificado se imprime en la consola.

* Para obtener la información de registro de todos los archivos de componente, anexe `/log/all/trace` en la dirección URL y pulse `Enter`.

* Formato de registro: `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>De forma predeterminada, el nivel de registro de todos los componentes está establecido en INFO.

* El nivel de registro configurado por el usuario se mantiene solamente para esa sesión del explorador. Cuando el usuario actualiza la página, el nivel de registro se establece en su valor inicial para todos los componentes.

### Lista de archivos de componentes en el espacio de trabajo de AEM Forms {#list-of-component-files-in-nbsp-aem-forms-workspace}

<table>
 <tbody>
  <tr>
   <td><p>allcategoryModel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>tasklistModel</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>vista de lista de tareas</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>processnamelistModel</p> </td>
   <td><p>taskModel</p> </td>
  </tr>
  <tr>
   <td><p>categorylistModel</p> </td>
   <td><p>processnamelistView</p> </td>
   <td><p>taskView</p> </td>
  </tr>
  <tr>
   <td><p>categorylistView</p> </td>
   <td><p>processnameModel</p> </td>
   <td><p>teamqueueView</p> </td>
  </tr>
  <tr>
   <td><p>categoryModel</p> </td>
   <td><p>processnameView</p> </td>
   <td><p>todoView</p> </td>
  </tr>
  <tr>
   <td><p>categoryView</p> </td>
   <td><p>searchtemplatedetailsView</p> </td>
   <td><p>trackingView</p> </td>
  </tr>
  <tr>
   <td><p>favoritecategoryModel</p> </td>
   <td><p>sharequeueModel</p> </td>
   <td><p>uisettingsModel</p> </td>
  </tr>
  <tr>
   <td><p>filterlistView</p> </td>
   <td><p>sharequeueView</p> </td>
   <td><p>uisettingsView</p> </td>
  </tr>
  <tr>
   <td><p>filterView</p> </td>
   <td><p>startpointlistModel</p> </td>
   <td><p>userinfoModel</p> </td>
  </tr>
  <tr>
   <td><p>outofofficeModel</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>outofofficeView</p> </td>
   <td><p>startpointModel</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>PreferencesView</p> </td>
   <td><p>startView</p> </td>
   <td><p>usersearchView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancehistoryView</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>wserrorModel</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistModel</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>wserrorView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistView</p> </td>
   <td><p>taskdetailsView</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### Niveles de registro disponibles en el espacio de trabajo de AEM Forms {#log-levels-available-in-nbsp-aem-forms-workspace}

* FATAL
* ERROR
* AVISAR
* INFORMACIÓN
* DEPURACIONES
* TRACE
* DESACTIVADO

## Depuración de información para exploradores {#debugging-information-for-browsers}

Las secuencias de comandos y los estilos se pueden depurar en distintos navegadores.

* **Depuración en IE**: Para depurar el espacio de trabajo de AEM Forms en IE, consulte: [https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx](https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx).

* **Depuración en Chrome**: Para abrir Debugger en Chrome, utilice el método abreviado: Ctrl + Mayús + I. Para obtener más información, consulte: [https://developer.chrome.com/extensions/tut_debugging.html](https://developer.chrome.com/extensions/tut_debugging.html).

* **Depuración en Firefox**: Hay varios complementos disponibles para depurar scripts y estilos en Firefox. Por ejemplo, Firebug es una de estas utilidades de depuración ([https://getfirebug.com](https://getfirebug.com)).

## Preguntas frecuentes {#faqs}

1. El formulario de PDF no se está procesando ni enviando en Google Chrome.

   1. Instale el complemento Adobe® Reader®.
   1. En Chrome, abra chrome://plugins para ver los complementos disponibles.
   1. Deshabilite el complemento Visor de PDF de Chrome y habilite el complemento Adobe Reader.

1. El formulario o la guía del SWF no se está procesando en Google Chrome.

   1. En Chrome, abra chrome://plugins para ver los complementos disponibles.
   1. Consulte los detalles para el complemento Adobe Flash® Player.
   1. Deshabilite PepperFlash en el complemento de Flash Player de Adobe.

1. He personalizado el espacio de trabajo de AEM Forms, pero no puedo ver los cambios.

   Borre la caché del explorador y, a continuación, acceda al espacio de trabajo de AEM Forms.

1. ¿Qué debe hacer el usuario para permitir que el formulario se procese en el HTML al abrirlo en el escritorio?

   Seleccione el botón de opción HTML del perfil predeterminado en el paso asignar tarea mientras utiliza Workbench.

1. Los datos adjuntos no se muestran cuando se hace clic en ellos.

   Para ver los archivos adjuntos, active las ventanas emergentes en el explorador.

1. Un usuario ha iniciado sesión en una aplicación de formularios. Si el usuario intenta iniciar sesión en el espacio de trabajo, es posible que no se cargue si no tiene permisos de espacio de trabajo.

   Cierre la sesión en la otra aplicación de formularios y, a continuación, inicie sesión en el espacio de trabajo.

1. Cuando se procesan en el espacio de trabajo de AEM Forms, los formularios HTML que utilizan Propiedades del proceso en su diseño muestran el botón Enviar dentro del formulario.

   Cuando se diseñan formularios, al utilizar Propiedades del proceso, se agrega un botón Enviar dentro del formulario. Cuando se representa como PDF en el espacio de trabajo de AEM Forms, el botón Enviar no es visible para el usuario final. Sin embargo, cuando se procesa como un formulario de HTML en el espacio de trabajo de AEM Forms, el botón Enviar es visible para el usuario final. Al hacer clic en este botón Enviar dentro del formulario, no se inicia ninguna acción. Al hacer clic en el botón Enviar en la parte inferior del espacio de trabajo de AEM Forms, fuera del formulario, se completa la tarea.
