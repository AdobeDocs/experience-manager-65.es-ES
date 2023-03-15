---
title: Creación de contenido orientado mediante el modo de Orientación
seo-title: Authoring Targeted Content Using Targeting Mode
description: El modo de Orientación y el componente Target proporcionan herramientas para crear contenido para las experiencias
seo-description: Targeting mode and the Target component provide tools for creating content for experiences
uuid: cea85c1b-1bc3-4498-9eaa-4ad10dc58ea4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9d940744-3b00-4721-829a-96d17bb738e8
docset: aem65
exl-id: edde225d-0be7-4306-8dda-d18d46fae977
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '5349'
ht-degree: 91%

---

# Creación de contenido orientado mediante el modo de Orientación{#authoring-targeted-content-using-targeting-mode}

Contenido orientado por el autor mediante el modo de segmentación de AEM. El modo de Orientación y el componente Target proporcionan herramientas para crear contenido para las experiencias:

* Reconozca fácilmente el contenido orientado que se encuentra en la página. Una línea discontinua forma un borde alrededor de todo el contenido orientado.
* Seleccione una marca y una actividad para ver las experiencias.
* Añada experiencias a una actividad o quite experiencias.
* Realice la prueba A/B y convierta a los ganadores (solo Adobe Target).
* Para añadir ofertas a una experiencia, créelas o utilice ofertas de una biblioteca.
* Configure los objetivos y controle el rendimiento.
* Simule la experiencia de usuario.
* Para obtener más personalización, configure el componente Target.

Puede utilizar AEM o Adobe Target como motor de orientación (para utilizar Adobe Target, debe tener una cuenta de Adobe Target válida). Si utiliza Adobe Target, primero debe configurar la integración. Consulte [instrucciones para la integración con Adobe Target](/help/sites-administering/target.md).

![chlimage_1-8](assets/chlimage_1-8.png)

Las actividades y experiencias que ve en el modo de Target reflejan la [consola Actividades](/help/sites-authoring/activitylib.md):

* Los cambios que realice en las actividades y experiencias mediante el modo de Orientación se reflejan en la consola Actividades.
* Los cambios que se realizan en la consola Actividades se reflejan en el modo de Orientación.

>[!NOTE]
>
>Al crear una campaña en Adobe Target, se asigna una propiedad denominada `thirdPartyId` a cada campaña. Al eliminar la campaña en Adobe Target, thirdPartyId no se elimina. No puede volver a utilizar `thirdPartyId` para las campañas de distintos tipos (AB, XT) y no se puede quitar manualmente. Para evitar este problema, asigne a cada campaña un nombre único; por tanto, los nombres de campaña no se pueden reutilizar en tipos de campaña diferentes.
>
>Si utiliza el mismo nombre en el mismo tipo de campaña, sobrescribirá la campaña existente.
>
>Si al sincronizar se muestra el mensaje de error “Se ha producido un error en la solicitud. `thirdPartyId` ya existe”, cambie el nombre de la campaña y vuelva a sincronizar.

>[!NOTE]
>
>Cuando se selecciona el destino, la combinación de marca y actividad permanecen a nivel de usuario y no a nivel de canal.

## Cambiar al modo de Orientación {#switching-to-targeting-mode}

Cambie al modo de Target para acceder a las herramientas de creación de contenido orientado.

Para cambiar al modo de Target:

1. Abra la página para la que desea crear contenido orientado.
1. En la barra de herramientas situada en la parte superior de la página, toque o haga clic en el menú emergente de modo para mostrar los tipos de modo disponibles.

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Toque o haga clic en **Direccionamiento**. Las opciones de orientación se muestran en la parte superior de la página.

   ![chlimage_1-10](assets/chlimage_1-10.png)

## Adición de una actividad con el modo de Orientación {#adding-an-activity-using-targeting-mode}

Utilice el modo de Orientación para añadir una actividad a una marca. Al añadir una actividad, contiene la experiencia predeterminada. Después de añadir la actividad, se inicia el proceso de orientación del contenido para la actividad.

También puede crear y administrar las actividades de Adobe Target desde AEM con la opción de seleccionar el motor de orientación (AEM o Adobe Target) y el tipo de actividad (orientación de la experiencia o prueba A/B).

Además, puede administrar objetivos y métricas para todas las actividades de Adobe Target y administrar los públicos de Adobe Target. También se incluye el informe de actividad de Adobe Target, que incluye la conversión de ganadores para la prueba A/B.

Al añadir una actividad, también aparece en la consola [Actividades](/help/sites-authoring/activitylib.md).

Para añadir una actividad:

1. Utilice el menú desplegable **Marca** para seleccionar la marca para la que desea crear la actividad.

   >[!NOTE]
   >
   >Se recomienda [crear marcas a través de la consola de actividades](/help/sites-authoring/activitylib.md#creating-a-brand-using-the-activities-console).
   >
   >
   >Si crea una marca de cualquier otra manera, asegúrese de que el nodo `/campaigns/<brand>/master` existe o se producirá un error al intentar crear una actividad.

1. Toque o haga clic en + junto al menú desplegable **Actividad**.
1. Escriba un nombre para la actividad.

   >[!NOTE]
   >
   >Al crear una actividad nueva y tener una configuración de nube de Adobe Target asociada a la página o a uno de sus elementos raíz, AEM supone automáticamente que Adobe Target es el motor.

1. En el menú desplegable del motor de **Orientación**, seleccione el motor de orientación.

   * Si selecciona **ContextHub AEM**, los campos restantes se atenúan y no están disponibles. Haga clic o pulse **Crear**.

   * Si selecciona **Adobe Target**, puede seleccionar una configuración (de forma predeterminada, es la configuración que proporcionó al [configurar la cuenta](/help/sites-administering/opt-in.md)) y el tipo de actividad.

   * Si utiliza la integración AEM/Adobe Campaign y envía contenido orientado (newsletters), seleccione **Adobe Campaign**. Consulte [Integración con Adobe Campaign](/help/sites-administering/campaign.md) para obtener más información.

1. En el menú Actividad, seleccione **Orientación de la experiencia** o **Prueba A/B**.

   * Orientación de la experiencia: administre las actividades de Adobe Target desde AEM.
   * Prueba A/B: cree o administre las actividades de la prueba A/B en Adobe Target desde AEM.

## El proceso de orientación: Crear, Orientar y Objetivos y configuraciones {#the-targeting-process-create-target-and-goals-settings}

El modo de Orientación le permite configurar diversas proporciones de una actividad. Utilice el proceso siguiente que consta de tres pasos para crear contenido orientado para una actividad de marca:

1. [Crear](#create-authoring-the-experiences): añada o quite experiencias y añada ofertas para cada experiencia.
1. [Orientar](#diagramtargetconfiguringtheaudiences): especifique el público al que se orienta cada experiencia. Puede orientar a un público concreto y, si utiliza la prueba A/B, decidir qué porcentaje del tráfico corresponde a cada experiencia.
1. [Objetivos y configuraciones](#settingsgoalssettingsconfiguringtheactivityandsettinggoals): programe la actividad y establezca la prioridad. También puede establecer objetivos de indicadores de éxito.

Utilice el procedimiento siguiente para iniciar el proceso de orientación del contenido para una actividad.

>[!NOTE]
>
>Para utilizar el proceso de direccionamiento, debe ser miembro del grupo de usuarios Autores de actividades de Target.

Para añadir una actividad:

1. En el menú desplegable **Marca**, seleccione la marca que contiene la actividad en que está trabajando.
1. En el menú desplegable **Actividad**, seleccione la actividad para la que está creando contenido orientado.
1. Para mostrar los controles que lo guiarán a través del proceso de orientación, toque o haga clic en **Iniciar orientación**.

   ![chlimage_1-11](assets/chlimage_1-11.png)

   >[!NOTE]
   >
   >Para cambiar la actividad con la que está trabajando, toque o haga clic en **Atrás**.

## Crear: creación de experiencias {#create-authoring-the-experiences}

El paso Crear de la orientación del contenido implica la creación de experiencias. Durante este paso, puede crear o eliminar las experiencias de la actividad y añadir ofertas a cada experiencia.

### Visualización de ofertas de experiencia en el modo de Orientación {#seeing-experience-offers-in-targeting-mode}

Después de [iniciar el proceso de orientación](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings), seleccione una experiencia para ver las ofertas que se proporcionan para esa experiencia. Al seleccionar una experiencia, los componentes orientados de la página cambian para mostrar la oferta para esa experiencia.

>[!CAUTION]
>
>Tenga cuidado al desactivar la orientación de un componente que ya está orientado en la instancia del autor. La actividad correspondiente también se eliminará automáticamente de la instancia de publicación.

>[!NOTE]
>
>Como oferta se entiende el contenido de un componente orientado.

Las experiencias se muestran en el panel Audiencies. En el siguiente ejemplo, las experiencias incluyen **Predeterminado**, **Mujer**, **Mujer mayor de 30 años** y **Mujer menor de 30 años**. Este ejemplo muestra la oferta predeterminada de un componente de **imagen** segmentado.

![chlimage_1-12](assets/chlimage_1-12.png)

Al seleccionar una experiencia distinta, el componente Imagen muestra la oferta para esa experiencia.

![chlimage_1-13](assets/chlimage_1-13.png)

Cuando se selecciona una experiencia y el componente segmentado no incluye una oferta para esa experiencia, el componente muestra la opción **Agregar oferta** superpuesta a la oferta predeterminada semitransparente. Cuando no se ha creado ninguna oferta para una experiencia, se muestra la oferta **predeterminada** para el segmento asignado a la experiencia.

![chlimage_1-14](assets/chlimage_1-14.png)

La experiencia predeterminada también se muestra cuando las propiedades del visitante no coinciden con ningún segmento asignado a las experiencias. Consulte [Adición de experiencias con el modo de direccionamiento](#adding-and-removing-experiences-using-targeting-mode).

### Ofertas personalizadas y ofertas de la biblioteca {#custom-offers-and-library-offers}

Las ofertas que [se crean en la página](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) y se utilizan para una experiencia única se denominan ofertas personalizadas. La imagen siguiente está superpuesta al contenido de una oferta personalizada:

![chlimage_1-15](assets/chlimage_1-15.png)

Las ofertas que [se añaden desde una biblioteca de ofertas](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library) se superponen a la imagen siguiente:

![chlimage_1-16](assets/chlimage_1-16.png)

Puede guardar ofertas personalizadas en una biblioteca de ofertas si decide que quiere volver a utilizarlas. También puede convertir una oferta de la biblioteca en una oferta personalizada si desea modificar el contenido de una experiencia. Tras la edición, puede volver a guardar la oferta en la biblioteca.

### Adición y eliminación de experiencias con el modo de Orientación {#adding-and-removing-experiences-using-targeting-mode}

Con el paso Crear del [proceso de orientación](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings), puede añadir y quitar experiencias. Además, puede duplicar una experiencia y también cambiarle el nombre.

#### Adición de experiencias con el modo de Orientación {#adding-experiences-using-targeting-mode}

Para añadir una experiencia:

1. Para agregar una experiencia, toque o haga clic en **+** **Agregar segmentación de experiencias** que aparece debajo de las experiencias existentes en el panel **Audiencias**.
1. Seleccione un público. De forma predeterminada, ese nombre es el nombre de la experiencia. Puede escribir otro nombre, si lo desea. Toque o haga clic en **OK**.

#### Eliminar experiencias con el modo de Orientación {#removing-experiences-using-targeting-mode}

Para eliminar una experiencia:

1. Toque o haga clic en la flecha situada junto al nombre de la experiencia.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Haga clic en **Eliminar**.

#### Cambiar el nombre de las experiencias con el modo de Orientación {#renaming-experiences-using-targeting-mode}

Para cambiar el nombre de las experiencias con el modo de Orientación:

1. Toque o haga clic en la flecha situada junto al nombre de la experiencia.
1. Haga clic en **Cambiar nombre de experiencia** y escriba el nombre nuevo.
1. Toque o haga clic en otro lugar de la pantalla para guardar los cambios.

#### Edición de públicos con el modo de Orientación {#editing-audiences-using-targeting-mode}

Para editar los públicos con el modo de Orientación:

1. Toque o haga clic en la flecha situada junto al nombre de la experiencia.
1. Haga clic en **Editar audiencia** y seleccione una audiencia nueva.
1. Haga clic en **Aceptar**.

#### Duplicar experiencias con el modo de Orientación {#duplicating-experiences-using-targeting-mode}

Para copiar experiencias con el modo de Orientación:

1. Toque o haga clic en la flecha situada junto al nombre de la experiencia.
1. Haga clic en **Duplicar** y elija el público.
1. Cambie el nombre de la experiencia, si lo desea, y haga clic en **OK**.

### Creación de ofertas con el modo de Orientación {#creating-offers-using-targeting-mode}

Oriente un componente para crear ofertas para las experiencias. Los componentes orientados proporcionan el contenido que se utiliza como ofertas para las experiencias.

* [Oriente un componente existente](/help/sites-authoring/content-targeting-touch.md#creating-a-default-offer-by-targeting-an-existing-component). El contenido se convierte en la oferta de la experiencia predeterminada.
* [Agregue un componente Target](/help/sites-authoring/content-targeting-touch.md#creating-an-offer-by-adding-a-target-component) y, a continuación, agregue contenido al componente.

Después de que se oriente un componente, puede añadir ofertas para cada experiencia:

* [Añada ofertas personalizadas](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer).
* [Añada ofertas de una biblioteca](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

Las herramientas siguientes están disponibles para trabajar con ofertas:

* [Añada una oferta personalizada a una biblioteca de ofertas](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library).
* [Convierta una oferta de la biblioteca en una oferta personalizada](/help/sites-authoring/content-targeting-touch.md#converting-a-library-offer-to-a-custom-library).
* [Abra una oferta de la biblioteca y modifique el contenido](/help/sites-authoring/content-targeting-touch.md#editing-a-library-offer).

#### Creación de una oferta predeterminada mediante la orientación de un componente existente {#creating-a-default-offer-by-targeting-an-existing-component}

Oriente un componente de la página para utilizarlo como la oferta para la experiencia predeterminada de la actividad. Al orientar un componente, se ajusta en un componente Target y su contenido se convierte en la oferta para la experiencia predeterminada.

Al orientar un componente, solo ese componente se puede utilizar en la oferta. No es posible quitar el componente de la oferta ni añadir otros componentes a la oferta.

Lleve a cabo el procedimiento siguiente después de [iniciar el proceso de orientación](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings).

1. Toque o haga clic en el componente que se va a orientar. Se muestra la barra de herramientas para el componente, similar a la del ejemplo siguiente.

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. Toque o haga clic en el icono Target.

   ![](do-not-localize/chlimage_1.png)

   El contenido del componente es la oferta para la experiencia predeterminada. Al orientar un componente, el nodo predeterminado se replicará para cada experiencia. Esto es necesario para editar el nodo de contenido adecuado durante la creación específica de la experiencia. Para estas experiencias no predeterminadas, [agregue una oferta personalizada](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) o [agregue una oferta de la biblioteca](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

#### Creación de una oferta mediante la adición de un componente Target {#creating-an-offer-by-adding-a-target-component}

Añada un componente Target para crear la oferta para la experiencia predeterminada. El componente Target es un contenedor para otros componentes, y los componentes que se encuentran en él se orientan. Al utilizar el componente Target, puede añadir varios componentes para crear una oferta. Asimismo, puede utilizar distintos componentes en cada experiencia para crear diferentes ofertas.

Consulte [Configurar las opciones del componente Target](/help/sites-authoring/content-targeting-touch.md#configuring-target-component-options) para obtener información sobre cómo personalizar este componente.

>[!NOTE]
>
>Las ofertas que crea mediante la [consola Ofertas](/help/sites-authoring/offerlib.md) también pueden contener varios componentes. Estas ofertas pertenecen a una biblioteca de ofertas y se pueden utilizar para varias experiencias.

Dado que el componente Target es un contenedor, aparece como un área de colocación de otros componentes.

En el modo de Target, el componente Target tiene un borde azul y el mensaje de destino indica la naturaleza de la orientación.

![chlimage_1-19](assets/chlimage_1-19.png)

En el modo de Edición, el componente Target tiene un icono de diana.

![](do-not-localize/chlimage_1-1.png)

Los componentes que arrastra al componente Target son componentes orientados.

![chlimage_1-20](assets/chlimage_1-20.png)

Al añadir un componente al componente Target, proporciona contenido para una experiencia determinada. Para especificar la experiencia, debe seleccionarla antes de añadir los componentes.

Puede añadir un componente Target a la página en modo de Edición o en modo de Target. Puede añadir componentes al componente Target solo en modo de Target. El componente Target pertenece al grupo de componentes de personalización.

Antes de poder editar contenido orientado, debe tocar o hacer clic en **Iniciar orientación**.

1. Arrastre el componente Target a la página en la que desea que aparezca la oferta.
1. De forma predeterminada, no se establece ningún identificador de ubicación. Toque o haga clic en la rueda de engranaje de configuración para definir la ubicación.

   >[!NOTE]
   >
   >Si la establece el administrador, es posible que deba definir la ubicación de forma explícita.
   >
   >
   >Los administradores pueden decidir si esta configuración es necesaria en **https://&lt;host>:&lt;port>/system/console/configMgr/com.day.cq.personalization.impl.servlets.TargetingConfigurationServlet**
   Para requerir que los usuarios introduzcan una ubicación, active la casilla de verificación **Forzar ubicación **.

1. Seleccione la experiencia para la que desea crear la oferta.
1. Cree la oferta:

   * Para la experiencia predeterminada, arrastre los componentes al área de colocación orientada y edite las propiedades de los componentes como de costumbre para crear el contenido de la oferta.
   * Para las experiencias no predeterminadas, [añada una oferta personalizada](#adding-a-custom-offer) o [añada una oferta de la biblioteca](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library).

#### Adición de una oferta personalizada {#adding-a-custom-offer}

Para crear una oferta, cree el contenido de un componente orientado en modo de Orientación. Al crear una oferta personalizada, se utiliza como la oferta para una sola experiencia.

Si decide que la oferta se puede utilizar para otras experiencias, puede crear una oferta personalizada y [agregarla a la biblioteca](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library). Para obtener información sobre el uso de la consola Ofertas para crear una oferta reutilizable, consulte [Agregar una oferta a una biblioteca de ofertas](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library).

1. Seleccione la experiencia a la que añade la oferta.
1. Para mostrar el menú de componentes, toque o haga clic en el componente orientado al que va a añadir la oferta.

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. Toque o haga clic en el icono +.

   El contenido de la oferta predeterminada se utiliza como la oferta para la experiencia actual.

1. Toque o haga clic en la oferta para mostrar el menú Oferta y, a continuación, toque o haga clic en el icono Editar.

   ![](do-not-localize/chlimage_1-2.png)

1. Edite el contenido del componente.

#### Adición de una oferta de una biblioteca de ofertas {#adding-an-offer-from-an-offer-library}

Agregue una oferta de la [biblioteca de ofertas](/help/sites-authoring/offerlib.md) a una experiencia. Puede agregar cualquier oferta de la biblioteca de la marca que está actualmente orientando.

No puede añadir ofertas de la biblioteca a la experiencia predeterminada.

1. Seleccione la experiencia a la que añade la oferta.
1. Para mostrar el menú de componentes, toque o haga clic en el componente orientado al que va a añadir la oferta.

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. Toque o haga clic en el icono Carpeta.

   ![](do-not-localize/chlimage_1-3.png)

1. Seleccione la oferta de la biblioteca y, a continuación, toque o haga clic en el icono de la marca.

   ![chlimage_1-23](assets/chlimage_1-23.png)

   El selector de ofertas le permite examinar o filtrar las ofertas. Al examinar o filtrar, puede que también desee clasificar las ofertas y cambiar la manera de verlas. El número que aparece en la parte superior derecha indica la cantidad de ofertas que están disponibles en la biblioteca actual.

   * Toque o haga clic en **Examinar** para desplazarse a otra carpeta. Se abrirá el panel de navegación; haga clic en la flecha para navegar por las carpetas. Vuelva a tocar o hacer clic en **Examinar** para cerrar el panel de navegación.

   ![chlimage_1-24](assets/chlimage_1-24.png)

   * Toque o haga clic en **Filtrar** para filtrar las ofertas por palabras clave o etiquetas. Introduzca palabras clave y seleccione etiquetas en el menú desplegable. Vuelva a tocar o hacer clic en **Filtrar** para cerrar el panel de filtrado.

   ![chlimage_1-25](assets/chlimage_1-25.png)

   * Para cambiar la manera de ordenar las ofertas, toque o haga clic en la flecha al lado de **La más reciente a la más antigua**. Las ofertas se pueden ordenar de la más reciente a la más antigua o de la más antigua a la más reciente.

   ![chlimage_1-26](assets/chlimage_1-26.png)

   Toque o haga clic en el icono junto a **Ver como** para ver las ofertas como mosaicos o como una lista.

   ![chlimage_1-27](assets/chlimage_1-27.png)

#### Adición de una oferta personalizada a una biblioteca {#adding-a-custom-offer-to-a-library}

Añada una oferta personalizada a la [biblioteca de ofertas](/help/sites-authoring/offerlib.md) cuando desee volver a utilizarla como la oferta para experiencias múltiples. Puede añadir ofertas a la biblioteca de la marca actual que está orientando.

Para obtener información sobre el uso de la consola Ofertas para crear una oferta reutilizable, consulte [Agregar una oferta a una biblioteca de ofertas](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library).

1. Seleccione la experiencia para mostrar la oferta personalizada.
1. Toque o haga clic en la oferta personalizada para ver el menú Oferta y, a continuación, toque o haga clic en el icono **Guardar oferta en biblioteca de ofertas**.

   ![](do-not-localize/chlimage_1-4.png)

1. Escriba un nombre para la oferta, seleccione la biblioteca a la que va a añadir la oferta y, a continuación, toque o haga clic en el icono de la marca.

#### Conversión de una oferta de la biblioteca en una biblioteca personalizada {#converting-a-library-offer-to-a-custom-library}

Convierta una oferta de la biblioteca en una oferta personalizada para cambiar la oferta para la experiencia actual y sin cambiar la oferta en otras experiencias.

1. Seleccione la experiencia para mostrar la oferta de la biblioteca.
1. Toque o haga clic en la oferta de la biblioteca para ver el menú Oferta y, a continuación, toque o haga clic en el icono Convertir a oferta en línea.

   ![](do-not-localize/chlimage_1-5.png)

#### Edición de una oferta de la biblioteca {#editing-a-library-offer}

Abra una oferta de la biblioteca de una experiencia en modo de Orientación para editar la oferta. Los cambios que realice se muestran en todas las experiencias que utiliza la oferta.

1. Seleccione la experiencia para mostrar la oferta de la biblioteca.
1. Convierta la oferta de la biblioteca en una oferta local o personalizada. Consulte [Conversión de una oferta de la biblioteca en una biblioteca personalizada](#converting-a-library-offer-to-a-custom-library).
1. Edite el contenido de la oferta.

1. Vuelva a guardarlo en la biblioteca. Consulte [Adición de una oferta personalizada a una biblioteca](#adding-a-custom-offer-to-a-library).

## Target: configuración de los públicos {#target-configuring-the-audiences}

El paso Target del [proceso de orientación](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) implica la asignación de públicos a las experiencias con que ha trabajado en el paso Crear. En la página Target se muestran los públicos a que se orienta cada experiencia. Puede especificar o cambiar el público para cada experiencia. Si utiliza Adobe Target, también puede crear pruebas A/B que le permiten orientar un porcentaje del tráfico de un público a una experiencia concreta.

### Si usa el direccionamiento de AEM o Adobe Target (segmentación de experiencias)… ... {#if-you-are-using-aem-targeting-or-adobe-target-experience-targeting}

Los públicos aparecen en el lado izquierdo del diagrama de asignación, y las experiencias en el lado derecho.

![chlimage_1-28](assets/chlimage_1-28.png)

Defina un público con un segmento. La configuración de nube de la página determina los segmentos que están disponibles. Cuando la página no está asociada a una configuración de nube de Adobe Target, los segmentos de AEM están disponibles para definir públicos. Cuando la página se asocie a una configuración de nube de Adobe Target, use los segmentos de Target.

Para obtener información sobre los motores de orientación, consulte [Motor de orientación](/help/sites-authoring/personalization.md#targeting-engine).

Una experiencia no debe utilizar más de un público. Un símbolo de advertencia se muestra al lado de una experiencia cuando se asigna a un público asignado a otra experiencia.

![](do-not-localize/chlimage_1-6.png)

### Asociación de experiencias a públicos (AEM o Adobe Target) {#associating-experiences-with-audiences-aem-or-adobe-target}

Utilice el procedimiento siguiente para asociar una experiencia a un público al usar la orientación de AEM (o la orientación de experiencias de Adobe Target):

1. Toque o haga clic en la flecha desplegable que hay junto al cuadro de público asignado a la experiencia.
1. De manera opcional, toque o haga clic en **Editar** y, a continuación, escriba una palabra clave para buscar el segmento que desee.
1. En la lista de públicos, seleccione el público y toque o haga clic en **OK**.

### Si utiliza la prueba A/B (Adobe Target)… ... {#if-you-are-using-a-b-testing-adobe-target}

Si tiene una actividad de prueba A/B, los públicos se encuentran a la izquierda, el porcentaje de visualización de cada experiencia se muestra en la mitad y las experiencias están a la derecha.

Puede cambiar los porcentajes, siempre que sumen el cien por ciento. En una prueba A/B, varias experiencias pueden utilizar a un público.

![chlimage_1-29](assets/chlimage_1-29.png)

### Asociación de públicos y porcentajes de tráfico a la prueba A/B {#associating-audiences-and-traffic-percentages-with-a-b-testing}

1. Toque o haga clic en el cuadro desplegable al lado del público asignado a la experiencia.
1. De manera opcional, haga clic en **Editar** y, a continuación, escriba una palabra clave para buscar el segmento que desee.
1. Toque o haga clic en **OK.**
1. Introduzca porcentajes para configurar la forma en que el tráfico del público se dirige a cada experiencia. El número total debe ser 100.
1. De manera opcional, haga clic en el menú desplegable situado junto al nombre de la experiencia para editarlo.

## Objetivos y configuraciones: configuración de la actividad y definición de objetivos {#goals-settings-configuring-the-activity-and-setting-goals}

El paso Objetivos y configuración del [proceso de direccionamiento](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) consiste en configurar el comportamiento de la actividad de la marca. Especifique cuándo comienza y finaliza la actividad, así como la prioridad de la actividad. Además, realiza un seguimiento de los objetivos. Puede decidir concretamente qué desea medir con sus actividades.

Las métricas de objetivo solo están disponibles si usa Adobe Target como motor de orientación. Debe definir al menos una métrica de objetivo. Si ha configurado Adobe Analytics y tiene una configuración de nube de A4T Analytics, puede seleccionar si desea que el origen del informe sea Adobe Target o Adobe Analytics.

Las métricas de objetivo se miden solo para la campaña publicada.

Si utiliza AEM como motor de orientación:

![chlimage_1-30](assets/chlimage_1-30.png)

Si utiliza Adobe Target como motor de orientación:

![chlimage_1-31](assets/chlimage_1-31.png)

Si utiliza Adobe Target como motor de determinación de objetivos y tiene A4T Analytics configurado en la cuenta, tiene un menú desplegable de **Fuente de informes** adicional:

![chlimage_1-32](assets/chlimage_1-32.png)

Las métricas de éxito siguientes están disponibles (se utilizan para publicar únicamente):

<table>
 <tbody>
  <tr>
   <td><strong>Conversión</strong></td>
   <td><p>El porcentaje de visitantes que hicieron clic en cualquier parte de la experiencia que se está probando. Las conversiones se pueden contabilizar una vez por visitante o cada vez que un visitante completa una conversión. La métrica de conversión se configura en una de las siguientes:</p>
    <ul>
     <li><strong>Visualizó una página</strong> : Puede definir qué página vio la audiencia seleccionando una de las siguientes opciones <strong>La URL es</strong> y, a continuación, definiendo la dirección URL o varias direcciones URL, o seleccionando <strong>La URL contiene</strong> y, a continuación, agregue una ruta o palabra clave.</li>
     <li><strong>Visualizó un mbox</strong> : Puede definir el mbox que vio la audiencia introduciendo el nombre del mbox. Para introducir varios mboxes, haga clic en <strong>Añadir un Mbox</strong>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Ingresos</strong></td>
   <td><p>Ingresos generados por la visita. Puede elegir entre las siguientes métricas de ingresos:</p>
    <ul>
     <li>Ingresos por visitante (RPV)</li>
     <li>Valor de pedido promedio (AOV)</li>
     <li>Ventas totales </li>
     <li>Pedidos</li>
    </ul> <p>Para cualquiera de estas opciones, si se ha visto un mbox indica que se ha alcanzado el objetivo. Puede definir uno o varios mbox.</p> </td>
  </tr>
  <tr>
   <td><strong>Compromiso</strong></td>
   <td><p>Puede medir tres tipos de participación:</p>
    <ul>
     <li>Vistas de la página</li>
     <li>Puntuación personalizada</li>
     <li>Tiempo pasado en el sitio</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Además, hay configuraciones avanzadas que le permiten determinar cómo contar las métricas de éxito. Las opciones incluyen contar la métrica por impresión o una vez por visitante y elegir si conservar al usuario en la actividad o quitarlo.

Use la configuración avanzada para determinar qué sucede **después** de que un usuario llegue a la métrica de objetivo. En la tabla siguiente se muestran las opciones disponibles.

<table>
 <tbody>
  <tr>
   <td><strong>Cuando un usuario encuentra esta métrica de objetivo...</strong></td>
   <td><strong>Selecciona lo siguiente para que suceda...</strong></td>
  </tr>
  <tr>
   <td><strong>Aumentar recuento y mantener el usuario en la actividad</strong></td>
   <td>Especifique cómo se incrementa el recuento:
    <ul>
     <li>Una vez por participante</li>
     <li>En cada impresión, excluidas las actualizaciones de página</li>
     <li>En cada impresión</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Aumentar recuento, liberar usuario y permitir la reentrada</strong></td>
   <td>Seleccione la experiencia que el visitante ve si vuelve a participar en la actividad:
    <ul>
     <li>La misma experiencia</li>
     <li>Experiencia aleatoria</li>
     <li>Experiencia no vista</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Aumentar recuento, liberar usuario y volver a entrar en la barra</strong></td>
   <td>Determine lo que el usuario ve en lugar del contenido de la actividad:
    <ul>
     <li>La misma experiencia, sin seguimiento</li>
     <li>Contenido predeterminado u otro contenido de actividad</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Consulte la [documentación de Adobe Target](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=es) para obtener más información sobre las métricas de éxito.

### Configuración (orientación de AEM) {#configuring-settings-aem-targeting}

Para definir la configuración si utiliza la orientación de AEM:

1. Para especificar el momento en que la actividad comenzará, use el menú desplegable **Iniciar** para seleccionar uno de los valores siguientes:

   * **Al activar**: la actividad se inicia cuando la página que contiene el contenido orientado se activa.
   * **Fecha y hora especificadas**: una hora determinada. Cuando seleccione esta opción, pulse o haga clic en el icono de calendario, seleccione una fecha y especifique la hora a la que desea iniciar la actividad.

1. Para especificar el momento en que la actividad finalizará, use el menú desplegable **Finalizar** para seleccionar uno de los valores siguientes:

   * **Al desactivar**: la actividad finaliza cuando la página que contiene el contenido orientado se desactiva.
   * **Fecha y hora especificadas**: una hora determinada. Al seleccionar esta opción, toque o haga clic en el icono de calendario, seleccione una fecha y especifique la hora de finalización de la actividad.

1. Para especificar una prioridad de la actividad, utilice el regulador para seleccionar **Baja**, **Normal** o **Alta**.

### Configuración de Objetivos y configuraciones (Adobe Target) {#configuring-goals-settings-adobe-target}

Para configurar los objetivos y las configuraciones si utiliza Adobe Target:

1. Para especificar el momento en que la actividad comenzará, use el menú desplegable **Iniciar** para seleccionar uno de los valores siguientes:

   * **Al activar**: la actividad se inicia cuando la página que contiene el contenido orientado se activa.
   * **Fecha y hora especificadas**: una hora determinada. Cuando seleccione esta opción, pulse o haga clic en el icono de calendario, seleccione una fecha y especifique la hora a la que desea iniciar la actividad.

1. Para especificar el momento en que la actividad finalizará, use el menú desplegable **Finalizar** para seleccionar uno de los valores siguientes:

   * **Al desactivar**: la actividad finaliza cuando la página que contiene el contenido orientado se desactiva.
   * **Fecha y hora especificadas**: una hora determinada. Al seleccionar esta opción, toque o haga clic en el icono de calendario, seleccione una fecha y especifique la hora de finalización de la actividad.

1. Para especificar una prioridad de la actividad, utilice el regulador para seleccionar **Baja**, **Normal** o **Alta**.
1. Si ha configurado Adobe Analytics con la cuenta de Adobe Target, se mostrará el menú desplegable **Origen del informe**. Seleccione **Adobe Target** o **Adobe Analytics** como fuente.

   Si selecciona **Adobe Analytics**, seleccione la empresa y el grupo de informes. Si selecciona **Adobe Target**, no hace falta que haga nada.

   ![chlimage_1-33](assets/chlimage_1-33.png)

1. En el área **Métrica de objetivo**, en **Mi objetivo principal**, seleccione la métrica de éxito que desee rastrear (conversión, ingresos, participación) y especifique cómo se mide esa métrica (o qué acción toma la audiencia para indicar que se ha alcanzado un objetivo). Consulte la definición de las métricas de objetivo en la tabla anterior y consulte la [documentación de Adobe Target](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=es) sobre las métricas de éxito.

   Para cambiar el nombre del objetivo, haga clic en los tres puntos de la esquina superior derecha y seleccione **Cambiar nombre**.

   Si necesita borrar todos los campos, haga clic en los tres puntos de la esquina superior derecha y seleccione **Borrar todos los campos**.

   Todas las métricas también tienen configuraciones avanzadas que puede definir. Seleccione **Configuraciones avanzadas** para acceder a las mismas. Consulte la definición de cómo se cuentan las métricas de éxito en la tabla anterior y consulte la [documentación de Adobe Target](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=es).

   >[!NOTE]
   Debe tener un objetivo definido como mínimo.

   ![chlimage_1-34](assets/chlimage_1-34.png)

   >[!NOTE]
   Si falta información en la métrica, la rodeará una línea roja.

1. Haga clic en **Añadir nueva métrica** para configurar métricas de éxito adicionales.

   ![chlimage_1-35](assets/chlimage_1-35.png)

   >[!NOTE]
   Para quitar los objetivos adicionales, toque o haga clic en los tres puntos y en **Eliminar**. AEM requiere que tenga un objetivo definido como mínimo.

1. Si desea tener más control sobre cómo se contabilizan las métricas de éxito, toque o haga clic en **Configuraciones avanzadas** para acceder a las mismas.
1. Haga clic en **Guardar**.

Una vez configuradas, puede [ver el rendimiento de las actividades](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test) que usan Adobe Target (orientación de la experiencia o de la prueba A/B). Además, con la orientación de la prueba A/B, puede [convertir a los ganadores.](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test)

## Simulación de una experiencia {#simulating-an-experience}

Simule la experiencia de un visitante para comprobar que el contenido de la página se muestra como se espera según el diseño del contenido orientado. Al simular, cargue distintos perfiles de usuario y vea el contenido orientado para ese usuario.

Los criterios siguientes determinar el contenido que se muestra al simular la experiencia de un visitante:

* Los datos del almacén de la sesión del usuario (a través de ContextHub).
* Las [actividades que están activadas](/help/sites-authoring/activitylib.md).
* Las [reglas que definen los segmentos](/help/sites-administering/campaign-segmentation.md).
* El contenido de las experiencias en los componentes Target.
* La [configuración del motor de orientación](/help/sites-authoring/activitylib.md).

Si se muestra contenido inesperado en la página al cargar un perfil, compruebe la configuración de cada elemento de la lista.

>[!NOTE]
Si utiliza la prueba A/B, al simular, las experiencias se muestran según el porcentaje de tráfico. Esto se controla mediante Adobe Target, lo que puede dar lugar a resultados inesperados para los autores. (La actividad del autor se sincroniza con las configuraciones específicas que permiten volver a evaluar durante la simulación). Es posible que los autores deban actualizar para ver las otras experiencias según la configuración del tráfico.

Para simular la experiencia del visitante, utilice las herramientas siguientes:

* La actividad Simulación en modo de Orientación: en la página se muestran las ofertas para el usuario seleccionado actualmente en ContextHub. Puede editar las ofertas orientadas al usuario.
* Modo de vista previa: utilice ContextHub para seleccionar a los usuarios y las ubicaciones que cumplen los criterios de los segmentos en que están basadas las experiencias. Al cambiar las selecciones de ContextHub, el contenido orientado cambia según corresponda.

1. Para cambiar al modo de Previsualización, en la barra de herramientas, toque o haga clic en **Previsualización**.
1. En la barra de herramientas, toque o haga clic en el icono de ContextHub.

   ![](do-not-localize/chlimage_1-7.png)

1. Utilice ContextHub para cambiar las propiedades del contexto. Por ejemplo, toque o haga clic en la propiedad Perfil para seleccionar a un usuario diferente.

   ![chlimage_1-36](assets/chlimage_1-36.png)

   La página cambia para mostrar el contenido orientado al contexto actual.

1. Para realizar cambios en las ofertas que se muestran, cambie al modo de Orientación. Con la actividad Simulación seleccionada, edite las ofertas para el contexto que haya configurado en modo de Vista previa.

## Configuración de las opciones del componente Target {#configuring-target-component-options}

Para personalizar el componente Target, acceda a las opciones del componente de una de las dos formas siguientes:

1. Una vez que haya orientado el componente, en el componente Target, toque o haga clic en el componente y, a continuación, en el icono de configuración (rueda de engranaje).

   ![](do-not-localize/chlimage_1-8.png)

   AEM muestra la ventana de opciones del componente Target.

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. Como alternativa, para acceder a estas configuraciones en modo de pantalla completa, en la ventana de opciones del componente Target, toque o haga clic en el icono de pantalla completa.

   ![](do-not-localize/chlimage_1-9.png)

   AEM muestra la ventana de opciones del componente Target a pantalla completa.

   ![chlimage_1-38](assets/chlimage_1-38.png)

1. Configure el componente Target tal y como se describe en las tablas siguientes.

<table>
 <tbody>
  <tr>
   <td><strong>Opción</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><strong>Lugar de residencia</strong></td>
   <td><p>La ubicación es una cadena que da un nombre a la ubicación del contenido de destino y conecta ofertas con lugares (o ubicaciones o componentes) en la página donde se deben colocar esas ofertas.</p> <p>Este campo es un valor genérico.</p> <p>Si introduce una oferta en un componente, la oferta recuerda el identificador de la ubicación. Al ejecutar la página, el motor evalúa los segmentos del usuario y, de acuerdo con ello, soluciona las experiencias de las campañas activas que deben mostrarse. A continuación, comprueba los identificadores de ubicación en la página e intenta hacer coincidir las ofertas con dichos identificadores de ubicación.</p> </td>
  </tr>
  <tr>
   <td><strong>Motor</strong></td>
   <td>Seleccionar entre <strong>Reglas de cliente (sin seguimiento), Adobe Target, ContextHub, </strong>y<strong> Adobe Campaign </strong>en función del motor que desee utilizar.</td>
  </tr>
 </tbody>
</table>

Si selecciona Adobe Target como motor:

![chlimage_1-39](assets/chlimage_1-39.png)

<table>
 <tbody>
  <tr>
   <td><strong>Opción</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><strong>Direccionamiento preciso</strong></td>
   <td><p>Al habilitar el direccionamiento preciso, se indica al componente que espere a que los datos de Client Context o Context Hub estén disponibles antes de enviar la solicitud a Adobe Target. Puede aumentar el tiempo de carga. Para la creación, la orientación precisa siempre está activada.</p> <p>Si selecciona la opción <strong>Direccionamiento preciso</strong> , el mbox realiza una acción <code>mboxDefine</code> primero y un <code>mboxUpdate</code> posteriormente, lo que resulta en una solicitud de Ajax una vez que los datos están disponibles.</p> <p>Si no selecciona la variable <strong>Direccionamiento preciso</strong> , el mbox realiza una acción <code>mboxCreate</code> que genera una solicitud sincrónica de inmediato (en este caso, es posible que no todos los datos de contexto estén disponibles aún).</p> <p><strong>Nota:</strong> Activar o desactivar el direccionamiento preciso en un componente específico no afecta a la configuración establecida globalmente. Siempre puede seleccionar Orientación precisa en el componente para anular la configuración global.</p> </td>
  </tr>
  <tr>
   <td><strong>Incluir segmentos resueltos</strong></td>
   <td><p>Al seleccionar esta casilla de verificación, se incluyen todos los segmentos resueltos en la llamada de mbox y todos los parámetros configurados en la página y en el marco de trabajo.</p> <p>Esto solo funciona en situaciones con XML API en que sincroniza segmentos de AEM. Si dispone de segmentos en AEM que Adobe Target no controla (como segmentos de script), esta opción le permite resolver el segmento en AEM y enviar información a Adobe Target de que el segmento está activo.</p> </td>
  </tr>
  <tr>
   <td><strong>Parámetros heredados de contexto</strong></td>
   <td>Enumera los parámetros de contexto heredados del marco de trabajo de Adobe Target, si los hay, asociados a la página seleccionada.</td>
  </tr>
  <tr>
   <td><strong>Parámetros de contexto</strong></td>
   <td>Haga clic o toque <strong>Añadir campo</strong> para configurar parámetros de contexto adicionales (lo mismo que está disponible en el marco de trabajo de Target). Se aplican los parámetros de contexto añadidos al componente <i>solamente</i> al componente y no a otro componente, como sería el caso si agregara parámetros de contexto directamente al marco de trabajo.</td>
  </tr>
  <tr>
   <td><strong>Parámetros estáticos</strong></td>
   <td>Haga clic o toque <strong>Añadir campo</strong> para configurar parámetros estáticos adicionales (lo mismo que está disponible en el marco de trabajo de Target). Se aplican parámetros estáticos añadidos al componente <i>solamente</i> al componente y no a otro componente, como sería el caso si agregara parámetros estáticos directamente al marco de trabajo. Los parámetros estáticos no proceden del contexto (Client Context o ContextHub).</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
Al seleccionar un componente y hacerlo orientable, AEM también reemplaza el componente e introduce un componente de Adobe Target. (El componente de Adobe Target no solo se utiliza al añadirlo manualmente a la página, sino también al orientar un componente existente).

Si selecciona Client Context (cliente) como motor:

![chlimage_1-40](assets/chlimage_1-40.png)

<table>
 <tbody>
  <tr>
   <td><strong>Opción</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><strong>Opciones del lado del cliente: estrategia</strong></td>
   <td><p>Seleccione una de las siguientes opciones:</p>
    <ul>
     <li><strong>Primero</strong>: la experiencia más alta de la lista, según se ha ordenado en la campaña.</li>
     <li><strong>Aleatorio</strong>: Se utiliza cualquier experiencia.</li>
     <li><strong>Puntuación del flujo de navegación</strong>: se utilizan las etiquetas y las visitas de etiquetas relacionadas que se rastrean en el contexto del cliente. Se comparan los porcentajes de visitas para las etiquetas definidas en la página de teaser.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Seleccione **Adobe Campaign** como motor si integra AEM con Adobe Campaign. Consulte [Integración de AEM con Adobe Campaign](/help/sites-administering/campaign.md) para obtener más información.

Seleccione **ContextHub** como motor si utiliza ContextHub para orientar. Consulte [Configuración de ContextHub.](/help/sites-developing/ch-configuring.md)
