---
title: Administrar [!DNL Adobe Stock] activos
description: Buscar, recuperar, obtener licencias y administrar [!DNL Adobe Stock] recursos desde [!DNL Adobe Experience Manager]. Utilice los recursos con licencia como cualquier otro recurso digital.
contentOwner: Vishabh Gupta
feature: Search, Adobe Stock
role: User, Admin
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2446'
ht-degree: 4%

---

# Uso [!DNL Adobe Stock] recursos en [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-assets-adobe-stock.html?lang=en) |
| AEM 6.5 | Este artículo |

<!-- old content

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager]. 

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] service provides designers and businesses with access to millions of high-quality, curated, royalty-free photos, vectors, illustrations, videos, templates, and 3D assets for all their creative projects. [!DNL Experience Manager] users are able to quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in [!DNL Experience Manager], without leaving the [!DNL Experience Manager] interface.
-->

<!-- New overview content
-->

[!DNL Adobe Stock] Este servicio proporciona a diseñadores y empresas acceso a millones de fotografías, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad, depurados y libres de derechos para todos sus proyectos creativos.

[!DNL Adobe Stock] la oferta para empresas, de forma predeterminada, incluye derechos de uso compartido en toda la organización. Una vez que un usuario de la organización ha concedido una licencia a un recurso, otros usuarios de la organización pueden identificar, descargar y utilizar este recurso sin tener que volver a obtener la licencia. Una vez que su organización ha concedido una licencia a un recurso, el derecho a utilizarlo es perpetuo.

Las organizaciones pueden integrar su empresa [!DNL Adobe Stock] planificar con [!DNL Experience Manager Assets] para garantizar que los recursos con licencia estén ampliamente disponibles para sus proyectos creativos y de marketing, con las potentes capacidades de administración de recursos de [!DNL Experience Manager]. [!DNL Experience Manager] los usuarios pueden buscar, previsualizar y obtener licencias rápidamente de los recursos de Adobe Stock guardados en [!DNL Experience Manager], sin salir del [!DNL Experience Manager] interfaz.

<!-- Old content
## Prerequisites {#prerequisites}

The integration requires an [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).
-->

## Integrar [!DNL Experience Manager] y [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] permite a los usuarios buscar, previsualizar, guardar y obtener licencias [!DNL Adobe Stock] recursos directamente desde [!DNL Experience Manager].

**Requisitos previos**

La integración requiere lo siguiente:

* Un [empresa [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/)
* Un usuario con permisos en Admin Console al perfil de producto de Stock predeterminado
* Un usuario con permisos de acceso de desarrollador para crear la integración en la consola de Adobe Developer

Una empresa [!DNL Adobe Stock] plan,

* Proporciona derechos de producto para [!DNL Adobe Stock] (Existencias conectadas al Experience Manager)
* Créditos comprados en el [!DNL Adobe Admin Console] para sus derechos de stock
* Habilita la autenticación de cuenta de servicio (JWT) en [!DNL Adobe Developer Console] para sus derechos de stock
* Permite administrar los créditos y las licencias globalmente desde [!DNL Adobe Admin Console]

Dentro del derecho, un perfil de producto predeterminado para [!DNL Adobe Stock] existe en [!DNL Admin Console]. Se pueden crear varios perfiles, que determinan quién puede obtener la licencia de los recursos de Stock. Un usuario que tenga acceso directamente al perfil del producto puede acceder a [https://stock.adobe.com/](https://stock.adobe.com/) y licencia de recursos de Stock. Mientras que hay otro método de utilizar el acceso de desarrollador para crear la integración (API) y autenticar la comunicación entre [!DNL Experience Manager] y [!DNL Adobe Stock].

>[!NOTE]
>
>La autenticación de la cuenta de servicio de Stock (JWT) viene con el derecho de Stock de la empresa.
>
>La integración no admite la autenticación Oauth para el derecho de Enterprise Stock.

<!-- old content
To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.
-->

## Pasos para la integración [!DNL Experience Manager] y [!DNL Adobe Stock] {#integration-steps}

Para integrar [!DNL Experience Manager] y [!DNL Adobe Stock], realice los siguientes pasos en la secuencia indicada:

1. [Obtener un certificado público](#public-certificate)

   Entrada [!DNL Experience Manager], cree una cuenta de IMS y genere un certificado público (clave pública).

1. [Crear una conexión de cuenta de servicio (JWT)](#createnewintegration)

   Entrada [!DNL Adobe Developer Console], cree un proyecto para su [!DNL Adobe Stock] organización. En el proyecto, configure una API con la clave pública para crear una conexión de cuenta de servicio (JWT). Obtenga las credenciales de la cuenta de servicio y la información de carga útil JWT.

1. [Configuración de la cuenta IMS](#create-ims-account-configuration)

   Entrada [!DNL Experience Manager], configure la cuenta de IMS con las credenciales de la cuenta de servicio y la carga útil JWT.

1. [Configurar servicio en la nube](#configure-the-cloud-service)

   Entrada [!DNL Experience Manager], configure un [!DNL Adobe Stock] Cloud Service con la cuenta de IMS.


### Creación de una configuración de IMS {#create-an-ims-configuration}

La configuración de IMS autentica su [!DNL Experience Manager Assets] instancia de autor con [!DNL Adobe Stock] derecho.

La configuración de IMS incluye dos pasos:

* [Obtener un certificado público](#public-certificate)
* [Configuración de la cuenta IMS](#create-ims-account-configuration)

### Obtener un certificado público {#public-certificate}

La clave pública (certificado) autentica el perfil del producto en Adobe Developer Console.

1. Inicie sesión en su [!DNL Experience Manager Assets] instancia de autor. La URL predeterminada es `http://localhost:4502/aem/start.html`.

1. Desde el **[!UICONTROL Herramientas]** panel, vaya a **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**.

1. En la página Configuraciones de IMS de Adobe, haga clic en **[!UICONTROL Crear]**. El **[!UICONTROL Configuración de cuenta técnica de IMS de Adobe]** se abre la página.

1. En el **[!UICONTROL Certificado]** pestaña, seleccione **[!UICONTROL Adobe Stock]** desde el **[!UICONTROL Solución de nube]** lista desplegable.

1. Puede crear un certificado o reutilizar un certificado existente para la configuración.

   Para crear un certificado, seleccione la **[!UICONTROL Crear nuevo certificado]** y especifique una **alias** para la clave pública. El alias sirve como nombre de la clave pública.

1. Haga clic en **[!UICONTROL Crear certificado]**. A continuación, haga clic en **[!UICONTROL OK]** para generar la clave pública.

1. Haga clic en **[!UICONTROL Descargar clave pública]** y guarde el archivo de clave pública (.crt) en el equipo. La clave pública se utiliza más adelante para configurar la API del inquilino de Brand Portal y generar credenciales de cuenta de servicio en la consola de Adobe Developer.

   Haga clic en **[!UICONTROL Siguiente]**.

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. En el **Cuenta** pestaña, se crea la cuenta de Adobe IMS que requiere las credenciales de la cuenta de servicio.

   Abra una pestaña nueva y [crear una conexión de cuenta de servicio (JWT) en la consola de Adobe Developer](#createnewintegration).

### Crear una conexión de cuenta de servicio (JWT) {#createnewintegration}

En la consola de Adobe Developer, los proyectos y las API se configuran en el nivel de organización. Al configurar una API, se crea una conexión de cuenta de servicio (JWT). Existen dos métodos para configurar la API: generar un par de claves (claves pública y privada) o cargar una clave pública. En este ejemplo, las credenciales de la cuenta de servicio se generan cargando la clave pública.

Para generar las credenciales de la cuenta de servicio y la carga útil JWT:

1. Inicie sesión en la consola de Adobe Developer con privilegios de administrador del sistema. La URL predeterminada es [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Asegúrese de haber seleccionado la organización IMS correcta (asignación de existencias) en la lista desplegable (organización).

1. Clic **[!UICONTROL Crear nuevo proyecto]**. Se crea un proyecto en blanco con un nombre generado por el sistema para su organización.

   Clic **[!UICONTROL Editar proyecto]**. Actualice el **[!UICONTROL Título del proyecto]** y **[!UICONTROL Descripción]** y haga clic en **[!UICONTROL Guardar]**.

1. En el **[!UICONTROL Resumen del proyecto]** pestaña, haga clic en **[!UICONTROL Añadir API]**.

1. En el **[!UICONTROL Añadir una ventana de API]**, seleccione **[!UICONTROL Adobe Stock]**. Haga clic en **[!UICONTROL Siguiente]**.

1. En el **[!UICONTROL Configurar API]** ventana, seleccione **[!UICONTROL Cuenta de servicio (JWT)]** autenticación. Haga clic en **[!UICONTROL Siguiente]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Clic **[!UICONTROL Cargar la clave pública]**. Clic **[!UICONTROL Seleccionar un archivo]** y cargue la clave pública (archivo .crt) descargada en el [obtener un certificado público](#public-certificate) sección. Haga clic en **[!UICONTROL Siguiente]**.

1. Compruebe la clave pública y haga clic en **[!UICONTROL Siguiente]**.

1. Seleccione el valor predeterminado **[!UICONTROL Adobe Stock]** perfil del producto y haga clic en **[!UICONTROL Guardar API configurada]**.

1. Una vez configurada la API, se le redirigirá a la página de información general de la API. Desde la parte inferior de navegación izquierda **[!UICONTROL Credenciales]**, haga clic en **[!UICONTROL Cuenta de servicio (JWT)]** opción. Aquí puede ver las credenciales y realizar acciones como generar tokens JWT, copiar detalles de credenciales y recuperar secretos de cliente.

1. Desde el **[!UICONTROL Credenciales del cliente]** pestaña, copie el **[!UICONTROL ID de cliente]**.

   Clic **[!UICONTROL Recuperar secreto de cliente]** y copie el **[!UICONTROL secreto de cliente]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Vaya a **[!UICONTROL Generar JWT]** y copie la pestaña **[!UICONTROL Carga útil JWT]** información.

Ahora puede utilizar el ID de cliente (clave de API), el secreto de cliente y la carga útil JWT para [configuración de la cuenta de IMS](#create-ims-account-configuration) in [!DNL Experience Manager Assets].

### Configuración de la cuenta IMS {#create-ims-account-configuration}

Debe tener el [certificado](#public-certificate) y [credenciales de cuenta de servicio (JWT)](#createnewintegration) para configurar la cuenta de IMS.

Para configurar la cuenta de IMS:

1. Abra la Configuración de IMS y vaya a **[!UICONTROL Cuenta]** pestaña. La página se ha mantenido abierta mientras [obtención del certificado público](#public-certificate).

1. Especifique un **[!UICONTROL Título]** para la cuenta de IMS.

   En el **[!UICONTROL Servidor de autorización]** , introduzca la dirección URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Introduzca el ID de cliente en la **[!UICONTROL Clave de API]** field, **[!UICONTROL Secreto del cliente]**, y **[!UICONTROL Carga útil]** (Carga útil JWT) que ha copiado mientras [creación de la conexión de cuenta de servicio (JWT)](#createnewintegration).

1. Haga clic en **[!UICONTROL Crear]**. Se crea una configuración de cuenta de IMS.

   ![configure-ims-account](assets/aem-stock-ims-config.png)

1. Seleccione la configuración de cuenta de IMS y haga clic en **[!UICONTROL Comprobar estado]**.

   Clic **[!UICONTROL Marque]** en el cuadro de diálogo. Si la configuración se realiza correctamente, aparecerá un mensaje que indica que la variable *Token recuperado correctamente*.

   ![control de estado](assets/aem-stock-healthcheck.png)


### Configurar servicio en la nube {#configure-the-cloud-service}

Para configurar la variable [!DNL Adobe Stock] servicio en la nube:

1. En el [!DNL Experience Manager] interfaz de usuario, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Stock]**.

1. En el [!DNL Adobe Stock Configurations] página, haga clic en **[!UICONTROL Crear]**.

1. Especifique un **[!UICONTROL Título]** para la configuración en la nube.

   Seleccione la configuración de IMS que ha creado durante [configuración de la cuenta de IMS](#create-ims-account-configuration).

   Seleccione la configuración regional en la lista desplegable.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   Su [!DNL Experience Manager Assets] la instancia de autor ahora está integrada con [!DNL Adobe Stock]. Puede crear varias [!DNL Adobe Stock] configuraciones (por ejemplo, configuraciones basadas en la configuración regional). Ahora puede acceder, buscar y obtener una licencia de [!DNL Adobe Stock] recursos desde el [!DNL Experience Manager] interfaz de usuario.

   ![search-stock-assets](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >En esta fase de integración, solo los administradores pueden acceder a [!DNL Adobe Stock] recursos, buscar recursos de Stock (mediante omnisearch) y obtener una licencia de [!DNL Adobe Stock] recursos.
   >
   >Los administradores también pueden agregar usuarios o grupos a [!DNL Adobe Stock] y conceda permisos a estos usuarios no administradores en [!DNL Experience Manager] para acceder a la configuración de Stock.

1. Para agregar usuarios o grupos, seleccione la [!DNL Adobe Stock] configuración de nube y haga clic en **[!UICONTROL Propiedades]**.

1. Busque y añada los usuarios o grupos a los que ha asignado permisos para acceder a la configuración de Adobe Stock. Consulte [asignar permisos al grupo de usuarios](#assign-permissions-to-group).


## Asignar permisos al grupo de usuarios {#assign-permissions-to-group}

Los administradores pueden crear grupos de usuarios y conceder permisos a determinados usuarios o grupos para acceder a [!DNL Adobe Stock] servicio en la nube.

A continuación se indican los permisos necesarios para que un usuario busque y conceda licencias a recursos de Adobe Stock:

* Configure la ruta: `/conf/global/settings/stock`
* Privilegios: `jcr:read`
* Tipo de permiso: `Allow`

Puede crear un grupo de usuarios o asignar permisos a un grupo de usuarios existente. Los permisos se pueden asignar desde el [!DNL Experience Manager Assets] o desde el [!DNL User Admin] Consola.

**Para proporcionar acceso a un grupo de usuarios desde [!DNL Experience Manager]:**

1. En el [!DNL Experience Manager] interfaz de usuario, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Grupos]**. Crear un grupo de usuarios para [!DNL Adobe Stock].

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Permisos]**.

1. Busque el grupo de usuarios en el panel izquierdo y añada uno nuevo **[!UICONTROL Entrada de control de acceso (ACE)]** para Adobe Stock.

   * Configure la ruta: `/conf/global/settings/stock`
   * Privilegios: `jcr:read`
   * Tipo de permiso: `Allow`

   Clic **[!UICONTROL Añadir]**.

   ![user-permissions](assets/aem-stock-user-permissions.png)

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Stock]**. Seleccione el [!DNL Adobe Stock] configuración de nube y haga clic en **[!UICONTROL Propiedades]**.

1. Agregue el grupo de usuarios recién creado al [!DNL Adobe Stock] configuración. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   ![assign-user](assets/aem-stock-adduser.png)

**Para proporcionar acceso a un usuario desde [!DNL User Admin Console]:**

1. Abra el [!DNL Experience Manager] Admin Console de usuario. La URL predeterminada es `http://localhost:4502/userdamin`.

1. En el panel izquierdo, busque el usuario introduciendo la variable `user_id` o `name`. Haga doble clic para abrir las propiedades del usuario.

1. Vaya a **[!UICONTROL Permisos]** pestaña y permitir `read` permisos para [!DNL Adobe Stock] configuración de nube: `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >Si la configuración en la nube no está permitida, el usuario solo puede acceder a **[!UICONTROL Assets]** en el [!DNL Experience Manager] interfaz.
   >
   >Para permitir el acceso a [!UICONTROL Assets] y [!DNL Adobe Stock] recursos, asegúrese de que la configuración de la nube esté permitida para el usuario.

1. Clic **[!UICONTROL Guardar]** para actualizar los permisos.

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. Añada el usuario o el grupo al [!DNL Adobe Stock] configuración de nube.


## Acceso a recursos de Adobe Stock {#access-stock-assets}

Un usuario no administrador que tiene permisos para [!DNL Adobe Stock] la configuración de nube de puede buscar y obtener la licencia de [!DNL Adobe Stock] recursos de la [!DNL Experience Manager] interfaz.

El usuario debe realizar un paso adicional para activar el [!DNL Adobe Stock] configuración de nube antes de acceder a [!DNL Adobe Stock] recursos. Es una actividad única. Si al usuario se le asignan permisos en varias páginas [!DNL Adobe Stock] configuraciones en la nube, el usuario puede seleccionar la configuración deseada en el **[!UICONTROL Preferencias de usuario]**.

Para activar la variable [!DNL Adobe Stock] configuración de nube:

1. Iniciar sesión en [!DNL Experience Manager].

1. Haga clic en el icono de usuario en la esquina superior derecha y, a continuación, haga clic en **[!UICONTROL Mis preferencias]**. El **[!UICONTROL Preferencias de usuario]** se abre.

1. Seleccione el **[!UICONTROL Configuración de Stock]** en la lista desplegable y haga clic en **[!UICONTROL Aceptar]** para activar la configuración.

   ![user-preferences](assets/aem-stock-preferences.png)

1. Vaya a **[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock]**. Ahora puede ver, buscar y obtener licencias [!DNL Adobe Stock] recursos.

En la tabla siguiente se explica cómo funcionan los permisos de usuario al acceder a [!DNL Adobe Stock] recursos:

| Usuario | Grupo | Permisos | Aceptar configuración de Stock en Preferencias de usuario | Acceso a recursos | Acceso a Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| administrador | N/D | Todos | N/D | Sí | Sí |
| test-doc1 | Usuario DAM | /conf/global /settings/stock/cloud-config | Sí | Sí | Sí |
| test-doc1 | Usuario DAM | /conf/global /settings/stock/cloud-config | No | Error: Error al cargar los datos | No |
| test-doc1 | Usuario DAM | **permitir**: /conf/global /settings/stock     **denegar**: /cloud-config | La configuración de Stock no es visible | Sí | No |


## Uso y administración [!DNL Adobe Stock] recursos en [!DNL Experience Manager] {#usemanage}

Con esta capacidad, las organizaciones pueden permitir que sus usuarios trabajen con [!DNL Adobe Stock] recursos en [!DNL Experience Manager Assets]. Desde dentro de [!DNL Experience Manager] interfaz de usuario, los usuarios pueden buscar [!DNL Adobe Stock] recursos y obtener la licencia de los recursos necesarios.

Una vez por [!DNL Adobe Stock] el recurso tiene licencia en [!DNL Experience Manager], se puede utilizar y administrar como un recurso habitual. Entrada [!DNL Experience Manager], los usuarios pueden buscar y previsualizar los recursos, copiarlos y publicarlos, y compartirlos en [!DNL Brand Portal]; acceder y utilizar los recursos mediante [!DNL Experience Manager] aplicación de escritorio, etc.

![Buscar por [!DNL Adobe Stock] recursos y filtrar resultados de sus [!DNL Adobe Experience Manager] workspace](assets/adobe-stock-search-results-workspace.png)

**A.** Busque recursos similares a los recursos cuya [!DNL Adobe Stock] Se ha proporcionado el ID. **B.** Busque recursos que coincidan con la selección de forma u orientación. **C.** Busque uno de los tipos de recursos más admitidos **D.** Abrir o contraer el panel de filtros **E.** Obtenga la licencia y guarde el recurso seleccionado en [!DNL Experience Manager] **F..** Guarde el recurso en [!DNL Experience Manager] con marca de agua **G.** Explorar recursos en [!DNL Adobe Stock] sitios web similares al recurso seleccionado **H..** Ver los recursos seleccionados en [!DNL Adobe Stock] sitio web **YO.** Número de recursos seleccionados de los resultados de búsqueda **J.** Cambiar entre la vista de tarjeta y la vista de lista

### Buscar recursos {#find-assets}

Su [!DNL Experience Manager] Los usuarios de, pueden buscar recursos en ambos, [!DNL Experience Manager] y [!DNL Adobe Stock]. Cuando la ubicación de búsqueda no se limita a [!DNL Adobe Stock], los resultados de búsqueda de [!DNL Experience Manager] y [!DNL Adobe Stock] se muestran.

* Para buscar [!DNL Adobe Stock] recursos, haga clic en **[!UICONTROL Navegación]** > **[!UICONTROL Assets]** > **[!UICONTROL Buscar Adobe Stock]**.

* Para buscar recursos en [!DNL Adobe Stock] y [!DNL Experience Manager Assets], haga clic en buscar ![búsqueda](assets/do-not-localize/search_icon.png).

También puede empezar a escribir `Location: Adobe Stock` en la barra de búsqueda para seleccionar [!DNL Adobe Stock] recursos. [!DNL Experience Manager] ofrece funcionalidades de filtrado avanzadas en los recursos buscados, lo que permite a los usuarios centrarse rápidamente en los recursos necesarios mediante filtros, como tipos de recursos admitidos, orientación de la imagen y estado con licencia.

>[!NOTE]
>
>Recursos buscados desde [!DNL Adobe Stock] se muestran en [!DNL Experience Manager]. [!DNL Adobe Stock] los recursos se recuperan y almacenan en [!DNL Experience Manager] repositorio solo después de que un usuario [guarda un recurso](/help/assets/aem-assets-adobe-stock.md#saveassets) o [otorga licencia a un recurso y lo guarda](/help/assets/aem-assets-adobe-stock.md#licenseassets). Recursos que ya están almacenados en [!DNL Experience Manager] se muestran y resaltan para facilitar la referencia y el acceso. Además, la variable [!DNL Stock] Los recursos de se guardan con algunos metadatos adicionales para indicar el origen como [!DNL Stock].

![Buscar filtros en [!DNL Experience Manager] y resaltados [!DNL Adobe Stock] recursos en resultados de búsqueda](assets/aem-search-filters2.jpg)

### Guarde y vea los recursos necesarios {#saveassets}

Seleccione un recurso en el que desee guardar [!DNL Experience Manager]. Clic [!UICONTROL Guardar] en la barra de herramientas situada en la parte superior y proporcione el nombre y la ubicación del recurso. Los recursos sin licencia se guardan localmente con una marca de agua.

La próxima vez que busque recursos, los recursos guardados se resaltarán con un distintivo para indicar que están disponibles en [!DNL Experience Manager Assets].

>[!NOTE]
>
>Los recursos añadidos recientemente muestran un distintivo Nuevo en lugar de Distintivo con licencia.

### Recursos de licencia {#licenseassets}

Los usuarios pueden autorizar [!DNL Adobe Stock] recursos mediante la cuota de su [!DNL Adobe Stock] plan empresarial. Al obtener la licencia de un recurso, se guarda sin una marca de agua y está disponible para buscarlo y utilizarlo en [!DNL Experience Manager Assets].

![Diálogo para autorizar y guardar [!DNL Adobe Stock] recursos en [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### Acceso a metadatos y propiedades de recursos {#access-metadata-and-asset-properties}

Los usuarios pueden acceder a los metadatos y previsualizarlos, incluido el [!DNL Adobe Stock] propiedades de metadatos de los recursos guardados en [!DNL Experience Manager]y agregue. **[!UICONTROL Referencias de licencia]** para un recurso. Sin embargo, las actualizaciones de la referencia de licencia no se sincronizan entre [!DNL Experience Manager] y [!DNL Adobe Stock] sitio web.

Los usuarios pueden ver las propiedades de los recursos con y sin licencia.

![Ver y acceder a metadatos y referencias de licencias de recursos guardados](assets/metadata_properties.jpg)


## Limitaciones conocidas {#known-limitations}

* **Problemas en la integración con [!DNL Experience Manager] Paquete de servicio 6.5.7.0 y superior**: Se identifica un problema inesperado durante la integración con [!DNL Experience Manager] 6.5.7.0 y superior. El problema se está probando y se espera que esté disponible en [!DNL Experience Manager] 6.5.11.0. Contacto [!DNL Customer Support] para obtener una revisión inmediata.

* **La funcionalidad para restringir a los usuarios las licencias no funciona correctamente**: Todos los usuarios que tienen `read` Los permisos de para la configuración de stock permiten buscar y obtener licencias de [!DNL Adobe Stock] recursos.

* **Los usuarios no administradores deben activar manualmente la variable [!DNL Adobe Stock] configuración de nube**: en el **[!UICONTROL Preferencias de usuario]** ventana, el **[!UICONTROL Configuración de Stock]** muestra el [!DNL Adobe Stock] la configuración de nube estaba habilitada, pero no funciona para un usuario que no sea administrador. El usuario debe hacer clic en **[!UICONTROL Aceptar]** para activar la configuración de Stock. Si no se realiza este paso, el sistema mostrará un mensaje de error al acceder a **[!UICONTROL Assets]**.

* **No se muestra la advertencia de imagen editorial**: al autorizar una imagen, los usuarios no pueden comprobar si una imagen es de uso editorial únicamente. Para evitar un posible uso indebido, los administradores pueden desactivar el acceso a los activos editoriales del Admin Console.

* **Se muestra un tipo de licencia incorrecto**: Es posible que se muestre un tipo de licencia incorrecto en [!DNL Experience Manager] para un recurso. Los usuarios pueden iniciar sesión en [!DNL Adobe Stock] para ver el tipo de licencia.

* **Los campos de referencia y los metadatos no están sincronizados**: Cuando un usuario actualiza un campo de referencia de licencia, la información de referencia de licencia se actualiza en [!DNL Experience Manager] pero no en el [!DNL Adobe Stock] sitio web. Del mismo modo, si el usuario actualiza los campos de referencia en la [!DNL Adobe Stock] sitio web, las actualizaciones no se sincronizan en [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Tutorial de vídeo sobre el uso de [!DNL Adobe Stock] recursos con [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] ayuda de plan empresarial](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] Preguntas más frecuentes](https://helpx.adobe.com/stock/faq.html)


<!--old content

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in [!UICONTROL User Preferences] panel. To access the panel from [!DNL Experience Manager] home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.
-->

