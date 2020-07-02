---
title: Preparación y envío de comunicación interactiva mediante la interfaz de usuario del agente
seo-title: Preparación y envío de comunicación interactiva mediante la interfaz de usuario del agente
description: La interfaz de usuario del agente permite a los agentes preparar y enviar la comunicación interactiva al proceso posterior. El agente realiza las modificaciones necesarias según lo permitido y envía la comunicación interactiva a un proceso de publicación, como correo electrónico o impresión.
seo-description: Preparación y envío de comunicación interactiva mediante la interfaz de usuario del agente
uuid: d1a19b83-f630-4648-9ad2-a22374e31aa9
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 110c86ea-9bd8-4018-bfcc-ca33e6b3f3ba
translation-type: tm+mt
source-git-commit: 4c4a5a15e9cbb5cc22bc5999fb40f1d6db3bb091
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 0%

---


# Preparación y envío de comunicación interactiva mediante la interfaz de usuario del agente {#prepare-and-send-interactive-communication-using-the-agent-ui}

La interfaz de usuario del agente permite a los agentes preparar y enviar la comunicación interactiva al proceso posterior. El agente realiza las modificaciones necesarias según lo permitido y envía la comunicación interactiva a un proceso de publicación, como correo electrónico o impresión.

## Información general {#overview}

Después de crear una comunicación interactiva, el agente puede abrir la comunicación interactiva en la interfaz de usuario del agente y preparar una copia específica del destinatario introduciendo datos y administrando contenido y archivos adjuntos. Por último, el agente puede enviar la comunicación interactiva a un proceso posterior.

Mientras prepara la comunicación interactiva mediante la interfaz de usuario del agente, el agente administra los siguientes aspectos de la comunicación interactiva en la interfaz de usuario del agente antes de enviarla a un proceso de publicación:

* **Datos**: La ficha Datos de la interfaz de usuario del agente muestra todas las variables editables por el agente y las propiedades del modelo de datos de formulario desbloqueadas en la comunicación interactiva. Estas variables/propiedades se crean al editar o crear fragmentos de documento incluidos en la Comunicación interactiva. La ficha Datos también incluye los campos creados en la plantilla de canal XDP/impresión. La ficha Datos solo aparece cuando hay variables, propiedades del modelo de datos de formulario o campos en la comunicación interactiva que el agente pueda editar.
* **Contenido**: En la ficha Contenido, el agente administra el contenido, como fragmentos de documento y variables de contenido, en la Comunicación interactiva. El agente puede realizar los cambios en el fragmento de documento como se permite al crear la comunicación interactiva en las propiedades de esos fragmentos de documento. El agente también puede reordenar, agregar o eliminar un fragmento de documento y agregar saltos de página, si se permite.
* **Datos adjuntos**: La ficha Datos adjuntos aparece en la interfaz de usuario del agente solo si la comunicación interactiva tiene datos adjuntos o si el agente tiene acceso a la biblioteca. El agente puede o no tener permiso para cambiar o editar los archivos adjuntos.

## Preparación de la comunicación interactiva mediante la interfaz de usuario del agente {#prepare-interactive-communication-using-the-agent-ui}

1. Seleccione **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y Documentos]**.
1. Seleccione la comunicación interactiva adecuada y toque **[!UICONTROL Abrir interfaz de usuario]** del agente.

   >[!NOTE]
   >
   >La interfaz de usuario del agente solo funciona si la comunicación interactiva seleccionada tiene un canal de impresión.

   ![openagentiui](assets/openagentiui.png)

   En función del contenido y las propiedades de la comunicación interactiva, aparece la interfaz de usuario del agente con las tres fichas siguientes: Datos, Contenido y Datos adjuntos.

   ![agentuitabs](assets/agentuitabs.png)

   Proceda a introducir datos, administrar el contenido y administrar los archivos adjuntos.

### Introducir datos {#enter-data}

1. En la ficha Datos, introduzca los datos de las variables, las propiedades del modelo de datos de formulario y los campos de plantilla de impresión (XDP), según sea necesario. Rellene todos los campos obligatorios marcados con un asterisco (&amp;ast;) para activar el botón **Enviar** .

   Toque un valor de campo de datos en la previsualización de comunicación interactiva para resaltar el campo de datos correspondiente en la ficha Datos o viceversa.

### Gestionar contenido {#manage-content}

En la ficha Contenido, administre el contenido como fragmentos de documento y variables de contenido en la Comunicación interactiva.

1. Select **[!UICONTROL Content]**. Aparece la ficha de contenido de la comunicación interactiva.

   ![agentuicontenttab](assets/agentuicontenttab.png)

1. Edite los fragmentos de documento, según sea necesario, en la ficha Contenido. Para enfocar el fragmento relevante en la jerarquía de contenido, puede tocar la línea o el párrafo correspondiente en la previsualización de comunicación interactiva o tocar el fragmento directamente en la jerarquía de contenido.

   Por ejemplo, el fragmento de documento con la línea &quot;Realizar un pago en línea ahora ... &quot; se selecciona en la previsualización del gráfico siguiente y se selecciona el mismo fragmento de documento en la ficha Contenido.

   ![contentmodulefocus](assets/contentmodulefocus.png)

   En la ficha Contenido o Datos, al tocar Resaltar los módulos seleccionados en el contenido ( ![resaltado, selectedmodulos incontencicr](assets/highlightselectedmodulesincontentccr.png)) en la parte superior izquierda de la previsualización, puede desactivar o habilitar la funcionalidad para ir al fragmento de documento cuando el texto, el párrafo o el campo de datos relevantes se tocan o seleccionan en la previsualización.

   Los fragmentos que el agente puede editar al crear la comunicación interactiva tienen el icono Editar contenido seleccionado ( ![iconeditselectedcontent](assets/iconeditselectedcontent.png)). Toque el icono Editar contenido seleccionado para iniciar el fragmento en modo de edición y realizar cambios en él. Utilice las siguientes opciones para dar formato y administrar el texto:

   * [Opciones de formato](#formattingtext)

      * [Copiar y pegar texto con formato de otras aplicaciones](#pasteformattedtext)
      * [Resaltar partes del texto](#highlightemphasize)
   * [Caracteres especiales](#specialcharacters)
   * [Métodos abreviados de teclado](/help/forms/using/keyboard-shortcuts.md)
   Para obtener más información sobre las acciones disponibles para varios fragmentos de documento en la interfaz de usuario del agente, consulte [Acciones e información disponible en la interfaz](#actionsagentui)de usuario del agente.

1. Para agregar un salto de página al resultado de impresión de la Comunicación interactiva, coloque el cursor donde desee insertar un salto de página y seleccione Salto de página antes o Salto de página después de ( ![pagebreakbeforeafter](assets/pagebreakbeforeafter.png)).

   Se inserta un marcador de posición de salto de página explícito en la Comunicación interactiva. Para ver la vista de cómo un salto de página explícito afecta a la comunicación interactiva, consulte la previsualización de impresión.

   ![explícitamente pagebreak](assets/explicitpagebreak.png)

   Continúe con la administración de los archivos adjuntos de la Comunicación interactiva.

### Administrar archivos adjuntos {#manage-attachments}

1. Seleccione **[!UICONTROL Datos adjuntos]**. La interfaz de usuario del agente muestra los archivos adjuntos disponibles tal como están configurados al crear la comunicación interactiva.

   Puede optar por no enviar un archivo adjunto junto con la Comunicación interactiva tocando el icono de vista y puede tocar la cruz del archivo adjunto para eliminarlo (si el agente puede eliminarlo u ocultarlo) de la Comunicación interactiva. Para los archivos adjuntos especificados como obligatorios al crear la comunicación interactiva, los iconos Vista y Eliminar están desactivados.

   ![Attachmentsagentui](assets/attachmentsagentui.png)

1. Toque el icono de acceso a la biblioteca (acceso a la ![biblioteca](assets/libraryaccess.png)) para acceder a la biblioteca de contenido e insertar recursos DAM como archivos adjuntos.

   >[!NOTE]
   >
   >El icono Acceso a biblioteca solo está disponible si el acceso a la biblioteca estaba activado al crear la comunicación interactiva (en las propiedades de Contenedor de Documento del canal de impresión).

1. Si el orden de los datos adjuntos no estaba bloqueado durante la creación de la comunicación interactiva, puede reordenarlos seleccionando un archivo adjunto y tocando las flechas hacia abajo y hacia arriba.
1. Utilice la Previsualización web y la Previsualización de impresión para ver si las dos salidas son las que necesita.

   Si considera que las previsualizaciones son satisfactorias, toque **[!UICONTROL Enviar]** para enviar o enviar la comunicación interactiva a un proceso de publicación. O bien, para realizar cambios, salga de la previsualización para volver a realizar los cambios.

## Formato del texto {#formattingtext}

Al editar un fragmento de texto en la interfaz de usuario del agente, la barra de herramientas cambia según el tipo de edición que elija: Fuente, párrafo o Lista:

![typeofformattingbarra de herramientas](assets/typeofformattingtoolbar.png) ![Fuente barra de herramientas](do-not-localize/fonttoolbar.png)

Fuente, barra de herramientas

![Barra de herramientas Párrafo](do-not-localize/paragraphtoolbar.png)

Barra de herramientas Párrafo

![Barra de herramientas Lista](do-not-localize/listtoolbar.png)

Barra de herramientas Lista

### Resaltar/enfatizar partes del texto {#highlightemphasize}

Para resaltar o resaltar partes del texto en un fragmento editable, seleccione el texto y toque Color de resaltado.

![resalttextagentui](assets/highlighttextagentui.png)

### Pegar texto con formato {#pasteformattedtext}

![pegar texto](assets/pastedtext.png)

### Insertar caracteres especiales en el texto {#specialcharacters}

La interfaz de usuario del agente ha incorporado la compatibilidad con 210 caracteres especiales. El administrador puede [añadir compatibilidad con más caracteres especiales personalizados personalizándolos](/help/forms/using/custom-special-characters.md).

#### envío de datos adjuntos {#attachmentdelivery}

* Cuando la comunicación interactiva se procesa con las API del lado del servidor como un PDF interactivo o no interactivo, el PDF procesado contiene archivos adjuntos como archivos PDF adjuntos.
* Cuando se carga un proceso de publicación asociado a una comunicación interactiva como parte del parámetro Enviar mediante la interfaz de usuario del agente, los archivos adjuntos se pasan como parámetro Lista&lt;com.adobe.idp.Documento> inAttachmentDocs.
* Los flujos de trabajo del mecanismo de Envío, como correo electrónico e impresión, también proporcionan archivos adjuntos junto con la versión en PDF de la Comunicación interactiva.

## Acciones e información disponibles en la interfaz de usuario del agente {#actionsagentui}

### Document fragments {#document-fragments}

![](do-not-localize/contentoptionsdocfragments.png)

* **Flechas** arriba/abajo: Flechas para mover los fragmentos de documento hacia arriba o hacia abajo en la Comunicación interactiva.
* **Eliminar**: Si está permitido, elimine el fragmento de documento de la comunicación interactiva.
* **Salto de página antes** (aplicable a fragmentos secundarios del área de destinatario): Inserta un salto de página antes del fragmento de documento.
* **Sangría**: Aumentar o reducir la sangría de un fragmento de documento.
* **Salto de página después** (aplicable a fragmentos secundarios del área de destinatario): Inserta un salto de página después del fragmento de documento.

![docfragoptions](assets/docfragoptions.png)

* Editar (solo fragmentos de texto): Abra el editor de texto enriquecido para editar el fragmento de documento de texto. Para obtener más información, consulte [Formato del texto](#formattingtext).

* Selección (icono de ojo): Incluye\excluye el fragmento de documento de la comunicación interactiva.
* Valores no rellenados (información): Indica el número de variables sin rellenar en el fragmento de documento.

### Fragmentos de documento de Lista {#list-document-fragments}

![listoptions](assets/listoptions.png)

* Insertar línea en blanco: Inserta una nueva línea en blanco.
* Selección (icono de ojo): Incluye\excluye el fragmento de documento de la comunicación interactiva.
* Omitir viñetas/numeraciones: Active esta opción para omitir viñetas/numeración en el fragmento de documento de lista.
* Valores no rellenados (información): Indica el número de variables sin rellenar en el fragmento de documento.

## Guardar comunicaciones interactivas como borrador {#save-as-draft}

Puede utilizar la interfaz de usuario del agente para guardar uno o varios borradores para cada comunicación interactiva y recuperar el borrador más adelante para continuar trabajando en él. Puede especificar un nombre diferente para cada borrador para identificarlo.

Adobe recomienda ejecutar estas instrucciones de forma secuencial para guardar correctamente una comunicación interactiva como borrador.

### Activar la función Guardar como borrador {#before-save-as-draft}

La función Guardar como borrador no está activada de forma predeterminada. Realice los siguientes pasos para habilitar la función:

1. Implementar la interfaz de Proveedor de servicio [ccrDocumentInstance](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) (SPI). El SPI permite guardar la versión de borrador de la Comunicación interactiva en la base de datos con un ID de borrador como identificador único.
1. Ir a `https://'[server]:[port]'/system/console/configMgr`.
1. Toque **[!UICONTROL Crear configuración]** de correspondencia.
1. Seleccione **[!UICONTROL Activar Guardar con CCRDocumentInstanceService]** y toque **[!UICONTROL Guardar]**.

### Guardar una comunicación interactiva como borrador {#save-as-draft-agent-ui}

Siga estos pasos para guardar una comunicación interactiva como borrador:

1. Seleccione una comunicación interactiva en Forms Manager y toque **[!UICONTROL Abrir interfaz de usuario]** del agente.

1. Realice los cambios correspondientes en la interfaz de usuario del agente y toque **[!UICONTROL Guardar como borrador]**.

1. Especifique el nombre del borrador en el campo **[!UICONTROL Nombre]** y toque **[!UICONTROL Hecho]**.

Una vez guardada la comunicación interactiva como borrador, toque **[!UICONTROL Guardar cambios]** para guardar cualquier cambio adicional en el borrador.

### Recuperar el borrador de una comunicación interactiva {#retrieve-draft}

Después de guardar una comunicación interactiva como borrador, puede recuperarla para seguir trabajando en ella. Recuperar la comunicación interactiva mediante:

`https://server:port/aem/forms/createcorrespondence.hmtl?draftid=[draftid]`

[Draft] hace referencia al identificador único de la versión de borrador que se genera después de guardar una comunicación interactiva como borrador.

>[!NOTE]
>
>Si realiza cambios en la Comunicación interactiva después de guardarla como borrador, la versión de borrador no se abre.
