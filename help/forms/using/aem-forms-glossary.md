---
title: Glosario de AEM Forms
description: El glosario de AEM Forms proporciona una lista completa de los términos, definiciones y conceptos clave utilizados en Adobe Experience Manager Forms (AEM Forms), que ayuda a los usuarios a comprender y trabajar con formularios adaptables y funciones relacionadas.
feature: Adaptive Forms
role: Admin, User, Developer
hidefromtoc: true
hide: true
source-git-commit: 37f471e09c13b7ab036ab1043d11dfed98da1d97
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 2%

---

# Glosario de AEM Forms

## [Formularios adaptables](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form)

Formularios dinámicos y adaptables que ajustan su diseño y presentación en función del dispositivo y la entrada del usuario, lo que mejora la experiencia del usuario en varias plataformas. Incluye lógica condicional, enlace de datos dinámico y comportamiento basado en reglas.

## [Creación de versiones de formularios adaptables](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/adaptive-forms-core-components/add-versioning-reviews-comments)

Capacidad para administrar varias versiones de un formulario en el repositorio mediante el control de versiones de nodos JCR. Garantiza pistas de auditoría y una reversión sencilla para formularios adaptables.

## [Integración de Adobe Analytics Forms](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation)

Proporciona información detallada sobre las interacciones del usuario (por ejemplo, abandonos de campo, tiempo empleado por sección) mediante Adobe Analytics, lo que permite la optimización del diseño de formulario basada en datos.

## [Paquete de complemento de AEM Forms](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi)

Una aplicación implementada en Adobe Experience Manager AEM AEM () como paquete que contiene servicios (proveedores de API) y servlets o JSP administrados por el marco de trabajo de Sling.

## [AEM Forms en JEE](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)

Una opción de implementación de AEM Forms que aprovecha los servidores Java Enterprise Edition (JEE), proporcionando escalabilidad de nivel empresarial, administración de transacciones y compatibilidad con flujos de trabajo empresariales complejos.

## [AEM Forms en OSGi](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/implementing/deploying/introduction/technical-requirements)

AEM Forms AEM AEM en el entorno OSGi es un paquete estándar de Author o Publish con AEM Forms implementado en él. Puede ejecutar AEM Forms en OSGi en un entorno de servidor único, configuración de granjas y de clústeres. La configuración de clúster solo está disponible para instancias de autor de AEM.

## [Adobe Sign en AEM Forms](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms)

Un servicio RESTful para flujos de trabajo de firma digital seguros y fluidos. Se integra con AEM Forms mediante la autenticación basada en OAuth, lo que permite colecciones de firmas automatizadas y un seguimiento en tiempo real.

## [AEM Forms Document Services 6.5](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services)

API proporcionadas por la capa web de AEM Forms para el uso remoto por clientes basados en HTTP, como los formularios SDK.Funcionalidades móviles en AEM Forms que permiten la creación, el ensamblado, la distribución y el archivado de documentos de PDF, la adición de firmas digitales y la descodificación de Forms con códigos de barras.

| **Nombre de servicio** | **Descripción** | **Vínculo de documentación** |
|------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Servicio de Forms** | Procese PDF forms mediante plantillas y XML, integre datos de formulario para importarlos o exportarlos y admita el procesamiento basado en fragmentos. | [Documentación del servicio Forms](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **Servicio de salida** | Genera documentos combinando datos con plantillas en formatos como PDF, PCL o PostScript. | [Documentación del servicio de salida](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **Servicio del ensamblador** | Combina, reorganiza, valida y aumenta los documentos de PDF y XDP. | [Documentación del servicio Assembler](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/use-document-services/assembler-service) |
| **Servicio ConvertPDF** | Convierte documentos de PDF a PostScript o formatos de imagen como PNG, JPEG o TIFF. | [Documentación del servicio ConvertPDF](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/use-document-services/using-convertpdf-service) |
| **Servicio de Forms con códigos de barras** | Extrae datos de códigos de barras en archivos de TIFF y PDF para automatizar los procesos de captura de datos. | [Documentación del servicio Forms con códigos de barras](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/use-document-services/using-barcoded-forms-service) |
| **Servicio DocAssurance** | Cifra, descifra, firma digitalmente y aplica directivas de seguridad de documentos a los PDF. | [Documentación del servicio DocAssurance](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services#doc-assurance-service) |
| **Servicio de PDF Generator** | Convierte formatos de archivo nativos (por ejemplo: Microsoft Word, Excel) en documentos de PDF. | [Documentación del servicio de PDF Generator](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/use-document-services/aem-document-services-programmatically#pdfgeneratorservice) |

## [API de comunicación as a Cloud Service de Forms](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction)

AEM Forms as a Cloud Service proporciona herramientas avanzadas para administrar formularios y flujos de trabajo de comunicaciones, lo que permite crear formularios digitales, capturar datos y comunicaciones personalizadas sin problemas. Las API de comunicación en la nube proporcionan generación, manipulación, validación e integración segura de documentos por lotes y bajo demanda con sistemas externos a través de HTTP, lo que garantiza operaciones optimizadas y seguras.

| **Nombre de servicio** | **Descripción** | **Vínculo de documentación** |
|-------------------------------|------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **Generación de documentos** | Combine una plantilla (XFA o PDF) con datos XML para generar documentos en los formatos de PDF e impresión, como PS, PCL, DPL, IPL y ZPL. | [Documentación de generación de documentos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=es#document-generation) |
| **Manipulación de documentos** | Combinar y reorganizar documentos de PDF. | [Documentación de manipulación de documentos](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation) |
| **Conversión de documento** | Conversión de un PDF en PDF/A y verificación del cumplimiento de PDF/A. | [Documentación de conversión de documentos](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-conversion) |
| **Documento Assurance** | Agregar o quitar campos de firma, firmar, certificar, cifrar, descifrar y aplicar derechos de uso a documentos de PDF. | [Documentación de Document Assurance](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#doc-assurance) |
| **Firmas digitales** | Integra Adobe Sign para la firma electrónica segura de formularios y documentos. | [Documentación de firmas digitales](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=es#digital-signatures) |


## [AEM Forms Workbench](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/install-workbench)

Una aplicación de escritorio para crear, editar e implementar flujos de trabajo, así como para administrar procesos empresariales centrados en formularios. Proporciona integración con servicios y sistemas back-end.

## [Tipo De Archivo](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/developing/archetype/overview)

AEM AEM Se utiliza una plantilla o un patrón para generar un nuevo proyecto con una estructura predefinida, lo que facilita la estandarización, la configuración rápida y la adherencia a las prácticas recomendadas de desarrollo de la.

## [Instancia de autor](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

Entorno donde los creadores y administradores de contenido diseñan, crean y administran el contenido antes de publicarlo. Admite versiones, previsualizaciones y pruebas.

## [Crear front-end](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Una interfaz de usuario para crear y administrar formularios en AEM Forms.

## [Bloque de formulario adaptable](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-references/form-components)

Una unidad de encapsulación que agrupa lógicamente los componentes relacionados y los metadatos, lo que permite una gestión dinámica de los datos y una escalabilidad sencilla en formularios de varios pasos.

## [Componentes principales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/introduction)

Bloques de creación reutilizables listos para usar para crear formularios, incluidos campos de formulario, contenedores de diseño, botones y otros elementos interactivos.

## [Administración de correspondencia](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/letters-correspondences/cm-overview)

Módulo que permite a las empresas crear, administrar y entregar correspondencia personalizada mediante plantillas predefinidas, reglas y fuentes de datos. Incluye plantillas de carta, comunicaciones con el cliente y generación por lotes.

## [CRX (Content repository extreme)](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/use-aem-forms-workspace/html-workspace-architecture)

AEM El repositorio de contenido Java (JCR) integrado en, que almacena datos estructurados y no estructurados, lo que permite el almacenamiento jerárquico de contenido, plantillas y configuraciones.

## [Componente personalizado](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/customize-adaptive-forms-core-components)

Componente personalizado que amplía la funcionalidad de AEM Forms, desarrollado con modelos Sling, Sightly (HTL) y Java. Normalmente se utiliza para lógica empresarial única o interactividad avanzada del lado del cliente.

## [XCI personalizado (información de configuración XML)](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/administrator-help/configure-forms/specifying-xci-configuration-options)

En Adobe Experience Manager AEM () Forms, un archivo XCI personalizado (Información de configuración XML) permite a los administradores definir propiedades de procesamiento específicas para formularios y documentos. Al configurar XCI en la consola de administración, puede anular los valores predeterminados del sistema con opciones personalizadas, lo que garantiza un procesamiento y una presentación personalizados de los formularios.

## [Integración de datos](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/form-data-model/data-integration)

Integración perfecta de fuentes de datos externas, como bases de datos, servicios web o API de REST, en formularios y flujos de trabajo para permitir experiencias de usuario dinámicas y personalizadas.

## [Fuentes de datos](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/form-data-model/configure-data-sources)

Interfaces para integrar datos externos en formularios, incluido JDBC para bases de datos relacionales, extremos REST para servicios web y OData para sistemas SAP. Administrado mediante el marco de trabajo de integración de datos de AEM Forms.

## [Fragmentos de documento](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/letters-correspondences/lists)

Componentes reutilizables de documentos, como encabezados, pies de página, exenciones de responsabilidad o cláusulas, que se pueden incluir dinámicamente en formularios o correspondencia para garantizar la coherencia.

## [Documento de registro (DoR)](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms)

Característica de AEM Forms que genera una versión de archivo no editable de un formulario enviado, normalmente en formato PDF, conservando el contenido y el diseño exactos como un registro de la transacción.

## [Edge Delivery Services](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/overview)

Entrega de contenido optimizada para AEM Forms, lo que garantiza una latencia reducida para recursos como formularios, temáticas y bibliotecas de cliente, donde los autores pueden actualizar y publicar contenido rápidamente.

## [Integración de Forms](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/form-data-model/data-integration)

Implica conectar AEM Forms a sistemas empresariales (por ejemplo, SAP, Salesforce) utilizando paquetes y conectores OSGi, admitiendo flujos de datos bidireccionales y actualizaciones en tiempo real.

## [Revisión de formulario](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms)

Una función controlada por el flujo de trabajo que permite a las partes interesadas revisar formularios adaptables, agregar anotaciones y aprobar cambios antes de publicar. AEM Utiliza la bandeja de entrada y la administración de tareas.

## [Modelo de datos de formulario (FDM)](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/using-form-data-model)

SOAP Una capa de representación que conecta formularios adaptables con fuentes de datos back-end, lo que permite la integración con servicios web RESTful, servicios de y OData. FDM permite a los autores de formularios asignar campos de formulario directamente a estructuras de datos back-end, lo que garantiza una sincronización perfecta de la entrada del usuario con sistemas externos.

## [Localización de formularios](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization)

El proceso de los formularios adaptables para admitir varios idiomas y configuraciones regionales, lo que garantiza que los formularios sean accesibles y fáciles de usar para una audiencia diversa.

## [Portal de formularios](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/use-forms-portal/creating-form-portal-page)

Los componentes del portal de Forms equipan a los desarrolladores web con componentes para crear y personalizar un portal de Forms en sitios web creados con Adobe Experience Manager AEM (). Permite a los usuarios descubrir, acceder y enviar formularios de forma eficaz en las plataformas web y móviles.

## [Front-end de envío y representación de formularios](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Interfaz de usuario final en AEM Forms que permite a los usuarios ver y enviar formularios a través de un explorador web.

## [Conjuntos de formularios](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/html5-forms/formset-in-aem-forms)

Colección de formularios relacionados agrupados para presentarlos como una sola entidad a los usuarios, lo que permite desglosar procesos de recopilación de datos complejos en secciones administrables.

## [Forms Designer](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/installing-configuring-designer)

Una aplicación independiente que se utiliza para diseñar plantillas de formularios en formularios XDP y utilizarla en su AEM Forms para generar documentos de registro.

## [Flujo de trabajo centrado en Forms](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow)

Un conjunto de pasos automatizados o manuales en AEM Forms que administran los procesos empresariales, como la aprobación de documentos, la publicación de contenido o las notificaciones a los usuarios.

## [Comunicación interactiva](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/getting-started/interactive-communications-overview)

Una implementación personalizada para administrar comunicaciones multicanal y altamente personalizadas. Combina datos de varias fuentes, como sistemas CRM o ERP, para ofrecer comunicaciones en varios formatos, como web, móvil, correo electrónico e impresión.

## [JCR (repositorio de contenido Java)](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr)

AEM Repositorio jerárquico y basado en estándares para almacenar contenido, configuraciones y metadatos en, que admite el almacenamiento de datos estructurado y no estructurado, y que admite el almacenamiento de datos estructurado y no estructurado en el espacio de trabajo.

## [Cartas](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/letters-correspondences/create-letter#create-a-letter-template)

Comunicaciones de clientes generadas que aprovechan AEM Forms Document Services. Las cartas se crean mediante una combinación de plantillas XDP, modelos de datos y fragmentos reutilizables, lo que garantiza la escalabilidad en escenarios de gran volumen.

## [Metadatos en AEM Forms](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/manage-administer-aem-forms/manage-form-metadata)

Los metadatos permiten una categorización y recuperación de recursos eficaz. AEM Forms incluye metadatos predefinidos para cada tipo de recurso y permite la personalización. También proporciona herramientas para crear, administrar e intercambiar metadatos sin problemas.

## [Generador de PDF](https://experienceleague.adobe.com/es/docs/experience-manager-learn/forms/document-services/using-pdfg-in-aem-forms)

Herramienta de AEM Forms que convierte varios formatos de archivo (por ejemplo, Word, Excel y PowerPoint) en documentos de PDF y proporciona funciones como cifrado, marca de agua y combinación.

## [Instancia de publicación](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

AEM Entorno en el que se proporciona contenido en directo a los usuarios finales. Ofrece formularios, páginas y otras experiencias digitales con un rendimiento optimizado.

## [Editor de reglas](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components)

Una herramienta visual en Forms adaptable que permite a los autores definir reglas y lógicas personalizadas para los campos de formulario, como visibilidad, validación y rellenado previo de datos, sin requerir experiencia en codificación.

## [Firmas manuscritas](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble)

Característica de AEM Forms que permite a los usuarios firmar formularios electrónicamente dibujando su firma directamente en el formulario con un mouse (ratón) o un dispositivo táctil.

## [Enviar acción en AEM Forms](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/configuring-submit-actions)

Acciones del lado del servidor o del lado del cliente ejecutadas al enviar el formulario. Algunos ejemplos son llamadas a la API de REST, invocar un flujo de trabajo o escribir datos en un JCR (repositorio de contenido Java).

## [Temas](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components)

Marcos de estilo impulsados por CSS aplicados a formularios adaptables, que utilizan LESS/SASS para preprocesadores. Las temáticas garantizan el cumplimiento de las directrices de promoción de la marca y los estándares de accesibilidad, puede personalizar una temática, cambiar sus elementos de diseño, diseño, colores, tipografía y, a veces, el código subyacente.

## [Plantilla](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components)

Modelos para formularios adaptables, que comprenden elementos estructurales (campos, diseños) y scripts preconfigurados, puede crear y personalizar nuevas plantillas o utilizar plantillas predeterminadas existentes.

## [Capa web](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Comprende JSP o servlets creados sobre servicios comunes y de formularios, que proporcionan funcionalidades como la creación de front-end, la representación y el envío de formularios front-end y las API de REST.

## [XDP (paquete de datos XML)](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/manage-administer-aem-forms/get-xdp-pdf-documents-aem)

Formato de archivo utilizado en AEM Forms para diseñar y estructurar formularios, lo que permite procesarlos como PDF o HTML y, al mismo tiempo, admite contenido dinámico e interactividad.

## [XFA (arquitectura de Forms XML)](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-an-xfa-form-template)

Una tecnología heredada para crear PDF forms interactivos y dinámicos. Los formularios XFA permiten funciones avanzadas, como ajustes de diseño dinámico, scripts e integración perfecta con sistemas back-end.

## [Esquema XML o JSON](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-xml-or-json-schema)

Una estructura estandarizada utilizada para definir el formato y la organización de los datos XML o JSON en los formularios y flujos de trabajo. Estos esquemas garantizan una gestión coherente de los datos y permiten la interoperabilidad con sistemas externos.

<!--

## **Custom Properties**  

Developer-defined metadata attributes added to components or forms for advanced behaviors, accessed via Sling APIs or Groovy scripts for dynamic processing.

## **Embedding** 

Integrating adaptive forms into AEM Sites or external web pages using `<iframe>` or SPA (Single Page Application) models. Embedding supports seamless session handling and cross-origin resource sharing (CORS).

## **CDN (Content Delivery Network)**  

Distributed networks (e.g., Akamai) used for caching and delivering forms-related resources, ensuring high availability and faster load times for geographically distributed users.


## **Dispatcher**  

An AEM caching and load balancing tool configured to optimize delivery of adaptive forms. Its filter rules ensure secure access control while caching frequently accessed forms and assets.

## **Editors**  

Tools like the Adaptive Forms Editor, Theme Editor, and Rule Editor, enabling developers and content authors to customize forms and their behavior without extensive coding.

## **Responsive UI**  

An implementation of media queries and flexible grids, ensuring adaptive forms render seamlessly across various screen sizes and devices.

## **Custom Functions**  

JavaScript-based utilities or REST microservices that provide additional logic (e.g., complex field validation or data pre-population), extending the out-of-the-box capabilities of AEM Forms.

## **Package Manager**  

AEM's CRX Package Manager facilitates importing/exporting adaptive forms, data schemas, or configurations as .zip files, enabling modular deployment in distributed environments.

## **UE (User Experience)**  

Design principles and optimizations applied in AEM Forms to enhance usability, including accessibility features (ARIA roles, tab navigation) and intuitive layouts.

## **Forms Submission Services**

Back-end services for handling form submissions, integrating with the AEM Workflow engine, third-party APIs, or direct JCR persistence.


Foundation components
e-signing
adobe sign
letters
submit action
data sources
adaptive form block
edge delivery services
forms integration
custom component 
themes
template 
custom properties
embedding
CDN
Dispatcher
editors
responsive UI
custom functions
package manager
communication APIs
UE
Forms submission services
Form review
Forms Versioning
Adobe analytics forms integration specific

## **AEM Forms Foundation Components**  
Core reusable elements within AEM Forms, built on Granite UI, enabling developers to create complex forms. They provide robust features like data bindings, field validations, and support for multilingual content.


## **e-Signing**  
An implementation of digital signature standards (e.g., PKCS #7) within AEM Forms, integrated with Adobe Sign APIs to ensure secure and legally binding electronic signatures.

## Workspace

A browser-based interface for users to interact with AEM Forms workflows, tasks, and approvals.

## Sling

A REST-based web framework used in AEM to map request URLs to content resources, enabling efficient content rendering and delivery.

-->