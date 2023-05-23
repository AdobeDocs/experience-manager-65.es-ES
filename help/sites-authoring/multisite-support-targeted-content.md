---
title: Uso del contenido de destino de varios sitios
seo-title: Working with Targeted Content in Multisites
description: AEM Si necesita administrar contenido de destino, como actividades, experiencias y ofertas, entre sus sitios, puede aprovechar la compatibilidad integrada con varios sitios para el contenido de destino, lo que le permitirá aprovechar las ventajas que ofrece la compatibilidad con múltiples sitios para la administración de contenido de destino.
seo-description: If you need to manage targeted content, such as activities, experiences, and offers between your sites, you can take advantage of AEM's built-in multisite support for targeted content
uuid: acb2ffe1-d846-4580-bb69-d5af860796db
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 4dda6a03-d3ad-4e65-8b37-cee030fa4f7f
exl-id: 5e345ffd-4e9c-467f-8ebb-c798eeb61dea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2872'
ht-degree: 26%

---

# Uso del contenido de destino de varios sitios{#working-with-targeted-content-in-multisites}

AEM Si necesita administrar contenido de destino, como actividades, experiencias y ofertas, entre sus sitios, puede aprovechar la compatibilidad integrada con varios sitios para el contenido de destino, lo que le permitirá aprovechar las ventajas que ofrece la compatibilidad con múltiples sitios para la administración de contenido de destino.

>[!NOTE]
>
>Trabajar con la compatibilidad con varios sitios para el contenido de destino es una función avanzada. Para utilizar esta característica, debe estar familiarizado con el [Administrador de varios sitios](/help/sites-administering/msm.md) y la [integración de Adobe Target](/help/sites-administering/target.md) con AEM.

Este documento describe lo siguiente:

* AEM Proporciona una breve descripción de la compatibilidad de varios sitios con el contenido de destino, a la vez que proporciona información general sobre la compatibilidad con varios sitios.
* Describe algunos escenarios de uso posibles sobre cómo vincular sitios (en una marca).
* Proporciona una guía detallada de ejemplo sobre cómo los especialistas en marketing pueden usar esta característica.
* Instrucciones detalladas sobre cómo implementar la compatibilidad con varios sitios para el contenido de destino.

Para configurar cómo sus sitios comparten contenido personalizado, debe realizar los siguientes pasos:

1. [Crear una nueva área](#creating-new-areas) o [crear una nueva área como live copy](#creating-new-areas). Un área incluye todas las actividades disponibles para un *área* de la página; es decir, la ubicación en la página a la que se dirige el componente. Crear una nueva área crea una área vacía, mientras que crear una nueva área como Live Copy permite heredar el contenido en las estructuras del sitio.

1. [Vincular el sitio o la página](#linking-sites-to-an-area) a un área.

En cualquier momento puede suspender o restaurar la herencia. Además, si no desea suspender la herencia, también puede crear experiencias locales. De forma predeterminada, todas las páginas utilizan el área principal a menos que se especifique lo contrario.

## Introducción a la compatibilidad con varios sitios para contenido de destino {#introduction-to-multisite-support-for-targeted-content}

La compatibilidad con varios sitios para el contenido de destino está disponible de forma predeterminada y le permite insertar contenido de destino desde la página maestra que administra mediante MSM en una Live Copy local o administrar las modificaciones globales y locales de dicho contenido.

Esto se administra en un **Área**. Las áreas separan el contenido de destino (actividades, experiencias y ofertas) que se usa en diferentes sitios y proporcionan un mecanismo basado en MSM para crear y administrar la herencia del contenido de destino junto a la herencia del sitio. AEM Esto evita que tenga que volver a crear contenido de destino en sitios heredados, tal como se requería en versiones anteriores a la versión 6.2.

En un área, solo las actividades vinculadas a ella se insertan en Live Copies. De forma predeterminada, el Área maestra está seleccionada. Después de crear áreas adicionales, puede vincularlas a sus sitios o páginas para indicar qué contenido de destino se inserta.

Un sitio o Live Copy vincula un área que contiene las actividades que deben estar disponibles en ese sitio o Live Copy. De forma predeterminada, el sitio o Live Copy está vinculado al área principal, pero también se pueden vincular otras áreas además del área principal.

>[!NOTE]
>
>Al utilizar la compatibilidad con varios sitios para el contenido de destino, debe tener en cuenta lo siguiente:
>
>* Cuando se utilizan despliegues o Live Copies, se requiere una licencia de MSM.
>* Cuando se utiliza la sincronización con Adobe Target, se requiere una licencia de Adobe Target.
>


## Casos de uso {#use-cases}

Puede configurar la compatibilidad de varios sitios para el contenido de destino de varias formas, según el caso de uso. En esta sección se describe cómo funcionaría teóricamente con una marca. Además, en [Ejemplo: Segmentación de contenido según la geografía](#example-targeting-content-based-on-geography), puede ver una aplicación real de contenido de segmentación en varios sitios.

El contenido dirigido se agrupa en las denominadas áreas, que definen el ámbito de los sitios o las páginas. Estas áreas se definen a nivel de marca. Una marca puede contener varias áreas. Las áreas pueden ser distintas entre marcas. Aunque una marca solo puede contener el área principal y, por lo tanto, se comparte entre todas las marcas, otra marca puede contener varias marcas (por ejemplo, por región). Por lo tanto, las marcas no necesitan reflejar el conjunto de áreas entre ellas.

Con la compatibilidad multisitio para el contenido de destino, puede, por ejemplo, tener dos (o más) sitios con **uno** que tengan una de las siguientes características:

* Un conjunto de contenido de destino totalmente *distinto*: si edita el contenido de destino en uno no afectará al otro. Los sitios vinculados a áreas diferentes leen y escriben en su propia área configurada. Por ejemplo:

   * Vínculos del sitio A al área X
   * Vínculos del sitio B al área Y

* Un conjunto *compartido* de contenido de destino: editar en uno tiene un impacto directo en ambos sitios; puede configurar esto teniendo dos sitios que se refieren a la misma área. Los sitios vinculados a la misma área comparten el contenido dirigido del área. Por ejemplo:

   * Vínculos del sitio A al área X
   * Vínculos del sitio B al área X

* Un conjunto distinto de contenido de destino *heredado* de otro sitio mediante MSM: el contenido se puede trasladar unidireccionalmente desde una copia maestra a una Live Copy. Por ejemplo:

   * Vínculos del sitio A al área X
   * El sitio B vincula al área Y (que es una Live Copy del área X)

También podría tener **múltiple** marcas que se utilizan en un sitio, lo que podría ser más complejo que este ejemplo.

![chlimage_1-270](assets/chlimage_1-270.png)

>[!NOTE]
>
>Para obtener información más técnica sobre esta característica, consulte [Cómo se estructura el sistema de administración de varios sitios para el contenido de destino](/help/sites-authoring/technical-multisite-targeted.md).

## Ejemplo: segmentación de contenido según la ubicación geográfica {#example-targeting-content-based-on-geography}

El uso de varios sitios para el contenido de destino le permite compartir, desplegar o aislar contenido de personalización. Para ilustrar mejor cómo se utiliza esta función, considere un escenario en el que desee controlar cómo se despliega el contenido de destino en función de la ubicación geográfica, como en el siguiente escenario:

Existen cuatro versiones del mismo sitio según la ubicación geográfica:

* El **Estados Unidos** el sitio se encuentra en la esquina superior izquierda y es el sitio maestro. En este ejemplo, está abierto en el modo de Orientación.
* Las otras tres versiones de este sitio son **Canadá**, **Buena Bretaña**, y **Australia**, que son todas Live Copies. Estos sitios están abiertos en el modo de vista previa.

![chlimage_1-271](assets/chlimage_1-271.png)

Cada sitio comparte contenido personalizado en regiones geográficas:

* Canadá comparte el área principal con Estados Unidos.
* La buena Bretaña está vinculada al área europea y hereda del área principal.
* Australia, porque se encuentra en el hemisferio sur y los productos de temporada no se aplicarían; además, tiene su propio contenido personalizado.

![chlimage_1-272](assets/chlimage_1-272.png)

Para el hemisferio norte, contamos con una actividad de invierno que se creó para una audiencia masculina, pero al vendedor de Norteamérica le gustaría tener una imagen de invierno diferente, por lo que la cambia en el sitio de los Estados Unidos.

![chlimage_1-273](assets/chlimage_1-273.png)

Después de actualizar la pestaña, el sitio canadiense cambia a la nueva imagen sin ninguna acción por nuestra parte. Lo hace porque comparte el área principal con Estados Unidos. En los Buenos sitios británicos y australianos, la imagen no cambia.

![chlimage_1-274](assets/chlimage_1-274.png)

El experto en marketing desea implementar estos cambios en la región europea y [despliega la live copy](/help/sites-administering/msm-livecopy.md) al tocar o hacer clic en **Desplegar página**. Después de actualizar la pestaña, el sitio de Buena Bretaña tiene la nueva imagen, ya que el área de Europa hereda del área principal (después del despliegue).

![chlimage_1-275](assets/chlimage_1-275.png)

La imagen en el sitio de Australia permanece sin cambios, que es el comportamiento deseado, ya que es verano en Australia y el experto en marketing no desea cambiar ese contenido. El sitio de Australia no cambia porque no comparte un área con ninguna otra región ni es una Live Copy de otra región. El experto en marketing nunca tiene que preocuparse de que el contenido dirigido del sitio australiano se sobrescriba.

Además, para la Buena Gran Bretaña, cuyo área es una Live Copy del área principal, puede ver el estado de la herencia mediante el indicador verde junto al nombre de la actividad. Si se hereda una actividad, no puede modificarla a menos que suspenda o desasocie la Live Copy.

En cualquier momento, puede suspender la herencia o desasociar la herencia por completo. También puede agregar siempre experiencias locales que solo estén disponibles para esa experiencia sin suspender la herencia.

>[!NOTE]
>
>Para obtener información más técnica sobre esta característica, consulte [Cómo se estructura el sistema de administración de varios sitios para el contenido de destino](/help/sites-authoring/technical-multisite-targeted.md).

### Creación de una nueva área frente a creación de una nueva como Live Copy {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

AEM En el caso de la creación de áreas nuevas o de la creación de áreas nuevas, tiene la opción de crear una Live Copy. La creación de una nueva área agrupa actividades y todo lo que pertenezca a esas actividades, como ofertas, experiencias, etc. Puede crear una nueva área cuando desee crear un conjunto de contenido de destino completamente distinto o cuando desee compartir un conjunto de contenido de destino.

Sin embargo, si tiene la herencia configurada a través de MSM entre los dos sitios, es posible que desee heredar las actividades. En este caso, se crea una nueva área como Live Copy, donde Y es una Live Copy de X y, por lo tanto, hereda también todas las actividades.

>[!NOTE]
>
>La opción predeterminada de despliegue activa las opciones de despliegue siguientes que estén relacionadas con el contenido de destino, siempre que una página sea una Live Copy vinculada a un área que también sea una Live Copy del área vinculada al modelo Páginas.

Por ejemplo, en el siguiente diagrama, hay cuatro sitios donde dos de ellos comparten el área principal (y todas las actividades que forman parte de esa área), uno que tiene un área que es una Live Copy, por lo que comparte las actividades durante el despliegue, y un sitio que es completamente independiente (y que, por lo tanto, requiere un área para sus actividades).

![chlimage_1-276](assets/chlimage_1-276.png)

AEM Para lograr este objetivo en la, debe hacer lo siguiente:

* Vínculos del sitio A al área maestra: no es necesario crear áreas. AEM Área maestra (Master Area) está seleccionada por defecto en la opción de configuración de la. El sitio A y B comparten actividades, etc.
* Vínculos del sitio B al área maestra: no se necesita crear área. AEM Área maestra (Master Area) está seleccionada por defecto en la opción de configuración de la. El sitio A y B comparten actividades, etc.
* El sitio C vincula al área heredada, que es una Live Copy del área maestra: cree un área como Live Copy donde crea una Live Copy basada en el área maestra. El área heredada hereda las actividades del área maestra durante el despliegue.
* El ID del sitio vincula a su propia área aislada: cree un área donde crea una área completamente nueva sin actividades definidas aún. El área aislada no compartirá actividades con ningún otro sitio.

## Creación de nuevas áreas {#creating-new-areas}

Las áreas pueden abarcar actividades y ofertas. Después de crear un área en cualquiera de ellos (por ejemplo, actividades), también tiene el área disponible en el otro (por ejemplo, ofertas).

>[!NOTE]
>
>El área predeterminada denominada Área maestra se contrae de forma predeterminada al pulsar o hacer clic en el nombre de una marca **hasta** crear otra área. A continuación, cuando selecciona una marca en la consola **Actividad** u **Ofertas**, llegará a la consola **Área**.

Para crear una nueva área:

1. Vaya a **Personalización** > **Actividades** u **Ofertas** y, a continuación, a su marca.
1. Haga clic o pulse **Crear área**.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Haga clic en **Área** y haga clic en **Siguiente**.
1. En el **Título** , introduzca un nombre para la nueva área. Si lo desea, seleccione etiquetas.
1. Haga clic o pulse en **Crear**.

   AEM redirige a la ventana de la marca, donde enumera las áreas creadas. Si hay otra área además del área principal, puede crear áreas directamente en la consola de marca.

   ![chlimage_1-278](assets/chlimage_1-278.png)

## Creación de áreas como Live Copies {#creating-areas-as-live-copies}

Puede crear un área como una Live Copy para heredar el contenido de destino en las estructuras del sitio.

Para crear un área como Live Copy:

1. Vaya a **Personalización** > **Actividades** u **Ofertas** y, a continuación, a su marca.
1. Haga clic o pulse **Crear área como Live Copy**.

   ![chlimage_1-279](assets/chlimage_1-279.png)

1. Seleccione el área de la que desea realizar una Live Copy y haga clic en **Siguiente**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. En el campo **Nombre**, introduzca un nombre para la Live Copy. De forma predeterminada, se incluyen las páginas secundarias; para excluirlas, seleccione la casilla de verificación **Excluir páginas secundarias**.

   ![chlimage_1-281](assets/chlimage_1-281.png)

1. En el **Configuraciones de despliegue** , seleccione la configuración adecuada.

   Consulte [Configuraciones de despliegue instaladas](/help/sites-administering/msm-sync.md#installed-rollout-configurations) para obtener descripciones de cada opción.

   Consulte [Creación y sincronización de Live Copies](/help/sites-administering/msm-livecopy.md) para obtener más información sobre live copies.

   >[!NOTE]
   >
   >Cuando una página se transforma en una Live Copy y el área configurada de la página modelo resulta ser también el modelo del área configurada para las Live Copy de las páginas, el valor de LiveAction **personalizationContentRollout** activa un elemento subRollout sincrónico, que forma parte de la **configuración de despliegue estándar**.

1. Haga clic o pulse en **Crear**.

   AEM redirige a la ventana de la marca, donde enumera las áreas creadas. Si hay otra área además del área principal, puede crear áreas directamente desde la ventana de marca.

   ![chlimage_1-282](assets/chlimage_1-282.png)

## Vinculación de sitios a un área {#linking-sites-to-an-area}

Puede vincular áreas a cualquiera de las páginas o a un sitio. Todas las subpáginas heredan las áreas, a menos que dichas páginas se superpongan debido a una asignación en una subpágina. Sin embargo, normalmente se establece el vínculo en el nivel del sitio.

Al vincular, solo están disponibles las actividades, experiencias y ofertas del área seleccionada. Esto evita la mezcla accidental de contenido administrado de forma independiente. Si no se configura ninguna otra área, se utiliza el área principal de cada marca.

>[!NOTE]
>
>Las páginas o los sitios que hacen referencia a la misma área utilizan el *mismo* conjunto compartido de actividades, experiencias y ofertas. Si edita una actividad, experiencia u oferta que compartan varios sitios, esto afectará a todos los sitios.

Para vincular un sitio a un área:

1. Desplácese hasta el sitio (o página) que desee vincular a un área.
1. Seleccione el sitio o la página y toque o haga clic en **Ver propiedades**.
1. Haga clic o pulse la pestaña **Personalización.**
1. En el **Marca** , seleccione la marca con la que desea vincular su área. Después de seleccionar la marca, las áreas disponibles están disponibles en la **Referencia de área** menú.

   ![chlimage_1-283](assets/chlimage_1-283.png)

1. Seleccione el área del menú desplegable **Referencia de área** y haga clic o pulse **Guardar**.

   ![chlimage_1-284](assets/chlimage_1-284.png)

## Desasociar una Live Copy o suspender la herencia del contenido de destino {#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

Puede que desee suspender o desasociar la herencia del contenido de destino. La suspensión o desasociación de la Live Copy se realiza por actividad. Por ejemplo, es posible que desee modificar las experiencias de la actividad, pero si esa actividad sigue vinculada a una copia heredada, no podrá modificar la experiencia ni ninguna de las propiedades de la actividad.

La suspensión de la Live Copy interrumpe temporalmente la herencia, pero en el futuro puede restaurarla. Al desasociar la Live Copy, se interrumpe la herencia de forma permanente.

Suspenda o desasocie la herencia del contenido de destino; para ello, restáurelo en una actividad. Si una página o sitio vincula un área de tipo Live Copy, puede ver el estado de herencia de una actividad.

Una actividad que hereda de otro sitio se marca en verde junto al nombre de la actividad. Una herencia suspendida se marca en rojo y una actividad creada localmente no tiene icono.

>[!NOTE]
>
>* Solo puede suspender o desasociar Live Copies en una actividad.
>* No es necesario suspender ni desasociar Live Copies para ampliar una actividad heredada. Siempre puede crear **nuevo** experiencias y ofertas locales para esa actividad. Si desea modificar una actividad existente, debe suspender la herencia.
>


### Suspender herencia {#suspending-inheritance}

Para suspender o desasociar la herencia del contenido de destino en una actividad:

1. Vaya a la página en la que desea desasociar o suspender la herencia y toque o haga clic en **Segmentación** en el menú desplegable mode.
1. Si la página está vinculada a un área que es una Live Copy, verá el estado de la herencia. Haga clic o pulse **Iniciar segmentación**.
1. Para suspender una actividad, siga uno de estos procedimientos:

   1. Seleccione un elemento de la actividad, como la audiencia. AEM La muestra automáticamente un cuadro de confirmación Suspender Live Copy. (Puede suspender la Live Copy tocando o haciendo clic en cualquier elemento durante el proceso de Segmentación).
   1. Seleccionar **Suspender Live Copy** en el menú desplegable de la barra de herramientas.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Haga clic o pulse **Suspender** para suspender la actividad. Las actividades suspendidas están marcadas en rojo.

   ![chlimage_1-286](assets/chlimage_1-286.png)

### Interrumpir herencia {#breaking-inheritance}

Para interrumpir la herencia del contenido de destino en una actividad:

1. Vaya a la página donde desea separar la Live Copy del patrón y toque o haga clic en **Segmentación** en el menú desplegable mode.
1. Si la página está vinculada a un área que es una Live Copy, verá el estado de la herencia. Haga clic o pulse **Iniciar segmentación**.
1. Seleccione **Separar Live Copy** en el menú desplegable de la barra de herramientas. AEM confirma que desea separar la Live Copy.
1. Haga clic o pulse **Desasociar** para desasociar la live copy de la actividad. Una vez independiente, ya no se muestra el menú desplegable con respecto a la herencia. La actividad es ahora una actividad local.

   ![chlimage_1-287](assets/chlimage_1-287.png)

## Restauración de la herencia del contenido de destino {#restoring-inheritance-of-targeted-content}

Si ha suspendido la herencia del contenido de destino en una actividad, puede restaurarla en cualquier momento. Sin embargo, si ha desvinculado la Live Copy, no puede restaurar la herencia.

Para restaurar la herencia del contenido de destino en una actividad:

1. Desplácese a la página donde desea restaurar la herencia y haga clic o pulse el modo **Segmentación** en el menú desplegable.
1. Haga clic o pulse **Iniciar segmentación**.
1. Seleccione **Reanudar Live Copy** en el menú desplegable de la barra de herramientas.

   ![chlimage_1-288](assets/chlimage_1-288.png)

1. Haga clic o pulse **Reanudar** para confirmar que desea reanudar la herencia de live copy. Las modificaciones realizadas en la actividad actual se pierden si se reanuda la herencia.

## Eliminación de áreas {#deleting-areas}

Cuando se elimina un área, se eliminan, a su vez, todas las actividades que contiene. AEM le advierte antes de que pueda eliminar un área. Si se elimina un área que tenga un sitio vinculado, la asignación de esta marca se reasignará automáticamente al área principal.

Para eliminar un área:

1. Desplácese a **Personalización** > **Actividades** o **Ofertas** y luego a su marca.
1. Toque o haga clic en el icono situado junto al área que desea eliminar.
1. Haga clic o pulse **Eliminar** y confirme que desea eliminar el área.
