---
title: Resumen de las nuevas funciones| AEM 6.5 Forms
seo-title: Resumen de las nuevas funciones| AEM 6.5 Forms
description: Las últimas funciones y mejoras en los formularios y documentos de la solución de gestión de experiencias digitales más avanzada del mundo.
seo-description: Las últimas funciones y mejoras en los formularios y documentos de la solución de gestión de experiencias digitales más avanzada del mundo.
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
translation-type: tm+mt
source-git-commit: eb6ecc224c4fdd8c1af6f7800dc30de419f5ef68

---


# Resumen de las nuevas funciones| AEM 6.5 Forms{#new-features-summary-aem-forms}

## Informes de transacciones {#transaction-reports}

Los informes de transacciones permiten capturar y rastrear el número de formularios enviados, documentos procesados y documentos procesados. El objetivo detrás del seguimiento de estas transacciones es tomar una decisión informada sobre el uso del producto y reequilibrar las inversiones en hardware y software. Algunos ejemplos de transacciones son:

* Envío de un formulario adaptable, un formulario HTML5 o un conjunto de formularios
* Representación de una impresión o una versión web de una comunicación interactiva
* Conversión de un documento de un formato de archivo a otro

Para obtener información sobre cómo configurar y utilizar los informes de transacciones, consulte Información general sobre los informes [de transacciones](../../forms/using/transaction-reports-overview.md).

![Un informe de transacción de muestra](assets/surface_transaction_reporting.png)

## Comunicaciones interactivas {#interactive-communications}

**Definir patrones de visualización de datos**

Los autores de comunicación interactiva ahora pueden definir patrones [de visualización de](../../forms/using/create-interactive-communication.md#main-pars-header-1162517146) datos para campos, variables y elementos del modelo de datos de formulario. Por ejemplo, formatos de fecha, moneda o teléfono.

**Usar nuevos tipos de gráficos**

Ahora puede agregar gráficos de [cuadrantes y gráficos con varias series](../../forms/using/chart-component-interactive-communications.md) a Comunicaciones interactivas.

**Ordenar columnas en una tabla**

Ahora puede [ordenar columnas de una tabla](../../forms/using/create-interactive-communication.md#sortcolumns) en la Comunicación interactiva. Puede enlazar y ordenar columnas de tabla con texto estático u objetos del modelo de datos.

**Uso de nuevos componentes en un canal web**

Ahora puede agregar componentes Botón y Separador al canal web. Para obtener más información, consulte [Agregar componente Botón al canal](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) web y componente [Separador en el canal](../../forms/using/create-interactive-communication.md#separatorcomponent)web.

**Modo de diseño para cambiar el tamaño de los componentes**

Ahora puede cambiar al modo [](../../forms/using/resize-using-layout-mode.md) Diseño para cambiar el tamaño de los componentes en el canal Web mediante una interfaz WYSIWYG.

**Mejoras de uso**

Los autores de comunicación interactiva ahora pueden utilizar varias operaciones fáciles de usar al crear correspondencias. La lista de operaciones incluye:

* [Realizar acciones de deshacer-rehacer en canales web e impresos](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Adición de variables en un fragmento de documento mediante el símbolo @](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Adición de elementos del modelo de datos en un fragmento de documento mediante el símbolo @](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Eliminar o agregar un canal web a una comunicación interactiva existente](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Enlazar elementos de origen de datos con campos y variables mediante acciones de arrastrar y soltar](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Resalte los campos y variables no enlazados durante la creación de Interactive Communication](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Realizar acciones adicionales como copiar, agrupar o más en componentes heredados de un canal web](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Mejoras en el proceso de sincronización**

Hay varias mejoras en el diseño de canal Web autogeneradas mediante el canal Imprimir.

![Gráficos interactivos de comunicaciones](assets/interactive-communication-charts.png)

## Formularios adaptables {#adaptive-forms}

### Uso de firmas digitales basadas en la nube de Adobe Sign en formularios adaptables {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Las firmas](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) digitales basadas en la nube o las firmas remotas son una nueva generación de firmas digitales que funcionan en equipos de escritorio, dispositivos móviles y la web: y cumplir los niveles más altos de cumplimiento y seguridad para la autenticación de firmantes. Ahora puede [firmar un formulario](../../forms/using/working-with-adobe-sign.md) adaptable con firmas digitales basadas en la nube.

#### Incrustar un formulario adaptable o una comunicación interactiva en aplicaciones de una sola página de AEM Sites {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms permite incrustar [sin problemas un formulario](../../forms/using/embed-adaptive-form-aem-sites-spa.md) adaptable o una comunicación interactiva en una aplicación de una sola página (SPA) de AEM Sites. El formulario adaptable y la comunicación interactiva incrustados son totalmente funcionales y los usuarios pueden rellenar y enviar el formulario sin salir de la página. Ayuda al usuario a permanecer en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario adaptable o la comunicación interactiva.

#### Ordenar columnas de tablas de formularios adaptables {#sort-columns-of-adaptive-form-tables}

Puede [ordenar cualquier columna de una tabla](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) de formulario adaptable en orden ascendente o descendente. Puede aplicar ordenación a columnas de tabla con texto estático, propiedades de objeto del modelo de datos o una combinación de texto estático y propiedades de objeto del modelo de datos.

#### Restringir la disponibilidad de plantillas de formularios adaptables a rutas específicas {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Los formularios adaptables han agregado compatibilidad con la propiedad cq:allowPaths. La propiedad [restringe la disponibilidad de plantillas de formularios adaptables a rutas](../../forms/using/creating-adaptive-form.md#main-pars-text)específicas.

#### Adición dinámica de casillas de verificación al formulario adaptable {#add-check-boxes-to-the-adaptive-form-dynamically}

Ahora puede definir reglas para [agregar casillas de verificación al formulario adaptable dinámicamente](../../forms/using/rule-editor.md#setpropertyrule) basadas en una función personalizada, un objeto de formulario o una propiedad de objeto.

## Flujos de trabajo de AEM {#aem-workflows}

### Uso de variables en flujos de trabajo de AEM {#use-variables-in-aem-workflows}

Las variables permiten que los pasos del flujo de trabajo retengan y pasen metadatos en todos los pasos del flujo de trabajo durante la ejecución. Puede crear diferentes tipos de variables para almacenar diferentes tipos de datos. Por ejemplo, instancias de enteros, cadenas, documentos o modelos de datos de formulario. Normalmente, se utiliza una variable o una colección de variables cuando se necesita tomar una decisión en función del valor que contiene o para almacenar la información que se necesita más adelante en un proceso.

Las variables son una extensión de la interfaz de [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) disponible en la versión anterior. Ayuda a ahorrar tiempo en el desarrollo del código personalizado de ECMAScript que se utiliza para recuperar y actualizar valores de metadatos. Para manipular los metadatos, siga utilizando la interfaz MetaDataMap y el código ECMAScript. Algunas ventajas del uso de variables mediante MetaDataMap y ECMAScript son:

* Almacene, actualice y utilice de forma dinámica los valores almacenados en una variable en todo el flujo de trabajo sin depender del código personalizado
* Recuperar y actualizar valores directamente en un modelo de datos de formulario y en un archivo de datos (XML/JSON) de un formulario enviado
* Almacenar documentos completos en una variable para realizar el procesamiento del documento

El paso Ir a, O Dividir y todos los pasos del flujo de trabajo de AEM Forms admiten variables. Puede utilizar la interfaz MetaDataMap para acceder a variables en los pasos del flujo de trabajo que no tengan una compatibilidad nativa con variables. Para obtener más información, consulte [Variables en flujos de trabajo](../../forms/using/variable-in-aem-workflows.md)de AEM.

![Configuración de una variable para en un flujo de trabajo](assets/variable.png)

#### Uso de un flujo de trabajo con distintos formularios adaptables {#use-a-workflow-with-different-adaptive-forms}

Puede [especificar un formulario adaptable para la tarea](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) de asignación y el documento del paso de registro de los flujos de trabajo centrados en el formulario en tiempo de ejecución. Permite que un flujo de trabajo funcione con distintos formularios adaptables. Puede decidir el método para seleccionar un formulario adaptable mientras diseña el flujo de trabajo. El formulario adaptable puede ubicarse en una ruta absoluta, enviarse como carga útil al flujo de trabajo o estar disponible en una ruta calculada mediante una variable.

#### Uso de funciones de registro mejoradas en los pasos del flujo de trabajo centrados en formularios {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Las capacidades de registro de los pasos de flujo de trabajo centrados en formularios están estandarizadas. Ahora, todos los pasos del flujo de trabajo centrados en el formulario producen registros normalizados similares. Ayuda a mejorar la velocidad de depuración.

## Integración de datos {#data-integration}

Ahora puede:

* [Valide los datos](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) de entrada según una lista de restricciones. Ayuda a garantizar que solo se envían datos válidos a la fuente de datos.
* [Omitir el extremo](../../forms/using/configure-data-sources.md#configure-soap-web-services) predeterminado definido en un archivo WSDL (Lenguaje de descripción de servicios Web).

* [Anule el](../../forms/using/configure-data-sources.md#configure-restful-web-services) esquema, host y ruta [base predeterminados](../../forms/using/configure-data-sources.md#configure-restful-web-services) definidos en el archivo de definición Swagger.

## Actualizaciones de plataformas y seguridad {#platform-and-security-updates}

### Principales actualizaciones de plataformas {#major-platform-updates}

Los formularios AEM se pueden configurar con cualquier combinación de sistemas operativos, servidores de aplicaciones, bases de datos, controladores de base de datos, JDK, servidores LDAP y servidores de correo electrónico admitidos. Los siguientes son los principales cambios en las plataformas [](../../forms/using/aem-forms-jee-supported-platforms.md)admitidas:

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
     <li>Oracle Weblogic</li>
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
     <li>Connector for EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms app<br /> </td>
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

* Póngase en contacto con el servicio de asistencia técnica de Adobe para obtener información sobre la migración a una plataforma diferente

#### Nuevas IU basadas en HTML5 {#new-html-based-uis}

En línea con el EOL planificado de Adobe Flash Player y la dirección general de la migración de contenido basado en Flash a estándares abiertos, AEM 6.5 Forms ha sustituido la IU basada en Flash de Health Monitor, Process Management, Reader Extension y Category Management UI de AEM Forms en la consola de administración JEE con la IU basada en HTML5.

#### Mejoras de seguridad {#security-improvements}

* AEM 6.5 Forms en la interfaz de usuario de la consola de administración JEE ahora se basa en Apache Struts 2.5.
* AEM 6.5 Forms ahora utiliza jQuery para 3.2.1 y jQuery UI 1.12.1. Consulte [Actualización de la documentación](/help/forms/home.md) para conocer el impacto del cambio.

#### Mejoras de accesibilidad {#accessibility-improvements}

AEM 6.5 Forms ha mejorado la accesibilidad de AEM Forms Workspace.
