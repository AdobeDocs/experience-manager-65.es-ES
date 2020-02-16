---
title: Control del acceso a documentos protegidos por políticas
seo-title: Control del acceso a documentos protegidos por políticas
description: Vea cómo puede ver, administrar y controlar el acceso a los documentos protegidos por políticas.
seo-description: Vea cómo puede ver, administrar y controlar el acceso a los documentos protegidos por políticas.
uuid: 2d9f95e9-e4ee-47e2-988e-a191d1d1d264
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f34058c3-384a-4b73-a386-5bc9125acbf8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Control del acceso a documentos protegidos por políticas {#controlling-access-to-policy-protected-documents}

Puede controlar la forma en que los destinatarios utilizan los documentos protegidos por políticas, independientemente de la amplitud de su distribución.

Con la página Documentos puede realizar las siguientes tareas:

* Busque y vea los detalles de los documentos protegidos por políticas. Puede ver información sobre el nombre del documento, el nombre del editor, el nombre de la política y la fecha en que se aplicó la política. Si se elimina la directiva que protegía un documento, también puede ver el ID de directiva eliminado en el nombre de la directiva. Los usuarios pueden ver y administrar sus propios documentos protegidos por políticas. Los administradores pueden ver y administrar todos los documentos protegidos por políticas.
* Cambie los detalles de la política aplicada a un documento. Los usuarios pueden editar sus propias políticas, los administradores pueden editar las políticas compartidas y personales, y los coordinadores de conjuntos de políticas pueden editar las políticas compartidas en los conjuntos de políticas para los que tienen permisos. Puede acceder a la directiva asociada a un documento directamente desde la página Detalles del documento.
* Revocar y restablecer el acceso a un documento protegido por una política. Los administradores pueden revocar y restablecer el acceso a cualquier documento. Los coordinadores de conjuntos de políticas (que tienen permiso para administrar documentos) pueden revocar y restablecer el acceso a los documentos protegidos por políticas que utilizan políticas compartidas desde sus conjuntos de políticas. Los usuarios pueden anular el acceso a sus documentos protegidos por políticas si han creado la política que protege el documento o si la política es compartida y permite esta capacidad.
* Cambie la directiva que se aplica a un documento. Los usuarios que aplican políticas a los documentos pueden cambiar una política si la han creado o si se trata de una política compartida que habilita esta capacidad. Los coordinadores de conjuntos de políticas pueden cambiar las políticas de sus conjuntos de políticas. Los administradores pueden cambiar las directivas que se aplican a cualquier documento.

Cuando un documento está protegido por una política y se revocan los privilegios de acceso o se cambia la política aplicada, los cambios surten efecto de la siguiente manera:

* Si el documento está en línea, los cambios se aplican inmediatamente a menos que el usuario tenga el documento abierto. En este caso, el usuario debe cerrar el documento para que los cambios surtan efecto.
* Si un destinatario está utilizando el documento sin conexión (por ejemplo, en un ordenador portátil), los cambios tendrán efecto la próxima vez que el destinatario se sincronice con la seguridad del documento abriendo cualquier documento protegido por una política.

## Ver información sobre un documento {#view-information-about-a-document}

Para cada documento que aparece en la página Documentos, puede ver el nombre del documento, el nombre del editor, el nombre de la política y la fecha en que se protegió el documento. Si se ha eliminado la directiva que protegía un documento, el ID de directiva se muestra en Nombre de directiva.

También puede ver más detalles, que se describen a continuación, sobre un documento concreto en la página Detalles del documento:

>[!NOTE]
>
>Debe utilizar el vínculo Nombre de directiva de la página Detalle del documento para acceder a las directivas que se generan automáticamente en Microsoft Outlook para los destinatarios de un documento adjunto a un mensaje de correo electrónico. Estas directivas no aparecen en la página de directivas.

**** Nombre del documento: El nombre del documento seleccionado.

**** ID del documento: Identificador único que la seguridad del documento asigna cuando se aplica una política al documento. document security utiliza este número para rastrear el documento.

**** Estado del documento: Estado del documento (por ejemplo, activo o revocado).

**** Editor: Nombre del usuario que adjuntó la directiva al documento.

**** Nombre de directiva: Nombre de la directiva que se utiliza para proteger el documento. Puede hacer clic en el nombre para abrir la directiva. Debe utilizar este vínculo para acceder a las directivas que Acrobat genera para los destinatarios de un documento que está adjunto a un mensaje de correo electrónico en Outlook. Estas directivas no aparecen en la página Políticas.

**** Tipo de directiva: Tipo de directiva que se aplicó al documento.

**** Fecha de publicación: La fecha en que se aplicó la política al documento.

**** Iteraciones relacionadas: Si el documento tiene iteraciones relacionadas, este elemento también aparece en la lista. Haga clic en el vínculo para ver la lista de iteraciones relacionadas del documento.

Los usuarios pueden ver información sobre sus documentos protegidos. Los administradores pueden ver información sobre los documentos que cualquier usuario ha protegido con una política. Los coordinadores de conjuntos de políticas pueden ver información sobre los documentos protegidos por políticas desde sus conjuntos de políticas.

1. En la página de seguridad del documento, haga clic en Documentos.
1. En la lista de documentos, haga clic en el documento correspondiente. Se abre la página Detalles del documento, que muestra información detallada sobre el documento. Esta página también proporciona opciones para anular el acceso a documentos, cambiar la directiva y ver eventos relacionados con este documento.

## Ver iteraciones relacionadas de un documento {#view-related-iterations-for-a-document}

Si está habilitado el seguimiento de iteraciones relacionadas, puede rastrear versiones de un documento que han guardado varios usuarios. Esta función solo es compatible con determinadas aplicaciones, como PTC Pro/ENGINEER Wildfire.

Esta función resulta útil cuando varios usuarios colaboran y guardan distintas versiones del mismo documento. la seguridad de los documentos puede realizar un seguimiento de las distintas iteraciones; por lo tanto, puede ver fácilmente la información del documento de las distintas versiones.

Si esta función está habilitada, puede ver las iteraciones relacionadas de un documento desde la página Documentos.

1. Vea la página Detalles del documento de un documento. (Consulte [Ver información sobre un documento](controlling-access-policy-protected-documents.md#view-information-about-a-document)).
1. Haga clic en Ver iteraciones relacionadas. La opción solo está disponible si la función está habilitada. Aparece la lista de iteraciones relacionadas. Para cada iteración, puede ver la siguiente información:

   * **** Iteración: El nombre del archivo. Puede ser diferente del nombre de archivo original y tiene un número de versión anexado al final.
   * **** Editor: El editor del documento original.
   * **** Creado por: Usuario que guardó la iteración.
   * **** Fecha de creación: Fecha y hora en que se guardó la iteración.
   * **** Política: Política que protege la iteración. Diferentes iteraciones pueden estar protegidas por diferentes políticas.

1. Para mostrar la página Detalles del documento de esa iteración, haga clic en el nombre de archivo de una iteración.

## Revocación y restablecimiento del acceso a los documentos {#revoking-and-reinstating-access-to-documents}

Puede revocar y restablecer el acceso a los documentos protegidos por políticas:

**** Usuarios: Puede revocar o restablecer el acceso a los documentos que proteja con sus propias políticas personales o con políticas compartidas para las que la capacidad de revocar esté habilitada para el usuario que aplique la política. Los usuarios que no puedan anular el acceso a un documento o cambiar una política deben ponerse en contacto con el administrador.

**** Administradores: Puede revocar o restablecer los privilegios de acceso a cualquier documento protegido por una política, incluidos los protegidos por políticas personales o compartidas. Si un administrador anula el acceso a un documento protegido con una directiva compartida, sólo un administrador puede restablecer los privilegios de acceso para ese documento.

**** Coordinadores de conjuntos de políticas: Puede revocar o restablecer los privilegios de acceso para documentos que protegen las políticas de sus conjuntos de políticas.

Cuando se revocan o restablecen los privilegios de acceso a documentos, el cambio se aplica en estos momentos:

* Si el documento está en línea y cerrado, el cambio surte efecto la próxima vez que el destinatario se sincronice con la seguridad del documento abriendo un documento protegido por una política.
* Si el documento está en línea y abierto, el cambio surte efecto cuando el destinatario cierra el documento.
* Si el documento está sin conexión (en uso sin conexión a Internet, como en un equipo portátil), el cambio se aplicará la próxima vez que el destinatario se sincronice con la seguridad del documento.

**Revocar el acceso a un documento protegido por una política**

1. En la página de seguridad del documento, haga clic en Documentos.
1. Seleccione la casilla de verificación situada junto al documento correspondiente y haga clic en Revocar. Puede anular el acceso a varios documentos a la vez.
1. Seleccione un mensaje para mostrar a los usuarios que intenten abrir el documento después de que se revoque:

   * **** Mensaje general: Indica que el autor revocó el documento
   * **** Documento finalizado: Indica que el autor finalizó el documento
   * **Documento revisado**: Indica que el autor revisó el documento

1. (Opcional) Si hay disponible una versión más reciente del documento, introduzca la URL y haga clic en Probar para comprobar la URL.
1. Haga clic en Aceptar y, a continuación, en Aceptar nuevamente para volver a la página Documentos.

**Restablecer privilegios de acceso a documentos**

1. En la página de seguridad del documento, haga clic en Documentos.
1. En la lista de documentos, haga clic en el documento correspondiente.
1. Haga clic en Anular revocación y, a continuación, en Aceptar.

## Cambiar una directiva aplicada a un documento {#switch-a-policy-that-is-applied-to-a-document}

Los usuarios, coordinadores de conjuntos de políticas y administradores pueden cambiar la política que se aplica a un documento protegido por una política (solo puede aplicar una política a la vez a un documento). Los usuarios pueden cambiar las directivas que se aplican a sus propios documentos protegidos por políticas si han creado la política o si la política es compartida y tiene esta capacidad habilitada. De lo contrario, el administrador o el coordinador del conjunto de directivas deben cambiar la directiva. Los administradores pueden cambiar las directivas de los documentos protegidos por políticas de cualquier usuario. Los coordinadores de conjuntos de políticas pueden cambiar las políticas de sus conjuntos de políticas.

Al cambiar una directiva, la nueva se aplica de la siguiente manera:

* Si el documento está en línea y cerrado, el cambio surte efecto la próxima vez que el destinatario se sincronice con la seguridad del documento, abriendo cualquier documento protegido por una política en línea.
* Si el documento está en línea y abierto, el cambio surte efecto cuando el usuario cierra el documento.
* Si el documento está sin conexión (en uso sin una conexión activa a Internet o a la red, como en un equipo portátil), el cambio se aplica la próxima vez que el usuario se sincronice con la seguridad del documento abriendo un documento protegido por una política en línea.

>[!NOTE]
>
>Para permitir el acceso anónimo a un documento protegido por una política que actualmente no tiene este acceso, elimine la política existente en la aplicación cliente y, a continuación, aplique una política que permita el acceso anónimo. Si cambia la directiva, los usuarios deben iniciar sesión para acceder al documento.

1. En la página de seguridad del documento, haga clic en Documentos.
1. En la lista de documentos, haga clic en el documento correspondiente.
1. Haga clic en Cambiar directiva. Aparece una lista de hasta 100 directivas.
1. Si no se muestra la directiva que desea, seleccione Nombre de directiva o ID de directiva en la lista Buscar, escriba el nombre o ID y haga clic en Buscar.
1. Haga clic en una nueva directiva de la lista.
1. Haga clic en Cambiar directiva y, a continuación, haga clic en Aceptar para volver a la página Documentos.

## Buscar un documento {#search-for-a-document}

Puede buscar documentos en la página Documentos mediante una combinación de criterios de intervalo de fechas y criterios de búsqueda disponibles en la lista. Estos criterios incluyen el nombre del documento, el nombre de la política o todos los documentos.

Algunas opciones de búsqueda adicionales solo están disponibles para los administradores:

**** ID del documento: Número de ID único que la seguridad del documento asigna al documento cuando se aplica la política.

**** Nombre del documento: Nombre del documento.

**** Nombre del editor: Nombre del usuario que adjuntó la directiva al documento. Puede seleccionar el usuario de todos los dominios o de un dominio especificado.

**** Id. de directiva: Número de ID de la directiva adjunta al documento.

**** Nombre de directiva: Nombre de la directiva adjunta al documento.

**** Todos los documentos: Todos los documentos protegidos por administradores y usuarios. El uso de la opción Todos los documentos para buscar puede devolver una larga lista de documentos.

1. En la página de seguridad del documento, haga clic en Documentos.
1. En la lista Buscar, seleccione los criterios de búsqueda necesarios.

   Puede especificar los criterios como ID del documento, nombre del documento, nombre del editor, ID de la política, nombre de la política o todos los documentos.

   Si especifica el nombre del editor, haga clic en el icono de la Libreta de direcciones, especifique el dominio en el que desea buscar al usuario y haga clic en Aceptar para volver a la página de búsqueda Documentos.

1. (Opcional) En la lista Fecha, seleccione una opción de intervalo de fechas. Si selecciona Fechas personalizadas, escriba la fecha en formato aaaa/mm/dd en los cuadros que aparecen o utilice el Selector de fecha para especificar el intervalo de fechas:

   * Haga clic en el calendario para abrir el Selector de fecha.
   * Utilice las flechas para buscar un año y un mes.
   * Haga clic en un día del mes en el calendario.
   * Haga clic en Aceptar para cerrar el Selector de fecha.

1. Haga clic en Buscar.

## Ordenar la lista de documentos {#sort-the-document-list}

Puede ordenar la lista de documentos por encabezado de columna. Los iconos de triángulo junto al encabezado de la columna indican qué columna se utiliza actualmente para ordenar. Un triángulo que apunta hacia arriba indica el orden ascendente, mientras que un triángulo que apunta hacia abajo indica el orden descendente.

1. En la página de seguridad del documento, haga clic en Documentos.
1. Haga clic en el encabezado de columna correspondiente.
1. Para cambiar el orden, vuelva a hacer clic en la columna.

## Agregar página de portada a documentos protegidos por políticas {#add-cover-page-to-policy-protected-documents}

En el caso de la mayoría de los visores de PDF que no son de Adobe, si abre un documento protegido por la seguridad, la primera página se muestra como una página en blanco o la aplicación se cancela sin abrir el documento.

Puede utilizar la compatibilidad con Página 0 (Documento de envoltorio) para permitir que los visores que no sean de Adobe PDF abran un documento protegido y muestren una portada en el documento.

>[!NOTE]
>
>Al ver dichos documentos (que contienen una página 0) en Adobe Reader/Acrobat o Mobile Reader, el documento protegido se abre de forma predeterminada.

**Para agregar una portada a un documento protegido por una política**

Utilice los siguientes procesos en el área de trabajo:

**** ProtegerDocumento con portada: Protege un documento PDF con la política especificada y agrega una portada al documento

**** Extraer documento protegido: Extrae el documento PDF protegido por una política del documento PDF con la portada

Utilice las siguientes API de seguridad de documento:

****`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` protectedDocumentWithCoverPage: Protege un PDF determinado con la política especificada y devuelve un documento con una portada y el documento protegido como **extractProtectedDocument adjunto**: Extrae el documento protegido, que es un archivo adjunto en el documento con portada. El documento con la portada se puede crear con el método protectedDocumentWithCoverPage`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`