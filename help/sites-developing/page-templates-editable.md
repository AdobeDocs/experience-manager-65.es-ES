---
title: 'Plantillas de página: editables'
seo-title: 'Plantillas de página: editables'
description: Se han introducido plantillas editables en, permiten a los no desarrolladores crear y editar plantillas, proporcionan plantillas que mantienen una conexión dinámica con cualquier página creada a partir de ellas y hacen que el componente de página sea más genérico
seo-description: Se han introducido plantillas editables en, permiten a los no desarrolladores crear y editar plantillas, proporcionan plantillas que mantienen una conexión dinámica con cualquier página creada a partir de ellas y hacen que el componente de página sea más genérico
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Plantillas de página: editables {#page-templates-editable}

Se han introducido plantillas editables para:

* Permite que los autores especializados [creen y editen plantillas](/help/sites-authoring/templates.md).

   * Estos autores especializados se denominan autores **de plantillas**
   * Los autores de plantillas deben ser miembros del `template-authors` grupo.

* Proporcione plantillas que mantengan una conexión dinámica con cualquier página creada a partir de ellas. Esto garantiza que cualquier cambio en la plantilla se refleje en las páginas mismas.
* Convierta el componente de página en más genérico para que el componente de página principal pueda utilizarse sin personalización.

Con las plantillas editables, los fragmentos que crean una página están aislados dentro de los componentes. Puede configurar las combinaciones necesarias de componentes en una interfaz de usuario, eliminando así la necesidad de desarrollar un nuevo componente de página para cada variación de página.

>[!NOTE]
>
>[También hay plantillas](/help/sites-developing/page-templates-static.md) estáticas disponibles.

Este documento:

* Proporciona información general sobre la creación de plantillas editables

   * Para obtener más información, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md)

* Describe las tareas de administración y desarrollo necesarias para crear plantillas editables
* Describe los fundamentos técnicos de las plantillas editables

En este documento se asume que ya está familiarizado con la creación y edición de plantillas. Consulte el documento de creación [Creación de plantillas](/help/sites-authoring/templates.md)de página, en el que se detallan las funciones de las plantillas editables tal como se exponen al autor de la plantilla.

>[!NOTE]
>
>El siguiente tutorial también puede ser de interés para configurar una plantilla de página editable en un nuevo proyecto:
>[Introducción a AEM Sites, parte 2: Creación de una página base y una plantilla](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part2.html)

## Creating a New Template {#creating-a-new-template}

La creación de plantillas editables se realiza principalmente con la consola de [plantillas y el editor](/help/sites-authoring/templates.md) de plantillas. En esta sección se ofrece una visión general de este proceso y se ofrece una descripción de lo que ocurre a nivel técnico.

Para obtener información sobre cómo utilizar plantillas editables en un proyecto de AEM, consulte [Creación de un proyecto de AEM con Lazybones](https://helpx.adobe.com/experience-manager/using/aem_lazybones.html).

Al crear una nueva plantilla editable, realiza estas acciones:

1. Cree una [carpeta para las plantillas](#template-folders). Esto no es obligatorio, pero se recomienda una práctica recomendada.
1. Seleccione un tipo [de](#template-type)plantilla. Se copia para crear la definición [de](#template-definitions)plantilla.

   >[!NOTE]
   >
   >Se proporciona una selección de tipos de plantilla lista para usar. También puede [crear sus propios tipos](/help/sites-developing/page-templates-editable.md#creating-template-types) de plantilla específicos del sitio si es necesario.

1. Configure la estructura, las políticas de contenido, el contenido inicial y el diseño de la nueva plantilla.

   **Estructura**

   * La estructura permite definir componentes y contenido para la plantilla.
   * Los componentes definidos en la estructura de la plantilla no se pueden mover a una página resultante ni eliminarse de ninguna página resultante.

      * Si va a crear una plantilla en una carpeta personalizada fuera del contenido de muestra de We.Retail, puede elegir Componentes básicos o utilizar Componentes [principales](https://helpx.adobe.com/experience-manager/core-components/using/developing.html).
   * Si desea que los autores de la página puedan añadir y quitar componentes, añada un sistema de párrafos a la plantilla.
   * Los componentes pueden volver a desbloquearse y bloquearse para que pueda definir el contenido inicial.
   Para obtener más información sobre cómo define la estructura un autor de plantilla, consulte [Creación de plantillas](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)de página.

   Para obtener información técnica sobre la estructura, consulte [Estructura](/help/sites-developing/page-templates-editable.md#structure) en este documento.

   **Políticas**

   * Las políticas de contenido definen las propiedades de diseño de un componente.

      * Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas.
   * Esto se aplica a la plantilla (y a las páginas creadas con la plantilla).
   Para obtener más información sobre cómo define el autor de una plantilla las políticas, consulte [Creación de plantillas](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)de página.

   Para obtener información técnica sobre las políticas, consulte Políticas [de contenido](/help/sites-developing/page-templates-editable.md#content-policies) en este documento.

   **Contenido inicial**

   * El contenido inicial define el contenido que aparecerá cuando se cree una página por primera vez en función de la plantilla.
   * A continuación, los autores de las páginas pueden editar el contenido inicial.
   Para obtener más información sobre cómo define la estructura un autor de plantilla, consulte [Creación de plantillas](/help/sites-authoring/templates.md#editing-a-template-initial-content-author)de página.

   Para obtener detalles técnicos sobre el contenido inicial, consulte Contenido [](/help/sites-developing/page-templates-editable.md#initial-content) inicial en este documento.

   **Diseño**

   * Puede definir el diseño de la plantilla para una amplia gama de dispositivos.
   * El diseño adaptable para plantillas funciona igual que para la creación de páginas.
   Para obtener más información sobre cómo define el diseño de plantilla un autor de plantilla, consulte [Creación de plantillas](/help/sites-authoring/templates.md#editing-a-template-layout-template-author)de página.

   Para obtener información técnica sobre el diseño de la plantilla, consulte [Diseño](/help/sites-developing/page-templates-editable.md#layout) en este documento.

1. Habilite la plantilla y, a continuación, déjela para árboles de contenido específicos.

   * Una plantilla puede habilitarse o deshabilitarse para que esté disponible o no esté disponible para los autores de la página.
   * Una plantilla puede estar disponible o no disponible para determinadas ramas de la página.
   Para obtener más información sobre cómo el autor de una plantilla habilita una plantilla, consulte [Creación de plantillas](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author)de página.

   Para obtener información técnica sobre cómo habilitar una plantilla, consulte [Activación y autorización de una plantilla para](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)uso en este documento

1. Utilícelo para crear páginas de contenido.

   * Al utilizar una plantilla para crear una página nueva, no existe ninguna diferencia visible ni ninguna indicación entre las plantillas estáticas y las editables.
   * Para el autor de la página, el proceso es transparente.
   Para obtener más información sobre cómo el autor de una página utiliza plantillas para crear una página, consulte [Creación y organización de páginas](/help/sites-authoring/managing-pages.md#templates).

   Para obtener detalles técnicos sobre la creación de páginas con plantillas editables, consulte [Páginas](/help/sites-developing/page-templates-editable.md#resultant-content-pages) de contenido resultantes en este documento.

>[!NOTE]
>
>La biblioteca de cliente del editor asume la presencia del espacio de nombres en las páginas de contenido y, si no se encuentra, `cq.shared` `Uncaught TypeError: Cannot read property 'shared' of undefined` se producirá el error de JavaScript.
>
>Todas las páginas de contenido de muestra contienen `cq.shared`, por lo que cualquier contenido basado en ellas incluye `cq.shared`. Sin embargo, si decide crear sus propias páginas de contenido desde cero sin basarlas en contenido de muestra, debe asegurarse de incluir el `cq.shared` espacio de nombres.
>
>Consulte [Uso de bibliotecas](/help/sites-developing/clientlibs.md) del lado del cliente para obtener más información.

>[!CAUTION]
>
>No introduzca nunca en una plantilla información que deba [internacionalizarse](/help/sites-developing/i18n.md).

## Carpetas de plantilla {#template-folders}

Para organizar las plantillas, puede utilizar las siguientes carpetas:

* **global**
* Específico del sitioLas carpetas específicas del sitio que se crean para organizar las plantillas se crean con una cuenta que tiene privilegios de administrador.

>[!NOTE]
>
>Aunque puede anidar las carpetas, cuando el usuario las ve en la consola **Plantillas** , se presentan como una estructura plana.

In a standard AEM instance the **global** folder already exists in the template console. Contiene plantillas predeterminadas y actúa como alternativa en caso de que no se encuentre ninguna política ni ningún tipo de plantilla en la carpeta actual. Puede agregar las plantillas predeterminadas a esta carpeta o crear una nueva carpeta (recomendado).

>[!NOTE]
>
>Se recomienda crear una nueva carpeta para albergar las plantillas personalizadas y no utilizar la carpeta global.

>[!CAUTION]
>
>Las carpetas deben ser creadas por un usuario con `admin` derechos.

Los tipos de plantilla y las directivas se heredan en todas las carpetas según el siguiente orden de prioridad:

1. La carpeta actual.
1. Principal(s) de la carpeta actual.
1. `/conf/global`
1. `/apps`
1. `/libs`

Se crea una lista de todas las entradas permitidas. Si alguna configuración se superpone ( `path`/ `label`), solo se presenta al usuario la instancia más cercana a la carpeta actual.

Para crear una nueva carpeta, puede hacer lo siguiente:

* Programáticamente o con CRXDE Lite
* Uso del navegador de configuración

## Uso de CRXDE Lite {#using-crxde-lite}

1. Se puede crear una nueva carpeta (en /conf) para su instancia mediante programación o con CRXDE Lite.

   Debe utilizarse la siguiente estructura:

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. A continuación, puede definir las siguientes propiedades en el nodo raíz de la carpeta:

   `<your-folder-name> [sling:Folder]`

   Nombre: `jcr:title`

   * Tipo: `String`

   * Valor: Título (para la carpeta) que desea que aparezca en la consola **Plantillas** .

1. Además ** de los permisos y privilegios de creación estándar (p. ej. `content-authors`) ahora debe asignar grupos y definir los derechos de acceso requeridos (ACL) para que los autores puedan crear plantillas en la nueva carpeta.

   El grupo `template-authors` es el grupo predeterminado que se debe asignar. Consulte la siguiente sección [ACL y grupos](/help/sites-developing/page-templates-editable.md#acls-and-groups) para obtener más información.

   Consulte Administración de derechos de [acceso](/help/sites-administering/user-group-ac-admin.md#access-right-management) para obtener información detallada sobre la administración y asignación de derechos de acceso.

### Uso del navegador de configuración {#using-the-configuration-browser}

1. Vaya a Navegación **** global -> **Herramientas** > Navegador **** de configuración.

   Las carpetas existentes se muestran a la izquierda, incluida la carpeta **** global.

1. Haga clic en **Crear**.
1. En el cuadro de diálogo **Crear configuración** se deben configurar los campos siguientes:

   * **Título**: Proporcionar un título para la carpeta de configuración
   * **Plantillas** editables: Haga clic para permitir plantillas editables dentro de esta carpeta

1. Haga clic en **Crear**

>[!NOTE]
>
>En el navegador de configuración, puede editar la carpeta global y activar la opción Plantillas **** editables si desea crear plantillas dentro de esta carpeta, aunque no se recomienda hacerlo.

### ACL y grupos {#acls-and-groups}

Una vez creadas las carpetas de plantilla (ya sea a través de CRXDE o con el navegador de configuración), las ACL deben definirse para los grupos adecuados para las carpetas de plantilla a fin de garantizar una seguridad adecuada.

Las carpetas de plantillas para la implementación [de referencia de](/help/sites-developing/we-retail.md) We.Retail pueden utilizarse como ejemplo.

#### El grupo de autores de plantillas {#the-template-authors-group}

El `template-authors` grupo es el grupo que se utiliza para administrar el acceso a las plantillas y viene de serie con AEM, pero está vacío. Los usuarios deben agregarse al grupo para el proyecto o sitio.

>[!CAUTION]
>
>El `template-authors` grupo *solo* está disponible para los usuarios que deben poder crear nuevas plantillas.
>
>La edición de plantillas es muy potente y, si no se realiza correctamente, se pueden romper las plantillas existentes. Por lo tanto, esta función debe centrarse y incluir únicamente a usuarios cualificados.

En la tabla siguiente se detallan los permisos necesarios para editar plantillas.

<table>
 <tbody>
  <tr>
   <th>Ruta</th>
   <th>Función/Grupo</th>
   <th>Permisos<br /> </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autores de plantilla<br /> </td>
   <td>leer, escribir, replicar</td>
   <td>Creadores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en un espacio específico del sitio <code>/conf</code></td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>read</td>
   <td>El usuario web anónimo debe leer las plantillas al procesar una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>replicateLos autores de contenido deben activar las plantillas de una página al activar una página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>leer, escribir, replicar</td>
   <td>Creadores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en un espacio específico del sitio <code>/conf</code></td>
  </tr>
  <tr>
   <td>Usuario Web anónimo</td>
   <td>read</td>
   <td>El usuario web anónimo debe leer las directivas al procesar una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>Los creadores de contenido deben activar las directivas de una plantilla de una página al activar una página</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autor de plantillas</td>
   <td>read</td>
   <td>El autor de la plantilla crea una nueva plantilla basada en uno de los tipos de plantilla predefinidos.</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>ninguno</td>
   <td>El usuario web anónimo no debe acceder a los tipos de plantilla</td>
  </tr>
 </tbody>
</table>

Este `template-authors` grupo predeterminado solo cubre la configuración del proyecto, donde todos `template-authors` los miembros pueden acceder a todas las plantillas y crearlas. Para configuraciones más complejas, donde se necesitan varios grupos de autores de plantillas para separar el acceso a las plantillas, se deben crear más grupos de autores de plantillas personalizadas. Sin embargo, los permisos para los grupos de autores de plantillas seguirían siendo los mismos.

#### Plantillas heredadas en /conf/global {#legacy-templates-under-conf-global}

Las plantillas ya no deben almacenarse en `/conf/global`, pero para algunas instalaciones heredadas puede que haya plantillas en esta ubicación. SOLO en estas situaciones heredadas deben configurarse explícitamente las siguientes `/conf/global` rutas.

<table>
 <tbody>
  <tr>
   <th>Ruta</th>
   <th>Función/Grupo</th>
   <th>Permisos<br /> </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>Autores de plantilla</td>
   <td>leer, escribir, replicar</td>
   <td>Creadores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>read</td>
   <td>El usuario web anónimo debe leer las plantillas al procesar una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>Los creadores de contenido deben activar las plantillas de una página al activar una página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>leer, escribir, replicar</td>
   <td>Creadores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>read</td>
   <td>El usuario web anónimo debe leer las directivas al procesar una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>Los creadores de contenido deben activar las directivas de una plantilla de una página al activar una página</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>Autor de plantillas</td>
   <td>read</td>
   <td>El autor de la plantilla crea una nueva plantilla basada en uno de los tipos de plantilla predefinidos</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>ninguno</td>
   <td>El usuario web anónimo no debe acceder a los tipos de plantilla</td>
  </tr>
 </tbody>
</table>

## Template Type {#template-type}

Al crear una nueva plantilla, debe especificar un tipo de plantilla:

* Los tipos de plantilla proporcionan plantillas para una plantilla. Al crear una nueva plantilla, se utiliza la estructura y el contenido inicial del tipo de plantilla seleccionado para crearlos en la nueva plantilla.

   * El tipo de plantilla se copia para crear la plantilla.
   * Una vez que se ha producido la copia, la única conexión entre la plantilla y el tipo de plantilla es una referencia estática con fines informativos.

* Los tipos de plantilla le permiten definir:

   * Tipo de recurso del componente de página.
   * La directiva del nodo raíz, que define los componentes permitidos en el editor de plantillas.
   * Se recomienda definir los puntos de interrupción para la cuadrícula adaptable y la configuración del emulador móvil en el tipo de plantilla. Esto es opcional, ya que la configuración también se puede definir en la plantilla individual (consulte Tipo [de plantilla y Grupos](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)de dispositivos móviles).

* AEM ofrece una pequeña selección de tipos de plantilla predeterminados, como Página HTML5 y Página de formulario adaptable.

   * Se proporcionan ejemplos adicionales como parte del contenido de muestra de [We.Retail](/help/sites-developing/we-retail.md) .

* Los desarrolladores suelen definir los tipos de plantilla.

Los tipos de plantilla predeterminados se almacenan en:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>No debe cambiar nada en la `/libs` ruta. Esto se debe a que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y puede sobrescribirse al aplicar una revisión o un paquete de funciones).

Los tipos de plantilla específicos del sitio deben almacenarse en la ubicación comparable de:

* `/apps/settings/wcm/template-types`

Las definiciones de los tipos de plantillas personalizadas deben almacenarse en carpetas definidas por el usuario (recomendadas) o bien en `global`. Por ejemplo:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Los tipos de plantilla deben respetar la estructura de carpetas correcta (por ejemplo: `/settings/wcm/...`); de lo contrario, no se encontrarán los tipos de plantilla.

### Tipo de plantilla y grupos de dispositivos móviles {#template-type-and-mobile-device-groups-br}

Los grupos [de](/help/sites-developing/mobile.md#device-groups) dispositivos utilizados para una plantilla editable (establecida como ruta relativa de la propiedad `cq:deviceGroups`) definen qué dispositivos móviles están disponibles como emuladores en el modo [de](/help/sites-authoring/responsive-layout.md) diseño de la creación de páginas. Este valor se puede establecer en dos lugares:

* En el tipo de plantilla editable
* En la plantilla editable

Al crear una nueva plantilla editable, el valor se copia del tipo de plantilla a la plantilla individual. Si el valor no está establecido en el tipo, se puede establecer en la plantilla. Una vez creada una plantilla, no hay herencia del tipo a la plantilla.

>[!CAUTION]
>
>El valor de `cq:deviceGroups` debe configurarse como una ruta relativa como, por ejemplo, `mobile/groups/responsive` y no como una ruta absoluta como, por ejemplo, `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>Con las plantillas [](/help/sites-developing/page-templates-static.md)estáticas, el valor de `cq:deviceGroups` puede configurarse en la raíz del sitio.
>
>Con las plantillas editables, este valor ahora se almacena en el nivel de plantilla y no se admite en el nivel de raíz de la página.

### Creación de tipos de plantilla {#creating-template-types}

Si ha creado una plantilla que puede servir de base para otras plantillas, puede copiar esta plantilla como un tipo de plantilla.

1. Cree una plantilla como lo haría con cualquier plantilla editable [como se documenta aquí](/help/sites-authoring/templates.md#creating-a-new-template-template-author), lo que servirá de base para el tipo de plantilla.
1. Con CRXDE Lite, copie la plantilla recién creada del `templates` nodo en el `template-types` nodo situado debajo de la carpeta [de](/help/sites-developing/page-templates-editable.md#template-folders)plantilla.
1. Elimine la plantilla del `templates` nodo situado debajo de la carpeta [de la](/help/sites-developing/page-templates-editable.md#template-folders)plantilla.
1. En la copia de la plantilla que se encuentra bajo el `template-types` nodo, elimine todas `cq:template` las propiedades y `cq:templateType``jcr:content` .

También puede desarrollar su propio tipo de plantilla utilizando como base una plantilla editable de ejemplo, disponible en GitHub.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra un proyecto de tipo aem-sites-example-custom-template en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definiciones de plantilla {#template-definitions}

Las definiciones de las plantillas editables se almacenan en carpetas [definidas por el](/help/sites-developing/page-templates-editable.md#template-folders) usuario (recomendadas) o de forma alternativa en `global`. Por ejemplo:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

El nodo raíz de la plantilla es del tipo `cq:Template` con una estructura de esqueleto de:

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

Los elementos principales son:

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

Este nodo contiene propiedades para la plantilla:

* **Nombre**: `jcr:title`

* **Nombre**: `status`

   * ``**Tipo**: `String`

   * **Valor**: `draft`, `enabled` o `disabled`

### Estructura {#structure}

Define la estructura de la página resultante:

* Se combina con el contenido inicial ( `/initial`) al crear una página nueva.
* Los cambios realizados en la estructura se reflejarán en cualquier página creada con la plantilla.
* El nodo `root` ( `structure/jcr:content/root`) define la lista de componentes que estarán disponibles en la página resultante.

   * Los componentes definidos en la estructura de plantilla no se pueden mover ni eliminar de ninguna página resultante.
   * Una vez desbloqueado el componente, la `editable` propiedad se establece en `true`.

   * Una vez desbloqueado un componente que ya contiene contenido, este contenido se moverá a la `initial` rama.

* El `cq:responsive` nodo contiene definiciones para el diseño interactivo.

### Contenido inicial {#initial-content}

Define el contenido inicial que tendrá una página nueva al crearla:

* Contiene un `jcr:content` nodo que se copia en cualquier página nueva.
* Se combina con la estructura ( `/structure`) al crear una página nueva.
* Las páginas existentes no se actualizarán si se cambia el contenido inicial después de la creación.
* El `root` nodo contiene una lista de componentes para definir lo que estará disponible en la página resultante.
* Si se agrega contenido a un componente en modo de estructura y dicho componente se desbloquea posteriormente (o viceversa), este contenido se utiliza como contenido inicial.

### Diseño {#layout}

Al [editar una plantilla puede definir el diseño](/help/sites-authoring/templates.md), con un diseño [interactivo](/help/sites-authoring/responsive-layout.md) estándar que también se puede [configurar](/help/sites-administering/configuring-responsive-layout.md).

### Content Policies {#content-policies}

Las políticas de contenido (o diseño) definen las propiedades de diseño de un componente. Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas. Esto se aplica a la plantilla (y a las páginas creadas con la plantilla). Las directivas de contenido se pueden crear y seleccionar en el editor de plantillas.

* La propiedad `cq:policy`, en el `root` nodo
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Proporciona una referencia relativa a la directiva de contenido para el sistema de párrafos de la página.

* La propiedad `cq:policy`, en los nodos explícitos del componente debajo de `root`, proporciona vínculos a las políticas de los componentes individuales.

* Las definiciones de directiva reales se almacenan en:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Las rutas de las definiciones de políticas dependen de la ruta del componente. `cq:policy` contiene una referencia relativa a la configuración misma.

>[!NOTE]
>
>Las páginas creadas a partir de plantillas editables no ofrecen un modo de diseño en el editor de páginas.
>
>El `policies` árbol de una plantilla editable tiene la misma jerarquía que la configuración del modo de diseño de una plantilla estática en:
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>La configuración del modo de diseño de una plantilla estática se definió por componente de página.

### Políticas de la página {#page-policies}

Las políticas de página permiten definir la directiva [de](#content-policies) contenido para la página (parsys principal), ya sea en la plantilla o en las páginas resultantes.

### Habilitar y permitir el uso de una plantilla {#enabling-and-allowing-a-template-for-use}

1. **Habilitar la plantilla**

   Para poder usar una plantilla, debe habilitarla:

   * [Activación de la plantilla](/help/sites-authoring/templates.md#enablingatemplateauthor) desde la consola **Plantillas** .

   * Definición de la propiedad status en el `jcr:content` nodo.

      * Por ejemplo, en:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Defina la propiedad:

         * Nombre:status
         * Tipo: Cadena
         * Value: `enabled`

1. **Plantillas permitidas**

   * [Defina las rutas de plantilla permitidas en las Propiedades **de **](/help/sites-authoring/templates.md#allowing-a-template-author)página de la página o página raíz adecuada de una subrama.
   * Establezca la propiedad:
      `cq:allowedTemplates`
En el `jcr:content` nodo de la rama requerida.
   Por ejemplo, con un valor de:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Páginas de contenido resultantes {#resultant-content-pages}

Páginas creadas a partir de plantillas editables:

* Se crean con un subárbol que se combina desde `structure` y `initial` en la plantilla

* Tenga referencias a la información contenida en la plantilla y el tipo de plantilla. Esto se logra con un `jcr:content` nodo con las propiedades:

   * `cq:template`
Proporciona la referencia dinámica a la plantilla real; permite que los cambios realizados en la plantilla se reflejen en las páginas reales.

   * `cq:templateType`
Proporciona una referencia al tipo de plantilla.

![chlimage_1-71](assets/chlimage_1-71.png)

El diagrama anterior muestra cómo las plantillas, el contenido y los componentes se interrelacionan:

* Controlador: `/content/<my-site>/<my-page>`la página resultante que hace referencia a la plantilla. El contenido controla todo el proceso. De acuerdo con las definiciones, accede a la plantilla y los componentes correspondientes.

* Configuración: `/conf/<my-folder>/settings/wcm/templates/<my-template>`la [plantilla y las directivas](#template-definitions) de contenido relacionadas definen la configuración de la página.

* Modelo: paquetes OSGiLos paquetes [OSGI](/help/sites-deploying/osgi-configuration-settings.md) implementan la funcionalidad.

* Vista: `/apps/<my-site>/components`Tanto en los entornos de autor como de publicación, el contenido lo representan [los componentes](/help/sites-developing/components.md).

Al procesar una página:

* **Plantillas**:

   * Se hará referencia a la `cq:template` propiedad de su `jcr:content` nodo para acceder a la plantilla que corresponde a esa página.

* **Componentes**:

   * El componente de página combinará el `structure/jcr:content` árbol de la plantilla con el `jcr:content` árbol de la página.

   * El componente de página solo permitirá al autor editar los nodos de la estructura de plantilla que se han marcado como editables (así como cualquier elemento secundario).
   * Cuando se procesa un componente en una página, la ruta relativa de dicho componente se toma del `jcr:content` nodo; se buscará la misma ruta bajo el `policies/jcr:content` nodo de la plantilla.

      * La `cq:policy` propiedad de este nodo apunta a la directiva de contenido real (es decir, contiene la configuración de diseño para ese componente).

      * Esto le permite tener varias plantillas que reutilizan las mismas configuraciones de directiva de contenido.
