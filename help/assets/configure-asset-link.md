---
title: Configuración de Experience Manager Assets para Adobe Asset Link
description: Configure Experience Manager Assets para utilizarlo con la extensión Adobe Asset Link para aplicaciones de Creative Cloud.
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
exl-id: 3a9b44d4-1756-4ad5-91df-df8d53e82193
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3060'
ht-degree: 0%

---

# Configuración de Experience Manager Assets para Adobe Asset Link {#adobe-asset-link}

[Adobe Asset Link (AAL)](https://www.adobe.com/es/creativecloud/business/enterprise/adobe-asset-link.html) optimiza la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido. Conecta Adobe Experience Manager Assets con aplicaciones de escritorio de Creative Cloud Adobe InDesign, Adobe Photoshop y Adobe Illustrator. El panel Adobe Asset Link permite a los creativos acceder al contenido almacenado en AEM Assets y modificarlo sin salir de las aplicaciones creativas con las que están más familiarizados.

Para configurar Experience Manager Assets para que se utilice con Asset Link, implemente las siguientes tareas. Utilice la cuenta de Experience Manager administrator para realizar la configuración:

1. Instale los paquetes según sea necesario. Los detalles se encuentran en [requisitos previos](#prerequisites).

1. Configure el Experience Manager [manualmente](#manual-configuration) o usando un [paquete](#configure-using-package).

1. Para asignar usuarios con licencia de Creative Cloud con usuarios de Experience Manager, administra [control de acceso de usuario](#user-access).

1. Cree [índice de consultas personalizado](#create-custom-index), configure [representaciones de FPO](/help/assets/configure-fpo-renditions.md) para el InDesign, configure [integración de Adobe Stock](/help/assets/aem-assets-adobe-stock.md) y configure [búsqueda visual o de similitudes](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## Requisitos previos y compatibilidad con varias funcionalidades {#prerequisites}

Asegúrese de instalar el paquete de servicio y el paquete adecuados según sea necesario. Consulte los siguientes requisitos para cada versión de Experience Manager y para funciones específicas.

| Capacidad de Assets | Versión del Experience Manager y requisitos de soporte |
|--- |--- |
| Asset Link funciona de forma predeterminada | Experience Manager 6.5 y 6.5.2 o posterior. Experience Manager </br> 6.4.4 y 6.4.6 o posterior. El Adobe </br> recomienda instalar el [Service Pack (SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=es) de Experience Manager más reciente antes de usar AAL. |
| Asset Link funciona después de instalar un paquete | Para el Experience Manager 6.4.0 - 6.4.3, instale el paquete [adobe-asset-link-support](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support). |
| Integración de Adobe Stock | Experience Manager 6.4.2 o posterior |
| Búsqueda visual o por similitud | Experience Manager 6.5.0 o posterior |


## Configuración del Experience Manager mediante el paquete de configuración {#configure-using-package}

El Adobe recomienda instalar el paquete de configuración [adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config) para automatizar la mayoría de las tareas de configuración, seguidas de algunas tareas manuales. También puede [configurar manualmente](#manual-configuration).

>[!CAUTION]
>
>Si la instancia de Experience Manager está configurada para el inicio de sesión del usuario con cuentas de IMS de Adobe, no utilice el paquete de configuración. En su lugar, [configure manualmente](#manual-configuration) su instancia de Experience Manager.

1. Para abrir el Administrador de paquetes, en la interfaz web del Experience Manager, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Uso compartido de paquetes]**. Instale el paquete `adobe-asset-link-config`.

1. Acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**. Busque la configuración **[!UICONTROL Proveedor de IMS de Adobe Granite OAuth]** y haga clic para editarla.

   Establezca las siguientes propiedades y guarde los cambios.

   * [!UICONTROL Asignaciones de grupo]: dejar vacío a menos que lo desee. Para obtener más información, consulte [Asignación de grupo](#group-mapping).
   * [!UICONTROL Organización]: escriba el identificador de organización que está usando en Adobe Admin Console. Para obtener más información sobre los identificadores de organización, consulte [Crear grupo de usuarios](https://helpx.adobe.com/enterprise/using/create-aal-user-group.html).

1. Busque la configuración **[!UICONTROL Controlador de autenticación del portador de Granite de Adobe]** y haga clic para editarlo.

   Agregue los ID de cliente **[!UICONTROL InDesignAem2]** a la propiedad de configuración **[!UICONTROL ID de cliente OAuth permitidos]**.


## Configurar el Experience Manager manualmente {#manual-configuration}

Configure el Experience Manager manualmente si decide no utilizar un paquete de configuración o si la implementación del Experience Manager está configurada para admitir el inicio de sesión del usuario con cuentas de IMS de Adobe.

Para configurar manualmente el Experience Manager:

1. Para obtener acceso al administrador de configuración, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**. Seleccione **[!UICONTROL OSGi]** > **[!UICONTROL Configuración]** en el menú de la parte superior.

1. Busque la configuración **[!UICONTROL Proveedor de IMS de Adobe Granite OAuth]** y haga clic para editarla.

   Establezca la siguiente configuración y haga clic en **[!UICONTROL Guardar]**.

   * [!UICONTROL Punto final de autorización]: ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL Extremo de token]: ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL Extremo de perfil]: ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL URL de validación]: ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL Organización]: establecida en el identificador de organización en [Adobe Admin Console](https://adminconsole.adobe.com/).
   * [!UICONTROL Asignaciones de grupos]: déjelo vacío a menos que tenga un caso especial. Para obtener más información, consulte [Asignación de grupo](#group-mapping).

1. Busque la configuración **[!UICONTROL Controlador de autenticación del portador de Granite de Adobe]** y haga clic para editarlo.

   Agregue los siguientes ID de cliente a la propiedad de configuración **[!UICONTROL ID de cliente de OAuth permitidos]**: `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`.

   Para agregar cada `Client ID`, haga clic en `+`. Haga clic en **[!UICONTROL Guardar]** después de agregar todos los identificadores.

1. En la configuración de **[!UICONTROL Proveedor y aplicación OAuth de Adobe Granite]**, inspeccione las instancias existentes de **[!UICONTROL Controlador de autenticación OAuth de Adobe Granite]**. Si encuentra una instancia con el valor `Config ID` de `ims`, utilícela para las instrucciones de este procedimiento. De lo contrario, haga clic en `+` para crear una instancia de configuración. Establezca los siguientes valores de propiedad y haga clic en **[!UICONTROL Guardar]**.

   * [!UICONTROL ID de cliente]: no cambiar
   * [!UICONTROL Secreto de cliente]: No cambiar
   * [!UICONTROL Id. de configuración]: ` ims`
   * [!UICONTROL Ámbito]: `AdobeID, OpenID, read_organizations` (otros valores también pueden estar en la configuración)
   * [!UICONTROL Id. de proveedor]: ` ims`
   * [!UICONTROL Crear usuarios]: ` Checked`
   * [!UICONTROL Propiedad de ID de usuario]: `Email` para la configuración recién creada. De lo contrario, no cambie.

1. Busque la configuración del **[!UICONTROL Controlador de sincronización predeterminado de Apache Jackrabbit Oak]** con el **[!UICONTROL Nombre del controlador de sincronización]** `ims` y haga clic para editarlo.

   Establezca las siguientes propiedades de configuración y haga clic en **[!UICONTROL Guardar]**.

   * [!UICONTROL Tiempo de caducidad del usuario y caducidad de la pertenencia al usuario]: Tiempo en minutos seguido de &#39;m&#39; sin espacio. Por ejemplo, `15m` durante 15 minutos. Para obtener más información, consulte [Asignación de grupo](#group-mapping).
   * [!UICONTROL Inscripción automática de usuario]: No cambiar
   * [!UICONTROL Pertenencia dinámica de usuario]: ` Deslect`

1. Busque la configuración **[!UICONTROL Controlador de autenticación OAuth de Granite de Adobe]** y haga clic para editarlo. Sin realizar ningún cambio, haz clic en **[!UICONTROL Guardar]**.

1. Para ajustar la prioridad relativa del controlador de autenticación del portador, en CRXDE, vaya a `/apps/system/config`. Busque `com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config` y abra su configuración. Al final, agregue `service.ranking=I"-10"`. Guarde los cambios.

   >[!NOTE]
   >
   >Cada solicitud autenticada con un token de portador incurre en la sobrecarga de tres llamadas a Adobe IMS, la sincronización de usuarios y la creación de un token de inicio de sesión en Experience Manager. Para compensar esta sobrecarga, Adobe Asset Link captura el token de inicio de sesión devuelto en la respuesta de Experience Manager y lo envía con solicitudes posteriores. Para que este proceso funcione, se debe ajustar la prioridad relativa del controlador de autenticación del portador.

1. (Opcional) Si los usuarios Experience Manager tienen nombres de dominio en mayúsculas o en mayúsculas y minúsculas en sus ID de correo electrónico, seleccione **[!UICONTROL Cambiar el usuario de bloqueo a minúsculas]** en **[!UICONTROL Configuraciones de la plataforma ACP de Adobe Granite]** en la consola web de Experience Manager.

## Configuración adicional después de la migración a Perfiles de empresa {#configure-migration-activity}

Los usuarios de Adobe Asset Link pueden conectarse a Experience Manager para permitir el inicio de sesión de IMS desde la organización principal de Creative Cloud para empresas (CCE). Experience Manager utiliza los ID de cliente para identificar la organización IMS permitida. Después de la migración a los perfiles empresariales, se debe configurar el ID de cliente y la clave secreta de la organización de IMS en Experience Manager para el controlador de autenticación del portador. Para obtener más información sobre los perfiles de negocio, consulte [introducción de perfiles de Adobe](https://helpx.adobe.com/enterprise/kb/introducing-adobe-profiles.html).

Solo se requiere una configuración adicional si utiliza diferentes organizaciones de Adobe IMS para Experience Manager y Creative Cloud para empresa (CCE) y se establece una relación de confianza de dominio entre estas dos organizaciones.

>[!NOTE]
>
>* La corrección para Perfiles de negocio se proporciona en Experience Manager 6.5.11.0.
>* La configuración existente sigue funcionando si utiliza la misma organización de Adobe IMS con Experience Manager y CCE.


**Requisitos previos**

1. Instancia de Experience Manager en funcionamiento con autenticación de portador configurada para AAL.
1. Instale el siguiente paquete (Service Pack 11) en su instancia de Experience Manager 6.5.

   [Descargar Experience Manager 6.5.11.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. Póngase en contacto con el [!UICONTROL Servicio de atención al cliente] para obtener el ID de cliente y la clave secreta para la autenticación del portador de su organización de IMS.

A continuación se indican las configuraciones adicionales que se requieren después de la migración a los perfiles empresariales:

1. En **[!UICONTROL Proveedor de configuración de Adobe Granite OAuth IMS]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`), establezca:

   * ID de configuración de OAuth (`oauth.configmanager.ims.configid`): `ims` (Verifíquelo una vez, puede que ya lo haya configurado)

   * Entidad propietaria de IMS (`ims.owningEntity`): su ID de organización de IMS

   ![ID de configuración de IMS](assets/bearer-authentication1.png)

1. Abra la configuración de **[!UICONTROL Controlador de autenticación del portador]** y agregue el ID de cliente obtenido de [!UICONTROL Atención al cliente] a la lista de **[!UICONTROL ID de cliente de OAuth permitidos]**.

   ![Agregar ID de cliente](assets/add-clientid-bearer-auth.png)

1. Abra la configuración **[!UICONTROL Proveedor y aplicación OAuth de Adobe Granite]** y agregue el **[!UICONTROL ID de cliente]** y el **[!UICONTROL Secreto de cliente]** (Clave secreta) obtenidos del Servicio de atención al cliente.

   Asegúrese de que el campo **[!UICONTROL Id. de configuración]** (`oauth.config.id`) contenga el mismo valor proporcionado en el campo **[!UICONTROL Id. de configuración de OAuth]** (`oauth.configmanager.ims.configid`) anterior.

   ![Verificar ID de cliente](assets/clientid-secretkey.png)

1. Abra la configuración del **[!UICONTROL Preprocesador de token de intercambio de clúster de Granite IMS de Adobe]** y establézcala en `enable`.

## Administrar el control de acceso de usuario {#user-access}

En esta sección se describe cómo administrar usuarios y su acceso al repositorio de Experience Manager.

### Asignación de grupos {#group-mapping}

La asignación de grupos determina cómo se corresponden los grupos de Experience Manager con los grupos de IMS de Adobe. Desempeña un papel importante en la forma en que se concede permiso a los usuarios de Adobe Asset Link para acceder a Experience Manager Assets.

Cuando se utiliza con Adobe Asset Link, el Experience Manager delega las funciones de administración de usuarios en Adobe IMS. Crea automáticamente usuarios y grupos que se corresponden con los usuarios y grupos de Adobe IMS. Además, sincroniza usuarios, grupos y miembros de grupos en Experience Manager para que coincidan con los de Adobe IMS.

Por ejemplo, imaginemos un escenario en el que los usuarios de Adobe Asset Link sean miembros del grupo de IMS de Adobe assetlink-users. En este caso, se crea un grupo sincronizado denominado assetlink-users en Experience Manager cuando un usuario de ese grupo de IMS de Adobe se conecta a Adobe Asset Link por primera vez. Cada nuevo usuario del grupo de IMS de Adobe se agrega al grupo correspondiente en Experience Manager cuando se conecta a Experience Manager a través de Adobe Asset Link por primera vez.

A los grupos de Experience Manager que corresponden a grupos de Adobe IMS y están sincronizados con ellos se les puede otorgar acceso directamente o haciéndolos miembros de otro grupo. A continuación, se muestra un ejemplo de cómo se pueden administrar los permisos.

![ejemplos de grupo](assets/group-examples.png)

Las siguientes reglas se aplican a las asignaciones de grupo en Experience Manager:

* Asegúrese de que la propiedad **[!UICONTROL Asignaciones de grupo]** de la configuración del proveedor de IMS de **[!UICONTROL Adobe Granite OAuth]** esté en blanco.
* La pertenencia al grupo de usuarios de Adobe Asset Link se evalúa cuando el usuario se autentica y ha transcurrido el período de tiempo de la propiedad **[!UICONTROL Hora de caducidad del usuario]** en la configuración de **[!UICONTROL Apache Jackrabbit Oak Default Sync Handler]**. Actualmente, los usuarios se pueden añadir y eliminar de grupos en Experience Manager para sincronizar con lo que se encuentra en Adobe IMS.
* Evite conflictos de nombres de grupo. Asegúrese de que los nombres utilizados para los grupos creados en Adobe IMS (para administrar usuarios) sean diferentes de todos los nombres de grupos del sistema del Experience Manager.

  Por ejemplo, asegúrese de que son diferentes del grupo `dam-users` y de los grupos creados por el administrador del Experience Manager.

  Un grupo de IMS de Adobe cuyo nombre entra en conflicto con el de un grupo de sistema de Experience Manager o un grupo creado manualmente no se utiliza para controlar los permisos de usuario.
* Si un usuario de IMS de Adobe se conecta a una instancia de Experience Manager, en la que el nombre del usuario entra en conflicto con un usuario de Experience Manager creado anteriormente, se le asigna otro nombre con números añadidos para que sea único.

**Configurar el control de acceso por primera vez**

Los usuarios que se conectan mediante Adobe Asset Link solo pueden ver los recursos e interactuar con ellos una vez que se les haya concedido el permiso necesario. La sección [Asignación de grupos](#group-mapping) anterior describe cómo se crean los grupos de usuarios en Experience Manager, que se corresponden con los grupos de usuarios de su organización en Adobe IMS y se sincronizan con ellos. Se recomienda que los administradores de Experience Manager utilicen estos grupos para administrar el control de acceso de los usuarios de Adobe Asset Link.

Para cada grupo de Experience Manager sincronizado con un grupo de IMS de Adobe (que se utiliza para administrar el control de acceso de los usuarios):

1. Asegúrese de que el grupo tenga un miembro que pueda utilizarse para una conexión inicial desde Adobe Asset Link.
1. Utilice ese usuario para iniciar sesión en Adobe Asset Link y conectarse al Experience Manager. Se espera que esta conexión falle.
1. En Experience Manager, busque el grupo que corresponda al grupo en Adobe IMS y asígnele el control de acceso deseado. Por ejemplo, el nuevo grupo pasa a ser miembro del grupo dam-users.
1. Cierre Vínculo de recursos de Adobe y reinicie la aplicación de Creative Cloud.
1. Para comprobar que el usuario tiene el acceso esperado, vuelva a abrir Adobe Asset Link.

Una vez realizados estos pasos, otros usuarios del mismo grupo pueden conectarse a Experience Manager con Adobe Asset Link en su primer intento. Automáticamente tienen los mismos permisos que los demás usuarios del grupo.

## Administrar usuarios de Experience Manager para Vínculo de recursos de Adobe {#manage-users}

Los usuarios de Adobe Asset Link pueden conectarse con Experience Manager cuando inician sesión en la aplicación de Creative Cloud. Esta autenticación utiliza la tecnología IMS de Adobe y crea información de usuario en Experience Manager, si no existe. Es habitual que los clientes empresariales de Experience Manager administren sus usuarios con un proveedor de identidad externo integrado con Experience Manager. Los proveedores de identidad incluyen Adobe IMS y otros productos que utilizan los protocolos SAML y LDAP. Alternativamente, los usuarios se pueden crear y administrar localmente en Experience Manager.

Los usuarios que se conectan al Experience Manager desde Adobe Asset Link no entran en conflicto con la información de usuario existente almacenada en Experience Manager desde el inicio de sesión directo anterior, en los casos siguientes:

* Todos los nombres de usuario utilizados para el inicio de sesión directo en Experience Manager son diferentes de los nombres de usuario utilizados en Adobe IMS para el inicio de sesión de Creative Cloud.
* Adobe IMS se utiliza como proveedor de identidad para el inicio de sesión directo del Experience Manager.
* Los usuarios se conectan al Experience Manager desde Adobe Asset Link antes de iniciar sesión directamente con el Experience Manager con la misma cuenta.


Por otro lado, la información de usuario creada como resultado del inicio de sesión del Experience Manager directo debe actualizarse para que funcione con Adobe Asset Link, en los siguientes casos:

* El mismo nombre de usuario, como la dirección de correo electrónico del usuario, se utiliza para ambos: la cuenta en Creative Cloud, que utiliza Adobe IMS, y la cuenta en un proveedor de identidad externo que no sea Adobe IMS.
* Se utiliza el mismo nombre de usuario para ambos: la cuenta en Creative Cloud y una cuenta de Experience Manager local.
* Las cuentas de Creative Cloud en Adobe IMS son Federated ID, que son proporcionadas por el mismo proveedor de identidad externo que se ha integrado con Experience Manager para el inicio de sesión directo.

Los usuarios creados a través de estos escenarios no tienen una propiedad que sea necesaria para los usuarios, los cuales se sincronizan con Adobe IMS.

Para actualizar a estos usuarios en Experience Manager para que trabajen con Adobe Asset Link:

1. En la consola web del Experience Manager, busque la configuración de **[!UICONTROL Configuración principal externa de Apache Jackrabbit Oak]** y haga clic para editarla. Anule la selección de la casilla **[!UICONTROL Protección de identidad externa]** y haga clic en **[!UICONTROL Guardar]**.
1. Para obtener acceso a la interfaz de administración de usuarios en Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**. Seleccione el usuario que desea actualizar y anote el final de la ruta URL del explorador para ese usuario, empezando por `/home/users`. También puede buscar el nombre de usuario en CRXDE. Ruta de acceso de usuario de ejemplo: `/home/users/x/xTac082TDh-guJzzG7WM`.
1. En CRXDE, vaya a la ruta del usuario, seleccione el nodo del usuario y vea las propiedades del nodo seleccionando la pestaña **[!UICONTROL Propiedades]** en el área inferior central. Este nodo tiene un valor de propiedad `jcr:primaryType` de `rep:User`.
1. En la parte inferior del área de la ficha **[!UICONTROL Propiedades]**, escriba un valor `Name` de `rep:externalId`, un valor `Type` de `String` y un valor `Value` de `rep:authorizableId`;`ims`, donde `rep:authorizableId` es el valor de la propiedad `rep:authorizableId` del nodo. (Se utiliza un punto y coma sin espacios para separar el valor `rep:authorizableId` de `ims`.)
1. Haga clic en el botón **[!UICONTROL Agregar]** a la derecha de la nueva entrada y, a continuación, haga clic en **[!UICONTROL Guardar todo]**.
1. Repita los pasos del 2 al 5 con los demás usuarios que desee actualizar para que funcionen con Adobe Asset Link.
1. En la consola web del Experience Manager, busque la configuración de **[!UICONTROL Configuración principal externa de Apache Jackrabbit Oak]** y haga clic para editarla. Anule la selección de la casilla **[!UICONTROL Protección de identidad externa]** y haga clic en **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Si los servicios no se restauran en unos minutos, reinicie el Experience Manager para permitir autenticaciones correctas.

Después de este cambio, un usuario Experience Manager actualizado puede conectarse con Adobe Asset Link y seguir utilizando el método de inicio de sesión directo en Experience Manager que se utilizó antes de la actualización. Si la autenticación con Adobe IMS se realiza correctamente, la información del perfil de usuario del Experience Manager se sincroniza con el perfil de usuario en Adobe IMS.

Existe un método mediante el cual se puede realizar una migración masiva de varios usuarios de Experience Manager para permitirles trabajar con Adobe Asset Link. Póngase en contacto con el Servicio de atención al Adobe para obtener más información y ayuda con la activación de esta opción.

Como alternativa a los pasos, en determinadas circunstancias, se puede proporcionar a un usuario de Adobe Asset Link un acceso rápido a Experience Manager. En estos casos, la información de usuario preexistente se encuentra y elimina con la administración de usuarios de Experience Manager o la CRXDE de Experience Manager antes de su conexión con Adobe Asset Link. La nueva información de usuario se crea en el Experience Manager después de la conexión. Utilice este método solo si está seguro de que no hay datos importantes que se agreguen como secundarios del nodo de usuario. Estos datos adicionales son cualquier nodo que sea secundario del nodo del usuario distinto de los nodos `tokens`, `preferences`, `profile`, `profiles`, `profiles/public` y `rep:policy/*`.

## Flujo de trabajo de inicio automático para procesar recursos de forma condicional {#auto-start-workflow}

En Experience Manager 6.4 y Experience Manager 6.5, los administradores pueden configurar flujos de trabajo para ejecutar y procesar recursos automáticamente en función de condiciones predefinidas.

La configuración es útil para usuarios y especialistas en marketing de línea de negocios, por ejemplo, para crear un flujo de trabajo personalizado en unas pocas carpetas específicas. Supongamos que todos los activos de la sesión fotográfica de una agencia pueden marcarse como agua o que todos los activos cargados por un freelancer pueden procesarse para crear representaciones específicas.

Para obtener más información y para la configuración del Experience Manager, consulte [flujo de trabajo de ejecución automática en los recursos](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html#auto-execute-workflow-on-some-assets).


## Crear un índice personalizado en las versiones de Experience Manager 6.4.x {#create-custom-index}

El Experience Manager contiene índices que se utilizan para consultas. Cree el siguiente índice personalizado para la versión especificada. Experience Manager 6.5.0 contiene este índice de forma predeterminada. Adobe Asset Link requiere este índice para determinar qué recursos ha retirado un usuario.

1. En CRXDE, busque el nodo `/oak:index`. Cree un nodo denominado `cqDrivelock` y establezca su `Type` en `oak:QueryIndexDefinition`.

1. Agregue las siguientes propiedades al nuevo nodo y guarde los cambios:

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## Configurar la búsqueda visual o de similitudes {#configure-visual-similarity-search}

La funcionalidad Búsqueda visual permite buscar recursos visualmente similares en el repositorio de AEM Assets mediante el panel Vínculo de recursos de Adobe. La funcionalidad está disponible en 6.5.0 o versiones posteriores y solo se buscan los recursos indexados. Para obtener más información, vea [cómo configurar la búsqueda visual](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## Generar representaciones solo para ubicación para Adobe InDesign {#fpo-renditions}

Experience Manager proporciona representaciones que se utilizan solo para la ubicación (FPO). Estas representaciones de FPO tienen un tamaño de archivo pequeño, pero son de la misma proporción de aspecto. Si una representación de FPO no está disponible para un recurso, Adobe InDesign utiliza el recurso original en su lugar. Este mecanismo de reserva garantiza que el flujo de trabajo creativo se desarrolle sin interrupciones. Para obtener más información, vea [generar representaciones de FPO](/help/assets/configure-fpo-renditions.md).


## Integración con Adobe Stock {#adobe-stock-integration}

Las organizaciones integran sus cuentas de Adobe Stock con Experience Manager Assets. Ayuda a los especialistas en marketing a poner a disposición de sus proyectos creativos y de marketing fotografías, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad y libres de derechos de autor. Los profesionales creativos pueden utilizar estos recursos mediante el panel Asset Link.

Para integrar con Adobe Stock, consulte [Recursos de Adobe Stock en Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md). Se requiere el Experience Manager 6.4.2 o posterior para la integración con Adobe Stock.


## Solucionar problemas relacionados con el Experience Manager {#troubleshoot}


Si tiene problemas al configurar o utilizar Adobe Asset Link, intente lo siguiente:

* Asegúrese de que la implementación cumpla los requisitos previos. Concretamente, asegúrese de que están instalados los paquetes de funciones o paquetes adecuados.
* Póngase en contacto con el socio o integrador de sistemas de su organización.
* Si los usuarios de Creative Cloud no pueden comprobar los recursos desprotegidos, compruebe el uso de mayúsculas y minúsculas en los nombres de dominio en los ID de correo electrónico. Para solucionarlo, consulte [configuración manual](#manual-configuration).
* Para obtener más información, consulte [solucionar problemas de Asset Link](https://helpx.adobe.com/enterprise/kb/asset-link-troubleshooting.html).


>[!MORELIKETHIS]
>
>* [Acerca de Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html)
>* [Use Asset Link en la aplicación de escritorio de Creative Cloud y administre recursos](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [Configurar Adobe Experience Manager Assets as a Cloud Service](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html).
