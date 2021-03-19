---
title: Procesamiento posterior de cartas y comunicaciones interactivas
seo-title: Procesamiento posterior de letras
description: El posprocesamiento de cartas en la gestión de correspondencia le permite crear procesos de anuncios de AEM y Forms, como imprimir y enviar por correo electrónico, e integrarlos en sus cartas.
seo-description: El posprocesamiento de cartas en la gestión de correspondencia le permite crear procesos de anuncios de AEM y Forms, como imprimir y enviar por correo electrónico, e integrarlos en sus cartas.
uuid: 40cb349d-6ba2-4794-9ec6-dcab15c35b8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9b06c394-8e26-429c-b78f-22afa271aeb3
docset: aem65
feature: Administración de correspondencia
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---


# Procesamiento posterior de cartas y comunicaciones interactivas{#post-processing-of-letters-and-interactive-communications}

## Procesamiento posterior {#post-processing}

Los agentes pueden asociar y ejecutar flujos de trabajo posteriores al procesamiento en cartas y comunicaciones interactivas. El proceso posterior que se va a ejecutar se puede seleccionar en la vista Propiedades de la plantilla Carta . Puede configurar los procesos de publicación para enviar por correo electrónico, imprimir, fax o archivar las cartas finales.

![Procesamiento posterior](assets/ppoverview.png)

Para asociar procesos de publicación con cartas o comunicaciones interactivas, primero debe configurar los procesos de publicación. Se pueden ejecutar dos tipos de flujos de trabajo en las cartas enviadas:

1. **Forms Workflow:** Estos son los flujos de trabajo de administración de procesos JEE de AEM Forms. Instrucciones para configurar [Forms Workflow](#formsworkflow).

1. **AEM flujo de trabajo:** AEM los flujos de trabajo también se pueden utilizar como procesos posteriores para las cartas enviadas. Instrucciones para configurar [AEM Workflow](../../forms/using/aem-forms-workflow.md).

## Flujo de trabajo de formularios {#formsworkflow}

1. En AEM, abra Configuración de la consola web de Adobe Experience Manager para su servidor mediante la siguiente URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Administrador de configuración](assets/2configmanager-1.png)

1. En esta página, busque Configuración del SDK de cliente de AEM Forms y expanda la aplicación haciendo clic en ella.
1. En URL de servidor, introduzca el nombre de su AEM Forms en el servidor JEE, detalles de inicio de sesión y, a continuación, haga clic en **Guardar**.

   ![Introduzca el nombre del servidor de LiveCycle](assets/1cofigmanager.png)

1. Especifique el nombre de usuario y la contraseña.
1. Asegúrese de que sun.util.calendar se agrega a la Configuración de Deserialization Firewall.

   Vaya a Deserialization Firewall Configuration y en clases Incluidas en la lista de permitidos de prefijos de paquete, agregue sun.util.calendar.

1. Ahora, los servidores están asignados y los procesos de publicación en AEM Forms en JEE están disponibles en la interfaz de usuario de AEM al crear cartas.

   ![Crear pantalla de carta con procesos de publicación enumerados](assets/0configmanager.png)

1. Para autenticar un proceso/servicio, copie el nombre de un proceso y vuelva a la página Configuraciones de la consola web de Adobe Experience Manager > Configuración del SDK del cliente de AEM Forms y agregue el proceso como un nuevo servicio.

   Por ejemplo, si la lista desplegable de la página de letras Propiedades muestra el nombre del proceso como Forms Workflow -> ValidCCPostProcess/SaveXML, añada un Nombre de servicio como `ValidCCPostProcess/SaveXML`.

1. Para utilizar AEM Forms en flujos de trabajo JEE para el posprocesamiento, configure los parámetros y resultados necesarios. A continuación se indican los valores predeterminados de los parámetros.

   Vaya a la página Configuraciones de la Consola Web de Adobe Experience Manager > **[!UICONTROL Configuraciones de Gestión de Correspondencia]** y configure los siguientes parámetros:

   1. **inPDFDoc (parámetro de documento PDF):** documento PDF como entrada. Esta entrada contiene la letra procesada como entrada. Los nombres de parámetro indicados son configurables. Se pueden configurar desde las configuraciones de Gestión de Correspondencia desde la configuración.
   1. **inXMLDoc (parámetro de datos XML):** Un documento XML como entrada. Esta entrada contiene datos introducidos por el usuario en forma de XML.
   1. **inXDPDoc (parámetro de documento XDP):**  un documento XML como entrada. Esta entrada contiene el diseño subyacente (XDP).
   1. **inAttachmentDocs (parámetro Attachment Documents ):** parámetro de entrada de lista. Esta entrada contiene todos los archivos adjuntos como entrada.
   1. **redirectURL (Salida de URL de redireccionamiento):** un tipo de salida que indica la dirección URL a la que se redirige.

   El flujo de trabajo de los formularios debe tener un parámetro de documento PDF o un parámetro de datos XML como entrada con el mismo nombre que se especifica en **[!UICONTROL Configuraciones de gestión de correspondencia]**. Esto es necesario para que el proceso aparezca en la lista desplegable Post Process .

## Configuración de la instancia de publicación {#settings-on-the-publish-instance}

1. inicie sesión en `https://localhost:publishport/aem/forms`.
1. Vaya a **[!UICONTROL Letters]** para ver la carta publicada que está disponible en la instancia de publicación.
1. Configure la Configuración de AEM DS. Consulte [Configuración de AEM DS](../../forms/using/configuring-the-processing-server-url-.md).

>[!NOTE]
>
>Al utilizar Forms o AEM flujos de trabajo, antes de realizar cualquier envío desde el servidor de publicación, es necesario configurar el servicio de configuración de DS. De lo contrario, el envío del formulario fallará.

## Recuperación de instancias de carta {#letter-instances-retrieval}

Las instancias de carta guardadas se pueden manipular aún más, como la recuperación de instancias de carta y la eliminación de instancias de carta, mediante las siguientes API definidas en LetterInstanceService.

<table>
 <tbody>
  <tr>
   <td><strong>API del lado del servidor</strong></td>
   <td><strong>Nombre de la operación</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><p>Letra públicaInstanceVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>Tira ICCException; </p> </td>
   <td>getLetterInstance</td>
   <td>Buscar la instancia de letra especificada </td>
  </tr>
  <tr>
   <td>El void public deleteLetterInstance(String letterInstanceId) lanza ICCException; </td>
   <td>deleteLetterInstance </td>
   <td>Se eliminó la instancia de letra especificada </td>
  </tr>
  <tr>
   <td>List getAllLetterInstances(Query) lanza ICCException; </td>
   <td>getAllLetterInstances </td>
   <td>Esta API recupera instancias de letras en función del parámetro de consulta de entrada. Para recuperar todas las instancias de letras, el parámetro de consulta se puede pasar como nulo.<br /> </td>
  </tr>
  <tr>
   <td>Public Boolean letterInstanceExists(String letterInstanceName) lanza ICCException; </td>
   <td>letterInstanceExists </td>
   <td>Comprobar si existe una LetterInstance con el nombre dado </td>
  </tr>
 </tbody>
</table>

## Asociación de un proceso posterior a una carta {#associating-a-post-process-with-a-letter}

En la interfaz de usuario de CCR, complete los siguientes pasos para asociar un proceso de publicación con una carta:

1. Pase el ratón sobre una letra y pulse **Ver propiedades**.
1. Seleccione **Editar**.
1. En la lista desplegable Propiedades básicas, seleccione el proceso de anuncio que desea asociar a la carta mediante la lista desplegable Proceso de anuncio . En la lista desplegable se enumeran los procesos de publicación relacionados con AEM y Forms.
1. Toque **Guardar**.
1. Después de configurar la carta con el proceso de publicación, publique la carta y, opcionalmente, en la instancia de publicación, especifique la URL de procesamiento en AEM servicio Configuración de DS. Esto garantiza que el proceso posterior se ejecute en la instancia de procesamiento.

## Volver a cargar una instancia de borrador de carta  {#reloaddraft}

Se puede volver a cargar una instancia de letra borrador en la interfaz de usuario mediante la siguiente URL:

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstaceID: ID exclusivo de la instancia de carta enviada.

Para obtener más información sobre cómo guardar un borrador de carta, consulte [Guardar borradores y enviar instancias de carta](../../forms/using/create-correspondence.md#savingdrafts).
