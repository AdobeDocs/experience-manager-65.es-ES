---
title: 'Plantillas de página: editables'
description: Se han introducido plantillas editables que permiten a los usuarios que no son desarrolladores crear y editar plantillas, proporcionar plantillas que mantengan una conexión dinámica con cualquier página creada a partir de ellas y hacer que el componente de página sea más genérico
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
exl-id: dcb66b6d-d731-493e-8936-12d529f6cbde
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '3224'
ht-degree: 5%

---

# Plantillas de página: editables {#page-templates-editable}

Se han introducido plantillas editables para:

* Permitir que los autores especializados [crear y editar plantillas](/help/sites-authoring/templates.md).

   * A estos autores especializados se les llama **autores de plantillas**
   * Los autores de plantillas deben ser miembros del `template-authors` grupo.

* Proporcione plantillas que mantengan una conexión dinámica con cualquier página creada a partir de ellas. Al hacerlo, se garantiza que los cambios realizados en la plantilla se reflejen en las propias páginas.
* Consiga que el componente de página sea más genérico para que el componente de página principal se pueda utilizar sin personalización.

Con las plantillas editables, los elementos que crean una página están aislados dentro de los componentes. Puede configurar las combinaciones necesarias de componentes en una interfaz de usuario para que no necesite desarrollar un nuevo componente de página para cada variación de página.

>[!NOTE]
>
>[Plantillas estáticas](/help/sites-developing/page-templates-static.md) también están disponibles.

Este documento:

* Proporciona información general sobre la creación de plantillas editables

   * Para obtener más información, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md)

* Describe las tareas de administrador/desarrollador necesarias para crear plantillas editables
* Describe los fundamentos técnicos de las plantillas editables

Este documento supone que ya está familiarizado con la creación y edición de plantillas. Consulte el documento de creación [Creación de plantillas de página](/help/sites-authoring/templates.md), que detalla las capacidades de las plantillas editables tal y como se exponen al autor de la plantilla.

>[!NOTE]
>
>El siguiente tutorial también puede ser de interés para configurar una plantilla de página editable en un nuevo proyecto:
>[Introducción a AEM Sites, parte 2: Creación de una página base y una plantilla](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/pages-templates.html?lang=en)

## Creación de una plantilla nueva {#creating-a-new-template}

La creación de plantillas editables se realiza principalmente con la variable [consola de plantillas y editor de plantillas](/help/sites-authoring/templates.md) por un autor de plantillas. Esta sección ofrece información general sobre este proceso y a continuación una descripción de lo que ocurre a nivel técnico.

Para obtener información sobre cómo utilizar plantillas editables en un proyecto AEM, consulte [Creación de un proyecto de AEM con Lazybones](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/create-aem-project-structure-using-lazybones/m-p/186478).

Al crear una plantilla editable nueva, debe:

1. Cree un [carpeta de las plantillas](#template-folders). Esta carpeta no es obligatoria, pero es una práctica recomendada.
1. Seleccione un [tipo de plantilla](#template-type). Este tipo se copia para crear la variable [definición de plantilla](#template-definitions).

   >[!NOTE]
   >
   >Se proporciona una selección de tipos de plantillas listas para usar. También puede [crear sus propios tipos de plantilla específicos del sitio](/help/sites-developing/page-templates-editable.md#creating-template-types), si es necesario.

1. Configure la estructura, las políticas de contenido, el contenido inicial y el diseño de la nueva plantilla.

   **Estructura**

   * La estructura permite definir componentes y contenido para la plantilla.
   * Los componentes definidos en la estructura de la plantilla no se pueden mover a una página resultante ni eliminarse de ninguna página resultante.

      * Si está creando una plantilla en una carpeta personalizada fuera de la `We.Retail` contenido de muestra, puede elegir Componentes básicos o utilizar [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=es).
   * Si desea que los autores de la página puedan añadir y eliminar componentes, agregue un sistema de párrafos a la plantilla.
   * Los componentes pueden volver a desbloquearse y bloquearse para que pueda definir el contenido inicial.

   Para obtener más información sobre cómo define un autor de plantillas la estructura, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Para obtener detalles técnicos de la estructura, consulte [Estructura](/help/sites-developing/page-templates-editable.md#structure) en este documento.

   **Políticas**

   * Las políticas de contenido definen las propiedades de diseño de un componente.

      * Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas.
   * Estas políticas se aplican a la plantilla (y a las páginas creadas con la plantilla).

   Para obtener más información sobre cómo define las políticas un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Para obtener detalles técnicos sobre las políticas, consulte [Políticas de contenido](/help/sites-developing/page-templates-editable.md#content-policies) en este documento.

   **Contenido inicial**

   * Contenido inicial define el contenido que aparece cuando se crea una página por primera vez en función de la plantilla.
   * Los autores de páginas pueden editar el contenido inicial.

   Para obtener más información sobre cómo define un autor de plantillas la estructura, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   Para obtener información técnica sobre el contenido inicial, consulte [Contenido inicial](/help/sites-developing/page-templates-editable.md#initial-content) en este documento.

   **Diseño**

   * Puede definir el diseño de la plantilla para una amplia gama de dispositivos.
   * El diseño interactivo para las plantillas funciona tal como lo hace para la creación de páginas.

   Para obtener más información sobre cómo define un autor de plantillas el diseño de la plantilla, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   Para obtener información técnica sobre el diseño de la plantilla, consulte [Diseño](/help/sites-developing/page-templates-editable.md#layout) en este documento.

1. Habilite la plantilla y luego déjela para árboles de contenido específicos.

   * Una plantilla se puede habilitar o deshabilitar para que esté disponible o no disponible para los autores de páginas.
   * Una plantilla puede estar disponible o no disponible para determinadas ramas de la página.

   Para obtener más información sobre cómo un autor de plantillas habilita una plantilla, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   Para obtener información técnica sobre cómo activar una plantilla, consulte [Activación y autorización de una plantilla para nosotros](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)e en este documento

1. Utilícelo para crear páginas de contenido.

   * Al utilizar una plantilla para crear una página, no hay ninguna diferencia visible ni ninguna indicación entre las plantillas estáticas y las editables.
   * Para el autor de la página, el proceso es transparente.

   Para obtener más información sobre cómo un autor de páginas utiliza plantillas para crear una página, consulte [Creación y organización de páginas](/help/sites-authoring/managing-pages.md#templates).

   Para obtener información técnica sobre la creación de páginas con plantillas editables, consulte [Páginas de contenido resultantes](/help/sites-developing/page-templates-editable.md#resultant-content-pages) en este documento.

>[!TIP]
>
>No introduzca nunca en una plantilla información que deba internacionalizarse. Para fines de internalización, la variable [función de localización de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=es) se recomienda.

>[!NOTE]
>
>Las plantillas son herramientas útiles para optimizar el flujo de trabajo de creación de páginas. Sin embargo, demasiadas plantillas pueden saturar a los autores y hacer que la creación de páginas sea confusa. Una buena regla general es mantener el número de plantillas por debajo de 100.
>
>Adobe no recomienda tener más de 1000 plantillas debido a posibles impactos en el rendimiento.

>[!NOTE]
>
>La biblioteca de cliente del editor asume la presencia de la variable `cq.shared` espacio de nombres en páginas de contenido. Si está ausente, resulta en el error de JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined`.
>
>Todas las páginas de contenido de ejemplo contienen `cq.shared`, por lo que cualquier contenido basado en ellos se incluye automáticamente `cq.shared`. Sin embargo, si decide crear sus propias páginas de contenido desde cero sin basarlas en contenido de muestra, debe asegurarse de incluir la variable `cq.shared` espacio de nombres.
>
>Consulte [Uso de bibliotecas del lado del cliente](/help/sites-developing/clientlibs.md) para obtener más información.

## Carpetas de plantilla {#template-folders}

Para organizar las plantillas, puede utilizar las siguientes carpetas:

* **global**
* Específico del sitio Las carpetas específicas del sitio que crea para organizar las plantillas se crean con una cuenta que tiene privilegios de administrador.

>[!NOTE]
>
>Aunque puede anidar sus carpetas, cuando el usuario las vea en la **Plantillas** se presentan como una estructura plana.

En una instancia de AEM estándar, la variable **global** La carpeta existe en la consola de plantillas. Esta carpeta contiene plantillas predeterminadas y actúa como alternativa si no se encuentran políticas ni tipos de plantilla en la carpeta actual. Puede añadir las plantillas predeterminadas a esta carpeta o crear una carpeta (recomendado).

>[!NOTE]
>
>Se recomienda crear una carpeta que contenga las plantillas personalizadas y no utilizar la carpeta global.

>[!CAUTION]
>
>Las carpetas deben ser creadas por un usuario con `admin` derechos.

Los tipos de plantilla y las directivas se heredan en todas las carpetas según el siguiente orden de prioridad:

1. La carpeta actual.
1. Principal o principal de la carpeta actual.
1. `/conf/global`
1. `/apps`
1. `/libs`

Se crea una lista de todas las entradas permitidas. Si alguna configuración se superpone ( `path`/ `label`), solo se presenta al usuario la instancia más cercana a la carpeta actual.

Para crear una carpeta, haga lo siguiente:

* Programado o con CRXDE Lite
* Uso del explorador de configuración

## Uso del CRXDE Lite {#using-crxde-lite}

1. Se puede crear una nueva carpeta (en /conf) para su instancia mediante programación o con CRXDE Lite.

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

   * Valor: El título (para la carpeta) que desea que aparezca en la **Plantillas** consola.

1. En *adición* a los permisos y privilegios de creación estándar (por ejemplo, `content-authors`), asigne grupos y defina los derechos de acceso (ACL) necesarios para que sus autores puedan crear plantillas en la nueva carpeta.

   La variable `template-authors` grupo es el grupo predeterminado al que se debe asignar. Consulte la siguiente sección [ACL y grupos](/help/sites-developing/page-templates-editable.md#acls-and-groups) para obtener más información.

   Consulte [Gestión de derechos de acceso](/help/sites-administering/user-group-ac-admin.md#access-right-management) para obtener más información sobre la administración y asignación de derechos de acceso.

### Uso del explorador de configuración {#using-the-configuration-browser}

1. Vaya a **Navegación global** -> **Herramientas** > **Explorador de configuración**.

   Las carpetas existentes se muestran a la izquierda, incluido el **global** carpeta.

1. Haga clic en **Crear**.
1. En el **Crear configuración** , se deben configurar los siguientes campos:

   * **Título**: Proporcionar un título para la carpeta de configuración
   * **Plantillas editables**: Seleccionar para permitir plantillas editables dentro de esta carpeta

1. Haga clic en **Crear**

>[!NOTE]
>
>En el Explorador de configuración, puede editar la carpeta global y activar el **Plantillas editables** si desea crear plantillas dentro de esta carpeta. Sin embargo, esta práctica no es una práctica recomendada.
>
>Consulte la documentación del [Explorador de configuración](/help/sites-administering/configurations.md) para obtener más información.

### ACL y grupos {#acls-and-groups}

Después de crear las carpetas de plantillas (ya sea a través de CRXDE o con el Explorador de configuración), las ACL deben definirse para los grupos adecuados para las carpetas de plantillas para garantizar la seguridad adecuada.

Las carpetas de plantillas para la variable [`We.Retail` implementación de referencia](/help/sites-developing/we-retail.md) se puede usar como ejemplo.

#### El grupo de autores de plantillas {#the-template-authors-group}

La variable `template-authors` grupo es el grupo que se utiliza para administrar el acceso a las plantillas y viene estándar con AEM, pero está vacío. Los usuarios deben agregarse al grupo para el proyecto o sitio.

>[!CAUTION]
>
>La variable `template-authors` grupo es *only* para usuarios que deben poder crear plantillas.
>
>La edición de plantillas es potente y, si no se realiza correctamente, las plantillas existentes pueden romperse. Por lo tanto, esta función debe centrarse y solo incluir a usuarios cualificados.

La siguiente tabla detalla los permisos necesarios para la edición de plantillas.

<table>
 <tbody>
  <tr>
   <th>Ruta </th>
   <th>Función/Grupo</th>
   <th>Permisos<br /> </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Template Autores<br /> </td>
   <td>leer, escribir, replicar</td>
   <td>Creadores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en un sitio específico <code>/conf</code> espacio</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>leer</td>
   <td>El usuario web anónimo debe leer las plantillas mientras procesa una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>replicateContent los autores deben activar las plantillas de una página al activar una página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>leer, escribir, replicar</td>
   <td>Creadores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en un sitio específico <code>/conf</code> espacio</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>leer</td>
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
   <td>leer</td>
   <td>El autor de plantillas crea una plantilla basada en uno de los tipos de plantilla predefinidos.</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>ninguno</td>
   <td>El usuario web anónimo no debe acceder a los tipos de plantilla</td>
  </tr>
 </tbody>
</table>

Esta opción predeterminada `template-authors` El grupo solo cubre la configuración del proyecto, donde todas las `template-authors` los miembros pueden acceder y crear todas las plantillas. Para configuraciones más complejas, donde es necesario que varios grupos de autores de plantillas separen el acceso a las plantillas, se deben crear más grupos de autores de plantillas personalizadas. Sin embargo, los permisos para los grupos de autores de plantillas seguirían siendo los mismos.

#### Plantillas heredadas en /conf/global {#legacy-templates-under-conf-global}

No almacene plantillas en `/conf/global`. Sin embargo, para algunas instalaciones heredadas, puede que todavía haya plantillas en esta ubicación. *Solo* en estas situaciones heredadas, debería `/conf/global` las rutas de acceso se deben configurar explícitamente.

<table>
 <tbody>
  <tr>
   <th>Ruta </th>
   <th>Función/Grupo</th>
   <th>Permisos<br /> </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>Template Autores</td>
   <td>leer, escribir, replicar</td>
   <td>Creadores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>leer</td>
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
   <td>Creadores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>leer</td>
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
   <td>leer</td>
   <td>El autor de plantillas crea una plantilla basada en uno de los tipos de plantilla predefinidos</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>ninguno</td>
   <td>El usuario web anónimo no debe acceder a los tipos de plantilla</td>
  </tr>
 </tbody>
</table>

## Tipo de plantilla {#template-type}

Al crear una plantilla, especifique un tipo de plantilla:

* Los tipos de plantilla proporcionan plantillas para una plantilla. Al crear una plantilla, se utiliza la estructura y el contenido inicial del tipo de plantilla seleccionado para crear la plantilla.

   * El tipo de plantilla se copia para crear la plantilla.
   * Una vez que se ha producido la copia, la única conexión entre la plantilla y el tipo de plantilla es una referencia estática con fines informativos.

* Los tipos de plantilla le permiten definir:

   * Tipo de recurso del componente de página.
   * La directiva del nodo raíz, que define los componentes permitidos en el editor de plantillas.
   * Adobe recomienda definir los puntos de interrupción para la cuadrícula adaptable y la configuración del emulador móvil en el tipo de plantilla. Este paso es opcional, ya que la configuración también se puede definir en la plantilla individual (consulte [Tipo de plantilla y grupos de dispositivos móviles](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p)).

* AEM ofrece una pequeña selección de tipos de plantillas listos para usar, como Página HTML5 y Página de formulario adaptable.

   * Se proporcionan ejemplos adicionales como parte del [`We.Retail`](/help/sites-developing/we-retail.md) contenido de muestra.

* Los desarrolladores suelen definir los tipos de plantilla.

Los tipos de plantilla predeterminados se almacenan en:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>No cambie nada en la variable `/libs` ruta. El motivo es que el contenido de `/libs` se sobrescribe la próxima vez que actualice la instancia (y se puede sobrescribir al aplicar una corrección o un paquete de funciones).

Los tipos de plantilla específicos del sitio se deben almacenar en una ubicación comparable de:

* `/apps/settings/wcm/template-types`

Las definiciones de los tipos de plantillas personalizadas deben almacenarse en carpetas definidas por el usuario (recomendadas) o, alternativamente, en `global`. Por ejemplo:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Los tipos de plantilla deben respetar la estructura de carpetas correcta (es decir, `/settings/wcm/...`); de lo contrario, no se encuentran los tipos de plantilla.

### Tipo de plantilla y grupos de dispositivos móviles {#template-type-and-mobile-device-groups-br}

La variable [grupos de dispositivos](/help/sites-developing/mobile.md#device-groups) se utiliza para una plantilla editable (se establece como ruta relativa de la propiedad) `cq:deviceGroups`) defina qué dispositivos móviles están disponibles como emuladores en la variable [modo de diseño](/help/sites-authoring/responsive-layout.md) de creación de páginas. Este valor se puede configurar en dos lugares:

* En el tipo de plantilla editable
* En la plantilla editable

Al crear una nueva plantilla editable, el valor se copia del tipo de plantilla a la plantilla individual. Si el valor no se define en el tipo , se puede configurar en la plantilla . Una vez creada una plantilla, no hay herencia del tipo a la plantilla.

>[!CAUTION]
>
>El valor de `cq:deviceGroups` debe configurarse como una ruta relativa como `mobile/groups/responsive` y no como una ruta absoluta como `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>con [plantillas estáticas](/help/sites-developing/page-templates-static.md), el valor de `cq:deviceGroups` se puede establecer en la raíz del sitio.
>
>Con las plantillas editables, este valor ahora se almacena en el nivel de plantilla y no se admite en el nivel de raíz de la página.

### Creación de tipos de plantilla {#creating-template-types}

Si ha creado una plantilla que puede servir de base para otras plantillas, puede copiar esta plantilla como un tipo de plantilla.

1. Cree una plantilla como lo haría con cualquier plantilla editable [tal como se documenta aquí](/help/sites-authoring/templates.md#creating-a-new-template-template-author), que puede servir de base para su tipo de plantilla.
1. Con el CRXDE Lite , copie la plantilla recién creada de la `templates` al nodo `template-types` en el nodo [carpeta de plantillas](/help/sites-developing/page-templates-editable.md#template-folders).
1. Elimine la plantilla de la sección `templates` en el nodo [carpeta de plantillas](/help/sites-developing/page-templates-editable.md#template-folders).
1. En la copia de la plantilla que se encuentra en el `template-types` nodo, eliminar todo `cq:template` y `cq:templateType` propiedades de todas `jcr:content` nodos.

También puede desarrollar su propio tipo de plantilla utilizando una plantilla editable de ejemplo como base, disponible en GitHub.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abra un proyecto de tipo aem-sites-example-custom-template en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Descargue el proyecto como [un archivo ZIP](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/zip/refs/heads/master)

## Definiciones de plantillas {#template-definitions}

Se almacenan las definiciones de las plantillas editables [carpetas definidas por el usuario](/help/sites-developing/page-templates-editable.md#template-folders) (recomendado) o alternativamente en `global`. Por ejemplo:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

El nodo raíz de la plantilla es del tipo `cq:Template` con una estructura esquelética de:

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

   * **Valor**: `draft`, `enabled`o `disabled`

### Estructura {#structure}

Define la estructura de la página resultante:

* Se combina con el contenido inicial ( `/initial`) al crear una página.
* Los cambios realizados en la estructura se reflejan en cualquier página creada con la plantilla.
* La variable `root` ( `structure/jcr:content/root`) define la lista de componentes que están disponibles en la página resultante.

   * Los componentes definidos en la estructura de la plantilla no se pueden mover ni eliminar de ninguna página resultante.
   * Una vez desbloqueado un componente, la variable `editable` la propiedad se establece en `true`.

   * Después de desbloquear un componente que ya contiene contenido, este contenido se mueve al `initial` rama.

* La variable `cq:responsive` contiene definiciones para el diseño interactivo.

### Contenido inicial {#initial-content}

Define el contenido inicial que tiene una página nueva al crearla:

* Contiene un `jcr:content` que se copia en cualquier página nueva.
* Se combina con la estructura ( `/structure`) al crear una página.
* Las páginas existentes se actualizan si el contenido inicial se cambia después de la creación.
* La variable `root` contiene una lista de componentes para definir qué están disponibles en la página resultante.
* Si el contenido se añade a un componente en modo de estructura y ese componente se desbloquea (o, a la inversa), este contenido se utiliza como contenido inicial.

### Diseño {#layout}

When [editar una plantilla, puede definir el diseño](/help/sites-authoring/templates.md), esta práctica utiliza [diseño adaptable estándar](/help/sites-authoring/responsive-layout.md) que también puede [configurado](/help/sites-administering/configuring-responsive-layout.md).

### Políticas de contenido {#content-policies}

Las políticas de contenido (o diseño) definen las propiedades de diseño de un componente, como su disponibilidad o dimensiones mínimas/máximas. Estas políticas se aplican a la plantilla (y a las páginas creadas con la plantilla). Las políticas de contenido se pueden crear y seleccionar en el editor de plantillas.

* La propiedad `cq:policy`, en el `root` node
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Proporciona una referencia relativa a la política de contenido para el sistema de párrafos de la página.

* La propiedad `cq:policy`, en los nodos explícitos del componente debajo de `root`, proporcione vínculos a las políticas de los componentes individuales.

* Las definiciones de directiva reales se almacenan en:
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Las rutas de las definiciones de políticas dependen de la ruta del componente. La variable `cq:policy` contiene una referencia relativa a la configuración misma.

>[!NOTE]
>
>Las páginas creadas a partir de plantillas editables no ofrecen un modo de diseño en el editor de páginas.
>
>La variable `policies` el árbol de una plantilla editable tiene la misma jerarquía que la configuración del modo de diseño de una plantilla estática en:
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>La configuración del modo de diseño de una plantilla estática se definió por componente de página.

### Políticas de la página {#page-policies}

Las políticas de página permiten definir la variable [política de contenido](#content-policies) para la página (parsys principal), en la plantilla o en las páginas resultantes.

### Activación y autorización de una plantilla para su uso {#enabling-and-allowing-a-template-for-use}

1. **Habilitar la plantilla**

   Para poder utilizar una plantilla, debe habilitarla:

   * [Activación de la plantilla](/help/sites-authoring/templates.md#enablingatemplateauthor) de la variable **Plantillas** consola.

   * Configuración de la propiedad de estado en la variable `jcr:content` nodo .

      * Por ejemplo, en:
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Defina la propiedad:

         * Nombre: status
         * Tipo: cadena
         * Valor: `enabled`

1. **Plantillas permitidas**

   * [Defina las rutas de plantilla permitidas en la variable **Propiedades de página**](/help/sites-authoring/templates.md#allowing-a-template-author) de la página o página raíz adecuada de una subrama.
   * Establezca la propiedad:
      `cq:allowedTemplates`
En el 
`jcr:content` nodo de la rama requerida.
   Por ejemplo, con un valor de:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Páginas de contenido resultantes {#resultant-content-pages}

Páginas creadas a partir de plantillas editables:

* Se crean con un subárbol que se combina a partir de `structure` y `initial` en la plantilla

* Tienen referencias a información contenida en la plantilla y el tipo de plantilla. Puede lograr esta funcionalidad con un `jcr:content` con las propiedades:

   * `cq:template`
Proporciona la referencia dinámica a la plantilla real; permite que los cambios realizados en la plantilla se reflejen en las páginas reales.

   * `cq:templateType`
Proporciona una referencia al tipo de plantilla.

![chlimage_1-71](assets/chlimage_1-71.png)

El diagrama anterior muestra cómo las plantillas, el contenido y los componentes se interrelacionan:

* Controlador - `/content/<my-site>/<my-page>`
La página resultante que hace referencia a la plantilla. El contenido controla todo el proceso. Según las definiciones, accede a la plantilla y los componentes adecuados.

* Configuración - `/conf/<my-folder>/settings/wcm/templates/<my-template>`
La variable [plantilla y políticas de contenido relacionadas](#template-definitions) defina la configuración de página.

* Modelo : los paquetes OSGi [Paquetes OSGI](/help/sites-deploying/osgi-configuration-settings.md) implemente la funcionalidad .

* Ver - `/apps/<my-site>/components`
Tanto en el entorno de autor como de publicación, el contenido se representa mediante [componentes](/help/sites-developing/components.md).

Al procesar una página:

* **Plantillas**:

   * La variable `cq:template` propiedad de su `jcr:content` se hace referencia al nodo para acceder a la plantilla que corresponde a esa página.

* **Componentes**:

   * El componente de página combina el `structure/jcr:content` árbol de la plantilla con la variable `jcr:content` de la página.

   * El componente de página solo permite al autor editar los nodos de la estructura de la plantilla que se han marcado como editables (y los secundarios).
   * Al procesar un componente en una página, la ruta relativa de dicho componente se toma de la `jcr:content` nodo; la misma ruta debajo de `policies/jcr:content` a continuación, se busca en el nodo de la plantilla.

      * La variable `cq:policy` La propiedad de este nodo apunta a la política de contenido real (es decir, contiene la configuración de diseño para ese componente).

      * Esta funcionalidad le permite tener varias plantillas que reutilizan las mismas configuraciones de directiva de contenido.
