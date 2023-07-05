---
title: Integración con Adobe Analytics mediante IMS
description: AEM Obtenga información acerca de la integración de la con Adobe Analytics mediante IMS
exl-id: 2833a6df-ef32-48ab-8395-0f26816f8443
source-git-commit: 5789954afea2d42444b6f6f9f185d7926624e7f0
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 65%

---


# Integración con Adobe Analytics mediante IMS {#integration-with-adobe-analytics-using-ims}

AEM La integración de la con Adobe Analytics mediante la API de Analytics Standard requiere la configuración de Adobe IMS (Identity Management System) mediante la consola de Adobe Developer.

>[!NOTE]
>
>La compatibilidad con la API de Adobe Analytics Standard AEM 2.0 es nueva en la versión 6.5.12.0 de. Esta versión de la API admite la autenticación IMS.
>
>El uso de la API de Adobe Analytics AEM Classic 1.4 en el modo de la aplicación sigue siendo compatible con la compatibilidad con versiones anteriores. El [La API de Analytics Classic utiliza la autenticación de credenciales de usuario](/help/sites-administering/adobeanalytics-connect.md).
>
>La selección de la API se basa en el método de autenticación utilizado para la integración de AEM/Analytics.
>
>También puede obtenerse más información en [Migración a las API 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/).

## Requisitos previos {#prerequisites}

Antes de iniciar este procedimiento:

* El [Soporte de Adobe](https://helpx.adobe.com/es/contact/enterprise-support.ec.html) debe aprovisionar su cuenta para lo siguiente:

   * Adobe Console
   * Adobe Developer Console
   * Adobe Analytics y
   * Adobe IMS (Identity Management System)

* El administrador del sistema de su organización debe utilizar el Admin Console para añadir los desarrolladores necesarios de su organización a los perfiles de producto relevantes.

   * Esto proporciona a los desarrolladores específicos permisos para habilitar integraciones en Adobe Developer Console.
   * Para obtener más información, consulte [Administración de desarrolladores](https://helpx.adobe.com/es/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configuración de IMS: generación de una clave pública {#configuring-an-ims-configuration-generating-a-public-key}

El primer paso de la configuración es crear una configuración de IMS en AEM y generar la clave pública.

1. En AEM, abra el menú **Herramientas**.
1. En la sección **Seguridad**, seleccione **Configuraciones de IMS de Adobe**.
1. Seleccione **Crear** para abrir la **Configuración de cuenta técnica de Adobe IMS**.
1. En la lista desplegable debajo de **Configuración de nube**, seleccione **Adobe Analytics**.
1. Active **Crear nuevo certificado** e introduzca un nuevo alias.
1. Confirme con **Crear certificado**.

   ![Asistente de configuración de cuenta técnica de IMS de Adobe](assets/integrate-analytics-io-01.png)

1. Seleccione **Descargar** (o **Descargar clave pública**) para descargar el archivo en la unidad local, de modo que esté listo para usarse cuando [configure IMS para la integración de Adobe Analytics con AEM](#configuring-ims-for-adobe-analytics-integration-with-aem).

   >[!CAUTION]
   >
   >Mantenga esta configuración abierta, será necesaria de nuevo cuando [complete la configuración de IMS en AEM](#completing-the-ims-configuration-in-aem).

   ![Cuadro de diálogo de información para añadir la clave al Adobe I/O](assets/integrate-analytics-io-02.png)

## Configuración de IMS para la integración de Adobe Analytics con AEM {#configuring-ims-for-adobe-analytics-integration-with-aem}

Con Adobe Developer Console, debe crear un proyecto (integración) con Adobe Analytics (para que lo use AEM) y, a continuación, asignar los privilegios necesarios.

### Creación del proyecto {#creating-the-project}

Abra Adobe Developer Console para crear un proyecto con Adobe Analytics que usará AEM:

1. Abra Adobe Developer Console para proyectos:

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. Se mostrarán todos los proyectos que tenga. Seleccione **Crear nuevo proyecto**. La ubicación y el uso dependerán de lo siguiente:

   * Si todavía no tiene ningún proyecto, **Crear nuevo proyecto** estará en el centro, abajo.
     ![Creación de un nuevo proyecto: primer proyecto](assets/integration-analytics-io-02.png)
   * Si ya tiene proyectos, estos se enumerarán y **Crear nuevo proyecto** estará en la parte superior derecha.
     ![Creación de un nuevo proyecto: varios proyectos](assets/integration-analytics-io-03.png)


1. Seleccione **Añadir a proyecto** seguido de **API**:

   ![Introducción a su nuevo proyecto](assets/integration-analytics-io-10.png)

1. Seleccione **Adobe Analytics** y, luego, **Siguiente**:

   >[!NOTE]
   >
   >Si está suscrito a Adobe Analytics, pero no lo ve en la lista, debe comprobar el [Requisitos previos](#prerequisites).

   ![Añada una API](assets/integration-analytics-io-12.png)

1. Seleccione **Cuenta de servicio (JWT)** como tipo de autenticación y continúe con **Siguiente**:

   ![Seleccione el tipo de autenticación](assets/integration-analytics-io-12a.png)

1. **Cargue la clave pública** y, cuando se complete, continúe con **Siguiente**:

   ![Cargar la clave pública](assets/integration-analytics-io-13.png)

1. Revise las credenciales y continúe con **Siguiente**:

   ![Revisar credenciales](assets/integration-analytics-io-15.png)

1. Seleccione los perfiles de producto necesarios y continúe con **Guardar la API configurada**:

   ![Seleccionar perfiles de producto necesarios](assets/integration-analytics-io-16.png)

1. La configuración se confirmará.

### Asignación de privilegios a la integración {#assigning-privileges-to-the-integration}

Ahora debe asignar los privilegios necesarios a la integración:

1. Abra la Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Vaya a **Productos** (barra de herramientas superior) y, a continuación, seleccione **Adobe Analytics: &lt;*your-tenant-id*>** (del panel izquierdo).
1. Seleccione **Perfiles de producto** y, a continuación, el espacio de trabajo necesario de la lista presentada. Por ejemplo, Espacio de trabajo predeterminado.
1. Seleccione **Credenciales de API** y la configuración de integración requerida.
1. Seleccione **Editor** como la **Función del producto**, en lugar de **Observador**.

## Detalles almacenados para el proyecto de integración de Adobe Developer Console {#details-stored-for-the-ims-integration-project}

Desde la consola Proyectos de Adobe Developer puede ver una lista de todos sus proyectos de integración:

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

Seleccione una entrada de proyecto específica para mostrar más detalles acerca de la configuración. Entre estas características se incluyen:

* Información general del proyecto
* Perspectivas
* Credenciales
   * Cuenta de servicio (JWT)
      * Detalles de la credencial
      * Generar JWT
* API
   * Por ejemplo, Adobe Analytics

En algunos de estos casos, deberá completar la integración de Adobe Analytics AEM en el entorno de la.

## Finalización de la configuración de IMS en AEM {#completing-the-ims-configuration-in-aem}

AEM Al volver a la configuración de IMS, puede añadir los valores necesarios desde el proyecto de integración para Analytics:

1. Vuelva a la [Configuración de IMS abierta en AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Seleccione **Siguiente**.

1. Aquí puede usar la variable [Detalles almacenados para el proyecto de integración de la consola de Adobe Developer](#details-stored-for-the-ims-integration-project):

   * **Título**: el texto.
   * **Servidor de autorización**: copie/pegue esto desde la línea `aud` de la sección **Carga útil** a continuación, p. ej., `https://ims-na1.adobelogin.com` en el ejemplo siguiente
   * **Clave de API**: copie esto desde la sección **Credenciales** de la [Información general del proyecto](#details-stored-for-the-ims-integration-project)
   * **Secreto del cliente**: genere esto en la [pestaña Secreto del cliente de la sección Cuenta de servicio (JWT)](#details-stored-for-the-ims-integration-project) y copie
   * **Carga útil**: copie esto desde la [pestaña Generar JWT de la sección Cuenta de servicio (JWT)](#details-stored-for-the-ims-integration-project)

   ![Detalles de configuración de IMS de AEM](assets/integrate-analytics-io-10.png)

1. Confirme con **Crear**.

1. La configuración de Adobe Analytics se mostrará en la consola de AEM.

   ![Configuración de IMS](assets/integrate-analytics-io-11.png)

## Confirmación de la configuración de IMS {#confirming-the-ims-configuration}

Para confirmar que la configuración funciona según lo esperado:

1. Abra:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Por ejemplo:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`

1. Seleccione la configuración.
1. Seleccione **Comprobar estado** en la barra de herramientas, seguido de **Comprobar**.

   ![Configuración de IMS: Comprobar estado](assets/integrate-analytics-io-12.png)

1. Si se ejecuta correctamente, verá un mensaje de confirmación.

## Configuración del servicio de Adobe Analytics Cloud {#configuring-the-adobe-analytics-cloud-service}

Ahora se puede hacer referencia a la configuración para que un Cloud Service utilice la API de Analytics Standard:

1. Abra el **Herramientas** menú. A continuación, dentro de **Cloud Services** , seleccione **Cloud Services heredados**.
1. Desplácese hacia abajo hasta **Adobe Analytics** y seleccione **Configurar ahora**.

   El **Crear configuración** se abrirá.

1. Introduzca una **Título** y, si lo desea, un **Nombre** (si se deja en blanco, se generará a partir del título).

   También puede seleccionar la plantilla requerida (si hay más de una disponible).

1. Confirme con **Crear**.

   El **Editar componente** se abrirá.

1. Introduzca los detalles en la **Configuración de Analytics** pestaña:

   * **Autenticación**: IMS

   * **Configuración de IMS**: seleccione el nombre de la configuración de IMS

1. Clic **Conectar con Analytics** para inicializar la conexión con Adobe Analytics.

   Si la conexión se realiza correctamente, aparecerá el mensaje **Conexión correcta.**

1. Seleccionar **OK** en el mensaje.

1. Complete otros parámetros según sea necesario, seguidos de **OK** en el cuadro de diálogo para confirmar la configuración.

1. Ahora puede continuar con [Adición de un marco de Analytics](/help/sites-administering/adobeanalytics-connect.md) para configurar los parámetros que se enviarán a Adobe Analytics.
