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
source-git-commit: a326e508a781b3afaba8b5e371aa862a30536740

---


# Propiedades de configuración de Interactive Communications{#interactive-communications-configuration-properties}

Interactive Communications incluye propiedades que se configuran automáticamente después de instalar el paquete [AEM Forms Add-on](../../forms/using/installing-configuring-aem-forms-osgi.md) . Los autores de comunicación interactiva pueden editar estas propiedades de configuración predeterminadas mediante la página Configuración **de la consola web de** Adobe Experience Manager.

Abra la página Configuración **de la consola web de** Adobe Experience Manager con la siguiente URL:

`https://&lt;server&gt;:&lt;port&gt;/&lt;contextPath&gt;/system/console/configMgr`

Las propiedades de configuración incluyen:

* [Configuración de fragmentos de documento](#document-fragments-configuration)
* [Crear configuración de correspondencia](#create-correspondence-configuration)
* [Configuración del canal web de comunicación interactiva y formulario adaptable](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [Configuración del tema del canal web de comunicación interactiva y formulario adaptable](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## Configuración de fragmentos de documento {#document-fragments-configuration}

Toque Configuración **de fragmentos de** documento en la página Configuración **de la consola web de** Adobe Experience Manager para ver las propiedades de configuración de los fragmentos de documento.

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
   <td><p>--</p> </td> 
  </tr> 
  <tr> 
   <td>Sangría</td> 
   <td>Ancho de una sola unidad de sangría aplicada al texto de la lista de fragmentos de documentos.</td> 
   <td>12.7mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Anchura mínima de números romanos</td> 
   <td>Anchura mínima que se aplicará al campo de viñeta o número cuando se utilicen números romanos en la lista de fragmentos de documento. </td> 
   <td>12.7mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Ancho mínimo del número</td> 
   <td>Anchura mínima que se aplicará al campo de viñeta o número, al utilizar listas numeradas separadas de números romanos en la lista de fragmentos de documento.</td> 
   <td>8.0mm</td> 
   <td>Número</td> 
  </tr> 
 </tbody> 
</table>

## Crear configuración de correspondencia {#create-correspondence-configuration}

Toque **Crear configuración** de correspondencia en la página Configuración **de la consola web de** Adobe Experience Manager para ver las propiedades de configuración de la interfaz de usuario del agente.

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
   <td>Habilitar incrustación de fuentes en PDF</td> 
   <td><p>Seleccione la casilla de verificación para activar la incrustación de fuentes en los documentos PDF. Después de seleccionar esta opción, puede incrustar nuevas fuentes después de generar o previsualizar los documentos PDF mediante la interfaz de usuario del agente. Utilice el canal Imprimir de comunicación interactiva para generar y previsualizar documentos PDF.</p> <p>La incrustación de fuentes en un documento PDF resulta útil si hay una fuente disponible en un equipo que se utiliza para generar el PDF y no está disponible en el equipo cliente que accede al PDF.</p> <p>Para obtener más información sobre la incrustación de fuentes, consulte <a href="../../forms/using/customize-text-editor.md" target="_blank">Personalizar editor</a>de texto.</p> </td> 
   <td>No seleccionado</td> 
   <td>No aplicable</td> 
  </tr> 
 </tbody> 
</table>

## Configuración del canal web de comunicación interactiva y formulario adaptable {#adaptive-form-and-interactive-communication-web-channel-configuration}

Toque Configuración **de canal web de comunicación interactiva y formulario** adaptable en la página de configuración **de la consola web de** Adobe Experience Manager para ver las propiedades de configuración del canal web de comunicaciones interactivas y formularios adaptables. En la tabla siguiente se describen las propiedades relacionadas con Interactive Communications:

| Propiedad | Descripción | Predeterminado | Valores aceptables |
|---|---|---|---|
| Mostrar marcador de posición | Seleccione la casilla de verificación para habilitar la visualización de marcadores de posición para los campos incluidos en formularios adaptables y comunicaciones interactivas. | Seleccionado | No aplicable |
| Número máximo de entradas de caché | Establezca el número máximo de formularios adaptables y comunicaciones interactivas que se pueden recuperar con la memoria caché. | 100 | Número |
| Convertir el nombre de archivo en único | Seleccione la casilla de verificación para incluir nombres únicos para los archivos como archivos adjuntos en formularios adaptables y comunicaciones interactivas. | No seleccionado | No aplicable |

## Configuración del tema del canal web de comunicación interactiva y formulario adaptable {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

Toque Configuración **del tema del canal web de comunicación interactiva y formulario** adaptable en la página de configuración **de la consola web de** Adobe Experience Manager para ver las propiedades de configuración de los temas del canal web de comunicaciones interactivas y formularios adaptables.

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
   <td>Lista de fuentes disponibles para usar al crear formularios adaptables y comunicaciones interactivas.</td> 
   <td><p>Georgia</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>Impacto</p> <p>Palatino Linotype</p> </td> 
   <td>Todas las fuentes válidas del servidor de Adobe</td> 
  </tr> 
 </tbody> 
</table>

