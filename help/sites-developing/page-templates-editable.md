---
title: 'Plantillas de página: editables'
seo-title: Page Templates - Editable
description: Se han introducido plantillas editables en, permiten a los usuarios que no son desarrolladores crear y editar plantillas, proporcionan plantillas que conservan una conexión dinámica con cualquier página creada a partir de ellas y hacen que el componente de página sea más genérico
seo-description: Editable templates have been introduced to, allow non-developers to create and edit templates, provide templates that retain a dynamic connection to any pages created from them, and make the page component more generic
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
exl-id: dcb66b6d-d731-493e-8936-12d529f6cbde
source-git-commit: ae56ffafff38fe60530a8850732de58ba8c8f8f9
workflow-type: tm+mt
source-wordcount: '3252'
ht-degree: 10%

---

# Plantillas de página: editables {#page-templates-editable}

Las plantillas editables se han introducido en:

* Permitir que los autores especializados [crear y editar plantillas](/help/sites-authoring/templates.md).

   * Estos autores especializados se denominan **autores de plantillas**
   * Los autores de plantillas deben ser miembros de `template-authors` grupo.

* Proporcione plantillas que mantengan una conexión dinámica con cualquier página creada a partir de ellas. Esto garantiza que cualquier cambio en la plantilla se refleje en las propias páginas.
* Hacer que el componente de página sea más genérico para que el componente de página principal se pueda utilizar sin personalización.

Con las plantillas editables, las partes que componen una página están aisladas dentro de los componentes. Puede configurar las combinaciones necesarias de componentes en una interfaz de usuario, lo que elimina la necesidad de desarrollar un nuevo componente de página para cada variación de página.

>[!NOTE]
>
>[Plantillas estáticas](/help/sites-developing/page-templates-static.md) también están disponibles.

Este documento:

* Ofrece información general sobre la creación de plantillas editables

   * Para obtener más información, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md)

* Describe las tareas de administrador/desarrollador necesarias para crear plantillas editables
* Describe los fundamentos técnicos de las plantillas editables

Este documento supone que ya está familiarizado con la creación y edición de plantillas. Consulte el documento de creación [Creación de plantillas de página](/help/sites-authoring/templates.md), que detalla las capacidades de las plantillas editables tal como se exponen al autor de la plantilla.

>[!NOTE]
>
>El siguiente tutorial también puede ser de interés para configurar una plantilla de página editable en un nuevo proyecto:
>[Introducción a AEM Sites, parte 2: Creación de una página base y una plantilla](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part2.html)

## Creación de una nueva plantilla {#creating-a-new-template}

La creación de plantillas editables se realiza principalmente con [consola de plantillas y editor de plantillas](/help/sites-authoring/templates.md) por un autor de plantillas. En esta sección se ofrece una descripción general de este proceso y se incluye una descripción de lo que sucede a nivel técnico.

AEM Para obtener más información sobre cómo utilizar plantillas editables en un proyecto de, consulte [AEM Creación de un proyecto de con Lazybones](https://helpx.adobe.com/experience-manager/using/aem_lazybones.html).

Al crear una nueva plantilla editable, realiza estas acciones:

1. Crear un [carpeta para las plantillas](#template-folders). Esto no es obligatorio, pero es una práctica recomendada.
1. Seleccione una [tipo de plantilla](#template-type). Esto se copia para crear el [definición de plantilla](#template-definitions).

   >[!NOTE]
   >
   >Se proporciona una selección de tipos de plantillas listas para usarse. También puede [crear sus propios tipos de plantillas específicas del sitio](/help/sites-developing/page-templates-editable.md#creating-template-types) si es necesario.

1. Configure la estructura, las políticas de contenido, el contenido inicial y el diseño de la nueva plantilla.

   **Estructura**

   * La estructura permite definir componentes y contenido para la plantilla.
   * Los componentes definidos en la estructura de la plantilla no se pueden mover a una página resultante ni eliminarse de ninguna página resultante.

      * Si está creando una plantilla en una carpeta personalizada fuera del contenido de muestra de We.Retail, puede elegir Componentes de base o utilizar [Componentes principales](https://helpx.adobe.com/experience-manager/core-components/using/developing.html).
   * Si desea que los autores de la página puedan añadir y quitar componentes, añada un sistema de párrafos a la plantilla.
   * Los componentes pueden volver a desbloquearse y bloquearse para que pueda definir el contenido inicial.

   Para obtener más información sobre cómo define la estructura un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Para obtener detalles técnicos de la estructura, consulte [Estructura](/help/sites-developing/page-templates-editable.md#structure) en este documento.

   **Políticas**

   * Las políticas de contenido definen las propiedades de diseño de un componente.

      * Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas.
   * Esto se aplica a la plantilla (y a las páginas creadas con la plantilla).

   Para obtener más información sobre cómo define las directivas un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Para obtener más información técnica sobre las directivas, consulte [Políticas de contenido](/help/sites-developing/page-templates-editable.md#content-policies) en este documento.

   **Contenido inicial**

   * El contenido inicial define el contenido que aparecerá cuando se cree una página por primera vez en función de la plantilla.
   * Los autores de la página pueden editar el contenido inicial.

   Para obtener más información sobre cómo define la estructura un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   Para obtener detalles técnicos sobre el contenido inicial, consulte [Contenido inicial](/help/sites-developing/page-templates-editable.md#initial-content) en este documento.

   **Diseño**

   * Puede definir el diseño de la plantilla para una amplia gama de dispositivos.
   * El diseño interactivo para las plantillas funciona tal como lo hace para la creación de páginas.

   Para obtener más información sobre cómo define el diseño de la plantilla un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   Para obtener más información técnica sobre el diseño de la plantilla, consulte [Diseño](/help/sites-developing/page-templates-editable.md#layout) en este documento.

1. Habilite la plantilla y déjela para árboles de contenido específicos.

   * Una plantilla se puede habilitar o deshabilitar para que esté disponible o no disponible para los autores de páginas.
   * Una plantilla puede estar disponible o no disponible para determinadas ramas de la página.

   Para obtener más información sobre cómo un autor de plantillas habilita una plantilla, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   Para obtener más información técnica sobre la activación de una plantilla, consulte [Activación y autorización de una plantilla](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)e en este documento

1. Úselo para crear páginas de contenido.

   * Al utilizar una plantilla para crear una página nueva, no existe ninguna diferencia visible ni ninguna indicación entre las plantillas estáticas y las editables.
   * Para el autor de la página, el proceso es transparente.

   Para obtener más información sobre cómo un autor de páginas utiliza plantillas para crear una página, consulte [Crear y organizar páginas](/help/sites-authoring/managing-pages.md#templates).

   Para obtener más información técnica sobre la creación de páginas con plantillas editables, consulte [Páginas de contenido resultantes](/help/sites-developing/page-templates-editable.md#resultant-content-pages) en este documento.

>[!TIP]
>
>No introduzca nunca en una plantilla información que deba internacionalizarse. Para fines de internalización, la variable [función de localización de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=es) se recomiendan.

>[!NOTE]
>
>Las plantillas son herramientas útiles para optimizar el flujo de trabajo de creación de páginas. Sin embargo, demasiadas plantillas pueden saturar a los autores y hacer que la creación de páginas sea confusa. Una buena regla general es mantener el número de plantillas por debajo de 100.
>
>Adobe no recomienda tener más de 1000 plantillas debido a posibles impactos en el rendimiento.

>[!NOTE]
>
>La biblioteca de cliente del editor supone la presencia de `cq.shared` en las páginas de contenido y, si no hay ningún error de JavaScript, `Uncaught TypeError: Cannot read property 'shared' of undefined` resultará.
>
>Todas las páginas de contenido de muestra contienen `cq.shared`, de modo que cualquier contenido basado en ellos incluye automáticamente `cq.shared`. Sin embargo, si decide crear sus propias páginas de contenido desde cero sin basarlas en contenido de ejemplo, debe asegurarse de incluir la variable `cq.shared` namespace.
>
>Consulte [Uso de bibliotecas del lado del cliente](/help/sites-developing/clientlibs.md) para obtener más información.

## Carpetas de plantilla {#template-folders}

Para organizar las plantillas, puede utilizar las siguientes carpetas:

* **global**
* Específico del sitio Las carpetas específicas del sitio que cree para organizar las plantillas se crean con una cuenta que contiene privilegios de administrador.

>[!NOTE]
>
>Aunque puede anidar las carpetas, cuando el usuario las vea en la **Plantillas** consola se presentan como una estructura plana.

En una instancia estándar de AEM, la carpeta **Global** ya existe en la consola de plantillas. Contiene plantillas predeterminadas y actúa como alternativa en caso de que no se encuentre ninguna política ni ningún tipo de plantilla en la carpeta actual. Puede agregar las plantillas predeterminadas a esta carpeta o crear una nueva carpeta (recomendado).

>[!NOTE]
>
>Se recomienda crear una nueva carpeta para guardar las plantillas personalizadas y no utilizar la carpeta global.

>[!CAUTION]
>
>Las carpetas debe crearlas un usuario con `admin` derechos.

Los tipos de plantilla y las directivas se heredan en todas las carpetas según el siguiente orden de prioridad:

1. La carpeta actual.
1. Elemento principal de la carpeta actual.
1. `/conf/global`
1. `/apps`
1. `/libs`

Se crea una lista de todas las entradas permitidas. Si alguna configuración se superpone ( `path`/ `label`), solo se presenta al usuario la instancia más cercana a la carpeta actual.

Para crear una carpeta nueva, puede hacer lo siguiente:

* Mediante programación o con el CRXDE Lite
* Uso del explorador de configuración

## Uso del CRXDE Lite {#using-crxde-lite}

1. Se puede crear una nueva carpeta (en /conf) para su instancia mediante programación o con el CRXDE Lite.

   Se debe utilizar la siguiente estructura:

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

   * Valor: el título (de la carpeta) que desea que aparezca en la **Plantillas** consola.

1. Entrada *adición* a los permisos y privilegios de creación estándar (por ejemplo, `content-authors`Ahora debe asignar grupos y definir los derechos de acceso (ACL) necesarios para que los autores puedan crear plantillas en la nueva carpeta.

   El `template-authors` group es el grupo predeterminado que debe asignarse. Consulte la siguiente sección [ACL y grupos](/help/sites-developing/page-templates-editable.md#acls-and-groups) para obtener más información.

   Consulte [Administración de derechos de acceso](/help/sites-administering/user-group-ac-admin.md#access-right-management) para obtener información detallada sobre la administración y asignación de derechos de acceso.

### Uso del explorador de configuración {#using-the-configuration-browser}

1. Ir a **Navegación global** -> **Herramientas** > **Explorador de configuración**.

   Las carpetas existentes se muestran a la izquierda, incluida la **global** carpeta.

1. Haga clic en **Crear**.
1. En el **Crear configuración** diálogo se deben configurar los siguientes campos:

   * **Título**: proporcione un título para la carpeta de configuración
   * **Plantillas editables**: Marque para permitir plantillas editables dentro de esta carpeta

1. Haga clic en **Crear**

>[!NOTE]
>
>En el Explorador de configuración, puede editar la carpeta global y activar el **Plantillas editables** si desea crear plantillas dentro de esta carpeta, sin embargo, esta no es la práctica recomendada.
>
>Consulte la documentación del [Explorador de configuración](/help/sites-administering/configurations.md) para obtener más información.

### ACL y grupos {#acls-and-groups}

Una vez creadas las carpetas de plantilla (ya sea mediante CRXDE o con el Explorador de configuración), se deben definir ACL para los grupos adecuados para las carpetas de plantilla para garantizar la seguridad adecuada.

Las carpetas de plantilla para la [Implementación de referencia de We.Retail](/help/sites-developing/we-retail.md) se puede utilizar como ejemplo.

#### El grupo de autores de plantillas {#the-template-authors-group}

El `template-authors` AEM group es el grupo que se utiliza para administrar el acceso a las plantillas y viene de serie con la opción de acceso a las plantillas, pero está vacío. Los usuarios deben agregarse al grupo para el proyecto o sitio.

>[!CAUTION]
>
>El `template-authors` el grupo está *solamente* para usuarios que deben poder crear nuevas plantillas.
>
>La edición de plantillas es muy potente y, si no se realiza correctamente, las plantillas existentes pueden romperse. Por lo tanto, esta función debe centrarse y solo incluir usuarios cualificados.

La siguiente tabla detalla los permisos necesarios para editar plantillas.

<table>
 <tbody>
  <tr>
   <th>Ruta </th>
   <th>Rol/grupo</th>
   <th>Permisos<br /> </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Template Autores<br /> </td>
   <td>leer, escribir, replicar</td>
   <td>Autores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en sitios específicos <code>/conf</code> espacio</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>read</td>
   <td>El usuario web anónimo debe leer las plantillas mientras procesa una página</td>
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
   <td>Autores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en sitios específicos <code>/conf</code> espacio</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>read</td>
   <td>El usuario web anónimo debe leer las directivas mientras procesa una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>Los autores de contenido deben activar las políticas de una plantilla de una página al activar una página</td>
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

Este valor predeterminado `template-authors` grupo solo abarca las configuraciones de proyecto, donde todas las `template-authors` los miembros pueden acceder a todas las plantillas y crearlas. Para configuraciones más complejas, donde se necesitan varios grupos de autores de plantillas para separar el acceso a las plantillas, se deben crear grupos de autores de plantillas más personalizados. Sin embargo, los permisos para los grupos de autores de plantillas seguirían siendo los mismos.

#### Plantillas heredadas en /conf/global {#legacy-templates-under-conf-global}

Las plantillas ya no deben almacenarse en `/conf/global`Sin embargo, para algunas instalaciones heredadas puede que aún haya plantillas en esta ubicación. SOLAMENTE en tales situaciones heredadas debería suceder lo siguiente `/conf/global` las rutas deben configurarse explícitamente.

<table>
 <tbody>
  <tr>
   <th>Ruta </th>
   <th>Rol/grupo</th>
   <th>Permisos<br /> </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>Template Autores</td>
   <td>leer, escribir, replicar</td>
   <td>Autores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>read</td>
   <td>El usuario web anónimo debe leer las plantillas mientras procesa una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>Los autores de contenido deben activar las plantillas de una página al activar una página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>leer, escribir, replicar</td>
   <td>Autores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>read</td>
   <td>El usuario web anónimo debe leer las directivas mientras procesa una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>Los autores de contenido deben activar las políticas de una plantilla de una página al activar una página</td>
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

## Tipo de plantilla {#template-type}

Al crear una plantilla nueva, debe especificar un tipo de plantilla:

* Los tipos de plantilla proporcionan plantillas para una plantilla de forma eficaz. Al crear una plantilla nueva, se utiliza la estructura y el contenido inicial del tipo de plantilla seleccionado para crear la nueva plantilla.

   * El tipo de plantilla se copia para crearla.
   * Una vez realizada la copia, la única conexión entre la plantilla y el tipo de plantilla es una referencia estática con fines informativos.

* Los tipos de plantilla permiten definir lo siguiente:

   * El tipo de recurso del componente de página.
   * La directiva del nodo raíz, que define los componentes permitidos en el editor de plantillas.
   * Se recomienda definir los puntos de interrupción para la cuadrícula adaptable y la configuración del emulador móvil en en el tipo de plantilla. Esto es opcional, ya que la configuración también se puede definir en la plantilla individual (consulte [Tipo de plantilla y grupos de dispositivos móviles](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)).

* AEM proporciona una pequeña selección de tipos de plantillas listas para usar, como Página de HTML5 y Página de formulario adaptable.

   * Se proporcionan ejemplos adicionales como parte de la variable [We.Retail](/help/sites-developing/we-retail.md) contenido de muestra.

* Los desarrolladores suelen definir los tipos de plantillas.

Los tipos de plantilla predeterminados se almacenan en:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>No debe cambiar nada en el `/libs` ruta. Esto se debe al contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y puede sobrescribirse al aplicar una revisión o un paquete de funciones).

Los tipos de plantilla específicos del sitio deben almacenarse en la ubicación comparable de:

* `/apps/settings/wcm/template-types`

Las definiciones de los tipos de plantillas personalizadas deben almacenarse en carpetas definidas por el usuario (recomendado) o, alternativamente, en `global`. Por ejemplo:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Los tipos de plantilla deben respetar la estructura de carpetas correcta (es decir, `/settings/wcm/...`); de lo contrario, no se encontrarán los tipos de plantilla.

### Tipo de plantilla y grupos de dispositivos móviles {#template-type-and-mobile-device-groups-br}

El [grupos de dispositivos](/help/sites-developing/mobile.md#device-groups) se utiliza para una plantilla editable (establecida como ruta relativa de la propiedad ) `cq:deviceGroups`) definir qué dispositivos móviles están disponibles como emuladores en la [modo de diseño](/help/sites-authoring/responsive-layout.md) de la creación de páginas. Este valor se puede establecer en dos lugares:

* En el tipo de plantilla editable
* En la plantilla editable

Al crear una nueva plantilla editable, el valor se copia del tipo de plantilla en la plantilla individual. Si el valor no se establece en el tipo, se puede establecer en la plantilla. Una vez creada una plantilla, no hay herencia del tipo a la plantilla.

>[!CAUTION]
>
>El valor de `cq:deviceGroups` debe establecerse como una ruta relativa como `mobile/groups/responsive` y no como una ruta absoluta como `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>Con [plantillas estáticas](/help/sites-developing/page-templates-static.md), el valor de `cq:deviceGroups` se puede establecer en la raíz del sitio.
>
>Con las plantillas editables, este valor ahora se almacena en el nivel de plantilla y no es compatible con el nivel de raíz de página.

### Creación de tipos de plantilla {#creating-template-types}

Si ha creado una plantilla que puede servir de base a otras plantillas, puede copiar esta plantilla como un tipo de plantilla.

1. Cree una plantilla como lo haría con cualquier plantilla editable [como se documenta aquí](/help/sites-authoring/templates.md#creating-a-new-template-template-author), que servirá de base para el tipo de plantilla.
1. Con el CRXDE Lite, copie la plantilla recién creada desde el `templates` nodo a `template-types` nodo bajo el [carpeta de plantillas](/help/sites-developing/page-templates-editable.md#template-folders).
1. Elimine la plantilla del `templates` nodo bajo el [carpeta de plantillas](/help/sites-developing/page-templates-editable.md#template-folders).
1. En la copia de la plantilla que se encuentra debajo de `template-types` nodo, eliminar todo `cq:template` y `cq:templateType` propiedades de todos `jcr:content` nodos.

También puede desarrollar su propio tipo de plantilla con una plantilla editable de ejemplo como base, disponible en GitHub.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra el proyecto aem-sites-example-custom-template-type en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## Definiciones de plantilla {#template-definitions}

Se almacenan las definiciones de las plantillas editables [carpetas definidas por el usuario](/help/sites-developing/page-templates-editable.md#template-folders) (recomendado) o alternativamente en `global`. Por ejemplo:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

El nodo raíz de la plantilla es del tipo `cq:Template` con una estructura esquemática de:

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

   * **Tipo**: `String`

   * **Valor**: `draft`, `enabled` o `disabled`

### Estructura {#structure}

Define la estructura de la página resultante:

* Se combina con el contenido inicial ( `/initial`) al crear una página nueva.
* Los cambios realizados en la estructura se reflejarán en cualquier página creada con la plantilla.
* El `root` ( `structure/jcr:content/root`) define la lista de componentes que estarán disponibles en la página resultante.

   * Los componentes definidos en la estructura de la plantilla no se pueden mover ni eliminar de ninguna página resultante.
   * Una vez desbloqueado un componente, `editable` La propiedad se establece en `true`.

   * Una vez desbloqueado un componente que ya contiene contenido, este se moverá al `initial` Rama.

* El `cq:responsive` El nodo contiene definiciones para el diseño interactivo.

### Contenido inicial {#initial-content}

Define el contenido inicial que tendrá una nueva página al crearla:

* Contiene un `jcr:content` que se copia en cualquier página nueva.
* Se combina con la estructura ( `/structure`) al crear una página nueva.
* Las páginas existentes no se actualizarán si el contenido inicial cambia después de la creación.
* El `root` El nodo contiene una lista de componentes para definir qué estará disponible en la página resultante.
* Si el contenido se añade a un componente en modo de estructura y dicho componente se desbloquea posteriormente (o viceversa), este contenido se utiliza como contenido inicial.

### Diseño {#layout}

Cuándo [edición de una plantilla puede definir el diseño](/help/sites-authoring/templates.md), esto utiliza [diseño interactivo estándar](/help/sites-authoring/responsive-layout.md) que también puede ser [configurado](/help/sites-administering/configuring-responsive-layout.md).

### Políticas de contenido {#content-policies}

Las políticas de contenido (o diseño) definen las propiedades de diseño de un componente, como su disponibilidad o las dimensiones mínimas/máximas. Esto se aplica a la plantilla (y a las páginas creadas con la plantilla). Las políticas de contenido se pueden crear y seleccionar en el editor de plantillas.

* La propiedad `cq:policy`, en el `root` nodo
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Proporciona una referencia relativa a la directiva de contenido para el sistema de párrafos de la página.

* La propiedad `cq:policy`, en los nodos explícitos de componente en `root`, proporcione vínculos a las directivas para los componentes individuales.

* Las definiciones de directivas reales se almacenan en:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Las rutas de las definiciones de directivas dependen de la ruta del componente. `cq:policy` contiene una referencia relativa a la propia configuración.

>[!NOTE]
>
>Las páginas creadas a partir de plantillas editables no ofrecen el modo Diseño en el editor de páginas.
>
>El `policies` El árbol de una plantilla editable tiene la misma jerarquía que la configuración del modo de diseño de una plantilla estática en:
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>Se definió la configuración de modo de diseño de una plantilla estática por componente de página.

### Políticas de la página {#page-policies}

Las políticas de página permiten definir la variable [política de contenido](#content-policies) para la página (parsys principal), en la plantilla o en las páginas resultantes.

### Habilitar y permitir el uso de una plantilla {#enabling-and-allowing-a-template-for-use}

1. **Habilitar la plantilla**

   Para poder utilizar una plantilla, debe habilitarse mediante lo siguiente:

   * [Activación de la plantilla](/help/sites-authoring/templates.md#enablingatemplateauthor) desde el **Plantillas** consola.

   * Estableciendo la propiedad status en `jcr:content` nodo.

      * Por ejemplo, en:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Defina la propiedad:

         * Nombre: estado
         * Tipo: cadena
         * Valor: `enabled`

1. **Plantillas permitidas**

   * [Defina las rutas de plantilla permitidas en la variable **Propiedades de página**](/help/sites-authoring/templates.md#allowing-a-template-author) de la página adecuada o de la página raíz de una subrama.
   * Establezca la propiedad:
      `cq:allowedTemplates`
En el 
`jcr:content` de la rama requerida.
   Por ejemplo, con un valor de:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Páginas de contenido resultantes {#resultant-content-pages}

Páginas creadas a partir de plantillas editables:

* Se crean con un subárbol que se combina con `structure` y `initial` en la plantilla

* Tener referencias a información contenida en la plantilla y el tipo de plantilla. Esto se logra con una `jcr:content` nodo con las propiedades:

   * `cq:template`
Proporciona la referencia dinámica a la plantilla real; permite que los cambios realizados en la plantilla se reflejen en las páginas reales.

   * `cq:templateType`
Proporciona una referencia al tipo de plantilla.

![chlimage_1-71](assets/chlimage_1-71.png)

El diagrama anterior muestra cómo se interrelacionan las plantillas, el contenido y los componentes:

* Controlador - `/content/<my-site>/<my-page>`
La página resultante que hace referencia a la plantilla. El contenido controla todo el proceso. Según las definiciones, accede a la plantilla y a los componentes adecuados.

* Configuración - `/conf/<my-folder>/settings/wcm/templates/<my-template>`
El [plantilla y políticas de contenido relacionadas](#template-definitions) defina la configuración de página.

* Modelo - Paquetes OSGi [Paquetes OSGI](/help/sites-deploying/osgi-configuration-settings.md) implemente la funcionalidad.

* Ver - `/apps/<my-site>/components`
Tanto en el entorno de creación como en el de publicación, el contenido se representa mediante [componentes](/help/sites-developing/components.md).

Al procesar una página:

* **Plantillas**:

   * El `cq:template` propiedad de su `jcr:content` se hará referencia al nodo para acceder a la plantilla que corresponde a esa página.

* **Componentes**:

   * El componente de página combinará las variables `structure/jcr:content` árbol de la plantilla con el `jcr:content` árbol de la página.

   * El componente de página solo permitirá al autor editar los nodos de la estructura de la plantilla que se han marcado como editables (así como los secundarios).
   * Al procesar un componente en una página, la ruta relativa de ese componente se tomará del `jcr:content` nodo; la misma ruta bajo el `policies/jcr:content` A continuación, se buscará en el nodo de la plantilla.

      * El `cq:policy` La propiedad de este nodo apunta a la directiva de contenido real (es decir, contiene la configuración de diseño para ese componente).

      * Esto le permite tener varias plantillas que reutilizan las mismas configuraciones de directiva de contenido.
