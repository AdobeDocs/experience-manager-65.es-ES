---
title: Resumen de las nuevas funciones | AEM 6.5 Forms
seo-title: New features summary | AEM 6.5 Forms
description: Últimas funciones y mejoras en formularios y documentos de la solución de administración de experiencias digitales más avanzada del mundo.
seo-description: Latest features and improvements to forms and documents of world’s most advanced digital experience management solution.
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 7%

---

# Resumen de las nuevas funciones | AEM 6.5 Forms{#new-features-summary-aem-forms}

## Informes de transacciones {#transaction-reports}

Los informes de transacciones permiten capturar y rastrear el número de formularios enviados, documentos procesados y documentos procesados. El objetivo detrás del seguimiento de estas transacciones es tomar una decisión informada sobre el uso del producto y reequilibrar las inversiones en hardware y software. Algunos ejemplos de transacciones son:

* Envío de un formulario adaptable, un formulario HTML5 o un conjunto de formularios
* Representación de una impresión o una versión web de una comunicación interactiva
* Conversión de un documento de un formato de archivo a otro

Para obtener información sobre cómo configurar y usar informes de transacciones, consulte [Información general sobre los informes de transacciones](../../forms/using/transaction-reports-overview.md).

![Un informe de transacción de ejemplo](assets/surface_transaction_reporting.png)

## Comunicaciones interactivas {#interactive-communications}

**Definir patrones de visualización de datos**

Los autores de comunicación interactiva ahora pueden definir [patrones de visualización de datos](create-interactive-communication.md#datadisplaypatterns) para campos, variables y elementos del modelo de datos de formulario. Por ejemplo, formatos de fecha, moneda o teléfono.

**Usar nuevos tipos de gráficos**

Ahora puede agregar [Gráficos cuadráticos y gráficos con varias series](../../forms/using/chart-component-interactive-communications.md) a Comunicaciones interactivas.

**Ordenar columnas en una tabla**

Ahora puede [ordenar columnas de una tabla](../../forms/using/create-interactive-communication.md#sortcolumns) en la Comunicación interactiva. Puede enlazar y ordenar columnas de tabla con texto estático u objetos del modelo de datos.

**Uso de componentes nuevos en un canal web**

Ahora puede añadir componentes Botón y Separador al canal web. Para obtener más información, consulte [Añadir el componente Botón al canal web](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) y [Componente separador en el canal web](../../forms/using/create-interactive-communication.md#separatorcomponent).

**Modo de diseño para cambiar el tamaño de los componentes**

Ahora puede cambiar a [Modo de diseño](../../forms/using/resize-using-layout-mode.md) para cambiar el tamaño de los componentes del canal web mediante una interfaz WYSIWYG.

**Mejoras de uso**

Los autores de comunicación interactiva ahora pueden utilizar varias operaciones fáciles de usar al crear correspondencias. La lista de operaciones incluye:

* [Realizar acciones de deshacer y rehacer en canales web e impresos](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Adición de variables en un fragmento de documento utilizando el símbolo @](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Adición de elementos del modelo de datos en un fragmento de documento utilizando un símbolo @](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Eliminar o agregar un canal web a una comunicación interactiva existente](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Enlazar elementos de fuentes de datos con campos y variables mediante acciones de arrastrar y soltar](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Resaltar campos y variables no enlazados al crear una comunicación interactiva](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Realizar acciones adicionales, como copiar, agrupar o más, en componentes heredados en un canal web](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Mejoras en el proceso de sincronización**

Hay varias mejoras en el diseño del canal web autogenerado mediante el canal de impresión.

![Gráficos de comunicaciones interactivos](assets/interactive-communication-charts.png)

## Formularios adaptables {#adaptive-forms}

### Uso de firmas digitales basadas en la nube de Adobe Sign en Adaptive Forms {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Firmas digitales basadas en la nube](https://helpx.adobe.com/es/sign/kb/digital-certificate-providers.html) o las firmas remotas son una nueva generación de firmas digitales que funcionan en equipos de escritorio, dispositivos móviles y la web, y que cumplen con los niveles más altos de cumplimiento y seguridad para la autenticación de firmantes. Ahora puede [firmar un formulario adaptable](../../forms/using/working-with-adobe-sign.md) con firmas digitales basadas en la nube.

#### Incrustar un formulario adaptable o una comunicación interactiva en aplicaciones de una sola página de AEM Sites {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms le permite [incrustar sin problemas un formulario adaptable](../../forms/using/embed-adaptive-form-aem-sites-spa.md) o Comunicación interactiva en una aplicación de una sola página de AEM Sites (SPA). El formulario adaptable integrado y la comunicación interactiva son totalmente funcionales y los usuarios pueden rellenar y enviar el formulario sin salir de la página. Ayuda al usuario a permanecer en el contexto de otros elementos de la página web e interactuar simultáneamente con la forma adaptativa o la comunicación interactiva.

#### Ordenar columnas de tablas de formularios adaptables {#sort-columns-of-adaptive-form-tables}

Puede [ordenar cualquier columna de una tabla de formulario adaptable](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) en orden ascendente o descendente. Puede aplicar la ordenación a columnas de tabla con texto estático, propiedades de objeto del modelo de datos o una combinación de texto estático y propiedades de objeto del modelo de datos.

#### Restringir la disponibilidad de plantillas de Forms adaptables a rutas específicas {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Los formularios adaptables han agregado compatibilidad con la propiedad cq:allowedPaths . La propiedad [restringe la disponibilidad de las plantillas de Forms adaptables a rutas específicas](creating-adaptive-form.md#adaptive-form-templates).

#### Agregar casillas de verificación al formulario adaptable de forma dinámica {#add-check-boxes-to-the-adaptive-form-dynamically}

Ahora puede definir reglas para [agregar casillas de verificación al formulario adaptable de forma dinámica](../../forms/using/rule-editor.md#setpropertyrule) en función de una función personalizada, un objeto de formulario o una propiedad de objeto.

## Flujos de trabajo de AEM {#aem-workflows}

### Uso de variables en flujos de trabajo AEM {#use-variables-in-aem-workflows}

Las variables permiten que los pasos del flujo de trabajo mantengan y pasen metadatos entre los pasos del flujo de trabajo durante la ejecución. Puede crear diferentes tipos de variables para almacenar diferentes tipos de datos. Por ejemplo, enteros, cadenas, documentos o instancias del modelo de datos de formulario. Normalmente, se utiliza una variable o una colección de variables cuando se necesita tomar una decisión en base al valor que mantiene o para almacenar información que se necesite más adelante en un proceso.

Las variables son una extensión de [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) interfaz disponible en la versión anterior. Ayuda a ahorrar tiempo en el desarrollo del código ECMAScript personalizado que se utiliza para recuperar y actualizar valores de metadatos. La interfaz MetaDataMap y el código ECMAScript se siguen utilizando para manipular los metadatos. Algunas ventajas de utilizar variables a través de MetaDataMap y ECMAScript son:

* Almacene, actualice y use de forma dinámica valores almacenados en una variable en todo el flujo de trabajo sin depender del código personalizado
* Recupere y actualice los valores directamente en un modelo de datos de formulario y en un archivo de datos (XML/JSON ) de un formulario enviado
* Almacenar documentos completos en una variable para realizar el procesamiento de documentos

El paso Ir a o Dividir y todos los pasos del flujo de trabajo de AEM Forms admiten variables. Puede utilizar la interfaz de MetaDataMap para acceder a variables en pasos de flujo de trabajo que no tengan compatibilidad nativa con variables. Para obtener más información, consulte [Variables en flujos de trabajo AEM](../../forms/using/variable-in-aem-workflows.md).

![Configuración de una variable para en un flujo de trabajo](assets/variable.png)

#### Uso de un flujo de trabajo con Forms adaptable diferente  {#use-a-workflow-with-different-adaptive-forms}

Puede [especificar un formulario adaptable para la tarea de asignación](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) y el paso del documento de registro de los flujos de trabajo centrados en el formulario en tiempo de ejecución. Permite que un flujo de trabajo funcione con diferentes Forms adaptables. Puede decidir el método para seleccionar un formulario adaptable al diseñar el flujo de trabajo. El formulario adaptable puede encontrarse en una ruta absoluta, enviarse como carga útil al flujo de trabajo o estar disponible en una ruta calculada mediante una variable.

#### Uso de las funciones de registro mejoradas de los pasos de flujo de trabajo centrados en formularios {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Las capacidades de registro de los pasos de flujo de trabajo centrados en formularios están estandarizadas. Ahora, todos los pasos de flujo de trabajo centrados en formularios producen registros estandarizados similares. Ayuda a mejorar la velocidad de depuración.

## Integración de datos de  {#data-integration}

Ahora puede:

* [Validación de datos de entrada](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) en función de una lista de restricciones. Ayuda a garantizar que solo se envíen datos válidos al origen de datos.
* [Anular extremo predeterminado](../../forms/using/configure-data-sources.md#configure-soap-web-services) definida en un archivo WSDL (lenguaje de descripción de servicios web).

* [Sobrescribir predeterminado](../../forms/using/configure-data-sources.md#configure-restful-web-services) [esquema, host y ruta base](../../forms/using/configure-data-sources.md#configure-restful-web-services) definida en el archivo de definición Swagger.

## Actualizaciones de plataforma y seguridad {#platform-and-security-updates}

### Principales actualizaciones de la plataforma {#major-platform-updates}

AEM Forms se puede configurar utilizando cualquier combinación de sistemas operativos admitidos, servidores de aplicaciones, bases de datos, controladores de base de datos, JDK, servidores LDAP y servidores de correo electrónico. A continuación se indican los cambios más importantes en [plataformas compatibles](../../forms/using/aem-forms-jee-supported-platforms.md):

<table>
 <tbody>
  <tr>
   <td>Componente</td>
   <td>Compatibilidad eliminada</td>
  </tr>
  <tr>
   <td>Sistemas operativos</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Servidores de aplicaciones<br /> </td>
   <td>
    <ul>
    <li>Perfil de libertad de WebSphere</li>
    <li>Oracle WebLogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Bases de datos</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>Oracle RAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Servidores LDAP</td>
   <td>
    <ul>
     <li>Microsoft Active Directory 2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Servidores de correo electrónico</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Conectores</td>
   <td>
    <ul>
     <li>Conector para Microsoft Sharepoint 2013</li>
     <li>Connector para Documentum 7.0 de EMC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>aplicación AEM Forms<br /> </td>
   <td>
    <ul>
     <li>Compatibilidad con Windows 8.1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Java </td>
   <td>
    <ul>
     <li>Java 11</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

&#42; Póngase en contacto con el servicio de asistencia al Adobe para obtener información sobre cómo migrar a una plataforma diferente

#### Nuevas IU basadas en HTML5 {#new-html-based-uis}

En línea con la Fin de la vida útil planificada del Flash Player de Adobe y la dirección general de la migración de contenido basado en Flash a estándares abiertos, AEM 6.5 Forms ha reemplazado la IU basada en Flash de la interfaz de usuario del Monitor de estado, Gestión de procesos, Extensión de Reader y Administración de categorías de AEM Forms en la consola de administración de JEE con la IU basada en HTML5.

#### Mejoras de seguridad {#security-improvements}

* AEM 6.5 Forms en la interfaz de usuario de la consola de administración de JEE se basa ahora en Apache Struts 2.5.
* AEM 6.5 Forms ahora utiliza jQuery a 3.2.1 y jQuery UI 1.12.1. Consulte, [documentación de actualización](/help/forms/home.md) para el impacto del cambio.

#### Mejoras de accesibilidad {#accessibility-improvements}

AEM 6.5 Forms ha mejorado la accesibilidad de AEM Forms Workspace.
