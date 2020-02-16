---
title: Representación de plantillas de formulario para formularios HTML5
seo-title: Representación de plantillas de formulario para formularios HTML5
description: Los perfiles de formularios HTML5 están asociados a representaciones de perfiles. Los procesamientos de perfiles son páginas JSP responsables de generar una representación HTML del formulario llamando al servicio OSGi de Forms.
seo-description: Los perfiles de formularios HTML5 están asociados a representaciones de perfiles. Los procesamientos de perfiles son páginas JSP responsables de generar una representación HTML del formulario llamando al servicio OSGi de Forms.
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Representación de plantillas de formulario para formularios HTML5 {#rendering-form-template-for-html-forms}

## Extremo de procesamiento {#render-endpoint}

Los formularios HTML5 tienen la noción de **perfiles** que se exponen como extremos REST para habilitar el procesamiento móvil de plantillas de formulario. Estos perfiles tienen asociado el procesador **de perfiles**. Son páginas JSP responsables de generar la representación HTML del formulario llamando al servicio OSGi de Forms. La ruta JCR del nodo Profile determina la dirección URL del punto final de procesamiento. El punto final de procesamiento predeterminado del formulario que apunta al perfil &#39;predeterminado&#39; tiene este aspecto:

https://&lt;*host*>:&lt;*puerto*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*ruta de la carpeta que contiene el formulario xdp*>&amp;template=&lt;*nombre del xdp*>

Por ejemplo, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Para un perfil personalizado, el punto final cambia en consecuencia. Por ejemplo, el punto final del perfil personalizado con el nombre formularios es:

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Si la plantilla reside en el repositorio de AEM en una aplicación llamada FormSubmission, el URI es:

```
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
   <td>Este parámetro especifica la ruta donde residen la plantilla y los recursos asociados. Esta ruta puede ser la ruta del sistema de archivos del servidor o una ruta del repositorio o http o una ruta ftp.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>Este parámetro especifica la dirección URL en la que se anuncia el xml de datos del formulario.<br /> </td>
  </tr>
 </tbody>
</table>

### Combinar datos con plantilla de formulario {#merge-data-with-form-template}

| Parámetro | Descripción |
|---|---|
| dataRef | Este parámetro especifica la ruta **** absoluta del archivo de datos que se combina con la plantilla. Este parámetro puede ser una URL a un servicio de descanso que devuelve los datos en formato xml. |
| data | Este parámetro especifica los bytes de datos codificados UTF-8 que se combinan con la plantilla. Si se especifica este parámetro, el formulario HTML5 omite el parámetro dataRef. |

### Paso del parámetro de procesamiento {#passing-the-render-parameter}

Los formularios HTML5 admiten tres métodos para pasar los parámetros de procesamiento. Puede pasar parámetros a través de direcciones URL, pares clave-valor y nodo de perfil. En el parámetro de procesamiento, el par clave-valor tiene la prioridad más alta seguida de un nodo de perfil. El parámetro Solicitud de URL tiene la menor prioridad.

* **Parámetros** de solicitud de URL: Puede especificar los parámetros de procesamiento en la URL. En los parámetros de solicitud de URL, los parámetros son visibles para el usuario final. Por ejemplo, la siguiente dirección URL de envío contiene el parámetro de plantilla en la dirección URL: `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **Parámetros** de solicitud de SetAttribute: Puede especificar los parámetros de procesamiento como un par clave-valor. En los parámetros de solicitud SetAttribute, el usuario final no puede ver los parámetros. Puede reenviar una solicitud desde cualquier otro JSP al JSP del procesador de perfiles de formulario HTML5 y utilizar *setAttribute* en el objeto de solicitud para pasar todos los parámetros de procesamiento. Este método tiene prioridad máxima.

* **** Parámetros de solicitud de nodo de perfil: Puede especificar los parámetros de procesamiento como propiedades de nodo de un nodo de perfil. En los parámetros de solicitud de nodo de perfil, el usuario final no puede ver los parámetros. El nodo de perfil es el nodo al que se envía la solicitud. Para especificar parámetros como propiedades de nodo, utilice la lista CRXDE.

### Parámetros de envío {#submit-parameters}

los formularios HTML5 envían datos; ejecutar scripts de servidor y servicios web en servidores AEM. Para obtener información detallada sobre los parámetros utilizados para ejecutar secuencias de comandos de servidor y servicios Web en servidores AEM, consulte Proxy [de servicio de formularios](/help/forms/using/service-proxy.md)HTML5.

**[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)**
