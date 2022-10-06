---
title: Instalación y configuración de Interactive Communications
seo-title: Install and configure Interactive Communications
description: Instale y configure AEM Forms Interactive Communications para crear correspondencia comercial, documentos, declaraciones, avisos de beneficios, correos de marketing, facturas y kits de bienvenida.
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
role: Admin
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1385'
ht-degree: 8%

---

# Instalación y configuración de Interactive Communications{#install-and-configure-interactive-communications}

## Introducción {#introduction}

AEM Form tiene la capacidad de centralizar la creación, el ensamblaje, la gestión y el envío de documentos seguros e interactivos, como correspondencia comercial, documentos, declaraciones, avisos de beneficios, correos de marketing, facturas y kits de bienvenida. Esta capacidad se conoce como comunicación interactiva. La funcionalidad se incluye en el paquete de complementos de AEM Forms. El paquete de complementos se implementa en una instancia de Autor o Publicación de AEM.

Puede utilizar la capacidad de comunicación interactiva para producir comunicaciones en varios formatos. Por ejemplo, web y PDF. Puede integrar la comunicación interactiva con AEM flujo de trabajo para procesar y entregar la comunicación ensamblada a los clientes en el canal de su elección. Por ejemplo, enviar una comunicación al usuario final por correo electrónico.

Si está actualizando desde una versión anterior y ya ha invertido en la gestión de correspondencia, puede instalar la variable [paquete de compatibilidad](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) para seguir utilizando la gestión de correspondencia. Para obtener información sobre las diferencias entre la comunicación interactiva y la gestión de correspondencia, consulte [Información general de comunicación interactiva](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

AEM Forms es una potente plataforma de clase empresarial. La comunicación interactiva es solo una de las funciones de AEM Forms. Para obtener la lista completa de funcionalidades, consulte [Introducción a AEM Forms](../../forms/using/introduction-aem-forms.md).

## Topología de implementación {#deployment-topology}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. Solo necesita un mínimo de una instancia de AEM Author and Processing para ejecutar la capacidad de comunicaciones interactivas. La siguiente topología es una topología indicativa para ejecutar AEM Forms Interactive Communications, Correspondence Management, AEM Forms Data Capture y el flujo de trabajo Forms-Centric en las funcionalidades OSGi. Para obtener información detallada sobre la topología, consulte [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topología recomendada](assets/recommended-topology.png)

AEM Forms Interactive Communications ejecuta interfaces de usuario de administración, autoría y agente en las instancias de autor de AEM Forms. Las instancias de publicación alojan la versión final de las comunicaciones interactivas que están listas para el consumo de los usuarios finales.

## Requisitos del sistema {#system-requirements}

Antes de empezar a instalar y configurar las funciones interactivas de comunicación y administración de correspondencia de AEM Forms, asegúrese de que:

* La infraestructura de hardware y software está implementada. Para obtener una lista detallada del hardware y software compatibles, consulte [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* La ruta de instalación de la instancia de AEM no contiene espacios en blanco.
* Se está ejecutando una instancia de AEM. En AEM terminología, una &quot;instancia&quot; es una copia de AEM que se ejecuta en un servidor en modo de autor o publicación. Se necesita al menos una instancia de AEM (Autor o Procesamiento) para ejecutar las funciones de comunicación interactiva y administración de correspondencia de AEM Forms:

   * **Autor**: Instancia de AEM utilizada para crear, cargar y editar contenido y para administrar el sitio web. Una vez que el contenido está listo para su lanzamiento, se duplica en la instancia de publicación.
   * **Procesando:** Una instancia de procesamiento es [Autor de AEM enriquecido](/help/forms/using/hardening-securing-aem-forms-environment.md) instancia. Puede configurar una instancia de Autor y endurecerla después de realizar la instalación.

   * **Publicación**: Instancia de AEM que sirve el contenido publicado al público a través de Internet o una red interna.

* Se cumplen los requisitos de memoria. El paquete de complementos de AEM Forms requiere:

   * 15 GB de espacio temporal para instalaciones basadas en Microsoft Windows.
   * 6 GB de espacio temporal para instalaciones basadas en UNIX.

* Requisitos adicionales para sistemas basados en UNIX: Si está utilizando el sistema operativo basado en UNIX, instale los siguientes paquetes del medio de instalación del sistema operativo correspondiente.

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>libxcb</td>
   <td>freetype</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuid</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## Instalación del paquete de complementos de AEM Forms {#install-aem-forms-add-on-package}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. El paquete contiene comunicaciones interactivas de AEM Forms, administración de correspondencia y otras funciones. Siga estos pasos para instalar el paquete de complementos:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Pulse **[!UICONTROL Adobe Experience Manager]**, disponible en el menú del encabezado.
1. En el **[!UICONTROL Filtros]** sección:
   1. Select **[!UICONTROL Forms]** de la variable **[!UICONTROL Solución]** lista desplegable.
   2. Seleccione la versión y el tipo del paquete. También puede usar la variable **[!UICONTROL Descargas de búsqueda]** para filtrar los resultados.
1. Pulse el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y toque **[!UICONTROL Descargar]**.
1. Abra [Administrador de paquetes](https://docs.adobe.com/content/help/es/experience-manager-65/administering/contentmanagement/package-manager.html) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

   También puede descargar el paquete a través del vínculo directo enumerado en la [Versiones de AEM Forms](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) artículo.

1. Una vez instalado el paquete, se le pedirá que reinicie la instancia de AEM. **No reinicie el servidor inmediatamente.** Antes de detener el servidor de AEM Forms, espere hasta que los mensajes ServiceEvent REGISTER y ServiceEvent UNREGISTER dejen de aparecer en la variable [AEM-Installation-Directory]/crx-quickstart/logs/error.log y el registro es estable.
1. Repita los pasos del 1 al 7 en todas las instancias de Autor y Publicación.

## Configuraciones posteriores a la instalación {#post-installation-configurations}

AEM Forms tiene algunas configuraciones obligatorias y opcionales. Las configuraciones obligatorias incluyen la configuración de las bibliotecas de BouncyCastle y el agente de serialización. Las configuraciones opcionales incluyen la configuración de Dispatcher y Adobe Target.

### Configuraciones posteriores a la instalación obligatorias {#mandatory-post-installation-configurations}

#### Configuración de las bibliotecas RSA y BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Realice los siguientes pasos en todas las instancias de Autor y Publicación para iniciar y delegar las bibliotecas:

1. Detenga la instancia de AEM subyacente.
1. Abra el [directorio de instalación de AEM]\crx-quickstart\conf\sling.properties para editar.

   Si usa [directorio de instalación de AEM]\crx-quickstart\bin\start.bat para comenzar AEM, edite las propiedades de sling ubicadas en [AEM_root]\crx-quickstart\.

1. Agregue las siguientes propiedades al archivo sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. Guarde y cierre el archivo e inicie la instancia de AEM.
1. Repita los pasos del 1 al 4 en todas las instancias de Autor y Publicación.

#### Configuración del agente de serialización {#configure-the-serialization-agent}

Siga estos pasos en todas las instancias de Autor y Publicación para añadir el paquete a la lista de permitidos:

1. Abra AEM Administrador de configuración en una ventana del explorador. La dirección URL predeterminada es https://&#39;[server]:[puerto]&#39;/system/console/configMgr.
1. Buscar y abrir **Deserialización de la configuración de Firewall**.
1. Agregue la variable **sun.util.calendar** al **lista de permitidos** campo . Haga clic en Guardar.
1. Repita los pasos del 1 al 3 en todas las instancias de Autor y Publicación .

### Configuraciones posteriores a la instalación opcionales {#optional-post-installation-configurations}

#### Instalación del paquete de compatibilidad {#install-compatibility-package}

La comunicación interactiva es el enfoque predeterminado y recomendado para crear comunicaciones con los clientes en AEM 6.5 Forms. Si ha actualizado o migrado desde una versión anterior y planea seguir utilizando letras (Gestión de Correspondencia), instale la variable [Paquete de compatibilidad de AEMFD](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT).

El paquete Compatibilidad con AEMFD le permite utilizar los siguientes recursos de AEM 6.4 Forms, AEM 6.3 Forms y AEM 6.2 Forms en AEM 6.5 Forms:

* Fragmentos de documento
* Cartas
* Diccionarios de datos
* Plantillas y páginas obsoletas de formularios adaptables

#### Configurar Dispatcher {#configure-dispatcher}

Dispatcher es una herramienta de equilibrio de carga o almacenamiento en caché de Adobe Experience Manager que se puede utilizar junto con un servidor web de clase empresarial. Si usa [Dispatcher](https://helpx.adobe.com/es/experience-manager/dispatcher/using/dispatcher-configuration.html)y, a continuación, realice las siguientes configuraciones para AEM Forms:

1. Configure el acceso para AEM Forms:

   Abra el archivo dispatcher.any para editarlo. Vaya a la sección de filtros y añada el siguiente filtro a la sección de filtros:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Guarde y cierre el archivo. Para obtener información detallada sobre los filtros, consulte [Documentación de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configure el servicio de filtros del referente:

   Inicie sesión en el gestor de configuración de Apache Felix como administrador. La dirección URL predeterminada del administrador de configuración es https://&#39;server&#39;:[port_number]/system/console/configMgr. En el **Configuraciones** seleccione **Filtro de referente de Apache Sling** . En el campo Permitir hosts , introduzca el nombre de host del Dispatcher para permitirlo como referente y haga clic en **Guardar**. El formato de la entrada es https://&#39;[server]:[puerto]&#39;.

#### Integrar Adobe Target {#integrate-adobe-target}

Es probable que sus clientes abandonen una comunicación interactiva si la experiencia que ofrece no es atractiva. Aunque resulta frustrante para los clientes, también puede aumentar el volumen y el coste de asistencia para su organización. Es fundamental y difícil identificar y ofrecer la experiencia correcta del cliente que aumenta la tasa de conversión. AEM formularios es la clave de este problema.

AEM formularios se integra con Adobe Target, una solución de Adobe Marketing Cloud, para ofrecer experiencias de cliente personalizadas y atractivas en varios canales digitales. Para utilizar Adobe Target para personalizar una comunicación interactiva, [Integración de Adobe Target con AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### Configuración de la comunicación SSL para el modelo de datos de formulario  {#configure-ssl-communcation-for-form-data-model}

Puede activar la comunicación SSL para el modelo de datos de formulario. Para habilitar la comunicación SSL para el modelo de datos de formulario, antes de iniciar cualquier instancia de AEM Forms, agregue certificados al almacén de confianza de Java de todas las instancias. Puede ejecutar el comando siguiente para añadir los certificados:

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## Pasos siguientes {#next-steps}

Ha configurado un entorno para utilizar capacidades interactivas de comunicación y gestión de correspondencia. Ahora, los pasos para utilizar esta capacidad son:

* [Resumen de la gestión de correspondencia](/help/forms/using/interactive-communications-overview.md)

* [Crear una comunicación interactiva](../../forms/using/create-interactive-communication.md)

* [Crear una carta de gestión de correspondencia](../../forms/using/create-letter.md)
