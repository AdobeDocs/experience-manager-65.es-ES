---
title: Crear correspondencia
seo-title: Crear correspondencia
description: Después de crear una plantilla de carta, puede utilizarla para crear correspondencia en AEM Forms administrando datos, contenido y archivos adjuntos.
seo-description: Después de crear una plantilla de carta, puede utilizarla para crear correspondencia en AEM Forms administrando datos, contenido y archivos adjuntos.
uuid: 48cf2b26-c9b4-4127-9ea0-1b36addbff60
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 87742cb2-357b-421f-b79d-e355887ddec0
docset: aem65
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Crear correspondencia{#create-correspondence}

## Crear correspondencia en la interfaz de usuario Crear correspondencia {#create-correspondence-in-the-create-correspondence-user-interface}

Después de crear una plantilla de [carta en Gestión de correspondencia](../../forms/using/create-letter.md), el usuario/agente/solicitante final puede abrir la carta en la interfaz de usuario Crear correspondencia y crear una correspondencia introduciendo datos, configurando contenido y administrando archivos adjuntos. Finalmente, el agente o ajustador de reclamaciones puede administrar el contenido en el modo de vista previa y enviar la carta.

### Vista previa de la correspondencia {#preview-a-correspondence}

Seleccione la carta que desea previsualizar mediante los pasos siguientes:

1. En la página Letras, pulse **Seleccionar**.
1. Toque la letra adecuada para seleccionarla.

   ![Seleccionar carta](assets/1_selectletter.png)

   Seleccionar carta

1. Para una carta basada en el diccionario de datos, seleccione **Vista previa** > **Vista previa**. O para una carta no basada en el diccionario de datos, seleccione **Vista previa**. También puede situarse sobre una carta (sin seleccionarla) y pulsar el icono Vista previa de carta para previsualizarla.

   >[!NOTE]
   >
   >Si un diccionario de datos no está asociado con la carta, se abre la vista previa de la carta. De lo contrario, si la carta está basada en el diccionario de datos, Gestión de correspondencia muestra las opciones Vista previa y Personalizado en el menú Vista previa y puede seleccionar una de las dos opciones. También puede asociar datos de prueba con un diccionario de datos. Cuando el [diccionario de datos tiene asociados datos de prueba](../../forms/using/data-dictionary.md#p-working-with-test-data-p), al seleccionar la opción de vista previa, la vista previa normal se abre con los datos de prueba rellenados.

1. Para poder procesar una correspondencia al previsualizarla, debe ser administrador o parte de uno de los siguientes grupos:

   * usuarios de formularios (para previsualizar en la instancia de autor)
   * cm-agent-users (para representación en instancia de publicación)

   Si no dispone de los permisos necesarios, solicite al administrador el acceso correspondiente. Para obtener más información sobre la creación y adición de usuarios a grupos, consulte [Adición de usuarios o grupos a un grupo](/help/sites-administering/security.md). Si intenta procesar una correspondencia sin tener los permisos adecuados, aparecerá la página de error 404.

1. Si ha seleccionado **Preview** > **Custom**, se abre un cuadro de diálogo. En el cuadro de diálogo, seleccione un archivo de datos, correspondiente al diccionario de datos, para previsualizar la carta con y, a continuación, seleccione **Preview**. Se crea un archivo de datos basado en un diccionario de datos para una carta específica. Para obtener más información sobre el archivo de datos, consulte [Diccionario de datos](../../forms/using/data-dictionary.md#p-working-with-test-data-p).

   ![Vista previa de la carta](assets/8_previewcustomdatafile.png)

1. La vista previa HTML de la carta (vista previa de formularios móviles) se abre con la pestaña Datos enfocada de forma predeterminada.

   Para obtener más información sobre los formularios móviles y las funciones que admiten, consulte [Diferenciación de funciones entre Mobile Forms y PDF form](https://helpx.adobe.com/livecycle/help/mobile-forms/feature-differentiation-mobile-forms-pdf.html).

   Hay tres pestañas: datos, contenido y archivos adjuntos. Si no hay elementos de datos (variables de marcador de posición y campos de diseño), la carta se abre directamente con la pestaña Content que se muestra. La pestaña Attachments solo está disponible cuando hay archivos adjuntos o el acceso a la biblioteca está habilitado.

   >[!NOTE]
   >
   >Para obtener más información sobre cómo cambiar entre el modo de representación HTML o PDF de la vista previa de letras, consulte [Cambiar el modo de representación de la letra](#changerenditionmode). Para obtener más información sobre la compatibilidad con PDF en Gestión y AEM de correspondencia, consulte [Interrupción de los complementos del explorador NPAPI y su impacto](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html) y [PDF forms en HTML5 Forms](https://helpx.adobe.com/aem-forms/kb/pdf-forms-to-html5-forms.html).

### Introducir datos {#enterdata}

En la pestaña Data , rellene los campos de diseño y los marcadores de posición disponibles.

1. Introduzca las variables de datos y contenido en los campos según sea necesario. Complete todos los campos obligatorios marcados con un asterisco (*) para habilitar el botón **Submit**.

   Pulse un valor de campo de datos en la vista previa de la carta HTML para resaltar el campo de datos correspondiente en la pestaña Data .

   ![Introduzca los datos en la carta](assets/2_enterdata.png) ![2_1_enterdata](assets/2_1_enterdata.png)

### Gestionar contenido {#managecontent}

En la pestaña contenido, administre el contenido, como los fragmentos del documento y las variables de contenido, de la carta.

1. Seleccione **Content**. Gestión de correspondencia muestra la pestaña de contenido de la carta.

   ![Pestaña Contenido: módulo de resaltado en contenido](assets/3_content.png)

1. Edite los módulos de contenido, según sea necesario, en la pestaña Content . Para centrar la atención en el módulo de contenido relevante en la jerarquía de contenido, puede tocar la línea o el párrafo correspondiente en la vista previa de la carta o pulsar el módulo de contenido directamente en la jerarquía de contenido.

   Por ejemplo, la línea &quot;Hemos revisado...&quot; está seleccionada en el gráfico siguiente y el módulo de contenido correspondiente está seleccionado en la pestaña Content .

   ![4_highlight_moduleincontent](assets/4_highlightmoduleincontent.png)

   En la ficha Contenido o Datos, al pulsar Resaltar los módulos seleccionados ( ![resaltselectedmoduesincontentcr](assets/highlightselectedmodulesincontentccr.png)) en la parte superior izquierda de la vista previa de la carta HTML, puede desactivar o habilitar la funcionalidad para ir al módulo de contenido/datos cuando el texto, párrafo o campo de datos relevantes está seleccionado en la vista previa de la carta.

   Para obtener más información sobre las acciones disponibles para varios módulos en la interfaz de usuario Crear correspondencia, consulte [Acciones e información disponible en la interfaz de usuario Crear correspondencia](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. Para localizar módulos de contenido, utilice el campo Find . Introduzca el nombre completo o parcial o el título del módulo de contenido para buscarlo en la correspondencia.
1. Pulse el icono Mostrar ( ![display](assets/display.png)) delante de una lista, texto, condición o área de destino para mostrarlo u ocultarlo en la carta.
1. Para editar un módulo de texto en línea o editable, pulse el icono **Editar** correspondiente ( ![edittextmodule](assets/edittextmodule.png)) o haga doble clic en el módulo de texto correspondiente en la vista previa de la carta.

   El sistema muestra un editor de texto para editar y dar formato al texto.

   El corrector ortográfico predeterminado del navegador comprueba la ortografía en el editor de texto. Para administrar la revisión ortográfica y gramatical, puede editar la configuración del corrector ortográfico del navegador o instalar complementos del navegador para revisar la ortografía y la gramática.

   También puede utilizar los distintos métodos abreviados del teclado en el editor de texto para administrar, editar y dar formato al texto. Para obtener más información sobre los [métodos abreviados del teclado del Editor de texto](/help/forms/using/keyboard-shortcuts.md#correspondence-management) en Atajos de teclado de la Gestión de correspondencia.

   ![5_edittextmodule](assets/5_edittextmodule.png)

   Es posible que desee reutilizar uno de los párrafos de texto que existen en otra aplicación del documento. Puede copiar y pegar texto directamente, como desde MS Word, páginas HTML o cualquier otra aplicación.

   Puede copiar y pegar uno o varios párrafos de texto en un módulo de texto editable. Por ejemplo, puede tener un documento de MS Word con una lista con viñetas de pruebas de residencia aceptables como las siguientes:

   ![pastetextmsword](assets/pastetextmsword.png)

   Puede copiar y pegar directamente el texto del documento de MS Word en un módulo de texto editable. El formato, como la lista con viñetas, la fuente y el color del texto, se conserva en el módulo de texto.

   ![pastetexteditabemograma](assets/pastetexteditablemodule.png)

   >[!NOTE]
   >
   >Sin embargo, el formato del texto pegado tiene algunas [limitaciones](https://helpx.adobe.com/aem-forms/kb/cm-copy-paste-text-limitations.html).

   Puede sangrar el texto y los números de la carta utilizando la tecla Tab. Por ejemplo, puede utilizar la tecla de tabulación para alinear varias columnas de texto de una lista con un formato de tabla.

   ![espacios de tabla](assets/tabspaces.png)

   Ejemplo: Uso de la tecla Tab para alinear varias columnas de texto en un formato tabular

   >[!NOTE]
   >
   >Para obtener más información sobre la configuración del espaciado de tabulación para los módulos de texto y las letras, consulte [Más información sobre el uso del espaciado de tabulación para organizar el texto](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).

1. Si es necesario, inserte caracteres especiales en la correspondencia. Por ejemplo, puede utilizar la paleta Caracteres especiales para insertar:

   * Símbolos monetarios como €, Euros y £
   * Símbolos matemáticos como la adminis... ...la adm., la j... ...la adm.
   * Símbolos de puntuación como ‟ y&quot;

   ![caracteres especiales](assets/specialcharacters.png)

   Correspondence Management ha incorporado compatibilidad con 210 caracteres especiales. El administrador puede [añadir compatibilidad para más caracteres especiales personalizados mediante personalización](../../forms/using/custom-special-characters.md).

1. Para resaltar o resaltar partes de texto en un módulo en línea editable, seleccione el texto y pulse Resaltar color.

   ![letterbackground color](assets/letterbackgroundcolor.png)

   Puede tocar directamente un color básico `**[A]**` presente en la paleta Colores básicos o pulsar **Seleccionar** después de utilizar el control deslizante `**[B]**` para elegir el tono apropiado del color.

   De forma opcional, también puede ir a la ficha Avanzado para seleccionar el tono, la luminosidad y la saturación `**[C]**` adecuados para crear el color preciso y, a continuación, pulsar Seleccionar `**[D]**` para aplicar el color y resaltar el texto.

   ![textbackgroundColor](assets/textbackgroundcolor.png)

1. Realice los cambios correspondientes en el contenido y el formato y pulse **Guardar**. Toque ( ![editnextmoduleccr](assets/editnextmoduleccr.png)) para moverse entre módulos de texto editables o pulse **Guardar y siguiente** para guardar los cambios y pasar al siguiente módulo de texto editable.
1. El sistema también muestra las variables sin rellenar para cada una de las ramas. Cuando no hay variables no rellenadas, las variables no rellenadas se muestran como 0. Si hay variables sin rellenar, puede tocar una rama para expandirla y localizar la variable sin rellenar. Utilice la barra de herramientas de contenido para eliminar contenido, aumentar/disminuir la sangría del contenido e insertar saltos de página antes o después del contenido.

   Puede insertar saltos de página por encima y por debajo de los módulos de datos incluso cuando formen parte de listas y condiciones.

1. Pulse Abrir/Cerrar variable de contenido ( ![opencontentvariables](assets/opencontentvariables.png)) para abrir las variables de contenido y rellenarlas correctamente.
1. Una vez que rellene la variable sin rellenar correctamente, el recuento de la variable sin rellenar se establecerá en 0.

   En la interfaz de usuario Crear correspondencia, el recuento de variables sin rellenar se muestra en cada nivel de la jerarquía de cualquier módulo que contenga al menos una variable. Si un módulo contiene variables no rellenadas, el recuento se muestra en los niveles de variable, módulo, área de destino y plantilla de carta.

   El recuento de variables no rellenadas incluye:

   * Solo variables de diccionario de datos y marcador de posición sin proteger. El recuento de variables no incluye variables de diseño o diccionario de datos protegido.
   * Campos obligatorios.
   * Los campos de diseño si son obligatorios y están enlazados al usuario.
   * Solo instancias de variables únicas. Si un módulo, área de destino o plantilla de carta contiene dos o más instancias de la misma variable, el recuento se muestra como 1 (uno). Sin embargo, para cada una de las instancias, el recuento se muestra como 1.

   El recuento de variables no rellenadas no incluye los módulos no seleccionados. Si un módulo se incluye en una plantilla de letras pero no está en la carta, no se muestra el recuento de variables no rellenadas en este módulo.

   Para el área de destino, módulo y variable, el recuento se muestra a la derecha de cada objeto en la plantilla de letras. Sin embargo, para la plantilla completa, el recuento se muestra en la barra de estado Crear correspondencia .

   Los módulos de una plantilla de letras muestran el recuento de variables no rellenadas como se describe a continuación:

   * **** TextoMuestra la suma de las variables únicas de marcador de posición sin rellenar y los elementos de diccionario de datos que contiene el módulo de texto.
   * **** ConditionMuestra la suma de las variables de condición únicas no rellenadas que contiene la condición y las variables contenidas en los módulos resultantes.
   * **** ListaMuestra la suma de todas las variables únicas no rellenadas que contiene los módulos asignados a la lista.
   * **Área de** destinoMuestra la suma de todas las variables únicas no rellenadas que contiene los módulos asignados al área de destino.

   Tenga en cuenta lo siguiente con respecto a las variables con valores predeterminados:

   * Un campo de variable booleana toma el valor predeterminado *false*. Sin embargo, se considera que la variable no está rellenada. Esto implica que el recuento de variables incluye todos los campos de variables booleanas con el valor *false*.

   * Un campo de variable numérica toma el valor predeterminado *0 (cero)*. Sin embargo, se considera que la variable no está rellenada. Esto implica que el recuento de variables incluye todos los campos numéricos de variables con valor *0 (cero)*.



#### Acciones e información disponibles en la ficha Crear contenido de correspondencia {#actions-and-info-available-in-the-create-correspondence-content-tab}

**Área de destino**

* Insertar línea en blanco: Inserta una nueva línea en blanco.
* Insertar texto en línea: Inserta un nuevo módulo de texto.
* Bloqueo de pedido (información): Indica que no se puede cambiar el orden del contenido.
* Valores no rellenados (información): Indica el número de variables sin rellenar en el área de destino.

**Módulo**

* Selección (icono de ojo): Incluye\excluye el módulo de la carta.
* Omitir viñetas (aplicable a los módulos de lista y sus módulos secundarios): Omite las viñetas de un módulo concreto.
* Salto de página antes (aplicable a módulos secundarios de área de destino): Inserta un salto de página antes del módulo.
* Salto de página después de (aplicable a módulos secundarios de área de destino): Inserta un salto de página antes del módulo.
* Valores no rellenados (información): Indica el número de variables sin rellenar en el área de destino.
* Editar (solo módulos de texto): Abra el editor de texto enriquecido para editar el módulo de texto.
* Panel de datos (módulos de texto y condición): Abra todas las variables del módulo.

**Módulo de lista**

* Insertar línea en blanco: Inserta una nueva línea en blanco.
* Biblioteca de contenido: Abre la biblioteca de contenido para agregar módulos a la lista.
* Configuración de lista (solo lista anidada):
* Bloqueo de pedido (información): Indica que no se puede cambiar el orden de los elementos de la lista.

### Administrar archivos adjuntos {#manage-attachments}

1. Seleccione **Attachments**. Gestión de Correspondencia muestra los archivos adjuntos disponibles, tal como se configuran al crear la plantilla de carta.
1. Puede optar por no enviar un archivo adjunto junto con la carta tocando el icono de vista y puede pulsar la cruz del archivo adjunto para eliminarlo de la carta. Para los archivos adjuntos especificados, al crear una plantilla de carta, como Obligatorio, los iconos Ver y Eliminar están desactivados.
1. Pulse el icono de acceso a biblioteca ( ![libraryaccess](assets/libraryaccess.png)) para acceder a la biblioteca de contenido e insertar los recursos DAM como archivos adjuntos.

   >[!NOTE]
   >
   >El icono Acceso a biblioteca solo está disponible si el acceso a la biblioteca estaba habilitado durante la creación de la carta.

1. Si el orden de los archivos adjuntos no se ha bloqueado al crear la correspondencia, puede reordenar los archivos adjuntos seleccionando un archivo adjunto y pulsando las flechas abajo y arriba.

   Para obtener más información, consulte [Attachment delivery](#attachmentdelivery).

### Administre el contenido en la vista previa y envíe la carta {#manage-content-in-preview-and-submit-the-letter}

Puede realizar cambios en el diseño y el contenido para garantizar que la carta tenga el aspecto que desea y se envíe a los distintos procesos de publicación.

1. Para resaltar todo el contenido editable de la carta, pulse **Resaltar secciones editables**.

   El contenido editable de la carta se resalta con fondo gris.

   ![Resaltar contenido editable](assets/4_highlightmoduleincontent-1.png)

1. Edite los módulos de contenido, según sea necesario, en la pestaña Content . Para centrar la atención en el módulo de contenido relevante en la jerarquía de contenido, puede tocar la línea o el párrafo correspondiente en la vista previa de la carta o pulsar el módulo de contenido directamente en la jerarquía de contenido.

   Por ejemplo, la línea &quot;Para permitirnos acceder...&quot; está seleccionada en el gráfico de abajo y el módulo de contenido correspondiente está seleccionado en la pestaña Content .

   Al pulsar Resaltar los módulos seleccionados en el contenido ( ![resaltselectedmodulesincontentcr](assets/highlightselectedmodulesincontentccr.png)), puede desactivar o habilitar la funcionalidad para resaltar el módulo de contenido en la ficha Contenido cuando se toca el texto, párrafo o campo de datos correspondiente en la vista previa de la carta.

   Para obtener más información sobre las acciones disponibles para varios módulos en la interfaz de usuario Crear correspondencia, consulte [Acciones e información disponible en la interfaz de usuario Crear correspondencia](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. Para añadir un salto de página a la letra, pulse donde desea insertar un salto de página y seleccione Salto de página antes o Salto de página después ( ![pagebreakbeforeafter](assets/pagebreakbeforeafter.png)).

   En la carta se inserta un marcador de posición de salto de página explícito. Para ver cómo un salto de página explícito afecta a la carta, consulte la vista previa del PDF acoplado.

   >[!NOTE]
   >
   >Como los formularios móviles no admiten saltos de página, los encabezados y pies de página aparecen solo una vez. Sin embargo, puede establecer explícitamente encabezados y pies de página en la presentación (por página) para que aparezcan en la vista previa de los formularios móviles. Además, las páginas en blanco de la carta, si las hay, no aparecen en la vista previa de los formularios móviles.

   ![Salto de página explícito](assets/8_pagebreak.png)

1. Para guardar la carta como borrador, para poder seguir trabajando más adelante, pulse Guardar como borrador. Para utilizar esta opción, la carta debe estar [publicada](../../forms/using/publishing-unpublishing-forms.md#publishanasset). Para obtener más información, consulte Instancia de borrador en [Guardar borradores y enviar instancias de carta](#savingdrafts).

   ![saveasborrador](assets/saveasdraft.png)

   El cuadro de diálogo Nombre de la carta borrador aparece con el id de instancia de la letra. Si lo desea, puede editar este ID. Tome nota del ID de la letra y, a continuación, pulse **Listo**. Posteriormente, puede utilizar este ID para [volver a cargar la letra borrador](submit-letter-topostprocess.md#reloaddraft).

1. Para obtener una vista previa de la carta como un PDF plano con el diseño exacto y los saltos de página a medida que se envíen, pulse ( ![vista previa](assets/preview.png)) Vista previa.

   La carta aparece como un PDF aplanado. El PDF plano es la representación exacta de la carta tal como se enviará con las fuentes, los saltos y el diseño correctos de la carta.

   >[!NOTE]
   >
   >Si utiliza Mozilla Firefox y el tipo de representación HTML, para previsualizar la carta como PDF aplanado, asegúrese de utilizar el complemento del explorador nativo y no el complemento de Acrobat. Para seleccionar el complemento nativo del navegador, vaya a la configuración de Mozilla Firefox y, para el tipo de contenido PDF, seleccione Vista previa en Firefox.

1. Si considera que la vista previa del PDF acoplado es satisfactoria, pulse **Enviar** para enviar la carta. O para realizar cambios en la carta, pulse **Salir de la vista previa** para volver a la vista previa Crear correspondencia de la carta para realizar cambios en ella. Al pulsar Enviar, si la configuración Administrar instancia de carta está habilitada en la instancia Publicar, se genera la instancia de envío de carta.

   Para obtener más información, consulte Instancia de borrador en Guardar borradores y enviar instancias de carta.

   También puede guardar la carta como borrador para realizar cambios en la carta más adelante.

   Después de realizar los cambios necesarios, puede enviar la carta desde la vista previa HTML5 o pulsar de nuevo Vista previa para revisar el resultado PDF acoplado.

   Para obtener información sobre las diferencias entre los formularios HTML5 y los PDF forms, consulte [Distinción de funciones entre los formularios HTML5 y los PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

## Guardar borradores y enviar instancias de carta {#savingdrafts}

Cuando se representa una carta en la interfaz de usuario Crear correspondencia , puede guardarla como si se estuviera viendo.

Existen dos tipos de instancias de letras que se pueden guardar: Borrador de instancia y Enviar instancia.

* **Instancia** de borrador: La instancia de borrador captura el estado actual de la letra que está previsualizando. Para guardar una instancia de borrador, primero asegúrese de que la carta y todos los recursos a los que hace referencia la carta están en estado Publicado . Para obtener información sobre la publicación de una carta, consulte [Publicar un recurso](../../forms/using/publishing-unpublishing-forms.md#publishanasset). Debe publicar una carta antes de guardarla como borrador, ya que cuando publica una carta, crea una versión de la carta, sus recursos dependientes y los datos en ese momento. Usted u otro usuario no pueden editar la versión publicada de una carta y se puede restaurar más tarde sin discrepancias inesperadas de la versión publicada. Puede volver a esta instancia más tarde y continuar desde donde se marchó.

* **Instancia** de envío: Las instancias de envío capturan el estado de la carta a medida que se envía. La instancia de envío almacena el estado PDF de la instancia de carta después de que se haya procesado junto con los datos introducidos por el usuario en la interfaz de usuario Crear correspondencia .

Estas instancias solo se pueden guardar cuando la carta se está viendo en la instancia de publicación. De forma predeterminada, el guardado en instancias está desactivado. Para habilitar el guardado de instancias de letras, realice los siguientes pasos.

1. En AEM, abra Configuración de la consola web de Adobe Experience Manager para su servidor mediante la siguiente URL: https://&lt;server>:&lt;port>/&lt;contextpath>/system/console/configMgr
1. Busque **[!UICONTROL Correspondence Management Configurations]** y haga clic en él.
1. Compruebe **[!UICONTROL Administrar instancias de carta en la configuración de publicación]** y haga clic en **[!UICONTROL Guardar]**.

Cuando se activa el guardado de instancias de carta, tiene la opción de seleccionar dónde guardar las instancias de carta. Existen dos opciones para guardar las instancias de carta: Guarde local o Guarde remoto.

### Almacenamiento local {#local-save}

Las instancias de letras se guardan en la instancia de publicación y se replican de forma inversa en la instancia de autor.

### Almacenamiento remoto {#remote-save}

Esta opción existe para las personas que tienen dudas sobre el guardado de datos de usuario en instancias de publicación, que en general están fuera del cortafuegos corporativo. Cuando se activa la opción de guardar de forma remota, las instancias de letras no se guardan en la instancia de publicación, pero se guardan de forma remota en el autor de procesamiento especificado mediante las configuraciones del SDK de cliente de LiveCycle.

#### Habilitar almacenamiento remoto {#enable-remote-save}

1. En AEM, abra Configuración de la consola web de Adobe Experience Manager para su servidor mediante la siguiente URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`
1. Busque **[!UICONTROL Correspondence Management Configurations]** y haga clic en él.
1. Busque la configuración **[!UICONTROL Remote Save]**, verifique y haga clic en **[!UICONTROL Save]**.

#### Especificar la configuración del autor de procesamiento {#specify-processing-author-settings}

1. En AEM, abra Configuración de la consola web de Adobe Experience Manager para su servidor mediante la siguiente URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Configuración de la consola web de Adobe Experience Manager](assets/2configmanager.png)

1. En esta página, busque Configuración del SDK de cliente de LiveCycle de Adobe y expanda esta opción haciendo clic en ella.

1. En la URL del servidor de procesamiento, introduzca el nombre del servidor de LiveCycle, proporcione la información de inicio de sesión y haga clic en **Guardar**.

   ![Introduzca el nombre y la información de inicio de sesión de su servidor de LiveCycle](assets/3configmanager.png)

1. Si es necesario, establezca el nombre de usuario y la contraseña con los que desea acceder al servidor.

#### Entrega de archivos adjuntos {#attachmentdelivery}

* Los archivos adjuntos están disponibles después del proceso en el PDF, que se crea después del envío del mensaje.
* Cuando la carta se procesa con API del lado del servidor como PDF interactivo o no interactivo, el PDF procesado contiene archivos adjuntos como archivos adjuntos PDF.
* Cuando se carga un proceso de publicación asociado a una plantilla de carta como parte de las operaciones Enviar o Completar correspondencia utilizando la interfaz de usuario Crear correspondencia, los archivos adjuntos se pasan como List&lt;com.adobe.idp.Document> en el parámetro AttachmentDocs .
* Los mecanismos de envío listos para usar, como correo electrónico e Imprimir, también entregan archivos adjuntos junto con el PDF de la correspondencia generada.

## Modos de representación de la vista previa de letras: Vista previa de formularios móviles y vista previa de PDF {#rendition-modes-of-letter-preview-mobile-forms-preview-and-pdf-preview}

AEM Forms Correspondence Management muestra una carta como HTML en la interfaz de usuario Crear correspondencia . Sin embargo, Gestión de correspondencia sigue admitiendo la reversión a la vista previa de PDF en lugar de a la vista previa HTML. Para obtener más información sobre cómo cambiar entre el modo de vista previa HTML y PDF, consulte [Cambiar el modo de representación de la letra](#changerenditionmode).

A continuación se muestran las ventajas y la funcionalidad disponibles en la vista previa de HTML y PDF.

**Ventajas de los formularios móviles/vista previa HTML**

* **Pulse un valor de campo de datos para resaltar el campo** de datos correspondiente: En la interfaz de usuario Crear correspondencia, puede pulsar un valor de campo de datos en la letra para resaltar el campo de datos correspondiente en la pestaña Datos . Para obtener más información, consulte [Introducir datos](#enterdata).

* **Compatibilidad con** navegadores: Los navegadores retiran la compatibilidad con NPAPI gradualmente, lo que afecta a la vista previa PDF de la carta. La vista previa de la carta en los formularios HTML/móviles no se ve afectada por esto.
* **Resalte el contenido editable en una carta**: En la interfaz de usuario Crear correspondencia , puede pulsar Resaltar contenido editable para resaltar todo el contenido editable de la carta en gris. Para obtener más información, consulte [Administrar contenido](#managecontent).

`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`
`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`  **Ventajas de la vista previa de PDF**

* **Salto** de página: En la vista previa del PDF, puede ver exactamente cómo los saltos de página de la carta afectan a su salida.
* **Vista previa** final: En la vista previa del PDF, puede ver el formato y el aspecto exactos de la carta, tal como aparecerá en su salida.

Para obtener información sobre la compatibilidad con secuencias de comandos en PDF forms, consulte [Compatibilidad con secuencias de comandos](https://help.adobe.com/en_US/livecycle/11.0/ScriptingSupport/index.html).

Para obtener más información sobre la compatibilidad con secuencias de comandos en formularios HTML5, consulte [Compatibilidad con secuencias de comandos para formularios HTML5](/help/forms/using/scripting-support.md).

### Cambiar el modo de representación de la letra {#changerenditionmode}

De forma predeterminada, la interfaz de usuario Crear correspondencia utiliza los formularios HTML o móviles para obtener la vista previa de la carta. La vista previa de formularios móviles no presenta problemas de representación en ningún explorador, ya que utiliza el complemento nativo del explorador y no requiere complementos adicionales. Puede cambiar el modo de vista previa de la carta a PDF. Sin embargo, las restricciones del navegador pueden crear problemas para diferentes funciones de la vista previa PDF interactiva de la carta.

Para obtener más información sobre la compatibilidad del explorador con la vista previa de la carta, consulte [Interrupción de los complementos del explorador NPAPI y su impacto](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html).

Para cambiar el modo de vista previa de la carta, complete los siguientes pasos:

1. Vaya a `https://[system]:'port'/system/console/configMgr` y, si es necesario, inicie sesión como administrador.
1. Vaya a **[!UICONTROL Correspondence Management Configurations]** > **[!UICONTROL Rendition Type]** y seleccione **HTML Rendition** (Default) o **PDF Rendition**.
1. Haga clic en **[!UICONTROL Guardar]**.

