---
title: Postprocesamiento de cartas y comunicaciones interactivas
seo-title: Postprocesamiento de cartas
description: El posprocesamiento de cartas en la administración de correspondencia le permite crear procesos de anuncios de AEM y Forms, como imprimir y enviar por correo electrónico, e integrarlos con sus cartas.
seo-description: El posprocesamiento de cartas en la administración de correspondencia le permite crear procesos de anuncios de AEM y Forms, como imprimir y enviar por correo electrónico, e integrarlos con sus cartas.
uuid: 40cb349d-6ba2-4794-9ec6-dcab15c35b8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9b06c394-8e26-429c-b78f-22afa271aeb3
docset: aem65
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 0%

---


# Postprocesamiento de cartas y comunicaciones interactivas{#post-processing-of-letters-and-interactive-communications}

## Postprocesamiento {#post-processing}

Los agentes pueden asociar y ejecutar flujos de trabajo de postprocesamiento en cartas y comunicaciones interactivas. El proceso posterior que se va a ejecutar se puede seleccionar en la vista Propiedades de la plantilla Carta. Puede configurar los procesos de publicación para enviar por correo electrónico, imprimir, enviar por fax o archivar sus cartas finales.

![Post-procesamiento](assets/ppoverview.png)

Para asociar procesos de publicación con cartas o comunicaciones interactivas, primero debe configurar los procesos de publicación. Se pueden ejecutar dos tipos de flujos de trabajo en las cartas enviadas:

1. **Forms Workflow:** Estos son los flujos de trabajo de administración de procesos de AEM Forms en JEE. Instrucciones para configurar [Forms Workflow](#formsworkflow).

1. **Flujo de trabajo de AEM:** AEM flujos de trabajo también se pueden usar como procesos posteriores para las cartas enviadas. Instrucciones para configurar [AEM Workflow](../../forms/using/aem-forms-workflow.md).

## Flujo de trabajo de formularios {#formsworkflow}

1. En AEM, abra la configuración de la consola web de Adobe Experience Manager para su servidor mediante la siguiente URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Administrador de configuración](assets/2configmanager-1.png)

1. En esta página, localice la configuración del SDK del cliente de AEM Forms y amplíela haciendo clic en ella.
1. En la URL del servidor, introduzca el nombre de su AEM Forms en el servidor JEE, los detalles de inicio de sesión y, a continuación, haga clic en **Guardar**.

   ![Escriba el nombre del servidor de LiveCycle](assets/1cofigmanager.png)

1. Especifique el nombre de usuario y la contraseña.
1. Asegúrese de que sun.util.calendar se agrega a la Configuración de Deserialization Firewall.

   Vaya a Deserialization Firewall Configuration (Configuración del cortafuegos de deserialización) y, en clases Incluidas en la lista de permitidos de prefijos de paquete, agregue sun.util.calendar.

1. Ahora los servidores están asignados y los procesos de publicación en AEM Forms en JEE están disponibles en la interfaz de usuario de AEM al crear letras.

   ![Crear pantalla de carta con los procesos de publicación enumerados](assets/0configmanager.png)

1. Para autenticar un proceso/servicio, copie el nombre de un proceso y vuelva a la página Configuraciones de la consola web de Adobe Experience Manager > Configuración del SDK del cliente de AEM Forms y agregue el proceso como un nuevo servicio.

   Por ejemplo, si el menú desplegable de la página Propiedades de la letra muestra el nombre del proceso como Forms Workflow -> VálidoCCPostProcess/SaveXML, agregue un nombre de servicio como `ValidCCPostProcess/SaveXML`.

1. Para utilizar AEM Forms en flujos de trabajo JEE para el posprocesamiento, configure los parámetros y salidas necesarios. A continuación se indican los valores predeterminados de los parámetros.

   Vaya a la página Configuraciones de la Consola Web de Adobe Experience Manager > **[!UICONTROL Configuraciones de Administración de Correspondencia]** y configure los siguientes parámetros:

   1. **inPDFDoc (parámetro de documento PDF):** Un documento PDF como entrada. Esta entrada contiene la letra procesada como entrada. Los nombres de parámetro indicados son configurables. Se pueden configurar desde las configuraciones de Correspondence Management desde la configuración.
   1. **inXMLDoc (parámetro de datos XML):** Un documento XML como entrada. Esta entrada contiene datos introducidos por el usuario en forma de XML.
   1. **inXDPDoc (parámetro de documento XDP):** Un documento XML como entrada. Esta entrada contiene el diseño subyacente (XDP).
   1. **inAttachmentDocs (parámetro de Documentos de datos adjuntos):** parámetro de entrada de lista. Esta entrada contiene todos los datos adjuntos como entrada.
   1. **redirectURL (Salida de URL de redireccionamiento):** un tipo de salida que indica la dirección URL a la que se redirige.

   El flujo de trabajo de los formularios debe tener parámetros de documento PDF o de datos XML como entrada con el mismo nombre que se especifica en **[!UICONTROL Configuraciones de administración de correspondencia]**. Esto es necesario para que el proceso aparezca en la lista desplegable Post Process.

## Configuración de la instancia de publicación {#settings-on-the-publish-instance}

1. inicie sesión en `https://localhost:publishport/aem/forms`.
1. Vaya a **[!UICONTROL Letras]** para vista de la carta publicada que está disponible en la instancia de publicación.
1. Configure las opciones de AEM DS. Consulte [Configuración de AEM DS](../../forms/using/configuring-the-processing-server-url-.md).

>[!NOTE]
>
>Al utilizar flujos de trabajo de Forms o AEM, antes de realizar un envío desde el servidor de publicación, es necesario configurar el servicio de configuración de DS. De lo contrario, fallará el envío del formulario.

## Recuperación de instancias de carta {#letter-instances-retrieval}

Las instancias de letras guardadas se pueden manipular aún más, como la recuperación de instancias de letras y la eliminación de instancias de letras, mediante las siguientes API definidas en LetterInstanceService.

<table>
 <tbody>
  <tr>
   <td><strong>API del lado del servidor</strong></td>
   <td><strong>Nombre de la operación</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><p>Public LetterInstanceVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>Expulsa ICCException; </p> </td>
   <td>getLetterInstance</td>
   <td>Buscar la instancia de letra especificada </td>
  </tr>
  <tr>
   <td>Public void deleteLetterInstance(String letterInstanceId) emite ICCException; </td>
   <td>deleteLetterInstance </td>
   <td>Se eliminó la instancia de letra especificada </td>
  </tr>
  <tr>
   <td>Lista getAllLetterInstances(Consulta) genera ICCException; </td>
   <td>getAllLetterInstances </td>
   <td>Esta API obtiene instancias de letras basadas en el parámetro de consulta de entrada. Para recuperar todas las instancias de letras, el parámetro de consulta se puede pasar como nulo.<br /> </td>
  </tr>
  <tr>
   <td>Public Boolean letterInstanceExists(String letterInstanceName) genera ICCException; </td>
   <td>letterInstanceExists </td>
   <td>Comprobar si existe una instancia de carta con el nombre dado </td>
  </tr>
 </tbody>
</table>

## Asociación de un proceso de publicación con una carta {#associating-a-post-process-with-a-letter}

En la interfaz de usuario de CCR, complete los siguientes pasos para asociar un proceso de publicación con una carta:

1. Pase el ratón sobre una letra y toque **Propiedades de la Vista**.
1. Seleccione **Editar**.
1. En la lista desplegable Propiedades básicas, seleccione el proceso de publicación que desea asociar con la letra. En la lista desplegable se muestran tanto los procesos de publicación relacionados con AEM como los relacionados con Forms.
1. Toque **Guardar**.
1. Después de configurar la carta con el proceso de publicación, publique la carta y, opcionalmente, en la instancia de publicación, especifique la URL de procesamiento en el servicio Configuración de AEM DS. Esto garantiza que el proceso posterior se ejecute en la instancia de procesamiento.

## Volver a cargar una instancia de borrador de carta  {#reloaddraft}

Se puede volver a cargar una instancia de borrador en la interfaz de usuario mediante la siguiente URL:

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstaceID: ID única de la instancia de carta enviada.

Para obtener más información sobre cómo guardar un borrador de carta, consulte [Guardado de borradores y envío de instancias de carta](../../forms/using/create-correspondence.md#savingdrafts).
