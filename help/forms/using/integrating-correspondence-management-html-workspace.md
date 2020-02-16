---
title: Integración de aplicaciones de terceros en el espacio de trabajo de AEM Forms
seo-title: Integración de aplicaciones de terceros en el espacio de trabajo de AEM Forms
description: Integre aplicaciones de terceros, como la gestión de correspondencia, en el espacio de trabajo de AEM Forms.
seo-description: Integración de aplicaciones de terceros como la gestión de correspondencia en el espacio de trabajo de AEM Forms.
uuid: 7654cf86-b896-4db2-8f5d-6c1b2e6c229f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f70f21e3-3bec-490d-889e-faf496fb738b
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Integración de aplicaciones de terceros en el espacio de trabajo de AEM Forms{#integrating-third-party-applications-in-aem-forms-workspace}

El espacio de trabajo de AEM Forms admite la administración de actividades de asignación y finalización de tareas para formularios y documentos. Estos formularios y documentos pueden ser formularios XDP, Flex® o guías (obsoletos) que se han procesado en formatos XDP, PDF, HTML o Flex.

Estas capacidades se mejoran aún más. AEM Forms ahora admite la colaboración con aplicaciones de terceros que admiten funciones similares al espacio de trabajo de AEM Forms. Una parte común de esta funcionalidad es el flujo de trabajo de asignación y la posterior aprobación de una tarea. AEM Forms proporciona una única experiencia unificada para los usuarios empresariales de AEM Forms, de modo que todas las asignaciones de tareas o aprobaciones de este tipo para las aplicaciones admitidas se pueden gestionar a través del espacio de trabajo de AEM Forms.

Por ejemplo, consideremos la gestión de correspondencia como el candidato de muestra para la integración con el espacio de trabajo de AEM Forms. Correspondence Management tiene el concepto de una &#39;Carta&#39;, que puede procesarse y permite realizar acciones.

## Crear recursos de Correspondencia {#create-correspondence-management-assets}

Comience creando una plantilla de gestión de correspondencia de ejemplo que se procesa en el espacio de trabajo de AEM Forms. Para obtener más información, consulte [Creación de una plantilla](../../forms/using/create-letter.md)de carta.

Acceda a la plantilla Gestión de correspondencia en su dirección URL para comprobar si la plantilla Gestión de correspondencia se puede procesar correctamente. La dirección URL tiene un patrón similar al `https://[server]:[port]/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;`

donde `encodedLetterId` es el Id. de letra con codificación URL. Especifique el mismo ID de letra al definir el proceso de procesamiento para la tarea de espacio de trabajo en Workbench.

## Crear una tarea para procesar y enviar una carta en AEM Workspace {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}

Antes de ejecutar estos pasos, asegúrese de que es miembro de los siguientes grupos:

* cm-agent-users
* Usuarios de Workspace

Para obtener más información, consulte [Agregar y configurar usuarios](/help/forms/using/admin-help/adding-configuring-users.md).

Siga los pasos siguientes para crear una tarea para procesar y enviar una carta en AEM Workspace:

1. Inicie Workbench. Inicie sesión en localhost como administrador.
1. Haga clic en Archivo > Nuevo > Aplicación. En el campo Nombre de la aplicación, introduzca `CMDemoSample` y haga clic en Finalizar.
1. Seleccione `CMDemoSample/1.0` y haga clic con el botón derecho `NewProcess`. En el campo de nombre, introduzca `CMRenderer` y haga clic en Finalizar.
1. Arrastre el selector de actividades del punto de inicio y configúrelo:

   1. En Datos de presentación, seleccione Utilizar un recurso CRX.

      ![useacrxasset](assets/useacrxasset.png)

   1. Busque un recurso. En el cuadro de diálogo Seleccionar recurso de formulario, la ficha Letras muestra todas las letras del servidor.

      ![Ficha Carta](assets/letter_tab_new.png)

   1. Seleccione la letra adecuada y haga clic en **Aceptar**.

1. Haga clic en Administrar perfiles de acción. Aparecerá el cuadro de diálogo Administrar perfil de acción. Asegúrese de que el proceso de procesamiento y el proceso de envío están correctamente seleccionados.
1. Para abrir la carta con un archivo XML de datos, busque y seleccione el archivo de datos adecuado en el proceso de preparación de datos.
1. Haga clic en Aceptar.
1. Defina las variables para Salida de punto de inicio y Datos adjuntos de tarea. Las variables definidas contendrán los datos Salida de punto de inicio y Datos adjuntos de tarea.
1. (Opcional) Para agregar otro usuario al flujo de trabajo, arrastre un selector de actividades, configúrelo y asígnelo a un usuario. Escriba un contenedor personalizado (ejemplo de abajo) o descargue e instale el DSC (que se muestra más abajo) para extraer la plantilla Carta, la salida del punto de inicio y el adjunto de la tarea.

   A continuación se muestra un contenedor personalizado de muestra:

   ```java
   public LetterInstanceInfo getLetterInstanceInfo(Document dataXML) throws Exception {
   try {
   if(dataXML == null)
   throw new Exception("dataXML is missing");
   
   CoreService coreService = getRemoteCoreService();
   if (coreService == null)
   throw new Exception("Unable to retrive service. Please verify connection details.");
   Map<String, Object> result = coreService.getLetterInstanceInfo(IOUtils.toString(dataXML.getInputStream(), "UTF-8"));
   LetterInstanceInfo letterInstanceInfo = new LetterInstanceInfo();
   
   List<Document> attachmentDocs = new ArrayList<Document>();
   List<byte[]> attachments = (List<byte[]>)result.get(CoreService.ATTACHMENT_KEY);
   if (attachments != null){
   for (byte[] attachment : attachments)
   { attachmentDocs.add(new Document(attachment)); }
   
   }
   letterInstanceInfo.setLetterAttachments(attachmentDocs);
   
   byte[] updateLayout = (byte[])result.get(CoreService.LAYOUT_TEMPLATE_KEY);
   if (updateLayout != null)
   { letterInstanceInfo.setLetterTemplate(new Document(updateLayout)); }
   
   else
   { throw new Exception("template bytes missing while getting Letter instance Info."); }
   
   return letterInstanceInfo;
   } catch (Exception e)
   { throw new Exception(e); }
   
   }
   ```

   [DSC de descarga de archivos](assets/dscsample.zip): Hay disponible un DSC de muestra en el archivo DSCSample.zip adjunto anteriormente. Descargue y descomprima el archivo DSCSample.zip. Antes de utilizar el servicio DSC, debe configurarlo. Para obtener más información, consulte [Configuración del servicio](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p)DSC.

   En el cuadro de diálogo Definir actividad, seleccione la actividad adecuada, como getLetterInstanceInfo, y haga clic en **Aceptar**.

1. Implemente la aplicación. Si se le solicita que registre y guarde los recursos.
1. Inicie sesión en el espacio de trabajo de formularios de AEM en https://[server]:[port]/lc/content/ws.
1. Abra la tarea que ha agregado, CMRenderer. Aparece la carta de Correspondencia de Administración.

   ![cminárea de trabajo](assets/cminworkspace.png)

1. Rellene los datos requeridos y envíe la carta. La ventana se cierra. En este proceso, la tarea se asigna al usuario especificado en el flujo de trabajo en el paso 9.

   >[!NOTE]
   >
   >El botón Enviar no se activa hasta que se completen todas las variables requeridas en la carta.

[Comuníquese con la asistencia técnica](https://www.adobe.com/account/sign-in.supportportal.html)
