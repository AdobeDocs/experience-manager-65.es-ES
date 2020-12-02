---
title: Iniciar las API de Documento Services desde AEM flujo de trabajo
seo-title: Iniciar las API de Documento Services desde AEM flujo de trabajo
description: Obtenga información sobre cómo invocar AEM servicios de Documento en DDX o en las entradas suministradas. Vea también cómo convertir PDF a PDF/A
seo-description: Obtenga información sobre cómo invocar AEM servicios de Documento en DDX o en las entradas suministradas. Vea también cómo convertir PDF a PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
translation-type: tm+mt
source-git-commit: 7caf09f7020c066072eac04a349a19b144dfeb7b
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---


# Iniciar las API de Documento Services desde AEM flujo de trabajo {#initiate-document-services-apis-from-aem-workflow}

## Ensamblador {#assembler}

AEM Forms proporciona flujos de trabajo personalizados para invocar las siguientes API de servicio de ensamblador:

* **invoke**: Invoca operaciones especificadas en DDX de entrada en las entradas suministradas.
* **toPDFA**: Convierte el documento PDF de entrada en documento PDF/A.

### Invocar flujo de trabajo DDX {#invoke-ddx-workflow}

El flujo de trabajo **Invocar DDX** invoca la API de servicio de ensamblador `Invoke`, que puede utilizar para montar o desmontar documentos, agregar marcas de agua a un PDF, etc.

1. Arrastre el paso del flujo de trabajo **[!UICONTROL Invocar DDX]** bajo la ficha Forms Workflow de la barra de tareas.
1. Haga clic con el botón doble en el paso de flujo de trabajo agregado para editar el componente.
1. En el cuadro de diálogo Editar componente, configure documentos de entrada, opciones de entorno y documentos de salida, y haga clic en **[!UICONTROL Aceptar]**.

#### Documentos de entrada {#input-documents}

El flujo de trabajo de invocar DDX requiere los siguientes documentos de entrada:

* **DDX**: Es una entrada obligatoria para el paso Invocar flujo de trabajo DDX y se puede especificar seleccionando una de las siguientes opciones en la lista desplegable de entrada DDX.

   * *Relativo a la carga útil*: El archivo de entrada DDX es relativo a la carpeta de carga útil del elemento de flujo de trabajo.
   * *Usar carga útil*: La carga útil del elemento de flujo de trabajo se utiliza como documento DDX de entrada.
   * *Ruta* absoluta: Ruta absoluta al documento DDX en el repositorio de CRX.

* **Crear mapa a partir de PayLoad**: Cuando se selecciona, todos los documentos de la carpeta de carga útil se agregan al mapa del Documento de entrada para la  `invoke` API en el ensamblador. El nombre de nodo de cada documento se utiliza como clave en el mapa.

* **Mapa** del Documento de entrada: Especifica el mapa del Documento de entrada. Puede agregar cualquier número de entradas, donde cada entrada especifica la clave del documento en el mapa y el origen del documento.

#### Opciones de entorno {#environment-options}

La ficha Opciones de Entorno le permite definir varias opciones de procesamiento para la API de invocación.

* *Nivel* de registro de trabajo: Especifica el nivel de registro para los registros de procesamiento.
* *Validar solamente*: Comprueba la validez del DDX de entrada.

* *Error* en caso de error: Especifica si la llamada al servicio de ensamblador debe fallar en caso de error. El valor predeterminado es False.

#### Documentos de salida {#output-documents}

Según el DDX de entrada, la API de invocación puede producir varios documentos de salida. La ficha Documentos de salida permite seleccionar dónde se guardará el documento de salida.

1. *Guardar salida en carga útil*: Guarda los documentos de salida en la carpeta de carga útil o sobrescribe la carga útil si la carga útil es un archivo.
1. *Mapa* del Documento de salida: Permite especificar explícitamente dónde guardar cada documento de salida agregando una entrada por documento de salida. Cada entrada especifica el documento y dónde guardarlo. Un documento de salida puede sobrescribir la carga útil o guardar en la carpeta de carga útil. Resulta útil cuando hay varios documentos de salida.

1. *Registro* de trabajos: Especifica dónde se guarda el documento de registro de trabajos, lo que resulta útil para solucionar errores.

### Convertir a flujo de trabajo de PDF/A {#convert-to-pdf-a-workflow}

El paso de flujo de trabajo Convertir a PDF/A invoca la API de servicio de ensamblador `toPDFA`. Se utiliza para convertir documentos PDF a documentos compatibles con PDF/A.

1. Arrastre el paso del flujo de trabajo **[!UICONTROL ConvertToPDFA]** debajo de la ficha Forms Workflow en la barra de tareas.

1. Haga clic con el botón doble en el paso de flujo de trabajo agregado para editar el componente.
1. En el cuadro de diálogo Editar componente, configure documentos de entrada, opciones de conversión y documentos de salida, y haga clic en **[!UICONTROL Aceptar]**.

#### Documentos de entrada {#input-documents-1}

Especifique el origen del documento para convertir a un documento compatible con PDF/A de una de las siguientes formas.

* *Relativo a la carga útil*: El documento de entrada es relativo a la carpeta de carga útil del elemento de flujo de trabajo.
* *Usar carga útil*: La carga útil del elemento de flujo de trabajo se utiliza como documento de entrada.
* *Ruta* absoluta: Ruta absoluta del documento de entrada en el repositorio de CRX.

#### Opciones de conversión {#conversion-options}

Las opciones de conversión permiten especificar opciones que modifican el proceso de conversión de PDF/A.

* *Cumplimiento* : Especifica el estándar PDF/A que debe cumplir el PDF/A de salida.
* *Nivel*  de resultado: Especifica el nivel de registro que se usará para los registros de conversión de PDF/A.
* *Firmas* : Especifica cómo se deben procesar las firmas en el documento de entrada durante la conversión.
* *Espacio*  de color: Especifica el espacio de color predefinido que se utilizará para el documento PDF/A de salida.
* ** VerifyConversion: Especifica si el documento PDF/A convertido debe verificarse para que sea compatible con PDF/A después de la conversión.
* *Nivel*  de registro de trabajo: Especifica el nivel de registro que se usará para procesar registros.

* *Esquema de extensión*  de metadatos: Especifica la ruta al esquema de extensión de metadatos que se utilizará para XMP propiedades en los metadatos del documento PDF.

#### Documentos de salida {#output-documents-1}

La ficha Documentos de salida permite especificar el destino de los documentos de salida

* *DOCUMENTO* PDFA: Especifica la ubicación en la que se guarda el documento PDF/A convertido. Puede sobrescribir el documento de carga útil o guardarlo en la carpeta de carga útil.
* *Registro* de conversión: Especifica la ubicación en la que se guardan los registros de conversión. Puede sobrescribir el documento de carga útil o puede guardarse en la carpeta de carga útil.

## Forms {#forms}

El flujo de trabajo Representar formulario PDF es un envoltorio alrededor de la `renderPDFForm` API de servicio de Forms para crear un formulario PDF con una plantilla XDP y un xml de datos.

### Flujo de trabajo de procesamiento de formulario PDF {#render-pdf-form-workflow}

1. Arrastre el paso de flujo de trabajo Representar formulario PDF debajo de la ficha Forms Workflow en la barra de tareas.
1. Haga clic con el botón doble en el paso de flujo de trabajo agregado para editar el componente.
1. En el cuadro de diálogo Editar componente, configure documentos de entrada, documentos de salida y parámetros adicionales, y haga clic en **[!UICONTROL Aceptar]**.

#### Documentos de entrada {#input-documents-2}

* *Archivo* de plantilla: Especifica la ubicación de la plantilla XDP. Es un campo obligatorio.

* *Documento* de datos: Especifica la ubicación del XML de datos que debe combinarse con la plantilla.

#### Documentos de salida {#output-documents-2}

* *Documento* de salida: - Especifica el nombre del formulario PDF generado.

#### Parámetros adicionales {#additional-parameters}

* *Raíz* de contenido: Especifica la ruta a la carpeta del repositorio en la que se almacenan los fragmentos o imágenes utilizados en la plantilla XDP de entrada.
* *Enviar Url*: Especifica la URL de envío predeterminada para el formulario PDF generado.
* *Configuración regional*: Especifica la configuración regional predeterminada para el formulario PDF generado.
* *Versión* de Acrobat: Especifica la versión de Acrobat de destino para el formulario PDF generado.
* *PDF* con etiquetas: Especifica si se debe hacer accesible el PDF generado.
* *Documento* XCI: Especifica la ruta al archivo XCI.

## Salida {#output}

El flujo de trabajo de generación de archivos PDF no interactivos es un envoltorio en torno a la `generatePDFOutput` API de servicio de salida. Se utiliza para generar documentos PDF no interactivos a partir de plantillas XDP y XML de datos.

### Generar flujo de trabajo de salida de PDF no interactivo   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. Arrastre el flujo de trabajo Generar salida de PDF no interactivo bajo la ficha Forms Workflow de la barra de tareas.
1. Haga clic con el botón doble en el paso de flujo de trabajo agregado para editar el componente.
1. En el cuadro de diálogo Editar componente, configure documentos de entrada, documentos de salida y parámetros adicionales, y haga clic en **[!UICONTROL Aceptar]**.

#### Documentos de entrada {#input-documents-3}

* *Archivo* de plantilla: Especifica la ubicación de la plantilla XDP. Es un campo obligatorio.

* *Documento* de datos: Especifica la ubicación del xml de datos que debe combinarse con la plantilla.

#### Documento de salida {#output-document}

*Documento* de salida: Especifica el nombre del formulario PDF generado.

#### Parámetros adicionales {#additional-parameters-1}

* *Raíz* de contenido: Especifica la ruta a la carpeta del repositorio en la que se almacenan los fragmentos o imágenes utilizados en la plantilla XDP de entrada.
* *Configuración regional*: Especifica la configuración regional predeterminada para el formulario PDF generado.
* *Versión* de Acrobat: Especifica la versión de Acrobat de destino para el formulario PDF generado.
* PDF linealizado: Especifica si se debe optimizar el PDF generado para la visualización en la Web.
* *PDF* con etiquetas: Especifica si se debe hacer accesible el PDF generado.
* *Documento* XCI: Especifica la ruta al archivo XCI.

