---
title: 'Creación de plantillas de página  '
seo-title: 'Creación de plantillas de página  '
description: La plantilla define la estructura de la página resultante y con el editor de plantillas, crear y mantener plantillas ya no es una tarea solo de desarrollador
seo-description: La plantilla define la estructura de la página resultante y con el editor de plantillas, crear y mantener plantillas ya no es una tarea solo de desarrollador
uuid: e14cd298-289f-43f0-aacb-314ed5d56c12
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: b53348ca-fc50-4e7d-953d-b4c03a5025bb
docset: aem65
exl-id: 363b8fab-6ce7-4338-8478-3f25f2a1f117
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '4901'
ht-degree: 95%

---

# Creación de plantillas de página  {#creating-page-templates}

Al crear una página, debe seleccionar una plantilla, que se utilizará como base para crear la página nueva. La plantilla define la estructura de la página resultante, cualquier contenido inicial y los componentes que se pueden utilizar.

Con el **Editor de plantillas**, la creación y el mantenimiento de plantillas ya no es una tarea exclusiva para desarrolladores. También puede participar un tipo de usuario avanzado, que se denomina **autor de la plantilla**. Los desarrolladores siguen necesitando configurar el entorno, crear bibliotecas de clientes y crear los componentes que se van a utilizar, pero una vez que estos conceptos básicos están establecidos, el **autor de la plantilla** tiene la flexibilidad de crear y configurar plantillas sin un proyecto de desarrollo.

La **Consola de plantillas** permite a los autores de plantillas:

* Crear una plantilla nueva o copiar una plantilla existente.
* Administrar el ciclo de vida de la plantilla.

El **Editor de plantillas** permite a los autores de plantillas:

* Añadir componentes a la plantilla y colocarlos en una cuadrícula interactiva.
* Preconfigurar los componentes. 
* Definir qué componentes se pueden editar en las páginas creadas con la plantilla.

En este documento se explica cómo un **autor de plantillas** puede utilizar la consola y el editor de plantillas para crear y gestionar plantillas editables.

Para obtener información detallada acerca de cómo funcionan las plantillas editables en un nivel técnico, consulte el documento para desarrolladores [Plantillas de página: editables](/help/sites-developing/page-templates-editable.md).

>[!NOTE]
>
>El **Editor de plantillas** no admite la segmentación directamente en el nivel de plantilla. Las páginas creadas a partir de una plantilla editable pueden estar segmentadas, pero esto no es posible para las plantillas en sí.

>[!CAUTION]
>
>Las páginas y plantillas creadas con la **Consola de plantillas** no están pensadas para utilizarse con la IU clásica y este uso no es compatible.

## Antes de comenzar {#before-you-start}

>[!NOTE]
>
>Un administrador debe configurar una carpeta de plantillas en el **Navegador de opciones de configuración** y aplicar los permisos adecuados para que un autor de una plantilla pueda crear una plantilla en esa carpeta.

Antes de comenzar, es importante tener en cuenta los puntos siguientes:

* La creación de una plantilla nueva requiere colaboración. Por este motivo, para cada tarea se indica la [Función.](#roles)

* En función de cómo esté configurada su instancia, podría resultar útil saber que AEM ahora proporciona [ dos tipos básicos de plantilla](/help/sites-authoring/templates.md#editable-and-static-templates). Esto no afecta a cómo realmente [utiliza una plantilla para crear una página](#using-a-template-to-create-a-page), pero afecta al tipo de plantilla que puede crear y el modo en que una página se relaciona con su plantilla.

### Funciones {#roles}

La creación de una nueva plantilla mediante la **consola Plantillas** y el **Editor de plantillas** requiere la colaboración entre las siguientes funciones:

* **Administrador**:

   * Crea una nueva carpeta de plantillas y requiere derechos `admin` (de administración).

   * A menudo, un desarrollador también puede realizar estas tareas.

* **Desarrollador**:

   * Se centra en los detalles técnicos/internos.
   * Debe tener experiencia en el entorno de desarrollo.
   * Proporciona al autor de plantillas la información necesaria.

* **Autor de plantillas**:

   * Se trata de un autor determinado que es miembro del grupo `template-authors`.

      * Esto le asigna los privilegios y los permisos necesarios.
   * Puede configurar el uso de componentes y otros detalles de alto nivel que requieren:

      * Un cierto grado de conocimiento técnico

         * Por ejemplo, el uso de patrones al definir los trazados.
      * Información técnica del desarrollador.



Debido a la naturaleza de algunas tareas, como la creación de una carpeta, es necesario un entorno de desarrollo, lo que requiere conocimiento o experiencia.

Las tareas descritas en este documento se enumeran con la función responsable de llevarlas a cabo.

### Plantillas editables y estáticas {#editable-and-static-templates}

Actualmente, AEM ofrece dos tipos básicos de plantillas:

* [Plantillas editables](/help/sites-authoring/templates.md#creatingandmanagingnewtemplates)

   * Los autores de plantillas las pueden [crear](#creatinganewtemplate) y [editar](#editingatemplate) con la consola y el editor de **plantillas**. A la consola de **Plantillas** se accede en la sección **General** de la consola de **Herramientas**.

   * Después de crear la página nueva, se mantiene una conexión dinámica entre la página y la plantilla. Esto significa que los cambios realizados en la estructura o el contenido bloqueado de la plantilla se reflejarán en cualquier página creada con esa plantilla. Los cambios en el contenido desbloqueado (es decir, inicial) no se reflejarán.
   * Utilice las políticas de contenido, que puede definir en el editor de plantillas, para mantener las propiedades del diseño. El modo de diseño del editor de páginas ya no se utiliza para las plantillas editables.

* Plantillas estáticas

   * Las plantillas estáticas han estado disponibles en diversas versiones de AEM.
   * Las [proporcionan los desarrolladores](/help/sites-developing/page-templates-static.md), por lo que los autores no las pueden crear ni editar.
   * Se copian para crear la página nueva, pero no existe ninguna conexión dinámica después de esto (aunque el nombre de plantilla se registra a título informativo).
   * Utilice el [modo de diseño](/help/sites-authoring/default-components-designmode.md) para mantener las propiedades del diseño.
   * Como editar plantillas estáticas es tarea exclusiva de un desarrollador, consulte el documento para desarrolladores [Plantillas de página: estáticas](/help/sites-developing/page-templates-static.md) para obtener más información.

Por definición, la consola y el editor de plantillas solo permiten la creación y edición de plantillas editables. Por tanto, el documento se centra exclusivamente en plantillas editables.

### Uso de una plantilla para crear una página {#using-a-template-to-create-a-page}

Al utilizar una plantilla [para crear una página nueva](/help/sites-authoring/managing-pages.md#creating-a-new-page), no existe ninguna diferencia visible ni ninguna indicación entre las plantillas estáticas y las editables. Para el autor de la página, el proceso es transparente.

## Creación y gestión de plantillas {#creating-and-managing-templates}

Al crear una nueva plantilla editable, realiza estas acciones:

* Usa la consola de **Plantillas**. Se encuentra disponible en la sección **General** de la consola de **Herramientas**.

   * O directamente en: [https://localhost:4502/libs/wcm/core/content/sites/templates.html/conf](https://localhost:4502/libs/wcm/core/content/sites/templates.html/conf)

* Puede [crear una carpeta para las plantillas](#creating-a-template-folder-admin), si lo necesita.
* [Crea una plantilla nueva](#creatinganewtemplateauthor), que inicialmente estará vacía.

* [Define propiedades adicionales](#definingtemplatepropertiesauthor) para la plantilla, si así lo necesita.
* [Edita la plantilla](#editingtemplates) para definir los elementos siguientes:

   * [Estructura](#editingatemplatestructureauthor): contenido predefinido que no se puede cambiar en las páginas creadas con la plantilla.
   * [Contenido inicial](#editing-a-template-initial-content-author): contenido predefinido que se puede cambiar en las páginas creadas con la plantilla.
   * [Diseño](#editingatemplatelayoutauthor): para una amplia gama de dispositivos.
   * [Estilos](/help/sites-authoring/style-system.md): defina los estilos que se van a utilizar con la plantilla y sus componentes.

* [Habilita la plantilla](#enablingatemplateauthor) para utilizarla al crear una página.
* [Autoriza la plantilla](#allowing-a-template-author) para la página o rama solicitada de su sitio web.
* [Publica la plantilla](#publishingatemplateauthor) para que esté disponible en el entorno de publicación.

>[!NOTE]
>
>A menudo, las **plantillas permitidas** se predefinen cuando su sitio web se configura inicialmente.

>[!CAUTION]
>
>No introduzca nunca en una plantilla información que deba [internacionalizarse. ](/help/sites-developing/i18n.md) Para fines de internalización, se recomiendan las [características de localización de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html).

### Creación de una carpeta de plantillas: administrador {#creating-a-template-folder-admin}

Se debe crear una carpeta de plantillas para su proyecto que contenga las plantillas específicas del proyecto. Es una tarea de administración que se describe en el documento [Plantillas de página: editables](/help/sites-developing/page-templates-editable.md#template-folders).

### Creación de una plantilla nueva: autor de plantillas {#creating-a-new-template-template-author}

1. Abra la **Consola de plantillas** (que encontrará en **Herramientas ->** **General**) y navegue a la carpeta requerida.

   >[!NOTE]
   >
   >En una instancia estándar de AEM, la carpeta **Global** ya existe en la consola de plantillas. Contiene plantillas predeterminadas y actúa como alternativa en caso de que no se encuentre ninguna política ni ningún tipo de plantilla en la carpeta actual.
   >
   >
   >Una práctica recomendada es utilizar una [carpeta de plantillas creada para su proyecto](/help/sites-developing/page-templates-editable.md#template-folders).

1. Seleccione **Crear** y, a continuación, **Crear plantilla** para abrir el asistente.

1. Elija un **Tipo de plantilla** y seleccione **Siguiente**.

   >[!NOTE]
   >
   >Los tipos de plantilla son diseños de plantilla predefinidos y se pueden concebir como plantillas para una plantilla. Los responsables de predefinirlos son los desarrolladores o el administrador del sistema. Encontrará más información en el documento para desarrolladores [Plantillas de página: editables](/help/sites-developing/page-templates-editable.md#template-type).

1. Complete los **detalles de la plantilla**:

   * **Nombre de la plantilla**
   * **Descripción**

1. Seleccione **Crear**. Se mostrará una confirmación; seleccione **Abrir**[](#editingatemplate) para comenzar a editar la plantilla o **Listo** para volver a la consola de plantillas.

   >[!NOTE]
   >
   >Cuando se crea una plantilla nueva, se marca como **Borrador** en la consola; esto indica que aún no está disponible para que los autores de páginas la utilicen.

### Definición de las propiedades de la plantilla: autor de plantillas   {#defining-template-properties-template-author}

Una plantilla puede tener las propiedades siguientes:

* Imagen

   * La imagen que se utilizará como [miniatura de la plantilla](/help/sites-authoring/templates.md#template-thumbnail-image) para ayudar en la selección, como en el asistente de Crear página.

      * Se puede cargar
      * Se puede generar de acuerdo con el contenido de la plantilla

* Título

   * Un título que se utiliza para identificar la plantilla como en el asistente de **Crear página**.

* Descripción

   * Una descripción opcional para proporcionar más información sobre la plantilla y su uso, que puede verse, por ejemplo, en el asistente de **Crear página**.

Para ver o editar las propiedades:

1. En la **Consola de plantillas**, seleccione la plantilla.
1. Para abrir el cuadro de diálogo, seleccione **Ver propiedades** en la barra de herramientas o en las opciones rápidas.
1. Ahora puede ver o editar las propiedades de la plantilla.

>[!NOTE]
>
>Las plantillas son herramientas útiles para optimizar el flujo de trabajo de creación de páginas. Sin embargo, demasiadas plantillas pueden sobrecargar a los autores y hacer que la creación de páginas sea confusa. Una buena regla general es mantener el número de plantillas por debajo de 100.
>
>Adobe no recomienda tener más de 1000 plantillas debido a posibles impactos en el rendimiento.

>[!NOTE]
>
>El estado de una plantilla (borrador, activada o desactivada) se indica en la consola.

#### Imagen de miniatura de plantilla {#template-thumbnail-image}

Para definir la miniatura de plantilla:

1. Edite las propiedades de la plantilla.
1. Elija si desea cargar una miniatura o que se genere a partir del contenido de la plantilla.

   * Si desea cargar una miniatura, toque o haga clic en **Cargar imagen**
   * Si desea generar una miniatura, toque o haga clic en **Generar previsualización**

1. Para ambos métodos, se mostrará una vista previa de la miniatura.

   Si el resultado no es satisfactorio, toque o haga clic en **Borrar** para cargar otra imagen o volver a generar la miniatura.

1. Cuando esté satisfecho con la miniatura, toque o haga clic en **Guardar y cerrar**.

### Activación y autorización de una plantilla: autor de plantillas   {#enabling-and-allowing-a-template-template-author}

Para poder utilizar una plantilla al crear una página, debe:

* [Activar la plantilla](#enablingatemplate) para que esté disponible para utilizarla al crear páginas.
* [Permitir que la plantilla](#allowingatemplate) especifique las ramas de contenido en las que esta se puede utilizar.

#### Activación de una plantilla: autor de plantillas {#enabling-a-template-template-author}

Una plantilla puede estar activada o desactivada para que esté disponible o no disponible en el asistente de **Crear página**.

>[!CAUTION]
>
>Una vez activada una plantilla, se mostrará una advertencia cuando un autor de plantillas comience a actualizar la plantilla aún más. El objetivo de esto consiste en informar al usuario de que es posible que la plantilla se utilice como referencia, por lo que cualquier cambio podría afectar a las páginas en que se haga referencia a la plantilla.

1. En la **Consola de plantillas**, seleccione la plantilla.
1. Seleccione **Activar** o **Desactivar** en la barra de herramientas y, de nuevo, en el cuadro de diálogo de confirmación.
1. Ahora puede usar la plantilla al [crear una página nueva](/help/sites-authoring/managing-pages.md#creating-a-new-page), aunque probablemente desee [editar la plantilla](#editingatemplate) según sea necesario.

>[!NOTE]
>
>El estado de una plantilla (borrador, activada o desactivada) se indica en la consola.

#### Autorización de una plantilla: autor {#allowing-a-template-author}

Una plantilla puede estar disponible o no disponible para determinadas ramas de la página.

1. Abra [Propiedades de la página](/help/sites-authoring/editing-page-properties.md) para la página raíz de la rama en que desea que la plantilla esté disponible.

1. Abra la pestaña **Avanzadas**.

1. En **Configuración de la plantilla**, utilice **Agregar campo** para especificar la(s) ruta(s) a su(s) plantilla(s).

   La ruta puede ser explícita o utilizar patrones. Por ejemplo:

   `/conf/<your-folder>/settings/wcm/templates/.*`

   El orden de las rutas es irrelevante, ya que todas se analizarán y se recuperarán todas las plantillas que se encuentren.

   >[!NOTE]
   >
   >Si la lista **Plantillas permitidas** se deja vacía, el árbol ascenderá hasta que se encuentre un valor o una lista.
   >
   >
   >Consulte [Disponibilidad de plantillas](/help/sites-developing/templates.md#template-availability): los principios para las plantillas permitidas siguen siendo los mismos.

1. Haga clic en **Guardar** para guardar los cambios realizados en las propiedades de la página.

>[!NOTE]
>
>Con frecuencia, las plantillas permitidas se predefinen para todo el sitio al configurarlo.

### Publicación de una plantilla: autor de plantillas {#publishing-a-template-template-author}

Puesto que la plantilla se toma como referencia cuando se representa la página, la plantilla completamente configurada debe publicarse para que esté disponible en el entorno de publicación.

1. En la **Consola de plantillas**, seleccione la plantilla.
1. Seleccione **Publicar** en la barra de herramientas para abrir el asistente.
1. Seleccione las **Políticas de contenido** que deben publicarse en combinación.

1. Seleccione **Publicar** en la barra de herramientas para completar la acción.

## Edición de plantillas: autores de plantillas   {#editing-templates-template-authors}

Al crear o editar una plantilla, hay distintas proporciones que se pueden definir. Editar plantillas es similar a crear páginas.

Las proporciones siguientes de una plantilla se pueden editar:

* [Estructura](#editingatemplatestructure)

   Los autores de la página no pueden mover/quitar de las páginas resultantes los componentes añadidos aquí. Si desea que los autores de la página puedan añadir y quitar componentes de las páginas resultantes, debe añadir un sistema de párrafos a la plantilla.

   Cuando los componentes se bloquean, puede añadir contenido, que los autores de la página no pueden editar. Puede desbloquear componentes para poder definir el [Contenido inicial](#editingatemplateinitialcontent).

   >[!NOTE]
   >
   >En el modo de estructura, todos los componentes que son la raíz de un componente desbloqueado no se pueden mover, cortar ni eliminar.

* [Contenido inicial](#editingatemplateinitialcontent)

   Cuando un componente se ha desbloqueado, puede definir el contenido inicial que se copiará a las páginas resultantes, creadas a partir de la plantilla. Estos componentes desbloqueados se pueden editar en las páginas resultantes.

   >[!NOTE]
   >
   >En el modo de **Contenido inicial**, así como en las páginas resultantes, cualquier componente desbloqueado que tenga una raíz accesible (es decir, componentes dentro de un contenedor de diseño) se puede eliminar.

* [Diseño](#editingatemplatelayout)

   Aquí puede predefinir el diseño de la plantilla para los formatos de dispositivo requeridos. El modo de **Diseño** para la creación de plantillas tiene la misma funcionalidad que el modo de [**Diseño** para la creación de páginas](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode).

* [Políticas de la página](#editingatemplatepagepolicies)

   En las políticas de la página, puede conectar las políticas predefinidas de página a la página. Estas políticas de la página definen las diversas configuraciones de diseño.

* [Estilos](/help/sites-authoring/style-system.md)

   El sistema de estilos permite a un autor de plantillas definir clases de estilos en la política de contenido de un componente, de modo que un autor de contenido puede seleccionarlos al editar el componente en una página. Estos estilos pueden ser variaciones visuales alternativas de un componente, lo que hacen que este sea más flexible.

   Consulte la [documentación del sistema de estilos](/help/sites-authoring/style-system.md) para obtener más información.

El selector **Modo** de la barra de herramientas le permite seleccionar y editar la proporción adecuada de la plantilla:

* [Estructura](#editingatemplatestructure)
* [Contenido inicial](#editingatemplateinitialcontent)
* [Diseño](#editingatemplatelayout)

![chlimage_1-135](assets/chlimage_1-133.png)

Mientras que la opción **Política de la página** del menú **Información de página** le permite [seleccionar las políticas de la página requeridas](#editingatemplatepagepolicies):

![screen_shot_2018-03-23at120604](assets/screen_shot_2018-03-23at120604.png)

>[!CAUTION]
>
>Si un autor comienza a editar una plantilla que ya se ha activado, se mostrará una advertencia. El objetivo de esto consiste en informar al usuario de que es posible que la plantilla se utilice como referencia, por lo que cualquier cambio podría afectar a las páginas en que se haga referencia a la plantilla.

### Edición de una plantilla: estructura, autor de plantillas {#editing-a-template-structure-template-author}

En el modo de **Estructura**, puede definir los componentes y el contenido de la plantilla, así como la política de la plantilla y sus componentes.

* Los componentes definidos en la estructura de la plantilla no se pueden mover a una página resultante ni eliminarse de ninguna página resultante.
* Si desea que los autores de la página puedan añadir y quitar componentes, añada un sistema de párrafos a la plantilla.
* Los componentes pueden volver a desbloquearse y bloquearse para que pueda definir el [contenido inicial](#editingatemplateinitialcontent).

* Se definen las políticas de diseño para los componentes y la página.

![screen_shot_2018-03-23at120819](assets/screen_shot_2018-03-23at120819.png)

En el modo de **Estructura** del editor de plantillas:

* **Añada componentes**

   Hay varias formas de añadir componentes a la plantilla:

   * Desde el navegador **Componentes** del panel lateral.
   * Mediante la opción **Insertar componente** (icono **+**), disponible en la barra de herramientas de los componentes que ya están en la plantilla o el cuadro **Arrastre los componentes aquí**.

   * Arrastrando un recurso (desde el navegador **Recursos** del panel lateral) directamente a la plantilla para generar el componente apropiado allí mismo.

   Una vez añadido, cada componente presenta las marcas siguientes:

   * Un borde
   * Un marcador para mostrar el tipo de componente
   * Un marcador para mostrar cuándo el componente se ha desbloqueado

   >[!NOTE]
   >
   >Al añadir un componente **Título** predefinido a la plantilla, contendrá la **estructura** de texto predeterminado.
   >
   >
   >Si lo cambia, y añade su propio texto, este texto actualizado se utilizará cuando se cree una página a partir de la plantilla.
   >
   >
   >Si deja el texto predeterminado (estructura), el título tendrá de manera predeterminada el nombre de la página siguiente.

   >[!NOTE]
   >
   >Aunque no sea una operación idéntica, la adición de componentes y recursos a una plantilla tiene muchas similitudes con acciones similares que se llevan a cabo al [crear páginas](/help/sites-authoring/editing-content.md).

* **Acciones de componente**

   Realice acciones con los componentes una vez añadidos a la plantilla. Cada instancia individual tiene una barra de herramientas que le permite acceder a las acciones disponibles; la barra de herramientas depende del tipo de componente.

   ![screen_shot_2018-03-23at120909](assets/screen_shot_2018-03-23at120909.png)

   También puede depender de las acciones realizadas, por ejemplo, cuando se ha asociado una política al componente, el icono de configuración de diseño está disponible.

* **Editar y configurar**

   Con estas dos acciones, puede añadir contenido a los componentes.

* **Borde para indicar la estructura**

   Al trabajar en el modo de **Estructura**, un borde naranja indica el componente seleccionado actualmente. Una línea discontinua también indica el componente raíz.

   Por ejemplo, en la captura de pantalla siguiente, el componente **Texto** está seleccionado, dentro de un **contenedor de diseño** (cuadrícula interactiva).

   ![chlimage_1-134](assets/chlimage_1-134.png)

* **Política y propiedades (general)**

   Las políticas de contenido (o diseño) definen las propiedades de diseño de un componente. Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas. Esto se aplica a la plantilla (y a las páginas creadas con la plantilla).

   Cree una política de contenido, o seleccione una existente, para un componente. Esto le permite definir los detalles del diseño.

   ![chlimage_1-135](assets/chlimage_1-135.png) ![chlimage_1-136](assets/chlimage_1-136.png)

   La ventana de configuración se divide en dos.

   * En la parte izquierda del cuadro de diálogo, debajo de la sección **Política**, puede seleccionar una política existente.
   * En el lado derecho del cuadro de diálogo, debajo de la sección **Propiedades**, puede establecer las propiedades específicas del tipo de componente.

   Las propiedades disponibles dependen del componente seleccionado. Por ejemplo, en el caso de un componente de texto, las propiedades definen las opciones de copiar y pegar, las opciones de formato y el estilo de párrafo entre otras opciones.

   ***Política***

   Las políticas de contenido (o diseño) definen las propiedades de diseño de un componente. Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas. Esto se aplica a la plantilla (y a las páginas creadas con la plantilla).

   En **Política**, puede seleccionar una política existente para aplicarla al componente a través de la lista desplegable.

   ![chlimage_1-137](assets/chlimage_1-137.png)

   Para añadir una política nueva, seleccione el botón de adición situado junto a la lista desplegable **Seleccionar política.** Se debe proporcionar un título nuevo en el campo **Título de la política**.

   ![chlimage_1-138](assets/chlimage_1-138.png)

   La política existente seleccionada en la lista desplegable **Seleccionar política** se puede copiar como una política nueva mediante el botón de copia situado al lado de la lista desplegable. Se debe proporcionar un título nuevo en el campo **Título de la política**. De forma predeterminada, la política copiada tendrá el título **Copia de X**, en que X es el título de la política copiada.

   ![chlimage_1-139](assets/chlimage_1-139.png)

   En el campo **Descripción de la política**, se ofrece de manera opcional una descripción de la política.

   En la sección **Otras plantillas que también usan la política seleccionada**, puede ver con facilidad las otras plantillas que usan la política seleccionada en la lista desplegable **Seleccionar política**.

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >Si se añaden diversos componentes del mismo tipo como contenido inicial, la misma política se aplica a todos los componentes. Esto refleja el mismo mecanismo de restricción en [**Modo diseño** para las plantillas estáticas](/help/sites-authoring/default-components-designmode.md).

   ***Propiedades***

   En el encabezamiento **Propiedades**, puede definir la configuración del componente. El encabezamiento tiene dos pestañas:

   * Principal
   * Características

   *Principal*

   En la pestaña **Principal**, se definen las opciones de configuración más importantes del componente.

   Por ejemplo, para un componente de imagen, las anchuras permitidas se pueden definir junto con la activación de la carga diferida.

   Si una configuración permite múltiples configuraciones, toque o haga clic en el botón **Añadir** para añadir otra configuración.

   ![chlimage_1-141](assets/chlimage_1-141.png)

   Para quitar una configuración, toque o haga clic en el botón **Eliminar** situado a la derecha de la configuración.

   Para quitar una configuración, toque o haga clic en el botón** Eliminar**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

   *Características*

   La pestaña **Características** le permite habilitar o deshabilitar características adicionales del componente.

   Por ejemplo, para un componente de imagen, puede definir la proporción del recorte, las orientaciones de imagen permitidas y si se permiten las cargas.

   ![chlimage_1-143](assets/chlimage_1-143.png)

   >[!CAUTION]
   >
   >Tenga en cuenta que, en AEM, las proporciones de recorte se definen como **altura/anchura**. Esto es distinto de la definición convencional de anchura/altura y se realiza por motivos de compatibilidad con sistemas anteriores. Los usuarios de creación de páginas no notarán ninguna diferencia siempre que defina claramente el **Nombre**, ya que esto es lo que se muestra en la interfaz de usuario.

   >[!NOTE]
   >
   >[](/help/sites-administering/rich-text-editor.md#main-pars-header-206036638)Las políticas de contenido para componentes que implementan el editor de texto enriquecido solo se pueden definir para las opciones que RTE tiene disponibles en su configuración de interfaz de usuario. [](/help/sites-administering/rich-text-editor.md#main-pars_header_206036638) [](/help/sites-administering/rich-text-editor.md#main-pars_header_206036638)

* **Política y propiedades (contenedor de diseño)**

   La configuración de la política y de las propiedades de un contenedor de diseño es similar al uso general, pero con algunas diferencias.

   >[!NOTE]
   >
   >Es obligatoria configurar una política para los componentes del contenedor, ya que le permite definir los componentes que estarán disponibles en el contenedor.

   La ventana de configuración se divide en dos, al igual que sucede con el uso general de la ventana.

   ***Política***

   Las políticas de contenido (o diseño) definen las propiedades de diseño de un componente. Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas. Esto se aplica a la plantilla (y a las páginas creadas con la plantilla).

   En **Política**, puede seleccionar una política existente para aplicarla al componente a través de la lista desplegable. Esto funciona igual que en el uso general de la ventana.

   ***Propiedades***

   En el encabezado **Propiedades**, puede elegir los componentes disponibles para el contenedor de diseño y definir sus opciones de configuración. El encabezado tiene tres pestañas:

   * Componentes permitidos
   * Componentes predeterminados
   * Configuración interactiva

   *Componentes permitidos*

   En la pestaña **Componentes permitidos**, defina los componentes disponibles para el contenedor de diseño.

   * Los componentes se agrupan por grupos de componentes, que se pueden expandir y contraer.
   * Es posible seleccionar un grupo completo marcando la casilla del nombre del grupo, y se puede anular la selección de todo desactivando la casilla de verificación.
   * Un signo menos indica se ha seleccionado al menos uno, pero no todos los elementos de un grupo.
   * Puede realizar búsquedas filtrando por el nombre de los componentes.
   * Los recuentos que aparecen a la derecha del nombre del grupo de componentes representan el número total de componentes seleccionados de dichos grupos, independientemente del filtro.

   ![chlimage_1-144](assets/chlimage_1-144.png)

   *Componentes predeterminados*

   En la pestaña **Componentes predeterminados**, puede definir qué componentes se asocian automáticamente a determinados tipos de medios, de modo que cuando un autor arrastra un recurso desde el navegador de recursos, AEM sabe a qué componente debe asociarlo. Tenga en cuenta que solo los componentes con zonas de colocación están disponibles para dicha configuración.

   Toque o haga clic en **Añadir asignación** para añadir un componente y una asignación de tipo MIME completamente nuevos.

   Seleccione un componente en la lista y pulse o haga clic en **Agregar tipo** para agregar un tipo MIME adicional a un componente ya asignado. Haga clic en el icono **Eliminar** para quitar un tipo MIME.

   ![chlimage_1-145](assets/chlimage_1-145.png)

   *Configuración interactiva*

   En la pestaña **Configuración interactiva**, puede configurar el número de columnas de la cuadrícula resultante del contenedor de diseño.

* **Desbloquear/bloquear componentes**

   Puede desbloquear/bloquear componentes para definir si el contenido está disponible para el cambio en el modo de **Contenido inicial**.

   Cuando un componente se ha desbloqueado:

   * Un indicador en forma de candado abierto se muestra en el borde.
   * La barra de herramientas de componentes se ajustará en consecuencia.
   * Cualquier contenido que ya haya introducido dejará de mostrarse en el modo de **Estructura**.

      * El contenido que ya haya introducido se considera contenido inicial y solo es visible en el modo de **Contenido inicial**.
   * Los componentes raíz del componente desbloqueado no se pueden mover, cortar ni eliminar.

   ![chlimage_1-146](assets/chlimage_1-146.png)

   Esto incluye el desbloqueo de componentes de contenedor para que se puedan añadir más componentes, ya sea en el modo **Contenido inicial** o en las páginas resultantes. Si ya ha agregado componentes o contenido al contenedor antes de desbloquearlo, estos ya no se mostrarán en el modo **Estructura**, pero se mostrarán en el modo **Contenido inicial**. En el **modo de Estructura**, solo el propio componente de contenedor se mostrará con su lista de **Componentes permitidos**.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   Para ahorrar espacio, el contenedor de diseño no aumenta para dar cabida a la lista de componentes permitidos. En su lugar, el contenedor se convierte en una lista por la que puede desplazarse.

   Los componentes que se pueden configurar se muestran con un icono de **directiva**, que se puede pulsar o hacer clic para editar la política y las propiedades de ese componente.

   ![chlimage_1-148](assets/chlimage_1-148.png)

* **Relación con las páginas existentes**

   Si la estructura se actualiza después de crear páginas basadas en la plantilla, esas páginas reflejarán los cambios realizados en la plantilla. Se muestra una advertencia en la barra de herramientas para recordarle este hecho junto con los cuadros de diálogo de confirmación.

   ![chlimage_1-149](assets/chlimage_1-149.png)

### Edición de una plantilla: contenido inicial, autor {#editing-a-template-initial-content-author}

El modo de **Contenido inicial** se utiliza con contenido definido que aparecerá cuando una página se crea por primera vez a partir de la plantilla. Entonces, los autores de páginas pueden editar el contenido inicial.

Aunque todo el contenido creado en el modo de **Estructura** sea visible en el **contenido inicial**, solo los componentes que se han desbloqueado se pueden seleccionar y editar.

>[!NOTE]
>
>El modo de **Contenido inicial** puede considerarse un modo de edición para las páginas creadas con esa plantilla. Por tanto, las políticas no se definen en el modo de **Contenido inicial**, sino en el modo de [**Estructura**](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

* Se marcan los componentes desbloqueados que quedan disponibles para editarse. Cuando están seleccionados tienen un borde azul:

   ![chlimage_1-150](assets/chlimage_1-150.png)

* Los componentes desbloqueados tienen una barra de herramientas que le permite editar y configurar el contenido:

   ![chlimage_1-151](assets/chlimage_1-151.png)

* Si un componente de contenedor se ha desbloqueado (en el modo de **Estructura**), puede añadir componentes nuevos al contenedor (en el modo de **Contenido inicial**). Los componentes añadidos en el modo de **Contenido inicial** se pueden mover o eliminar de las páginas resultantes.

   Puede añadir un componente mediante el área **Arrastrar componentes aquí** o la opción **Insertar nuevo componente** de la barra de herramientas del contenedor adecuado.

   ![chlimage_1-152](assets/chlimage_1-152.png) ![chlimage_1-153](assets/chlimage_1-153.png)

* Si el contenido inicial de la plantilla se actualiza después de que se creen las páginas a partir de esta, esas páginas no se verán afectadas por los cambios del contenido inicial en la plantilla.

>[!NOTE]
>
>El contenido inicial está diseñado para preparar componentes y el diseño de página que sirve como punto de partida para crear el contenido. No se prevé que el contenido real permanezca tal cual. Por este motivo, no se puede traducir el contenido inicial.
>
>Si necesita incluir texto traducible en la plantilla, como en encabezados o pies de página, puede utilizar las funciones de [localización de los componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/get-started/localization.html).

### Edición de una plantilla: diseño, autor de plantillas {#editing-a-template-layout-template-author}

Puede definir el diseño de la plantilla para una amplia gama de dispositivos. El [diseño interactivo](/help/sites-authoring/responsive-layout.md) para las plantillas funciona tal como lo hace para la creación de páginas.

>[!NOTE]
>
>Los cambios en el diseño se reflejarán en el modo de **Contenido inicial**, pero no se observará ningún cambio en el modo de **Estructura**.

![chlimage_1-154](assets/chlimage_1-154.png)

### Edición de una plantilla: diseño de página, autor/desarrollador de plantillas {#editing-a-template-page-design-template-author-developer}

El diseño de la página, incluidas las bibliotecas del lado del cliente y las políticas de página requeridas, se mantienen en la opción **Diseño de página** del menú **Información de la página**.

Para acceder al cuadro de diálogo **Diseño de página**:

1. En el **Editor de plantillas**, seleccione **Información de página** en la barra de herramientas y, a continuación, **Diseño de página** para abrir el cuadro de diálogo.
1. El cuadro de diálogo **Diseño de página** se abre y se divide en dos secciones:

   * En la mitad izquierda, se definen las [políticas de la página](/help/sites-authoring/templates.md#page-policies)
   * En la mitad derecha, se definen las [propiedades de página](/help/sites-authoring/templates.md#page-properties)

   ![chlimage_1-155](assets/chlimage_1-155.png)

#### Políticas de la página {#page-policies}

Puede aplicar una política de contenido a la plantilla o a las páginas resultantes. De esta forma, se define la política de contenido para el sistema de párrafos principal de la página.

![chlimage_1-156](assets/chlimage_1-156.png)

* Puede seleccionar una política existente para la página en el menú desplegable **Seleccionar política**.

   ![chlimage_1-157](assets/chlimage_1-157.png)

   Para añadir una política nueva, seleccione el botón de adición situado junto a la lista desplegable **Seleccionar política.** Se debe proporcionar un título nuevo en el campo **Título de la política**.

   ![chlimage_1-158](assets/chlimage_1-158.png)

   La política existente seleccionada en la lista desplegable **Seleccionar política** se puede copiar como una política nueva mediante el botón de copia situado al lado de la lista desplegable. Se debe proporcionar un título nuevo en el campo **Título de la política**. De forma predeterminada, la política copiada tendrá el título **Copia de X**, en que X es el título de la política copiada.

   ![chlimage_1-159](assets/chlimage_1-159.png)

* Defina un título para la política en el campo **Título de la política**. Es necesario que una política tenga un título para que se pueda seleccionar fácilmente en la lista desplegable **Seleccionar política**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

* En el campo **Descripción de la política**, se ofrece de manera opcional una descripción de la política.
* En la sección **Otras plantillas que también usan la política seleccionada**, puede ver con facilidad las otras plantillas que usan la política seleccionada en la lista desplegable **Seleccionar política**.

   ![chlimage_1-161](assets/chlimage_1-161.png)

#### Propiedades de página {#page-properties}

Con las propiedades de página, puede definir las bibliotecas del cliente necesarias mediante el cuadro de diálogo **Diseño de página**. Estas bibliotecas del cliente incluyen las hojas de estilo y el lenguaje Javascript que se van a cargar con la plantilla y las páginas creadas con esa plantilla.

![chlimage_1-162](assets/chlimage_1-162.png)

* Especifique las bibliotecas del cliente que desee aplicar a las páginas creadas con esta plantilla. Introduzca el nombre de una biblioteca en el campo de texto de la sección **Bibliotecas del cliente**.

   ![chlimage_1-163](assets/chlimage_1-163.png)

* Si son necesarias diversas bibliotecas, haga clic en el botón Añadir para añadir un campo de texto adicional para el nombre de la biblioteca.

   ![chlimage_1-164](assets/chlimage_1-164.png)

   Añada tantos campos de texto como sea necesario para las bibliotecas del cliente.

   ![chlimage_1-165](assets/chlimage_1-165.png)

* Defina la posición relativa de las bibliotecas según sea necesario arrastrando los campos con el control de arrastre.

   ![chlimage_1-166](assets/chlimage_1-166.png)

>[!NOTE]
>
>Si bien el autor de una plantilla puede especificar la política de página de la plantilla, deberá obtener información del desarrollador sobre las bibliotecas del cliente apropiadas.

### Edición de una plantilla: propiedades de la página inicial, autor {#editing-a-template-initial-page-properties-author}

Con la opción **Propiedades de la página inicial**, puede definir las [propiedades de la página](/help/sites-authoring/editing-page-properties.md) inicial que se deben utilizar al crear páginas resultantes.

1. En el editor de plantillas, seleccione **Información de página** en la barra de herramientas y, luego, **Propiedades de la página inicial** para abrir el cuadro de diálogo.

1. En el cuadro de diálogo, puede definir las propiedades que desee aplicar a las páginas creadas con esta plantilla.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Confirme las definiciones con **Listo**.

## Prácticas recomendadas   {#best-practices}

Al crear plantillas debe tener en cuenta:

1. El impacto que tendrán los cambios en la plantilla una vez que las páginas se han creado a partir de esa plantilla.

   A continuación se muestra una lista de las posibles diferentes operaciones en plantillas, así como la manera en que estas afectan a las páginas creadas a partir de ellas:

   * Cambios en la estructura:

      * Estos se aplican de forma inmediata a las páginas resultantes.
      * Sigue siendo necesario publicar la plantilla modificada para que los visitantes vean los cambios.
   * Cambios en las políticas de contenido y las configuraciones de diseño:

      * Estos se aplican de forma inmediata a las páginas resultantes.
      * Sigue siendo necesario publicar los cambios para que los visitantes puedan verlos.
   * Cambios en el contenido inicial:

      * Estos se aplican únicamente a las páginas creadas después de los cambios realizados en la plantilla.
   * Los cambios en el diseño dependen de si el componente modificado forma parte de:

      * Únicamente la estructura: se aplican inmediatamente
      * Contienen el contenido inicial: solo en las páginas creadas después del cambio

   Tenga una precaución especial al:

   * Bloquear o desbloquear componentes en plantillas activadas.
   * Esto puede tener efectos colaterales, ya que puede ser que las páginas existentes ya las utilicen. Normalmente:

      * En las páginas existentes, no estará disponible la opción de desbloquear los componentes (que estaban bloqueados).
      * Al bloquear los componentes (que eran editables), ese contenido se ocultará y no se mostrará en las páginas.

   >[!NOTE]
   >
   >AEM proporciona advertencias explícitas al cambiar el estado de bloqueo de componentes en las plantillas que ya no son borradores.

1. [Cree sus propias carpetas](#creatingatemplatefolderdeveloper) para las plantillas específicas del sitio.
1. [Publique sus plantillas](#publishingatemplateauthor) desde la consola **Plantillas**.
