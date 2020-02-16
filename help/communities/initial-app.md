---
title: Aplicación inicial de Simulador para pruebas
seo-title: Aplicación inicial de Simulador para pruebas
description: Creación de plantillas, componentes y secuencias de comandos
seo-description: Creación de plantillas, componentes y secuencias de comandos
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Aplicación inicial de Simulador para pruebas {#initial-sandbox-application}

En esta sección, creará lo siguiente:

* La **[plantilla](#createthepagetemplate)**que se utilizará para crear páginas de contenido en el sitio web de ejemplo
* El **[componente y la secuencia de comandos](#create-the-template-s-rendering-component)**que se utilizarán para procesar las páginas del sitio web

## Creación de la plantilla de contenido {#create-the-content-template}

Una plantilla define el contenido predeterminado de una nueva página. Los sitios Web complejos pueden utilizar varias plantillas para crear los distintos tipos de páginas del sitio. Además, el conjunto de plantillas puede convertirse en un modelo utilizado para implementar cambios en un clúster de servidores.

En este ejercicio, todas las páginas se basan en una plantilla sencilla.

1. En el panel del explorador de CRXDE Lite

   * select `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Crear > Crear plantilla]**

1. En el cuadro de diálogo Crear plantilla, escriba los valores siguientes y haga clic en **[!UICONTROL Siguiente]**:

   * Etiqueta: `playpage`
   * Título: `An SCF Sandbox Play Template`
   * Descripción: `An SCF Sandbox template for play pages`
   * Tipo de medio: `an-scf-sandbox/components/playpage`
   * Clasificación: &lt;dejar como predeterminado>
   La etiqueta se utiliza para el nombre del nodo.

   El tipo de recurso aparece en el nodo jcr:content `playpage`de la propiedad `sling:resourceType`. Identifica el componente (recurso) que procesa el contenido cuando lo solicita un explorador.

   En este caso, todas las páginas creadas con la `playpage`plantilla son representadas por el `an-scf-sandbox/components/playpage` componente. Por convención, la ruta del componente es relativa, lo que permite a Sling buscar el recurso primero en la `/apps` carpeta y, si no se encuentra, en la `/libs` carpeta.

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. Si utiliza copiar/pegar, asegúrese de que el valor Tipo de recurso no tenga espacios al inicio o al final.

   Haga clic en **[!UICONTROL Siguiente]**. 

1. &quot;Rutas permitidas&quot; se refiere a las rutas de las páginas que utilizan esta plantilla, de modo que la plantilla aparece enumerada en el cuadro de diálogo **[!UICONTROL Nueva página]** .

   Para agregar una ruta, haga clic en el botón más `+` y escriba `/content(/.&ast;)?` en el cuadro de texto que aparece. Si utiliza copiar/pegar, asegúrese de que no hay espacios al inicio o al final.

   Nota: El valor de la propiedad path permitida es una expresión *regular.* Las páginas de contenido que tengan una ruta que coincida con la expresión pueden utilizar la plantilla. En este caso, la expresión regular coincide con la ruta de la carpeta **/content** y todas sus subpáginas.

   Cuando un autor crea una página a continuación `/content`, la `playpage`plantilla titulada &quot;Plantilla de página de Simulador para pruebas de SCF&quot; aparece en una lista de plantillas disponibles para usar.

   Después de crear la página raíz a partir de la plantilla, el acceso a la plantilla se puede restringir a este sitio Web modificando la propiedad para incluir la ruta raíz en la expresión regular, es decir,

   `/content/an-scf-sandbox(/.&ast;)?`

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Haga clic en **[!UICONTROL Siguiente]**. 

   Haga clic en **[!UICONTROL Siguiente]** en el panel Padres **** permitidos.

   Haga clic en **[!UICONTROL Siguiente]** en los paneles Elementos secundarios **** permitidos.

   Haga clic en **[!UICONTROL Aceptar]**.

1. Una vez que haga clic en Aceptar y termine de crear la plantilla, observará que aparecen triángulos rojos en las esquinas de los valores de la ficha Propiedades para la nueva `playpage`plantilla. Estos triángulos rojos indican ediciones que no se han guardado.

   Haga clic en **[!UICONTROL Guardar todo]** para guardar la nueva plantilla en el repositorio.

   ![chlimage_1-77](assets/chlimage_1-77.png)

### Creación del componente de procesamiento de la plantilla {#create-the-template-s-rendering-component}

Cree el *componente* que define el contenido y procesa todas las páginas creadas en función de la plantilla [de](#createthepagetemplate)página de reproducción.

1. En CRXDE Lite, haga clic con el botón derecho **`/apps/an-scf-sandbox/components`** y, a continuación, haga clic en **[!UICONTROL Crear > Componente]**.
1. Al establecer el nombre del nodo (Label) en *playpage*, la ruta del componente es

   `/apps/an-scf-sandbox/components/playpage`

   que corresponde al tipo de recurso de la plantilla de página de reproducción (opcionalmente menos la parte inicial **`/apps/`** de la ruta).

   En el cuadro de diálogo **[!UICONTROL Crear componente]** , escriba los siguientes valores de propiedad:

   * Etiqueta: **playpage**
   * Título: Componente **Reproducción de Simulador para pruebas SCF**
   * Descripción: **Este es el componente que procesa el contenido de una página de Simulador para pruebas de SCF.**
   * Super Tipo: *&lt;dejar en blanco>*
   * Agrupar:
   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Haga clic en **[!UICONTROL Siguiente]** hasta que aparezca el panel Elementos secundarios **** permitidos del cuadro de diálogo

   * Haga clic en **[!UICONTROL Aceptar]**
   * Haga clic en **[!UICONTROL Guardar todo]**

1. Compruebe que la ruta del componente y el resourceType de la plantilla coinciden.

   >[!CAUTION]
   >
   >La correspondencia entre la ruta de acceso al componente playpage y la propiedad sling:resourceType de la plantilla playpage es crucial para el correcto funcionamiento del sitio web.

   ![chlimage_1-79](assets/chlimage_1-79.png)