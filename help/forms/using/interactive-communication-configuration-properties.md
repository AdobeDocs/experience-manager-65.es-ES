---
title: Propiedades de configuración de Interactive Communications
seo-title: Interactive Communication configuration properties
description: Editar propiedades de configuración predeterminadas para Interactive Communications
seo-description: Edit default configuration properties for Interactive Communications
uuid: 4030078f-64a3-40bb-9892-49e22a8da561
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: acb61d37-cd22-422e-bbf3-a2979b13ad41
docset: aem65
feature: Interactive Communication
exl-id: 09eeade6-e16d-4159-b26a-803c7201097a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 7%

---

# Propiedades de configuración de Interactive Communications{#interactive-communications-configuration-properties}

Interactive Communications incluye propiedades que se configuran automáticamente después de instalar el [Complemento de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md) paquete. Los autores de Interactive Communication pueden editar estas propiedades de configuración predeterminadas mediante el **Configuración de la consola web de Adobe Experience Manager** página.

Abra el **Configuración de la consola web de Adobe Experience Manager** con la siguiente dirección URL:

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

Las propiedades de configuración incluyen:

* [Configuración de fragmentos de documento](#document-fragments-configuration)
* [Crear configuración de correspondencia](#create-correspondence-configuration)
* [Configuración del canal web de comunicaciones interactivas y formularios adaptables](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [Configuración del tema del canal web de comunicaciones interactivas y formularios adaptables](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## Configuración de fragmentos de documento {#document-fragments-configuration}

Toque **Configuración de fragmentos de documento** en el **Configuración de la consola web de Adobe Experience Manager** para ver las propiedades de configuración de los fragmentos de documento.

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
   <td>Formato de visualización específico de la configuración regional para campos, variables y elementos del modelo de datos de formulario disponibles al crear una comunicación interactiva para canales impresos y web.</td> 
   <td> 
    <ul> 
     <li>configuración regional = en_US, de_DE, fr_FR y ja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>Sangría</td> 
   <td>La anchura de una unidad de sangría aplicada al texto de la lista de fragmentos de documento.</td> 
   <td>12,7 mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Anchura mínima de los números romanos</td> 
   <td>Ancho mínimo que se aplicará al campo de viñeta o número, al utilizar números romanos en fragmentos de documento de lista. </td> 
   <td>12,7 mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Ancho mínimo de número</td> 
   <td>Ancho mínimo que se aplicará a la viñeta o al campo numérico, al utilizar listas numeradas separadas de números romanos en fragmentos de documentos de lista.</td> 
   <td>8,0 mm</td> 
   <td>Número</td> 
  </tr> 
 </tbody> 
</table>

## Crear configuración de correspondencia {#create-correspondence-configuration}

Toque **Crear configuración de correspondencia** en el **Configuración de la consola web de Adobe Experience Manager** para ver las propiedades de configuración de la interfaz de usuario del agente.

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
   <td>Aplicar marca de agua durante la vista previa</td> 
   <td>Seleccione la casilla de verificación para aplicar una marca de agua al canal de impresión de comunicación interactiva en el modo de vista previa.</td> 
   <td>No seleccionado</td> 
   <td>No aplicable</td> 
  </tr> 
  <tr> 
   <td>Habilitar incrustación de fuentes en el PDF</td> 
   <td><p>Seleccione la casilla de verificación para activar la incrustación de fuentes en los documentos del PDF. Después de seleccionar esta opción, puede incrustar nuevas fuentes después de generar o previsualizar los documentos del PDF mediante la interfaz de usuario del agente. Utilice el canal de impresión de la comunicación interactiva para generar y previsualizar documentos de PDF.</p> <p>La incrustación de fuentes en un documento de PDF resulta útil si una fuente está disponible en un equipo que se utiliza para generar el PDF y no está disponible en el equipo cliente que accede al PDF.</p> <p>Para obtener más información sobre cómo incrustar fuentes, consulte <a href="../../forms/using/customize-text-editor.md" target="_blank">Personalizar editor de texto</a>.</p> </td> 
   <td>No seleccionado</td> 
   <td>No aplicable</td> 
  </tr> 
 </tbody> 
</table>

## Configuración del canal web de comunicaciones interactivas y formularios adaptables {#adaptive-form-and-interactive-communication-web-channel-configuration}

Toque **Configuración del canal web de comunicaciones interactivas y formularios adaptables** en el **Configuración de la consola web de Adobe Experience Manager** para ver las propiedades de configuración del canal web de comunicaciones interactivas y Forms adaptable. En la tabla siguiente se describen las propiedades relacionadas con las comunicaciones interactivas:

| Propiedad | Descripción | Predeterminado | Valores aceptables |
|---|---|---|---|
| Mostrar marcador de posición | Seleccione la casilla de verificación para activar la visualización de marcadores de posición para los campos incluidos en formularios adaptables y comunicaciones interactivas. | Seleccionado | No aplicable |
| Máximo de entradas de caché | Establezca el número máximo de formularios adaptables y comunicaciones interactivas que se pueden recuperar mediante la memoria caché. | 100 | Número |
| Convertir el nombre de archivo en único | Seleccione la casilla de verificación para incluir nombres únicos para los archivos como archivos adjuntos en Adaptive Forms y Comunicaciones interactivas. | No seleccionado | No aplicable |

## Configuración del tema del canal web de comunicaciones interactivas y formularios adaptables {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

Toque **Configuración del tema del canal web de comunicaciones interactivas y formularios adaptables** en el **Configuración de la consola web de Adobe Experience Manager** para ver las propiedades de configuración de los temas del canal web Adaptive Forms e Interactive Communications.

<table>
 <tbody> 
  <tr> 
   <td>Propiedad</td> 
   <td>Descripción</td> 
   <td>Predeterminado</td> 
   <td>Valores aceptables</td> 
  </tr> 
  <tr> 
   <td>Nombre de la lista de fuentes</td> 
   <td>Lista de fuentes disponibles para usar durante la creación de Forms adaptable y comunicaciones interactivas.</td> 
   <td><p>Georgia</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>Impacto</p> <p>Palatino Linotype</p> </td> 
   <td>Todas las fuentes válidas del servidor de Adobe</td> 
  </tr> 
 </tbody> 
</table>
