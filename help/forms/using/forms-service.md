---
title: Servicio de Forms
seo-title: Servicio de Forms
description: El artículo describe el servicio de Forms y las tareas relacionadas con el formulario que puede realizar con el servicio de Forms.
seo-description: El artículo describe el servicio de Forms y las tareas relacionadas con el formulario que puede realizar con el servicio de Forms.
uuid: 3258d3c2-8755-4815-8c97-b2cfb9a9dfd4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: a9695d10-43ec-40eb-942f-7720abaa0973
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 6%

---


# Servicio de Forms {#forms-service}

## Información general {#overview}

El servicio Forms permite crear aplicaciones cliente de captura de datos interactivas que validan, procesan, transforman y envían formularios que se suelen crear en Designer. El servicio Forms procesa como documentos PDF cualquier diseño de formulario que desarrolle.

El servicio Forms también permite a las organizaciones ampliar sus procesos inteligentes de captura de datos mediante la implementación de formularios electrónicos como archivos PDF de Adobe. También puede utilizar el servicio para importar y exportar datos a y desde PDF forms existentes, respectivamente.

Utilice el servicio de Forms para hacer lo siguiente:

* Representar PDF forms basados en plantillas y datos XML.
* Habilite la integración de datos de formulario para importar datos en PDF forms y extraerlos.
* Procesar formularios basados en fragmentos.

## Creación de PDF forms  {#creating-pdf-forms-nbsp}

Utilice el servicio de formularios para crear PDF forms para la captura de datos. Normalmente, el inicio se realiza con una plantilla de AEM Forms Designer. Utilice la operación `renderPDFForm` (vínculo a Javadoc) del servicio de Forms para convertir esta plantilla en un formulario PDF.

El primer parámetro de la operación `renderPDFForm` es el nombre del archivo de plantilla (por ejemplo, `ExpenseClaim.xdp`). Puede almacenar el archivo de plantilla en un sistema de archivos local, en un repositorio CRX o en una ubicación HTTP o FTP. Puede especificar la ubicación del archivo de plantilla estableciendo la raíz de contenido en el parámetro `PDFFormRenderOptions` de la operación `renderPDFForm`. Consulte Javadoc para obtener detalles de otras opciones que puede especificar para el parámetro `PDFFormRenderOptions`.

La operación `renderPDFForm` también puede aceptar datos XML. Los datos XML se combinan con la plantilla al crear un formulario PDF para que el formulario PDF generado contenga los datos especificados. El segundo parámetro para la operación `renderPDFForm` puede aceptar un objeto Documento (Javadoc) que contenga datos XML.

## Extracción de datos de PDF forms  {#extracting-data-from-pdf-forms-nbsp}

Utilice la operación `exportData` (Javadoc) del servicio de Forms para extraer datos XML de un formulario PDF. Esta operación acepta un documento como su primer parámetro. Puede exportar los datos como un documento XDP o como un archivo XML. Si exporta los datos como un archivo XML, los datos exportados quitan el sobre XDP y devuelven un archivo XML sin formato. Puede especificar esta disposición con el segundo parámetro.

## Importación de datos en PDF forms {#importing-data-into-pdf-forms}

El servicio Forms también permite combinar un formulario PDF creado con AEM Forms Designer o la operación `renderPDFForm` con datos XML. La operación `importData` (Javadoc) del servicio Forms acepta el formulario PDF y los datos XML y devuelve un formulario PDF con datos XML.

## Representación de formularios basados en fragmentos {#rendering-forms-based-on-fragments}

El servicio Forms puede procesar formularios basados en fragmentos creados con AEM Forms Designer. Un fragmento es una parte reutilizable de un formulario. Se guarda como un archivo XDP independiente que se puede insertar en varios diseños de formulario. Por ejemplo, un fragmento puede incluir un bloque de direcciones o texto legal.

El uso de fragmentos simplifica y acelera la creación y el mantenimiento de un gran número de formularios. Al crear un formulario, inserte una referencia al fragmento requerido para que el fragmento aparezca en el formulario. La referencia de fragmento contiene un subformulario que señala al archivo XDP físico.

Las ventajas de utilizar fragmentos son las siguientes:

* **Reutilización** del contenido: Puede reutilizar el contenido en varios diseños de formulario. Para reutilizar rápidamente partes del mismo contenido en varios formularios, cree un fragmento. Copiar o volver a crear el contenido lleva más tiempo. El uso de fragmentos también garantiza que las partes de un diseño de formulario utilizadas con frecuencia tengan un contenido y un aspecto coherentes en todos los formularios de referencia.
* **Actualizaciones** globales: Puede realizar cambios globales en varios formularios solo una vez en un archivo. Puede cambiar el contenido, los objetos de secuencia de comandos, los enlaces de datos, el diseño o los estilos de un fragmento. Todos los formularios XDP que hacen referencia al fragmento reflejan los cambios.
* **Creación** de formularios compartidos: Puede compartir la creación de formularios entre varios recursos. Los desarrolladores de formularios con experiencia en secuencias de comandos u otras funciones avanzadas de AEM Forms Designer pueden desarrollar y compartir fragmentos que utilizan secuencias de comandos y propiedades dinámicas. Los diseñadores de formularios pueden utilizar los fragmentos para diseñar formularios. Además, pueden utilizar los fragmentos para garantizar que todas las partes de un formulario tengan una apariencia y funcionalidad coherentes en varios formularios.

