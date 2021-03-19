---
title: Integración de la IU Crear correspondencia con su portal personalizado
seo-title: Integración de la IU Crear correspondencia con su portal personalizado
description: Aprenda a integrar la interfaz de usuario de creación de correspondencia con su portal personalizado
seo-description: Aprenda a integrar la interfaz de usuario de creación de correspondencia con su portal personalizado
uuid: 68ef5bf2-b271-4c44-8840-6c495069164d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 0d3bb98e-7139-4d8e-b110-6ebd11debda1
docset: aem65
feature: Administración de correspondencia
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 4%

---


# Integración de la IU Crear correspondencia con su portal personalizado{#integrating-create-correspondence-ui-with-your-custom-portal}

## Información general {#overview}

Este artículo detalla cómo puede integrar la solución Crear correspondencia con su entorno.

## Invocación basada en URL {#url-based-invocation}

Una forma de llamar a la aplicación Crear correspondencia desde un portal personalizado es preparar la URL con los siguientes parámetros de solicitud:

* el identificador de la plantilla de carta (con el parámetro cmLetterId ).

* la dirección URL de los datos XML recuperados del origen de datos deseado (con el parámetro cmDataUrl ).

Por ejemplo, el portal personalizado prepararía la dirección URL como\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`, que podría ser el href de un vínculo en el portal.

>[!NOTE]
>
>Llamar a de este modo no es seguro, ya que los parámetros necesarios se pasan como una solicitud de GET, al exponer lo mismo (claramente visible) en la dirección URL.

>[!NOTE]
>
>Antes de llamar a la aplicación Crear correspondencia, guarde y cargue los datos para llamar a la IU Crear correspondencia en la URL de datos determinada. Esto se puede hacer desde el propio portal personalizado o a través de otro proceso de back-end.

## Invocación basada en datos en línea {#inline-data-based-invocation}

Otra forma (y más segura) de llamar a la aplicación Crear correspondencia podría ser simplemente visitar la URL en https://&#39;[server]:[port]&#39;/[contextPath]/aem/forms/createcorrespondence.html, enviando los parámetros y datos para llamar a la aplicación Crear Correspondencia como una solicitud de POST (ocultándolos al usuario final). Esto también significa que ahora puede pasar los datos XML para la aplicación Crear correspondencia en línea (como parte de la misma solicitud, utilizando el parámetro cmData), que no era posible/ideal en el método anterior.

### Parámetros para especificar la letra {#parameters-for-specifying-letter}

| **Nombre** | **Tipo** | **Descripción** |
|---|---|---|
| cmLetterInstanceId | Cadena | Identificador de la instancia de letra. |
| cmLetterId | Cadena | El nombre de la plantilla Carta. |

El orden de los parámetros de la tabla especifica la preferencia de los parámetros utilizados para cargar la carta.

### Parámetros para especificar el origen de datos XML {#parameters-for-specifying-the-xml-data-source}

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td> 
   <td><strong>Tipo</strong></td> 
   <td><strong>Descripción</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>Datos XML de un archivo de origen usando protocolos básicos como cq, ftp, http o file.<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>Cadena</td> 
   <td>Uso de datos xml disponibles en la instancia de carta.</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>Booleano</td> 
   <td>Para reutilizar los datos de prueba adjuntos en un diccionario de datos.</td> 
  </tr>
 </tbody>
</table>

El orden de los parámetros de la tabla especifica la preferencia de los parámetros utilizados para cargar los datos XML.

### Otros parámetros {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td> 
   <td><strong>Tipo</strong></td> 
   <td><strong>Descripción</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>Booleano</td> 
   <td>True para abrir la carta en el modo de vista previa<br /> </td> 
  </tr>
  <tr>
   <td>Aleatorio</td> 
   <td>Marca de tiempo</td> 
   <td>Para resolver los problemas de almacenamiento en caché del explorador.</td> 
  </tr>
 </tbody>
</table>

Si utiliza el protocolo http o cq para cmDataURL, la dirección URL de http/cq debe ser accesible de forma anónima.
