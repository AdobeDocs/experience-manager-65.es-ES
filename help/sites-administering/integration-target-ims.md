---
title: Integración con Adobe Target mediante IMS
description: AEM Obtenga información acerca de la integración de la con Adobe Target mediante IMS
exl-id: 8ddd86d5-a5a9-4907-b07b-b6552d7afdc8
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 55%

---

# Integración con Adobe Target mediante IMS{#integration-with-adobe-target-using-ims}

AEM La integración de la con Adobe Target mediante la API de Target Standard requiere la configuración de Adobe IMS (Identity Management System) mediante la consola de Adobe Developer.

>[!NOTE]
>
>La compatibilidad con la API de Adobe Target AEM Standard es nueva en la versión 6.5 de. La API de Target Standard utiliza la autenticación IMS.
>
>El uso de la API de Adobe Target AEM Classic en la sigue siendo compatible con la compatibilidad con versiones anteriores. El [La API de Target Classic utiliza la autenticación de credenciales de usuario](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).
>
>La selección de la API se basa en el método de autenticación utilizado para la integración de AEM/Target.
>Consulte también la [ID de inquilino y código de cliente](#tenant-client) sección.

## Requisitos previos {#prerequisites}

Antes de iniciar este procedimiento:

* El [Soporte de Adobe](https://helpx.adobe.com/es/contact/enterprise-support.ec.html) debe aprovisionar su cuenta para lo siguiente:

   * Adobe Console
   * Adobe Developer Console
   * Adobe Target y
   * Adobe IMS (Identity Management System)

* El administrador del sistema de su organización debe utilizar el Admin Console para añadir los desarrolladores necesarios de su organización a los perfiles de producto relevantes.

   * Esto proporciona a los desarrolladores específicos permisos para habilitar integraciones en Adobe Developer Console.
   * Para obtener más información, consulte [Administración de desarrolladores](https://helpx.adobe.com/es/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configuración de IMS: generación de una clave pública {#configuring-an-ims-configuration-generating-a-public-key}

El primer paso de la configuración es crear una configuración de IMS en AEM y generar la clave pública.

1. En AEM, abra el menú **Herramientas**.
1. En la sección **Seguridad**, seleccione **Configuraciones de IMS de Adobe**.
1. Seleccione **Crear** para abrir la **Configuración de cuenta técnica de Adobe IMS**.
1. En la lista desplegable debajo de **Configuración de nube**, seleccione **Adobe Target**.
1. Active **Crear nuevo certificado** e introduzca un nuevo alias.
1. Confirme con **Crear certificado**.

   ![](assets/integrate-target-io-01.png)

1. Seleccione **Descargar** (o **Descargar clave pública**) para descargar el archivo en la unidad local, de modo que esté listo para usarse cuando [configure IMS para la integración de Adobe Target con AEM](#configuring-ims-for-adobe-target-integration-with-aem).

   >[!CAUTION]
   >
   >Mantenga esta configuración abierta, será necesaria de nuevo cuando [complete la configuración de IMS en AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## Configuración de IMS para la integración de Adobe Target con AEM {#configuring-ims-for-adobe-target-integration-with-aem}

Con la consola de Adobe Developer, debe crear un proyecto (integración) con Adobe Target AEM que vaya a utilizar y, a continuación, asignar los privilegios necesarios.

### Creación del proyecto {#creating-the-project}

Abra Adobe Developer Console para crear un proyecto con Adobe Target que utilizará AEM:

1. Abra Adobe Developer Console para proyectos:

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. Se mostrarán todos los proyectos que tenga. Seleccione **Crear nuevo proyecto**. La ubicación y el uso dependerán de lo siguiente:

   * Si todavía no tiene ningún proyecto, **Crear nuevo proyecto** estará en el centro, abajo.
      ![Creación de un nuevo proyecto: primer proyecto](assets/integration-target-io-02.png)
   * Si ya tiene proyectos, estos se enumerarán y **Crear nuevo proyecto** estará en la parte superior derecha.
      ![Creación de un nuevo proyecto: varios proyectos](assets/integration-target-io-03.png)


1. Seleccione **Añadir a proyecto** seguido de **API**:

   ![](assets/integration-target-io-10.png)

1. Seleccione **Adobe Target** y, luego, **Siguiente**:

   >[!NOTE]
   >
   >Si está suscrito a Adobe Target, pero no lo ve en la lista, debe comprobar el [Requisitos previos](#prerequisites).

   ![](assets/integration-target-io-12.png)

1. **Cargue la clave pública** y, cuando se complete, continúe con **Siguiente**:

   ![](assets/integration-target-io-13.png)

1. Revise las credenciales y continúe con **Siguiente**:

   ![](assets/integration-target-io-15.png)

1. Seleccione los perfiles de producto necesarios y continúe con **Guardar la API configurada**:

   >[!NOTE]
   >
   >Los perfiles de producto mostrados dependen de si tiene lo siguiente:
   >
   >* Adobe Target Standard: solo está disponible el **Espacio de trabajo predeterminado**
   >* Adobe Target Premium: se enumeran todos los espacios de trabajo disponibles, como se muestra a continuación


   ![](assets/integration-target-io-16.png)

1. La creación se confirmará.

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### Asignación de privilegios a la integración {#assigning-privileges-to-the-integration}

Ahora debe asignar los privilegios necesarios a la integración:

1. Abra la Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Vaya a **Productos** (barra de herramientas superior) y, a continuación, seleccione **Adobe Target - &lt;*your-tenant-id*>** (del panel izquierdo).
1. Seleccione **Perfiles de producto** y, a continuación, el espacio de trabajo necesario de la lista presentada. Por ejemplo, Espacio de trabajo predeterminado.
1. Seleccione **Credenciales de API** y la configuración de integración requerida.
1. Seleccione **Editor** como la **Función del producto**, en lugar de **Observador**.

## Detalles almacenados para el proyecto de integración de Adobe Developer Console {#details-stored-for-the-ims-integration-project}

Desde Adobe Developer Console y Proyectos, puede ver una lista de todos sus proyectos de integración:

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

Seleccione **Ver** (a la derecha de una entrada de proyecto específica) para mostrar más detalles acerca de la configuración. Entre estas características se incluyen:

* Información general del proyecto
* Perspectivas
* Credenciales
   * Cuenta de servicio (JWT)
      * Detalles de la credencial
      * Generar JWT
* API
   * Por ejemplo, Adobe Target

En algunos de estos casos, deberá completar la integración de Adobe Target en AEM según IMS.

## Finalización de la configuración de IMS en AEM {#completing-the-ims-configuration-in-aem}

AEM Al volver a la configuración de la consola de Adobe Developer para Target, puede completar la configuración de IMS añadiendo los valores necesarios:

1. Vuelva a la [Configuración de IMS abierta en AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Seleccione **Siguiente**.

1. Aquí puede usar los [detalles de la configuración del proyecto en Adobe Developer Console](#details-stored-for-the-ims-integration-project):

   * **Título**: el texto.
   * **Servidor de autorización**: copie/pegue esto desde la línea `aud` de la sección **Carga útil** a continuación, p. ej., `https://ims-na1.adobelogin.com` en el ejemplo siguiente
   * **Clave de API**: copie esto desde el [Información general](#details-stored-for-the-ims-integration-project) sección
   * **Secreto del cliente**: genere esto en la [Información general](#details-stored-for-the-ims-integration-project) sección, y copiar
   * **Carga útil**: copie esto desde la sección [Generar JWT](#details-stored-for-the-ims-integration-project)

   ![](assets/integrate-target-io-10.png)

1. Confirme con **Crear**.

1. La configuración de Adobe Target se mostrará en la consola de AEM.

   ![](assets/integrate-target-io-11.png)

## Confirmación de la configuración de IMS {#confirming-the-ims-configuration}

Para confirmar que la configuración funciona según lo esperado:

1. Abra:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Por ejemplo:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Seleccione la configuración.
1. Seleccione **Comprobar estado** en la barra de herramientas, seguido de **Comprobar**.

   ![](assets/integrate-target-io-12.png)

1. Si se ejecuta correctamente, verá el siguiente mensaje:

   ![](assets/integrate-target-io-13.png)

## Configuración del Cloud Service de Adobe Target {#configuring-the-adobe-target-cloud-service}

Ahora se puede hacer referencia a la configuración para que un Cloud Service utilice la API de Target Standard:

1. Abra el **Herramientas** menú. A continuación, dentro de **Cloud Services** , seleccione **Cloud Services heredados**.
1. Desplácese hacia abajo hasta **Adobe Target** y seleccione **Configurar ahora**.

   El **Crear configuración** se abrirá.

1. Introduzca una **Título** y, si lo desea, un **Nombre** (si se deja en blanco, se generará a partir del título).

   También puede seleccionar la plantilla requerida (si hay más de una disponible).

1. Confirme con **Crear**.

   El **Editar componente** se abrirá.

1. Introduzca los detalles en la **Configuración de Adobe Target** pestaña:

   * **Autenticación**: IMS

   * **ID de inquilino**: el ID del inquilino de Adobe IMS. Consulte también la [ID de inquilino y código de cliente](#tenant-client) sección.

      >[!NOTE]
      >
      >Para IMS, este valor debe tomarse del propio Target. Puede iniciar sesión en Target y extraer el ID de inquilino de la dirección URL.
      >
      >Por ejemplo, si la dirección URL es:
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >A continuación, debe utilizar `yourtenantid`.

   * **Código de cliente**: Consulte la [ID de inquilino y código de cliente](#tenant-client) sección.

   * **Configuración de IMS**: seleccione el nombre de la configuración de IMS

   * **Tipo de API**: REST

   * **Configuración de A4T Analytics Cloud**: Seleccione la configuración de Analytics Cloud que se utiliza para las métricas y los objetivos de las actividades de Target. Lo necesita si utiliza Adobe Analytics como fuente de informes al segmentar contenido. Si no ve la configuración de nube, consulte la nota en [Configuración de A4T Analytics Cloud](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).

   * **Usar objetivos precisos**: De forma predeterminada, esta casilla de verificación está seleccionada. Si se selecciona, la configuración del servicio en la nube esperará a que el contexto se cargue antes de cargar el contenido. Véase la nota siguiente.

   * **Sincronizar segmentos de Adobe Target** AEM : seleccione esta opción para descargar los segmentos definidos en Target y utilizarlos en las listas de segmentos de la lista de segmentos que se van a usar en la. Debe seleccionar esta opción cuando la propiedad Tipo de API sea REST, ya que los segmentos en línea no son compatibles y siempre necesita utilizar segmentos de Target. (Tenga en cuenta que el término de AEM de &quot;segmento&quot; equivale a la &quot;audiencia&quot; de Target).

   * **Biblioteca de cliente**: Seleccione si desea la biblioteca de cliente AT.js o mbox.js (obsoleto).

   * **Utilizar el sistema Tag Management para ofrecer la biblioteca de cliente**: utilice DTM (en desuso), Adobe Launch o cualquier otro sistema de administración de etiquetas.

   * **AT.js personalizado**: Déjelo en blanco si marcó la casilla Tag Management o para usar el AT.js predeterminado. También puede cargar su archivo AT.js personalizado. Solo aparece si ha seleccionado AT.js.
   >[!NOTE]
   >
   >[Configuración de un Cloud Service para utilizar la API de Target Classic](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) ha quedado obsoleto (utiliza la pestaña Configuración de Adobe Recommendations ).

1. Clic **Conectar con Target** para inicializar la conexión con Adobe Target.

   Si la conexión se realiza correctamente, aparecerá el mensaje **Conexión correcta.**

1. Seleccionar **OK** en el mensaje, seguido de **OK** en el cuadro de diálogo para confirmar la configuración.

1. Ahora puede continuar con [Agregar un marco de trabajo de Target](/help/sites-administering/target-configuring.md#adding-a-target-framework) para configurar ContextHub o los parámetros de ClientContext que se enviarán a Target. AEM Tenga en cuenta que esto puede no ser necesario para exportar fragmentos de experiencia de la a Target.

### ID de inquilino y código de cliente {#tenant-client}

Con [Adobe Experience Manager 6.5.8.0](/help/release-notes/release-notes.md), el campo Código de cliente se ha añadido a la ventana de configuración de Target.

Al configurar los campos ID de inquilino y Código de cliente, tenga en cuenta lo siguiente:

1. Para la mayoría de los clientes, el ID de inquilino y el código de cliente son los mismos. Esto significa que ambos campos contienen la misma información y son idénticos. Asegúrese de introducir el ID de inquilino en ambos campos.
2. Para fines heredados, también puede introducir valores diferentes en los campos ID de inquilino y Código de cliente.

En ambos casos, tenga en cuenta que:

* De forma predeterminada, el código de cliente (si se agrega primero) también se copia automáticamente en el campo ID de inquilino.
* Tiene la opción de cambiar el conjunto de ID de inquilino predeterminado.
* En consecuencia, las llamadas de servidor a Target se basarán en el ID de inquilino y las llamadas del lado del cliente a Target se basarán en el código del cliente.

AEM Como se ha indicado anteriormente, el primer caso es el más común para la versión 6.5 de la. De cualquier manera, asegúrate **ambos** Los campos contienen la información correcta según sus necesidades.

>[!NOTE]
>
>Si desea cambiar una configuración de Target existente:
>
>1. Vuelva a introducir el ID de inquilino.
>2. Volver a conectar con Target.
>3. Guarde la configuración.

