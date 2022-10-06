---
title: Conector de SharePoint
seo-title: SharePoint Connector
description: Day JCR Connector para Microsoft SharePoint 2010 y Microsoft SharePoint 2013, versión 4.0.
seo-description: Learn about the Sharepoint Connector in AEM.
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
exl-id: 10ea7d2e-6e44-4d5c-a2b2-63c73b18f172
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 3%

---

# Conector de SharePoint{#sharepoint-connector}

Este artículo incluye detalles sobre el conector JCR de Adobe para Microsoft SharePoint 2010 y Microsoft SharePoint 2013, versión 4.0.

El conector SharePoint admite las siguientes funcionalidades básicas:

* Leer contenido y metadatos desde SharePoint.
* Reconocimiento de la configuración de seguridad de SharePoint para el contenido al que se accede mediante la aplicación de autenticación y autorización nativas de SharePoint
* Integración de contenido con Content Finder
* Uso de componentes de AEM, como Recurso externo para mostrar imágenes y vídeos de SharePoint
* Sincronización de SharePoint con AEM Assets

Todas las funcionalidades se implementan utilizando los servicios web nativos de SharePoint como interfaz para el contenido y los servicios de SharePoint.

>[!NOTE]
>
>SharePoint Connector también es compatible con AEM Service Pack 2 6.1. El conector ya no es compatible con el montaje del repositorio virtual y, por lo tanto, no se puede montar. Si desea acceder al repositorio de Sharepoint mediante API de Java, utilice la implementación del repositorio JCR del conector de Sharepoint en su proyecto.
>
>Las operaciones de instalación, configuración, administración y TI del servidor SharePoint y la infraestructura de TI relacionada están fuera del ámbito de este documento. Consulte la documentación del proveedor en [SharePoint](https://www.microsoft.com/sharepoint) para obtener información sobre estos temas. El conector requiere que estas partes de la infraestructura estén correctamente instaladas, configuradas y operadas.

## Introducción {#getting-started}

Para comenzar con el conector, haga lo siguiente:

* Asegúrese de tener Java 7 instalado como mínimo.
* Descargue el archivo de distribución de paquetes del conector desde Distribución de software.
* Copiar una *license.properties* al directorio que contiene el *cq-quickstart-6.4.0.jar* archivo.

* Toque o haga doble clic en el archivo .jar para iniciarlo AEM o inícielo desde la línea de comandos.
* Instale el paquete del conector desde el Administrador de paquetes.
* Configure las opciones del conector.

## Instalación del conector de SharePoint {#installing-sharepoint-connector}

El conector es un paquete de contenido que facilita la instalación. Instale el paquete mediante el Administrador de paquetes y, a continuación, establezca la URL del servidor de SharePoint y otras opciones de configuración. El contenido de SharePoint está disponible en el repositorio de AEM.

### Requisitos de instalación {#installation-requirements}

El conector requiere lo siguiente:

* Java Runtime Environment 1.7 o posterior
* Servicios Web de SharePoint disponibles a través de la red
* URL del servidor de SharePoint
* Credenciales de usuario y permisos para repositorios CRX y SharePoint
* [Plataformas compatibles](#supported-platforms)

El conector SharePoint está disponible para su descarga desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### Plataformas compatibles {#supported-platforms}

El conector admite lo siguiente:

* AEM versiones:

   * AEM 6.4, 6.3

* Versiones de Microsoft SharePoint:

   * Microsoft Office SharePoint Server (MOSS) 2010
   * Microsoft Office SharePoint Server (MOSS) 2013

* Si necesita soporte para implementaciones personalizadas del conector (OEM, requisitos especiales, métodos de autenticación personalizados), póngase en contacto con la oficina de Adobe de su región.

>[!NOTE]
>
>El conector solo admite configuraciones oficialmente admitidas por Microsoft. Consulte [MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) y [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx) requisitos del sistema.

### Instalación estándar {#standard-installation}

La distribución de software se utiliza para distribuir funciones de productos, ejemplos y correcciones. Para obtener más información, consulte la [Documentación de distribución de software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution).


#### Integración con AEM {#integrating-with-aem}

Para instalar el paquete de contenido del conector.

1. Abra un ticket de soporte de Adobe para solicitar el paquete de funciones del conector.
1. Descargue el paquete cuando esté disponible y, a continuación, abra el Administrador de paquetes para su instancia de AEM.
1. Toque o haga clic **Instalar** en la página de descripción del paquete.
1. En el **Instalación del paquete** cuadro de diálogo, pulsar o hacer clic **Instalar**.

   **Nota**: Asegúrese de haber iniciado sesión como administrador.

1. Cuando el paquete esté instalado, toque o haga clic en **Cerrar**.

## Configuración del conector SharePoint {#configuring-sharepoint-connector}

Después de instalar el conector de SharePoint, configure la aplicación y las capas de SharePoint para el conector.

Establezca la URL del servidor de SharePoint para que su repositorio de SharePoint sea compatible con JCR. Puede establecer parámetros adicionales para configurar la conexión con el servidor de SharePoint. Además, configure la autenticación con el conector SharePoint.

### Configuración de la conexión con el servidor SharePoint {#configuring-the-connection-with-the-sharepoint-server}

Para establecer la URL del servidor de SharePoint y las opciones avanzadas, realice estos pasos:

1. Vaya a la consola de administración de OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Busque la variable **Conector JCR de día para Microsoft Sharepoint** paquete.
1. Edite los valores de configuración.
1. Establezca la URL del servidor de SharePoint como el valor de **Espacios de trabajo**.
1. Toque o haga clic **Guardar**.

![imagen_1-62](assets/chlimage_1-62.png)

Parámetros &quot;Espacios de trabajo&quot; y &quot;Nombre de espacio de trabajo predeterminado&quot;:

De forma predeterminada, el conector expone un único espacio de trabajo JCR. El servidor de SharePoint expuesto por este espacio de trabajo se configura mediante el parámetro de configuración &quot;URL del servidor de SharePoint&quot;.

El conector también se puede configurar para varios espacios de trabajo. En este caso, cada espacio de trabajo está asociado con la URL del servidor SharePoint correspondiente que se expone a través del espacio de trabajo. Para agregar un espacio de trabajo, agregue una definición de espacio de trabajo al parámetro Workspaces . Una definición de espacio de trabajo tiene el siguiente formato:
`<name>`= `<url>` donde
`<name>` es el nombre del espacio de trabajo JCR y
`<url>` es la dirección URL del servidor de SharePoint para ese espacio de trabajo.

En AEM, realice un paso más aparte de los pasos de configuración anteriores. Lista de permitidos de &#39;**com.day.cq.dam.cq-dam-jcr-connectors** paquete &#39;.

Para lista de permitidos de paquetes en AEM, realice los siguientes pasos:

1. Vaya a la consola de administración de OSGi: http://localhost:4502/system/console/configMgr.
1. Busque el servicio &quot;Apache Sling Login Admin Whitelist&quot;.
1. Select **Omitir la lista blanca**.
1. Agregar `com.day.cq.dam.cq-dam-jcr-connectors` en la lista blanca, paquetes predeterminados
1. Haga clic en Guardar.

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>Si configura varios espacios de trabajo, especifique el nombre del espacio de trabajo predeterminado en el parámetro Nombre de espacio de trabajo predeterminado .

Para obtener información adicional sobre los parámetros relacionados con la autenticación, consulte [Autenticación](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### Verificación de la configuración de Sharepoint {#verifying-the-sharepoint-setup}

Después de configurar el conector, compruebe lo siguiente:

* Se ejecuta el servidor de SharePoint y la instancia de conector puede acceder a los servicios web
* Las credenciales de usuario de SharePoint son válidas y el usuario tiene los permisos SharePoint necesarios
* El conector está instalado y configurado correctamente

### Configuración de la sincronización de DAM con el servidor de SharePoint {#configuring-dam-sync-with-the-sharepoint-server}

Para sincronizar los recursos de SharePoint con AEM, realice los pasos siguientes:

1. Vaya a la consola de administración de OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Busque el servicio &quot;Default DAMAsetSynchronization&quot;.
1. Edite los valores de configuración.
1. Establezca el nombre de usuario y la contraseña correspondiente del usuario que tiene acceso al sitio de SharePoint.
1. Haga clic en Guardar.

Habilite el servicio de sincronización de DAM, que está deshabilitado de forma predeterminada:

1. Vaya a los componentes de la consola web OSGi: [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. Busque &quot;com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService&quot;.
1. Haga clic en Habilitar.

De forma opcional, puede configurar el retardo de sincronización entre diferentes ciclos de sincronización:

1. Vaya a la consola de administración de OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. Busque &quot;DAY CQ DAM JCR Connector Asset Synchronization Service&quot;.
1. Edite los valores de configuración.
1. Establezca el valor del periodo de sincronización (en segundos).
1. Haga clic en Guardar.

### Configuración de la autenticación {#configuring-authentication}

Sharepoint incluye los métodos de autenticación Classic y Basada en Reclamaciones, ambos compatibles con los siguientes tipos de autenticación:

* Basic
* Basado en Forms

En particular, están disponibles los siguientes tipos de autenticación:

* Classic-Basic
* Classic-Forms
* Reclamaciones Básicas
* Reclamaciones basadas en Forms

El conector AEM JCR para Microsoft SharePoint 2010 y Microsoft SharePoint 2013, versión 4.0. admite la autenticación basada en notificaciones (que Microsoft sugiere), que funciona en los siguientes modos:

* **Autenticación básica/NTLM**: El conector primero intenta conectarse utilizando la autenticación básica. Si no está disponible, cambia a la autenticación basada en NTLM.
* **Autenticación basada en Forms**: Sharepoint valida a los usuarios según las credenciales que escriban los usuarios en un formulario de inicio de sesión (normalmente una página web). El sistema emite un token para solicitudes autenticadas que contiene una clave para restablecer la identidad en solicitudes posteriores.

**Configuración de la autenticación basada en Forms**

Vaya a: [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. Haga clic en OSGI -> Configuración
1. Buscar &quot;Day JCR Connector for Microsoft Sharepoint&quot;
1. Haga clic en &quot;Editar los valores de configuración&quot;
1. Establezca el valor de &quot;Fábrica de conexión de Sharepoint&quot; como &quot;com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory&quot;.
1. Haga clic en **Guardar**.

**Configuración de la autenticación básica (Windows)**

1. [Deshabilitar la autenticación de tokens](#disable-token-authentication).
1. Vaya a [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. Haga clic en OSGI > Configuración.
1. Buscar **Conector JCR de día para Microsoft Sharepoint**.
1. Haga clic `Edit the configuration values`.
1. Establezca el valor de la Fábrica de conexión de Sharepoint en `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`.
1. Haga clic en **Guardar**.

Solo los usuarios autenticados tanto en AEM como en SharePoint pueden acceder al contenido de SharePoint a través del conector.

También puede utilizar la extensión del conector para la autenticación a fin de crear un módulo de autenticación personalizado, que, por ejemplo, asigna el acceso de los usuarios de AEM a usuarios específicos de SharePoint. Cree AEM usuarios correspondientes a usuarios de SharePoint (el nombre de usuario y la contraseña deben coincidir) para poder ver el contenido de SharePoint asignado a la instancia del conector.

Para crear un usuario en AEM:

1. Inicie sesión en http://localhost:9502/with el usuario administrador.
1. Haga clic en Herramientas.
1. Haga clic en Seguridad.
1. Haga clic en Usuarios.
1. Haga clic en **Crear usuario**.
1. Proporcione el ID de usuario (el nombre de usuario tiene acceso a SharePoint).
1. Proporcione la contraseña correspondiente.
1. Haga clic en el símbolo de visto verde para crear el usuario.

Para agregar el usuario en el grupo de administración:

1. Vaya a Administración de grupos.
1. Haga clic en el nodo &quot;a&quot;.
1. Haga clic en &quot;administradores&quot;.
1. Escriba el ID de usuario creado anteriormente en el cuadro de texto antes de **Examinar** botón.
1. Haga clic en el símbolo de visto verde para agregar el usuario al grupo de administración.

### Deshabilitar la autenticación de tokens {#disable-token-authentication}

1. Descargar e instalar el paquete `basic auth`. `zip` de Distribución de software.

1. Cierre Quickstart.
1. Abra el archivo . *\crx-quickstart\repository\repository.xml*.
1. Buscar la etiqueta `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. Inserción de la etiqueta `<param name="disableTokenAuth" value="true"/>` dentro de la etiqueta mencionada en el paso 4.
1. Guarde y cierre el archivo xml.
1. Reinicie QuickStart e inicie sesión con sus credenciales.

#### Compatibilidad con distintos métodos de autenticación del servidor SharePoint {#supporting-different-authentication-methods-of-the-sharepoint-server}

En su versión estándar, el conector admite el IIS estándar **Windows** autenticación (básica) y autenticación basada en Forms (basada en token). La variable [otros métodos de autenticación](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2) se puede admitir mediante el mecanismo de extensibilidad.

Los siguientes pasos proporcionan directrices sobre la ampliación de la autenticación estándar para que admita varios métodos de autenticación del servidor SharePoint:

1. Implementación `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` para gestionar el lado del cliente de su proceso de autenticación específico.
1. Instale el `SharepointConnectionFactory` implementación como paquete de fragmentos con host de fragmentos `com.day.crx.spi.crx2sharepoint-bundle`.

   Al utilizar Maven, adapte la siguiente configuración de la variable `maven-bundle-plugin` a los requisitos del proyecto:

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

1. Registre el `SharepointConnectionFactory` en la configuración del conector. En la ventana de configuración del conector, haga clic en **Opciones avanzadas**. En el para **Fábrica de conexión de Sharepoint** especifique el nombre de la implementación `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. Reinicie el conector.
