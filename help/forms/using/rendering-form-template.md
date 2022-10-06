---
title: Representación de la plantilla de formulario para formularios HTML5
seo-title: Rendering form template for HTML5 forms
description: Los perfiles de formulario de HTML5 están asociados a renderizaciones de perfiles. Las renderizaciones de perfil son páginas JSP responsables de generar la representación de HTML del formulario llamando al servicio OSGi de Forms.
seo-description: HTML5 forms profiles are associated with profile renders. Profile Renders are JSP pages responsible for generating HTML representation of the form by calling the Forms OSGi service.
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: Mobile Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# Representación de la plantilla de formulario para formularios HTML5 {#rendering-form-template-for-html-forms}

## Punto final de procesamiento {#render-endpoint}

Los formularios del HTML 5 tienen la noción de **Perfiles** que se exponen como extremos REST para permitir el procesamiento móvil de plantillas de formulario. Estos perfiles están asociados **Procesador de perfiles**. Son páginas JSP responsables de generar la representación del HTML del formulario llamando al servicio Forms OSGi. La ruta JCR del nodo Perfil determina la dirección URL del punto final de procesamiento. El punto final de procesamiento predeterminado del formulario que señala al perfil &quot;predeterminado&quot; tiene este aspecto:

https://&lt;*host*>:&lt;*puerto*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*ruta de la carpeta que contiene el formulario xdp*>&amp;template=&lt;*nombre del xdp*>

Por ejemplo, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`. 

Para un perfil personalizado, el punto final cambia en consecuencia. Por ejemplo, el punto final del perfil personalizado con el nombre formularios es:

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Si la plantilla reside en el repositorio AEM en una aplicación llamada FormSubmission, el URI es:

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## Parámetros de procesamiento {#render-parameters}

Los parámetros de solicitud admitidos al procesar el formulario como HTML son:

<table>
 <tbody>
  <tr>
   <th><strong>Parámetro </strong></th>
   <th><strong>Descripción</strong></th>
  </tr>
  <tr>
   <td>template<br /> </td>
   <td>Este parámetro especifica el nombre del archivo de plantilla.<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>Este parámetro especifica la ruta donde residen la plantilla y los recursos asociados. Esta ruta puede ser la ruta del sistema de archivos del servidor o una ruta del repositorio, http o una ruta ftp.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>Este parámetro especifica la dirección URL a la que se publica el xml de datos del formulario.<br /> </td>
  </tr>
 </tbody>
</table>

### Combinar datos con la plantilla de formulario {#merge-data-with-form-template}

| Parámetro | Descripción |
|---|---|
| dataRef | Este parámetro especifica **ruta absoluta** del archivo de datos que se combina con la plantilla. Este parámetro puede ser una URL a un servicio de descanso que devuelva los datos en formato xml. |
| data | Este parámetro especifica los bytes de datos codificados UTF-8 que se combinan con la plantilla. Si se especifica este parámetro, el formulario HTML5 ignora el parámetro dataRef. |

### Pasar el parámetro de renderización {#passing-the-render-parameter}

Los formularios de HTML5 admiten tres métodos para pasar los parámetros de procesamiento. Puede pasar parámetros a través de direcciones URL, pares clave-valor y nodo de perfil. En el parámetro de renderización, el par clave-valor tiene la prioridad más alta seguida del nodo de perfil. El parámetro de solicitud de URL tiene la menor prioridad.

* **Parámetros de solicitud de URL**: Puede especificar los parámetros de renderización en la URL. En los parámetros de solicitud de URL, los parámetros son visibles para el usuario final. Por ejemplo, la siguiente URL de envío contiene un parámetro de plantilla en la URL: `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **Parámetros de solicitud de SetAttribute**: Puede especificar los parámetros de renderización como un par clave-valor. En los parámetros de solicitud de SetAttribute, el usuario final no puede ver los parámetros. Puede reenviar una solicitud desde cualquier otro JSP al JSP del procesador de perfiles de formulario de HTML 5 y usar *setAttribute* en el objeto request para pasar todos los parámetros de renderización. Este método tiene la prioridad más alta.

* **Parámetros de solicitud de nodo de perfil:** Puede especificar los parámetros de renderización como propiedades de nodo de un nodo de perfil. En los parámetros de solicitud del nodo de perfil, el usuario final no puede ver los parámetros. El nodo de perfil es el nodo al que se envía la solicitud. Para especificar parámetros como propiedades de nodo, utilice CRXDE lite.

### Parámetros de envío {#submit-parameters}

los formularios HTML5 envían datos; ejecutar scripts del lado del servidor y servicios web en servidores AEM. Para obtener información detallada sobre los parámetros utilizados para ejecutar secuencias de comandos del lado del servidor y servicios web en servidores AEM, consulte [HTML5 forms Service Proxy](/help/forms/using/service-proxy.md).
