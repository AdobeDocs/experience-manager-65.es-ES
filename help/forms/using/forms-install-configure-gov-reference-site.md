---
title: Configurar y configurar el sitio de referencia de We.Gov
seo-title: Configurar y configurar el sitio de referencia de We.Gov
description: Instale, configure y personalice un paquete de demostración de AEM Forms.
seo-description: Instale, configure y personalice un paquete de demostración de AEM Forms.
uuid: 0a6ad8f9-0d38-40c3-ad8d-e705edef55f8
contentOwner: anujkapo
discoiquuid: fe5da0aa-d3a8-4b77-a447-9e429fdc2816
docset: aem65
translation-type: tm+mt
source-git-commit: 33f73225fbb2c48353c1f34db3339c0bb79d4236

---


# Configurar y configurar el sitio de referencia de We.Gov{#set-up-and-configure-we-gov-reference-site}

## Detalles del paquete de demostración {#demo-package-details}

### Requisitos previos de instalación {#installation-prerequisites}

Este paquete se creó para **AEM Forms 6.4 OSGI Author**, se ha probado y, por tanto, se admite en las siguientes versiones de plataforma:

| VERSIÓN DE AEM | VERSIÓN DEL PAQUETE DE AEM FORMS | ESTADO |
|---|---|---|
| 6.4 | 5.0.86 | **Admitido** |
| 6.5 | 6.0.80 | **Admitido** |

Este paquete contiene la configuración de nube que admite las siguientes versiones de plataforma:

| PROVEEDOR DE NUBE | VERSIÓN DE SERVICIO | ESTADO |
|---|---|---|
| Adobe Sign | API v5 | **Admitido** |
| Microsoft Dynamics 365 | 1710 (9.1.0.3020) | **Admitido** |

**Consideraciones sobre la instalación del paquete:**

* Se espera que el paquete se instale en un servidor limpio, libre de otros paquetes de demostración o versiones de paquetes de demostración anteriores
* Se espera que el paquete se instale en un servidor OSGI, que se ejecuta en modo Autor

### ¿Qué incluye este paquete? {#what-does-this-package-include}

El paquete de demostración de AEM Forms We.Gov ( **we-gov-forms.pkg.all-&lt;version>.zip **) se incluye en un paquete que incluye otros subpaquetes y servicios. El paquete incluye los siguientes módulos:

* **we-gov-forms.pkg.all-&lt;version>.zip** -* Paquete completo de demostración*

   * **we-gov-forms.ui.apps-&lt;version>.zip** *- Contiene todos los componentes, bibliotecas de clientes, usuarios de muestras, modelos de flujo de trabajo, etc.*

      * **we-gov-forms.core-&lt;version>.jar*** - Contiene todos los servicios OSGI, implementación de pasos personalizados del flujo de trabajo, etc.*

      * **core.wcm.components.all-2.0.4.zip** : *colección de componentes WCM de muestra*

      * **grid-aem.ui.apps-1.0-SNAPSHOT.zip** - Paquete de diseño de cuadrícula de sitios *AEM para el control de columnas de páginas Sitios*
   * **we-gov-forms.ui.content-&lt;version>.zip***: contiene todo el contenido, las páginas, las imágenes, los *formularios, los recursos de comunicación interactivos, etc.

   * **we-gov-forms.config.public-&lt;version>.zip** : *contiene todos los nodos de configuración predeterminados, incluidas las configuraciones de nube de marcadores de posición, para ayudar a evitar problemas con el modelo de datos de formularios y el enlace de servicios.*


Los recursos incluidos en este paquete incluyen:

* Páginas de sitio de AEM con plantillas editables
* Formularios adaptables de AEM Forms
* Comunicaciones interactivas de AEM Forms (canal web e impresión)
* Documento XDP de AEM Forms de registro
* Modelo de datos de AEM Forms MS Dynamics Forms
* Integración de Adobe Sign
* Modelo de flujo de trabajo de AEM
* Imágenes de muestra de Recursos AEM

## Opciones de configuración {#configuration-options}

Esta sección incluye detalles sobre las opciones de configuración. En este momento, esta sección está intencionalmente vacía.

## Instalación del paquete de demostración {#demo-package-installation}

Esta sección contiene información sobre la instalación del paquete de demostración.

### Desde paquete compartido {#from-package-share}

1. Vaya a *https://&lt;aemserver>:&lt;port>/crx/packageshare/*

   O bien, en AEM, haga clic en Implementación y vaya al icono Uso compartido de paquetes.

   ![Icono de Package Share](assets/package_share_icon.jpg)

1. Inicie sesión con su Adobe ID.
1. Busque el paquete **we-gov-forms.pkg.all-&lt;version>** .
1. Seleccione la opción &quot;Descargar&quot; y acepte los términos y condiciones.
1. Una vez descargado, seleccione la opción &quot;Descargado&quot; para localizar el paquete en el Administrador de paquetes.
1. Seleccione la opción &quot;Instalar&quot; para instalar el paquete.

   ![paquete de formularios .gov](assets/wegov_forms_package.jpg)

1. Permita que se complete el proceso de instalación.
1. Vaya a *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html?wcmmode=disabled* para asegurarse de que la instalación se realizó correctamente.

### Desde un archivo ZIP local {#from-a-local-zip-file}

1. Descargue y localice el archivo **we-gov-forms.pkg.all-&lt;version>.zip** .
1. Vaya a *https://&lt;aemserver>:&lt;puerto>/crx/packmgr/index.jsp*.
1. Seleccione la opción &quot;Cargar paquete&quot;.

   ![Opción Cargar paquete](assets/upload_package.jpg)

1. Utilice el navegador de archivos para desplazarse hasta el archivo ZIP descargado y seleccionarlo.
1. Haga clic en &quot;Abrir&quot; para cargar.
1. Una vez cargado, seleccione la opción &quot;Instalar&quot; para instalar el paquete.

   ![Instalar el paquete de formularios WeGov](assets/wegov_forms_package-1.jpg)

1. Permita que se complete el proceso de instalación.
1. Vaya a *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html?wcmmode=disabled* para asegurarse de que la instalación se realizó correctamente.

### Instalación de nuevas versiones de paquetes {#installing-new-package-versions}

Para instalar la nueva versión del paquete, siga los pasos definidos en 4.1 y 4.2. Es posible instalar una versión más reciente del paquete mientras ya hay otro paquete más antiguo instalado, pero se recomienda desinstalar primero la versión anterior del paquete. Para hacerlo, siga los pasos a continuación.

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/crx/packmgr/index.jsp*
1. Busque el archivo **we-gov-forms.pkg.all-&lt;version>.zip** anterior.
1. Seleccione la opción &quot;Más&quot;.
1. En el menú desplegable, seleccione la opción &quot;Desinstalar&quot;.

   ![Desinstalar el paquete WeGov](assets/uninstall_wegov_forms_package.jpg)

1. En la confirmación, seleccione &quot;Desinstalar&quot; nuevamente y permita que se complete el proceso de desinstalación.

## Configuración del paquete de demostración {#demo-package-configuration}

Esta sección contiene detalles e instrucciones sobre la configuración posterior a la implementación del paquete de demostración antes de la presentación.

### Configuración ficticia del usuario {#fictional-user-configuration}

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/libs/granite/security/content/groupadmin.html*
1. Busque &quot;**workflow**&quot;.
1. Seleccione el grupo &quot;usuarios **del** flujo de trabajo&quot; y haga clic en &quot;Propiedades&quot;.
1. Vaya a la ficha &quot;Miembros&quot;.
1. Escriba **wegov** en el campo &quot;Seleccionar usuario o grupo&quot;.
1. Seleccione en el menú desplegable &quot;Usuarios **del formulario** We.Gov&quot;.

   ![Edición de la configuración de grupo para usuarios de flujo de trabajo](assets/edit_group_settings.jpg)

1. Haga clic en &quot;Guardar y cerrar&quot; en la barra de menús.
1. Repita los pasos del 2 al 7 buscando &quot;**análisis**&quot;, seleccionando el grupo &quot;Administradores **de** Analytics&quot; y agregando el grupo &quot;Usuarios **de formulario** We.Gov&quot; como miembro.
1. Repita los pasos del 2 al 7 buscando &quot;usuarios **de** formularios&quot;, seleccionando el grupo &quot;usuarios **de** formularios&quot; y agregando el grupo &quot;Usuarios **de formularios de** We.Gov&quot; como miembro.
1. Repita los pasos del 2 al 7 buscando &quot;usuarios **de** formularios&quot;, seleccionando el grupo &quot;usuarios **de** formularios&quot; y agregando esta vez el grupo &quot;** Usuarios de We.Gov**&quot; como miembro.

### Configuración del servidor de correo electrónico {#email-server-configuration}

1. Revisar la documentación de configuración [Configurar notificación por correo electrónico](/help/sites-administering/notification.md)

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/system/console/configMgr*
1. Busque y haga clic en el **servicio de correo de CQ **Day para configurarlo.

   ![Configurar el servicio de correo CQ Day](assets/day_cq_mail_service.jpg)

1. Configure el servicio para conectarse al servidor SMTP de su elección:

   1. **Nombre de host** del servidor SMTP: e.g (smtp.gmail.com)
   1. **Puerto** del servidor: por ejemplo (465) para gmail usando SSL
   1. **** Usuario SMTP: demo@ &lt;nombre_empresa>.com
   1. **Dirección**&quot;De&quot;: aemformsdemo@adobe.com
   ![Configurar SMTP](assets/configure_smtp.jpg)

1. Haga clic en &quot;Guardar&quot; para guardar la configuración.

### Configuración de AEM SSL {#aemsslconfig}

Esta sección contiene detalles sobre la configuración de SSL en la instancia de AEM para poder configurar la configuración de Adobe Sign Cloud.

**Referencias:**

1. [SSL de forma predeterminada](/help/sites-administering/ssl-by-default.md)

**Notas:**

1. Vaya a https://&lt;aemserver>:&lt;port>/aem/inbox donde podrá completar el proceso explicado en el vínculo de documentación de referencia anterior.
1. El paquete **we-gov-forms.pkg.all-&lt;version>.zip** incluye una clave SSL de muestra y un certificado al que se puede acceder extrayendo la carpeta **we-gov-forms.pkg.all-&lt;version>.zip/ssl** que forma parte del paquete.

1. Certificado SSL y detalles de clave:

   1. emitido a &quot;CN=localhost&quot;
   1. 10 años de validez
   1. valor de contraseña de &quot;password&quot;

### Adobe Sign cloud configuration {#adobe-sign-cloud-configuration}

Esta sección contiene detalles e instrucciones sobre la configuración de Adobe Sign Cloud.

**Referencias:**

1. [Integración de Adobe Sign con AEM Forms](adobe-sign-integration-adaptive-forms.md)

#### Cloud configuration {#cloud-configuration}

1. **Revise los requisitos previos. Consulte Configuración[SSL de](../../forms/using/forms-install-configure-gov-reference-site.md#aemsslconfig)AEM para obtener la configuración SSL necesaria.**
1. Ir a:

   *https://&lt;aemserver>:&lt;puerto>/libs/adobesign/cloudservices/adobesign.html/conf/we-gov*

   >[!NOTE]
   >
   >La dirección URL utilizada para acceder al servidor AEM debe coincidir con la URL configurada en el URI de redirección de OAuth de Adobe Sign para evitar problemas de configuración (por ejemplo, *https://&lt;aemserver>:&lt;puerto>/mnt/overlay/adobesign/cloudservices/adobesign/properties.html*)

1. Seleccione la configuración &quot;We.gov Adobe Sign&quot;.
1. Haga clic en &quot;Propiedades&quot;.
1. Vaya a la ficha &quot;Configuración&quot;.
1. Escriba la dirección URL de oAuth, por ejemplo: [https://secure.na1.echosign.com/public/oauth](https://secure.na1.echosign.com/public/oauth)
1. Proporcione el ID de cliente y el secreto de cliente configurados de la instancia de Adobe Sign configurada.
1. Haga clic en &quot;Conectar con Adobe Sign&quot;.
1. Después de una conexión correcta, haga clic en &quot;Guardar y cerrar&quot; para completar la integración.

### Configuración de nube de MS Dynamics {#ms-dynamics-cloud-configuration}

Esta sección contiene detalles e instrucciones sobre la configuración de MS Dynamics Cloud.

**Referencias:**

1. [Configuración de OData de Microsoft Dynamics](https://docs.adobe.com/content/help/en/experience-manager-64/forms/form-data-model/ms-dynamics-odata-configuration.html)
1. [Configuración de Microsoft Dynamics para AEM Forms](https://helpx.adobe.com/experience-manager/kt/forms/using/config-dynamics-for-aem-forms.html)

#### Servicio de nube MS Dynamics OData {#ms-dynamics-odata-cloud-service}

1. Ir a:

   https://&lt;aemserver>:&lt;puerto>/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html/conf/we-gov

   1. Asegúrese de que está accediendo al servidor utilizando la misma dirección URL de redireccionamiento configurada en el registro de la aplicación de MS Dynamics.

1. Seleccione la configuración &quot;Servicio de nube de OData de Microsoft Dynamics&quot;.
1. Haga clic en &quot;Propiedades&quot;.

   ![Propiedades del servicio de nube de OData de Microsoft](assets/properties_odata_cloud_service.jpg)

1. Vaya a la ficha &quot;Ajustes de autenticación&quot;.
1. Introduzca los siguientes detalles:

   1. **** Raíz del servicio: por ejemplo https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/
   1. **** Tipo de autenticación: OAuth 2.0
   1. **Configuración** de autenticación (consulte Configuración [de nube de](../../forms/using/forms-install-configure-gov-reference-site.md#dynamicsconfig) MS Dynamics para recopilar esta información):

      1. ID de cliente: también denominado ID de aplicación
      1. Secreto del cliente
      1. URL de OAuth, por ejemplo: [https://login.windows.net/common/oauth2/authorize](https://login.windows.net/common/oauth2/authorize)
      1. Actualizar URL del token: por ejemplo: [https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token)
      1. URL del autentificador de acceso, por ejemplo: [https://login.windows.net/common/oauth2/token](https://login.windows.net/common/oauth2/token)
      1. Ámbito de autorización: **open**
      1. Encabezado de autenticación: portador **de autorización**
      1. Recurso: p. ej. [https://msdynamicsserver.api.crm3.dynamics.com](https://msdynamicsserver.api.crm3.dynamics.com)
   1. Haga clic en &quot;Conectar a OAuth&quot;.


1. Después de autenticarse correctamente, haga clic en &quot;Guardar y cerrar&quot; para completar la integración.

#### Configuración de la nube de MS Dynamics {#dynamicsconfig}

Los pasos detallados en esta sección se incluyen para ayudarle a localizar el ID de cliente, el secreto de cliente y los detalles de la instancia de MS Dynamics Cloud.

1. Vaya a [https://portal.azure.com/](https://portal.azure.com/) e inicie sesión.
1. En el menú de la izquierda, seleccione &quot;Todos los servicios&quot;.
1. Busque o vaya a &quot;Registro de la aplicación&quot;.
1. Cree o seleccione un registro de aplicación existente.
1. Copie el ID **de** aplicación que se va a usar como ID **de** cliente de OAuth en la configuración de nube de AEM
1. Haga clic en &quot;Configuración&quot; o &quot;Manifiesto&quot; para configurar las direcciones URL de **respuesta.**

   1. Esta URL debe coincidir con la URL utilizada para acceder al servidor AEM al configurar el servicio OData.

1. En la vista Configuración, haga clic en &quot;Teclas&quot; para ver cómo crear una nueva clave (se utiliza como secreto de cliente en AEM).

   1. Asegúrese de guardar una copia de la clave ya que no podrá verla más tarde en Azure o AEM.

1. Para localizar la URL del recurso o la URL raíz del servicio, vaya al panel de instancia de MS Dynamics.
1. En la barra de navegación superior, haga clic en &quot;Ventas&quot; o en su propio tipo de instancia y en &quot;Seleccionar configuración&quot;.
1. Haga clic en &quot;Personalizaciones&quot; y &quot;Recursos para desarrolladores&quot; cerca de la parte inferior derecha.
1. Allí encontrará la URL de la raíz del servicio: e.g

* [https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/](https://msdynamicsserver.api.crm3.dynamics.com/api/data/v9.1/)*

1. Los detalles sobre la URL del autentificador de acceso y actualización están disponibles aquí:

* [https://docs.microsoft.com/en-us/rest/api/datacatalog/authenticate-a-client-app](https://docs.microsoft.com/en-us/rest/api/datacatalog/authenticate-a-client-app)*

#### Prueba del modelo de datos de formulario {#testing-the-form-data-model}

Una vez completada la configuración de nube, es posible que desee probar el modelo de datos de formulario.

1. Ir a

   *https://&lt;aemserver>:&lt;puerto>/aem/forms.html/content/dam/formsanddocuments-fdm/we-gov*

1. Seleccione &quot;We.gov Microsoft Dynamics CRM FDM&quot; y &quot;Properties&quot;.

   ![Propiedades de Dynamics CRM FDM](assets/properties_dynamics_crm.jpg)

1. Vaya a la ficha &quot;Actualizar origen&quot;.
1. Asegúrese de que la &quot;Configuración según el contexto&quot; esté configurada en &quot;/conf/we-gov&quot; y que la fuente de datos configurada sea &quot;ms-ddynamic-odata-cloud-service&quot;.

   ![Origen de datos configurado](assets/configured_data_source.jpg)

1. Edite el modelo de datos de formulario.

   >[!NOTE]
   Asegúrese de hacer clic en **Cancelar** en lugar de en **Guardar y cerrar** para evitar problemas que requieran reinstalación.

1. Pruebe los servicios para asegurarse de que se conectan correctamente a la fuente de datos configurada.

   >[!NOTE]
   Se ha informado de que se requería un reinicio de AEM Server para que la fuente de datos se enlazara correctamente al FDM.

### Adobe Analytics configuration {#adobe-analytics-configuration}

Esta sección contiene detalles e instrucciones sobre la configuración de Adobe Analytics Cloud.

**Referencias:**

* [Integración con Adobe Analytics](../../sites-administering/adobeanalytics.md)

* [Conexión a Adobe Analytics y creación de marcos](../../sites-administering/adobeanalytics-connect.md)

* [Visualización de datos de análisis de la página](../../sites-authoring/pa-using.md)

* [Configuración de análisis e informes](configure-analytics-forms-documents.md)

* [Visualización y comprensión de los informes de análisis de AEM Forms](view-understand-aem-forms-analytics-reports.md)

### Configuración del servicio en la nube de Adobe Analytics {#adobe-analytics-cloud-service-configuration}

Este paquete viene preconfigurado para conectarse a Adobe Analytics. Se proporcionan los pasos siguientes para permitir que se actualice esta configuración.

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/libs/cq/core/content/tools/cloudservices.html*
1. Busque la sección Adobe Analytics y seleccione el vínculo &quot;Mostrar configuraciones&quot;.
1. Seleccione la configuración &quot;We.Gov Adobe Analytics (Configuración de Analytics)&quot;.

   ![Configuración del servicio en la nube de Analytics](assets/analytics_config.jpg)

1. Haga clic en el botón &quot;Editar&quot; para actualizar la configuración de Adobe Analytics (deberá proporcionar el secreto compartido). Haga clic en &quot;Conectar con Analytics&quot; para conectarse y en &quot;Aceptar&quot; para completar.

   ![We.Gov Adobe Analytics](assets/wegov_adobe_analytics.jpg)

1. En la misma página, haga clic en &quot;We.Gov Adobe Analytics Framework (Analytics Framework)&quot; si desea actualizar las configuraciones de marco (consulte [Habilitar la creación](../../forms/using/forms-install-configure-gov-reference-site.md#enableauthoring) de AEM para habilitar la creación).

### Informes de Adobe Analytics {#adobe-analytics-reporting}

#### Ver informes de sitios de Adobe Analytics {#view-adobe-analytics-sites-reporting}

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/sites.html/content*
1. Seleccione &quot;AEM Forms We.Gov Site&quot; para ver las páginas del sitio.
1. Seleccione una de las páginas del sitio (p. ej. Inicio) y elija &quot;Analytics y recomendaciones&quot;.

   ![Análisis y recomendaciones](assets/analytics_recommendations.jpg)

1. En esta página, verá información recuperada de Adobe Analytics que se refiere a la página Sitios de AEM (nota: por diseño, esta información se actualiza periódicamente desde Adobe Analytics y no se muestra en tiempo real).

   ![Análisis de AEM Sites](assets/sites_analysis.jpg)

1. De nuevo en la página de vista de página (a la que se accede en el paso 3.1), también puede ver la información de vista de página cambiando la configuración de visualización para ver los elementos en la &quot;Vista de lista&quot;.
1. Busque el menú desplegable &quot;Ver&quot; y seleccione &quot;Vista de lista&quot;.

   ![Vista de lista](assets/list_view.jpg)

1. En el mismo menú, seleccione &quot;Ver configuración&quot; y seleccione las columnas que desee mostrar en la sección &quot;Análisis&quot;.

   ![Configurar columnas](assets/configure_columns.jpg)

1. Haga clic en &quot;Actualizar&quot; para que las nuevas columnas estén disponibles.

   ![Visualización de nuevas columnas](assets/new_columns_display.jpg)

#### Ver informes de formularios de Adobe Analytics {#view-adobe-analytics-forms-reporting}

1. Ir a

   *https://&lt;aemserver>:&lt;puerto>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. Seleccione el formulario adaptable &quot;Solicitud de inscripción para beneficios de salud&quot; y seleccione la opción &quot;Informe de Analytics&quot;.

   ![Informe de Analytics](assets/analytics_report.jpg)

1. Espere a que se cargue la página y vea los datos del informe de Analytics.

   ![Ver datos de informes de Analytics](assets/analytics_report_data.jpg)

#### Ver informes de Adobe Analytics {#view-adobe-analytics-reporting}

De forma opcional, puede navegar directamente a Adobe Analytics para ver los datos de análisis.

1. Vaya a [https://my.omniture.com/login/](https://my.omniture.com/login/)
1. Inicie sesión con sus credenciales:

   1. **** Empresa: Demostración de AEM Forms
   1. **** Usuario: &lt;disponible a petición>
   1. **** Contraseña: &lt;disponible a petición>

1. Seleccione el &quot;Sitio de referencia de We.Gov&quot; en los grupos de informes.

   ![Grupos de informes](assets/report_suites.jpg)

1. Seleccione uno de los informes disponibles para mostrar los datos de análisis de ese informe.

   ![Datos analíticos de un informe](assets/analytics_data.jpg)

## Personalizaciones del paquete de demostración {#demo-package-customizations}

Esta sección incluye instrucciones sobre la personalización de la demostración.

### Habilitar la creación de AEM {#enableauthoring}

Este paquete de demostración incluye un archivo de configuración de servicio OSGI que controla el comportamiento del servicio de filtro WCM en el servidor de creación de destino. Esta configuración hace que el servidor funcione en modo de autor desactivado (equivalente a ?wcmmode=disabled) para permitir la demostración. Para actualizar esta configuración y habilitar la creación, lleve a cabo los siguientes pasos:

1. Vaya a *https://&lt;aemserver>:&lt;puerto>/system/console/configMgr*
1. Busque y haga clic en el **servicio de servicio de servicio de CQ WCM Filter **Day para configurar.

   ![Filtro WCM de CQ de día](assets/day_cq_wcm_filter.jpg)

1. Establezca el valor de &quot;Modo **** WCM&quot; en &quot;**Editar**&quot;.
1. Haga clic en &quot;**Guardar**&quot; para aplicar la configuración.

### Personalización de plantillas {#templates-customization}

Las plantillas editables se encuentran en la siguiente ubicación:

*https://&lt;aemserver>:&lt;puerto>/libs/wcm/core/content/sites/templates.html/conf/we-gov*

Estas plantillas incluyen las plantillas Sitio de AEM, Formulario adaptable y Comunicaciones interactivas, creadas y ensambladas con componentes que se pueden encontrar en:

*https://&lt;aemserver>:&lt;puerto>/crx/de/index.jsp#/apps/we-gov/components*

#### Style system {#customizetemplates}

Este sitio también incluye bibliotecas cliente, una de las cuales importa Bootstrap 4 ( [https://getbootstrap.com/](https://getbootstrap.com/) ). Esta biblioteca de cliente está disponible en

*https://&lt;aemserver>:&lt;puerto>/crx/de/index.jsp#/apps/we-gov/clientlibs/clientlib-base/css/bootstrap*

Las plantillas editables incluidas en este paquete también vienen preconfiguradas con directivas de plantilla/página que utilizan las clases CSS de Bootstrap 4 para paginación, estilo, etc. No se han agregado todas las clases a las directivas de plantilla, pero se puede agregar a las directivas cualquier clase que admita Bootstrap 4. Consulte la página de introducción para obtener una lista de las clases disponibles:

[https://getbootstrap.com/docs/4.1/getting-started/introduction/](https://getbootstrap.com/docs/4.1/getting-started/introduction/)

Las plantillas incluidas en este paquete también admiten el sistema de estilos:

[Sistema de estilos](../../sites-authoring/style-system.md)

#### Logotipos de plantilla {#template-logos}

Los Recursos DAM del proyecto también incluyen logotipos e imágenes de We.Gov. Estos recursos están disponibles en:

*https://&lt;aemserver>:&lt;puerto>/assets.html/content/dam/we-gov*

Al editar las plantillas de página y formulario, puede elegir actualizar los logotipos de marca editando los componentes Navegación y Pie de página. Estos componentes ofrecen un cuadro de diálogo configurable de marca y logotipo que se puede utilizar para actualizar logotipos:

![Logotipos de plantilla](assets/template_logos.jpg)

Consulte Edición del contenido de la página para obtener más información:

[Edición del contenido de una página](../../sites-authoring/editing-content.md)

### Personalización de páginas de sitios {#sites-pages-customization}

Todas las páginas del sitio están disponibles en: *https://&lt;aemserver>:&lt;puerto>/sites.html/content/we-gov*

Estas páginas de sitio también utilizan el paquete de cuadrícula de AEM para controlar el diseño de algunos componentes.

#### Style system {#style-system}

Las páginas incluidas en este paquete también admiten el sistema de estilos:

[Sistema de estilos](../../sites-authoring/style-system.md)

También puede consultar el sistema [de estilo de personalización de](../../forms/using/forms-install-configure-gov-reference-site.md#customizetemplates) Plantillas para obtener documentación sobre los estilos admitidos.

### Personalización de formularios adaptables {#adaptive-forms-customization}

Todos los formularios adaptables están disponibles en:

*https://&lt;aemserver>:&lt;puerto>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

Estos formularios se pueden personalizar para adaptarse a determinados casos de uso. Tenga en cuenta que ciertos campos y la lógica de envío no deben modificarse para garantizar que el formulario siga funcionando correctamente. Esto incluye:

**Solicitud De Inscripción Para Beneficios De Salud:**

* contact_id - Campo oculto utilizado para recibir el ID de contacto de MS Dynamics durante el envío
* Enviar: la lógica del botón Enviar requiere personalización para admitir rellamadas. La personalización está documentada, pero se requiere una secuencia de comandos grande para enviar el formulario mientras se realiza una operación POST y GET a MS Dynamics mediante el modelo de datos de formularios.
* Panel raíz: el evento Initialize se utiliza para agregar un botón de MS Dynamics a la Bandeja de entrada de AEM de la manera menos intrusiva posible, ya que todos los componentes de la interfaz de usuario Granite de la Bandeja de entrada de AEM no se pueden modificar.

#### Estilo de formulario adaptable {#adaptive-form-styling}

Los formularios adaptables también se pueden diseñar con el Editor de estilo o el editor de temas:

* [Estilo en línea de los componentes de formularios adaptables](inline-style-adaptive-forms.md)
* [Creación y uso de temas](themes.md)

### Personalización de flujos de trabajo {#workflow-customization}

El formulario adaptable de inscripción se envía a un flujo de trabajo OSGI para su procesamiento. Este flujo de trabajo se encuentra en* https://&lt;aemserver>:&lt;puerto>/conf/we-gov/settings/models/we-gov-process.html*.

Debido a ciertas limitaciones, este flujo de trabajo contiene varias secuencias de comandos y pasos personalizados del proceso de flujo de trabajo OSGI. Estos pasos del flujo de trabajo se crearon como pasos genéricos y no se crearon con los cuadros de diálogo de configuración. En este momento, la configuración de los pasos del flujo de trabajo depende de los argumentos del proceso.

Todo el código Java de paso de flujo de trabajo está contenido en el paquete **we-gov-forms.core-&lt;version>.jar** .

## Consideraciones de demostración y problemas conocidos {#demo-considerations-and-known-issues}

Esta sección contiene información sobre las funciones de demostración y las decisiones de diseño que pueden requerir consideraciones especiales durante el proceso de demostración.

### Consideraciones de demostración {#demo-considerations}

* Según AGRS-159, asegúrese de que el nombre (primero, medio y último) del contacto utilizado en el formulario adaptable de inscripción sea único.
* El formulario adaptable de inscripción enviará el correo electrónico de Adobe Sign al correo electrónico especificado en el campo de correo electrónico del formulario. Esa dirección de correo electrónico no puede ser la misma dirección de correo electrónico que el correo electrónico utilizado para configurar la configuración de nube de Adobe Sign.
* De forma predeterminada, el paquete de demostración incluye varias configuraciones de servicio OSGI para controlar el comportamiento general del servidor de destino que aloja la demostración. Esta configuración incluye una configuración del servicio de filtro WCM que, de forma predeterminada, hace que el servidor funcione en un modo de autor **** desactivado (equivalente a ?wcmmode=disabled). Consulte [Activación de la creación](../../forms/using/forms-install-configure-gov-reference-site.md#enableauthoring) de AEM para permitir la creación de páginas.

### Problemas conocidos {#known-issues}

* (AGRS-120) El componente Navegación del sitio actualmente no admite páginas secundarias anidadas con una profundidad de más de 2 niveles.
* (AGRS-159) El FDM de MS Dynamics actual debe realizar dos operaciones para, en primer lugar, enviar los datos del formulario adaptable de matriculación a Dynamics y, a continuación, recuperar el registro de usuario para recuperar el ID de contacto. En su estado actual, la recuperación del ID de contacto fallará si hay más de dos usuarios con el mismo nombre en Dynamics, lo que no permitirá que se envíe el formulario adaptable de matriculación.

## Próximos pasos {#next-steps}

Ahora todos están listos para explorar el sitio de referencia de We.Gov. Para obtener más información sobre el flujo de trabajo y los pasos del sitio de referencia de We.Gov, consulte [Recorrido](../../forms/using/forms-gov-reference-site-user-demo.md)del sitio de referencia de We.Gov.
