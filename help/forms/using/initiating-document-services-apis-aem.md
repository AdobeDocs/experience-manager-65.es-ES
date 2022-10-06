---
title: Iniciar las API de servicios de documentos desde AEM flujo de trabajo
seo-title: Initiate Document Services APIs from AEM Workflow
description: Aprenda a invocar AEM Document Services en DDX o en las entradas suministradas. Consulte también cómo convertir el PDF a PDF/A
seo-description: Learn how to invoke AEM Document services on DDX or supplied inputs. Also see hwo to convert PDF to PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
exl-id: 123087a2-9d09-4579-9185-2ccd7d25bf8d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 2%

---

# Iniciar las API de servicios de documentos desde AEM flujo de trabajo  {#initiate-document-services-apis-from-aem-workflow}

## Ensamblador {#assembler}

AEM Forms proporciona flujos de trabajo personalizados para invocar las siguientes API del servicio Assembler:

* **invoke**: Invoca operaciones especificadas en la entrada DDX en las entradas suministradas.
* **toPDFA**: Convierte el documento del PDF de entrada en el documento PDF/A.

### Invocar flujo de trabajo DDX {#invoke-ddx-workflow}

La variable **Invocar DDX** El flujo de trabajo invoca la variable `Invoke` API de servicio del ensamblador, que puede utilizar para ensamblar o desmontar documentos, agregar marcas de agua a un PDF, etc.

1. Arrastre el **[!UICONTROL Invocar DDX]** paso del flujo de trabajo en la ficha Forms Workflow de la barra de tareas.
1. Haga doble clic en el paso de flujo de trabajo añadido para editar el componente.
1. En el cuadro de diálogo Editar componente, configure los documentos de entrada, las opciones de entorno y los documentos de salida y haga clic en **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents}

El flujo de trabajo Invocar DDX requiere los siguientes documentos de entrada:

* **DDX**: Es una entrada obligatoria para el paso Invocar flujo de trabajo DDX y se puede especificar seleccionando una de las siguientes opciones en la lista desplegable de entrada DDX.

   * *Relativo A Carga Útil*: El archivo de entrada DDX es relativo a la carpeta de carga útil para el elemento de flujo de trabajo.
   * *Usar carga útil*: La carga útil del elemento de flujo de trabajo se utiliza como documento DDX de entrada.
   * *Ruta absoluta*: La ruta absoluta al documento DDX en el repositorio CRX.

* **Crear mapa a partir de PayLoad**: Cuando se selecciona, todos los documentos de la carpeta de carga útil se añaden al Mapa del documento de entrada para el `invoke` API en Assembler. El nombre de nodo de cada documento se utiliza como clave en el mapa.

* **Mapa del documento de entrada**: Especifica el mapa del documento de entrada. Puede agregar cualquier número de entradas, donde cada una especifica la clave del documento en el mapa y el origen del documento.

#### Opciones de entorno {#environment-options}

La pestaña Opciones de entorno le permite establecer varias opciones de procesamiento para la API de invocación.

* *Nivel de registro de trabajo*: Especifica el nivel de registro para los registros de procesamiento.
* *Validar solo*: Comprueba la validez del DDX de entrada.

* *Error al producirse el error*: Especifica si la llamada al servicio Assembler debe fallar en caso de error. El valor predeterminado es False.

#### Documentos de salida {#output-documents}

En función del DDX de entrada, la API de invocación puede producir varios documentos de salida. La pestaña Documentos de salida permite seleccionar dónde se guardará el documento de salida.

1. *Guardar salida en carga útil*: Guarda los documentos de salida en la carpeta de carga útil o sobrescribe la carga útil si esta es un archivo.
1. *Mapa del documento de salida*: Permite especificar explícitamente dónde guardar cada documento de salida agregando una entrada por documento de salida. Cada entrada especifica el documento y dónde guardarlo. Un documento de salida puede sobrescribir la carga útil o guardarse en la carpeta de carga útil. Resulta útil cuando hay varios documentos de salida.

1. *Registro de trabajos*: Especifica dónde guardar el documento de registro de trabajos, lo que resulta útil para solucionar errores.

### Convertir en flujo de trabajo PDF/A {#convert-to-pdf-a-workflow}

El paso Convertir en PDF/A del flujo de trabajo invoca la variable `toPDFA` API de servicio del ensamblador. Se utiliza para convertir documentos PDF a documentos compatibles con el PDF/A.

1. Arrastre el **[!UICONTROL ConvertToPDFA]** paso del flujo de trabajo en la ficha Forms Workflow de la barra de tareas.

1. Haga doble clic en el paso de flujo de trabajo añadido para editar el componente.
1. En el cuadro de diálogo Editar componente, configure los documentos de entrada, las opciones de conversión y los documentos de salida y haga clic en **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents-1}

Especifique el origen del documento para convertirlo en un documento compatible con el PDF/A de una de las siguientes maneras.

* *Relativo A Carga Útil*: El documento de entrada es relativo a la carpeta de carga útil para el elemento de flujo de trabajo.
* *Usar carga útil*: La carga útil del elemento de flujo de trabajo se utiliza como documento de entrada.
* *Ruta absoluta*: La ruta absoluta del documento de entrada en el repositorio CRX.

#### Opciones de conversión {#conversion-options}

Las opciones de conversión permiten especificar opciones que modifican el proceso de conversión de PDF/A.

* *Cumplimiento* : Especifica el estándar del PDF/A que debe cumplir el PDF/A de salida.
* *Nivel de resultado* : Especifica el nivel de registro que se utilizará para los registros de conversión de PDF/A.
* *Firmas* : Especifica cómo se deben procesar las firmas del documento de entrada durante la conversión.
* *Espacio de color* : Especifica el espacio de color predefinido que se utilizará para el documento A/PDF de salida.
* *Verificar* Conversión: Especifica si el documento de PDF/A convertido debe verificarse para que sea compatible con el PDF/A después de la conversión.
* *Nivel de registro de trabajo* : Especifica el nivel de registro que se utilizará para procesar registros.

* *Esquema de extensión de metadatos* : Especifica la ruta al esquema de extensión de metadatos que se utilizará para XMP propiedades en los metadatos del documento de PDF.

#### Documentos de salida {#output-documents-1}

La pestaña Documentos de salida permite especificar el destino de los documentos de salida

* *Documento PDFA*: Especifica la ubicación en la que se guarda el documento A/PDF convertido. Puede sobrescribir el documento de carga útil o guardarse en la carpeta de carga útil.
* *Registro de conversión*: Especifica la ubicación en la que se guardan los registros de conversión. Puede sobrescribir el documento de carga útil o guardarse en la carpeta de carga útil.

## Forms {#forms}

El flujo de trabajo del formulario de PDF de procesamiento es un envoltorio `renderPDFForm` API de servicio de Forms para crear un formulario de PDF utilizando una plantilla XDP y un xml de datos.

### Flujo de trabajo del formulario del PDF de procesamiento {#render-pdf-form-workflow}

1. Arrastre el paso del flujo de trabajo del formulario de PDF de procesamiento a la ficha Forms Workflow de la barra de tareas.
1. Haga doble clic en el paso de flujo de trabajo añadido para editar el componente.
1. En el cuadro de diálogo Editar componente, configure los documentos de entrada, los documentos de salida y los parámetros adicionales y haga clic en **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents-2}

* *Archivo de plantilla*: Especifica la ubicación de la plantilla XDP. Es un campo obligatorio.

* *Documento de datos*: Especifica la ubicación del xml de datos que debe combinarse con la plantilla.

#### Documentos de salida {#output-documents-2}

* *Documento de salida*: - Especifica el nombre del formulario de PDF generado.

#### Parámetros adicionales {#additional-parameters}

* *Raíz del contenido*: Especifica la ruta a la carpeta del repositorio en la que se almacenan los fragmentos o imágenes utilizados en la plantilla XDP de entrada.
* *Dirección Url De Envío*: Especifica la dirección URL de envío predeterminada para el formulario de PDF generado.
* *Configuración regional*: Especifica la configuración regional predeterminada para el formulario de PDF generado.
* *Versión de Acrobat*: Especifica la versión de Acrobat de destino para el formulario de PDF generado.
* *PDF etiquetado*: Especifica si se debe hacer accesible el PDF generado.
* *Documento XCI*: Especifica la ruta al archivo XCI.

## Salida {#output}

El flujo de trabajo Generar PDF no interactivo es un envoltorio alrededor de `generatePDFOutput` API del servicio de salida. Se utiliza para generar documentos de PDF no interactivos a partir de la plantilla XDP y el xml de datos.

### Generar flujo de trabajo de salida de PDF no interactivo   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. Arrastre el flujo de trabajo Generar salida de PDF no interactivo a la ficha Forms Workflow de la barra de tareas.
1. Haga doble clic en el paso de flujo de trabajo añadido para editar el componente.
1. En el cuadro de diálogo Editar componente, configure los documentos de entrada, los documentos de salida y los parámetros adicionales y haga clic en **[!UICONTROL OK]**.

#### Documentos de entrada {#input-documents-3}

* *Archivo de plantilla*: Especifica la ubicación de la plantilla XDP. Es un campo obligatorio.

* *Documento de datos*: Especifica la ubicación del xml de datos que debe combinarse con la plantilla.

#### Documento de salida {#output-document}

*Documento de salida*: Especifica el nombre del formulario de PDF generado.

#### Parámetros adicionales {#additional-parameters-1}

* *Raíz del contenido*: Especifica la ruta a la carpeta del repositorio en la que se almacenan los fragmentos o imágenes utilizados en la plantilla XDP de entrada.
* *Configuración regional*: Especifica la configuración regional predeterminada para el formulario de PDF generado.
* *Versión de Acrobat*: Especifica la versión de Acrobat de destino para el formulario de PDF generado.
* PDF linarizado: Especifica si se debe optimizar el PDF generado para la visualización web.
* *PDF etiquetado*: Especifica si se debe hacer accesible el PDF generado.
* *Documento XCI*: Especifica la ruta al archivo XCI.
