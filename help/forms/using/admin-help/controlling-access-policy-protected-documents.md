---
title: Control del acceso a documentos protegidos por políticas
seo-title: Control del acceso a documentos protegidos por políticas
description: Consulte cómo puede ver, administrar y controlar el acceso a los documentos protegidos por políticas.
seo-description: Consulte cómo puede ver, administrar y controlar el acceso a los documentos protegidos por políticas.
uuid: 2d9f95e9-e4ee-47e2-988e-a191d1d1d264
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f34058c3-384a-4b73-a386-5bc9125acbf8
feature: Seguridad de los documentos
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2190'
ht-degree: 0%

---


# Control del acceso a documentos protegidos por políticas {#controlling-access-to-policy-protected-documents}

Puede controlar la forma en que los destinatarios utilizan los documentos protegidos por políticas independientemente de la cantidad de documentos que los distribuya.

Mediante la página Documentos puede realizar las siguientes tareas:

* Busque y vea los detalles de los documentos protegidos por políticas. Puede ver información sobre el nombre del documento, el nombre del editor, el nombre de la directiva y la fecha en que se aplicó la directiva. Si se elimina la directiva que protegía un documento, también puede ver el ID de la directiva eliminada bajo el nombre de la directiva. Los usuarios pueden ver y administrar sus propios documentos protegidos por políticas. Los administradores pueden ver y administrar todos los documentos protegidos por políticas.
* Cambie los detalles de la directiva que se aplica a un documento. Los usuarios pueden editar sus propias políticas, los administradores pueden editar las políticas compartidas y personales, y los coordinadores de los conjuntos de políticas pueden editar las políticas compartidas en los conjuntos de políticas para los que tienen permisos. Puede acceder a la directiva asociada a un documento directamente desde la página Detalles del documento.
* Revocar y restablecer el acceso a un documento protegido por políticas. Los administradores pueden revocar y restablecer el acceso a cualquier documento. Los coordinadores de conjuntos de políticas (que tienen permiso para administrar documentos) pueden revocar y restablecer el acceso a los documentos protegidos por políticas que utilizan políticas compartidas desde sus conjuntos de políticas. Los usuarios pueden revocar el acceso a sus documentos protegidos por políticas si han creado la política que protege el documento o si la política es compartida y permite esta capacidad.
* Cambie la directiva que se aplica a un documento. Los usuarios que aplican directivas a los documentos pueden cambiar una directiva si la han creado o si se trata de una directiva compartida que habilita esta capacidad. Los coordinadores de conjuntos de políticas pueden cambiar las políticas de sus conjuntos de políticas. Los administradores pueden cambiar las directivas que se aplican a cualquier documento.

Cuando un documento está protegido por una directiva y usted revoca los privilegios de acceso o cambia la política aplicada, los cambios surten efecto de la siguiente manera:

* Si el documento está en línea, los cambios se aplican inmediatamente a menos que el usuario tenga el documento abierto. En este caso, el usuario debe cerrar el documento para que los cambios surtan efecto.
* Si un destinatario está utilizando el documento sin conexión (por ejemplo, en un portátil), los cambios surtirán efecto la próxima vez que el destinatario se sincronice con la seguridad del documento abriendo cualquier documento protegido por políticas.

## Ver información sobre un documento {#view-information-about-a-document}

Para cada documento que aparece en la página Documentos, puede ver el nombre del documento, el nombre del editor, el nombre de la política y la fecha en que se protegió el documento. Si se ha eliminado la directiva que protegía un documento, el ID de la directiva aparece en Nombre de la directiva.

También puede ver más detalles, que se describen a continuación, sobre un documento concreto en la página Detalles del documento:

>[!NOTE]
>
>Debe utilizar el vínculo Nombre de directiva de la página Detalle del documento para acceder a las directivas que se generan automáticamente en Microsoft Outlook para los destinatarios de un documento que está adjunto a un mensaje de correo electrónico. Estas políticas no aparecen en la página de directivas.

**Nombre del documento:** el nombre del documento seleccionado.

**ID del documento:**  identificador único que asigna la seguridad del documento cuando se aplica una política al documento. document security utiliza este número para realizar un seguimiento del documento.

**Estado del documento:** estado del documento (por ejemplo, activo o revocado).

**Editor:** nombre del usuario que adjuntó la directiva al documento.

**Nombre de directiva:** el nombre de la directiva que se usa para proteger el documento. Puede hacer clic en el nombre para abrir la directiva. Debe utilizar este vínculo para acceder a las directivas que Acrobat genera para los destinatarios de un documento que está adjunto a un mensaje de correo electrónico en Outlook. Estas políticas no aparecen en la página Directivas .

**Tipo de directiva:** el tipo de directiva que se aplicó al documento.

**Fecha de publicación:** la fecha en la que se aplicó la política al documento.

**Iteraciones relacionadas:** si el documento tiene iteraciones relacionadas, este elemento también aparece en la lista. Haga clic en el vínculo para ver la lista de iteraciones relacionadas para el documento.

Los usuarios pueden ver información sobre sus documentos protegidos. Los administradores pueden ver información sobre documentos que cualquier usuario ha protegido con una directiva. Los coordinadores de conjuntos de políticas pueden ver información sobre documentos protegidos por políticas de sus conjuntos de políticas.

1. En la página de seguridad del documento, haga clic en Documentos.
1. En la lista de documentos, haga clic en el documento correspondiente. Se abre la página Detalles del documento, que muestra información detallada sobre el documento. Esta página también proporciona opciones para revocar el acceso al documento, cambiar la directiva y ver los eventos relacionados con este documento.

## Ver iteraciones relacionadas de un documento {#view-related-iterations-for-a-document}

Si está habilitado el seguimiento de iteraciones relacionadas, puede rastrear versiones de un documento que varios usuarios han guardado. Esta función solo es compatible con ciertas aplicaciones, como PTC Pro/ENGINEER Wildfire.

Esta función resulta útil cuando varios usuarios colaboran y guardan distintas versiones del mismo documento. la seguridad de los documentos puede realizar un seguimiento de las distintas iteraciones; por lo tanto, puede ver fácilmente la información del documento de las distintas versiones.

Si esta función está habilitada, puede ver las iteraciones relacionadas de un documento desde la página Documentos.

1. Vea la página Detalle del documento de un documento. (Consulte [Ver información sobre un documento](controlling-access-policy-protected-documents.md#view-information-about-a-document)).
1. Haga clic en Ver iteraciones relacionadas. La opción solo está disponible si la función está habilitada. Aparecerá la lista de iteraciones relacionadas. Para cada iteración, puede ver la siguiente información:

   * **Iteración:** El nombre de archivo. Puede ser diferente del nombre de archivo original y tiene un número de versión anexado al final.
   * **Editor:** el editor del documento original.
   * **Creado por:** el usuario que guardó la iteración.
   * **Fecha de creación:** fecha y hora en que se guardó la iteración.
   * **Política:** la política que protege la iteración. Las distintas iteraciones pueden estar protegidas por políticas diferentes.

1. Para mostrar la página Detalle del documento para esa iteración, haga clic en el nombre de archivo de una iteración.

## Revocación y restablecimiento del acceso a los documentos {#revoking-and-reinstating-access-to-documents}

Puede revocar y restablecer el acceso a los documentos protegidos por políticas:

**Usuarios:** pueden revocar o restablecer el acceso a los documentos que protegen con sus propias políticas personales o con políticas compartidas para las que la capacidad de revocación esté habilitada para el usuario que aplique la política. Los usuarios que no puedan revocar el acceso a un documento o cambiar una directiva deben ponerse en contacto con el administrador.

**Administradores:** pueden revocar o restablecer privilegios de acceso a cualquier documento protegido por políticas, incluidos los protegidos por políticas personales o compartidas. Si un administrador revoca el acceso a un documento protegido con una directiva compartida, solo un administrador puede restablecer los privilegios de acceso para ese documento.

**Coordinadores de conjuntos de políticas:** pueden revocar o restablecer privilegios de acceso para documentos que protegen las políticas de sus conjuntos de políticas.

Cuando revoca o restablece los privilegios de acceso a documentos, el cambio entra en vigor en estos momentos:

* Si el documento está en línea y cerrado, el cambio surte efecto la próxima vez que el destinatario se sincronice con la seguridad del documento abriendo un documento protegido por políticas.
* Si el documento está en línea y abierto, el cambio surte efecto cuando el destinatario cierra el documento.
* Si el documento está sin conexión (en uso sin conexión a Internet, como en un ordenador portátil), el cambio surte efecto la próxima vez que el destinatario se sincronice con la seguridad del documento.

**Revocar el acceso a un documento protegido por una política**

1. En la página de seguridad del documento, haga clic en Documentos.
1. Seleccione la casilla de verificación situada junto al documento correspondiente y haga clic en Revocar. Puede revocar el acceso a varios documentos a la vez.
1. Seleccione un mensaje para mostrar a los usuarios que intenten abrir el documento después de revocarlo:

   * **Mensaje general:** indica que el autor revocó el documento
   * **Documento finalizado:** indica que el autor finalizó el documento
   * **Documento revisado**: Indica que el autor revisó el documento

1. (Opcional) Si hay disponible una versión más reciente del documento, introduzca la dirección URL y haga clic en Probar para verificar la dirección URL.
1. Haga clic en Aceptar y, a continuación, en Aceptar de nuevo para volver a la página Documentos.

**Restablecer privilegios de acceso a documentos**

1. En la página de seguridad del documento, haga clic en Documentos.
1. En la lista de documentos, haga clic en el documento correspondiente.
1. Haga clic en Anular revocación y, a continuación, haga clic en Aceptar.

## Cambiar una directiva aplicada a un documento {#switch-a-policy-that-is-applied-to-a-document}

Los usuarios, coordinadores de conjuntos de directivas y administradores pueden cambiar la directiva que se aplica a un documento protegido por políticas (solo puede aplicar una directiva a la vez a un documento). Los usuarios pueden cambiar de políticas que se aplican a sus propios documentos protegidos por políticas si han creado la directiva o si la directiva es compartida y tiene esta capacidad habilitada. De lo contrario, el administrador o el coordinador del conjunto de directivas deben cambiar la directiva. Los administradores pueden cambiar de directiva para cualquier documento protegido por políticas del usuario. Los coordinadores de conjuntos de políticas pueden cambiar las políticas de sus conjuntos de políticas.

Al cambiar una directiva, la nueva directiva se aplica de la siguiente manera:

* Si el documento está en línea y cerrado, el cambio entra en vigor la próxima vez que el destinatario se sincroniza con la seguridad del documento abriendo cualquier documento protegido por políticas en línea.
* Si el documento está en línea y abierto, el cambio entra en vigor cuando el usuario cierra el documento.
* Si el documento está sin conexión (en uso sin una conexión activa a Internet o a la red, como en un portátil), el cambio se aplica la próxima vez que el usuario se sincronice con la seguridad del documento abriendo un documento protegido por políticas en línea.

>[!NOTE]
>
>Para permitir el acceso anónimo a un documento protegido por políticas que actualmente no tiene este acceso, elimine la política existente en la aplicación cliente y, a continuación, aplique una política que permita el acceso anónimo. Si cambia la directiva, los usuarios deberán iniciar sesión para acceder al documento.

1. En la página de seguridad del documento, haga clic en Documentos.
1. En la lista de documentos, haga clic en el documento correspondiente.
1. Haga clic en Cambiar directiva. Se muestra una lista de hasta 100 directivas.
1. Si no se muestra la directiva que desea, seleccione Nombre de directiva o ID de directiva en la lista Buscar, escriba el nombre o ID y haga clic en Buscar.
1. Haga clic en una política nueva de la lista.
1. Haga clic en Cambiar directiva y, a continuación, haga clic en Aceptar para volver a la página Documentos.

## Buscar un documento {#search-for-a-document}

Puede buscar documentos en la página Documentos mediante una combinación de criterios de intervalo de fechas y criterios de búsqueda disponibles en la lista. Estos criterios incluyen el nombre del documento, el nombre de la directiva o todos los documentos.

Algunas opciones de búsqueda adicionales solo están disponibles para los administradores:

**ID de documento:** Número de ID único que la seguridad del documento asigna al documento cuando se aplica la política.

**Nombre del documento:** Nombre del documento.

**Nombre del publicador:** Nombre del usuario que adjuntó la directiva al documento. Puede seleccionar el usuario de todos los dominios o de un dominio especificado.

**ID de directiva:** número de ID de la directiva adjunta al documento.

**Nombre de la directiva:** Nombre de la directiva adjunta al documento.

**Todos los documentos:** Todos los documentos protegidos por administradores y usuarios. El uso de la opción Todos los documentos para buscar puede devolver una larga lista de documentos.

1. En la página de seguridad del documento, haga clic en Documentos.
1. En la lista Buscar, seleccione los criterios de búsqueda necesarios.

   Puede especificar los criterios como ID del documento, nombre del documento, nombre del editor, ID de la política, nombre de la política o todos los documentos.

   Si especifica el nombre del editor, haga clic en el icono de la Libreta de direcciones, especifique el dominio en el que desea buscar al usuario y haga clic en Aceptar para volver a la página de búsqueda Documentos.

1. (Opcional) En la lista Fecha, seleccione una opción de intervalo de fechas. Si selecciona Fechas personalizadas, escriba la fecha con el formato aaaa/mm/dd en las casillas que aparecen o use el Selector de fechas para especificar el intervalo de fechas:

   * Haga clic en el calendario para abrir el selector de fechas.
   * Utilice las flechas para encontrar un año y un mes.
   * Haga clic en un día del mes en el calendario.
   * Haga clic en Aceptar para cerrar el selector de fechas.

1. Haga clic en Buscar.

## Ordenar la lista de documentos {#sort-the-document-list}

Puede ordenar la lista de documentos por encabezado de columna. Los iconos de triángulo junto al encabezado de la columna indican qué columna se utiliza actualmente para ordenar. Un triángulo que señala hacia arriba indica el orden ascendente, mientras que un triángulo que señala hacia abajo indica el orden descendente.

1. En la página de seguridad del documento, haga clic en Documentos.
1. Haga clic en el encabezado de columna correspondiente.
1. Para cambiar el orden, vuelva a hacer clic en la columna .

## Agregar portada a documentos protegidos por políticas {#add-cover-page-to-policy-protected-documents}

En el caso de la mayoría de los visores que no son de Adobe PDF, si abre un documento protegido por seguridad de documento, la primera página se muestra como una página en blanco o la aplicación se interrumpe sin abrir el documento.

Puede utilizar la compatibilidad con Página 0 (documento de envoltura) para permitir que los visores que no sean de Adobe PDF abran un documento protegido y muestren una portada en el documento.

>[!NOTE]
>
>Al ver estos documentos (que contienen una Página 0) en Adobe Reader/Acrobat o Mobile Reader, el documento protegido se abre de forma predeterminada.

**Para agregar una portada a un documento protegido por una directiva**

Utilice los siguientes procesos en el área de trabajo:

**Documento de Protect con portada:** protege un documento PDF con la política especificada y agrega una portada al documento

**Extraer documento protegido:** extrae el documento PDF protegido por políticas del documento PDF con portada

Utilice las siguientes API de seguridad del documento:

**protectionDocumentWithCoverPage:** protege un PDF determinado con la política especificada y devuelve un documento con una portada y el documento protegido como un 
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractoProtegidoDocument adjunto:**  extrae el documento protegido que es un archivo adjunto en el documento con portada. El documento con la portada se puede crear utilizando el método protectionDocumentWithCoverPage
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`