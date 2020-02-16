---
title: Crear una comunicación interactiva
seo-title: Crear una comunicación interactiva
description: Cree una comunicación interactiva con el editor de comunicación interactiva. Utilice la función de arrastrar y soltar para crear la comunicación interactiva y previsualizar las salidas de impresión y web en diferentes tipos de dispositivos.
seo-description: Cree una comunicación interactiva con el editor de comunicación interactiva. Utilice la función de arrastrar y soltar para crear la comunicación interactiva y previsualizar las salidas de impresión y web en diferentes tipos de dispositivos.
uuid: d524a3de-00b4-444f-b3c7-be443fa24ec8
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f4d98cb9-84d8-4735-91d2-b9ceec861e5e
docset: aem65
translation-type: tm+mt
source-git-commit: d12d35bf8355d3069071523427a7794b88c09b13

---


# Crear una comunicación interactiva{#create-an-interactive-communication}

## Información general {#overview}

Las comunicaciones interactivas centralizan y gestionan la creación, el ensamblaje y la entrega de correspondencias personalizadas e interactivas. Utilice la impresión como canal maestro para Web, puede minimizar la duplicación de esfuerzos al crear la salida web de la comunicación interactiva.

### Requisitos previos {#prerequisites}

Los siguientes son los requisitos previos para crear una comunicación interactiva:

* Configure un modelo [de datos de](/help/forms/using/data-integration.md) formulario que contenga datos de prueba o un origen de datos real, como una instancia de Microsoft® Dynamics.
* Asegúrese de que tiene los fragmentos [](/help/forms/using/document-fragments.md)de documento.
* Asegúrese de que tiene [plantillas para impresión y canal](/help/forms/using/web-channel-print-channel.md)web.
* Asegúrese de que tiene el [tema](/help/forms/using/themes.md) requerido para el canal Web.

## Crear comunicación interactiva {#createic}

1. Inicie sesión en la instancia de creación de AEM y vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Toque **[!UICONTROL Crear]** y seleccione Comunicación **** interactiva. Aparece la página Crear comunicación interactiva.

   ![create-interactive-Communication](assets/create-interactive-communication.png)

1. Indique la siguiente información. :

   * **[!UICONTROL Título]**: Introduzca el título de la comunicación interactiva.
   * **[!UICONTROL Nombre]**: El nombre de la comunicación interactiva se deriva del título que se introduce. Edite si es necesario.
   * **[!UICONTROL Descripción]**: Escriba una descripción de la comunicación interactiva.
   * **[!UICONTROL Modelo]** de datos de formulario: Explore y seleccione el modelo de datos de formulario. Para obtener más información sobre el modelo de datos de formulario, consulte Integración [de datos de formularios](/help/forms/using/data-integration.md)AEM.

   * **[!UICONTROL Servicio]** de relleno previo: Seleccione el servicio de rellenado previo para recuperar los datos y rellenar previamente la comunicación interactiva.
   * **[!UICONTROL Tipo]** de proceso posterior: Puede seleccionar el flujo de trabajo de AEM o Forms que se activará al enviar la comunicación interactiva. Seleccione el tipo de flujo de trabajo que se va a activar.

   * **[!UICONTROL Post Process]**: Seleccione el nombre del flujo de trabajo que se va a activar. Cuando seleccione Flujo de trabajo de AEM, proporcione Ruta de datos de datos adjuntos, Ruta de diseño, Ruta de acceso a PDF, Ruta de datos de impresión y Ruta de datos web.
   * **[!UICONTROL Etiquetas]**: Seleccione las etiquetas que desee aplicar a la comunicación interactiva. También puede escribir un nombre de etiqueta nuevo o personalizado y pulsar Intro para crearlo.
   * **[!UICONTROL Autor]**: el nombre del autor se toma automáticamente del nombre de usuario del usuario que ha iniciado sesión.
   * **** Fecha de publicación: Introduzca la fecha de publicación de la comunicación interactiva.
   * **[!UICONTROL Fecha]** de cancelación de publicación: Introduzca la fecha para cancelar la publicación de la comunicación interactiva.

1. Puntee **[!UICONTROL Siguiente]**. Aparece la pantalla para especificar los detalles de la impresión y del canal Web.
1. Introduzca lo siguiente:

   * **[!UICONTROL Imprimir]**: Seleccione esta opción para generar el canal de impresión de la comunicación interactiva.
   * **[!UICONTROL Imprimir plantilla]**: Busque y seleccione un XDP como plantilla de impresión.
   * **[!UICONTROL Web]**: Seleccione esta opción para generar el canal web o el resultado interactivo de la comunicación interactiva.
   * **[!UICONTROL Plantilla]** web de comunicación interactiva: Busque y seleccione la plantilla web.
   * **[!UICONTROL Tema]** y **[!UICONTROL seleccionar tema]**: Explore y seleccione el tema para aplicar estilo al canal web de la comunicación interactiva. Para obtener más información, consulte [Temas en AEM Forms](/help/forms/using/themes.md).

   * **[!UICONTROL Usar Imprimir como imagen principal para el canal]** web: Seleccione esta opción para crear el canal web en sincronización con el canal de impresión. El uso del canal de impresión como maestro para el canal web garantiza que el contenido y el enlace de datos del canal web se deriven del canal de impresión y que los cambios realizados en el canal de impresión se reflejen en el canal web al tocar Sincronizar. Sin embargo, los autores pueden romper la herencia de componentes específicos del canal web, según sea necesario. Para obtener más información, consulte [Sincronizar canal Web con canal](../../forms/using/create-interactive-communication.md#synchronize)Imprimir.
Si selecciona la opción **[!UICONTROL Usar Imprimir como principal para el canal]** web, puede seleccionar cualquiera de los siguientes modos para generar el canal web:

      * **[!UICONTROL Diseño]** automático: Seleccione este modo para generar automáticamente marcadores de posición, contenido y enlace de datos para el canal Web desde el canal Imprimir.
      * **[!UICONTROL Organiza** manualmente: Seleccione este modo para seleccionar manualmente y agregar elementos de canal Imprimir al canal Web mediante el contenido maestro disponible en la ficha Fuentes **[!UICONTROL de]** datos. Para obtener más información, consulte [Seleccionar elementos de canal Imprimir para crear contenido](#selectprintchannelelements)de canal Web.
   Para obtener más información sobre el canal de impresión y el canal Web, consulte Canal [de impresión y canal](/help/forms/using/web-channel-print-channel.md)Web.

1. Toque **[!UICONTROL Crear]**. Se crea la comunicación interactiva y aparece un cuadro de alerta. Toque **[!UICONTROL Editar]** para empezar a generar el contenido de la comunicación interactiva, tal como se explica en [Agregar contenido mediante la interfaz](#step2)de usuario de creación de la comunicación interactiva. También puede tocar **[!UICONTROL Listo]** y elegir editar la comunicación interactiva más adelante.

## Agregar contenido a la comunicación interactiva {#step2}

Después de crear una comunicación interactiva, puede utilizar la interfaz de creación de comunicación interactiva para crear su contenido.

Para obtener más información sobre la interfaz de creación de Interactive Communication, consulte [Introducción a la creación](/help/forms/using/introduction-interactive-communication-authoring.md)de Interactive Communication.

1. La interfaz de creación de Interactive Communication se inicia cuando toca Editar como se indica en [Crear comunicación](#createic)interactiva. También puede desplazarse a un recurso de comunicación interactiva existente en AEM, seleccionarlo y tocar **[!UICONTROL Editar]** para iniciar la interfaz de creación de comunicación interactiva.

   De forma predeterminada, aparece el canal de impresión de la comunicación interactiva, a menos que la comunicación interactiva sea solo de canal web. El canal de impresión de la comunicación interactiva muestra las áreas de destino, tal como están disponibles en la plantilla de canal de impresión/XDP seleccionada. En estas áreas y campos de destino, puede agregar componentes o recursos.

1. Con el canal Imprimir seleccionado, seleccione la ficha **[!UICONTROL Componentes]** . Los siguientes componentes están disponibles en el canal de impresión:

   | **Componente** | **Funcionalidad** |
   |---|---|
   | Gráfico | Agrega un gráfico que puede utilizar en Comunicación interactiva para la representación visual de datos bidimensionales recuperados de una colección de modelos de datos de formulario. Para obtener más información, consulte [Uso de gráficos en Interactive Communications](/help/forms/using/chart-component-interactive-communications.md). |
   | Fragmento de documento | Permite agregar un componente reutilizable, como texto, lista o condición, a una comunicación interactiva. El componente agregado puede estar basado en modelo de datos de formulario o sin modelo de datos de formulario. |
   | Imagen | Permite insertar una imagen. |

   Arrastre y suelte los componentes en la comunicación interactiva y configúrelos según sea necesario.

   También puede utilizar las operaciones de deshacer y rehacer mientras crea una comunicación interactiva para los canales Imprimir y Web.

   Utilice la operación de deshacer para descartar la última acción realizada y la operación de rehacer para incorporar de nuevo la acción descartada. Por ejemplo, si ha insertado una imagen o ha creado un enlace de datos en una comunicación interactiva y necesita descartarlo, utilice la operación de deshacer.

   ![Deshacer Rehacer acciones](assets/undo_redo_actions_new.png)

   Las opciones de deshacer y rehacer se muestran en la barra de herramientas de la página de la IU de creación. La opción Deshacer solo se muestra después de realizar una acción. La opción Rehacer se muestra en la barra de herramientas de la página sólo después de realizar una operación de deshacer. Estas acciones se restablecen al actualizar la página.

1. Con el canal de impresión seleccionado, vaya a la ficha **[!UICONTROL Recursos]** y aplique el filtro para mostrar solo los recursos que desee ver.

   Con el navegador de recursos, también puede arrastrar y soltar recursos directamente en áreas de destino de comunicación interactiva.

   ![assets-docfragments](assets/assets-docfragments.png)

1. Arrastre y suelte los fragmentos del documento en la Comunicación interactiva. A continuación se muestran los tipos de fragmentos de documento que puede utilizar en el canal de impresión de la comunicación interactiva.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de fragmento de documento</strong></td>
   <td><strong>Ejemplo de propósito</strong></td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/texts-interactive-communications.md" target="_blank">Texto</a></td>
   <td>Texto para agregar la dirección, el correo electrónico del destinatario y el texto del cuerpo de la carta </td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/conditions-interactive-communications.md" target="_blank">Condición</a></td>
   <td>Condición para agregar la imagen de encabezado adecuada a la comunicación en función del tipo de directiva: Standard o Premium. <br /> </td>
  </tr>
  <tr>
   <td>Lista</td>
   <td>Grupo de fragmentos de documento, incluidos texto, condiciones, otras listas e imágenes. <br /> </td>
  </tr>
 </tbody>
</table>

También puede reemplazar el enlace entre un área de destino y un fragmento de documento soltando el nuevo fragmento en el área de destino mediante la ficha **Recursos** . El sombreado de color azul del área de destino mientras arrastra el fragmento indica que el fragmento de documento se puede soltar en el área de destino.

Para obtener más información sobre los fragmentos de documento, consulte Fragmentos [de documento](/help/forms/using/document-fragments.md).

La interfaz de creación le permite distinguir entre los campos y variables independientes y enlazados dentro de una comunicación interactiva. La interfaz resalta los campos y las variables independientes mediante un borde naranja.

![unbound_fields_variables_highlight_dc](assets/unbound_fields_variables_highlights_dc.jpg)

Además, cuando pasa el ratón sobre estos elementos, se muestra una información de objeto con el mensaje Campo (sin enlazar) o Variable (sin enlazar).

Es posible que en ocasiones no se muestre una variable no enlazada utilizada en un fragmento de documento en la interfaz de creación. Puede deberse a una regla de texto en línea dentro de un fragmento de documento o en el caso de un fragmento de condición. En estos casos, una información de objeto, resaltada en azul, se muestra como parte del fragmento de documento. La información de objeto muestra el número de variables sin enlazar utilizadas dentro de un fragmento de documento.

![Variable desenlazada](assets/df_unbound_variable_new.png)

Toque el fragmento de documento, ![configure_icon](assets/configure_icon.png) (Configurar) y, a continuación, toque **[!UICONTROL Propiedades]** desde la barra de tareas de la comunicación interactiva. La sección **[!UICONTROL Variables y Objetos]** del modelo de datos enumera las variables, incluidas las variables ocultas, y los objetos del modelo de datos utilizados en los fragmentos del documento. Utilice el icono ![Editar](https://helpx.adobe.com/content/dam/help/images/en/edit.png) (Editar) situado junto a cada objeto o variable del modelo de datos para editar las propiedades.

1. Para configurar el enlace de variables, toque una variable, seleccione ![configure_icon](assets/configure_icon.png) (Configurar) y, a continuación, configure las propiedades de enlace en el panel Propiedades de la barra lateral.

   * **Ninguno**: El agente rellenará el valor de la variable.
   * **Fragmento** de texto: Si está seleccionada, puede examinar y seleccionar un fragmento de documento de texto cuyo contenido se procesa en el campo. Solo los fragmentos de documentos de texto pueden enlazarse a variables que no tengan variables dentro.
   * **Objeto** del modelo de datos: Seleccione una propiedad del modelo de datos de formulario cuyo valor se rellene en el campo.
   * **** Valor predeterminado: Puede definir un valor predeterminado para la variable mediante este campo. El valor se muestra al obtener una vista previa de la comunicación interactiva o en la interfaz de usuario del agente.
   * **** Patrón de visualización: También puede definir un formato de visualización para una variable. Seleccione cualquiera de las opciones predefinidas en la lista desplegable **Tipo** para aplicar un formato de visualización a una variable. Seleccione **Personalizado** para definir un patrón de visualización que no esté disponible en la lista. Para obtener más información, consulte Patrones [de visualización](../../forms/using/create-interactive-communication.md#datadisplaypatterns)de datos.
   Vaya a [Variables y Objetos](../../forms/using/create-interactive-communication.md#hiddenvariables) del modelo de datos para configurar el enlace de variables ocultas en el fragmento del documento.

   También puede arrastrar y soltar elementos de origen de datos o fragmentos de documento de texto para configurar el enlace de variables.  Para crear un enlace con cualquiera de los elementos de la fuente de datos, seleccione la ficha Fuentes **de** datos y arrastre y suelte el elemento en el nombre de la variable. El elemento y la variable del origen de datos deben ser del mismo tipo para configurar el enlace correctamente. Si arrastra y suelta un elemento de fuente de datos en una variable ya enlazada, el nuevo elemento reemplaza al anterior para crear un nuevo enlace con la variable. Del mismo modo, seleccione la ficha **Recursos** y arrastre y suelte el fragmento de documento de texto en el nombre de la variable para configurar el enlace entre ellos. El fragmento del documento de texto no debe contener variables.

1. Para agregar una tabla, con el canal de impresión seleccionado, en la ficha **[!UICONTROL Recursos]** aplique el filtro para mostrar solo los fragmentos de diseño. Arrastre y suelte el fragmento de diseño necesario en la comunicación interactiva. Un fragmento de diseño se basa en un XDP y puede utilizarse para crear diseños gráficos o tablas estáticas y dinámicas en Comunicación interactiva que se rellenan con datos dinámicos.

   Ejemplo: Una tabla de diseño para mostrar la prima bruta, el descuento por lealtad % y la disponibilidad de asistencia de emergencia en carretera para las políticas antiguas y nuevas.

   Para obtener más información sobre los fragmentos de diseño, consulte Fragmentos [de documento](/help/forms/using/document-fragments.md).

1. Con el canal de impresión seleccionado, en la ficha **[!UICONTROL Recursos]** aplique el filtro para mostrar imágenes. Arrastre y suelte las imágenes necesarias en la Comunicación interactiva, como el logotipo de la empresa.

   Además, gestione lo siguiente en la Comunicación interactiva:

   * [Adición y configuración de gráficos](/help/forms/using/chart-component-interactive-communications.md)
   * [Sincronización del canal web con el canal de impresión](../../forms/using/create-interactive-communication.md#synchronize)

      * Sincronización automática
      * Cancelar herencia
      * Volver a habilitar la herencia
      * Sincronizar
   * [Datos adjuntos y acceso a la biblioteca](../../forms/using/create-interactive-communication.md#attachmentslibrary)
   * [Propiedades del campo XDP/Layout](../../forms/using/create-interactive-communication.md#xdplayoutfieldproperties)
   * [Agregar reglas a componentes](../../forms/using/create-interactive-communication.md#rules)


1. Cambiar a canal **** web. El canal web aparece en el editor de comunicación interactiva. Al cambiar del canal Imprimir al canal Web por primera vez, se produce la sincronización automática. Para obtener más información, consulte [Sincronización de canales Web desde el canal](../../forms/using/create-interactive-communication.md#synchronize)de impresión.

   Dado que en este ejemplo utilizamos Imprimir como imagen principal de la Web, los marcadores de posición del canal de impresión, el contenido y el enlace de datos se sincronizan con el canal web. Sin embargo, puede cambiar y personalizar el contenido específico en el canal web. [Cancele la herencia](../../forms/using/create-interactive-communication.md#main-pars-header-103384010) de las áreas y variables de destino que se han generado mediante el canal de impresión para poder personalizar el contenido.

   ![webchannelassets](assets/webchannelassets.png)

   Toque el fragmento de documento, ![configure_icon](assets/configure_icon.png) (Configurar) y, a continuación, toque **[!UICONTROL Propiedades]** desde la barra de tareas de la comunicación interactiva. La sección **[!UICONTROL Variables y Objetos]** del modelo de datos enumera las variables, incluidas las variables ocultas, y los objetos del modelo de datos utilizados en los fragmentos del documento. Utilice el icono ![Editar](https://helpx.adobe.com/content/dam/help/images/en/edit.png) (Editar) situado junto a cada objeto o variable del modelo de datos para editar las propiedades. Además, para los fragmentos de documento que se han generado [](../../forms/using/create-interactive-communication.md#main-pars-header-1213963149) automáticamente en el canal Web mediante el canal Imprimir, utilice el icono ![](assets/cancelinheritance.png) (Cancelar herencia) junto a cada objeto y variable del modelo de datos para [cancelar la herencia](../../forms/using/create-interactive-communication.md#main-pars-header-103384010) y poder editarlas.

1. Para agregar componentes adicionales en el canal Web, con el canal Web seleccionado, toque **[!UICONTROL Componentes]**. Arrastre y suelte los componentes en el canal web de la comunicación interactiva según sea necesario y continúe configurándolos.

   | Componentes | Funcionalidad |
   |---|---|
   | Gráfico | Agrega un gráfico que puede utilizar en Comunicación interactiva para la representación visual de datos bidimensionales recuperados de una colección de modelos de datos de formulario. Para obtener más información, consulte [Uso del componente](../../forms/using/chart-component-interactive-communications.md)de gráfico. |
   | Fragmento de documento | Permite agregar un componente, texto, lista o condición reutilizables a una comunicación interactiva. El componente reutilizable que se agrega a una comunicación interactiva puede estar basado en modelos de datos de formulario o sin modelo de datos de formulario. |
   | Imagen | Permite insertar una imagen. |
   | Panel | Permite agregar un [panel](../../forms/using/create-interactive-communication.md#add-panel-component-to-the-web-channel) a la comunicación interactiva. |
   | Tabla | Agrega una tabla que le permite organizar los datos en filas y columnas. |
   | Área de destino | Inserta un área de destino en un canal web para organizar los componentes específicos del canal web. El área de destino es un contenedor sin formato que le permite agrupar componentes específicos de canal web. |
   | Texto | Agrega texto enriquecido al canal web de una comunicación interactiva. El texto también puede utilizar objetos del modelo de datos de formulario para hacer que el contenido sea dinámico. |
   | Botón | Permite agregar un [botón](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) a la comunicación interactiva. Puede utilizar el componente Botón para desplazarse a otras comunicaciones interactivas, formularios adaptables, otros recursos, como imágenes o fragmentos de documentos, o a una URL externa. |
   | Separador | Permite insertar una línea horizontal dentro de una comunicación interactiva. Utilice este componente para distinguir entre secciones de una correspondencia. Por ejemplo, puede utilizar el componente Separador para distinguir entre las secciones Detalles del cliente y Detalles de la tarjeta de crédito en un estado de cuenta de tarjeta de crédito. |

1. Si es necesario, inserte recursos en el canal web.

   Puede [obtener una vista previa de la comunicación](#previewic) interactiva para ver el aspecto de las salidas de impresión y web de la comunicación interactiva y seguir realizando los cambios necesarios.

## Vista previa de la comunicación interactiva {#previewic}

Puede utilizar la opción **** Vista previa para evaluar el aspecto de la comunicación interactiva. El canal web de comunicación interactiva también ofrece una opción para emular la experiencia de una comunicación interactiva para varios dispositivos. Por ejemplo, iPhone, iPad y Escritorio. Puede utilizar las opciones **Vista previa** y **Regla de** emulador ![en conjunto](assets/ruler.png) para obtener una vista previa de las salidas web para dispositivos de diferentes tamaños de pantalla. Los datos de ejemplo de la vista previa se rellenan desde el modelo de datos de formularios especificado.

1. Seleccione el canal (de impresión o web) para previsualizar y tocar la vista previa. Aparece la comunicación interactiva.

   >[!NOTE]
   >
   >La vista previa se rellena con los datos de ejemplo del modelo de datos de formulario especificado. Para obtener más información sobre la vista previa de la comunicación interactiva con otros datos o el uso del servicio de cumplimentación previa, consulte [Uso del modelo](/help/forms/using/using-form-data-model.md) de datos de formulario y [Trabajo con el modelo](/help/forms/using/work-with-form-data-model.md)de datos de formulario.

1. Para el canal web, utilice la ![regla](assets/ruler.png) para ver el aspecto de la comunicación interactiva en varios dispositivos.

   ![webchannelpreview](assets/webchannelpreview.png)

Además, puede [preparar y enviar la comunicación interactiva mediante la interfaz de usuario](/help/forms/using/prepare-send-interactive-communication.md)del agente.

## Configuración de propiedades en Interactive Communication {#configure-properties-in-interactive-communication}

### Datos adjuntos y acceso a la biblioteca {#attachmentslibrary}

En el canal Imprimir, puede configurar los archivos adjuntos y el acceso a la biblioteca para permitir que el agente administre los archivos adjuntos en la interfaz de usuario del agente para la comunicación interactiva:

1. En el canal Imprimir, resalte el contenedor de documentos y toque **Propiedades**.

   ![documentcontenerpropiedades](assets/documentcontainerproperties.png)

   El panel Propiedades aparece en la barra lateral.

   ![propiedades, datos adjuntos](assets/propertiesattachments.png)

1. Expanda **Archivos adjuntos** y especifique las siguientes propiedades:

   * **[!UICONTROL Permitir acceso]** a la biblioteca: Seleccione esta opción para habilitar el acceso a la biblioteca para el agente en la interfaz de usuario del agente. Si está activado, el agente puede agregar archivos de la biblioteca mientras prepara la comunicación interactiva.
   * **[!UICONTROL Permitir Reordenación De Archivos Adjuntos]**: Seleccione esta opción para permitir que el agente vuelva a ordenar los archivos adjuntos con la comunicación interactiva.
   * **[!UICONTROL Número Máximo De Datos Admitidos]**: Especifique el número máximo de datos adjuntos permitidos con la comunicación interactiva.
   * **[!UICONTROL Archivos Para Adjuntar]**: Toque **[!UICONTROL Agregar]** y busque para seleccionar los archivos que desea adjuntar y especifique lo siguiente:

      * **[!UICONTROL Adjuntar este archivo al documento de forma predeterminada]**: Puede cambiar esta opción si sólo el archivo adjunto no es obligatorio.
      * **** Obligatorio: El agente no podrá quitar los datos adjuntos en la interfaz de usuario del agente.
   ![archivos adjuntos](assets/attachfiles.png)

1. Puntee **[!UICONTROL Listo]**.

### Propiedades del campo XDP/Layout {#xdplayoutfieldproperties}

1. Mientras edita el canal de impresión de una comunicación interactiva, pase el ratón sobre un campo, que se ha creado en la plantilla de canal de impresión, y seleccione ![configure_icon](assets/configure_icon.png) (Configurar).

   El cuadro de diálogo Propiedades aparece en la barra lateral.

   ![data_display_pattern_fields](assets/data_display_patterns_fields.jpg)

1. Especifique lo siguiente:

   * **[!UICONTROL Nombre]**: Nombre del nodo JCR.
   * **[!UICONTROL Título]**: Escriba un título que será visible para el agente en la interfaz de usuario del agente y en el árbol Contenedor del documento.
   * **[!UICONTROL Tipo]** de enlace: Seleccione uno de los siguientes tipos de enlace para el campo.

      * Ninguno: El agente rellenará el valor de la propiedad.
      * Fragmento de texto: Si está seleccionada, puede examinar y seleccionar un fragmento de documento de texto cuyo contenido se procesa en el campo. También puede arrastrar y soltar el fragmento de documento de texto en el nombre del campo para configurar el enlace entre ellos. El fragmento del documento de texto no debe contener variables.
      * Objeto del modelo de datos: Seleccione una propiedad del modelo de datos de formulario cuyo valor se rellene en el campo. También puede seleccionar la ficha Fuentes **de** datos y arrastrar y soltar la propiedad en el campo.
   * **[!UICONTROL Valores]** predeterminados: El valor predeterminado garantiza que el campo no esté vacío cuando el objeto del modelo de datos o fragmento de texto especificado no proporcione ningún valor. Si el tipo de enlace de datos es ninguno, el valor predeterminado se rellena previamente en el campo.
   * **[!UICONTROL Patrón]** de visualización: También puede definir un formato de visualización para un campo. Seleccione cualquiera de las opciones predefinidas en la lista desplegable **Tipo** para aplicar un formato de visualización a un campo. Seleccione **Personalizado** para definir un patrón de visualización que no esté disponible en la lista. Para obtener más información, consulte Patrones [de visualización de datos](../../forms/using/create-interactive-communication.md#datadisplaypatterns)

   * **[!UICONTROL Editable por agente]**: Seleccione esta opción para permitir que el agente edite el valor en el campo en la interfaz de usuario del agente. Esta configuración no se aplica si el tipo de enlace es Fragmento de texto.
   * **[!UICONTROL Etiqueta]**: Especifique una cadena de texto que se muestre con el campo al agente en la interfaz de usuario del agente. Esta configuración no se aplica si el tipo de enlace es Fragmento de texto.
   * **[!UICONTROL Información del objeto]**: Introduzca una cadena de texto que estará visible al pasar el ratón por encima del agente en la interfaz de usuario del agente. Esta configuración no se aplica si el tipo de enlace es Fragmento de texto.
   * **[!UICONTROL Requerido]**: Seleccione esta opción para que el campo sea obligatorio para el agente. Esta configuración no se aplica si el tipo de enlace es Fragmento de texto.
   * **[!UICONTROL Permitir varias líneas]**: Seleccione este campo para permitir varias líneas de texto como entrada en el campo. Esta configuración no se aplica si el tipo de enlace es Fragmento de texto.


1. Toque ![done_icon](assets/done_icon.png).

### Patrones de visualización de datos {#datadisplaypatterns}

La interfaz de creación permite definir patrones de visualización de datos para campos, variables y elementos del modelo de datos de formulario disponibles al crear una comunicación interactiva para canales web e impresos.

Para configurar el patrón de visualización de datos, toque el elemento, seleccione ![configure_icon](assets/configure_icon.png) (Configurar) y configure el patrón de visualización en el panel **[!UICONTROL Propiedades]** de la barra lateral. Seleccione cualquier opción predefinida en la lista desplegable **[!UICONTROL Tipo]** para ver el patrón asociado al tipo seleccionado. Seleccione **[!UICONTROL Personalizado]** en la lista desplegable **[!UICONTROL Tipo]** para definir un patrón que no esté disponible en la lista. La edición de valores en el campo **[!UICONTROL Patrón]** modifica automáticamente el tipo a **[!UICONTROL Personalizado]**.

Para aplicar el patrón de visualización, el número de caracteres o dígitos definidos en el campo Patrón debe coincidir o superar los caracteres o dígitos definidos en el valor de los campos, variables y elementos del modelo de datos de formulario. For more information, see [example](../../forms/using/create-interactive-communication.md#greaternumberofdigits).

![data_display_pattern_example](assets/data_display_patterns_ssn_new.png)

Puede volver a definir el patrón de visualización para un elemento de campo, variable o modelo de datos de formulario después de generar contenido web a partir del canal de impresión. Como resultado, un elemento puede tener diferentes patrones de visualización definidos para los canales web e impresos. Si no define un patrón de visualización para un elemento en el canal de impresión y genera automáticamente contenido web mediante el canal de impresión, el enlace de datos definido para el elemento en el canal de impresión define las opciones de patrón de visualización disponibles en la lista desplegable **[!UICONTROL Tipo]** . Si no hay ningún enlace definido para el elemento, el tipo de datos del elemento define las opciones de patrón de visualización disponibles. Por ejemplo, si crea un enlace de datos de tipo Número para un elemento en el canal de impresión, las opciones de patrón de visualización disponibles en la lista desplegable **[!UICONTROL Tipo]** son de tipo Número en varios formatos.

Cambie al modo de **vista previa** o abra la interfaz de usuario del agente para ver el patrón de visualización aplicado a estos elementos.

En la tabla siguiente se muestra un ejemplo de los valores que se muestran como resultado de configurar el patrón de visualización de datos para una variable:

| Tipo | Valor predeterminado | Patrón de visualización | Valor de visualización | Descripción |
|---|---|---|---|---|
| Número de la Seguridad Social | 123456789 | text{999-99-999} | 123-45-6789 | El número de dígitos del campo de valor predeterminado coincide con el número de dígitos del campo Patrón. El valor basado en el patrón se muestra correctamente. |
| Número de la Seguridad Social | 1234567 | text{999-99-999} | 1-23-4567 | El número de dígitos en el campo de valor predeterminado es menor que el número de dígitos en el campo Patrón. El patrón se aplica a los 7 dígitos disponibles. |
| Número de la Seguridad Social | 1234567890 | text{999-99-999} | 1234567890 | El número de dígitos en el campo de valor predeterminado es mayor que el número de dígitos en el campo Patrón. Como resultado, no hay cambios en el valor de visualización. |

Si no se especifica un patrón de visualización para una variable o un elemento de modelo de datos de formulario, se utiliza de forma predeterminada la configuración [de fragmento de documento](https://helpx.adobe.com//experience-manager/6-5/forms/using/interactive-communication-configuration-properties.html) global.

Si no se aplica un patrón de visualización a una variable de tipo de datos numérico, la vista previa de impresión muestra el patrón según la configuración del fragmento de documento global. Si aplica cambios a la configuración de fragmento de documento global predeterminada, la interfaz de usuario del agente seguirá mostrando el patrón según los separadores predeterminados definidos para la configuración regional.

Del mismo modo, para los campos, si no se especifica el patrón de visualización, se aplica al campo el patrón definido al crear la plantilla de impresión (XDP). Si no hay ningún patrón al crear la plantilla de impresión, los patrones predeterminados basados en especificaciones XFA se aplican a los campos.

Además, si el patrón de visualización especificado es incorrecto o no se puede aplicar, los patrones predeterminados basados en especificaciones XFA se aplican a los campos, variables o elementos del modelo de datos de formulario.

## Aplicación de reglas a los componentes de comunicación interactiva {#rules}

Para condicionalizar componentes o contenido en la comunicación interactiva, toque el componente o elemento de contenido y seleccione ![createruleicon](assets/createruleicon.png) (Crear regla) para iniciar el Editor de reglas.

Para obtener más información, consulte:

* [Editor de reglas](/help/forms/using/rule-editor.md)
* [Introducción a la creación de comunicación interactiva](/help/forms/using/introduction-interactive-communication-authoring.md)

## Uso de tablas {#tables}

### Tablas dinámicas en comunicación interactiva {#dynamic-tables-in-interactive-communication}

Puede agregar tablas dinámicas en Comunicación interactiva mediante fragmentos de diseño. Los pasos siguientes utilizan un ejemplo de extracto de tarjeta de crédito para ilustrar el uso de un fragmento de diseño para crear una tabla dinámica en una comunicación interactiva.

1. Asegúrese de que el fragmento de diseño necesario para crear la tabla está disponible en AEM.
1. En el canal de impresión de la comunicación interactiva, arrastre y suelte un fragmento de diseño (con una tabla de varias columnas) en un área de destino desde el navegador de recursos.

   ![lf_dragdrop](assets/lf_dragdrop.png)

   Aparece una tabla en el área de diseño Comunicación interactiva.

   ![lf_dragdrop_table](assets/lf_dragdrop_table.png)

1. Especifique el enlace de datos para cada una de las celdas de la tabla. Para crear una fila repetible, inserte las propiedades del modelo de datos de formulario en la fila que pertenezca a una propiedad de colección común.

   1. Puntee en una celda de la tabla y seleccione ![configure_icon](assets/configure_icon.png) (Configurar).

      El cuadro de diálogo Propiedades aparece en la barra lateral.

      ![lf_cell_properties](assets/lf_cell_properties.png)

   1. Configure las propiedades:

      * **[!UICONTROL Nombre]**: Nombre del nodo JCR.
      * **[!UICONTROL Título]**: Escriba un título que estará visible en el editor de comunicación interactiva.
      * **[!UICONTROL Tipo]** de enlace: Seleccione uno de los siguientes tipos de enlace para el campo.

         * **[!UICONTROL Ninguna]**
         * **[!UICONTROL Objeto]** del modelo de datos: El valor de una propiedad del modelo de datos de formulario se rellena en el campo. También puede seleccionar la ficha Fuentes **de** datos y arrastrar y soltar la propiedad en el campo.
      * **[!UICONTROL Objeto]** del modelo de datos: Propiedad del modelo de datos de formulario cuyo valor se rellena en el campo.
      * **[!UICONTROL Valor]** predeterminado: El valor predeterminado garantiza que el campo no esté vacío cuando el objeto del modelo de datos especificado no proporciona ningún valor. El valor predeterminado se rellena previamente en el campo.

      * **[!UICONTROL Editable por agente]**: Seleccione esta opción para permitir que el agente edite el valor en el campo en la interfaz de usuario del agente.
   1. Toque ![done_icon](assets/done_icon.png).



1. Obtenga una vista previa de la comunicación interactiva para ver la tabla representada con los datos.

   ![lf_preview](assets/lf_preview.png)

### Tablas solo para canales Web {#webchanneltables}

Toque el panel raíz en la plantilla Web y toque **+** para agregar un componente **Tabla** a la comunicación interactiva. En la comunicación interactiva se inserta una tabla con dos filas. La primera fila de la tabla representa el encabezado Tabla.

#### Agregar filas y columnas a la tabla {#addrowscolumnstable}

**Para agregar o eliminar columnas:**

1. Toque el cuadro de texto predeterminado en la fila de encabezado de tabla para ver la barra de herramientas de componentes.
1. Seleccione **Agregar columna** o **Eliminar columna** para agregar o eliminar columnas de tabla respectivamente.

![component_toolbar_table1](assets/component_toolbar_table1.png)

**Para agregar o eliminar filas:**

1. Toque cualquiera de las filas de tabla para ver la barra de herramientas de componentes. También puede seleccionar una fila de tabla mediante el navegador de contenido de la barra de tareas de la comunicación interactiva.
1. Seleccione **Agregar fila** o **Eliminar fila** para agregar o eliminar filas de tabla respectivamente. Utilice las opciones **Subir** y **Bajar** disponibles en la barra de herramientas para reorganizar las filas de la tabla.

![Component Toolbar](assets/component_toolbar_table_row_new.png)

******** A. Agregue la fila **B. Eliminar fila** C.**Subir** D. Bajar

#### Agregar o editar texto en celdas de tabla {#addedittexttable}

1. Seleccione el cuadro de texto predeterminado en la celda de la tabla y toque ![](assets/edit.png) (Editar).
1. Escriba el texto en la celda de la tabla y toque ![](assets/done_icon.png) para guardarlo.

#### Creación de enlaces entre celdas de tabla y elementos de objeto del modelo de datos {#createbindingtablecells}

1. Seleccione el cuadro de texto predeterminado en la fila de la tabla y toque ![](assets/edit.png) (Editar).
1. Puntee en la lista desplegable de objetos del Modelo de datos y seleccione la propiedad.
1. Toque para guardar y crear un enlace entre la celda de la tabla y la propiedad del objeto del modelo de datos.

![Crear enlace de datos](assets/create_data_binding_table_new.png)

#### Creación de un hipervínculo para texto en la celda de la tabla {#createhyperlinktable}

1. Seleccione el cuadro de texto predeterminado en la celda de la tabla y toque ![](https://helpx.adobe.com/content/dam/help/images/en/edit.png) (Editar).
1. Seleccione el texto en la celda de la tabla y toque el icono Hipervínculo.
1. Especifique la dirección URL en el campo **Ruta** .
1. Toque ![](assets/done_icon.png) para guardar las propiedades del hipervínculo.

![Crear hipervínculo](assets/create_hyperlink_table_new.png)

#### Crear tablas dinámicas {#createdynamictables}

Puede crear una tabla dinámica solo de canal web en una comunicación interactiva mediante una propiedad de modelo de datos de colección de tipos. Dicha tabla es una representación de las propiedades secundarias de una propiedad de colección. Solo se pueden editar las propiedades de formato de las distintas celdas de la tabla.

1. Cambie al canal Web y luego elija mostrar el explorador de fuentes de datos.
1. Arrastre y coloque una propiedad de colección en un subformulario. Se crea una tabla en el subformulario.
1. Obtenga una vista previa de la tabla en la vista previa web de la comunicación interactiva.

#### Ordenar columnas en una tabla {#sortcolumns}

Puede ordenar los datos en función de cualquier columna de una tabla en la Comunicación interactiva. Los valores de la columna se pueden ordenar en orden ascendente o descendente.

La ordenación se puede aplicar a las columnas de tablas que contengan:

* Texto estático
* Propiedades del objeto del modelo de datos
* Combinación de las propiedades del objeto de modelo de datos y texto estático

Para habilitar la clasificación:

1. Seleccione la tabla y toque ![](assets/configure_icon.png) (Configurar). También puede seleccionar la tabla mediante el navegador de **contenido** de la barra de tareas de la comunicación interactiva.
1. Seleccione **Activar ordenación.**
1. Toque ![](assets/done_icon.png) para guardar las propiedades de la tabla. Los iconos de clasificación, flechas arriba y abajo, en los encabezados de columna representan que la clasificación se ha activado.

   ![Habilitar ordenación](assets/enable_sorting_new-1.png)

1. Cambie al modo **Vista previa** para ver el resultado. La tabla se ordena automáticamente en función de la primera columna de la tabla.
1. Haga clic en el encabezado de columna para ordenar los valores en función de la columna.

   Un encabezado de columna con una flecha hacia arriba representa que:

   * se ordena en función de esa columna.
   * los valores de la columna se muestran en orden ascendente.
   ![Orden ascendente](assets/sorting_ascending_new-1.png)

   Del mismo modo, un encabezado de columna con una flecha hacia abajo representa que los valores de la columna se muestran en orden descendente.

## Editar propiedades de comunicación interactiva {#edit-interactive-communication-properties}

Una vez que haya creado una comunicación interactiva, podrá editar sus propiedades en una etapa posterior.

Utilice la página **Propiedades** para:

* Edite los valores de los campos especificados al crear la comunicación interactiva, como Título y Descripción.
* Agregue o elimine un canal Web para una comunicación interactiva existente.
* Vista previa, descarga o eliminación de la comunicación interactiva
* Abra la interfaz de usuario del [agente](/help/forms/using/prepare-send-interactive-communication.md).

Para acceder a la página **Propiedades** :

1. Inicie sesión en la instancia de creación de AEM y vaya a **Adobe Experience Manager** > **Formularios** > **Formularios y documentos**.
1. Seleccione la comunicación interactiva y toque **Propiedades**.
1. Seleccione la ficha **General** para editar los campos **Título** y **Descripción** .

### Agregar o eliminar el canal Web {#add-or-delete-the-web-channel}

Ejecute los siguientes pasos para agregar el canal Web para una comunicación interactiva existente:

1. En la página **Propiedades** , seleccione la ficha **Canales** .
1. Seleccione la casilla de verificación **Web** y seleccione una plantilla para el canal Web.
1. Seleccione **Usar Imprimir como principal para el canal** Web para habilitar la sincronización entre el canal Web y el canal Imprimir.
1. Toque **Guardar y cerrar** para guardar los cambios.

   Del mismo modo, puede tocar la casilla de verificación **Web** de la ficha **Canales** para eliminar el canal Web de la comunicación interactiva.

## Agregar componente Botón al canal web {#add-button-component-to-the-web-channel}

Puede agregar un botón como componente al canal web de la comunicación interactiva. Defina reglas con el editor [de](../../forms/using/rule-editor.md) reglas para poder navegar a otras comunicaciones interactivas, formularios adaptables, otros recursos como imágenes o fragmentos de documentos o una URL externa al tocar el botón.

Para agregar un botón y definir reglas en él:

1. Toque el panel raíz en la plantilla Web y toque **+** para agregar el componente **Botón** a la comunicación interactiva.
1. Toque el componente de botón y toque ![](assets/edit-rules.png) para definir las reglas al tocar el botón.
1. En la sección **Cuándo** , seleccione **clic** en la lista desplegable de botones que se encuentra en el estado.
1. En la sección **Entonces** :

   1. Seleccione una acción en la lista desplegable. Por ejemplo, seleccione **Navegar** como tipo de acción.

   1. Especifique la URL de la comunicación interactiva, el formulario adaptable, un recurso o una página web. Por ejemplo, especifique la URL en el siguiente formato para navegar a otra comunicación interactiva: https://&lt;nombre-servidor>:&lt;puerto>/editor.html/content/forms/af/&lt;nombre de la comunicación interactiva>/channels/&lt;nombre_canal: imprimir o Web>.html
   1. Especifique la opción para abrir el recurso en la misma ficha, ficha nueva o ventana nueva.
   1. Toque **Listo** y, a continuación, **Cerrar** para guardar la regla.
   Del mismo modo, puede seleccionar otras opciones disponibles en la lista desplegable Tipo de acción, como Invocar servicio y Enviar formulario. Para obtener más información, consulte Editor [de reglas](../../forms/using/rule-editor.md).

1. Obtenga una vista previa de la comunicación interactiva y toque el botón para ver la comunicación interactiva, el formulario adaptable, un recurso o una página web especificada en el paso 4, letra b).

## Agregar el componente Panel al canal Web {#add-panel-component-to-the-web-channel}

El componente Panel es un marcador de posición para agrupar otros componentes y controla cómo se distribuye un grupo de componentes, como acordeón y fichas, en la Comunicación interactiva. Un componente de panel también permite hacer que un grupo de componentes se pueda repetir para el usuario final, como en varias entradas necesarias para rellenar las credenciales educativas.

Realice los siguientes pasos para agregar un componente Panel al canal Web:

1. Inserte el componente **Panel** en el canal Web utilizando cualquiera de las siguientes opciones:

   * Toque un componente, toque **+** y seleccione el componente **Panel** .

   * En el panel Navegador de **componentes** , arrastre y suelte el componente **Panel** en la comunicación interactiva.

   * Toque el **panel** en el panel del navegador de **contenido** y toque **Agregar panel** secundario. Al seleccionar la opción **Agregar panel** secundario, se muestra el cuadro de diálogo **Agregar panel** secundario. Introduzca el título y una descripción y un nombre opcionales para el componente Panel.

1. Toque el panel desde el navegador de **contenido** para realizar acciones adicionales en el panel, como configurar, editar reglas, copiar, eliminar e insertar componentes.

   También puede arrastrar y soltar un panel dentro del navegador de **contenido** para reflejar el cambio en la estructura de la comunicación interactiva en el panel derecho.

## Sincronización del canal web con el canal de impresión {#synchronize}

Al seleccionar Imprimir como principal para el canal Web al crear una comunicación interactiva, el canal Web se crea en sincronización con el canal Imprimir y el contenido y el enlace de datos del canal Web se deriva del canal de impresión y los cambios realizados en el canal de impresión podrían reflejarse en el canal Web al tocar Sincronizar.

Sin embargo, los autores pueden romper la herencia de los componentes del canal web, según sea necesario.

![Crear Web maestra](assets/create_ic_print_master_new-1.png) de impresión ![impresa](assets/create_ic_print_master_web_new-1.png)

### Sincronización automática {#autosync}

Si selecciona la opción **[!UICONTROL Usar Imprimir como principal para el canal]** web, puede seleccionar cualquiera de los siguientes modos para generar el canal web:

* **[!UICONTROL Diseño]** automático: Seleccione este modo para generar automáticamente marcadores de posición, contenido y enlace de datos para el canal Web desde el canal Imprimir.
* **[!UICONTROL Organizar]** manualmente: Seleccione este modo para seleccionar manualmente y agregar elementos de canal Imprimir al canal Web mediante el contenido maestro disponible en la ficha Fuentes de datos. Para obtener más información, consulte [Seleccionar elementos de canal Imprimir para crear contenido](#selectprintchannelelements)de canal Web.

![Crear opciones de IC](assets/create_ic_options_updated_new.png)

>[!NOTE]
>
>Al sincronizar los canales, solo se sincronizan los fragmentos de documento, las imágenes, las condiciones, las listas y los fragmentos de diseño del canal de impresión al canal web. Los subformularios o nodos principales que incluyen dichos elementos no se sincronizan.

### Seleccione Imprimir elementos de canal para crear contenido de canal Web {#selectprintchannelelements}

Si selecciona Imprimir como principal al crear la comunicación interactiva y no selecciona la opción de sincronización automática, también puede arrastrar y soltar elementos del canal Imprimir en la interfaz de creación de canal Web.

Vaya a Fuentes **de** datos > Contenido **** maestro para ver los elementos del canal Imprimir. Arrastre y suelte las áreas, campos o tablas de destino en la interfaz de creación de canales Web. Un icono de círculo azul junto al nombre del elemento indica que el elemento Imprimir canal ya se ha incluido en el canal Web.

![Contenido principal](assets/master_content.png)

### Cancelar herencia {#cancelinheritance}

En el canal web, los componentes se incrustan en las áreas de destino.

Pase el ratón sobre el área o variable de destino relevante en el canal web, seleccione ![cancelar herencia](assets/cancelinheritance.png) (Cancelar herencia) y, a continuación, en el cuadro de diálogo Cancelar herencia, toque **[!UICONTROL Sí]**.

La herencia de los componentes dentro del área de destino se cancela y ahora puede editarlos según sea necesario.

### Volver a activar la herencia {#re-enable-inheritance}

En el canal Web, si ha cancelado la herencia de un componente, puede volver a activarlo. Para volver a habilitar la herencia, pase el ratón sobre el límite del área de destino correspondiente, que incluye el componente, y toque ![volver a habilitar la herencia](assets/reenableinheritance.png).

Aparecerá el cuadro de diálogo Revertir herencia.

![revertinheritance](assets/revertinheritance.png)

Si es necesario, seleccione **[!UICONTROL Sincronizar la página después de revertir la herencia]**. Seleccione esta opción para sincronizar toda la comunicación interactiva. Si no selecciona esta opción, solo se sincronizará el área de destino relevante al restablecer la herencia.

Puntee **[!UICONTROL Sí]**.

### Sincronizar {#synchronize-1}

Si utiliza Imprimir como principal para el canal Web y realiza cambios en el canal Imprimir, puede sincronizar el contenido para llevar los cambios recién realizados al canal Web.

1. Para sincronizar el canal Web con el canal Imprimir, cambie al canal Web y toque el icono Más opciones.

   ![Opciones de sincronización automática](assets/auto_sync_options_new.png)

1. Toque una de las siguientes opciones:

   * **[!UICONTROL Sincronizar con impresión]**: Sincroniza el contenido solo para las áreas de destino en las que no se cancela la herencia.
   * **[!UICONTROL Restablecer]**: Sincroniza el contenido del canal Web con el canal Imprimir y descarta todos los cambios realizados en el canal Web.

### Utilice la barra de herramientas de componentes para realizar acciones en componentes heredados {#componenttoolbar}

Una vez que haya generado automáticamente contenido en el canal web mediante la opción Sincronizar, puede realizar más acciones en los componentes sin cancelar la herencia.

![Component Toolbar](assets/component_toolbar_inherited_web_new.png)

Toque el componente para ver las siguientes opciones:

* **** Copiar: Copie un componente y péguelo en otros lugares de la comunicación interactiva.
* **** Cortar: Mueva un componente de un lugar a otro en la comunicación interactiva.
* **** Insertar componente: Inserte un componente encima del componente seleccionado.
* **** Pegar: Pegue el componente que corte o copió utilizando las opciones descritas anteriormente.
* **** Grupo: Seleccione varios componentes si desea cortar, copiar o pegar varios componentes juntos.
* **** Principal: Seleccione el elemento principal de un componente.
* **** Ver expresión SOM: Vea la expresión [](../../forms/using/using-som-expressions-adaptive-forms.md) SOM del componente.

* **** Agrupar objetos en el panel: Agrupe los componentes de un panel para poder realizar operaciones en dichos componentes simultáneamente. Para obtener más información, consulte Objetos **[de grupo en Panel](../../forms/using/create-interactive-communication.md#main-pars-header-1815149576)**.

* **** Cancelar herencia: [Cancelar la herencia](../../forms/using/create-interactive-communication.md#main-pars-header-103384010) de los componentes dentro del área de destino para editarlos.

### Group objects in Panel {#groupobjectspanel}

La interfaz de creación de canales web facilita la agrupación de los componentes en un panel para poder realizar operaciones en dichos componentes de forma simultánea. La ficha **Contenido** muestra los componentes agrupados como elementos secundarios del panel en el árbol de contenido.

1. Puntee en un componente y seleccione la operación Agrupar ( ![grupo](assets/group.jpg)).
1. Seleccione varios componentes y toque **Agrupar objetos en el panel**.

   ![Objetos de grupo](assets/component_toolbar_group_objects_new.png)

1. En el cuadro de diálogo **Agrupar objetos en panel** , introduzca un nombre para el panel.
1. Introduzca un título y una descripción opcionales para el panel.
1. Haga clic en ![bullet_checkmark](assets/bullet_checkmark.png).

   Los componentes agrupados se muestran como elementos secundarios del panel en el árbol de contenido.

   ![content_tree_groups](assets/content_tree_grouping.png)

