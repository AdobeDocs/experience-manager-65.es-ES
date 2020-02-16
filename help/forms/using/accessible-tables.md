---
title: Creación de tablas complejas accesibles en formularios HTML5
seo-title: Creación de tablas complejas accesibles en formularios HTML5
description: Aprenda a crear tablas accesibles en formularios HTML5.
seo-description: Aprenda a crear tablas accesibles en formularios HTML5.
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Creación de tablas complejas accesibles en formularios HTML5 {#create-accessible-complex-tables-in-html-forms}

La implementación predeterminada de tablas en formularios HTML5 utiliza elementos DIV HTML para representar una tabla. El procesamiento implica el uso de funciones ARIA para cumplir los requisitos de accesibilidad.

Para evitar problemas de accesibilidad con lectores de pantalla que no admiten completamente las funciones ARIA utilizadas con tablas de datos, HTML5 Forms proporciona una representación alternativa para las tablas. Estas tablas se basan en el nuevo formato de tabla introducido en Designer, que también admite:

* Encabezados de fila
* Intervalo de filas

Para utilizar el nuevo formato en formularios HTML5, marque la tabla como compleja. Para marcar la tabla como compleja, agregue la `extras` etiqueta en el subformulario de origen XML de tabla de la siguiente manera:

```
</extras>
 <text name="complexTable">1</text>
 </extras>
```

Las tablas marcadas como *complejaTable* siguen la representación HTML nativa y proporcionan una mejor compatibilidad de accesibilidad para determinados lectores de pantalla.  Para crear un intervalo de filas, seleccione celdas consecutivas de una tabla en la misma columna, haga clic con el botón secundario en la selección y, a continuación, haga clic en **[!UICONTROL Combinar celdas]**.

*****Nota: La creación de un lapso de filas solo funciona para las celdas situadas más a la izquierda.*

Para marcar una fila como encabezado de fila, seleccione todas las celdas de la fila, haga clic con el botón secundario en la selección y, a continuación, haga clic en **[!UICONTROL Marcar encabezado]**.

Para marcar una celda como encabezado de columna, seleccione cualquier celda de la columna, haga clic con el botón secundario en la selección y, a continuación, haga clic en **[!UICONTROL Marcar encabezado]**.

Limitaciones en el nuevo formato *AccessibleTable* :

* Falta de compatibilidad con los campos ampliables si se utiliza rowspan en la tabla
* No se admiten tablas anidadas (tablas dentro de celdas de tabla)
* La compatibilidad para el grupo de filas está limitada a las filas de encabezado y celdas de encabezado
* El apoyo se limita a los cuadros ordinarios
* No se admiten prefijos de datos en tablas con un intervalo de filas > 1

