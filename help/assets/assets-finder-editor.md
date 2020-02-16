---
title: Crear y configurar páginas del editor de recursos
description: Obtenga información sobre cómo crear páginas personalizadas del editor de recursos y editar varios recursos simultáneamente.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# Crear y configurar páginas del editor de recursos {#creating-and-configuring-asset-editor-pages}

En este documento se describe lo siguiente:

* Por qué se crearían páginas personalizadas del editor de recursos.
* Cómo crear y personalizar páginas del editor de recursos, que son páginas WCM que le permiten ver y editar metadatos, así como realizar acciones en el recurso.
* Cómo editar varios recursos simultáneamente.

<!-- TBD: Add UICONTROL tags. Need PM review. Flatten the structure a bit. Re-write to remove Geometrixx mentions and to adhere to 6.5 OOTB samples. -->

>[!NOTE]
>
>Uso compartido de recursos está disponible como implementación de referencia de código abierto. Consulte [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/). No se admite oficialmente.

## ¿Por qué crear y configurar páginas del editor de recursos? {#why-create-and-configure-asset-editor-pages}

La administración de activos digitales se utiliza en cada vez más escenarios. Al pasar de una solución a pequeña escala para un pequeño grupo de usuarios con formación profesional (por ejemplo, fotógrafos o taxónomos) a grupos de usuarios más grandes y diversos (por ejemplo, usuarios empresariales, autores de WCM, periodistas, etc.), la potente interfaz de usuario de Recursos Adobe Experience Manager (AEM) para usuarios profesionales puede proporcionar demasiada información y los interesados empiezan a solicitar interfaces de usuario o aplicaciones específicas para acceder a los recursos digitales que les interesan.

Estas aplicaciones centradas en los recursos pueden ser simples galerías de fotos en una intranet donde los empleados pueden cargar fotos de las visitas a las ferias o un centro de prensa en un sitio web público, como el ejemplo proporcionado con Geometrixx. Las aplicaciones centradas en los recursos también pueden extenderse a soluciones completas, incluidos carros de compras, cierres de compra y procesos de verificación.

La creación de una aplicación centrada en los recursos se convierte en gran medida en un proceso de configuración que no requiere codificación, solo conocimiento de los grupos de usuarios y sus necesidades, así como conocimiento de los metadatos que se utilizan. Las aplicaciones centradas en los recursos creadas con Recursos AEM son extensibles: con un esfuerzo de codificación moderado, se pueden crear componentes reutilizables para buscar, ver y modificar recursos.

Una aplicación centrada en recursos en AEM consiste en una página del editor de recursos, que se puede utilizar para obtener una vista detallada de un recurso específico. La página Editor de recursos también permite editar metadatos, siempre que el usuario que accede al recurso tenga los permisos necesarios.

## Crear y configurar una página de uso compartido de recursos {#creating-and-configuring-an-asset-share-page}

Puede personalizar la funcionalidad de Buscador de DAM y crear páginas que tengan toda la funcionalidad que necesita, las cuales se denominan páginas de Uso compartido de recursos. Para crear una nueva página de uso compartido de recursos, agregue la página mediante la plantilla de uso compartido de recursos de Geometrixx y, a continuación, personalice las acciones que los usuarios pueden realizar en esa página, determine cómo ven los usuarios los recursos y decida cómo pueden crear sus consultas.

A continuación se indican algunos casos de uso para crear una página personalizada de uso compartido de recursos:

* Centro de prensa para periodistas
* Motor de búsqueda de imágenes para usuarios comerciales internos
* Base de datos de imágenes para usuarios de sitios web
* Interfaz de etiquetado de medios para editores de metadatos

### Crear una página de uso compartido de recursos {#creating-an-asset-share-page}

Para crear una nueva página de uso compartido de recursos, puede crearla cuando esté trabajando en sitios web o desde el administrador de recursos digitales.

>[!NOTE]
>
>De forma predeterminada, cuando se crea una página de uso compartido de recursos a partir de **Nuevo** en el administrador de recursos digital, se crea automáticamente un visor de recursos y un editor de recursos.

Para crear una nueva página de uso compartido de recursos en la consola **Sitios** web:

1. En la ficha **Sitios** web, navegue hasta el lugar donde desee crear una página de uso compartido de recursos y haga clic en **Nuevo**.

1. Seleccione la página Uso compartido **de** recursos y haga clic en **Crear**. La nueva página se crea y la página de uso compartido de recursos se muestra en la ficha **Sitios** web.

![dam8](assets/dam8.png)

La página básica creada con la plantilla Geometrixx DAM Asset Share tiene el siguiente aspecto:

![screen_shot_2012-04-18at115456am](assets/screen_shot_2012-04-18at115456am.png)

Para personalizar la página Uso compartido de recursos, utilice elementos de la barra de tareas y también edite las propiedades del generador de consultas. La página **Geometrixx Press Center** es una versión personalizada de una página basada en esta plantilla:

![screen_shot_2012-04-19at123048pm](assets/screen_shot_2012-04-19at123048pm.png)

Para crear una nueva página de uso compartido de recursos a través del administrador de recursos digital:

1. En el administrador de recursos digitales, en **Nuevo**, seleccione **Nuevo recurso compartido**.
1. En el **Título**, introduzca el nombre de la página de uso compartido de recursos. Si lo desea, escriba un nombre para la dirección URL.

   ![screen_shot_2012-04-19at23626pm](assets/screen_shot_2012-04-19at23626pm.png)

1. Haga doble clic en la página de uso compartido de recursos para abrirla y configurarla.

   ![screen_shot_2012-04-19at24114pm](assets/screen_shot_2012-04-19at24114pm.png)

   De forma predeterminada, al crear una página de uso compartido de recursos desde **Nuevo**, se crea automáticamente un visor de recursos y un editor de recursos.

#### Personalizar acciones {#customizing-actions}

Puede determinar qué acciones pueden realizar los usuarios en recursos digitales seleccionados a partir de una selección de acciones predefinidas.

Para agregar acciones a la página Uso compartido de recursos:

1. En la página Uso compartido de recursos que desee personalizar, haga clic en **Acciones** en la barra de tareas.

Están disponibles las siguientes acciones:

![assetshare2](assets/assetshare2.bmp)

| Acción | Descripción |
|---|---|
| [!UICONTROL Acción Eliminar] | Los usuarios pueden eliminar los recursos seleccionados. |
| [!UICONTROL Acción de descarga] | Permite a los usuarios descargar los recursos seleccionados en sus equipos. |
| [!UICONTROL Acción de Lightbox] | Guarda los recursos en una &quot;caja de luz&quot; en la que puede realizar otras acciones. Esto resulta útil cuando se trabaja con recursos en varias páginas. La caja de luz también se puede utilizar como carro de compras para los activos. |
| [!UICONTROL Acción de mover] | Los usuarios pueden mover el recurso a otra ubicación |
| [!UICONTROL Acción de etiquetas] | Permite a los usuarios agregar etiquetas a los recursos seleccionados |
| [!UICONTROL Acción de ver recursos] | Abre el recurso en el editor de recursos para su manipulación por parte del usuario. |

1. Arrastre la acción adecuada al área **Acciones** de la página. Al hacerlo, se crea un botón que se utiliza para ejecutar esa acción.

![chlimage_1-159](assets/chlimage_1-387.png)

#### Determinar cómo se presentan los resultados de búsqueda {#determining-how-search-results-are-presented}

Puede determinar cómo se muestran los resultados a partir de una lista predefinida de lentes.

Para cambiar la forma en que se ven los resultados de la búsqueda:

1. En la página Uso compartido de recursos que desee personalizar, haga clic en Buscar.

![chlimage_1](assets/assetshare3.png)

1. Arrastre la lente adecuada al centro superior de la página. En el Centro de Prensa, las lentes ya están disponibles. Los usuarios pulsan el icono de lente correspondiente para mostrar los resultados de búsqueda según sus preferencias.

Están disponibles las siguientes lentes:

| Objetivo | Descripción |
|---|---|
| **[!UICONTROL Vista de lista]** | Presenta los recursos en una lista con detalles. |
| **[!UICONTROL Vista en mosaico]** | Presenta los recursos en forma de mosaico. |

#### Vista en mosaico {#mosaic-lens}

![chlimage_1-160](assets/chlimage_1-388.png)

#### Vista de lista {#list-lens}

![chlimage_1-161](assets/chlimage_1-389.png)

#### Personalización del Generador de consultas {#customizing-the-query-builder}

El creador de consultas permite introducir términos de búsqueda y crear contenido para la página Uso compartido de recursos. Al editar el generador de consultas, también puede determinar cuántos resultados de búsqueda se muestran por página, qué editor de recursos se abre al hacer doble clic en un recurso, la ruta de acceso que busca la consulta y personalizar los tipos de nodos.

Para personalizar el generador de consultas:

1. En la página Uso compartido de recursos que desee personalizar, haga clic en **Editar** en el Generador de consultas. De forma predeterminada, se abre la ficha **General** .
1. Seleccione el número de resultados por página, la ruta del editor de recursos (si tiene un editor de recursos personalizado) y el título Acciones.

![screen_shot_2012-04-23at15055pm](assets/screen_shot_2012-04-23at15055pm.png)

1. Click the **Paths** tab. Escriba una ruta o varias rutas que se ejecutarán en la búsqueda. Estas rutas se sobrescriben si el usuario utiliza el predicado Rutas.

![screen_shot_2012-04-23at15150pm](assets/screen_shot_2012-04-23at15150pm.png)

1. Introduzca otro tipo de nodo, si lo desea.

1. En el campo URL **del Generador de** consultas, puede anular o ajustar el generador de consultas e introducir las nuevas direcciones URL del servlet con el componente existente del creador de consultas. En el campo **Dirección URL** de la fuente, también puede anular la dirección URL de la fuente.

![screen_shot_2012-04-23at15313pm](assets/screen_shot_2012-04-23at15313pm.png)

1. En el campo **Texto** , introduzca el texto que desea que aparezca para los resultados y los números de página de los resultados. Haga clic en **Aceptar** cuando termine de realizar cambios.

![screen_shot_2012-04-23at15300pm](assets/screen_shot_2012-04-23at15300pm.png)

#### Agregar predicados {#adding-predicates}

Recursos AEM incluye varios predicados que puede agregar a la página Uso compartido de recursos. Esto permite a los usuarios restringir aún más las búsquedas. En algunos casos, pueden sobrescribir un parámetro del generador de consultas (por ejemplo, el parámetro Path).

Para agregar predicados:

1. En la página Uso compartido de recursos que desee personalizar, haga clic en **Buscar**.

![assetshare3](assets/assetshare3.png)

1. Arrastre los predicados correspondientes a la página Uso compartido de recursos debajo del generador de consultas. Al hacerlo, se crean los campos correspondientes.

![assetshare4](assets/assetshare4.bmp)

Están disponibles los siguientes predicados:

| Predicado | Descripción |
|---|---|
| **[!UICONTROL Predicado de fecha]** | Permite a los usuarios buscar recursos que se modificaron antes y después de determinadas fechas. |
| **[!UICONTROL Predicado de opciones]** | El propietario del sitio puede especificar una propiedad para buscar (como en el predicado de propiedades, por ejemplo cq:tags) y un árbol de contenido desde el que rellenar las opciones (por ejemplo, el árbol de etiquetas). Al hacerlo, se genera una lista de opciones en la que los usuarios pueden seleccionar los valores (etiquetas) que debe tener la propiedad seleccionada (propiedad de etiqueta). Este predicado permite crear controles de lista como la lista de etiquetas, tipos de archivo, orientaciones de imagen, etc. Es ideal para un conjunto fijo de opciones. |
| **[!UICONTROL Predicado de ruta]** | Permite a los usuarios definir la ruta y las subcarpetas, si lo desean. |
| **[!UICONTROL Predicado de propiedades]** | El propietario del sitio especifica una propiedad para buscar, por ejemplo tiff:ImageLength y el usuario puede entonces introducir un valor, por ejemplo: 800. Esto devuelve todas las imágenes con una altura de 800 píxeles. Un predicado útil si la propiedad puede tener valores arbitrarios. |

Para obtener más información, consulte el [predicado Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html).

1. Para seguir configurando el predicado, haga doble clic en él. Por ejemplo, cuando se abre el predicado de rutas, es necesario asignar la ruta raíz.

![screen_shot_2012-04-23at15640pm](assets/screen_shot_2012-04-23at15640pm.png)

## Creación y configuración de una página Editor de recursos {#creating-and-configuring-an-asset-editor-page}

Puede personalizar el editor de recursos para determinar cómo pueden ver y editar los recursos digitales los usuarios. Para ello, se crea una nueva página Editor de recursos y, a continuación, se personalizan las vistas y las acciones que los usuarios pueden realizar en esa página.

>[!NOTE]
>
>Si desea agregar campos personalizados al editor de recursos DAM, agregue nuevos nodos cq:Widget a `/apps/dam/content/asseteditors.`

### Creación de una página del editor de recursos {#creating-the-asset-editor-page}

Al crear la página Editor de recursos, se recomienda crear la página directamente debajo de la página Uso compartido de recursos.

Para crear una página del editor de recursos:

1. En la ficha **Sitios** web, navegue hasta el lugar donde desee crear una página de editor de recursos y haga clic en **Nuevo**.
1. Seleccione **Geometrixx Asset Editor** y haga clic en **Crear**. La nueva página se crea y la página se enumera en la ficha **Sitios** web.

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

La página básica creada con la plantilla Editor de recursos de Geometrixx tiene el siguiente aspecto:

![assetshare5](assets/assetshare5.bmp)

Para personalizar la página del Editor de recursos, utilice elementos de la barra de tareas. La página Editor de recursos a la que se accede desde el Centro **de prensa de** Geometrixx es una versión personalizada de una página basada en esta plantilla:

![assetshare6](assets/assetshare6.bmp)

#### Configuración de un editor de recursos para abrirlo desde una página de uso compartido de recursos {#setting-which-asset-editor-opens-from-an-asset-share-page}

Después de crear la página del editor de recursos personalizada, debe asegurarse de que, al hacer doble clic en los recursos que ha creado, se abran los recursos en la página del editor personalizada.

Para configurar la página Editor de recursos:

1. En la página Uso compartido de recursos, haga clic en **Editar** junto al Generador de consultas.

![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. Haga clic en la ficha **General** si aún no está seleccionada.

1. En el campo **Ruta del Editor** de recursos, introduzca la ruta del editor de recursos en el que desea que la página Uso compartido de recursos abra los recursos y haga clic en **Aceptar**.

![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### Agregar componentes del editor de recursos {#adding-asset-editor-components}

Para determinar la funcionalidad que tiene un editor de recursos, agregue componentes a la página.

Para agregar componentes del editor de recursos:

1. En la página Editor de recursos que desee personalizar, seleccione Editor **de recursos** en la barra de tareas. Se muestran todos los componentes del editor de recursos disponibles.

>[!NOTE]
>
>Lo que se puede personalizar depende de los componentes disponibles. Para activar los componentes, vaya al modo Diseño y seleccione los componentes que necesita activados.

1. Arrastre los componentes de la barra de tareas al editor de recursos y realice las modificaciones necesarias en los cuadros de diálogo de componentes. Los componentes se describen en la siguiente tabla y se describen en las instrucciones detalladas que se indican a continuación.

>[!NOTE]
>
>Al diseñar la página del editor de recursos, se crean componentes que son de solo lectura o editables. Los usuarios saben que un campo se puede editar si aparece una imagen de un lápiz en ese componente. De forma predeterminada, la mayoría de los componentes están configurados como de solo lectura.

| Componente | Descripción |
|---|---|
| **[!UICONTROL Campo de texto de formulario]de metadatos y[!UICONTROL metadatos]** | Permite agregar metadatos adicionales a un recurso y realizar una acción, como enviar, en dicho recurso. |
| **[!UICONTROL Recursos secundarios]** | Permite personalizar subrecursos. |
| **Etiquetas** | Permite a los usuarios seleccionar y agregar etiquetas a un recurso. |
| **[!UICONTROL Miniatura]** | Muestra una miniatura del recurso, su nombre de archivo y le permite agregar un texto alternativo. Aquí también puede agregar acciones del editor de recursos. |
| **[!UICONTROL Título]** | Muestra el título del recurso, que se puede personalizar. |

![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### Campo de texto y formulario de metadatos: configuración del componente Ver metadatos {#metadata-form-and-text-field-configuring-the-view-metadata-component}

El formulario de metadatos es un formulario que incluye una acción de inicio y finalización. En el medio, se introducen campos **de texto** . Consulte [Formularios](/help/sites-authoring/default-components-foundation.md#form-component) para obtener más información sobre cómo trabajar con formularios.

1. Cree una acción de inicio haciendo clic en **Editar** en el área Inicio del formulario. Si lo desea, puede introducir un título de cuadro. De forma predeterminada, el título Cuadro es **Metadatos**. Active la casilla de verificación Validación del cliente si desea que se genere el código de cliente java-script para la validación.

![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. Para crear una acción de finalización, haga clic en **Editar** en el área Final del formulario. Por ejemplo, es posible que desee crear un botón **Enviar** para permitir que los usuarios envíen los cambios de metadatos. De forma opcional, puede agregar un botón **Restablecer** que restablezca los metadatos a su estado original.

![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. Entre el inicio **del** formulario y el final **del** formulario, arrastre Campos de texto de metadatos al formulario. Los usuarios rellenan los metadatos en estos campos de texto, en los que pueden enviar o completar otra acción.

1. Haga doble clic en el nombre del campo, por ejemplo, **Título** para abrir el campo de metadatos y realizar cambios. En la ficha **General** de la ventana **Editar componente** , se definen el espacio de nombres y la etiqueta del campo, así como el tipo, por ejemplo `dc:title`.

![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

Consulte [Personalización y ampliación de Recursos](/help/assets/extending-assets.md) AEM para obtener información sobre cómo modificar los espacios de nombres disponibles en el formulario de metadatos.

1. Click the **Constraints** tab. Aquí puede seleccionar si un campo es obligatorio y, si es necesario, agregar restricciones.

![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. Click the **Display** tab. Aquí puede introducir un nuevo ancho y un número de filas para el campo de metadatos. Seleccione la casilla **Campo de solo** lectura para permitir a los usuarios editar los metadatos.

![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

A continuación se muestra un ejemplo de un formulario de metadatos con varios campos:

![chlimage_1-162](assets/chlimage_1-390.png)

En la página Editor de recursos, los usuarios pueden introducir valores en los campos de metadatos (si son editables) y realizar la acción final (por ejemplo, enviando los cambios).

#### Subactivos {#sub-assets}

En el componente Recursos secundarios se pueden ver y seleccionar subrecursos. Puede determinar los nombres que aparecen bajo el recurso [](/help/assets/assets.md#what-are-digital-assets) principal y los subrecursos.

![screen_shot_2012-04-23at24025pm](assets/screen_shot_2012-04-23at24025pm.png)

Haga doble clic en el componente Recursos secundarios para abrir el cuadro de diálogo Recursos secundarios, donde puede cambiar los títulos del recurso principal y de los subrecursos. Los valores predeterminados aparecen debajo del campo correspondiente.

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

A continuación se muestra un ejemplo de un componente Sub Assets rellenado:

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

Por ejemplo, si selecciona un subrecurso, tenga en cuenta cómo el componente muestra la página adecuada y cómo el título del cuadro cambia de Recursos secundarios a Hermanos.

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### Etiquetas {#tags}

El componente Etiquetas es un componente en el que los usuarios pueden asignar etiquetas existentes a un recurso, lo que ayuda a organizarlo y recuperarlo posteriormente. Puede hacer que este componente sea de solo lectura, por lo que los usuarios no pueden agregar etiquetas, sino solo verlas.

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

Haga doble clic en el componente Etiquetas para abrir el cuadro de diálogo Etiquetas, donde puede cambiar el título de Etiquetas, si lo desea, y donde puede seleccionar los espacios de nombres asignados. Para que este campo sea editable, desactive la casilla de verificación **[!UICONTROL Ocultar edición]** . De forma predeterminada, las etiquetas son editables.

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

Si los usuarios pueden editar etiquetas, pueden hacer clic en el lápiz para agregar etiquetas seleccionándolas en el menú desplegable Etiquetas.

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

A continuación se muestra un componente Etiquetas rellenado:

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### Miniatura {#thumbnail}

El componente Miniatura es donde el recurso muestra la miniatura seleccionada (para muchos de los formatos la miniatura se extrae automáticamente). Además, el componente muestra el nombre de archivo y [las acciones que puede modificar](/help/assets/assets-finder-editor.md#adding-asset-editor-actions).

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

Haga doble clic en el componente de miniatura para abrir el cuadro de diálogo de miniaturas donde puede cambiar el texto alternativo. De forma predeterminada, el texto alternativo de la miniatura es **Haga clic para descargar** el recurso.

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

A continuación se muestra un ejemplo de un componente Miniatura relleno:

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### Título {#title}

El componente Título muestra el título del recurso y una descripción.

![chlimage_1-163](assets/chlimage_1-391.png)

De forma predeterminada, está en modo de solo lectura, por lo que los usuarios no pueden editarlo. Para que sea editable, haga doble clic en el componente y desactive la casilla de verificación **Ocultar botón** de edición. Además, introduzca un título para varios recursos.

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

Si se puede editar el Título, puede agregar un título y una descripción haciendo clic en el lápiz para abrir la ventana Propiedades **del** recurso. Además, puede activar y desactivar el recurso seleccionando la fecha y la hora.

Cuando los usuarios editan el Título haciendo clic en el icono de lápiz, pueden cambiar el **Título**, la **Descripción** y especificar **Tiempo de activación** y **** desactivación para activar y desactivar el recurso.

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

A continuación se muestra un ejemplo de un componente Título rellenado:

![chlimage_1-164](assets/chlimage_1-392.png)

#### Agregar acciones del editor de recursos {#adding-asset-editor-actions}

Puede determinar qué acciones pueden realizar los usuarios en recursos digitales seleccionados a partir de una selección de acciones predefinidas.

Para agregar acciones a la página Editor de recursos:

1. En la página Editor de recursos que desee personalizar, haga clic en Editor **de** recursos en la barra de tareas.

![screen_shot_2012-04-23at35515pm](assets/screen_shot_2012-04-23at35515pm.png)

Están disponibles las siguientes acciones:

| Acción | Descripción |
|---|---|
| [!UICONTROL Descargar] | Permite a los usuarios descargar los recursos seleccionados en sus equipos. |
| [!UICONTROL Editores] | Permite a los usuarios editar una imagen (edición interactiva) |
| [!UICONTROL Lightbox] | Guarda los recursos en una &quot;caja de luz&quot; en la que puede realizar otras acciones. Esto resulta útil cuando se trabaja con recursos en varias páginas. |
| [!UICONTROL Bloqueo] | Permite a los usuarios bloquear un recurso. Esta funcionalidad no está habilitada de forma predeterminada y debe habilitarse en la lista de componentes. |
| [!UICONTROL Referencias] | Haga clic aquí para mostrar en qué páginas se está utilizando el recurso. |
| [!UICONTROL Versiones] | Permite crear y restaurar versiones de un recurso. |

1. Arrastre la acción adecuada al área **Acciones** de la página. Al hacerlo, se crea un botón que se utiliza para ejecutar esa acción.

![chlimage_1-165](assets/chlimage_1-393.png)

## Edición múltiple de recursos con la página Editor de recursos {#multi-editing-assets-with-the-asset-editor-page}

Con Recursos AEM, puede realizar cambios en varios recursos a la vez. Después de haber seleccionado los recursos, puede cambiar al mismo tiempo los siguientes:

* Etiquetas
* Metadatos

Para editar varios recursos con la página Editor de recursos:

1. Abra la página **Centro** de prensa de Geometrixx:
   `https://localhost:4502/content/geometrixx/en/company/press.html`

1. Seleccione los recursos:

   * en Windows: `Ctrl + click` cada recurso.
   * en Mac: `Cmd + click` cada recurso.
   Para seleccionar un rango de recursos: haga clic en el primer recurso y, a continuación, en `Shift + click` el último.

1. Haga clic en **Editar metadatos** en el campo **Acciones** (parte izquierda de la página).
1. La página Editor **de recursos del Centro de** prensa de Geometrixx se abre en una nueva ficha. Los metadatos de los recursos se muestran de la siguiente manera:

   * En cursiva se muestra una etiqueta que no se aplica a todos los recursos, sino solo a algunos.
   * Una etiqueta que se aplica a todos los recursos se muestra con una fuente normal.
   * Metadatos distintos de las etiquetas: el valor del campo solo se muestra si es el mismo para todos los recursos seleccionados.

1. Haga clic en **Descargar** para descargar un archivo zip que contenga las representaciones originales de los recursos.
1. Haga clic en el icono del lápiz situado junto al campo **Etiquetas** para editar las etiquetas:

   * Una etiqueta que no se aplica a todos los recursos, pero solo a algunos tiene un fondo gris.
   * Una etiqueta que se aplica a todos los recursos tiene un fondo blanco.
   Puede hacer lo siguiente:

   * Haga clic en el icono **x** para eliminar la etiqueta de todos los recursos.
   * Haga clic en el icono **+** para agregar la etiqueta a todos los recursos.
   * Haga clic en la **flecha** y seleccione una etiqueta para agregar una nueva etiqueta a todos los recursos.
   Haga clic en **Aceptar** para escribir los cambios en el formulario. La casilla situada junto al campo **Etiquetas** se activa automáticamente.

1. Edite el campo Descripción. Por ejemplo, establézcalo en:

   `This is a common description`

   Cuando se edita un campo, su valor sobrescribe los valores existentes de los recursos seleccionados al enviar el formulario.

   Nota: la casilla al lado del campo se activa automáticamente cuando se edita el campo.

1. Haga clic en **Actualizar metadatos** para enviar el formulario y guardar los cambios para todos los recursos.

   Nota: solo se modifican los metadatos marcados.
