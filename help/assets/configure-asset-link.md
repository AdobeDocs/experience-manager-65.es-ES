---
title: Configuración de Experience Manager Assets para Asset Link de Adobe
description: Configure Experience Manager Assets para usarlo con la extensión de Adobe Asset Link para aplicaciones de Creative Cloud.
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
source-git-commit: e91fa04d87c7ecacf3ad8a148227948eafe15b1e
workflow-type: tm+mt
source-wordcount: '3149'
ht-degree: 1%

---


# Configuración de Experience Manager Assets para Asset Link de Adobe {#adobe-asset-link}

[Adobe Asset Link (AAL)](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html) optimiza la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido. Conecta Adobe Experience Manager Assets con las aplicaciones de escritorio de Creative Cloud Adobe InDesign, Adobe Photoshop y Adobe Illustrator. El panel Adobe Asset Link permite a los creativos acceder y modificar el contenido almacenado en AEM Assets sin salir de las aplicaciones creativas con las que están más familiarizados.

Para configurar Experience Manager Assets para que se utilice con Asset Link, implemente las siguientes tareas. Utilice la cuenta de administrador del Experience Manager para realizar la configuración:

1. Instale los paquetes según sea necesario. Los detalles están en [requisitos previos](#prerequisites).

1. Configure el Experience Manager: [manualmente](#manual-configuration) o utilizando un [paquete](#configure-using-package).

1. Para asignar usuarios con licencia de Creative Cloud a usuarios de Experience Manager, administre [control de acceso del usuario](#user-access).

1. Crear [índice de consulta personalizado](#create-custom-index), configure [Representaciones de FPO](/help/assets/configure-fpo-renditions.md) para InDesign, configure [Integración con Adobe Stock](/help/assets/aem-assets-adobe-stock.md)y configure [búsqueda visual o de similitud](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## Requisitos previos y compatibilidad con diversas funcionalidades {#prerequisites}

Asegúrese de instalar el paquete de servicio y el paquete adecuados según sea necesario. Consulte los siguientes requisitos para cada versión del Experience Manager y para funciones específicas.

| Capacidad de los recursos | Versión del Experience Manager y requisitos de asistencia |
|--- |--- |
| Asset Link funciona de forma predeterminada | Experience Manager 6.5 y 6.5.2 o posterior. </br> Experience Manager 6.4.4 y 6.4.6 o posterior. </br> Adobe recomienda instalar la última [Paquete de servicio de Experience Manager (SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html) antes de utilizar AAL. |
| Asset Link funciona después de instalar un paquete | Para Experience Manager 6.4.0 - 6.4.3, instale [adobe-asset-link-support](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) paquete. |
| Integración con Adobe Stock | Experience Manager 6.4.2 o posterior |
| Búsqueda visual o de similitud | Experience Manager 6.5.0 o posterior |


## Configuración del Experience Manager mediante el paquete de configuración {#configure-using-package}

Adobe recomienda que instale [adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config) paquete de configuración para automatizar la mayoría de las tareas de configuración, seguido de algunas tareas manuales. También puede [configurar manualmente](#manual-configuration).

>[!CAUTION]
>
>Si la instancia de Experience Manager está configurada para el inicio de sesión del usuario con cuentas de IMS de Adobe, no use el paquete de configuración. En su lugar, [configurar manualmente](#manual-configuration) la instancia de Experience Manager.

1. Para abrir el Administrador de paquetes, en la interfaz web de Experience Manager, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Uso compartido de paquetes]**. Instalar `adobe-asset-link-config` paquete.

1. Acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**. Localizar **[!UICONTROL Proveedor de IMS de Adobe Granite OAuth]** y haga clic en para editarla.

   Establezca las siguientes propiedades y guarde los cambios.

   * [!UICONTROL Asignaciones de grupos]: Deje vacío a menos que lo desee. Para obtener más información, consulte [Asignación de grupos](#group-mapping).
   * [!UICONTROL Organización]: Introduzca el ID de organización que utiliza en Adobe Admin Console. Para obtener más información sobre los ID de organización, consulte [Crear grupo de usuarios](https://helpx.adobe.com/enterprise/using/create-aal-user-group.html).

1. Localizar **[!UICONTROL Controlador de autenticación del portador de Adobe Granite]** y haga clic en para editarla.

   Agregar **[!UICONTROL InDesignAem2]** Los ID de cliente a la variable **[!UICONTROL ID de cliente de OAuth permitidos]** propiedad configuration .


## Configuración manual del Experience Manager {#manual-configuration}

Configure manualmente el Experience Manager si decide no utilizar un paquete de configuración o si la implementación del Experience Manager está configurada para admitir el inicio de sesión del usuario con cuentas de Adobe IMS.

Para configurar manualmente el Experience Manager:

1. Para acceder al administrador de configuración, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**. Select **[!UICONTROL OSGi]** > **[!UICONTROL Configuración]** en el menú de la parte superior.

1. Busque la variable **[!UICONTROL Proveedor de IMS de Adobe Granite OAuth]** y haga clic en para editarla.

   Establezca la siguiente configuración y haga clic en **[!UICONTROL Guardar]**.

   * [!UICONTROL Punto final de autorización]: ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL Extremo de token]: ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL Punto final del perfil]: ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL Dirección URL de validación]: ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL Organización]: Configúrelo en el ID de organización en la variable [Adobe Admin Console](https://adminconsole.adobe.com/).
   * [!UICONTROL Asignaciones de grupos]: Deje vacío a menos que tenga un caso especial. Para obtener más información, consulte [Asignación de grupos](#group-mapping).

1. Localizar **[!UICONTROL Controlador de autenticación del portador de Adobe Granite]** y haga clic en para editarla.

   Agregue los siguientes ID de cliente a **[!UICONTROL ID de cliente de OAuth permitidos]** propiedad configuration: `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`.

   Para agregar cada `Client ID`, haga clic en `+`. Haga clic en **[!UICONTROL Guardar]** después de agregar todos los ID.

1. En **[!UICONTROL Adobe Granite OAuth Aplicación y Proveedor]** configuración, inspeccione los **[!UICONTROL Controlador de autenticación OAuth de Granite de Adobe]** instancias. Si encuentra una instancia con la variable `Config ID` valor de `ims`, utilícelo para las instrucciones de este procedimiento. De lo contrario, haga clic en `+` para crear una instancia de configuración. Establezca los siguientes valores de propiedad y haga clic en **[!UICONTROL Guardar]**.

   * [!UICONTROL ID de cliente]: No cambiar
   * [!UICONTROL Secreto del cliente]: No cambiar
   * [!UICONTROL ID de configuración]: ` ims`
   * [!UICONTROL Ámbito]: `AdobeID, OpenID, read_organizations` (otros valores también pueden estar en la configuración)
   * [!UICONTROL ID del proveedor]: ` ims`
   * [!UICONTROL Crear usuarios]: ` Checked`
   * [!UICONTROL Propiedad de ID de usuario]: `Email` para la configuración recién creada. De lo contrario, no cambie.

1. Busque la variable **[!UICONTROL Controlador de sincronización predeterminado Apache Jackrabbit Oak]** con el **[!UICONTROL Nombre del controlador de sincronización]** `ims` y haga clic en para editarlo.

   Establezca las siguientes propiedades de configuración y haga clic en **[!UICONTROL Guardar]**.

   * [!UICONTROL Hora de caducidad del usuario y caducidad de la pertenencia del usuario]: Tiempo en minutos después de &quot;m&quot; sin espacio. Por ejemplo, `15m` durante 15 minutos. Para obtener más información, consulte [Asignación de grupos](#group-mapping).
   * [!UICONTROL Pertenencia automática del usuario]: No cambiar
   * [!UICONTROL Pertenencia dinámica de usuario]: ` Deslect`

1. Busque la variable **[!UICONTROL Controlador de autenticación OAuth de Granite de Adobe]** y haga clic en para editarla. Sin realizar ningún cambio, haga clic en **[!UICONTROL Guardar]**.

1. Para ajustar la prioridad relativa del gestor de autenticación del portador, en CRXDE, vaya a `/apps/system/config`. Localizar `com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config` y abra su configuración. Al final, agregue `service.ranking=I"-10"`. Guarde los cambios.

   >[!NOTE]
   >
   >Cada solicitud autenticada con un token al portador incurre en la sobrecarga de tres llamadas a Adobe IMS, la sincronización de usuarios y la creación de un token de inicio de sesión en el Experience Manager. Para superar esta sobrecarga, Adobe Asset Link captura el token de inicio de sesión devuelto en la respuesta del Experience Manager y lo envía con solicitudes posteriores. Para que este proceso funcione, se debe ajustar la prioridad relativa del gestor de autenticación del portador.

1. (Opcional) Si los usuarios del Experience Manager tienen nombres de dominio con mayúsculas o minúsculas mixtos en sus ID de correo electrónico, seleccione **[!UICONTROL Cambiar el usuario de bloqueo a minúsculas]** en **[!UICONTROL Configuraciones de la plataforma ACP de Adobe Granite]** en la consola web de Experience Manager.

## Configuración adicional después de la migración a Perfiles de negocio {#configure-migration-activity}

Los usuarios de Adobe Asset Link pueden conectarse al Experience Manager para permitir el inicio de sesión de IMS desde la organización principal del Creative Cloud para empresas (CCE). El Experience Manager utiliza los ID de cliente para identificar la organización de IMS permitida. Después de la migración a los perfiles empresariales, es necesario configurar el ID de cliente y la clave secreta para la organización de IMS en el Experience Manager del gestor de autenticación del portador. Para obtener más información sobre los perfiles empresariales, consulte [introducción de perfiles de Adobe](https://helpx.adobe.com/enterprise/kb/introducing-adobe-profiles.html).

Solo es necesaria una configuración adicional si utiliza distintas organizaciones de Adobe IMS para Experience Manager y Creative Cloud de Enterprise (CCE), y se establece una relación de confianza de dominio entre estas dos organizaciones.

>[!NOTE]
>
>* La corrección para perfiles empresariales se proporciona en el Experience Manager 6.5.11.0.
>* La configuración existente sigue funcionando si utiliza la misma organización de Adobe IMS con Experience Manager y CCE.



**Requisitos previos**

1. Una instancia de Experience Manager en ejecución con autenticación de portador configurada para AAL.
1. Instale el siguiente paquete (Service Pack 11) en su instancia de Experience Manager 6.5.

   [Descargar Experience Manager 6.5.11.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. Contacto [!UICONTROL Asistencia al cliente] para obtener el ID de cliente y la clave secreta para la autenticación del portador de su organización de IMS.

A continuación se indican las configuraciones adicionales que se requieren después de la migración a los perfiles empresariales:

1. En **[!UICONTROL Proveedor de configuración de Adobe Granite OAuth IMS]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`), configurado:

   * ID de configuración de OAuth (`oauth.configmanager.ims.configid`): `ims` (Verificar una vez, puede que ya esté configurado)

   * Entidad propietaria de IMS (`ims.owningEntity`): Su id de organización de IMS

   ![ID de configuración de IMS](assets/bearer-authentication1.png)

1. Apertura **[!UICONTROL Gestor de autenticación del portador]** y añada el ID de cliente obtenido de [!UICONTROL Asistencia al cliente] a la lista de **[!UICONTROL ID de cliente de OAuth permitidos]**.

   ![Añadir ID de cliente](assets/add-clientid-bearer-auth.png)

1. Apertura **[!UICONTROL Adobe Granite OAuth Aplicación y Proveedor]** y añada la variable **[!UICONTROL ID de cliente]** y **[!UICONTROL Secreto del cliente]** (Clave secreta) obtenida de la asistencia al cliente.

   Asegúrese de que la variable **[!UICONTROL ID de configuración]** campo (`oauth.config.id`) contiene el mismo valor que se proporciona en **[!UICONTROL ID de configuración de OAuth]** campo (`oauth.configmanager.ims.configid`).

   ![Verificar ID de cliente](assets/clientid-secretkey.png)

1. Apertura **[!UICONTROL Adobe Granite IMS Cluster Exchange Token Preprocessor]** y configúrelo en `enable`.

## Administrar el control de acceso de los usuarios {#user-access}

En esta sección se describe cómo administrar usuarios y su acceso al repositorio de Experience Manager.

### Asignación de grupos {#group-mapping}

La asignación de grupos determina cómo se corresponden los grupos en Experience Manager con los grupos en Adobe IMS. Desempeña un papel importante en la forma en que se concede permiso a los usuarios de Adobe Asset Link para acceder a Experience Manager Assets.

Cuando se utiliza con Adobe Asset Link, el Experience Manager delega funciones de administración de usuarios en Adobe IMS. Se crean automáticamente usuarios y grupos que corresponden a usuarios y grupos en Adobe IMS. Además, sincroniza a los usuarios, grupos y miembros del grupo en el Experience Manager para que coincidan con los de Adobe IMS.

Por ejemplo, imaginemos un escenario en el que los usuarios de Adobe Asset Link son miembros del grupo de recursos IMS de Adobe y los usuarios de vínculos. En este caso, se crea en Experience Manager un grupo sincronizado denominado Asset-link-users cuando un usuario de ese grupo IMS de Adobe se conecta a Adobe Asset Link por primera vez. Cada nuevo usuario del grupo IMS de Adobe se agrega a ese grupo correspondiente en Experience Manager cuando se conecta al Experience Manager a través de Adobe Asset Link por primera vez.

Los grupos en Experience Manager que se corresponden y se sincronizan con grupos en Adobe IMS pueden obtener acceso directamente o haciéndolos miembros de otro grupo. A continuación se muestra un ejemplo de cómo se pueden administrar los permisos.

![ejemplos de grupo](assets/group-examples.png)

Las siguientes reglas se aplican a las asignaciones de grupo en el Experience Manager:

* Asegúrese de que la variable **[!UICONTROL Asignaciones de grupos]** propiedad en **[!UICONTROL Proveedor de IMS de Adobe Granite OAuth]** está en blanco.
* La pertenencia al grupo de usuarios de Asset Link de Adobe se evalúa cuando el usuario se autentica y el período de tiempo en **[!UICONTROL Hora de caducidad del usuario]** propiedad en **[!UICONTROL Controlador de sincronización predeterminado Apache Jackrabbit Oak]** ha transcurrido. Actualmente, los usuarios se pueden agregar y eliminar de los grupos en Experience Manager para sincronizar con lo que se encuentra en Adobe IMS.
* Evite conflictos de nombres de grupos. Asegúrese de que los nombres utilizados para los grupos creados en Adobe IMS (para administrar usuarios) son diferentes de todos los nombres de grupos del sistema del Experience Manager.

   Por ejemplo, asegúrese de que son diferentes de la variable `dam-users` y los grupos creados por el administrador del Experience Manager.

   Un grupo IMS de Adobe cuyo nombre esté en conflicto con el nombre de un grupo de sistema de Experience Manager o un grupo creado manualmente no se utiliza para controlar los permisos de usuario.
* Si un usuario de IMS de Adobe se conecta a una instancia de Experience Manager, en la que el nombre del usuario entra en conflicto con un usuario de Experience Manager creado anteriormente, se asigna otro nombre al usuario de IMS de Adobe con números agregados para que sea único.

**Configuración del control de acceso por primera vez**

Los usuarios que se conectan mediante Adobe Asset Link solo pueden ver e interactuar con los recursos después de que se les haya concedido el permiso necesario. La variable [Asignación de grupos](#group-mapping) sección anterior describe cómo se crean los grupos de usuarios en Experience Manager, que se corresponden y se sincronizan con los grupos de usuarios de su organización en Adobe IMS. Se recomienda que los administradores del Experience Manager utilicen estos grupos para administrar el control de acceso de los usuarios de Adobe Asset Link.

Para cada grupo de Experience Manager sincronizado con un grupo IMS de Adobe (que se utiliza para administrar el control de acceso de los usuarios):

1. Asegúrese de que el grupo tenga un miembro que pueda utilizarse para una conexión inicial desde Adobe Asset Link.
1. Utilice ese usuario para iniciar sesión en Adobe Asset Link y conectarse al Experience Manager. Se espera que esta conexión falle.
1. En Experience Manager, localice el grupo que corresponde al grupo en Adobe IMS y asígnele el control de acceso deseado. Por ejemplo, el nuevo grupo se convierte en miembro del grupo dam-users.
1. Cierre Adobe Asset Link y reinicie la aplicación Creative Cloud.
1. Para comprobar que el usuario tiene el acceso esperado, vuelva a abrir Adobe Asset Link.

Una vez realizados estos pasos, otros usuarios del mismo grupo pueden conectarse al Experience Manager con Adobe Asset Link en su primer intento. Tienen automáticamente los mismos permisos que los demás usuarios del grupo.

## Administrar usuarios de Experience Manager para Adobe Asset Link {#manage-users}

Los usuarios de Adobe Asset Link pueden conectarse con Experience Manager cuando inician sesión en su aplicación Creative Cloud. Esta autenticación utiliza la tecnología IMS de Adobe y crea información de usuario en Experience Manager, si no existe. Es habitual que los clientes empresariales Experience Manager administren a sus usuarios con un proveedor de identidad externo que esté integrado con el Experience Manager. Los proveedores de identidad incluyen Adobe IMS y otros productos que utilizan los protocolos SAML y LDAP. Como alternativa, los usuarios se pueden crear y administrar localmente en Experience Manager.

Los usuarios que se conectan al Experience Manager desde Adobe Asset Link no tienen ningún conflicto con la información de usuario existente almacenada en el Experience Manager desde el inicio de sesión directo anterior, si:

* Todos los nombres de usuario utilizados para el inicio de sesión directo en el Experience Manager son diferentes de los nombres de usuario utilizados en Adobe IMS para el inicio de sesión del Creative Cloud.
* Adobe IMS se utiliza como proveedor de identidad para el inicio de sesión del Experience Manager directo.
* Los usuarios se conectan al Experience Manager desde Adobe Asset Link antes del inicio de sesión del Experience Manager directo con la misma cuenta.


Por otro lado, la información de usuario creada como resultado del inicio de sesión directo del Experience Manager debe actualizarse para que funcione con Adobe Asset Link, en los siguientes casos:

* El mismo nombre de usuario, como la dirección de correo electrónico del usuario, se utiliza para ambas: la cuenta en el Creative Cloud, que utiliza Adobe IMS, y la cuenta en un proveedor de identidad externo que no sea Adobe IMS.
* Se utiliza el mismo nombre de usuario para ambos: la cuenta en Creative Cloud y una cuenta de Experience Manager local.
* Las cuentas de Creative Cloud de Adobe IMS son Federated ID, que se proporcionan mediante el mismo proveedor de identidad externo que se integra con Experience Manager para el inicio de sesión directo.

Los usuarios creados mediante estos escenarios no tienen una propiedad requerida para los usuarios, que se sincroniza con Adobe IMS.

Para actualizar a estos usuarios en Experience Manager para que trabajen con Adobe Asset Link:

1. En la consola web del Experience Manager, busque **[!UICONTROL Configuración principal externa de Apache Jackrabbit Oak]** y haga clic en para editarla. Anule la selección de **[!UICONTROL Protección de identidad externa]** y haga clic en **[!UICONTROL Guardar]**.
1. Para acceder a la interfaz de Administración de usuarios en Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**. Seleccione el usuario que desea actualizar y anote el final de la ruta URL de su explorador para ese usuario, empezando por `/home/users`. Alternativamente, puede buscar el nombre de usuario en CRXDE. Una ruta de usuario de muestra: `/home/users/x/xTac082TDh-guJzzG7WM`.
1. En CRXDE, vaya a la ruta del usuario, seleccione el nodo de usuario y vea las propiedades del nodo seleccionando la **[!UICONTROL Propiedades]** en el área inferior central. Este nodo tiene un `jcr:primaryType` valor de propiedad de `rep:User`.
1. En la parte inferior del **[!UICONTROL Propiedades]** , introduzca un `Name` valor de `rep:externalId`, `Type` valor de `String`y `Value` valor de `rep:authorizableId`;`ims`, donde `rep:authorizableId` es el valor de la variable `rep:authorizableId` propiedad del nodo . (Se usa un punto y coma sin espacios para separar el `rep:authorizableId` valor de `ims`.)
1. Haga clic en el **[!UICONTROL Agregar]** a la derecha de la nueva entrada y, a continuación, haga clic en **[!UICONTROL Guardar todo]**.
1. Repita los pasos del 2 al 5 para cualquier otro usuario que desee actualizar para que funcione con Adobe Asset Link.
1. En la consola web del Experience Manager, busque **[!UICONTROL Configuración principal externa de Apache Jackrabbit Oak]** y haga clic en para editarla. Anule la selección de **[!UICONTROL Protección de identidad externa]** y haga clic en **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Si los servicios no se restauran en unos minutos, reinicie el Experience Manager para permitir autenticaciones correctas.

Después de este cambio, un usuario Experience Manager actualizado puede conectarse con Adobe Asset Link y seguir utilizando el método de inicio de sesión directo en el Experience Manager que se utilizó antes de la actualización. Cuando la autenticación se realiza correctamente con Adobe IMS, la información del perfil de usuario del Experience Manager se sincroniza con el perfil de usuario en Adobe IMS.

Existe un método mediante el cual se puede realizar una migración masiva de varios usuarios Experience Manager para permitirles trabajar con Adobe Asset Link. Póngase en contacto con el servicio de atención al Adobe para obtener más información y ayuda sobre cómo habilitar esta opción.

Como alternativa a los pasos, en determinadas circunstancias, un usuario de Asset Link de Adobe puede tener acceso rápido al Experience Manager. En estos casos, la información de usuario preexistente se encuentra y elimina con el Experience Manager User Management o el Experience Manager CRXDE antes de su conexión con Adobe Asset Link. La nueva información de usuario se crea en el Experience Manager después de la conexión. Utilice este método solo si está seguro de que no hay datos importantes que se agreguen como elementos secundarios del nodo de usuario. Estos datos adicionales son cualquier nodo que es el nodo secundario del nodo de usuario que no sea `tokens`, `preferences`, `profile`, `profiles`, `profiles/public`y `rep:policy/*` nodos.

## Flujo de trabajo de inicio automático para procesar recursos de forma condicional {#auto-start-workflow}

En Experience Manager 6.4 y Experience Manager 6.5, los administradores pueden configurar flujos de trabajo para ejecutar y procesar automáticamente recursos en función de condiciones predefinidas.

La configuración es útil para los usuarios de la línea de negocios y los especialistas en marketing, por ejemplo, para crear un flujo de trabajo personalizado en algunas carpetas específicas. Digamos que todos los activos de la sesión fotográfica de una agencia pueden estar marcados con agua o que todos los activos cargados por un profesional independiente pueden procesarse para crear representaciones específicas.

Para obtener más información y para la configuración del Experience Manager, consulte [flujo de trabajo de ejecución automática en recursos](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html#auto-execute-workflow-on-some-assets).


## Crear un índice personalizado en las versiones de Experience Manager 6.4.x {#create-custom-index}

Experience Manager contiene índices que se utilizan para la consulta. Cree el siguiente índice personalizado para la versión especificada. El Experience Manager 6.5.0 contiene este índice de forma predeterminada. Adobe Asset Link requiere este índice para determinar qué recursos ha retirado un usuario.

1. En CRXDE, busque `/oak:index` nodo . Creación de un nodo denominado `cqDrivelock` y establezca su `Type` a `oak:QueryIndexDefinition`.

1. Agregue las siguientes propiedades al nuevo nodo y guarde los cambios:

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## Configurar la búsqueda visual o de similitud {#configure-visual-similarity-search}

La función Búsqueda visual permite buscar recursos visualmente similares en el repositorio de AEM Assets mediante el panel Vínculo de recursos de Adobe . La funcionalidad está disponible en las versiones 6.5.0 o posteriores y solo se buscan los recursos indexados. Para obtener más información, consulte [configuración de la búsqueda visual](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## Generar solo para ubicación representaciones para Adobe InDesign {#fpo-renditions}

Experience Manager proporciona representaciones que se utilizan solo para la colocación (FPO). Estas representaciones de FPO tienen un tamaño de archivo pequeño, pero tienen la misma proporción de aspecto. Si una representación de FPO no está disponible para un recurso, Adobe InDesign utiliza el recurso original en su lugar. Este mecanismo de reserva garantiza que el flujo de trabajo creativo se ejecute sin interrupciones. Para obtener más información, consulte [generar representaciones de FPO](/help/assets/configure-fpo-renditions.md).


## Integración con Adobe Stock {#adobe-stock-integration}

Las organizaciones integran sus cuentas de Adobe Stock con Experience Manager Assets. Ayuda a los especialistas en marketing a poner a disposición de sus proyectos creativos y de marketing fotos, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad y sin derechos de autor. Los profesionales creativos pueden utilizar estos recursos mediante el panel Asset Link.

Para integrarlo con Adobe Stock, consulte [Recursos de Adobe Stock en Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md). Se necesita Experience Manager 6.4.2 o posterior para la integración con Adobe Stock.


## Solución de problemas relacionados con el Experience Manager {#troubleshoot}


Si tiene problemas al configurar o usar Adobe Asset Link, pruebe lo siguiente:

* Asegúrese de que la implementación cumpla los requisitos previos. Concretamente, asegúrese de que están instalados los paquetes o paquetes de funciones adecuados.
* Póngase en contacto con el socio de su organización o con el integrador de sistemas.
* Si los usuarios del Creative Cloud no pueden comprobarlo en los recursos desprotegidos, compruebe si hay mayúsculas y minúsculas en los nombres de dominio en los ID de correo electrónico. Para solucionarlo, consulte [configuración manual](#manual-configuration).
* Para obtener más información, consulte [resolución de problemas de Asset Link](https://helpx.adobe.com/enterprise/kb/asset-link-troubleshooting.html).


>[!MORELIKETHIS]
>
>* [Acerca de Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Uso de Asset Link en la aplicación de escritorio de Creative Cloud y administración de recursos](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [Configuración as a Cloud Service de Adobe Experience Manager Assets](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html).






