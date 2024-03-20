---
title: Crear y organizar páginas
description: AEM En esta sección se describe cómo crear y administrar páginas con las que se puede crear contenido para después crear contenido en las mismas.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: bd2636d1-6f13-4c6c-b8cd-3bed9e83a101
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 16%

---

# Crear y organizar páginas{#creating-and-organizing-pages}

En esta sección se describe cómo crear y administrar páginas con Adobe Experience Manager AEM () para poder [crear contenido](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md) en esas páginas.

>[!NOTE]
>
>Su cuenta necesita el [derechos de acceso adecuados](/help/sites-administering/security.md) y [permissions](/help/sites-administering/security.md#permissions) para realizar acciones en páginas como, por ejemplo, crear, copiar, mover, editar o eliminar.
>
>Si se producen problemas, le sugerimos que se ponga en contacto con el administrador del sistema.

## Organizar el sitio web {#organizing-your-website}

AEM Como creador, debe organizar el sitio web dentro de la organización de la creación de. Esto implica crear y asignar un nombre a las páginas de contenido para que:

* puede encontrarlos fácilmente en el entorno de creación
* los visitantes del sitio pueden explorarlas fácilmente en el entorno de publicación

También puede usar [carpetas](#creating-a-new-folder) para organizar el contenido.

La estructura de un sitio web se puede considerar como una *estructura de árbol* que contiene las páginas de contenido. Los nombres de estas páginas de contenido se utilizan para formar las direcciones URL, mientras que el título se muestra cuando se visualiza el contenido de la página.

A continuación se muestra un extracto del sitio de Geometrixx; donde, por ejemplo, la variable `Triangle` Se accederá a esta página:

* Entorno de creación

  `http://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

* Entorno de publicación

  `http://localhost:4503/content/geometrixx/en/products/triangle.html`

  Según la configuración de la instancia, utilice `/content` puede ser opcional en el entorno de publicación.

```xml
  /content
    /geometrixx
      /en
        /toolbar...
        /products
          /triangle
            /overview
            /features
          /square...
          /circle...
          /...
        /...
      /fr...
      /de...
      /es...
      /...
    /...
```

Esta estructura se puede ver desde la consola Sitios web, que puede utilizar para [navegar por la estructura de árbol](/help/sites-classic-ui-authoring/author-env-basic-handling.md#main-pars-text-15).

![chlimage_1-151](assets/chlimage_1-151.png)

### Convenciones de nomenclatura de páginas {#page-naming-conventions}

Al crear una página, hay dos campos de claves:

* **[Título](#title)**:

   * Se muestra al usuario en la consola, en la parte superior del contenido de la página al editar. 
   * Este campo es obligatorio.

* **[Nombre](#name)**:

   * Se usa para generar la URI.
   * La entrada del usuario para este campo es opcional. Si no se especifica, el nombre se obtiene a partir del título.

AEM Al crear una página, se debe hacer lo siguiente [valida el nombre de página según las convenciones](/help/sites-developing/naming-conventions.md) AEM impuesta por el y el JCR.

La implementación y la lista de caracteres permitidos difieren ligeramente según la interfaz de usuario (es más extensa para la interfaz con capacidad táctil), pero el mínimo permitido es:

* de &#39;a&#39; a &#39;z&#39;
* De &#39;A&#39; a &#39;Z&#39;
* De &#39;0&#39; a &#39;9&#39;
* _ (guion bajo)
* `-` (guion/signo menos)

Utilice únicamente estos caracteres si desea asegurarse de que se aceptan o utilizan (si necesita obtener todos los detalles de todos los caracteres permitidos, consulte ) [las convenciones de nomenclatura](/help/sites-developing/naming-conventions.md)).

#### Título {#title}

Si proporciona solo una página **Título** AEM al crear una página, se deriva la página de forma de **Nombre** de esta cadena y [valide el nombre según las convenciones](/help/sites-developing/naming-conventions.md) AEM impuesta por el y el JCR. En ambas IU, una **Título** se aceptará el campo que contenga caracteres no válidos, pero los caracteres no válidos se sustituirán en el nombre derivado. Por ejemplo:

| Título | Nombre derivado |
|---|---|
| Schön | schoen.html |
| SC%&amp;&amp;ast;ç+ | sc---c-.html |

#### Nombre {#name}

Si proporciona una página **Nombre** AEM al crear una página, se debe hacer lo siguiente [valida el nombre según las convenciones](/help/sites-developing/naming-conventions.md) AEM impuesta por el y el JCR.

En la IU clásica puede **no puede introducir caracteres no válidos** en el **Nombre** field.

>[!NOTE]
>En la IU táctil puede hacer lo siguiente **no se pueden enviar caracteres no válidos** en el **Nombre** field. AEM Cuando detecta caracteres no válidos, se resalta el campo y se muestra un mensaje explicativo para indicar los caracteres que deben eliminarse o reemplazarse.

>[!NOTE]
>
>Evite utilizar un código de dos letras como se define en la norma ISO-639-1, a menos que sea la raíz de un idioma.
>
>Consulte [Preparación de contenido para su traducción](/help/sites-administering/tc-prep.md) para obtener más información.

### Plantillas {#templates}

En AEM, una plantilla especifica un tipo de página especializado. Se utiliza una plantilla como base para cualquier página nueva que se cree.

La plantilla define la estructura de una página, incluida una imagen en miniatura y otras propiedades. Por ejemplo, puede tener plantillas independientes para páginas de productos, mapas del sitio e información de contacto. Las plantillas están formadas por [componentes](#components).

AEM incluye varias plantillas listas para usar de forma predeterminada. Las plantillas ofrecidas dependen del sitio web individual y la información que se proporcione (al crear la nueva página) depende de la interfaz de usuario que se utilice. Los campos principales son:

* **Título** El título se muestra en la página web resultante.

* **Nombre** Se utiliza al dar nombre a la página.

* **Plantilla** Una lista de plantillas disponibles para usar durante la generación de la nueva página.

### Componentes {#components}

Componentes son los elementos ofrecidos por AEM para que pueda añadir tipos de contenido específicos. AEM El paquete incluye una serie de componentes listos para usar que proporcionan una amplia funcionalidad, entre los que se incluyen:

* Texto
* Imagen
* Presentación de diapositivas
* Vídeo
* muchos más

Una vez que haya creado y abierto una página, puede [añadir contenido mediante los componentes](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#insertinganewparagraph), disponible en el [compinche](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick).

## Administrar páginas {#managing-pages}

### Creación de una nueva página {#creating-a-new-page}

A menos que se hayan creado todas las páginas por adelantado, antes de empezar a crear contenido, debe crear una página:

1. Desde el **Sitios web** , seleccione el nivel en el que desea crear una página.

   En el ejemplo siguiente, se crea una página en el nivel **Productos** - se muestra en el panel izquierdo; el panel derecho muestra páginas que ya existen en el nivel inferior **Productos**.

   ![screen_shot_2012-02-15at114413am](assets/screen_shot_2012-02-15at114413am.png)

1. En el **Nuevo...** (haga clic en la flecha situada junto a **Nuevo...**), seleccione **Nueva página...**. El **Crear página** se abre.

   Clic **Nuevo...** también actúa como un acceso directo a la variable **Nueva página...** opción.

1. El **Crear página** El cuadro de diálogo le permite:

   * Proporcione un **Título**; esto se muestra al usuario.
   * Proporcione un **Nombre**; se utiliza para generar el URI. Si no se especifica, el nombre se derivará del título.

      * Si proporciona una página **Nombre** AEM al crear una página, se debe hacer lo siguiente [valida el nombre según las convenciones](/help/sites-developing/naming-conventions.md) AEM impuesta por los JCR y los de la.
      * En la IU clásica puede: **no puede introducir caracteres no válidos** en el **Nombre** field.

   * Haga clic en la plantilla que desee utilizar para crear la nueva página.

     La plantilla se utiliza como base para la nueva página; por ejemplo, para determinar el diseño básico de una página de contenido.

   >[!NOTE]
   >
   >Consulte [Convenciones de asignación de nombres a páginas](#page-naming-conventions).

   La información mínima necesaria para crear una página es la siguiente **Título** y la plantilla requerida.

   ![screen_shot_2012-02-15at114845am](assets/screen_shot_2012-02-15at114845am.png)

   >[!NOTE]
   >
   >Si desea utilizar caracteres Unicode en las direcciones URL, establezca el Alias ( `sling:alias`) propiedad ([propiedades de página](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)).

1. Clic **Crear** para crear la página. Volverá a la **Sitios web** consola en la que puede ver una entrada para la nueva página.

   La consola proporciona información sobre la página (por ejemplo, cuándo se editó por última vez y quién la modificó), que se actualiza según sea necesario.

   >[!NOTE]
   >
   >También puede crear una página cuando esté editando una página existente. Uso de **Crear página secundaria** desde el **Página** de la barra de tareas crea una página directamente debajo de la página que se está editando.

### Abrir una página para su edición {#opening-a-page-for-editing}

Puede abrir la página para que [editado](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#editing-a-component-content-and-properties) mediante uno de varios métodos:

* Desde **Sitios web** consola, puede **doble clic** Abra la entrada de página para abrirla y editarla.

* Desde **Sitios web** consola, puede **clic con el botón derecho** (menú contextual) Seleccione el elemento de página y, a continuación, seleccione **Abrir** en el menú.

* Una vez abierta una página, puede desplazarse a otras páginas del sitio (para editarlas) haciendo clic en los hipervínculos.

### Copiar y pegar una página    {#copying-and-pasting-a-page}

Al copiar, puede copiar lo siguiente:

* una sola página
* una página junto con todas las subpáginas

1. Desde el **Sitios web** , seleccione la página que desee copiar.

   >[!NOTE]
   >
   >En este momento, no es relevante si desea copiar una sola página o las subpáginas subyacentes.

1. Clic **Copiar**.

1. Vaya a la nueva ubicación y haga clic en:

   * **Pegar** : para pegar la página junto con todas las subpáginas
   * **Mayús + Pegar** - para pegar solo la página seleccionada

   Las páginas se pegan en la nueva ubicación.

   >[!NOTE]
   >
   >El nombre de página puede ajustarse automáticamente si una página existente ya tiene el mismo nombre.

   >[!NOTE]
   >
   >También puede utilizar **Copiar página** desde el **Página** pestaña de la barra de tareas. Se abrirá un cuadro de diálogo en el que puede especificar el destino, etc.

### Mover página o cambiarle el nombre {#moving-or-renaming-page}

>[!NOTE]
>
>Cambiar el nombre de una página también está sujeto a las [Convenciones de nomenclatura de páginas](#page-naming-conventions) al especificar el nuevo nombre de página.

El procedimiento para mover o cambiar el nombre de una página es el mismo. Con la misma acción puede:

* mover una página a una nueva ubicación
* cambiar el nombre de una página en la misma ubicación
* mover una página a una nueva ubicación y cambiarle el nombre simultáneamente

AEM le ofrece la funcionalidad de actualizar los vínculos internos a la página que se está moviendo o cambiando de nombre. Esto se puede hacer página por página para proporcionar una flexibilidad total.

Para mover o cambiar el nombre de una página:

1. Existen varios métodos para activar un movimiento:

   * Desde el **Sitios web** consola, haga clic en para seleccionar la página y, a continuación, seleccione **Mover...**
   * Desde el **Sitios web** consola, también puede seleccionar el elemento de página y, a continuación, **clic con el botón derecho** y seleccione **Mover...**
   * Al editar una página, puede seleccionar **Mover página** desde el **Página** pestaña de la barra de tareas.

1. El **Mover** se abre la ventana; aquí puede especificar una nueva ubicación, un nuevo nombre para la página o ambos.

   ![screen_shot_2012-02-15at121336pm](assets/screen_shot_2012-02-15at121336pm.png)

   La página también enumera todas las páginas que hacen referencia a la página que se está moviendo. Según el estado de la página de referencia, es posible que pueda ajustar esos vínculos en las páginas o volver a publicarlas.

1. Rellene los campos siguientes, según corresponda:

   * **Destino**

     Utilice el mapa del sitio (disponible a través del selector desplegable) para seleccionar la ubicación a la que se debe mover la página.

     Si solo va a cambiar el nombre de la página, ignore este campo.

   * **Mover**

     Especifique la página que desea mover: normalmente se rellena de forma predeterminada, según cómo y dónde haya iniciado la acción de mover.

   * **Cambiar nombre a**

     La etiqueta de la página actual se muestra de forma predeterminada. Especifique la nueva etiqueta de página, si es necesario.

   * **Ajuste**

     AEM Actualice los vínculos de la página enumerada que apunten a la página desplazada: por ejemplo, si la página A tiene vínculos a la página B, ajusta los vínculos de la página A en caso de que mueva la página B, por ejemplo, para la página B.

     Se puede seleccionar o deseleccionar para cada página de referencia individual.

   * **Volver a publicar**

     Volver a publicar la página de referencia; de nuevo, esto se puede seleccionar para cada página individual.

   >[!NOTE]
   >
   >Si la página ya estaba activada, al mover la página se desactivará automáticamente. De forma predeterminada, se reactivará cuando se complete el movimiento, pero esto puede cambiar desmarcando la opción **Volver a publicar** para la página en el **Mover** ventana.

1. Clic **Mover**. Se requiere confirmación. Clic **OK** para confirmar.

   >[!NOTE]
   >
   >El título de la página no se actualizará.

### Eliminar una página {#deleting-a-page}

1. Puede eliminar una página desde varias ubicaciones:

   * Dentro de **Sitios web** consola, haga clic en para seleccionar la página, haga clic con el botón derecho y seleccione **Eliminar** en el menú resultante.
   * Dentro de **Sitios web** consola, haga clic en para seleccionar la página y, a continuación, seleccione **Eliminar** en el menú de la barra de herramientas.
   * En la barra de tareas utilice **Página** pestaña para seleccionar **Eliminar página** : esto elimina la página que está abierta actualmente.

1. Después de seleccionar eliminar una página, debe confirmar la solicitud, ya que la acción no se puede deshacer.

   >[!NOTE]
   >
   >Después de la eliminación, si la página se ha publicado, puede restaurar la versión más reciente (o una específica), pero es posible que no tenga exactamente el mismo contenido que la última versión si se han realizado más modificaciones. Consulte [Cómo Restaurar Páginas](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoringpages) para obtener más información.

>[!NOTE]
>
>Si una página ya está activada, se desactiva automáticamente antes de la eliminación.

### Bloquear una página   {#locking-a-page}

Puede [bloquear/desbloquear una página](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#locking-a-page) desde una consola o al editar una página individual. La información sobre las páginas bloqueadas también se muestra en ambas ubicaciones.

### Crear una nueva carpeta {#creating-a-new-folder}

>[!NOTE]
>
>Las carpetas también están sujetas a las [Convenciones de asignación de nombres a páginas](#page-naming-conventions) al especificar el nuevo nombre de carpeta.

1. Abra el **Sitios web** y vaya a la ubicación requerida.
1. En el **Nuevo...** (haga clic en la flecha situada junto a **Nuevo...**), seleccione **Nueva carpeta...**.
1. El **Crear carpeta** se abre el cuadro de diálogo. Aquí puede indicar el **Nombre** y el **Título**:

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. Seleccione **Crear** para crear la carpeta.
