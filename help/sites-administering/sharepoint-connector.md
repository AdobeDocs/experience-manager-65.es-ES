---
title: Conector de SharePoint
seo-title: Conector de SharePoint
description: Day JCR Connector para Microsoft SharePoint 2010 y Microsoft SharePoint 2013, versión 4.0.
seo-description: Obtenga información sobre el conector de Sharepoint en AEM.
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Conector de SharePoint{#sharepoint-connector}

Este artículo incluye detalles sobre el conector JCR de Adobe para Microsoft SharePoint 2010 y Microsoft SharePoint 2013, versión 4.0.

El conector de SharePoint admite las siguientes funciones básicas:

* Lectura de contenido y metadatos desde SharePoint.
* Reconocimiento de la configuración de seguridad de SharePoint para el contenido al que se accede mediante la autenticación y autorización nativas de SharePoint
* Integración de contenido con Content Finder
* Uso de componentes de AEM, como Recursos externos, para mostrar imágenes y vídeos de SharePoint
* Sincronización de SharePoint con AEM Assets

Todas las funcionalidades se implementan usando los servicios web nativos de SharePoint como interfaz para el contenido y los servicios de SharePoint.

>[!NOTE]
>
>SharePoint Connector también es compatible con AEM 6.1 service pack 2. El conector ya no es compatible con el montaje del repositorio virtual y, por lo tanto, no se puede montar. Si desea acceder al repositorio de Sharepoint mediante las API de Java, utilice la implementación del repositorio JCR del conector de Sharepoint en su proyecto.
>
>Las operaciones de instalación, configuración, administración y TI del servidor de SharePoint y la infraestructura de TI relacionada están fuera del ámbito de este documento. Consulte la documentación del proveedor en [SharePoint](https://www.microsoft.com/sharepoint) para obtener información sobre estos temas. El conector requiere que estas partes de la infraestructura estén correctamente instaladas, configuradas y operadas.


## Introducción {#getting-started}

Para comenzar con el conector, haga lo siguiente:

* Asegúrese de que tiene al menos Java 7 instalado.
* Descargue el archivo de distribución de paquetes de conector desde Package Share.
* Copie un archivo *license.properties* válido en el directorio que contiene el archivo *cq-quickstart-6.4.0.jar* .

* Toque o haga doble clic en el archivo .jar para iniciar AEM, o bien iniciarlo desde la línea de comandos.
* Instale el paquete de conector desde el Administrador de paquetes.
* Configure las opciones del conector.

## Instalación del conector de SharePoint {#installing-sharepoint-connector}

El conector es un paquete de contenido que facilita la instalación. Instale el paquete mediante el Administrador de paquetes y, a continuación, establezca la URL del servidor de SharePoint y otras opciones de configuración. El contenido de SharePoint está disponible en el repositorio de AEM.

### Requisitos de instalación {#installation-requirements}

El conector requiere lo siguiente:

* Java Runtime Environment 1.7 o posterior
* Servicios Web de SharePoint disponibles a través de la red
* URL del servidor de SharePoint
* Credenciales de usuario y permisos para repositorios de CRX y SharePoint
* [Plataformas admitidas](#supported-platforms)

El conector de SharePoint está disponible para su descarga desde [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### Plataformas compatibles {#supported-platforms}

El conector admite lo siguiente:

* Versiones de AEM:

   * AEM 6.5, 6.4, 6.3

* Versiones de Microsoft SharePoint:

   * Microsoft Office SharePoint Server (MOSS) 2010
   * Microsoft Office SharePoint Server (MOSS) 2013

* Si necesita asistencia para implementaciones personalizadas del conector (OEM, requisitos especiales, métodos de autenticación personalizados), póngase en contacto con la oficina de Adobe de su región.

>[!NOTE]
>
>El conector solo admite configuraciones oficialmente admitidas por Microsoft. Consulte los requisitos [del sistema MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) y [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx) .

### Instalación estándar {#standard-installation}

Uso compartido de paquetes AEM se utiliza para distribuir funciones de productos, ejemplos y correcciones rápidas. Para obtener más información, consulte la documentación [de Uso compartido de](/help/sites-administering/package-manager.md#package-share)paquetes.

Para acceder a Uso compartido de paquetes en la página de bienvenida de AEM, toque o haga clic en **Herramientas** y, a continuación, seleccione Uso compartido **de paquetes**. Necesita un ID de Adobe válido que incluya la dirección de correo electrónico de su empresa. Además, después de iniciar sesión en su cuenta, solicite el acceso de Uso compartido de paquetes.

#### Integración con AEM {#integrating-with-aem}

Para instalar el paquete de contenido del conector.

1. Abra un ticket de asistencia técnica de Adobe para solicitar la función de conector.
1. Descargue el paquete cuando esté disponible y, a continuación, abra el Administrador de paquetes para su instancia de AEM.
1. Toque o haga clic en **Instalar** en la página de descripción del paquete.
1. En el cuadro de diálogo **Instalar paquete** , toque o haga clic en **Instalar**.

   **Nota**: Asegúrese de haber iniciado sesión como administrador.

1. Cuando el paquete esté instalado, toque o haga clic en **Cerrar**.

## Configuración del conector de SharePoint {#configuring-sharepoint-connector}

Después de instalar el conector de SharePoint, configure la aplicación y las capas de SharePoint para el conector.

Configure la URL del servidor de SharePoint para que el repositorio de SharePoint sea compatible con JCR. Puede establecer parámetros adicionales para configurar la conexión con el servidor de SharePoint. Además, configure la autenticación con el conector de SharePoint.

### Configuración de la conexión con el servidor de SharePoint {#configuring-the-connection-with-the-sharepoint-server}

Para establecer la dirección URL del servidor de SharePoint y las opciones avanzadas, lleve a cabo estos pasos:

1. Vaya a la Consola de administración de OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Busque el **conector JCR de día para el paquete de Microsoft Sharepoint** .
1. Edite los valores de configuración.
1. Establezca la URL de SharePoint Server como el valor de **Workspaces**.
1. Tap/click **Save**.

![chlimage_1-62](assets/chlimage_1-62.png)

Parámetros &#39;Workspaces&#39; y &#39;Default Workspace Name&#39;:

De forma predeterminada, el conector expone un solo espacio de trabajo JCR. El servidor de SharePoint expuesto por este espacio de trabajo se establece mediante el parámetro de configuración &#39;URL del servidor de SharePoint&#39;.

El conector también se puede configurar para varios espacios de trabajo. En este caso, cada área de trabajo está asociada con la dirección URL del servidor de SharePoint correspondiente que se muestra a través del área de trabajo. Para agregar un espacio de trabajo, agregue una definición de espacio de trabajo al parámetro Workspaces. Una definición de espacio de trabajo tiene el siguiente formato:
`<name>`= `<url>` donde`<name>``<url>` es el nombre del espacio de trabajo JCR y es la dirección URL del servidor de SharePoint para ese espacio de trabajo.

En AEM, realice un paso más aparte de los pasos de configuración anteriores. Incluya en la lista blanca el paquete &#39;**com.day.cq.dam.cq-dam-jcr-conectores**&#39;.

Para incluir paquetes en la lista blanca en AEM, lleve a cabo los siguientes pasos:

1. Vaya a la Consola de administración de OSGi: http://localhost:4502/system/console/configMgr.
1. Busque el servicio &quot;Apache Sling Login Admin Whitelist&quot;.
1. Seleccione Omitir la lista blanca.
1. Añada &#39;**com.day.cq.dam.cq-dam-jcr-conectores**&#39; en los paquetes predeterminados de la lista blanca
1. Haga clic en Guardar.

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>Si configura varios espacios de trabajo, especifique el nombre del espacio de trabajo predeterminado en el parámetro Nombre de espacio de trabajo predeterminado.

Para obtener información adicional sobre los parámetros relacionados con la autenticación, consulte [Autenticación](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### Verificación de la configuración de Sharepoint {#verifying-the-sharepoint-setup}

Después de configurar el conector, compruebe lo siguiente:

* Se ejecuta el servidor de SharePoint y la instancia de conector tiene acceso a los servicios Web
* Las credenciales de usuario de SharePoint son válidas y el usuario tiene los permisos de SharePoint necesarios
* El conector está instalado y configurado correctamente

### Configuración de la sincronización DAM con el servidor de SharePoint {#configuring-dam-sync-with-the-sharepoint-server}

Para sincronizar los recursos de SharePoint con AEM, lleve a cabo los siguientes pasos:

1. Vaya a la Consola de administración de OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Busque el servicio &quot;Default DAMAssetSynchronization&quot;.
1. Edite los valores de configuración.
1. Establezca el nombre de usuario y la contraseña correspondiente del usuario que tiene acceso en el sitio de SharePoint.
1. Haga clic en Guardar.

Habilite el servicio de sincronización DAM, que está deshabilitado de forma predeterminada:

1. Vaya a los Componentes de la Consola Web OSGi: [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. Busque &quot;com.day.cq.dam.jcrconectores.impl.AssetSynchronizationService&quot;.
1. Haga clic en Habilitar.

Opcionalmente, puede configurar el retraso de sincronización entre diferentes ciclos de sincronización:

1. Vaya a la Consola de administración de OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. Busque &quot;DAY CQ DAM JCR Connector Asset Synchronization Service&quot;.
1. Edite los valores de configuración.
1. Establezca el valor del período de sincronización (en segundos).
1. Haga clic en Guardar.

### Configuración de la autenticación {#configuring-authentication}

Sharepoint incluye los métodos de autenticación Clásica y Basada en notificaciones, ambos compatibles con los siguientes tipos de autenticación:

* Básico
* Basado en formularios

En particular, están disponibles los siguientes tipos de autenticación:

* Classic-Basic
* Classic-Forms
* Reclamaciones básicas
* Reclamaciones basadas en formularios

Conector JCR de AEM para Microsoft SharePoint 2010 y Microsoft SharePoint 2013, versión 4.0. admite la autenticación basada en notificaciones (que Microsoft sugiere), que funciona en los siguientes modos:

* **Autenticación** básica/NTLM: El conector primero intenta conectarse usando la autenticación básica. Si no está disponible, cambia a la autenticación basada en NTLM.
* **Autenticación** basada en formularios: Sharepoint valida a los usuarios en función de las credenciales que escriben los usuarios en un formulario de inicio de sesión (generalmente una página web). El sistema emite un token para solicitudes autenticadas que contiene una clave para restablecer la identidad de solicitudes posteriores.

**Configuración de la autenticación basada en formularios**

Ir a: [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. Haga clic en OSGI -> Configuración
1. Buscar &quot;Day JCR Connector for Microsoft Sharepoint&quot;
1. Haga clic en &quot;Editar los valores de configuración&quot;
1. Establezca el valor de ‘Fábrica de conexión de Sharepoint’ como ‘com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory’
1. Haga clic en **Guardar**.

**Configuración de la autenticación básica (Windows)**

1. [Deshabilitar la autenticación](#disable-token-authentication)por token.
1. Vaya a [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. Haga clic en OSGI > Configuración.
1. Busque **Day JCR Connector for Microsoft Sharepoint**.
1. Haga clic `Edit the configuration values`.
1. Establezca el valor de la Fábrica de conexiones de Sharepoint en `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`.
1. Haga clic en **Guardar**.

Solo un usuario autenticado tanto en AEM como en SharePoint puede acceder al contenido de SharePoint a través del conector.

También puede utilizar la extensión de conector para la autenticación a fin de crear un módulo de autenticación personalizado que, por ejemplo, asigne el acceso de los usuarios de AEM a usuarios específicos de SharePoint. Cree usuarios de AEM correspondientes a usuarios de SharePoint (el nombre de usuario y la contraseña deben coincidir) para poder ver el contenido de SharePoint asignado a la instancia de conector.

Para crear un usuario en AEM:

1. Inicie sesión en http://localhost:9502/with el usuario administrador.
1. Haga clic en Herramientas.
1. Haga clic en Seguridad.
1. Haga clic en Usuarios.
1. Haga clic en **Crear usuario**.
1. Proporcione el ID de usuario (el nombre de usuario tiene acceso en SharePoint).
1. Proporcione la contraseña correspondiente.
1. Haga clic en el símbolo de visto verde para crear el usuario.

Para agregar el usuario al grupo de administración:

1. Vaya a Administración de grupos.
1. Haga clic en el nodo ‘a’.
1. Haga clic en ‘administradores’.
1. Escriba el ID de usuario creado arriba en el cuadro de texto antes del botón **Examinar** .
1. Haga clic en el símbolo de visto verde para agregar el usuario al grupo de administración.

### Deshabilitar la autenticación por token {#disable-token-authentication}

1. Descargue e instale el paquete `basic auth`. `zip` desde Package Share.

1. Cierre QuickStart.
1. Abra el archivo *\crx-quickstart\repository\repository.xml*.
1. Buscar la etiqueta `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. Inserte la etiqueta `<param name="disableTokenAuth" value="true"/>` dentro de la etiqueta mencionada en el paso 4.
1. Guarde y cierre el archivo xml.
1. Reinicie QuickStart e inicie sesión con sus credenciales.

#### Compatibilidad con diferentes métodos de autenticación del servidor de SharePoint {#supporting-different-authentication-methods-of-the-sharepoint-server}

En su versión estándar, el conector admite la autenticación **Windows** (básica) estándar de IIS y la autenticación basada en formularios (basada en tokens). Los [otros métodos](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2) de autenticación se pueden admitir a través del mecanismo de extensibilidad.

Los siguientes pasos proporcionan instrucciones para ampliar la autenticación estándar a fin de admitir varios métodos de autenticación del servidor de SharePoint:

1. Implementar `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` para gestionar el cliente del proceso de autenticación específico.
1. Instale la `SharepointConnectionFactory` implementación como un paquete de fragmentos con el host de fragmentos `com.day.crx.spi.crx2sharepoint-bundle`.

   Al utilizar Maven, adapte la siguiente configuración de la `maven-bundle-plugin` a los requisitos del proyecto:

   ```xml
              <plugin>
                  <groupId>org.apache.felix</groupId>
                  <artifactId>maven-bundle-plugin</artifactId>
                  <extensions>true</extensions>
                  <configuration>
                      <instructions>
                          <Export-Package />
                          <Private-Package>
                              <!-- your private package here -->
                          </Private-Package>
                          <Fragment-Host>
                              com.day.crx.spi.crx2sharepoint-bundle
                          </Fragment-Host>
                       </instructions>
                  </configuration>
              </plugin>
   ```

1. Registre la implementación `SharepointConnectionFactory` en la configuración del conector. En la ventana de configuración del conector, haga clic en Opciones **avanzadas**. En el campo correspondiente a **la Fábrica** de conexiones de Sharepoint, especifique el nombre de la implementación `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. Reinicie el conector.

