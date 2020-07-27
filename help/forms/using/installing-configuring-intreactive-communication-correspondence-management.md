---
title: Instalación y configuración de Interactive Communications
seo-title: Instalación y configuración de Interactive Communications
description: Instale y configure AEM Forms Interactive Communications para crear correspondencias comerciales, documentos, declaraciones, avisos de beneficios, correos electrónicos de marketing, facturas y kits de bienvenida.
seo-description: Instale y configure AEM Forms Interactive Communications para crear correspondencias comerciales, documentos, declaraciones, avisos de beneficios, correos electrónicos de marketing, facturas y kits de bienvenida.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 1%

---


# Instalación y configuración de Interactive Communications{#install-and-configure-interactive-communications}

## Introducción {#introduction}

AEM Form permite centralizar la creación, el montaje, la gestión y el envío de documentos interactivos y seguros, como correspondencias comerciales, documentos, declaraciones, avisos de beneficios, correos de marketing, facturas y kits de bienvenida. Esta capacidad se conoce como comunicación interactiva. La capacidad se incluye en el paquete complementario de AEM Forms. El paquete de complemento se implementa en una instancia de creación o publicación de AEM.

Puede utilizar la capacidad de comunicación interactiva para producir comunicaciones en varios formatos. Por ejemplo, web y PDF. Puede integrar la comunicación interactiva con el flujo de trabajo de AEM para procesar y entregar la comunicación ensamblada a los clientes en el canal que deseen. Por ejemplo, enviar una comunicación al usuario final por correo electrónico.

Si está actualizando desde una versión anterior y ya ha invertido en la gestión de correspondencia, puede instalar el paquete [de](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) compatibilidad para continuar utilizando la gestión de correspondencia. Para obtener información sobre las diferencias entre la comunicación interactiva y la administración de correspondencia, consulte Información general sobre la comunicación [interactiva](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

AEM Forms es una potente plataforma de clase empresarial. La comunicación interactiva es sólo una de las capacidades de los AEM Forms. Para obtener la lista completa de las funciones, consulte [Introducción a los AEM Forms](../../forms/using/introduction-aem-forms.md).

## Topología de implementación {#deployment-topology}

El paquete de complemento AEM Forms es una aplicación implementada en AEM. Solo se requiere un mínimo de un AEM Author y una instancia de procesamiento para ejecutar la funcionalidad de comunicaciones interactivas. La siguiente topología es una topología indicativa para ejecutar comunicaciones interactivas de AEM Forms, administración de correspondencia, captura de datos de AEM Forms y flujo de trabajo basado en formularios en las capacidades de OSGi. Para obtener información detallada sobre la topología, consulte [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topología recomendada](assets/recommended-topology.png)

AEM Forms Interactive Communications ejecuta interfaces de administrador, creación y agente en las instancias de autor de AEM Forms. Las instancias de Publicar alojan la versión final de las comunicaciones interactivas que están listas para el consumo de los usuarios finales.

## Requisitos del sistema {#system-requirements}

Antes de comenzar a instalar y configurar las funciones interactivas de comunicación y administración de correspondencia de los AEM Forms, asegúrese de que:

* La infraestructura de hardware y software está establecida. Para obtener una lista detallada del hardware y el software admitidos, consulte los requisitos [técnicos](/help/sites-deploying/technical-requirements.md).

* La ruta de instalación de la instancia de AEM no contiene espacios en blanco.
* Se está ejecutando una instancia de AEM. En la terminología de AEM, una &quot;instancia&quot; es una copia de AEM que se ejecuta en un servidor en el modo de creación o publicación. Se requieren al menos una instancia de AEM (Autor o Procesamiento) para ejecutar las funciones de comunicación interactiva y gestión de correspondencia de los AEM Forms:

   * **Autor**: Instancia de AEM que se utiliza para crear, cargar y editar contenido y administrar el sitio web. Una vez que el contenido está listo para activarse, se replica en la instancia de publicación.
   * **Procesamiento:** Una instancia de procesamiento es una instancia de AEM Author [](/help/forms/using/hardening-securing-aem-forms-environment.md) endurecida. Puede configurar una instancia de Autor y endurecerla después de realizar la instalación.

   * **Publicar**: Instancia de AEM que sirve el contenido publicado al público a través de Internet o de una red interna.

* Se cumplen los requisitos de memoria. El paquete adicional de AEM Forms requiere:

   * 15 GB de espacio temporal para instalaciones basadas en Microsoft Windows.
   * 6 GB de espacio temporal para instalaciones basadas en UNIX.

* Requisitos adicionales para sistemas basados en UNIX: Si utiliza el sistema operativo basado en UNIX, instale los siguientes paquetes desde el medio de instalación del sistema operativo correspondiente.

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
   <td>libXoutput</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## Install AEM Forms add-on package {#install-aem-forms-add-on-package}

El paquete de complemento AEM Forms es una aplicación implementada en AEM. El paquete contiene AEM Forms de comunicación interactiva, administración de correspondencia y otras capacidades. Realice los siguientes pasos para instalar el paquete de complemento:

1. Abra Distribución [de software](https://experience.adobe.com/downloads). Necesita un Adobe ID para iniciar sesión en la distribución de software.
1. Toque **[!UICONTROL Adobe Experience Manager]** disponible en el menú de encabezado.
1. En la sección **[!UICONTROL Filtros]** :
   1. Seleccione **[!UICONTROL Formularios]** en la lista desplegable **[!UICONTROL Solución]** .
   2. Seleccione la versión y escriba el paquete. También puede utilizar la opción **[!UICONTROL Buscar descargas]** para filtrar los resultados.
1. Toque el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar los términos]** del EULA y toque **[!UICONTROL Descargar]**.
1. Abra el Administrador [de paquetes](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Select the package and click **[!UICONTROL Install]**.

   También puede descargar el paquete a través del vínculo directo que aparece en el artículo de versiones [de](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html) AEM Forms.

1. Después de instalar el paquete, se le pedirá que reinicie la instancia de AEM. **No reinicie el servidor inmediatamente.** Antes de detener el servidor de AEM Forms, espere hasta que los mensajes ServiceEvent REGISTERED y ServiceEvent UNREGISTER dejen de aparecer en el archivo [AEM-Installation-Directory]/crx-quickstart/logs/error.log y el registro sea estable.
1. Repita los pasos del 1 al 7 en todas las instancias de Autor y Publicación.

## Configuraciones posteriores a la instalación {#post-installation-configurations}

Los AEM Forms tienen algunas configuraciones obligatorias y opcionales. Las configuraciones obligatorias incluyen la configuración de las bibliotecas de BouncyCastle y el agente de serialización. Las configuraciones opcionales incluyen la configuración del despachante y el Adobe Target.

### Configuraciones posteriores a la instalación obligatorias {#mandatory-post-installation-configurations}

#### Configuración de bibliotecas RSA y BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Realice los siguientes pasos en todas las instancias de Autor y Publicación para iniciar las bibliotecas delegadas:

1. Detenga la instancia de AEM subyacente.
1. Abra el directorio [\crx-quickstart\conf\sling.properties de instalación de]AEM para editarlo.

   Si ha utilizado el directorio [de instalación de]AEM\crx-quickstart\bin\start.bat en inicio AEM, edite el archivo sling.properties ubicado en [AEM_root]\crx-quickstart\.

1. Añada las siguientes propiedades en el archivo sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. Guarde y cierre el archivo y inicio de la instancia de AEM.
1. Repita los pasos del 1 al 4 en todas las instancias de Autor y Publicación.

#### Configurar el agente de serialización {#configure-the-serialization-agent}

Realice los siguientes pasos en todas las instancias de Autor y Publicación para agregar el paquete a la lista de permitidos:

1. Abra AEM Configuration Manager en una ventana del explorador. La dirección URL predeterminada es https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Busque y abra **Deserialization Firewall Configuration**.
1. Añada el paquete **sun.util.calendar** al campo de **lista de permitidos** . Haga clic en Guardar.
1. Repita los pasos del 1 al 3 en todas las instancias de Autor y Publicación.

### Configuraciones posteriores a la instalación opcionales {#optional-post-installation-configurations}

#### Instalar paquete de compatibilidad {#install-compatibility-package}

La comunicación interactiva es el método predeterminado y recomendado para crear comunicaciones con los clientes en AEM 6.5 Forms. Si ha actualizado o migrado desde una versión anterior y planea seguir utilizando letras (Gestión de correspondencia), instale el paquete [de compatibilidad con](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT)AEMFD.

El paquete de compatibilidad con AEMFD le permite utilizar los siguientes recursos de AEM 6.4 Forms, AEM 6.3 Forms y AEM 6.2 Forms en AEM 6.5 Forms:

* Fragmentos de Documento
* Cartas
* Diccionarios de datos
* Plantillas y páginas obsoletas de formularios adaptables

#### Configurar Dispatcher {#configure-dispatcher}

Dispatcher está utilizando la herramienta de almacenamiento en caché y equilibrio de carga para AEM. AEM Dispatcher también ayuda a proteger el servidor AEM de los ataques. Puede aumentar la seguridad de su instancia de AEM mediante el uso de Dispatcher junto con un servidor web de clase empresarial. Si utiliza [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html), realice las siguientes configuraciones para AEM Forms:

1. Configurar el acceso para AEM Forms:

   Abra el archivo dispatcher.any para editarlo. Vaya a la sección de filtros y agregue el siguiente filtro a la sección de filtros:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Guarde y cierre el archivo. Para obtener información detallada sobre filtros, consulte la documentación [de](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)Dispatcher.

1. Configure el servicio de filtros de remitente del reenvío:

   Inicie sesión en el administrador de configuración de Apache Felix como administrador. La dirección URL predeterminada del administrador de configuración es https://&#39;server&#39;:[port_number]/system/console/configMgr. En el menú **Configuraciones** , seleccione la opción Filtro **de Remitente del reenvío Sling de** Apache. En el campo Permitir hosts, escriba el nombre de host del despachante para que se pueda utilizar como remitente del reenvío y haga clic en **Guardar**. El formato de la entrada es https://&#39;[server]:[port]&#39;.

#### Integrar Adobe Target {#integrate-adobe-target}

Es probable que sus clientes abandonen una comunicación interactiva si la experiencia que ofrece no es atractiva. Aunque resulta frustrante para los clientes, también puede aumentar el volumen de asistencia y el costo de su organización. Es fundamental y difícil identificar y proporcionar la experiencia adecuada del cliente que aumenta la tasa de conversión. Los formularios AEM son la clave para este problema.

Los formularios AEM se integran con Adobe Target, una solución de Adobe Marketing Cloud, para ofrecer experiencias personalizadas y atractivas a los clientes en varios canales digitales. Para utilizar Adobe Target para personalizar una comunicación interactiva, [integre Adobe Target con AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### Configurar la comunicación SSL para el modelo de datos de formulario  {#configure-ssl-communcation-for-form-data-model}

Puede habilitar la comunicación SSL para el modelo de datos de formulario. Para habilitar la comunicación SSL para el modelo de datos de formulario, antes de iniciar una instancia de AEM Forms, agregue certificados al almacén de confianza de Java de todas las instancias. Puede ejecutar el comando siguiente para agregar los certificados:

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## Pasos siguientes {#next-steps}

Ha configurado un entorno para utilizar las funciones interactivas de comunicación y administración de correspondencia. Ahora, los pasos hacia el uso de la capacidad son:

* [Información general sobre la gestión de correspondencia](/help/forms/using/interactive-communications-overview.md)

* [Crear una comunicación interactiva](../../forms/using/create-interactive-communication.md)

* [Crear una carta de administración de correspondencia](../../forms/using/create-letter.md)

