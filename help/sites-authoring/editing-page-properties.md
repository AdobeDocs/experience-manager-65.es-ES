---
title: 'Edición de las propiedades de página  '
seo-title: 'Edición de las propiedades de página  '
description: Permite definir las propiedades de una página
seo-description: Permite definir las propiedades de una página
uuid: d3a2183b-8082-4cfc-aeed-26facbf3f3e6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1e9dd0d7-209a-4989-b66b-bca0d04b437a
docset: aem65
translation-type: tm+mt
source-git-commit: 7fed51b68c626b54565b9120f69229872946016f
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 85%

---


# Edición de las propiedades de página{#editing-page-properties}

Puede definir las propiedades para una página. Estas pueden variar en función de la naturaleza de la página. Por ejemplo, algunas páginas pueden estar conectadas a una Live Copy. Otras no lo están y la información de la Live Copy está disponible según corresponda.

## Propiedades de página {#page-properties}

Las propiedades se distribuyen entre varias pestañas.

### Básico {#basic}

* **Título**

   El título de la página se muestra en varias ubicaciones. Por ejemplo, la lista de la pestaña **Sitios web** y las vistas de lista o tarjeta **Sitios**.

   Es un campo obligatorio.

* **Etiquetas**

   Aquí puede agregar o quitar etiquetas de la página al actualizar la lista en el cuadro de diálogo de selección:

   * Tras seleccionar una etiqueta, esta se muestra bajo el cuadro de selección. Para eliminar una etiqueta de esta lista, utilice la x.
   * Se puede especificar una etiqueta completamente nueva si se escribe el nombre en un cuadro de selección vacío.

      * La nueva etiqueta se creará cuando pulse Intro.
      * A continuación, la nueva etiqueta se mostrará con una pequeña estrella a la derecha que indicará que es una etiqueta nueva.
   * Con la función de lista desplegable, puede seleccionar etiquetas existentes.
   * Aparece una x cuando pasa el puntero sobre una entrada de etiqueta en el cuadro de selección; esto puede usarse para quitar esa etiqueta para esta página.

   Para obtener más información sobre las etiquetas, consulte [Utilizar etiquetas](/help/sites-authoring/tags.md).

* **Ocultar en navegación**

   Indica si se muestra o se oculta la página en la navegación por páginas del sitio resultante.

* **Marca**

   Aplique una identidad de marca uniforme en todas las páginas agregando una indicación de marca a cada título de página. Esta funcionalidad requiere el uso del componente Página de la versión 2.14.0 o posterior de los [Componentes principales.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)

   * **Anular** : marque esta opción para definir la indicación de marca en esta página.
      * El valor será heredado por cualquier página secundaria a menos que también tengan sus valores **Override** establecidos.
   * **Valor**  de anulación: el texto de la indicación de marca que se va a anexar al título de la página.
      * El valor se anexa al título de la página después de un carácter de barra vertical, como &quot;Ciclo de la Toscana&quot; | Siempre listo para la WKND&quot;
* **Título de página**

   Un título que se usará en la página. Normalmente, lo utilizan los componentes del título. Si la opción se deja vacía, se utilizará el **Título**.

* **Título de navegación**

   Puede especificar un título diferente para utilizarlo en la navegación (por ejemplo, si requiere un título más conciso). Si la opción se deja vacía, se utilizará el **Título**.

* **Subtítulo**

   Un subtítulo para usar en la página.

* **Descripción**

   Aquí puede indicar una descripción de la página, su propósito o cualquier otro detalle.

* **Tiempo de activación**

   La fecha y hora a la que se activará la página publicada. Cuando se publique, esta página se mantendrá inactiva hasta la hora especificada.

   Deje vacíos estos campos para las páginas que desee publicar inmediatamente (el caso normal).

* **Tiempo de inactividad**

   La hora a la que se desactivará la página publicada.

   Vuelva a dejar estos campos vacíos para una acción inmediata.

* **URL de vanidad**

   Permite introducir una URL de vanidad para esta página, que le permitirá disponer de una URL más corta y/o descriptiva.

   Por ejemplo: si la URL de vanidad está configurada en `welcome`en la página identificada por la ruta `/v1.0/startpage`para el sitio Web `http://example.com,` entonces `http://example.com/welcome`sería la URL de vanidad de `http://example.com/content/v1.0/startpage`

   >[!CAUTION]
   >
   >URL de vanidad:
   >
   >* Deben ser únicas, por lo que tiene que asegurarse de que ninguna otra página utilice este valor.
   >* No admiten patrones regex.
   >* No debe configurarse en una página existente.


   También debe configurar Dispatcher para habilitar el acceso a las direcciones URL personales. Consulte [Habilitación del acceso a direcciones URL de vanidad](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls) para obtener más detalles.

* **Redirigir URL de vanidad**

   Indica si desea que la página use la URL de vanidad.

### Avanzado  {#advanced}

* **Idioma**

   El idioma de la página.

* **Raíz del idioma**

   Si la página es la raíz de una copia en un idioma, es necesario marcar esta opción.

* **Redirigir**

   Indique la página a la cual esta página debería redirigirse automáticamente.

* **Diseño**

   Indique el [diseño](/help/sites-developing/designer.md) que se usará para esta página.

* **Alias**

   Especifique un alias para usar con esta página.

   >[!NOTE]
   >
   >Alias establece la propiedad `sling:alias` para definir un nombre de alias para el recurso (esto solo afecta al recurso, no a la ruta).
   >
   >Por ejemplo: si define un alias de `latin-lang` para el nodo `/content/we-retail/spanish`, se puede acceder a esta página mediante `/content/we-retail/latin-language`.
   >
   >Para obtener más información, consulte [Nombres de páginas localizados en Optimizaciones para la administración de direcciones URL y SEO](/help/managing/seo-and-url-management.md#localized-page-names).

* **Heredado de &lt;*path*>**

   Indica si la página se ha heredado y dónde.

* **Configuración de nube**

   La ruta de acceso de la configuración.

* **Plantillas permitidas**

   [Defina la lista de plantillas disponibles](/help/sites-authoring/templates.md#allowingatemplate) dentro de esta rama secundaria.

* **Habilitar** (requisito de autenticación)

   Habilite (o deshabilite) el uso de la autenticación para acceder a la página.

   >[!NOTE]
   >
   >Los grupos de usuarios cerrados para la página se definen en la pestaña **[Permisos](/help/sites-authoring/editing-page-properties.md#permissions)**.

   >[!CAUTION]
   >
   >La ficha **[Permisos](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** permite editar configuraciones de CUG según la presencia de la mezcla `granite:AuthenticationRequired`. Si los permisos de página se configuran usando configuraciones de CUG obsoletas, según la presencia de la propiedad `cq:cugEnabled`, se mostrará un mensaje de advertencia en **Requisito de autenticación** y la opción no será editable, ni tampoco se podrán editar los [Permisos](/help/sites-authoring/editing-page-properties.md#permissions).
   >
   >
   >En ese caso, los permisos de CUG se deben editar en la [IU clásica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

* **Página de inicio de sesión**

   La página que se usará para iniciar sesión.

* **Configuración de exportación**

   Especificar una configuración de exportación.

### Miniatura     {#thumbnail}

Muestra la imagen de la página en miniatura. Puede hacer lo siguiente:

* **Generar vista previa**

   Genere una vista previa de la página para utilizarla como miniatura.

* **Cargar imagen**

   Cargue una imagen para utilizarla como miniatura.

* **Seleccionar imagen**

   Seleccione un recurso existente para utilizarlo como miniatura.

* **Revertir**

   Esta opción está disponible después de realizar un cambio en la miniatura. Si no desea mantener el cambio, puede revertirlo antes de guardar.

### Redes sociales {#social-media}

* **Compartir en redes sociales**

   Define las opciones de uso compartido disponibles en la página. Expone las opciones disponibles para el [componente principal de compartición](https://helpx.adobe.com/experience-manager/core-components/using/sharing.html).

   * **Permitir al usuario que comparta en Facebook**
   * **Permitir al usuario que comparta en Pinterest**
   * **Variación de XF preferida**
Define la variación de fragmentos de la experiencia que se utiliza para generar metadatos para la página.

### Cloud Services{#cloud-services}

* **Cloud Services**

   Defina propiedades para [servicios de nube](/help/sites-developing/extending-cloud-config.md).

### Personalización {#personalization}

* **Configuración de ContextHub**

   Seleccione la [configuración de ContextHub](/help/sites-developing/ch-configuring.md) y la [ruta de acceso de los segmentos](/help/sites-administering/segmentation.md).

* **Configuración de ámbito**

   Seleccione una [marca para especificar un ámbito de objetivo](/help/sites-authoring/target-adobe-campaign.md).

   >[!NOTE]
   >Esta opción requiere una cuenta de usuario en el grupo `Target Adminstrators`.

### Permisos     {#permissions}

* **Permisos**

   En esta ficha puede:

   * [Agregar permisos](/help/sites-administering/user-group-ac-admin.md)
   * [Editar grupo de usuarios cerrado](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * Ver los [permisos efectivos](/help/sites-administering/user-group-ac-admin.md)
   >[!CAUTION]
   >
   >La ficha **Permisos** permite editar configuraciones de CUG según la presencia de la mezcla `granite:AuthenticationRequired`. Si los permisos de la página se configuran mediante ajustes de CUG obsoletas, dependiendo de la presencia de la propiedad `cq:cugEnabled`, se mostrará un mensaje de advertencia y los permisos de CUG no se podrán editar, al igual que el Requisito de autenticación de la ficha [Avanzado](/help/sites-authoring/editing-page-properties.md#advanced).
   >
   >
   >En ese caso, los permisos de CUG se deben editar en la [IU clásica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

   >[!NOTE]
   >
   >La ficha Permisos no permite la creación de grupos CUG vacíos, lo cual puede resultar útil como forma sencilla de denegar el acceso de cada usuario. Para esto, es necesario utilizar CRX Explorer. Consulte el documento [Administración de derechos de usuario, grupo y acceso](/help/sites-administering/user-group-ac-admin.md) para obtener más información.

### Modelo {#blueprint}

* **Modelo**

   Defina propiedades para una página de modelo en un entorno de [administración de varios sitios](/help/sites-administering/msm.md). Controla las circunstancias dentro de las que se propagarán las modificaciones a Live Copy.

### Live Copy     {#live-copy}

* **Live Copy**

   Defina propiedades para una página Live Copy en un entorno de [administración de varios sitios](/help/sites-administering/msm.md). Controla las circunstancias dentro de las cuales se propagarán las modificaciones desde el modelo.

### Estructura del sitio     {#site-structure}

* Proporcione vínculos a páginas que proporcionan funcionalidad para todo el sitio, como **Página de suscripción**, **Página sin conexión**, entre otros. 

## Edición de las propiedades de página {#editing-page-properties-1}

Puede definir propiedades de página:

* Desde la consola **Sitios:**

   * [Creando una página nueva](/help/sites-authoring/managing-pages.md#creating-a-new-page) (un subconjunto de las propiedades)

   * Pulsando o haciendo clic en **Propiedades**

      * Para una sola página
      * Para varias páginas (solo se pueden editar en masa un subconjunto de las propiedades)

* Desde el editor de páginas:

   * Utilizando **Información de página** (a continuación, **Abrir propiedades**)

### Desde la consola Sitios: página individual {#from-the-sites-console-single-page}

Tocando o haciendo clic en **Propiedades** para definir las propiedades de la página:

1. Mediante la consola **Sitios**, desplácese hasta la ubicación de la página para la que desee ver y editar las propiedades.

1. Seleccione la opción **Propiedades** de la página requerida mediante:

   * [Acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [Modo de selección](/help/sites-authoring/basic-handling.md#selectionmode)

   Las propiedades de página se mostrarán mediante las pestañas adecuadas.

1. Visualice o edite las propiedades según sea oportuno. 

1. A continuación, utilice **Guardar** para guardar las actualizaciones, seguido de **Cerrar** para volver a la consola.

### Al editar una página {#when-editing-a-page}

Al editar una página puede, utilizar **Información de página** para definir las propiedades de la página:

1. Abra la página para la que desee editar las propiedades.

1. Seleccione el icono **Información de página** para abrir el menú de selección:

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. Seleccione **Abrir propiedades** y se abrirá un cuadro de diálogo que le permitirá editar las propiedades, ordenadas por la ficha correspondiente. Los siguientes botones también están disponibles en la parte derecha de la barra de herramientas:

   * **Cancelar**
   * **Guardar y cerrar**

1. Utilice el botón **Guardar y cerrar** para guardar los cambios. 

### Desde la consola Sitios: varias páginas {#from-the-sites-console-multiple-pages}

Desde la consola **Sites** puede seleccionar varias páginas y luego utilizar **Ver propiedades** para ver o editar las propiedades de la página. Esto se conoce como edición masiva de propiedades de página.

>[!NOTE]
>
>La edición de propiedades por lotes también está disponible para los recursos. Se parece mucho, pero presenta algunos aspectos diferentes. Consulte [Edición de propiedades de varios recursos](/help/assets/metadata.md) para obtener más información.
>
>También dispone del [Editor por lotes](/help/sites-administering/bulk-editor.md), que le permite buscar contenido de varias páginas con GQL (Google Query Language) y, a continuación, editar el contenido directamente en el editor por lotes para luego guardar los cambios (en las páginas originales).

Puede seleccionar varias páginas para editarlas por lotes utilizando distintos métodos, como los siguientes:

* Mientras se desplaza por la consola **Sitios**
* Después de utilizar la opción **Buscar** para localizar un conjunto de páginas

![epp-01](assets/epp-01.png)

Después de seleccionar las páginas y hacer clic o pulsar en la opción **Propiedades**, se muestran las propiedades por lotes:

![epp-02](assets/epp-02.png)

Solo se pueden editar por lotes las páginas que:

* Comparten el mismo tipo de recurso.
* No forman parte de una Live Copy

   * Si alguna de las páginas está en una Live Copy, se mostrará un mensaje cuando se abran las propiedades. 

Cuando esté en la edición por lotes, podrá efectuar las siguientes acciones:

* **Ver**

   Mientras visualiza las Propiedades de página de varias páginas, puede ver:

   * Una lista de las páginas afectadas

      * Si lo desea, puede seleccionarlas o deseleccionarlas.
   * Pestañas

      * Las propiedades se ordenan en pestañas, al igual que cuando se visualizan las propiedades de una página.
   * Un subconjunto de propiedades

      * Se pueden ver las propiedades que están disponibles en todas las páginas seleccionadas (deben haberse marcado específicamente como disponibles para la edición por lotes).
      * Si reduce la selección de páginas a una sola página, se verán todas las propiedades.
   * Propiedades comunes con un valor común

      * En el modo Ver solo se muestran las propiedades con un valor común.
      * Cuando el campo admite varios valores (por ejemplo, etiquetas), los valores solo se mostrarán si *todos* son comunes. Si solo son comunes algunos de ellos, solo se mostrarán en el momento de editar.

   Cuando no existen propiedades con un valor común, se muestra un mensaje. 

* **Editar**

   Mientras edita las Propiedades de página de varias páginas:

   * Puede actualizar los valores en los campos disponibles.

      * Los nuevos valores se aplicarán a todas las páginas seleccionadas al activar **Listo**.
      * Si el campo admite varios valores (por ejemplo, Etiquetas), puede agregar un valor nuevo o eliminar un valor común.
   * Los campos que son comunes en las páginas, pero que tienen diferentes valores, se señalizarán con un valor especial; por ejemplo, el texto `<Mixed Entries>`. Se debe tener cuidado al editar estos campos para evitar la pérdida de datos.


>[!NOTE]
>
>El componente de página se puede configurar para especificar los campos disponibles para la edición por lotes. Consulte [Configuración de la página para editar las propiedades de página por lotes](/help/sites-developing/bulk-editing.md).
