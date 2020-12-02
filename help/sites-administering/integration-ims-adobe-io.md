---
title: Integración con Adobe Target mediante Adobe I/O
seo-title: Integración con Adobe Target mediante Adobe I/O
description: Obtenga información sobre la integración de AEM con Adobe Target mediante Adobe I/O
seo-description: Obtenga información sobre la integración de AEM con Adobe Target mediante Adobe I/O
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
translation-type: tm+mt
source-git-commit: 26efba567985dcb89b2610935cab18943b7034b3
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 1%

---


# Integración con Adobe Target mediante Adobe I/O{#integration-with-adobe-target-using-adobe-i-o}

La integración de AEM con Adobe Target mediante la API de Target Standard requiere la configuración de Adobe IMS (Identity Management System) y Adobe I/O.

>[!NOTE]
>
>La compatibilidad con la API de Adobe Target Standard es nueva en AEM 6.5. La API de Target Standard utiliza la autenticación IMS.
>
>El uso de la API de Adobe Target Classic en AEM sigue siendo compatible con versiones anteriores. La [API de Destinatario Classic utiliza autenticación de credenciales de usuario](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).
>
>La selección de la API está impulsada por el método de autenticación utilizado para la integración de AEM/Destinatario.

## Requisitos previos {#prerequisites}

Antes de iniciar este procedimiento:

* [La ](https://helpx.adobe.com/es/contact/enterprise-support.ec.html) asistencia de Adobe debe aprovisionar su cuenta para:

   * Consola de Adobe
   * Adobe I/O
   * Adobe Target y
   * Adobe IMS (sistema Identity Management)

* El administrador de sistemas de su organización debe utilizar el Admin Console para agregar los desarrolladores requeridos de su organización a los perfiles de productos relevantes.

   * Esto proporciona a los desarrolladores específicos permisos para habilitar integraciones dentro de Adobe I/O.
   * Para obtener más información, consulte [Administrar programadores](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configuración de IMS - Generación de una clave pública {#configuring-an-ims-configuration-generating-a-public-key}

La primera etapa de la configuración es crear una configuración de IMS en AEM y generar la clave pública.

1. En AEM, abra el menú **Herramientas**.
1. En la sección **Seguridad** seleccione **Configuraciones de IMS de Adobe**.
1. Seleccione **Crear** para abrir la **Configuración de cuenta técnica de IMS de Adobe**.
1. Con el menú desplegable en **Configuración de nube**, seleccione **Adobe Target**.
1. Active **Crear nuevo certificado** e introduzca un nuevo alias.
1. Confirme con **Crear certificado**.

   ![](assets/integrate-target-io-01.png)

1. Seleccione **Descargar** (o **Descargar clave pública**) para descargar el archivo en la unidad local, de modo que esté listo para su uso cuando [configure la integración de Adobe I/O para Adobe Target con AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem).

   >[!CAUTION]
   >
   >Mantenga esta configuración abierta, será necesaria nuevamente cuando [complete la configuración de IMS en AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## Configuración de la integración de Adobe I/O para Adobe Target con AEM {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

Debe crear el proyecto de Adobe I/O (integración) con Adobe Target que AEM utilizar y, a continuación, asignar los privilegios necesarios.

### Creación del proyecto {#creating-the-project}

Abra la consola de Adobe I/O para crear un proyecto de E/S con Adobe Target que AEM:

>[!NOTE]
>
>Consulte también los [tutoriales de Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html).

1. Abra la consola de Adobe I/O para proyectos:

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. Se mostrarán todos los proyectos que tenga. Seleccione **Crear nuevo proyecto**: la ubicación y el uso dependerán de:

   * Si todavía no tiene ningún proyecto, **Crear nuevo proyecto** será central, inferior.
      ![Crear nuevo proyecto: primer proyecto](assets/integration-target-io-02.png)
   * Si ya tiene proyectos existentes, se enumerarán y **Crear nuevo proyecto** estará en la parte superior derecha.
      ![Crear nuevo proyecto - Varios proyectos](assets/integration-target-io-03.png)


1. Seleccione **Añadir al proyecto** seguido de **API**:

   ![](assets/integration-target-io-10.png)

1. Seleccione **Adobe Target** y luego **Siguiente**:

   >[!NOTE]
   >
   >Si está suscrito a Adobe Target, pero no lo ve en la lista, debe comprobar los [Requisitos previos](#prerequisites).

   ![](assets/integration-target-io-12.png)

1. **Cargue la clave** pública y, cuando termine, continúe con  **Siguiente**:

   ![](assets/integration-target-io-13.png)

1. Revise las credenciales y continúe con **Siguiente**:

   ![](assets/integration-target-io-15.png)

1. Seleccione los perfiles de producto necesarios y continúe con **Guardar API configurada**:

   >[!NOTE]
   >
   >Los perfiles del producto mostrados dependen de si tiene:
   >
   >* Adobe Target Standard: solo **Espacio de trabajo predeterminado** está disponible
   >* Adobe Target Premium: se muestran todos los espacios de trabajo disponibles, como se muestra a continuación


   ![](assets/integration-target-io-16.png)

1. Se confirmará la creación.

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### Asignación de privilegios a la integración {#assigning-privileges-to-the-integration}

Ahora debe asignar los privilegios necesarios a la integración:

1. Abra el Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Vaya a **Productos** (barra de herramientas superior) y, a continuación, seleccione **Adobe Target - &lt;*su-identificación-inquilina*>** (en el panel izquierdo).
1. Seleccione **Perfiles del producto** y, a continuación, el espacio de trabajo requerido de la lista presentada. Por ejemplo, Espacio de trabajo predeterminado.
1. Seleccione **Integraciones** y luego la configuración de integración requerida.
1. Seleccione **Editor** como la **Función del producto**; en lugar de **Observador**.

## Detalles almacenados para el proyecto de integración de Adobe I/O {#details-stored-for-the-adobe-io-integration-project}

Desde la consola Adobe I/O Projects puede ver una lista de todos los proyectos de integración:

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

Seleccione **Vista** (a la derecha de una entrada de proyecto específica) para mostrar más detalles sobre la configuración. Entre estas características se incluyen:

* Información general del proyecto
* Perspectivas
* Credenciales
   * Cuenta de servicio (JWT)
      * Detalles de credenciales
      * Generar JWT
* API
   * Por ejemplo, Adobe Target

Algunas de ellas deberán completar la integración de Adobe I/O para Destinatario en AEM.

## Cómo completar la configuración de IMS en AEM {#completing-the-ims-configuration-in-aem}

Si vuelve a AEM, puede completar la configuración de IMS agregando los valores necesarios de la integración de Adobe I/O para Destinatario:

1. Vuelva a la configuración [IMS abierta en AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Seleccione **Siguiente**.

1. Aquí puede utilizar los [detalles de Adobe I/O](#details-stored-for-the-adobe-io-integration-project):

   * **Título**: Tu texto.
   * **Servidor** de autorización: Copie o pegue esto desde la  `"aud"` línea de la sección  **** Carga útil siguiente, por ejemplo,  `"https://ims-na1.adobelogin.com"` en el ejemplo siguiente
   * **Clave** de API: Copie esto desde la  [](#details-stored-for-the-adobe-io-integration-project) sección Información general de la integración de Adobe I/O para Destinatario
   * **Secreto** del cliente: Genere esto en la  [](#details-stored-for-the-adobe-io-integration-project) sección Información general de la integración de Adobe I/O para Destinatario y copie
   * **Carga útil**: Copie esto desde la  [sección Generar ](#details-stored-for-the-adobe-io-integration-project) JWT de la integración de Adobe I/O para Destinatario

   ![](assets/integrate-target-io-10.png)

1. Confirme con **Crear**.

1. La configuración de Adobe Target se mostrará en la consola de AEM.

   ![](assets/integrate-target-io-11.png)

## Confirmación de la configuración de IMS {#confirming-the-ims-configuration}

Para confirmar que la configuración está funcionando según lo esperado:

1. Abra:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Por ejemplo:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Seleccione la configuración.
1. Seleccione **Comprobar estado** en la barra de herramientas, seguido de **Check**.

   ![](assets/integrate-target-io-12.png)

1. Si se realiza correctamente, verá el mensaje:

   ![](assets/integrate-target-io-13.png)

## Configuración del Cloud Service de Adobe Target {#configuring-the-adobe-target-cloud-service}

Ahora se puede hacer referencia a la configuración para que un Cloud Service utilice la API de Target Standard:

1. Abra el menú **Herramientas**. A continuación, en la sección **Cloud Services**, seleccione **Cloud Services heredados**.
1. Desplácese hacia abajo hasta **Adobe Target** y seleccione **Configurar ahora**.

   Se abrirá el cuadro de diálogo **Crear configuración**.

1. Escriba un **Título** y, si lo desea, un **Nombre** (si se deja en blanco, se generará a partir del título).

   También puede seleccionar la plantilla requerida (si hay más de una disponible).

1. Confirme con **Crear**.

   Se abrirá el cuadro de diálogo **Editar componente**.

1. Introduzca los detalles en la ficha **Configuración de Adobe Target**:

   * **Autenticación**: IMS
   * **ID** del inquilino: ID de inquilino de IMS de Adobe

      >[!NOTE]
      >
      >Para IMS, este valor debe tomarse del propio Destinatario. Puede iniciar sesión en Destinatario y extraer el ID del inquilino de la dirección URL.
      >
      >Por ejemplo, si la dirección URL es:
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >Luego usaría `yourtenantid`.

   * **Configuración** de IMS: seleccione el nombre de la configuración de IMS
   * **Tipo** de API: REST
   * **Configuración** de A4T Analytics Cloud: Seleccione la configuración de nube de Analytics que se utiliza para las métricas y los objetivos de actividad de destinatario. Esto es necesario si utiliza Adobe Analytics como fuente de sistema de informes al destinar contenido. Si no ve la configuración de nube, consulte la nota en [Configuración de A4T Analytics Cloud](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).
   * **Usar objetivos** precisos: De forma predeterminada, esta casilla de verificación está activada. Si se selecciona, la configuración del servicio en la nube esperará a que se cargue el contexto antes de cargar el contenido. Véase la nota siguiente.
   * **Sincronizar segmentos desde Adobe Target**: Seleccione esta opción para descargar los segmentos definidos en Destinatario y utilizarlos en AEM. Debe seleccionar esta opción cuando la propiedad Tipo de API sea REST, ya que los segmentos en línea no son compatibles y siempre debe utilizar segmentos de Destinatario. (Tenga en cuenta que el término AEM de &#39;segmento&#39; equivale al Destinatario &#39;audiencia&#39;).
   * **Biblioteca** de cliente: Seleccione si desea la biblioteca de cliente de AT.js o mbox.js (desaprobada).
   * **Utilice el sistema de administración de etiquetas para entregar la biblioteca** del cliente: Utilice DTM (desaprobada), Inicio de Adobe o cualquier otro sistema de administración de etiquetas.
   * **AT.js** personalizado: Deje en blanco si ha marcado la casilla Administración de etiquetas o si desea utilizar AT.js predeterminado. Como alternativa, cargue su AT.js personalizado. Solo aparece si ha seleccionado AT.js.

   >[!NOTE]
   >
   >[La configuración de un Cloud Service para utilizar la ](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) API de Destinatario Classic ha quedado obsoleta (utiliza la ficha Configuración de Adobe Recommendations).

   Por ejemplo:

   ![](assets/integrate-target-io-14.png)

1. Haga clic en **Conectar a Destinatario** para inicializar la conexión con Adobe Target.

   Si la conexión es correcta, se muestra el mensaje **Conexión correcta**.

1. Seleccione **Aceptar** en el mensaje, seguido de **Aceptar** en el cuadro de diálogo para confirmar la configuración.
1. Ahora puede proceder a [Añadir un Destinatario Framework](/help/sites-administering/target-configuring.md#adding-a-target-framework) para configurar los parámetros de ContextHub o ClientContext que se enviarán a Destinatario. Tenga en cuenta que esto puede no ser necesario para exportar fragmentos de experiencia AEM a Destinatario.

