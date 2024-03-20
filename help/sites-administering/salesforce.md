---
title: Integración con Salesforce
description: Obtenga información sobre la integración de Adobe Experience Manager AEM () con Salesforce.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0f3aaa0a-ccfb-4162-97a6-ee5485595d28
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 0%

---


# Integración con Salesforce {#integrating-with-salesforce}

Al integrar Salesforce con Adobe Experience Manager AEM (), se proporcionan capacidades de administración de posibles clientes y se utilizan las capacidades existentes listas para usarse de Salesforce. AEM Puede configurar la publicación de posibles clientes en Salesforce y crear componentes que accedan a los datos directamente desde Salesforce.

AEM La integración bidireccional y ampliable entre las soluciones de y Salesforce permite:

* Que las organizaciones utilicen y modifiquen completamente los datos para mejorar la experiencia del cliente.
* Participación desde el marketing hasta las actividades de ventas.
* Organizaciones que transmiten y reciben datos automáticamente desde un almacén de datos de Salesforce.

Este documento describe lo siguiente:

* Cómo configurar los Cloud Service AEM de Salesforce (configurar los parámetros para que se integren con Salesforce).
* Aprenda a utilizar la información de contacto/posible cliente de Salesforce en Client Context y para personalización.
* AEM Aprenda a utilizar el modelo de flujo de trabajo de Salesforce para publicar usuarios como posibles clientes en Salesforce.
* Obtenga información sobre cómo crear un componente que muestre datos de Salesforce.

## AEM Configuración de la integración de con Salesforce {#configuring-aem-to-integrate-with-salesforce}

AEM Para configurar la integración de los usuarios con Salesforce, primero debe configurar una aplicación de acceso remoto en Salesforce. A continuación, configure el servicio en la nube de Salesforce para que se vincule a esta aplicación de acceso remoto.

>[!NOTE]
>
>Puede crear una cuenta de desarrollador gratuita en Salesforce.

AEM Para configurar la integración de los con Salesforce:

>[!CAUTION]
>
>Instale el [API de Salesforce](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=salesforce*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=2&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcom.adobe.cq.mcm.salesforce.content-1.0.4.zip) integración antes de continuar con el procedimiento. Para obtener más información sobre cómo trabajar con paquetes, consulte la [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md#package-share) página.

1. AEM En, navegue hasta **Cloud Service**. En Servicios de terceros, haga clic en **Configurar ahora** in **Salesforce**.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Cree una configuración, por ejemplo, **promotor**.

   >[!NOTE]
   >
   >La nueva configuración redirige a una nueva página: **http://localhost:4502/etc/cloudservices/salesforce/developer.html**. Este es exactamente el mismo valor que debe especificar en la URL de devolución de llamada al crear la aplicación de acceso remoto en Salesforce. Estos valores deben coincidir.

1. Inicie sesión en su cuenta de Salesforce (o si no la tiene, cree una en [https://developer.salesforce.com](https://developer.salesforce.com).)
1. En Salesforce, vaya a **Crear** > **Aplicaciones** para llegar a **Aplicaciones conectadas** (en versiones anteriores de Salesforce, el flujo de trabajo era **Implementar** > **Acceso remoto**).
1. Clic **Nuevo** AEM para que pueda conectarse con Salesforce de forma.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Introduzca el **Nombre de aplicación conectada**, **Nombre de API**, y **Correo electrónico de contacto**. Seleccione el **Habilitar la configuración de OAuth** marque la casilla e introduzca la **URL de devolución de llamada** y agregue un ámbito de OAuth (por ejemplo, acceso completo). La URL de devolución de llamada tiene un aspecto similar al siguiente: `http://localhost:4502/etc/cloudservices/salesforce/developer.html`

   Cambie el nombre del servidor/número de puerto y el nombre de página para que coincidan con la configuración.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Clic **Guardar** para guardar la configuración de Salesforce. Salesforce crea un **clave del cliente** y **secreto de cliente** AEM , que necesita para la configuración de la.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >Espere varios minutos (hasta 15 minutos) para que se active la aplicación de acceso remoto en Salesforce.

1. AEM En, navegue hasta **Cloud Service** y vaya a la configuración de Salesforce que creó anteriormente (por ejemplo, **promotor**). Clic **Editar** e introduzca la clave de cliente y el secreto de cliente desde salesforce.com.

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | URL de inicio de sesión | Este es el punto final de autorización de Salesforce. Su valor está rellenado previamente y sirve para la mayoría de los casos. |
   |---|---|
   | Clave de cliente | Escriba el valor obtenido de la página Registro de aplicación de acceso remoto en salesforce.com |
   | Secreto del cliente | Escriba el valor obtenido de la página Registro de aplicación de acceso remoto en salesforce.com |

1. Clic **Conectar con Salesforce** para conectarse. Salesforce solicita que permita que la configuración se conecte a Salesforce.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   AEM En, se abre un cuadro de diálogo de confirmación que le indica que se ha conectado correctamente.

1. Vaya a la página raíz del sitio web y haga clic en **Propiedades de página**. A continuación seleccione **Cloud Service** y agregue **Salesforce** y seleccione la configuración correcta (por ejemplo, **promotor**).

   ![chlimage_1-75](assets/chlimage_1-75.png)

   Ahora puede utilizar el modelo de flujo de trabajo para publicar posibles clientes en Salesforce y crear componentes que accedan a los datos desde Salesforce.

## AEM Exportación de usuarios de como posibles clientes de Salesforce {#exporting-aem-users-as-salesforce-leads}

AEM Si desea exportar un usuario como cliente potencial de Salesforce, configure el flujo de trabajo para publicar posibles clientes en Salesforce.

AEM Para exportar usuarios de como posibles clientes de Salesforce:

1. Vaya al flujo de trabajo de Salesforce en `http://localhost:4502/workflow` haciendo clic con el botón derecho en el flujo de trabajo **Exportación de Salesforce.com** y haciendo clic en **Inicio**.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. AEM Seleccione el usuario de la cuenta de usuario que desea crear como posible cliente, como el **Carga útil** para este flujo de trabajo (inicio > usuarios). Asegúrese de seleccionar el nodo de perfil del usuario, ya que contiene información como **givenName**, y  **familyName**, que se asignan a los posibles clientes de Salesforce **FirstName** y **LastName** campos.

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >AEM Antes de iniciar este flujo de trabajo, hay ciertos campos obligatorios que un nodo principal en la aplicación debe tener antes de publicarse en Salesforce. Estos son **givenName**, **familyName**, **compañía**, y **email**. AEM Para ver una lista completa de las asignaciones entre el usuario y el posible cliente de Salesforce, consulte: [AEM Asignación de configuración entre el usuario de la aplicación y el posible cliente de Salesforce.](#mapping-configuration-between-aem-user-and-salesforce-lead)

1. Haga clic en **Aceptar**. La información de usuario se exporta a salesforce.com. Puede verificarlo en salesforce.com.

   >[!NOTE]
   >
   >Los registros de errores muestran si se importa un posible cliente. Consulte el registro de errores para obtener más información.

### Configuración del flujo de trabajo de exportación de Salesforce.com {#configuring-the-salesforce-com-export-workflow}

Si es necesario, configure el flujo de trabajo de exportación de Salesforce.com para que coincida con la configuración correcta de Salesforce.com o para realizar otros cambios.

Para configurar el flujo de trabajo de exportación de Salesforce.com:

1. Navegue hasta `http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.`

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. Abra el paso Exportación de Salesforce.com y seleccione **Argumentos** , seleccione la configuración correcta y haga clic en **OK**. Además, si desea que el flujo de trabajo vuelva a crear un posible cliente eliminado en Salesforce, active la casilla de verificación.

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Clic **Guardar** para guardar los cambios.

   ![chlimage_1-79](assets/chlimage_1-79.png)

### AEM Asignación de la configuración entre el usuario de y el posible cliente de Salesforce {#mapping-configuration-between-aem-user-and-salesforce-lead}

AEM Para ver o editar la configuración de asignación actual entre un usuario de la aplicación y un posible cliente de Salesforce, abra el Administrador de configuración: `https://<hostname>:<port>/system/console/configMgr` y buscar **Configuración de asignación de posibles clientes de Salesforce**.

1. Abra el Administrador de configuración haciendo clic en **Consola web** o ir directamente a `https://<hostname>:<port>/system/console/configMgr.`
1. Buscar por **Configuración de asignación de posibles clientes de Salesforce**.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Cambie las asignaciones según sea necesario. La asignación predeterminada sigue el patrón **aemUserAttribute=sfLeadAttribute**. Clic **Guardar** para guardar los cambios.

## Configurar el almacén de Client Context de Salesforce {#configuring-salesforce-client-context-store}

AEM El almacén de contexto del cliente de Salesforce muestra información adicional sobre el usuario que ha iniciado sesión actualmente que lo que ya está disponible en el cliente de. Extrae esta información adicional de Salesforce según la conexión del usuario con Salesforce.

Para ello, configure lo siguiente:

1. AEM Vincule un usuario de con un ID de Salesforce a través del componente Salesforce Connect.
1. Agregue los datos de perfil de Salesforce a la página de contexto del cliente para que pueda configurar qué propiedades desea ver.
1. (Opcional) Cree un segmento que utilice los datos del almacén de Client Context de Salesforce.

### AEM Vinculación de un usuario de con un ID de Salesforce {#linking-an-aem-user-with-a-salesforce-id}

AEM Asigne un usuario de con un ID de Salesforce para que pueda cargarlo en el contexto del cliente. En una situación real, se establecería una vinculación basada en datos de usuario conocidos con validación. Para fines de demostración, en este procedimiento se utiliza la variable **Salesforce Connect** componente.

1. AEM Vaya a un sitio web en, inicie sesión, y arrastre y suelte el elemento de la barra de herramientas. **Salesforce Connect** Componente de la barra de tareas.

   >[!NOTE]
   >
   >Si la variable **Salesforce Connect** El componente no está disponible, vaya a **Diseño** visualizarlo y seleccionarlo para que esté disponible en la **Editar** vista.

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   Al arrastrar el componente a la página, se muestra **Vínculo a Salesforce=Desactivado**.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >Este componente solo tiene fines de demostración. En situaciones reales, habría otro proceso para vincular o hacer coincidir a los usuarios con posibles clientes.

1. Después de arrastrar el componente en la página, ábralo para configurarlo. Seleccione la configuración, el tipo de contacto y el posible cliente o contacto de Salesforce y haga clic en **OK**.

   ![chlimage_1-82](assets/chlimage_1-82.png)

   AEM Vincula al usuario con el contacto o posible cliente de Salesforce.

   ![chlimage_1-83](assets/chlimage_1-83.png)

### Añadir datos de Salesforce a Client Context {#adding-salesforce-data-to-client-context}

Puede cargar datos de usuario de Salesforce en Client Context para usarlos para la personalización:

1. Abra el contexto de cliente que desea ampliar navegando allí, por ejemplo, `http://localhost:4502/etc/clientcontext/default/content.html.`

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. Arrastre el **Datos de perfil de Salesforce** al contexto del cliente.

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. Abra el componente haciendo doble clic en él. Seleccionar **Agregar elemento** y seleccione una propiedad de la lista desplegable. Añada tantas propiedades como desee y seleccione. **OK**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. Ahora verá las propiedades específicas de Salesforce de Salesforce en el contexto de cliente.

   ![chlimage_1-85](assets/chlimage_1-85.png)

### Creación de un segmento con datos del almacén de Client Context de Salesforce {#building-a-segment-using-data-from-salesforce-client-context-store}

Puede crear un segmento que utilice datos del almacén de contexto de cliente de Salesforce. Para ello, haga lo siguiente:

1. AEM Vaya a la segmentación de en la lista de segmentos de la lista de distribución de. **Herramientas** > **Segmentación** o va a [http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation).
1. Cree o actualice un segmento para incluir datos de Salesforce. Para obtener más información, consulte [Segmentación](/help/sites-administering/campaign-segmentation.md).

## Buscando posibles clientes {#searching-leads}

AEM Se envía con un componente de búsqueda de muestra que busca posibles clientes en Salesforce según los criterios dados. Este componente muestra cómo utilizar la API de REST de Salesforce para buscar objetos de Salesforce. Para almacenar en déclencheur una llamada a salesforce.com, vincule una página con una configuración de Salesforce.

>[!NOTE]
>
>Este es un componente de ejemplo que muestra cómo utilizar la API de REST de Salesforce para consultar objetos Salesforce. Utilícelo como ejemplo para crear componentes más complejos según sus necesidades.

Para utilizar este componente:

1. Desplácese hasta la página en la que desee utilizar esta configuración. Abra las propiedades de la página y seleccione **Cloud Service.** Clic **Agregar servicios** y seleccione **Salesforce** y la configuración adecuada, y haga clic en **OK**.

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. Arrastre el componente de búsqueda de Salesforce a la página (siempre que se haya habilitado). Para habilitarlo, vaya al modo Diseño y agréguelo al área correspondiente).

   ![chlimage_1-21](assets/chlimage_1-21.jpeg)

1. Abra el componente Buscar, especifique los parámetros de búsqueda y haga clic en **OK.**

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. AEM muestra los posibles clientes especificados en el componente de búsqueda que coinciden con los criterios especificados.

   ![chlimage_1-87](assets/chlimage_1-87.png)
