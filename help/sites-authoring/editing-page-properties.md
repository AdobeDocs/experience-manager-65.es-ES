---
title: Edición de propiedades de página de contenido
description: Definir las propiedades necesarias para una página.
uuid: d3a2183b-8082-4cfc-aeed-26facbf3f3e6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1e9dd0d7-209a-4989-b66b-bca0d04b437a
docset: aem65
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 62%

---

# Edición de las propiedades de página  {#editing-page-properties}

Puede definir las propiedades para una página. Estas pueden variar según la naturaleza de la página. Por ejemplo, algunas páginas pueden estar conectadas a una Live Copy, mientras que otras no lo están, y la información de la Live Copy estará disponible según corresponda.

## Propiedades de página {#page-properties}

Las propiedades se distribuyen entre varias pestañas.

### Básico {#basic}

* **Título**

  El título de la página se muestra en varias ubicaciones. Por ejemplo, la lista de la pestaña **Sitios web** y las vistas de lista o tarjeta **Sitios**.

  Este es un campo obligatorio.

* **Etiquetas**

  Aquí puede agregar o quitar etiquetas de la página al actualizar la lista en el cuadro de diálogo de selección:

   * Después de seleccionar una etiqueta, aparece debajo del cuadro de selección. Puede quitar una etiqueta de esta lista utilizando la x.
   * Se puede especificar una etiqueta completamente nueva si se escribe el nombre en un cuadro de selección vacío.

      * La nueva etiqueta se creará cuando pulse Intro.
      * La nueva etiqueta se mostrará con una pequeña estrella a la derecha que indicará que es una etiqueta nueva.

   * Con la funcionalidad desplegable puede seleccionar etiquetas existentes.
   * Aparece una x cuando pasa el ratón sobre una entrada de etiqueta en el cuadro de selección, que se puede utilizar para quitar esa etiqueta para esa página.

  Para obtener más información sobre las etiquetas, consulte [Uso de etiquetas](/help/sites-authoring/tags.md).

* **Ocultar en navegación**

  Indica si se muestra o se oculta la página en la navegación por páginas del sitio resultante.

* **Marca**

  Aplique una identidad de marca uniforme en todas las páginas adjuntando un slug de marca al título de cada página. Esta funcionalidad requiere el uso del componente de página de la versión 2.14.0 o posterior de los [Componentes principales.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)

   * **Sobrescribir**: marque para definir el slug de marca en esta página.
      * El valor lo heredará cualquier página secundaria a menos que también tenga valores establecidos de **Sobrescribir**.
   * **Sobrescribir valor**: el texto del slug de marca que se añadirá al título de la página.
      * El valor se anexa al título de la página después de un carácter de barra vertical como “Ciclismo en Toscana | Siempre listo para WKND”
* **Título de página**

  Título que se utilizará en la página. Normalmente se utiliza en los componentes de título. Si está vacío, se utilizará el **Título** de la página.

* **Título de navegación**

  Puede especificar un título independiente para utilizarlo en la navegación (por ejemplo, si desea algo más conciso). Si está vacío, la variable **Título** se utilizará.

* **Subtítulo**

  Un subtítulo para usar en la página.

* **Descripción**

  La descripción de la página, su propósito o cualquier otro detalle que desee agregar.

* **Tiempo de activación**

  La fecha y hora a las que se activará la página publicada. Cuando se publique, esta página se mantendrá inactiva hasta el momento especificado.

  Deje estos campos vacíos para las páginas que desee publicar inmediatamente (el escenario normal).

* **Tiempo de inactividad**

  Hora a la que se desactivará la página publicada.

  De nuevo, deje estos campos vacíos para una acción inmediata.

* **URL mnemónica**

  Permite introducir una URL de vanidad para esta página, que puede permitirle tener una URL más corta o expresiva.

  Por ejemplo, si la URL de vanidad está configurada en `welcome`a la página identificada por la ruta `/v1.0/startpage`para el sitio web `http://example.com,` entonces `http://example.com/welcome`sería la URL de vanidad de `http://example.com/content/v1.0/startpage`

  >[!CAUTION]
  >
  >URL de vanidad:
  >
  >* Debe ser única, por lo que debe asegurarse de que ninguna otra página utilice ese valor.
  >* No admiten patrones regex.
  >* No debe configurarse en una página existente.
  >

  También debe configurar Dispatcher para habilitar el acceso a las URL de vanidad. Consulte [Habilitar el acceso a las URL de vanidad](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-access-to-vanity-urls-vanity-urls) para obtener más información.

* **Redirigir URL de vanidad**

  Indica si desea que la página use la URL de vanidad.

### Avanzado  {#advanced}

* **Idioma**

  El idioma de la página.

* **Raíz del idioma**

  Si la página es la raíz de una copia en un idioma, es necesario marcar esta opción.

* **Redirigir**

  Indique la página a la que esta página debe redirigirse automáticamente.

* **Design**

  Indique el [diseño](/help/sites-developing/designer.md) para utilizar en esta página.

* **Alias**

  Especifique un alias para utilizarlo con esta página.

   * Por ejemplo, si define un alias de `private` para la página `/content/wknd/us/en/magazine/members-only`, se puede acceder a esta página también mediante `/content/wknd/us/en/magazine/private`
   * La creación de un alias establece la propiedad `sling:alias` en el nodo de página, lo que solo afecta al recurso, no a la ruta del repositorio.
   * Las páginas a las que se accede mediante alias en el editor no se pueden publicar. Las [Opciones de publicación](/help/sites-authoring/publishing-pages.md) del editor solo están disponibles para las páginas a las que se accede a través de sus rutas reales.
   * Para obtener más información, consulte [Nombres de páginas localizadas en Prácticas recomendadas para la administración de direcciones URL y SEO](/help/managing/seo-and-url-management.md#localized-page-names).

* **Heredado de &lt;*ruta*>**

  Indica si la página se hereda. y de dónde.

* **Configuración de nube**

  La ruta a la configuración.

* **Plantillas permitidas**

  [Defina la lista de plantillas disponibles](/help/sites-authoring/templates.md#allowingatemplate) dentro de esta subrama.

* **Activar** (Requisito de autenticación)

  Habilite (o deshabilite) el uso de la autenticación para acceder a la página.

  >[!NOTE]
  >
  >Los grupos de usuarios cerrados para la página se definen en la pestaña **[Permisos](/help/sites-authoring/editing-page-properties.md#permissions)**.

  >[!CAUTION]
  >
  >El **[Permisos](/help/sites-authoring/editing-page-properties.md#main-pars-procedure-949394300)** permite editar las configuraciones de CUG en función de la presencia del `granite:AuthenticationRequired` mixin. Si los permisos de página se configuran utilizando configuraciones de CUG obsoletas, según la presencia de `cq:cugEnabled` propiedad, se mostrará un mensaje de advertencia en **Requisito de autenticación** y la opción no será editable, como tampoco lo hará la variable [Permisos](/help/sites-authoring/editing-page-properties.md#permissions) ser editable.
  >
  >
  >En tal caso, los permisos de CUG deben editarse en la variable [IU clásica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

* **Página de inicio de sesión**

  La página que se utilizará para iniciar sesión.

* **Configuración de exportación**

  Especifique una configuración de exportación.

### Miniatura    {#thumbnail}

Muestra la miniatura de la página. Puede hacer lo siguiente:

* **Generar previsualización**

  Genere una previsualización de la página para utilizarla como miniatura.

* **Cargar imagen**

  Cargue una imagen para utilizarla como miniatura.

* **Seleccionar imagen**

  Seleccione un recurso existente para utilizarlo como miniatura.

* **Revertir**

  Esta opción está disponible después de realizar un cambio en la miniatura. Si no desea mantener el cambio, puede revertirlo antes de guardarlo.

### Redes sociales {#social-media}

* **Compartir en redes sociales**

  Define las opciones de uso compartido disponibles en la página. Expone las opciones disponibles para [Uso compartido del componente principal](https://helpx.adobe.com/experience-manager/core-components/using/sharing.html).

   * **Habilitar el uso compartido de usuarios en Facebook**
   * **Habilitar el uso compartido de usuarios en Pinterest**
   * **Variación de XF preferida**
Defina la variación del fragmento de experiencia que se utilizará para generar los metadatos de la página

### Cloud Services {#cloud-services}

* **Cloud Services**

  Definir propiedades para [cloud services](/help/sites-developing/extending-cloud-config.md).

### Personalización {#personalization}

* **Configuración de ContextHub**

  Seleccione el [Configuración de ContextHub](/help/sites-developing/ch-configuring.md) y [Ruta de segmentos](/help/sites-administering/segmentation.md).

* **Configuración de ámbito**

  Seleccione una [marca para especificar un ámbito de objetivo](/help/sites-authoring/target-adobe-campaign.md).

  >[!NOTE]
  >Esta opción requiere una cuenta de usuario en el grupo `Target Adminstrators`.

### Permisos    {#permissions}

* **Permisos**

  En esta pestaña puede:

   * [Agregar permisos](/help/sites-administering/user-group-ac-admin.md)
   * [Editar grupo de usuarios cerrado](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)

   * Ver los [Permisos efectivos](/help/sites-administering/user-group-ac-admin.md)

  >[!CAUTION]
  >
  >El **Permisos** permite editar las configuraciones de CUG en función de la presencia del `granite:AuthenticationRequired` mixin. Si los permisos de página se configuran utilizando configuraciones de CUG obsoletas, según la presencia de `cq:cugEnabled` , se mostrará un mensaje de advertencia y los permisos de CUG no podrán editarse, como tampoco lo hará el requisito de autenticación de la propiedad [Avanzadas](/help/sites-authoring/editing-page-properties.md#advanced) pestaña puede editarse.
  >
  >
  >En tal caso, los permisos de CUG deben editarse en la variable [IU clásica](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

  >[!NOTE]
  >
  >La pestaña Permisos no permite la creación de grupos de CUG vacíos, lo que puede resultar útil como una forma sencilla de denegar el acceso a todos los usuarios. Para ello, se debe utilizar el Explorador de CRX. Ver el documento [Administración de derechos de usuario, grupo y acceso](/help/sites-administering/user-group-ac-admin.md) para obtener más información.

### Modelo {#blueprint}

* **Modelo**

  Defina propiedades para una página de modelo en [administración de varios sitios](/help/sites-administering/msm.md). Controla las circunstancias dentro de las que se propagarán las modificaciones a Live Copy.

### Live Copy    {#live-copy}

* **Live Copy**

  Definir propiedades para una página Live Copy en [administración de varios sitios](/help/sites-administering/msm.md). Controla las circunstancias dentro de las cuales se propagarán las modificaciones desde el modelo.

### Estructura del sitio    {#site-structure}

* Proporcione vínculos a páginas que proporcionan funcionalidad para todo el sitio, como **Página de suscripción**, **Página sin conexión**, entre otros. 

## Edición de las propiedades de página   {#editing-page-properties-1}

Puede definir las propiedades de la página:

* Desde la consola **Sitios:**

   * [Creando una página nueva](/help/sites-authoring/managing-pages.md#creating-a-new-page) (un subconjunto de las propiedades)

   * Pulsando o haciendo clic en **Propiedades**

      * Para una sola página
      * Para varias páginas (solo un subconjunto de las propiedades está disponible para su edición en masa)

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

1. Seleccionar **Abrir propiedades** y se abrirá un cuadro de diálogo que le permitirá editar las propiedades, ordenadas por la pestaña correspondiente. Los siguientes botones también están disponibles en la parte derecha de la barra de herramientas:

   * **Cancelar**
   * **Guardar y cerrar**

1. Utilice el botón **Guardar y cerrar** para guardar los cambios. 

### Desde la consola Sitios: varias páginas {#from-the-sites-console-multiple-pages}

Desde la consola **Sites** puede seleccionar varias páginas y luego utilizar **Ver propiedades** para ver o editar las propiedades de la página. Esto se conoce como edición masiva de propiedades de página.

>[!NOTE]
>
>La edición de propiedades por lotes también está disponible para los archivos. Es muy similar, pero difiere en algunos puntos. Consulte [Edición de propiedades de varios recursos](/help/assets/metadata.md) para obtener más información.
>
>También está el [Editor por lotes](/help/sites-administering/bulk-editor.md), que le permite buscar contenido de varias páginas con GQL (Google Query Language) y, a continuación, editar el contenido directamente en el editor por lotes antes de guardar los cambios en las páginas de origen.

Puede seleccionar varias páginas para editarlas por lotes mediante varios métodos, entre ellos:

* Al examinar la consola **Sites**
* Después de usar **Buscar** para localizar un conjunto de páginas

![epp-01](assets/epp-01.png)

Después de seleccionar las páginas y hacer clic o pulsar en la opción **Propiedades**, se muestran las propiedades por lotes:

![epp-02](assets/epp-02.png)

Solo se pueden editar por lotes las siguientes páginas:

* Las que compartan el mismo tipo de recurso.
* Las que no formen parte de una Live Copy.

   * Si alguna de las páginas está en una Live Copy, se mostrará un mensaje cuando se abran las propiedades. 

Cuando esté en la edición por lotes, podrá efectuar las siguientes acciones:

* **Ver**

  Al ver las Propiedades de página de varias páginas, puede ver lo siguiente:

   * Una lista de las páginas afectadas

      * Si es necesario, puede seleccionar o anular la selección

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

  Al editar Propiedades de página para varias páginas:

   * Puede actualizar los valores en los campos disponibles.

      * Los nuevos valores se aplicarán a todas las páginas seleccionadas al activar **Listo**.
      * Cuando el campo admite varios valores (por ejemplo, etiquetas), puede agregar un nuevo valor o eliminar un valor común.

   * Los campos que son comunes en las páginas, pero que tienen diferentes valores, se señalizarán con un valor especial; por ejemplo, el texto `<Mixed Entries>`.

>[!NOTE]
>
>El componente de página se puede configurar para especificar los campos disponibles para la edición por lotes. Consulte [Configurar la página para la edición masiva de propiedades de página](/help/sites-developing/bulk-editing.md).
