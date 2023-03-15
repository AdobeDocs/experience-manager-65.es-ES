---
title: Aplicación de zona protegida inicial
seo-title: Initial Sandbox Application
description: Creación de plantillas, componentes y scripts
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

# Aplicación de zona protegida inicial {#initial-sandbox-application}

En esta sección, creará lo siguiente:

* El **[plantilla](#createthepagetemplate)** que se utilizará para crear páginas de contenido en el sitio web de ejemplo.
* El **[componente y script](#create-the-template-s-rendering-component)** que se utilizará para procesar las páginas del sitio web.

## Creación de la plantilla de contenido {#create-the-content-template}

Una plantilla define el contenido predeterminado de una nueva página. Los sitios web complejos pueden utilizar varias plantillas para crear los distintos tipos de páginas del sitio. Además, el conjunto de plantillas puede convertirse en un modelo utilizado para implementar cambios en un clúster de servidores.

En este ejercicio, todas las páginas se basan en una plantilla simple.

1. En el panel del explorador del CRXDE Lite:

   * Seleccione `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Crear]** > **[!UICONTROL Crear plantilla]**

1. En el cuadro de diálogo Crear plantilla, escriba los siguientes valores y haga clic en **[!UICONTROL Siguiente]**:

   * Etiqueta: `playpage`
   * Título: `An SCF Sandbox Play Template`
   * Descripción: `An SCF Sandbox template for play pages`
   * Tipo de medio: `an-scf-sandbox/components/playpage`
   * Clasificación: &lt;leave as=&quot;&quot; default=&quot;&quot;>

   Label se utiliza para el nombre del nodo.

   El Tipo de recurso aparece en la `playpage`El nodo jcr:content de como propiedad `sling:resourceType`. Identifica el componente (recurso) que procesa el contenido cuando un explorador lo solicita.

   En este caso, todas las páginas creadas con `playpage` Las plantillas son procesadas por `an-scf-sandbox/components/playpage` componente. Por convención, la ruta al componente es relativa, lo que permite a Sling buscar el recurso primero en la `/apps` y, si no se encuentra, en la carpeta `/libs` carpeta.

   ![create-content-template](assets/create-content-template-1.png)

1. Si utiliza copiar/pegar, asegúrese de que el valor del Tipo de recurso no tenga espacios iniciales o finales.

   Haga clic en **[!UICONTROL Siguiente]**.

1. &quot;Rutas permitidas&quot; se refiere a las rutas de las páginas que utilizan esta plantilla, de modo que la plantilla se enumera para la variable **[!UICONTROL Nueva página]** diálogo.

   Para añadir una ruta, haga clic en el botón &quot;+&quot; `+` y tipo `/content(/.&ast;)?` en el cuadro de texto que aparece. Si utiliza copiar/pegar, asegúrese de que no haya espacios iniciales o finales.

   Nota: El valor de la propiedad de ruta permitida es un *expresión regular*. Las páginas de contenido que tienen una ruta que coincide con la expresión pueden utilizar la plantilla. En este caso, la expresión regular coincide con la ruta del **/content** y todas sus subpáginas.

   Cuando un autor crea una página a continuación `/content`, el `playpage` La plantilla titulada &quot;An SCF Sandbox Page Template&quot; aparece en una lista de plantillas disponibles para su uso.

   Una vez creada la página raíz a partir de la plantilla, el acceso a la plantilla se podría restringir a este sitio web modificando la propiedad para incluir la ruta raíz en la expresión regular, es decir.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. Haga clic en **[!UICONTROL Siguiente]**.

   Clic **[!UICONTROL Siguiente]** en el **[!UICONTROL Principales permitidos]** panel.

   Clic **[!UICONTROL Siguiente]** en el **[!UICONTROL Elementos secundarios permitidos]** paneles.

   Haga clic en **[!UICONTROL Aceptar]**.

1. Una vez que haga clic en Aceptar y termine de crear la plantilla, verá que se muestran triángulos rojos en las esquinas de los valores de la pestaña Propiedades para la nueva plantilla `playpage` plantilla. Estos triángulos rojos indican ediciones que no se han guardado.

   Clic **[!UICONTROL Guardar todo]** para guardar la nueva plantilla en el repositorio.

   ![verify-content-template](assets/verify-content-template.png)

### Crear el componente de procesamiento de la plantilla {#create-the-template-s-rendering-component}

Cree el *componente* que define el contenido y procesa cualquier página creada en función de la variable [plantilla de página de reproducción](#createthepagetemplate).

1. En CRXDE Lite, haga clic con el botón derecho **`/apps/an-scf-sandbox/components`** y haga clic en **[!UICONTROL Crear > Componente]**.
1. Estableciendo el nombre del nodo (Label) en *página de reproducción*, la ruta al componente es

   `/apps/an-scf-sandbox/components/playpage`

   que corresponde al Tipo de recurso de la plantilla de página de reproducción (opcionalmente menos el inicial) **`/apps/`** parte de la ruta).

   En el **[!UICONTROL Crear componente]** , escriba los siguientes valores de propiedad:

   * Etiqueta: **página de reproducción**
   * Título: **Un componente de reproducción de zona protegida SCF**
   * Descripción: **Este es el componente que procesa el contenido de una página de zona protegida SCF.**
   * Supertipo: *&lt;leave blank=&quot;&quot;>*
   * Grupo: *&lt;leave blank=&quot;&quot;>*

   ![create-template-component](assets/create-template-component.png)

1. Clic **[!UICONTROL Siguiente]** hasta que **[!UICONTROL Elementos secundarios permitidos]** aparece el panel del cuadro de diálogo:

   * Haga clic en **[!UICONTROL Aceptar]**.
   * Haga clic en **[!UICONTROL Guardar todo]**.

1. Compruebe que la ruta al componente y el resourceType de la plantilla coincidan.

   >[!CAUTION]
   >
   >La correspondencia entre la ruta al componente de página de reproducción y la propiedad sling:resourceType de la plantilla de página de reproducción es crucial para el correcto funcionamiento del sitio web.

   ![verify-template-component](assets/verify-template-component.png)
