---
title: La generación de PDF no puede imprimir un gran número de PDF con Workbench
description: Cuando un cliente genera un gran número de PDF a través de servicios implementados mediante Workbench, el servicio de impresión falla.
exl-id: f3746b8e-4c38-447a-b5bf-d11fc77556f7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
role: User, Developer
source-git-commit: 20d6c716b4ba799a7d4ae2858459f7c38cf3da02
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---

# La generación de PDF no puede imprimir un gran número de PDF a través de Workbench {#PDF-generation-fails-to-print-a-large-number-of-PDFs-via-WorkBench}

## Problema {#issue}

Cuando un cliente genera un gran número de PDF a través de servicios implementados mediante Workbench. El servicio falla debido a que no hay memoria suficiente. El error se muestra como:

`ALC-OUT-002-013: XMLFormFactory, PAexecute failure: "0: Out of Memory"`

<!--
Attached is a simplified template (BollatoRiservatiLandscape_table_simple.xdp) that simulates the problem.
Using the Designer, if we associate the template "BollatoRiservatiLandscape_table_semplice.xdp" with the XML file "BollatoRiservati.xml" during the generation of the pdf, the process comes to occupy 1.6 Gb of RAM. On the server side, with the complete template, the pdf generation process breaks down, occupying 2 GB of RAM.
-->

Esto se debe a que el número máximo de páginas en una solicitud de impresión está limitado a aproximadamente 1000 páginas en Windows. Cuando se genera una salida de impresión, es necesario cargar la plantilla y los datos en la memoria y el diseño resultante se crea en la memoria. Esto significa que el tamaño de la salida final tiene límites. El proceso que genera la salida de impresión es una tarea de 32 bits, lo que significa que está limitada a 2 GB de RAM en Windows <!--and 4 GB on UNIX-->.

## Se aplica a {#applies-to}

La solución se aplica a AEM Forms <!--JEE Server and AEM Forms on OSGi Server--> para x86_win32 XMLFM.

## Solución {#solution}

El factor más grande que afecta al uso de la memoria es la cantidad de datos de un formulario. Sin embargo, hay otros factores en un diseño de formulario que afectan en menor medida al uso de la memoria. Cuando tenga en cuenta estos factores, puede diseñar un formulario para una salida de impresión más grande. La siguiente sección indica, en orden de prioridad, los factores que influyen en el espacio de memoria:

### Factor de impacto {#impact-factor}

**Alta**

1. **Subformularios de opción**: un conjunto de subformularios de opción es una variación del objeto del conjunto de subformularios que le permite personalizar la visualización de subformularios específicos desde el conjunto mediante instrucciones condicionales.
1. **Usar texto estático en lugar de subtítulos**: casi todos los campos proporcionan un subtítulo dentro de, el usuario debe utilizarlo en lugar de tener un texto estático adicional como subtítulo.
1. Utilice **formato de texto enriquecido (RTF)** siempre que sea posible.

**Promedio**

Factores adicionales que se deben tener en cuenta al diseñar la plantilla de formulario para ayudar a mejorar el uso de la memoria:

1. Evite utilizar texto estático para etiquetar un campo. En su lugar, utilice subtítulos en el campo de texto.
2. No utilice en exceso rectángulos, líneas, objetos y tablas.
3. Avoid using RichText and Choice Subforms if possible.
4. Avoid excessive use of Subforms and nested Subforms.

### Data size Limitation {#data-size-limitations}

As we are limited by the max process memory and the memory consumed by the process does not only depend on the size of the data file. It is very closely linked to the form design, and to some extent, to the actual amount of data being merged in the form.

If the form has many small nodes with small data, the process consumes more memory (and hence go out of memory faster), than a form that has less number of nodes (even) with large data.

Read the [Appendix below](#appendix) for more information, where test results are based on Print form (Non-Tagged PDF). Using tagged PDF process memory requirement increases. It also depends on the number of fields in the form - roughly the process memory requirement would be slightly more than 1.5 times of non-tagged PDF.

### Interactive Forms {#interactive-forms}

Interactive forms would consume more memory than Print Forms as interactive fields are rendered again. In the tests carried out, the memory consumption increased by a factor of 1.5 approximately as compared to print forms and these were static interactive forms.

### Image formats {#image-formats}

Adobe does not recommend any specific image format. But it would be nice to have a smaller size of image, e.g.,  PNG (Portable Network Graphics). It is also not advisable to use images of high resolutions whose sizes vary several hundreds of MegaBytes. Also, it is not advisable to use compressed images whose size upon decompression expands to several hundreds of Megabytes of data.

### Appendix {#appendix}

**Table Examples**

Different variants for tables are shown below that show rendering number of pages versus data size for simple table and complex table.

1. A Table with a single column where 5000 pages of PDFs are generated, data file size 24 MB and 30-K records.

   ![table_single_column](/help/forms/using/assets/table_single_column.png)

1. A table with many small columns where 800 pages of PDFs are generated, data file size is 4.6 MB and 20-K records.
   ![table_many_small_columns](/help/forms/using/assets/table_many_small_columns.png)

1. A table with many small columns, but bigger data file because of usage of bigger xmlTag names.
En este caso, todo es igual que el anterior, pero los nombres de etiquetas xml se han hecho grandes (por lo que el tamaño del archivo de datos aumentará sin ningún aumento en los datos efectivos reales), el resultado final (límite superior) es casi el mismo. Aunque el tamaño del archivo de datos aumentó de 4,6 MB a 44,6 MB. Aquí se generan 800 páginas de PDF, el tamaño del archivo de datos es de 44,6 MB y los registros de 20-K.

   ![nombre_etiqueta_xml_table_greater_table](/help/forms/using/assets/table_bigger_xml_tagname.png)

Por lo tanto, es difícil establecer un límite superior general en el tamaño del archivo de datos. Cada formulario es único y, por lo tanto, el consumo de memoria diferiría de una forma a otra.
