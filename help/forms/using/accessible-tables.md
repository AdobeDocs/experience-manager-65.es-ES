---
title: Crear tablas complejas accesibles en formularios HTML5
seo-title: Crear tablas complejas accesibles en formularios HTML5
description: Aprenda a crear tablas accesibles en formularios HTML5.
seo-description: Aprenda a crear tablas accesibles en formularios HTML5.
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Crear tablas complejas accesibles en formularios HTML5 {#create-accessible-complex-tables-in-html-forms}

La implementación predeterminada de tablas en HTML5 Forms utiliza elementos DIV HTML para representar una tabla. La renderización implica el uso de funciones ARIA para satisfacer los requisitos de accesibilidad.

Para evitar problemas de accesibilidad con lectores de pantalla que no admiten completamente las funciones ARIA utilizadas con tablas de datos, HTML5 Forms proporciona una representación alternativa para las tablas. Estas tablas se basan en el nuevo formato de tabla introducido en Designer, que también admite:

* Encabezados de fila
* Intervalo de fila

Para utilizar el nuevo formato en HTML5 Forms, marque la tabla como compleja. Para marcar la tabla como compleja, añada la etiqueta `extras` en el subformulario fuente XML de la tabla de la siguiente manera:

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

Las tablas marcadas como *complexTable* siguen la representación HTML nativa y proporcionan un mejor soporte de accesibilidad para determinados lectores de pantalla.  Para crear un intervalo de filas, seleccione celdas consecutivas de una tabla en la misma columna, haga clic con el botón derecho en la selección y, a continuación, haga clic en **[!UICONTROL Combinar celdas]**.

>[!NOTE]
>
>La creación de un intervalo de filas solo funciona para celdas de la izquierda.

Para marcar una fila como encabezado de fila, seleccione todas las celdas de la fila, haga clic con el botón secundario en la selección y, a continuación, haga clic en **[!UICONTROL Marcar encabezado]**.

Para marcar una celda como encabezado de columna, seleccione cualquier celda de la columna, haga clic con el botón derecho en la selección y, a continuación, haga clic en **[!UICONTROL Marcar encabezado]**.

Limitaciones en el nuevo formato *AccessibleTable*:

* Falta de compatibilidad con campos ampliables si se utiliza rowspan en la tabla
* No se admiten tablas anidadas (tablas dentro de celdas de tabla)
* La compatibilidad con el intervalo de filas está limitada a las filas de encabezado y celdas de encabezado
* El soporte se limita a tablas regulares
* No se admiten prefijos de datos en tablas con intervalo de tiempo > 1

