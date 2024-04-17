---
title: Configuración de segmentación
description: AEM Obtenga información sobre cómo configurar la segmentación para la campaña de.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 6d759907-8796-4749-bd80-306ec7f2c819
solution: Experience Manager, Experience Manager Sites
feature: Administering,Personalization
role: Admin
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 7%

---


# Configuración de segmentación {#configuring-segmentation}

>[!NOTE]
>
>Este documento cubre la configuración de la segmentación tal como se utiliza con Client Context. Para configurar segmentos con ContextHub mediante la IU táctil, consulte [Configuración de la segmentación con ContextHub](/help/sites-administering/segmentation.md).

La segmentación es una consideración clave al crear una campaña. Consulte [Glosario de segmentación](/help/sites-authoring/segmentation-overview.md) para obtener información sobre cómo funciona la segmentación y los términos clave.

Según la información que ya haya recopilado acerca de los visitantes del sitio y los objetivos que desee lograr, debe definir los segmentos y las estrategias necesarios para el contenido de destino.

Estos segmentos se utilizan para proporcionar a un visitante contenido dirigido específicamente. Este contenido se mantiene en la variable [Campañas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md) de la página web. Las páginas de teaser definidas aquí se pueden incluir como párrafos de teaser en cualquier página y definir para qué segmento de visitante se aplica el contenido especializado.

AEM le permite crear y actualizar fácilmente segmentos, teasers y campañas. También le permite verificar los resultados de sus definiciones.

El **Editor de segmentos** permite definir fácilmente un segmento:

![La ventana Editor de segmentos](assets/segmenteditor.png)

Puede **Editar** Seleccione cada segmento para especificar un **Título**, **Descripción** y **Aumentar** factor. Mediante la barra de tareas puede agregar **Y** y **O** contenedores para definir el **Lógica de segmento** y, a continuación, agregue el requerido **Características del segmento** para definir los criterios de selección.

## Factor de ampliación {#boost-factor}

Cada segmento tiene un **Aumentar** parámetro que se utiliza como factor de ponderación; un número mayor indica que el segmento se seleccionará con preferencia sobre un segmento con un número menor.

* Valor mínimo: `0`
* Valor máximo: `1000000`

## Lógica de segmento {#segment-logic}

Los siguientes contenedores lógicos están disponibles de forma predeterminada y le permiten construir la lógica de su selección de segmentos. Se pueden arrastrar de la barra de tareas al editor:

<table>
 <tbody>
  <tr>
   <td> Contenedor Y<br /> </td>
   <td> El operador booleano AND.<br /> </td>
  </tr>
  <tr>
   <td> Contenedor O<br /> </td>
   <td> El operador booleano OR.</td>
  </tr>
 </tbody>
</table>

## Características del segmento {#segment-traits}

Las siguientes características del segmento están disponibles y se pueden arrastrar de la barra de tareas al editor:

<table>
 <tbody>
  <tr>
   <td> Intervalo IP<br /> </td>
   <td>Define un intervalo de direcciones IP que puede tener el visitante.<br /> </td>
  </tr>
  <tr>
   <td> Visitas individuales de página<br /> </td>
   <td>La frecuencia con la que se ha solicitado la página. <br /> </td>
  </tr>
  <tr>
   <td> Propiedad de página<br /> </td>
   <td>Cualquier propiedad de la página visitada.<br /> </td>
  </tr>
  <tr>
   <td> Palabras clave de referencia<br /> </td>
   <td>Palabras clave que coinciden con la información del sitio web de referencia. <br /> </td>
  </tr>
  <tr>
   <td> Script</td>
   <td>Expresión JavaScript que se va a evaluar.<br /> </td>
  </tr>
  <tr>
   <td> Referencia de segmentos <br /> </td>
   <td>Referencia a otra definición de segmento.<br /> </td>
  </tr>
  <tr>
   <td> Nube de etiquetas<br /> </td>
   <td>Etiquetas que deben coincidir con las de las páginas visitadas.<br /> </td>
  </tr>
  <tr>
   <td> Edad del usuario<br /> </td>
   <td>Como se toma del perfil de usuario.<br /> </td>
  </tr>
  <tr>
   <td> Propiedad de usuario<br /> </td>
   <td>Cualquier otra información que esté disponible en el perfil del usuario. </td>
  </tr>
 </tbody>
</table>

Puede combinar estos rasgos mediante los operadores booleanos OR y AND (consulte [Creación de un nuevo segmento](#creating-a-new-segment)) para definir el escenario exacto para seleccionar este segmento.

Cuando toda la instrucción se evalúa como verdadera, este segmento se ha resuelto. Si hay varios segmentos aplicables, la variable **[Aumentar](/help/sites-administering/campaign-segmentation.md#boost-factor)** también se utiliza el factor.

>[!CAUTION]
>
>El editor de segmentos no comprueba la existencia de referencias circulares. Por ejemplo, el segmento A hace referencia a otro segmento B, que a su vez hace referencia al A. Asegúrese de que los segmentos no contengan ninguna referencia circular.

>[!NOTE]
>
>Propiedades con la variable **_i18n** Los sufijos se establecen mediante una secuencia de comandos que forma parte de la interfaz de usuario de la personalización clientlib. Todos los clientlibs relacionados con la interfaz de usuario se cargan en el autor solamente, ya que la interfaz de usuario no es necesaria para la publicación.
>
>Por lo tanto, al crear un segmento con estas propiedades, normalmente es necesario confiar en **browserFamily** por ejemplo, en lugar de **browserFamily_i18n**.

### Creación de un nuevo segmento {#creating-a-new-segment}

Para definir el nuevo segmento:

1. En el carril, elija **Herramientas > Operaciones > Configuración**.
1. Haga clic en **Segmentación** en el panel izquierdo y vaya a la ubicación requerida.
1. Crear un [nueva página](/help/sites-authoring/editing-content.md#creatinganewpage) uso del **Segmento** plantilla.
1. Abra la nueva página para ver el editor de segmentos:

   ![El primer paso para crear un segmento en el Editor de segmentos](assets/screen_shot_2012-02-02at101726am.png)

1. Utilice la barra de tareas o el menú contextual (por lo general, haga clic con el botón secundario del mouse y seleccione **Nuevo...** para abrir la ventana Insertar nuevo componente) y encontrar el rasgo del segmento que necesita. A continuación, arrástrela a **Editor de segmentos** aparecerá en la lista predeterminada **Y** contenedor.
1. Haga doble clic en el nuevo rasgo para editar los parámetros específicos; por ejemplo, la posición del ratón:

   ![Edición de un componente en el Editor de segmentos](assets/screen_shot_2012-02-02at103135am.png)

1. Clic **OK** para guardar su definición:
1. Puede **Editar** la definición del segmento para darle un **Título**, **Descripción** y **[Aumentar](#boost-factor)** factor:

   ![Edición de la configuración de segmentos en el Editor de segmentos](assets/screen_shot_2012-02-02at103547am.png)

1. Añada más rasgos si es necesario. Puede formular expresiones booleanas mediante el complemento **Contenedor Y** y **Contenedor O** componentes encontrados en **Lógica de segmento**. Con el editor de segmentos puede eliminar características o contenedores que ya no se necesitan o arrastrarlos a nuevas posiciones dentro de la instrucción.

### Uso de contenedores AND y OR {#using-and-and-or-containers}

AEM Puede construir segmentos complejos en la. Es útil tener en cuenta algunos puntos básicos:

* El nivel superior de la definición es siempre el contenedor AND que se crea inicialmente; esto no se puede cambiar, pero no afecta al resto de la definición del segmento.
* Asegúrese de que tenga sentido anidar el contenedor. Los contenedores pueden verse como los corchetes de su expresión boolean.

El siguiente ejemplo se utiliza para seleccionar visitantes que están:

Varón y entre 16 y 65 años

OR

Mujer y entre 16 y 62 años

Como el operador principal es OR, debe empezar con un **Contenedor O**. Dentro de esto tiene 2 frases AND, para cada una de ellas necesita una **Contenedor Y**, en el que se pueden añadir los rasgos individuales.

![Ejemplo de los operadores AND y OR en el Editor de segmentos](assets/screen_shot_2012-02-02at105145am.png)

## Prueba de la aplicación de un segmento {#testing-the-application-of-a-segment}

Una vez definido el segmento, se pueden probar los resultados potenciales con la ayuda del **[Client Context](/help/sites-administering/client-context.md)**:

1. Seleccione el segmento que desea probar.
1. Prensa **[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)** para abrir **[Client Context](/help/sites-administering/client-context.md)**, que muestra los datos recopilados. Para realizar pruebas, puede **Editar** determinados valores, o **Cargar** otro perfil para ver el impacto allí.

1. Según los rasgos definidos, los datos disponibles para la página actual pueden coincidir o no con la definición del segmento. El estado de la coincidencia se muestra debajo de la definición.

Por ejemplo, una definición de segmento simple se puede basar en la edad y el sexo del usuario. Al cargar un perfil específico, se muestra que el segmento se ha resuelto correctamente:

![Uso de la ventana Client Context para probar una operación de segmentación AND](assets/screen_shot_2012-02-02at105926am.png)

O no:

![Uso de la ventana Client Context para probar una operación de segmentación NOT](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>Todos los rasgos se resuelven inmediatamente, aunque la mayoría solo cambia al volver a cargar la página. Los cambios en la posición del ratón son visibles inmediatamente, por lo que son útiles para realizar pruebas.

Estas pruebas también se pueden realizar en páginas de contenido y en combinación con **Teaser** componentes.

Al pasar el ratón por encima de un párrafo de teaser, se mostrarán los segmentos aplicados, independientemente de si se resuelven actualmente y, por lo tanto, de por qué se ha seleccionado la instancia de teaser actual:

![Un ejemplo de paso del ratón sobre un segmento](assets/chlimage_1-47.png)

### Uso del segmento {#using-your-segment}

Los segmentos se utilizan actualmente en [Campañas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md). Se utilizan para dirigir el contenido real que ven determinadas audiencias de destino. Consulte [Explicación de los segmentos](/help/sites-authoring/segmentation-overview.md) para obtener más información.
