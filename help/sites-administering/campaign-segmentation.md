---
title: Configuración de la segmentación
seo-title: Configuración de la segmentación
description: Obtenga información sobre cómo configurar la segmentación para AEM Campaña.
seo-description: Obtenga información sobre cómo configurar la segmentación para AEM Campaña.
uuid: 604ca34d-cdb9-49ff-8f75-02a44b60a8a2
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c68d5853-684f-42f2-a215-c1eaee06f58a
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 3%

---


# Configuración de la segmentación {#configuring-segmentation}

>[!NOTE]
>
>Este documento cubre la configuración de la segmentación como se utiliza con Client Context. Para configurar segmentos con ContextHub mediante la IU táctil, consulte [Configuración de la segmentación con ContextHub](/help/sites-administering/segmentation.md).

La segmentación es una consideración clave al crear una campaña. Consulte [glosario de segmentación](/help/sites-authoring/segmentation-overview.md) para obtener información sobre cómo funciona la segmentación y los términos clave.

En función de la información que ya haya recopilado sobre los visitantes del sitio y los objetivos que desee alcanzar, deberá definir los segmentos y estrategias necesarios para el contenido objetivo.

Estos segmentos se utilizan para proporcionar un visitante con contenido dirigido específicamente. Este contenido se mantiene en la sección [Campañas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md) del sitio web. Las páginas de teaser definidas aquí se pueden incluir como párrafos de teaser en cualquier página y definir para qué segmento de visitante se aplica el contenido especializado.

AEM le permite crear y actualizar fácilmente segmentos, teasers y campañas. También le permite verificar los resultados de sus definiciones.

El **Editor de segmentos** permite definir fácilmente un segmento:

![](assets/segmenteditor.png)

Puede **Editar** cada segmento para especificar un factor **Título**, **Descripción** e **Ampliar**. Con la barra de tareas, puede agregar contenedores **AND** y **OR** para definir la **Lógica del segmento** y luego agregar las **Características del segmento** necesarias para definir los criterios de selección.

## Factor de ampliación {#boost-factor}

Cada segmento tiene un parámetro **Boost** que se utiliza como factor de ponderación; un número mayor indica que el segmento se seleccionará en lugar de un segmento con un número menor.

* Valor mínimo: `0`
* Valor máximo: `1000000`

## Lógica del segmento {#segment-logic}

Los siguientes contenedores lógicos están disponibles de forma predeterminada y le permiten construir la lógica de la selección de segmentos. Se pueden arrastrar de la barra de tareas al editor:

<table>
 <tbody>
  <tr>
   <td> Contenedor Y<br /> </td>
   <td> El operador booleano AND.<br /> </td>
  </tr>
  <tr>
   <td> Contenedor O<br /> </td>
   <td> Operador booleano OR.</td>
  </tr>
 </tbody>
</table>

## Características del segmento {#segment-traits}

Las siguientes características de segmento están disponibles de forma predeterminada; se pueden arrastrar desde la barra de tareas al editor:

<table>
 <tbody>
  <tr>
   <td> Rango de IP<br /> </td>
   <td>Define un rango de direcciones IP que el visitante puede tener.<br /> </td>
  </tr>
  <tr>
   <td> Visitas de la página<br /> </td>
   <td>Frecuencia con la que se solicitó la página. <br /> </td>
  </tr>
  <tr>
   <td> Propiedad de página<br /> </td>
   <td>Cualquier propiedad de la página visitada.<br /> </td>
  </tr>
  <tr>
   <td> Palabras clave de referencia<br /> </td>
   <td>Palabras clave para coincidir con la información del sitio web de referencia. <br /> </td>
  </tr>
  <tr>
   <td> Script</td>
   <td>Expresión de JavaScript que se va a evaluar.<br /> </td>
  </tr>
  <tr>
   <td> Referencia del segmento <br /> </td>
   <td>Referencia a otra definición de segmento.<br /> </td>
  </tr>
  <tr>
   <td> Nube de etiquetas<br /> </td>
   <td>Etiquetas que se deben comparar con las de las páginas visitadas.<br /> </td>
  </tr>
  <tr>
   <td> Edad del usuario<br /> </td>
   <td>Tomada del perfil del usuario.<br /> </td>
  </tr>
  <tr>
   <td> Propiedad de usuario<br /> </td>
   <td>Cualquier otra información disponible en el perfil del usuario. </td>
  </tr>
 </tbody>
</table>

Puede combinar estas características con los operadores booleanos O y AND (consulte [Creación de un nuevo segmento](#creating-a-new-segment)) para definir el escenario exacto para seleccionar este segmento.

Cuando toda la instrucción se evalúa como true, este segmento se ha resuelto. En el evento de que se apliquen varios segmentos, también se utiliza el factor **[Ampliación](/help/sites-administering/campaign-segmentation.md#boost-factor)**.

>[!CAUTION]
>
>El editor de segmentos no comprueba la existencia de referencias circulares. Por ejemplo, el segmento A hace referencia a otro segmento B, que a su vez hace referencia al segmento A. Debe asegurarse de que los segmentos no contengan referencias circulares.

>[!NOTE]
>
>Las propiedades con el sufijo **_i18n** se establecen mediante una secuencia de comandos que forma parte de la clientlib de la interfaz de usuario de la personalización. Todos los clientes relacionados con la interfaz de usuario se cargan en el autor solo porque la interfaz de usuario no es necesaria durante la publicación.
>
>Por lo tanto, al crear un segmento con estas propiedades, normalmente es necesario confiar en **browserFamily** por ejemplo en lugar de **browserFamily_i18n**.

### Creación de un nuevo segmento {#creating-a-new-segment}

Para definir el nuevo segmento:

1. En el carril, elija **Herramientas > Operaciones > Configuración**.
1. Haga clic en la página **Segmentación** en el panel izquierdo y navegue a la ubicación requerida.
1. Cree una [nueva página](/help/sites-authoring/editing-content.md#creatinganewpage) con la plantilla **Segmento**.
1. Abra la nueva página para ver el editor de segmentos:

   ![](assets/screen_shot_2012-02-02at101726am.png)

1. Utilice la barra de tareas o el menú contextual (normalmente, haga clic con el botón secundario del ratón y seleccione **Nuevo...** para abrir la ventana Insertar nuevo componente) para encontrar la característica de segmento que necesita. Luego arrástrelo al **Editor de segmentos** aparecerá en el contenedor predeterminado **AND**.
1. Haga clic con el botón doble en la nueva característica para editar los parámetros específicos; por ejemplo, la posición del ratón:

   ![](assets/screen_shot_2012-02-02at103135am.png)

1. Haga clic en **Aceptar** para guardar la definición:
1. Puede **Editar** la definición del segmento para darle un factor **Título**, **Descripción** e **[Ampliar](#boost-factor)**:

   ![](assets/screen_shot_2012-02-02at103547am.png)

1. Añada más características si es necesario. Puede formular expresiones booleanas utilizando los componentes **AND Contenedor** y **OR Contenedor** que se encuentran en **Lógica del segmento**. Con el editor de segmentos puede eliminar características o contenedores que ya no necesite o arrastrarlos a nuevas posiciones dentro de la instrucción.

### Uso de Contenedores Y y O {#using-and-and-or-containers}

Puede construir segmentos complejos en AEM. Esto ayuda a tener en cuenta algunos puntos básicos:

* El nivel superior de la definición es siempre el contenedor AND que se crea inicialmente; esto no se puede cambiar, pero no afecta al resto de la definición del segmento.
* Asegúrese de que la anidación del contenedor tenga sentido. Los contenedores se pueden ver como corchetes de la expresión booleana.

El ejemplo siguiente se utiliza para seleccionar visitantes que:

Hombre y entre 16 y 65 años

O

Mujeres y entre 16 y 62 años

Como el operador principal es OR, debe tener un inicio con un **Contenedor OR**. Dentro de esto tiene 2 instrucciones AND, para cada una de ellas necesita un **Contenedor AND**, en el cual puede agregar las características individuales.

![](assets/screen_shot_2012-02-02at105145am.png)

## Prueba de la aplicación de un segmento {#testing-the-application-of-a-segment}

Una vez definido el segmento, los resultados potenciales se pueden probar con la ayuda de **[Client Context](/help/sites-administering/client-context.md)**:

1. Seleccione el segmento que se va a probar.
1. Pulse **[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)** para abrir el **[Client Context](/help/sites-administering/client-context.md)**, que muestra los datos que se han recopilado. Para realizar pruebas, puede **Editar** ciertos valores o **Cargar** otro perfil para ver el impacto allí.

1. Según las características definidas, los datos disponibles para la página actual pueden o no coincidir con la definición del segmento. El estado de la coincidencia se muestra debajo de la definición.

Por ejemplo: una definición de segmento simple puede basarse en la edad y el sexo del usuario. La carga de un perfil específico muestra que el segmento se ha resuelto correctamente:

![](assets/screen_shot_2012-02-02at105926am.png)

O no:

![](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>Todas las características se resuelven inmediatamente, aunque la mayoría solo cambia al volver a cargar la página. Los cambios en la posición del ratón son visibles inmediatamente, por lo que resultan útiles para realizar pruebas.

Estas pruebas también se pueden realizar en páginas de contenido y en combinación con componentes de **teaser**.

Si pasa el ratón por encima de un párrafo de teaser, se mostrarán los segmentos aplicados, tanto si se resuelven actualmente como por qué se ha seleccionado la instancia de teaser actual:

![](assets/chlimage_1-47.png)

### Uso del segmento {#using-your-segment}

Los segmentos se utilizan actualmente en [Campañas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md). Se utilizan para dirigir el contenido real que ven audiencias de destinatario específicas. Consulte [Explicación de los segmentos](/help/sites-authoring/segmentation-overview.md) para obtener más información.
