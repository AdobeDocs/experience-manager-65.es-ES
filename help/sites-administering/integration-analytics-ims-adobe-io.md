---
title: Integración con Adobe Analytics mediante Adobe I/O
description: Obtenga información sobre la integración de AEM con Adobe Analytics mediante Adobe I/O
source-git-commit: c2c7c3f745a5f1edc1a8d2a73922f86f0b952ff7
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 1%

---

# Integración con Adobe Analytics mediante Adobe I/O {#integration-with-adobe-analytics-using-adobe-i-o}

La integración de AEM con Adobe Analytics mediante la API de Analytics Standard requiere la configuración de Adobe IMS (Identity Management System) y Adobe I/O.

>[!NOTE]
>
>La compatibilidad con la API de Adobe Analytics Standard 2.0 es nueva en AEM 6.5.12.0. Esta versión de la API admite la autenticación IMS.
>
>El uso de la API 1.4 de Adobe Analytics Classic en AEM sigue siendo compatible con versiones anteriores. La variable [La API de Analytics Classic utiliza la autenticación de credenciales de usuario](/help/sites-administering/adobeanalytics-connect.md).
>
>La selección de la API se basa en el método de autenticación utilizado para la integración de AEM/Analytics.
>
>También puede obtenerse más información en [Migración a las API 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/).

## Requisitos previos {#prerequisites}

Antes de iniciar este procedimiento:

* [Compatibilidad con Adobe](https://helpx.adobe.com/es/contact/enterprise-support.ec.html) debe aprovisionar su cuenta para:

   * Consola Adobe
   * Adobe I/O
   * Adobe Analytics y
   * Adobe IMS (sistema Identity Management)

* El administrador del sistema de su organización debe utilizar el Admin Console para agregar los desarrolladores necesarios de su organización a los perfiles de producto relevantes.

   * Esto proporciona a los desarrolladores específicos permisos para habilitar integraciones dentro de Adobe I/O.
   * Para obtener más información, consulte [Administrar desarrolladores](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configuración de IMS: generación de una clave pública {#configuring-an-ims-configuration-generating-a-public-key}

El primer paso de la configuración es crear una configuración de IMS en AEM y generar la clave pública.

1. En AEM, abra el **Herramientas** para abrir el Navegador.
1. En el **Seguridad** sección seleccionar **Configuraciones de IMS de Adobe**.
1. Select **Crear** para abrir el **Configuración de cuenta técnica de Adobe IMS**.
1. Uso de la lista desplegable debajo de **Configuración de nube**, seleccione **Adobe Analytics**.
1. Activar **Crear nuevo certificado** e introduzca un nuevo alias.
1. Confirme con **Crear certificado**.

   ![](assets/integrate-analytics-io-01.png)

1. Select **Descargar** (o **Descargar clave pública**) para descargar el archivo en la unidad local, de modo que esté listo para usar cuando [configuración de Adobe I/O para la integración de Adobe Analytics con AEM](#configuring-adobe-i-o-for-adobe-analytics-integration-with-aem).

   >[!CAUTION]
   >
   >Mantenga esta configuración abierta, será necesaria de nuevo cuando [Finalización de la configuración de IMS en AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-analytics-io-02.png)

## Configuración del Adobe I/O para la integración de Adobe Analytics con AEM {#configuring-adobe-i-o-for-adobe-analytics-integration-with-aem}

Debe crear el proyecto de Adobe I/O (integración) con Adobe Analytics que AEM utilizará y, a continuación, asignar los privilegios necesarios.

### Creación del proyecto {#creating-the-project}

Abra la consola Adobe I/O para crear un proyecto de E/S con Adobe Target que AEM usar:

<!--
>[!NOTE]
>
>See also the [Adobe I/O tutorials](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html).
-->

1. Abra la consola Adobe I/O para proyectos:

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. Se mostrarán todos los proyectos que tenga. Select **Crear nuevo proyecto** - la ubicación y el uso dependerán de:

   * Si todavía no tiene ningún proyecto, **Crear nuevo proyecto** estará en el centro, abajo.
      ![Crear nuevo proyecto: primer proyecto](assets/integration-analytics-io-02.png)
   * Si ya tiene proyectos existentes, estos se enumerarán y **Crear nuevo proyecto** estará en la parte superior derecha.
      ![Crear nuevo proyecto: varios proyectos](assets/integration-analytics-io-03.png)


1. Select **Agregar a proyecto** seguido de **API**:

   ![Introducción a su nuevo proyecto](assets/integration-analytics-io-10.png)

1. Select **Adobe Analytics**, luego **Siguiente**:

   >[!NOTE]
   >
   >Si está suscrito a Adobe Analytics, pero no lo ve en la lista, debe comprobar la variable [Requisitos previos](#prerequisites).

   ![Añadir una API](assets/integration-analytics-io-12.png)

1. Select **Cuenta de servicio (JWT)** como tipo de autenticación, continúe con **Siguiente**:

   ![Seleccionar tipo de autenticación](assets/integration-analytics-io-12a.png)

1. **Cargar la clave pública** y, cuando se complete, continúe con **Siguiente**:

   ![Cargar la clave pública](assets/integration-analytics-io-13.png)

1. Revise las credenciales y continúe con **Siguiente**:

   ![Revisar credenciales](assets/integration-analytics-io-15.png)

1. Seleccione los perfiles de producto necesarios y continúe con **Guardar la API configurada**:

   >[!NOTE]
   >
   >Los perfiles de producto mostrados con dependen de si tiene:
   >
   >* Adobe Target Standard: solo **Espacio de trabajo predeterminado** está disponible
   >* Adobe Target Premium : se enumeran todos los espacios de trabajo disponibles, como se muestra a continuación


   ![Seleccionar perfiles de producto necesarios](assets/integration-analytics-io-16.png)

1. La configuración se confirmará.

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### Asignación de privilegios a la integración {#assigning-privileges-to-the-integration}

Ahora debe asignar los privilegios necesarios a la integración:

1. Abra el Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Vaya a **Productos** (barra de herramientas superior) y, a continuación, seleccione **Adobe Analytics: &lt;*your-tenant-id*>** (del panel izquierdo).
1. Select **Perfiles de producto** y, a continuación, el espacio de trabajo necesario de la lista presentada. Por ejemplo, Espacio de trabajo predeterminado.
1. Select **Credenciales de API**, luego la configuración de integración requerida.
1. Select **Editor** como el **Función del producto**; en lugar de **Observador**.

## Detalles almacenados para el proyecto de integración de Adobe I/O {#details-stored-for-the-adobe-io-integration-project}

Desde la consola Proyectos de Adobe I/O puede ver una lista de todos sus proyectos de integración:

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

Seleccione una entrada de proyecto específica para mostrar más detalles sobre la configuración. Entre estas características se incluyen:

* Información general del proyecto
* Perspectivas
* Credenciales
   * Cuenta de servicio (JWT)
      * Detalles de la credencial
      * Generar JWT
* API
   * Por ejemplo, Adobe Analytics

En algunos de estos casos, deberá completar la integración de Adobe I/O para Adobe Analytics en AEM.

## Finalización de la configuración de IMS en AEM {#completing-the-ims-configuration-in-aem}

Al volver a AEM puede completar la configuración de IMS añadiendo los valores necesarios desde la integración de Adobe I/O para Target:

1. Vuelva a la [Configuración de IMS abierta en AEM](#configuring-an-ims-configuration-generating-a-public-key).
1. Seleccione **Siguiente**.

1. Aquí puede usar la variable [detalles de la configuración del proyecto en Adobe I/O](#details-stored-for-the-adobe-io-integration-project):

   * **Título**: El texto.
   * **Servidor de autorización**: Copie/pegue esto desde el `aud` línea del **Carga útil** a continuación, p. ej. `https://ims-na1.adobelogin.com` en el ejemplo siguiente
   * **Clave de API**: Copie esto desde el **Credenciales** de la sección [Información general del proyecto](#details-stored-for-the-adobe-io-integration-project)
   * **Secreto del cliente**: Genere esto en el [Pestaña Secreto del cliente de la sección Cuenta de servicio (JWT)](#details-stored-for-the-adobe-io-integration-project)y copie
   * **Carga útil**: Copie esto desde el [Ficha Generar JWT de la sección Cuenta de servicio (JWT)](#details-stored-for-the-adobe-io-integration-project)

   ![AEM detalles de configuración de IMS](assets/integrate-analytics-io-10.png)

1. Confirme con **Crear**.

1. La configuración de Adobe Target se mostrará en la consola AEM.

   ![Configuración de IMS](assets/integrate-analytics-io-11.png)

## Confirmación de la configuración de IMS {#confirming-the-ims-configuration}

Para confirmar que la configuración funciona según lo esperado:

1. Abra:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Por ejemplo:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Seleccione la configuración.
1. Select **Comprobar estado** en la barra de herramientas, seguido de **Marque**.

   ![Configuración de IMS - Comprobar estado](assets/integrate-analytics-io-12.png)

1. Si se realiza correctamente, verá un mensaje de confirmación.

   <!--
   ![](assets/integrate-target-io-13.png)
   -->

## Configuración del servicio Adobe Analytics Cloud {#configuring-the-adobe-analytics-cloud-service}

Ahora se puede hacer referencia a la configuración para que un Cloud Service utilice la API de Analytics Standard:

1. Abra el **Herramientas** para abrir el Navegador. A continuación, dentro de la función **Cloud Services** , seleccione **Cloud Services heredados**.
1. Desplácese hacia abajo hasta **Adobe Analytics** y seleccione **Configurar ahora**.

   La variable **Crear configuración** se abrirá.

1. Escriba un **Título** y, si lo desea, una **Nombre** (si se deja en blanco, esto se generará a partir del título).

   También puede seleccionar la plantilla necesaria (si hay más de una disponible).

1. Confirme con **Crear**.

   La variable **Editar componente** se abrirá.

1. Introduzca los detalles en la **Configuración de análisis** pestaña:

   * **Autenticación**: IMS

   * **Configuración de IMS**: seleccione el nombre de la configuración de IMS

1. Haga clic en **Conectarse a Analytics** para inicializar la conexión con Adobe Target.

   Si la conexión se realiza correctamente, aparecerá el mensaje **Conexión correcta** se muestra.

1. Select **OK** en el mensaje.

1. Complete otros parámetros según sea necesario, seguido de **OK** en el cuadro de diálogo para confirmar la configuración.

1. Ahora puede continuar con [Adición de un marco de Analytics](/help/sites-administering/adobeanalytics-connect.md) para configurar los parámetros que se enviarán a Adobe Analytics.
