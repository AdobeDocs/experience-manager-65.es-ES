---
title: Información general sobre comunicaciones interactivas
seo-title: Información general sobre comunicaciones interactivas
description: Este artículo incluye información general, casos de uso de muestra, flujo de trabajo de creación y diferencias entre la comunicación interactiva y la carta.
seo-description: Funciones clave de comunicación interactiva, casos de uso de muestra, flujo de trabajo de creación y diferencias entre la comunicación interactiva y la administración de correspondencia
uuid: a06b4ac7-ca20-4d6d-b2b7-87b21e2f5cf9
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 67b03098-c58d-4a57-90e0-e4ddd78e5d99
translation-type: tm+mt
source-git-commit: dc7804c9985bf9a14bfad40f546e393b39615dab

---


# Información general sobre comunicaciones interactivas {#interactive-communications-overview}

Este artículo incluye información general, casos de uso de muestra, flujo de trabajo de creación y diferencias entre la comunicación interactiva y la carta.

![](do-not-localize/correspondence-management.png)

Interactive Communications centraliza y gestiona la creación, el ensamblaje y la entrega de correspondencia segura, personalizada e interactiva, como correspondencia comercial, documentos, declaraciones, avisos de beneficios, correos electrónicos de marketing, facturas y kits de bienvenida.

## Funciones clave {#key-capabilities}

A continuación se describen las funciones clave de Interactive Communications:

* Integración lista para usar con el modelo de datos de formulario para permitir un acceso fácil y simplificado a las bases de datos back-end y otros sistemas CRM, como MS® Dynamics
* Interfaz de creación integrada para canales web e impresos con capacidad para generar automáticamente canales web a partir del canal de impresión
* Gráficos para presentar información en formatos visuales fáciles de entender en impresión y Web
* Los fragmentos de documento admiten el editor de reglas y el modelo de datos de formulario
* La interfaz de usuario del agente muestra la impresión y la vista previa web de la comunicación interactiva
* Arrastrar y soltar componentes para construir rápidamente canales de impresión y web

## Ejemplo de caso de uso {#sample-use-case}

El kit de [bienvenida para un caso de uso de cliente](/help/forms/using/finance-reference-site-walkthrough.md#credit-card-application-walkthrough) de tarjeta de crédito muestra las capacidades de una comunicación interactiva.

## Interactive Communication creation  {#interactive-communication-creation}

![interactive_Communication-01](assets/interactive_communication-01.jpg)

### Flujo de trabajo {#workflow}

Para crear una comunicación interactiva, tenga los [componentes](#buildingblocks) básicos de la comunicación interactiva listos y complete los siguientes pasos:

1. Elija [crear una comunicación](/help/forms/using/create-interactive-communication.md)interactiva.

1. Especifique el modelo [de datos de](/help/forms/using/data-integration.md)formulario, el servicio de cumplimentación previa y las plantillas [de canal web e](/help/forms/using/web-channel-print-channel.md)impresión. Puede elegir generar un canal web a partir del canal de impresión.

1. Mediante la interfaz [de](/help/forms/using/introduction-interactive-communication-authoring.md)arrastrar y soltar, agregue fragmentos de documento, imágenes, componentes a la impresión y al canal web de la comunicación interactiva según sea necesario.
1. Configure las propiedades de los componentes insertados, como por ejemplo:

   1. [Imágenes](/help/forms/using/create-interactive-communication.md#step2)
   1. [Tablas](/help/forms/using/create-interactive-communication.md#tables) (incluidos los fragmentos de diseño)
   1. [Gráficos](/help/forms/using/chart-component-interactive-communications.md)
   1. [Fragmentos de documento](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. Obtenga una vista previa de los canales web y de impresión y, si es necesario, edite la comunicación interactiva.
1. El agente utiliza la interfaz de usuario del agente para [preparar la comunicación](/help/forms/using/prepare-send-interactive-communication.md) interactiva para enviarla al proceso de destinatario o anuncio.

### Componentes {#buildingblocks}

A continuación se indican los componentes necesarios para crear una comunicación interactiva:

* [Modelo de datos de formulario](/help/forms/using/data-integration.md)
* [Plantillas de canal web e impresión](/help/forms/using/web-channel-print-channel.md)
* [Fragmentos de documento](/help/forms/using/document-fragments.md)
* Imágenes
* [Temas](/help/forms/using/themes.md) para el canal Web

## Comunicaciones Interactivas Frente A Administración De Correspondencia {#interactive-communications-vs-correspondence-management}

Interactive Communication es el método predeterminado y recomendado para crear comunicaciones con los clientes. Para seguir utilizando las letras creadas en AEM 6.3 Forms y AEM 6.2 Forms, debe [instalar un paquete](/help/forms/using/compatibility-package.md)de compatibilidad. A continuación se muestra una comparación entre las capacidades de la comunicación interactiva y la carta.

<table>
 <tbody>
  <tr>
   <td><strong>Capacidad</strong></td>
   <td><strong>Comunicación interactiva</strong></td>
   <td><strong>Carta</strong></td>
  </tr>
  <tr>
   <td>Salida</td>
   <td>Imprimir y Web</td>
   <td>Imprimir</td>
  </tr>
  <tr>
   <td>Esquema</td>
   <td>Modelo de datos de formulario </td>
   <td>Diccionario de datos </td>
  </tr>
  <tr>
   <td>Localización</td>
   <td>No se admite en el modelo de datos de formulario</td>
   <td>Compatible con el diccionario de datos</td>
  </tr>
  <tr>
   <td>Editor de reglas</td>
   <td>
    <ul>
     <li>Editor de reglas de compatibilidad de texto y condición para crear condiciones en línea</li>
     <li>El editor de comunicaciones interactivas admite la aplicación de reglas en componentes del canal web</li>
    </ul> </td>
   <td>No hay IU para la creación de expresiones condicionales</td>
  </tr>
  <tr>
   <td>Creación</td>
   <td>Interfaz de arrastrar y soltar para construir canales web e impresos</td>
   <td>Sin mecanismo de arrastrar y soltar </td>
  </tr>
  <tr>
   <td>Gráficos</td>
   <td>Gráficos admitidos tanto en impresión como en canal web</td>
   <td>No se admite</td>
  </tr>
  <tr>
   <td>Temas</td>
   <td>Utiliza temas para aplicar estilo al canal web</td>
   <td>No admite temas</td>
  </tr>
  <tr>
   <td>Auditoría y control de versiones</td>
   <td>No se admite</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Borra y gestiona instancias</td>
   <td>No se admite</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Procesamiento por lotes</td>
   <td>Admitido </td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Firma del agente</td>
   <td>No se admite</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Funciones remotas</td>
   <td>No se admite</td>
   <td>Admitido</td>
  </tr>
 </tbody>
</table>

