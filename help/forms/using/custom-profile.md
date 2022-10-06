---
title: Creación de un perfil personalizado para formularios HTML5
seo-title: Creating a custom profile for HTML5 forms
description: Un perfil de formularios HTML5 es un nodo de recursos en Apache Sling. Representa una versión personalizada del servicio de procesamiento de formularios de HTML5.
seo-description: A HTML5 forms profile is a resource node in Apache Sling. It represents a customized version of HTML5 forms Render service.
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: Mobile Forms
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Creación de un perfil personalizado para formularios HTML5 {#creating-a-custom-profile-for-html-forms}

Un perfil es un nodo de recursos en [Apache Sling](https://sling.apache.org/). Representa la versión personalizada del servicio de representación de formularios de HTML5. Puede utilizar el servicio de representación de formularios de HTML5 para personalizar el aspecto, el comportamiento y las interacciones de los formularios de HTML5. Existe un nodo de perfil en la variable `/content` en el repositorio JCR. Puede colocar el nodo directamente debajo de la variable `/content` o cualquier subcarpeta de la `/content` carpeta.

El nodo de perfil tiene la variable **sling:resourceSuperType** y el valor predeterminado es **xfaforms/profile**. La secuencia de comandos de renderización para el nodo se encuentra en /libs/xfaforms/profile.

Los scripts de Sling son scripts JSP. Estas secuencias de comandos JSP sirven como contenedores para reunir el HTML del formulario solicitado y los artefactos JS/CSS necesarios. Estos scripts de Sling también se denominan **Scripts de renderizador de perfil**. El procesador de perfiles llama al servicio OSGi de Forms para procesar el formulario solicitado.

El script de perfil se encuentra en html.jsp y html.POST.jsp para solicitudes de GET y POST. Puede copiar y modificar uno o más archivos para anular y agregar las personalizaciones. No realice ningún cambio in situ, la actualización del parche sobrescribe dichos cambios.

Un perfil contiene varios módulos. Los módulos son formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp y footer.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

Los módulos formRuntime.jsp contienen referencias de las bibliotecas cliente. También muestra los métodos para extraer información de configuración regional de la solicitud e incluir los mensajes localizados en la solicitud. Puede incluir sus propias bibliotecas o estilos personalizados de JavaScript en formRuntime.jsp.

## config.jsp {#config-jsp}

El módulo config.jsp contiene varias configuraciones, como el registro, los servicios proxy y la versión de comportamiento. Puede agregar su propia configuración y personalización de utilidades al módulo config.jsp. También puede agregar configuraciones como el registro de utilidades personalizado al módulo config.jsp.

## toolbar.jsp {#toolbar-jsp}

El archivo toolbar.jsp contiene código para crear una barra de herramientas de color. Para quitar la barra de herramientas, elimine toolbar.jsp del HTML.jsp

## formBody.jsp {#formbody-jsp}

El módulo formBody.jsp es para la representación de HTML del formulario XFA.

## nav_footer.jsp {#nav-footer-jsp}

Al principio, el formulario HTML5 solo procesa la primera página del formulario. Cuando un usuario desplaza el formulario, se carga el resto de los formularios. Hace que la experiencia de carga sea más rápida. El componente nav_footer.jsp contiene todos los estilos y elementos necesarios para facilitar la carga de las páginas en el desplazamiento.

## footer.jsp {#footer-jsp}

El módulo footer.jsp está vacío. Permite añadir secuencias de comandos que solo se utilizan para la interacción del usuario.

## Creación de perfiles personalizados {#creating-custom-profiles}

Para crear un perfil personalizado, realice los pasos siguientes:

### Crear nodo de perfil {#create-profile-node}

1. Vaya a la interfaz CRX DE en la URL: `https://'[server]:[port]'/crx/de` e inicie sesión en la interfaz con credenciales de administrador.

1. En el panel izquierdo, vaya a la ubicación */content/xfaforms/profiles*.

1. Copie el nodo predeterminado y pegue el nodo en una carpeta diferente (*/content/profiles*) con nombre *hrform*.

1. Seleccione el nuevo nodo, *hrform* y agregue una propiedad de cadena: *sling:resourceType* con valor: *formulario/demostración*.

1. Haga clic en Guardar todo en el menú de la barra de herramientas para guardar los cambios.

### Creación de la secuencia de comandos del renderizador de perfil {#create-the-profile-renderer-script}

Después de crear un perfil personalizado, agregue información de renderización a este perfil. Al recibir una solicitud para el nuevo perfil, CRX verifica la existencia de la carpeta /apps para que se represente la página JSP. Cree la página JSP en la carpeta /apps .

1. En el panel izquierdo, vaya a la `/apps` carpeta.
1. Haga clic con el botón derecho en el `/apps` carpeta y elija crear una carpeta con el nombre **hrform**.
1. Insistir en el **hrform** carpeta crear una carpeta denominada **demostración**.
1. Haga clic en el **Guardar todo** botón.
1. Vaya a `/libs/xfaforms/profile/html.jsp` y copie el nodo **html.jsp**.
1. Pegar **html.jsp** en el nodo `/apps/hrform/demo` carpeta creada anteriormente con el mismo nombre **html.jsp** y haga clic en **Guardar**.
1. Si tiene cualquier otro componente del script de perfil, siga los pasos del 1 al 6 para copiar los componentes en la carpeta /apps/hrform/demo .

1. Para verificar que el perfil se ha creado, abra la dirección URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

Para verificar los formularios, [Importar formularios](/help/forms/using/get-xdp-pdf-documents-aem.md) desde el sistema de archivos local a AEM Forms y [vista previa del formulario](/help/forms/using/previewing-forms.md) en AEM instancia de autor del servidor.
