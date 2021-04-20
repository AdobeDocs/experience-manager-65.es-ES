---
title: Creación y sincronización de Live Copies
description: Aprenda a crear y sincronizar Live Copies.
feature: Multi Site Manager
exl-id: 896b35dd-4510-4c94-8615-03d9649c2f64
translation-type: tm+mt
source-git-commit: 05dc73448d6902ccdbc92782fff39ef1a6339056
workflow-type: tm+mt
source-wordcount: '4174'
ht-degree: 1%

---

# Creación y sincronización de Live Copies{#creating-and-synchronizing-live-copies}

Puede crear una Live Copy desde una página o configuración de modelo y, a continuación, administrar la herencia y la sincronización.

## Administración de configuraciones de modelo {#managing-blueprint-configurations}

Una configuración de modelo identifica un sitio web existente que desea usar como fuente para una o más páginas de Live Copy.

>[!NOTE]
>
>Las configuraciones del modelo permiten insertar cambios en el contenido en Live Copies. Consulte [Live Copies: configuración de origen, modelos y modelo](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations).

Al crear una configuración de modelo, se selecciona una plantilla que define la estructura interna del modelo. La plantilla de modelo predeterminada supone que el sitio web de origen tiene las siguientes características:

* El sitio web tiene una página raíz.
* Las páginas secundarias inmediatas de la raíz son ramas de idioma del sitio web. Al crear una Live Copy, los idiomas se presentan como contenido opcional para incluirlos en la copia.
* La raíz de cada rama de idioma tiene una o más páginas secundarias. Al crear una Live Copy, las páginas secundarias se presentan como capítulos que puede incluir en la Live Copy.

>[!NOTE]
>
>Una estructura diferente requiere otra plantilla de modelo.

Después de crear la configuración de modelo, configure las siguientes propiedades:

* **Nombre**: Nombre de la configuración del modelo.
* **Ruta de origen**: Ruta de la página raíz del sitio que está utilizando como origen (modelo).
* **Descripción**. (Opcional) Descripción de la configuración del modelo. La descripción aparece en la lista de configuraciones de modelo entre las que elegir al crear un sitio.

Cuando se utiliza la configuración del modelo, puede asociarla con una configuración de lanzamiento que determina cómo se sincronizan las Live Copies del origen/modelo. Consulte [Especificación de las opciones de configuración de lanzamiento para utilizar](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use).

### Creación de una configuración de modelo {#creating-a-blueprint-configuration}

Para crear una configuración de modelo:

1. [](/help/sites-authoring/basic-handling.md#global-navigation) Vaya al menú  **** Herramientas y, a continuación, seleccione el menú  **** Sitios .
1. Seleccione **Blueprints** para abrir la consola **Configuración de modelo**:

   ![chlimage_1-209](assets/blueprint-configurations.png)

1. Seleccione **Crear**.
1. Seleccione la plantilla de modelo y, a continuación, **Next** para continuar.
1. Seleccione la página de origen que se utilizará como modelo; a continuación **Siguiente** para continuar.
1. Definir:

   * **Título**: título obligatorio para el modelo
   * **Descripción**: una descripción opcional para proporcionar más detalles.

1. **** Cree la configuración del modelo en función de su especificación.

### Edición o eliminación de una configuración de modelo {#editing-or-deleting-a-blueprint-configuration}

Puede editar o eliminar una configuración de modelo existente:

1. [](/help/sites-authoring/basic-handling.md#global-navigation) Vaya al menú  **** Herramientas y, a continuación, seleccione el menú  **** Sitios .
1. Seleccione **Blueprints** para abrir la consola **Configuración de modelo**:

   ![chlimage_1-210](assets/blueprint-configurations.png)

1. Seleccione la configuración del modelo necesaria: las acciones adecuadas estarán disponibles en la barra de herramientas:

   * **Propiedades**; puede utilizarlo para ver y luego editar las propiedades de la configuración.
   * **Eliminar**

## Creación de una copia activa {#creating-a-live-copy}

### Creación de una Live Copy de una página {#creating-a-live-copy-of-a-page}

Puede crear una Live Copy de cualquier página o rama. Al crear la Live Copy, puede especificar las opciones de configuración de lanzamiento que se utilizarán para sincronizar el contenido:

* Las configuraciones de lanzamiento seleccionadas se aplican a la página de Live Copy y a sus páginas secundarias.
* Si no especifica ninguna configuración de lanzamiento, MSM determina qué configuraciones de lanzamiento usar. Consulte [Especificación de la configuración de lanzamiento para utilizar](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use).

Puede crear una Live Copy de cualquier página:

* Páginas a las que se hace referencia mediante una [configuración de modelo](#creating-a-blueprint-configuration).
* Y páginas que no tienen conexión con una configuración.
* AEM también admite la creación de una Live Copy dentro de las páginas de otra Live Copy.

La única diferencia es que la disponibilidad del comando **Rollout** en las páginas de origen/modelo depende de si la fuente está referenciada por una configuración de modelo:

* Si crea la Live Copy desde una página de origen a la que se hace referencia **es** en una configuración de modelo, el comando Despliegue estará disponible en las páginas de origen/modelo.
* Si crea la Live Copy desde una página de origen a la que no se hace referencia **en una configuración de modelo, el comando Desplegar no estará disponible en las páginas de origen/modelo.**

Para crear una Live Copy:

1. En la consola **Sites**, seleccione **Crear** y, a continuación, **Live Copy**.

   ![chlimage_1-212](assets/chlimage_1-212.png)

1. Seleccione la página de origen y, a continuación, toque o haga clic en **Siguiente**. Por ejemplo:

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. Especifique la ruta de destino de la Live Copy (abra la carpeta o página principal de la Live Copy) y, a continuación, toque o haga clic en **Siguiente**.

   ![chlimage_1-214](assets/chlimage_1-214.png)

   >[!NOTE]
   >
   >La ruta de destino no puede estar dentro de la ruta de origen.

1. Escriba:

   * un **Título** para la página.
   * a **Name**, que se utiliza en la dirección URL.

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. Utilice la casilla de verificación **Excluir páginas secundarias**:

   * Seleccionado: crear una Live Copy solo de la página seleccionada (Live Copy superficial)
   * No seleccionado: crear una Live Copy que incluya todos los descendientes de la página seleccionada (copia en vivo profunda)

1. (Opcional) Para especificar una o más configuraciones de lanzamiento que se utilizarán para la Live Copy, utilice la lista desplegable **Implementar configuraciones** para seleccionarlas; las configuraciones seleccionadas se mostrarán debajo del selector desplegable.
1. Haga clic o pulse **Crear**. Se mostrará un mensaje de confirmación, desde el cual puede seleccionar **Open** o **Done**.

### Creación de una Live Copy de un sitio a partir de una configuración de modelo {#creating-a-live-copy-of-a-site-from-a-blueprint-configuration}

Cree una Live Copy con una configuración de modelo para crear un sitio basado en el contenido del modelo (origen). Al crear una Live Copy a partir de una configuración de modelo, se seleccionan una o varias ramas de idioma del origen del modelo que se van a copiar y, a continuación, se seleccionan los capítulos que se copiarán de las ramas de idioma. Consulte [Creación de una configuración de modelo](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

Si omite algunas ramas o capítulos de idioma de la Live Copy, puede agregarlos más adelante; consulte [Creación de una Live Copy dentro de una Live Copy (configuración de modelo)](#creating-a-live-copy-inside-a-live-copy-blueprint-configuration).

>[!CAUTION]
>
>Cuando el origen del modelo contiene vínculos y referencias que se dirigen a un párrafo en una rama diferente, los destinatarios no se actualizan en las páginas de Live Copy, sino que siguen apuntando al destino original.

Cuando cree el sitio, proporcione valores para las siguientes propiedades:

* **Idiomas** iniciales: Las ramas de idioma del origen del modelo que se incluirán en la Live Copy.
* **Capítulos** iniciales: Las páginas secundarias de las ramas de idioma del modelo que se incluirán en la Live Copy.
* **Ruta** de destino: La ubicación de la página raíz del sitio de Live Copy.
* **Título**: Título de la página raíz del sitio de Live Copy.
* **Nombre**: (Opcional) El nombre del nodo JCR que almacena la página raíz de la Live Copy. El valor predeterminado se basa en el título.
* **Propietario** del sitio: (Opcional)
* **Live Copy**: Seleccione esta opción para establecer una relación activa con el sitio de origen. Si no selecciona esta opción, se crea una copia del modelo, pero no se sincroniza posteriormente con el origen.
* **Configuración de lanzamiento**: (Opcional) Seleccione una o varias opciones de configuración de lanzamiento para sincronizar la Live Copy. De forma predeterminada, las configuraciones de lanzamiento se heredan del modelo; consulte [Especificación de las opciones de configuración de lanzamiento para utilizar](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use) para obtener más información.

Para crear una Live Copy de un sitio a partir de una configuración de modelo:

1. En la consola **Sitios**, seleccione **Crear** y, a continuación, **Sitio** en el selector desplegable.
1. Seleccione la configuración del modelo que se utilizará como origen de la Live Copy y continúe con **Next**:

   ![chlimage_1-216](assets/blueprint-configuration-select.png)

1. Utilice el selector **Initial Languages** para especificar el idioma o los idiomas del sitio del modelo que se utilizarán para la Live Copy.

   Todos los idiomas disponibles están seleccionados de forma predeterminada. Para eliminar un idioma, toque o haga clic en el **X** que aparece junto al idioma.

   Por ejemplo:

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Utilice la lista desplegable **Initial Chapters** para seleccionar las secciones del modelo que desea incluir en la Live Copy. De nuevo, todos los capítulos disponibles se incluyen de forma predeterminada, pero se pueden eliminar.
1. Proporcione valores para las propiedades restantes y, a continuación, seleccione **Crear**. En el cuadro de diálogo de confirmación, seleccione **Listo** para volver a la consola **Sitios** o **Abrir sitio** para abrir la página raíz del sitio.

### Creación de una Live Copy dentro de una Live Copy (configuración de modelo) {#creating-a-live-copy-inside-a-live-copy-blueprint-configuration}

Cuando crea una Live Copy dentro de la Live Copy existente (creada con una configuración de modelo), puede insertar cualquier copia de idioma o capítulos que no se incluyeron cuando la Live Copy se creó originalmente.

## Supervisión de Live Copy {#monitoring-your-live-copy}

### Ver el estado de una Live Copy {#seeing-the-status-of-a-live-copy}

Las propiedades de una página de Live Copy muestran la siguiente información sobre la Live Copy:

* **Fuente**: La página de origen de la página de Live Copy.
* **Estado**: Estado de sincronización de la Live Copy. El estado incluye si la Live Copy está actualizada con el origen, cuándo se produjo la última sincronización y quién realizó la sincronización.
* **Configuración**:

   * Indica si la página sigue estando sujeta a la herencia de Live Copy.
   * Indica si la configuración se hereda de la página principal.
   * Cualquier configuración de lanzamiento que use la Live Copy.

Para ver las propiedades:

1. En la consola **Sites**, seleccione la página de Live Copy y abra las propiedades.
1. Seleccione la pestaña **Live Copy**.

   Por ejemplo:

   ![chlimage_1-218](assets/chlimage_1-218.png)

   >[!NOTE]
   >
   >Para obtener más información, consulte también el artículo de la Base de conocimiento [Mensaje de estado de Livecopy - Up-to-date/Green/In Sync](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

### Ver las Live Copies de una página de modelo {#seeing-the-live-copies-of-a-blueprint-page}

Las páginas de modelo (a las que se hace referencia en una configuración de modelo) proporcionan una lista de las páginas de Live Copy que utilizan la página actual (modelo) como origen. Utilice esta lista para realizar un seguimiento de las Live Copies. La lista aparece en la pestaña **Blueprint** de las [propiedades de página](/help/sites-authoring/editing-page-properties.md).

![chlimage_1-219](assets/chlimage_1-219.png)

## Sincronización de Live Copy {#synchronizing-your-live-copy}

### Despliegue de un modelo {#rolling-out-a-blueprint}

Despliegue una página de modelo para insertar cambios de contenido en Live Copies. Una acción **Rollout** ejecuta las configuraciones de lanzamiento que utilizan el déclencheur [On Rollout](/help/sites-administering/msm-sync.md#rollout-triggers).

>[!NOTE]
>
>Pueden producirse conflictos si se crean nuevas páginas con el mismo nombre de página en la rama del modelo y en una rama de Live Copy dependiente.
>
>Estos [conflictos deben manejarse y resolverse en el momento del despliegue](/help/sites-administering/msm-rollout-conflicts.md).


#### Despliegue de un modelo desde Propiedades de página {#rolling-out-a-blueprint-from-page-properties}

1. En la consola **Sites**, seleccione la página en el modelo y abra las propiedades.
1. Abra la pestaña **Modelo**.
1. Seleccione **Despliegue**.

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. Especifique las páginas y las páginas secundarias y, a continuación, confirme con la marca de verificación:

   ![chlimage_1-221](assets/chlimage_1-221.png)

1. Especifique si el trabajo de despliegue debe ejecutarse inmediatamente (**Now**) o en otra fecha u hora (**Later**).

   ![Modelo de implementación](assets/rollout-blueprint.png)

Los lanzamientos se procesan como trabajos asincrónicos y se pueden comprobar en el [**Panel** Estado de trabajos asincrónicos](asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) en **Navegación global** -> **Herramientas** -> **Operaciones** -> **Trabajos**

>[!NOTE]
>
>El procesamiento asincrónico de la implementación requiere AEM 6.5.3.0 o superior. En versiones anteriores, las páginas se procesaban inmediata y sincrónicamente.

#### Despliegue un modelo desde el carril de referencia {#roll-out-a-blueprint-from-the-reference-rail}

1. En la consola **Sitios**, seleccione la página en la Live Copy y abra el panel **[Referencias](/help/sites-authoring/basic-handling.md#references)** (en la barra de herramientas).
1. Seleccione la opción **Blueprint** de la lista para mostrar los modelos asociados con esta página.
1. Seleccione el modelo requerido de la lista.
1. Toque o haga clic en **Despliegue**.
1. Se le pedirá que confirme los detalles del despliegue:

   * **Ámbito de despliegue**:

      Especifique si el ámbito es solo para la página seleccionada o si debe incluir las subpáginas.

   * **Programa**:

      Especifique si el trabajo de despliegue debe ejecutarse inmediatamente (**Now**) o en una fecha u hora posterior (**Later**).

      ![chlimage_1-222](assets/rollout-live-copy.png)

1. Después de confirmar estos detalles, seleccione **Rollout** para realizar la acción.

Los lanzamientos se procesan como trabajos asincrónicos y se pueden comprobar en el [**Panel** Estado de trabajos asincrónicos](asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) en **Navegación global** -> **Herramientas** -> **Operaciones** -> **Trabajos**

>[!NOTE]
>
>El procesamiento asincrónico de la implementación requiere AEM 6.5.3.0 o superior. En versiones anteriores, las páginas se procesaban inmediata y sincrónicamente a menos que se activara la opción **Background rollout**.

#### Despliegue un modelo desde la información general de Live Copy {#roll-out-a-blueprint-from-the-live-copy-overview}

La acción [Despliegue también está disponible en la Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview), cuando se selecciona una página de modelo.

1. Abra [Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) y seleccione una Página de modelo.
1. Seleccione **Despliegue** en la barra de herramientas.
1. Especifique las páginas y las páginas secundarias y, a continuación, confirme con la marca de verificación:

   ![chlimage_1-223](assets/chlimage_1-223.png)

1. Especifique si el trabajo de despliegue debe ejecutarse inmediatamente (**Now**) o en otra fecha u hora (**Later**).

   ![Modelo de implementación](assets/rollout-blueprint.png)

Los lanzamientos se procesan como trabajos asincrónicos y se pueden comprobar en el [**Panel** Estado de trabajos asincrónicos](asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations) en **Navegación global** -> **Herramientas** -> **Operaciones** -> **Trabajos**

>[!NOTE]
>
>El procesamiento asincrónico de la implementación requiere AEM 6.5.3.0 o superior. En versiones anteriores, las páginas se procesaban inmediata y sincrónicamente.

### Sincronización de una Live Copy {#synchronizing-a-live-copy}

Sincronice una página de Live Copy para extraer los cambios de contenido del origen a la Live Copy.

#### Sincronizar una Live Copy desde las propiedades de página {#synchronize-a-live-copy-from-page-properties}

Sincronice una Live Copy para extraer cambios del origen a la Live Copy.

>[!NOTE]
>
>La sincronización ejecuta las configuraciones de lanzamiento que utilizan el déclencheur [On Rollout](/help/sites-administering/msm-sync.md#rollout-triggers).

1. En la consola **Sites**, seleccione la página de Live Copy y abra las propiedades.
1. Abra la pestaña **Live Copy**.
1. Toque o haga clic en **Sincronizar**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

   Se solicitará confirmación, use **Sync** para continuar.

#### Sincronizar una Live Copy desde la información general de Live Copy {#synchronize-a-live-copy-from-the-live-copy-overview}

La acción [Sincronizar también está disponible en la Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview), cuando se selecciona una página de Live Copy.

1. Abra [Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) y seleccione una página de Live Copy.
1. Seleccione **Sincronizar** en la barra de herramientas.
1. Confirme la acción **Despliegue** en el cuadro de diálogo después de especificar si desea incluir:

   * **Página y páginas secundarias**
   * **Página solamente**

   ![chlimage_1-225](assets/chlimage_1-225.png)

## Cambio del contenido de Live Copy {#changing-live-copy-content}

Para cambiar el contenido de Live Copy, puede:

* Agregue párrafos a la página.
* Actualice el contenido existente rompiendo la herencia de la Live Copy para cualquier página o componente.

>[!NOTE]
>
>Si crea manualmente una nueva página en la Live Copy, entonces es local para la Live Copy, lo que significa que no tiene una página de origen correspondiente a la que adjuntar.
>
>La práctica recomendada para crear una página local que forme parte de la relación sería crearla en el origen y realizar un despliegue (profundo). Esto creará la página localmente como Live Copies.

>[!NOTE]
>
>Pueden producirse conflictos si se crean nuevas páginas con el mismo nombre de página en la rama del modelo y en una rama de Live Copy dependiente.
>
>Estos [conflictos deben manejarse y resolverse en el momento del despliegue](/help/sites-administering/msm-rollout-conflicts.md).


### Adición de componentes a una página de Live Copy {#adding-components-to-a-live-copy-page}

Agregue componentes a una página de Live Copy en cualquier momento. El estado de herencia de la Live Copy y su sistema de párrafos no controla la capacidad de añadir componentes.

Cuando la página de Live Copy se sincroniza con la página de origen, los componentes añadidos permanecen inalterados. Consulte también [Cambio del orden de los componentes en una página de Live Copy](#changing-the-order-of-components-on-a-live-copy-page).

>[!NOTE]
>
>Los cambios realizados localmente en un componente marcado como contenedor no se sobrescribirán con el contenido del modelo en un lanzamiento. Consulte [Prácticas recomendadas de MSM](/help/sites-administering/msm-best-practices.md#components-and-container-synchronization) para obtener más información.

### Suspender la herencia de una página {#suspending-inheritance-for-a-page}

Cuando crea una Live Copy, la configuración de la Live Copy se guarda en la página raíz de las páginas copiadas. Todas las páginas secundarias de la página raíz heredan las configuraciones de Live Copy. Los componentes de las páginas de Live Copy también heredan la configuración de Live Copy.

Puede suspender la herencia de Live Copy de una página de Live Copy para poder cambiar las propiedades y los componentes de la página. Al suspender la herencia, las propiedades y los componentes de la página ya no se sincronizan con el origen.

>[!NOTE]
>
>También puede [separar una Live Copy](#detaching-a-live-copy) de su modelo para eliminar todas las conexiones. La acción Desasociar es permanente e irreversible.

>[!NOTE]
>
>Si el componente está marcado como contenedor, las acciones de cancelación y suspensión no se aplican a sus componentes secundarios. Consulte también [Prácticas recomendadas de MSM](/help/sites-administering/msm-best-practices.md#components-and-container-synchronization) para obtener más información.

#### Suspender la herencia de las propiedades de página {#suspending-inheritance-from-page-properties}

Para suspender la herencia en una página:

1. Abra las propiedades de la página de Live Copy mediante el comando **Ver propiedades** de la consola **Sitios** o utilizando **Información de página** en la barra de herramientas de la página.
1. Toque o haga clic en la pestaña **Live Copy**.
1. Seleccione **Suspender** en la barra de herramientas. A continuación, puede seleccionar:

   * **Suspender**: solo página actual
   * **Suspender con elementos secundarios**: página actual junto con las páginas secundarias

1. Seleccione **Suspender** en el cuadro de diálogo de confirmación.

#### Suspender la herencia desde la información general de Live Copy {#suspending-inheritance-from-the-live-copy-overview}

La acción [Suspender también está disponible en la Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview), cuando se selecciona una página de Live Copy.

1. Abra [Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) y seleccione una página de Live Copy.
1. Seleccione **Suspender** en la barra de herramientas.
1. Seleccione la opción adecuada desde:

   * **Suspender**
   * **suspender con elto.sup.**

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. Confirme la acción **Suspender** en el cuadro de diálogo **Suspender Live Copy**:

   ![chlimage_1-227](assets/chlimage_1-227.png)

### Reanudar la herencia de una página {#resuming-inheritance-for-a-page}

Suspender la herencia de Live Copy de una página es una acción temporal. Una vez suspendida, la acción **Resume** está disponible, lo que le permite restablecer la relación activa.

Al volver a habilitar la herencia, la página no se sincroniza automáticamente con el origen. Puede solicitar una sincronización, si es necesario:

* En el cuadro de diálogo **Reanudar**/**Revertir**; por ejemplo:

   ![chlimage_1-228](assets/chlimage_1-228.png)

* En una etapa posterior, seleccionando manualmente la acción de sincronización.

>[!CAUTION]
>
>Al volver a habilitar la herencia, la página no se sincroniza automáticamente con el origen. Puede solicitar manualmente una sincronización si es necesario; bien en el momento de la reanudación o más tarde.

#### Reanudar la herencia de las propiedades de página {#resuming-inheritance-from-page-properties}

Una vez [suspendida](#suspending-inheritance-from-page-properties) la acción **Reanudar** se convierte en la barra de herramientas de las propiedades de la página:

![chlimage_1-229](assets/chlimage_1-229.png)

Cuando se selecciona, se muestra el cuadro de diálogo. Puede seleccionar una sincronización, si es necesario, y confirmar la acción.

#### Reanudar una página de Live Copy desde la información general de Live Copy {#resume-a-live-copy-page-from-the-live-copy-overview}

La acción [Reanudar también está disponible en la Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview), cuando se selecciona una página de Live Copy.

1. Abra [Live Copy Overview](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) y seleccione una Live Copy Page que se haya suspendido; se mostrará como **HERENCIA CANCELADA**.
1. Seleccione **Reanudar** en la barra de herramientas.
1. Indique si desea sincronizar la página después de revertir la herencia y, a continuación, confirme la acción **Reanudar** en el cuadro de diálogo **Reanudar Live Copy**.

### Cambio de la profundidad de herencia (superficial/profunda) {#changing-inheritance-depth-shallow-deep}

En una Live Copy existente, puede cambiar la profundidad de una página; es decir, si se incluyen las páginas secundarias.

* Cambio a una Live Copy superficial:

   * Tendrá un efecto inmediato y no es reversible.

      * Las páginas secundarias se separan explícitamente de la Live Copy. No se pueden conservar más modificaciones en niños si se deshacen.

      * Eliminará cualquier descendiente `LiveRelationships` aunque haya anidado `LiveCopies`.

* Cambio a una Live Copy profunda:

   * Las páginas secundarias permanecen intactas.
   * Para ver el efecto del conmutador, puede realizar un despliegue, las modificaciones de contenido se aplican según la configuración de lanzamiento.

* Cambie a una Live Copy superficial y, a continuación, vuelva a una copia profunda:

   * Todos los elementos secundarios (anteriormente) de la Live Copy superficial se tratan como si se hubieran creado manualmente y, por lo tanto, se mueven utilizando `[oldname]_msm_moved name`.

Para especificar o cambiar la profundidad:

1. Abra las propiedades de la página de Live Copy mediante el comando **Ver propiedades** de la consola **Sitios** o utilizando **Información de página** en la barra de herramientas de la página.
1. Toque o haga clic en la pestaña **Live Copy**.
1. En la sección **Configuration**, defina o borre la opción **Live Copy Inheritance** en función de si se incluyen las páginas secundarias:

   * activada: una Live Copy profunda (se incluyen las páginas secundarias)
   * clear: una Live Copy superficial (se excluyen las páginas secundarias)

   >[!CAUTION]
   >
   >Cambiar a una Live Copy superficial tendrá un efecto inmediato y no es reversible.
   >
   >Consulte [Live Copies - Composición](/help/sites-administering/msm.md#live-copies-composition) para obtener más información.

1. Toque o haga clic en **Guardar** para mantener las actualizaciones.

### Cancelación de la herencia de un componente {#cancelling-inheritance-for-a-component}

Cancele la herencia de Live Copy de un componente para que el componente ya no se sincronice con el componente de origen. Si es necesario, puede habilitar la herencia en un momento posterior.

>[!NOTE]
>
>Si el componente está marcado como contenedor, las acciones de cancelación y suspensión no se aplican a sus componentes secundarios. Consulte también [Prácticas recomendadas de MSM](/help/sites-administering/msm-best-practices.md#components-and-container-synchronization) para obtener más información.

>[!NOTE]
>
>Al volver a habilitar la herencia, el componente no se sincroniza automáticamente con el origen. Puede solicitar manualmente una sincronización si es necesario.

Cancele la herencia para cambiar el contenido del componente o eliminar el componente:

1. Toque o haga clic en el componente cuya herencia desea cancelar.

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. En la barra de herramientas de componentes, toque o haga clic en el icono **Cancelar herencia**.

   ![Imagen](do-not-localize/chlimage_1-8.png)

1. En el cuadro de diálogo Cancelar herencia, confirme la acción con **Yes**.

   La barra de herramientas de componentes se actualiza para incluir todos los comandos de edición (adecuados).

### Volver a habilitar la herencia para un componente {#re-enabling-inheritance-for-a-component}

Para habilitar la herencia para un componente, toque o haga clic en el icono **Volver a habilitar la herencia** de la barra de herramientas de componentes.

![image](do-not-localize/chlimage_1-9.png)

### Cambio del orden de los componentes en una página de Live Copy {#changing-the-order-of-components-on-a-live-copy-page}

Si una Live Copy contiene componentes que forman parte de un sistema de párrafos, la herencia de ese sistema de párrafos se adhiere a las siguientes reglas:

* Se puede modificar el orden de los componentes de un sistema de párrafos heredado, incluso con la herencia establecida.
* Al desplegar, el orden de los componentes se restaurará a partir del modelo. si se añadieron nuevos componentes a la Live Copy antes del despliegue, estos se reordenarán junto con los componentes por encima de los cuales se añadieron.
* Si se cancela la herencia del sistema de párrafos, el orden de los componentes no se restaurará durante el despliegue y se mantendrá tal cual en la Live Copy.

>[!NOTE]
>
>Al revertir una herencia cancelada en un sistema de párrafos, el orden de los componentes **no se restaurará automáticamente** del modelo. Puede solicitar manualmente una sincronización si es necesario.

Utilice el siguiente procedimiento para cancelar la herencia del sistema de párrafos.

1. Abra la página Live Copy.
1. Arrastre un componente existente a una nueva ubicación de la página.
1. En el cuadro de diálogo **Cancelar herencia**, confirme la acción con **Yes**.

### Omisión de las propiedades de una página de Live Copy {#overriding-properties-of-a-live-copy-page}

Las propiedades de página de una página Live Copy se heredan (y no se pueden editar) de la página de origen de forma predeterminada.

Puede cancelar la herencia de una propiedad cuando necesite cambiar el valor de la propiedad de Live Copy. Un icono de vínculo indica que la herencia está habilitada para la propiedad.

![chlimage_1-231](assets/chlimage_1-231.png)

Al cancelar la herencia, puede cambiar el valor de la propiedad. Un icono de vínculo roto indica que se ha cancelado la herencia.

![chlimage_1-232](assets/chlimage_1-232.png)

Posteriormente, puede volver a habilitar la herencia para una propiedad si es necesario.

>[!NOTE]
>
>Al volver a habilitar la herencia, la propiedad de la página de Live Copy no se sincroniza automáticamente con la propiedad de origen. Puede solicitar manualmente una sincronización si es necesario.

1. Abra las propiedades de la página de Live Copy mediante la opción **Ver propiedades** de la consola **Sitios** o el icono **Información de página** de la barra de herramientas de la página.
1. Para cancelar la herencia de una propiedad, toque o haga clic en el icono de vínculo que aparece a la derecha de la propiedad.

   ![image](do-not-localize/chlimage_1-10.png)

1. En el cuadro de diálogo de confirmación **Cancelar herencia**, pulse o haga clic en **Sí**.

### Revertir propiedades de una página de Live Copy {#revert-properties-of-a-live-copy-page}

Para habilitar la herencia para una propiedad, toque o haga clic en el icono **Revertir herencia** que aparece junto a la propiedad.

![image](do-not-localize/chlimage_1-11.png)

### Restablecimiento de una página de Live Copy {#resetting-a-live-copy-page}

Restaurar una página de Live Copy a:

* Elimine todas las cancelaciones de herencia y
* Devuelva la página al mismo estado que la página de origen.

El restablecimiento afecta a los cambios realizados en las propiedades de la página, el sistema de párrafos y los componentes.

#### Restaurar una página de Live Copy desde las propiedades de página {#reset-a-live-copy-page-from-the-page-properties}

1. En la consola **Sites**, seleccione la página de Live Copy y seleccione **Ver propiedades**.
1. Abra la pestaña **Live Copy**.
1. Seleccione **Reset** en la barra de herramientas.

   ![chlimage_1-233](assets/chlimage_1-233.png)

1. En el cuadro de diálogo **Restaurar Live Copy**, confirme con **Restaurar**.

#### Restaurar una página de Live Copy desde la información general de Live Copy {#reset-a-live-copy-page-from-the-live-copy-overview}

La acción [Restablecer también está disponible en la Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview), cuando se selecciona una página de Live Copy.

1. Abra [Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) y seleccione una página de Live Copy.
1. Seleccione **Reset** en la barra de herramientas.
1. Confirme la acción **Reset** en el cuadro de diálogo **Restaurar Live Copy**:

   ![chlimage_1-234](assets/chlimage_1-234.png)

## Comparación de una página de Live Copy con una página de modelo {#comparing-a-live-copy-page-with-a-blueprint-page}

Para realizar un seguimiento de los cambios realizados, puede ver la página del modelo en **Referencias** y compararla con su página de copia activa:

1. En la consola **Sites**, [vaya a un modelo o a una página de Live Copy y selecciónela](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. Abra el panel **[Referencias](/help/sites-authoring/basic-handling.md#references)** y seleccione:

   * **Modelo**  (cuando se selecciona una página de Live Copy)
   * **Live Copies**  (cuando se selecciona una página de modelo)

1. Seleccione la Live Copy específica y:

   * **Comparar con modelo**  (cuando se selecciona una página de Live Copy)
   * **Comparar con Live Copy**  (cuando se selecciona una página de modelo)

   Por ejemplo:

   ![chlimage_1-235](assets/chlimage_1-235.png)

1. Las dos páginas (Live Copy y modelo) se abrirán en paralelo.

   Para obtener información completa sobre el uso de esta característica, consulte la [diferencia de la página](/help/sites-authoring/page-diff.md).

## Desasociar una Live Copy {#detaching-a-live-copy}

Separar de forma permanente elimina la relación activa entre una Live Copy y su página de origen/modelo. Todas las propiedades relevantes para MSM se eliminan de la Live Copy y las páginas de Live Copy se convierten en una copia independiente.

>[!CAUTION]
>
>No puede restablecer la relación activa después de desasociar la Live Copy.
>
>Para eliminar la relación activa con la opción de reinstalarla más adelante, puede [cancelar la herencia de Live Copy](#suspending-inheritance-for-a-page) para la página.

Hay implicaciones sobre dónde dentro del árbol que utiliza **Desasociar**:

* **Desasociar en una página raíz de LiveCopy**

   Cuando esta operación se realiza en la página raíz de una Live Copy, elimina la relación activa entre todas las páginas del modelo y su Live Copy.

   Los cambios adicionales en las páginas del modelo (tal como estaba) **no afectarán** a la Live Copy (tal como estaba).

* **Desasociar en una subpágina de una LiveCopy**

   Cuando esta operación se realiza en una subpágina (o rama) dentro de una Live Copy:

   * la relación activa se elimina para esa subpágina (o rama)
   * y las páginas (sub)de la rama de Live Copy se tratan como si se hubieran creado manualmente.

   *Sin embargo*, las páginas secundarias siguen estando sujetas a la relación activa de la rama principal, por lo que un despliegue adicional de las páginas de modelo:

   1. Cambie el nombre de las páginas separadas:

      * Esto se debe a que MSM los considera como páginas creadas manualmente que causan un conflicto, ya que tienen el mismo nombre que las páginas de Live Copy que intenta crear.
   1. Cree una nueva página (Live Copy) con el nombre original, que contenga los cambios de la implementación.

   >[!NOTE]
   >
   >Consulte [Conflictos de despliegue de MSM](/help/sites-administering/msm-rollout-conflicts.md) para obtener más información sobre estas situaciones.

### Desasociar una página de Live Copy de las propiedades de página {#detach-a-live-copy-page-from-the-page-properties}

Para separar una Live Copy:

1. En la consola **Sitios**, seleccione la página de Live Copy y pulse o haga clic en **Ver propiedades**.
1. Abra la pestaña **Live Copy**.
1. En la barra de herramientas, seleccione **Desasociar**.

   ![chlimage_1-236](assets/chlimage_1-236.png)

1. Se mostrará un cuadro de diálogo de confirmación, seleccione **Desasociar** para completar la acción.

### Desasociar una página de Live Copy de la información general de Live Copy {#detach-a-live-copy-page-from-the-live-copy-overview}

La acción [Desasociar también está disponible en la Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview), cuando se selecciona una página de Live Copy.

1. Abra [Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md#using-the-live-copy-overview) y seleccione una página de Live Copy.
1. Seleccione **Separar** en la barra de herramientas.
1. Confirme la acción **Desasociar** en el cuadro de diálogo **Desasociar Live Copy**:

   ![chlimage_1-237](assets/chlimage_1-237.png)
