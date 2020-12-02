---
title: Creación de un perfil personalizado para formularios HTML5
seo-title: Creación de un perfil personalizado para formularios HTML5
description: Un perfil de formularios HTML5 es un nodo de recursos en Apache Sling. Representa una versión personalizada del servicio de procesamiento de formularios HTML5.
seo-description: Un perfil de formularios HTML5 es un nodo de recursos en Apache Sling. Representa una versión personalizada del servicio de procesamiento de formularios HTML5.
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# Creación de un perfil personalizado para formularios HTML5 {#creating-a-custom-profile-for-html-forms}

Un perfil es un nodo de recursos en [Apache Sling](https://sling.apache.org/). Representa la versión personalizada del servicio de representación de formularios HTML5. Puede utilizar el servicio de representación de formularios HTML5 para personalizar el aspecto, el comportamiento y las interacciones de los formularios HTML5. Existe un nodo de perfil en la carpeta `/content` del repositorio JCR. Puede colocar el nodo directamente en la carpeta `/content` o en cualquier subcarpeta de la carpeta `/content`.

El nodo perfil tiene la propiedad **sling:resourceSuperType** y el valor predeterminado es **xfaforms/perfil**. La secuencia de comandos de procesamiento del nodo se encuentra en /libs/xfaforms/perfil.

Los scripts Sling son scripts JSP. Estas secuencias de comandos JSP sirven como contenedores para reunir el HTML para el formulario solicitado y los artefactos JS/CSS requeridos. Estas secuencias de comandos de Sling también se denominan **secuencias de comandos del procesador de Perfil**. El procesador de perfil llama al servicio OSGi de Forms para procesar el formulario solicitado.

La secuencia de comandos de perfil está en html.jsp y html.POST.jsp para solicitudes de GET y POST. Puede copiar y modificar uno o varios archivos para anular y agregar las personalizaciones. No realice ningún cambio en el lugar, la actualización del parche sobrescribe dichos cambios.

Un perfil contiene varios módulos. Los módulos son formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_filename.jsp y Football.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

Los módulos formRuntime.jsp contienen referencias de las bibliotecas de cliente. También muestra métodos para extraer información de configuración regional de la solicitud e incluir los mensajes localizados en la misma. Puede incluir sus propias bibliotecas o estilos personalizados de JavaScript en formRuntime.jsp.

## config.jsp {#config-jsp}

El módulo config.jsp contiene varias configuraciones, como registro, servicios proxy y versión de comportamiento. Puede agregar su propia configuración y personalización de utilidades al módulo config.jsp. También puede agregar configuraciones como el registro de utilidades personalizadas al módulo config.jsp.

## toolbar.jsp {#toolbar-jsp}

El archivo toolbar.jsp contiene código para crear una barra de herramientas de color. Para quitar la barra de herramientas, elimine toolbar.jsp del archivo HTML.jsp

## formBody.jsp {#formbody-jsp}

El módulo formBody.jsp es para la representación HTML del formulario XFA.

## nav_filename.jsp {#nav-footer-jsp}

Al principio, el formulario HTML5 procesa solo la primera página del formulario. Cuando un usuario desplaza el formulario, se carga el resto de los formularios. Hace que la carga sea más rápida. El componente nav_ada.jsp contiene todos los estilos y elementos necesarios para facilitar la carga de las páginas al desplazarse.

## pie de página.jsp {#footer-jsp}

El módulo pie.jsp está vacío. Permite agregar secuencias de comandos que se utilizan únicamente para la interacción del usuario.

## Creación de Perfiles personalizados {#creating-custom-profiles}

Para crear un perfil personalizado, realice los siguientes pasos:

### Crear nodo de Perfil {#create-profile-node}

1. Vaya a la interfaz CRX DE en la dirección URL: `https://'[server]:[port]'/crx/de` e inicie sesión en la interfaz con credenciales de administrador.

1. En el panel izquierdo, navegue a la ubicación */content/xfaforms/perfiles*.

1. Copie el nodo predeterminado y pegue el nodo en otra carpeta (*/content/perfiles*) con el nombre *hrform*.

1. Seleccione el nuevo nodo, *hrform*, y agregue una propiedad de cadena: *sling:resourceType* con valor: *formulario/demostración*.

1. Haga clic en Guardar todo en el menú de la barra de herramientas para guardar los cambios.

### Crear la secuencia de comandos del procesador de perfil {#create-the-profile-renderer-script}

Después de crear un perfil personalizado, agregue información de procesamiento a este perfil. Al recibir una solicitud para el nuevo perfil, CRX comprueba la existencia de la carpeta /apps para la página JSP que se va a procesar. Cree la página JSP en la carpeta /apps.

1. En el panel izquierdo, desplácese a la carpeta `/apps`.
1. Haga clic con el botón derecho en la carpeta `/apps` y elija crear una carpeta con el nombre **formulario**.
1. Dentro de la carpeta **hrform** cree una carpeta con el nombre **demo**.
1. Haga clic en el botón **Guardar todo**.
1. Vaya a `/libs/xfaforms/profile/html.jsp` y copie el nodo **html.jsp**.
1. Pegue el nodo **html.jsp** en la carpeta `/apps/hrform/demo` creada anteriormente con el mismo nombre **html.jsp** y haga clic en **Guardar**.
1. Si tiene algún otro componente del script de perfil, siga los pasos 1 a 6 para copiar los componentes en la carpeta /apps/hrform/demo.

1. Para comprobar que se ha creado el perfil, abra la dirección URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

Para comprobar los formularios, [Importe los formularios](/help/forms/using/get-xdp-pdf-documents-aem.md) desde el sistema de archivos local a AEM Forms y [previsualización del formulario](/help/forms/using/previewing-forms.md) en AEM instancia de autor del servidor.
