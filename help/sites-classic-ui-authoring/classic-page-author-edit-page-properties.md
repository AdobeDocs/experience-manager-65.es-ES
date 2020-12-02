---
title: 'Edición de las propiedades de página  '
seo-title: 'Edición de las propiedades de página  '
description: Las propiedades de una página pueden variar en función de su naturaleza. Por ejemplo, algunas páginas pueden estar conectadas a una Live Copy. Otras no lo están y la información de la Live Copy está disponible según corresponda.
seo-description: Las propiedades de una página pueden variar en función de su naturaleza. Por ejemplo, algunas páginas pueden estar conectadas a una Live Copy. Otras no lo están y la información de la Live Copy está disponible según corresponda.
uuid: 63d37d1b-52da-489d-b02b-e8b3d17571d1
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 23768c73-ac64-4727-8313-160c8c131b05
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 96%

---


# Edición de las propiedades de página{#editing-page-properties}

Puede definir las propiedades para una página. Estas pueden variar en función de la naturaleza de la página. Por ejemplo, algunas páginas pueden estar conectadas a una Live Copy. Otras no lo están y la información de la Live Copy está disponible según corresponda.

## Propiedades de página {#page-properties}

Las propiedades se distribuyen entre varias pestañas:

### Básico {#basic}

* **Título**

   El título de la página se muestra en varias ubicaciones. Por ejemplo, la lista de la pestaña **Sitios web** y las vistas de lista o tarjeta **Sitios**.

   Es un campo obligatorio.

* **Etiquetas**

   Aquí puede agregar o quitar etiquetas de la página al actualizar la lista en el cuadro de diálogo de selección:

   * Tras seleccionar una etiqueta, esta se muestra bajo el cuadro de selección. Para eliminar una etiqueta de esta lista, utilice la x.
   * Se puede especificar una etiqueta completamente nueva si se escribe el nombre en un cuadro de selección vacío.

      La nueva etiqueta se creará cuando pulse Intro. A continuación, la nueva etiqueta se mostrará en un cuadro, con una pequeña estrella a la derecha que indicará que es una etiqueta nueva.

   * Con la función de lista desplegable, puede seleccionar etiquetas existentes.
   * Aparece una x cuando pasa el puntero sobre una entrada de etiqueta en el cuadro de selección; esto puede usarse para quitar esa etiqueta para esta página.

* **Ocultar en navegación**

   Un conmutador para indicar si la página se muestra o se oculta en el panel de navegación.

* **Título de página**

   Un título que se usará en la página.

* **Título de navegación**

   Puede especificar un título diferente para utilizarlo en la navegación (por ejemplo, si requiere un título más conciso). Si la opción se deja vacía, se utilizará el **Título**.

* **Subtítulo**

   Un subtítulo para usar en la página.

* **Descripción**

   Su descripción de la página, su propósito o cualquier otro detalle que quiera añadir.

* **Tiempo de activación**

   La fecha y hora a la que se activará la página publicada. Cuando se publique, esta página se mantendrá inactiva hasta la hora especificada.

   Deje vacíos estos campos para las páginas que desee publicar inmediatamente (el caso normal).

* **Tiempo de inactividad**

   La hora a la que se desactivará la página publicada.

   Nuevamente, deje vacíos estos campos para las páginas que desee publicar inmediatamente.

* **URL de vanidad**

   Permite especificar una URL de vanidad para esta página. Esta opción le permitirá crear URL más cortas y expresivas.

   Por ejemplo: si la URL de vanidad está configurada en w `elcome`a la página identificada por la ruta / `v1.0/startpage`para el sitio Web h `ttp://example.com,` entonces h `ttp://example.com/welcome`sería la URL de vanidad de h `ttp://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >URL de vanidad:
   >
   >* Deben ser únicas, por lo que tiene que asegurarse de que ninguna otra página utilice este valor.
   >* No admiten patrones regex.


* **Redirigir URL de vanidad**

   Indica si desea que la página use la URL de vanidad.

### Avanzado  {#advanced}

* **Idioma**

   El idioma de la página.

* **Redirigir**

   Indique la página a la cual esta página debería redirigirse automáticamente.

* **Diseño**

   Indique el [diseño](/help/sites-developing/designer.md) que se usará para esta página.

* **Alias**

   Especifique un alias para usar con esta página.

* **Habilitar grupo de usuarios cerrado**

   Habilita (o deshabilita) el uso de [grupos de usuarios cerrados](/help/sites-administering/cug.md) (CUG).

* **Página de inicio de sesión**

   La página que se usará para iniciar sesión.

* **Grupos admitidos**

   Grupos elegibles para iniciar sesión en el CUG.

* **Territorio**

   Nombre de territorio para el CUG.

* **Configuración de exportación**

   Especificar una configuración de exportación.

### Miniatura     {#thumbnail}

* **Miniatura de la página**

   Muestra la imagen de la página en miniatura. Puede hacer lo siguiente:

   * **Generar vista previa**

      Genere una vista previa de la página para utilizarla como miniatura.

   * **Cargar imagen**

      Cargue una imagen para utilizarla como miniatura.

### Cloud Services{#cloud-services}

* **Cloud Services**

   Defina propiedades para [servicios de nube](/help/sites-developing/extending-cloud-config.md).

### Personalización {#personalization}

* **Personalización**

   Seleccione una [marca para especificar un ámbito de objetivo](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

### Permisos    {#permissions}

* **Permisos** (IU táctil)

   Ver los [permisos en vigor y añadir permisos nuevos](/help/sites-administering/user-group-ac-admin.md).

### Modelo {#blueprint}

* **Modelo**

   Defina propiedades para una página de modelo en un entorno de [administración de varios sitios](/help/sites-administering/msm.md). Controla las circunstancias dentro de las que se propagarán las modificaciones a Live Copy.

### Live Copy     {#live-copy}

* **Live Copy**

   Defina propiedades para una página Live Copy en un entorno de [administración de varios sitios](/help/sites-administering/msm.md). Controla las circunstancias dentro de las cuales se propagarán las modificaciones desde el modelo.

### Estructura del sitio     {#site-structure}

* Proporcione vínculos a páginas que proporcionan funcionalidad para todo el sitio, como **Página de suscripción**, **Página sin conexión**, entre otros. 

## Edición de las propiedades de página {#editing-page-properties-2}

### Edición de las propiedades de una página específica {#editing-page-properties-for-a-specific-page}

Las Propiedades de página definen las diversas propiedades de la página, como los títulos, cuando aparecen el sitio web y otros.

1. Abra la página que desee editar.

1. En la barra de tareas, abra la ficha **Página** y, a continuación, seleccione **Propiedades de página...**

   Se abre un cuadro de diálogo con varias fichas.

1. Haga los cambios que necesite y haga clic en **Aceptar** para guardarlos.

