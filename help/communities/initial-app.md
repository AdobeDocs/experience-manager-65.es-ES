---
title: Aplicación de espacio aislado inicial
seo-title: Initial Sandbox Application
description: Crear plantilla, componente y secuencia de comandos
seo-description: Create template, component, and script
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 2%

---

# Aplicación de espacio aislado inicial {#initial-sandbox-application}

En esta sección, se crea lo siguiente:

* La variable **[plantilla](#createthepagetemplate)** que se utilizará para crear páginas de contenido en el sitio web de ejemplo.
* La variable **[componente y secuencia de comandos](#create-the-template-s-rendering-component)** que se utilizará para procesar las páginas del sitio web.

## Creación de la plantilla de contenido {#create-the-content-template}

Una plantilla define el contenido predeterminado de una página nueva. Los sitios web complejos pueden utilizar varias plantillas para crear los distintos tipos de páginas del sitio. Además, el conjunto de plantillas puede convertirse en un modelo utilizado para implementar cambios en un clúster de servidores.

En este ejercicio, todas las páginas se basan en una plantilla sencilla.

1. En el panel del explorador del CRXDE Lite:

   * Seleccione `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Crear]** > **[!UICONTROL Crear plantilla]**

1. En el cuadro de diálogo Crear plantilla, escriba los valores siguientes y haga clic en **[!UICONTROL Siguiente]**:

   * Etiqueta: `playpage`
   * Título: `An SCF Sandbox Play Template`
   * Descripción: `An SCF Sandbox template for play pages`
   * Tipo de medio: `an-scf-sandbox/components/playpage`
   * Clasificación: &lt;leave as=&quot;&quot; default=&quot;&quot;>

   La etiqueta se utiliza para el nombre del nodo.

   El tipo de recurso aparece en la variable `playpage`El nodo jcr:content de como propiedad `sling:resourceType`. Identifica el componente (recurso) que procesa el contenido cuando lo solicita un explorador.

   En este caso, todas las páginas creadas con la variable `playpage` la plantilla se representa mediante la variable `an-scf-sandbox/components/playpage` componente. Por norma, la ruta al componente es relativa, lo que permite a Sling buscar el recurso primero en la `/apps` y, si no se encuentran, en la `/libs` carpeta.

   ![create-content-template](assets/create-content-template-1.png)

1. Si utiliza copiar/pegar, asegúrese de que el valor Tipo de recurso no tenga espacios al principio o al final.

   Haga clic en **[!UICONTROL Siguiente]**.

1. &quot;Rutas permitidas&quot; se refiere a las rutas de las páginas que utilizan esta plantilla, de modo que la plantilla se enumera para la variable **[!UICONTROL Nueva página]** diálogo.

   Para añadir una ruta, haga clic en el botón más `+` y tipo `/content(/.&ast;)?` en el cuadro de texto que aparece. Si utiliza copiar/pegar, asegúrese de que no haya espacios al principio o al final.

   Nota: El valor de la propiedad de ruta permitida es un *expresión regular*. Las páginas de contenido que tengan una ruta que coincida con la expresión pueden utilizar la plantilla . En este caso, la expresión regular coincide con la ruta del **/content** y todas sus subpáginas.

   Cuando un autor crea una página a continuación `/content`, el `playpage` plantilla titulada &quot;Una plantilla de página de espacio aislado de SCF&quot; aparece en una lista de plantillas disponibles para usar.

   Una vez creada la página raíz a partir de la plantilla, el acceso a la plantilla se puede restringir a este sitio web modificando la propiedad para incluir la ruta raíz en la expresión regular, es decir,

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. Haga clic en **[!UICONTROL Siguiente]**.

   Haga clic en **[!UICONTROL Siguiente]** en el **[!UICONTROL Principales permitidos]** panel.

   Haga clic en **[!UICONTROL Siguiente]** en el **[!UICONTROL Niños permitidos]** paneles.

   Haga clic en **[!UICONTROL Aceptar]**.

1. Una vez que haga clic en Aceptar y termine de crear la plantilla, verá que se muestran triángulos rojos en las esquinas de los valores de la pestaña Propiedades para la nueva plantilla `playpage` plantilla. Estos triángulos rojos indican ediciones que no se han guardado.

   Haga clic en **[!UICONTROL Guardar todo]** para guardar la nueva plantilla en el repositorio.

   ![verify-content-template](assets/verify-content-template.png)

### Crear el componente de renderización de la plantilla {#create-the-template-s-rendering-component}

Cree la variable *componente* que define el contenido y procesa todas las páginas creadas en función de la variable [plantilla de página de reproducción](#createthepagetemplate).

1. En el CRXDE Lite, haga clic con el botón derecho **`/apps/an-scf-sandbox/components`** y haga clic en **[!UICONTROL Crear > Componente]**.
1. Al establecer el nombre del nodo (etiqueta) en *playpage*, la ruta al componente es

   `/apps/an-scf-sandbox/components/playpage`

   que corresponde al Tipo de recurso de la plantilla de página de reproducción (opcionalmente menos el valor inicial **`/apps/`** parte de la ruta).

   En el **[!UICONTROL Crear componente]** , escriba los siguientes valores de propiedad:

   * Etiqueta: **playpage**
   * Título: **Un componente de reproducción de espacio aislado de SCF**
   * Descripción: **Este es el componente que procesa contenido para una página de espacio aislado de SCF.**
   * Super Tipo: *&lt;leave blank=&quot;&quot;>*
   * Grupo: *&lt;leave blank=&quot;&quot;>*

   ![create-template-component](assets/create-template-component.png)

1. Haga clic en **[!UICONTROL Siguiente]** hasta que **[!UICONTROL Niños permitidos]** del cuadro de diálogo:

   * Haga clic en **[!UICONTROL Aceptar]**.
   * Haga clic en **[!UICONTROL Guardar todo]**.

1. Compruebe que la ruta al componente y el resourceType de la plantilla coinciden.

   >[!CAUTION]
   >
   >La correspondencia entre la ruta al componente playpage y la propiedad sling:resourceType de la plantilla playpage es crucial para el correcto funcionamiento del sitio web.

   ![verify-template-component](assets/verify-template-component.png)
