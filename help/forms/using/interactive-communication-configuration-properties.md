---
title: Propiedades de configuración de Interactive Communications
seo-title: Propiedades de configuración de Interactive Communication
description: Editar propiedades de configuración predeterminadas para Interactive Communications
seo-description: Editar propiedades de configuración predeterminadas para Interactive Communications
uuid: 4030078f-64a3-40bb-9892-49e22a8da561
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: acb61d37-cd22-422e-bbf3-a2979b13ad41
docset: aem65
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 7%

---


# Propiedades de configuración de Interactive Communications{#interactive-communications-configuration-properties}

Interactive Communications incluye propiedades que se configuran automáticamente después de instalar el paquete [AEM Forms Add-on](../../forms/using/installing-configuring-aem-forms-osgi.md). Los autores de la comunicación interactiva pueden editar estas propiedades de configuración predeterminadas mediante la página **Configuración de la consola web de Adobe Experience Manager**.

Abra la página **Configuración de la consola web de Adobe Experience Manager** con la siguiente dirección URL:

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

Las propiedades de configuración incluyen:

* [Configuración de fragmentos de documento](#document-fragments-configuration)
* [Crear configuración de correspondencia](#create-correspondence-configuration)
* [Configuración del Canal web de comunicación interactiva y formulario adaptable](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [Configuración del tema del Canal web de comunicación interactiva y formulario adaptable](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## Configuración de fragmentos de documento {#document-fragments-configuration}

Toque **Configuración de fragmentos de Documento** en la página **Configuración de la consola web de Adobe Experience Manager** para vista de las propiedades de configuración de los fragmentos de documento.

<table>
 <tbody> 
  <tr> 
   <td>Propiedad</td> 
   <td>Descripción</td> 
   <td>Predeterminado</td> 
   <td>Valores aceptables</td> 
  </tr> 
  <tr> 
   <td>Formatos de visualización de datos</td> 
   <td>Formato de visualización específico de la configuración regional para campos, variables y elementos del modelo de datos de formulario disponibles al crear una comunicación interactiva para canales Web e impresos.</td> 
   <td> 
    <ul> 
     <li>locale = en_US, de_DE, fr_FR y ja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>Sangría</td> 
   <td>Ancho de una sola unidad de sangría aplicada al texto en fragmentos de documento de lista.</td> 
   <td>12,7 mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Anchura mínima de números romanos</td> 
   <td>Anchura mínima que se aplicará al campo de viñeta o número cuando se utilicen números romanos en fragmentos de documento de lista. </td> 
   <td>12,7 mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Ancho mínimo del número</td> 
   <td>Anchura mínima que se aplicará al campo de viñeta o número cuando se utilicen listas numeradas distintas de números romanos en fragmentos de documento de lista.</td> 
   <td>8,0 mm</td> 
   <td>Número</td> 
  </tr> 
 </tbody> 
</table>

## Crear configuración de correspondencia {#create-correspondence-configuration}

Toque **Crear configuración de correspondencia** en la página **Configuración de la consola web de Adobe Experience Manager** para vista de las propiedades de configuración de la interfaz de usuario del agente.

<table>
 <tbody> 
  <tr> 
   <td>Propiedad</td> 
   <td>Descripción</td> 
   <td>Predeterminado</td> 
   <td>Valores aceptables</td> 
  </tr> 
  <tr> 
   <td>Mostrar contenido resuelto para editarlo</td> 
   <td>Seleccione la casilla de verificación para mostrar el contenido resuelto (valores reales en lugar de marcadores de posición) mientras edita el módulo de texto en la interfaz de usuario del agente.</td> 
   <td>No seleccionado</td> 
   <td>No aplicable</td> 
  </tr> 
  <tr> 
   <td>Aplicar marca de agua durante la previsualización</td> 
   <td>Seleccione la casilla de verificación para aplicar una marca de agua al canal de impresión de comunicación interactiva en modo de Previsualización.</td> 
   <td>No seleccionado</td> 
   <td>No aplicable</td> 
  </tr> 
  <tr> 
   <td>Habilitar incrustación de fuentes en PDF</td> 
   <td><p>Seleccione la casilla de verificación para activar la incrustación de fuentes en los documentos PDF. Después de seleccionar esta opción, puede incrustar nuevas fuentes después de generar o previsualizar los documentos PDF mediante la interfaz de usuario del agente. Utilice el canal de impresión de la comunicación interactiva para generar y previsualización de documentos PDF.</p> <p>La incrustación de fuentes en un documento PDF resulta útil si hay una fuente disponible en un equipo que se utiliza para generar el PDF y no está disponible en el equipo cliente que accede al PDF.</p> <p>Para obtener más información sobre la incrustación de fuentes, consulte <a href="../../forms/using/customize-text-editor.md" target="_blank">Personalizar editor de texto</a>.</p> </td> 
   <td>No seleccionado</td> 
   <td>No aplicable</td> 
  </tr> 
 </tbody> 
</table>

## Configuración del Canal Web de comunicación interactiva y formulario adaptable {#adaptive-form-and-interactive-communication-web-channel-configuration}

Toque **Configuración del Canal Web de comunicación interactiva y formulario adaptable** en la página **Configuración de la consola Web de Adobe Experience Manager** para vista de las propiedades de configuración del canal Web de Forms adaptable y Comunicaciones interactivas. En la tabla siguiente se describen las propiedades relacionadas con Interactive Communications:

| Propiedad | Descripción | Predeterminado | Valores aceptables |
|---|---|---|---|
| Mostrar marcador de posición | Seleccione la casilla de verificación para habilitar la visualización de marcadores de posición para los campos incluidos en formularios adaptables y comunicaciones interactivas. | Seleccionado | No aplicable |
| Número máximo de entradas de caché | Establezca el número máximo de formularios adaptables y comunicaciones interactivas que se pueden recuperar con la memoria caché. | 100 | Número |
| Convertir el nombre de archivo en único | Seleccione la casilla de verificación para incluir nombres únicos para los archivos como archivos adjuntos en Adaptive Forms e Interactive Communications. | No seleccionado | No aplicable |

## Configuración del tema del Canal Web de comunicación interactiva y formulario adaptable {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

Toque **Configuración del tema del Canal Web de comunicación interactiva y formulario adaptable** en la página **Configuración de la consola Web de Adobe Experience Manager** para vista de las propiedades de configuración de las temáticas de canal Web de Forms adaptable y comunicaciones interactivas.

<table>
 <tbody> 
  <tr> 
   <td>Propiedad</td> 
   <td>Descripción</td> 
   <td>Predeterminado</td> 
   <td>Valores aceptables</td> 
  </tr> 
  <tr> 
   <td>Nombre de Lista de fuente</td> 
   <td>Lista de las fuentes disponibles para usar al crear Forms adaptable y Comunicaciones interactivas.</td> 
   <td><p>Georgia</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>Impacto</p> <p>Palatino Linotype</p> </td> 
   <td>Todas las fuentes válidas del servidor Adobe</td> 
  </tr> 
 </tbody> 
</table>

