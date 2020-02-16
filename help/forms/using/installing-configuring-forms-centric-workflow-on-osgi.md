---
title: Instalación y configuración del flujo de trabajo centrado en formularios en OSGi
seo-title: Instalación y configuración del flujo de trabajo centrado en formularios en OSGi
description: Instale y configure AEM Forms Interactive Communications para crear correspondencias comerciales, documentos, declaraciones, avisos de beneficios, correos electrónicos de marketing, facturas y kits de bienvenida.
seo-description: Instale y configure AEM Forms Interactive Communications para crear correspondencias comerciales, documentos, declaraciones, avisos de beneficios, correos electrónicos de marketing, facturas y kits de bienvenida.
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# Instalación y configuración del flujo de trabajo centrado en formularios en OSGi{#installing-and-configuring-forms-centric-workflow-on-osgi}

## Introducción {#introduction}

Las empresas recopilan y procesan datos de múltiples formularios, sistemas de back-end y otras fuentes de datos. El procesamiento de datos implica procedimientos de revisión y aprobación, tareas repetitivas y archiving de datos. Por ejemplo, si se revisa un formulario y se convierte a un documento PDF. Cuando se realizan manualmente, las tareas repetitivas pueden llevar mucho tiempo y recursos.

Puede utilizar el flujo de trabajo centrado en [formularios en OSGi](../../forms/using/aem-forms-workflow.md) para crear rápidamente flujos de trabajo adaptables basados en formularios. Estos flujos de trabajo pueden ayudarle a automatizar los flujos de trabajo de revisión y aprobación, los flujos de trabajo de procesos comerciales y otras tareas repetitivas. Estos flujos de trabajo también ayudan a procesar documentos (crear, compilar, distribuir y archivar documentos PDF, agregar firmas digitales para limitar el acceso a documentos, descodificar formularios con códigos de barras, etc.) y utilizar el flujo de trabajo de firma de Adobe Sign con formularios y documentos.

Una vez configurados, estos flujos de trabajo pueden activarse manualmente para completar un proceso definido o ejecutarse mediante programación cuando los usuarios envían un formulario o una comunicación interactiva. La capacidad se incluye en el paquete del complemento AEM Forms.

AEM Forms es una potente plataforma de clase empresarial. El flujo de trabajo centrado en formularios en OSGi es solo una de las funciones de AEM Forms. Para obtener la lista completa de funciones, consulte [Introducción a AEM Forms](../../forms/using/introduction-aem-forms.md).

>[!NOTE]
>
>Con el flujo de trabajo centrado en Forms en OSGi, puede generar e implementar rápidamente flujos de trabajo para diversas tareas en la pila OSGi, sin tener que instalar la capacidad de administración de procesos completa en la pila JEE. Consulte una [comparación](../../forms/using/capabilities-osgi-jee-workflows.md) de los flujos de trabajo de AEM centrados en formularios en OSGi y Process Management en JEE para conocer la diferencia y las similitudes en las funciones.
>
>Después de la comparación, si decide instalar la capacidad de administración de procesos en la pila JEE, consulte [Instalar o actualizar AEM Forms en JEE](/help/forms/home.md) para obtener información detallada sobre la instalación y configuración de la pila JEE y las funciones de administración de procesos.

## Topología de implementación {#deployment-topology}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. Solo se requiere un mínimo de una instancia de AEM Author o de procesamiento (autor de producción) para ejecutar el flujo de trabajo centrado en formularios en la capacidad OSGi.  Una instancia de procesamiento es una instancia de AEM Author [](/help/forms/using/hardening-securing-aem-forms-environment.md) endurecida. No realice ninguna creación real, como crear flujos de trabajo o formularios adaptables, en el autor de la producción.

La siguiente topología es una topología indicativa para ejecutar comunicaciones interactivas de AEM Forms, administración de correspondencia, captura de datos de AEM Forms y flujo de trabajo centrado en formularios en funciones OSGi. Para obtener información detallada sobre la topología, consulte [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topología recomendada](assets/recommended-topology.png)

El flujo de trabajo centrado en los formularios de AEM en OSGi ejecuta la bandeja de entrada de AEM y la interfaz de usuario de creación del modelo de flujo de trabajo de AEM en las instancias de autor de AEM Forms.

## Requisitos del sistema {#system-requirements}

>[!NOTE]
>
>Vaya a la sección [Próximos pasos](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) del documento si ya ha instalado AEM Forms en OSGi, tal como se explica en el artículo [Instalar y configurar funciones](../../forms/using/installing-configuring-aem-forms-osgi.md) de captura de datos.

Antes de empezar a instalar y configurar el flujo de trabajo centrado en formularios en OSGi, asegúrese de que:

* La infraestructura de hardware y software está establecida. Para obtener una lista detallada de hardware y software compatibles, consulte Requisitos [técnicos](/help/sites-deploying/technical-requirements.md).

* La ruta de instalación de la instancia de AEM no contiene espacios en blanco.
* Se está ejecutando una instancia de AEM. En la terminología de AEM, una &quot;instancia&quot; es una copia de AEM que se ejecuta en un servidor en el modo de creación o publicación. Se requiere al menos una instancia de AEM (autor o procesamiento) para ejecutar el flujo de trabajo centrado en formularios en OSGi:

   * **Autor**: Instancia de AEM que se utiliza para crear, cargar y editar contenido y administrar el sitio web. Una vez que el contenido está listo para activarse, se replica en la instancia de publicación.
   * **** Procesamiento: Una instancia de procesamiento es una instancia de AEM Author [](/help/forms/using/hardening-securing-aem-forms-environment.md) endurecida. Puede configurar una instancia de Autor y endurecerla después de realizar la instalación.

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

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. El paquete contiene un flujo de trabajo centrado en Forms en OSGi y otras funciones. Realice los siguientes pasos para instalar el paquete de complemento:

1. Inicie sesión en el servidor [de](https://localhost:4502) AEM como administrador y abra el recurso compartido [de](https://localhost:4502/crx/packageshare)paquetes. Necesita un ID de Adobe para iniciar sesión en el recurso compartido de paquetes.
1. En Uso compartido [de paquetes de](https://localhost:4502/crx/packageshare/login.html)AEM, busque los paquetes de complementos de formularios de **AEM 6.5** o los **paquetes** de servicios más recientes, haga clic en el paquete aplicable a su sistema operativo y, a continuación, haga clic en **Descargar**. Lea y acepte el contrato de licencia y haga clic en **Aceptar**. Se inicia la descarga. Una vez descargado, la palabra **Descargado** aparece junto al paquete.

   También puede utilizar el número de versión para buscar un paquete de complemento. Para ver el número de versión del paquete más reciente, consulte el artículo de la versión [de](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms.

1. Una vez finalizada la descarga, haga clic en **Descargado**. Se le redirige al administrador de paquetes. En el administrador de paquetes, busque el paquete descargado y haga clic en **Instalar**.

   Si descarga manualmente el paquete mediante el vínculo directo que aparece en el artículo de la versión [de AEM Forms, inicie sesión en el administrador de paquetes, haga clic en](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) Cargar paquete ****, seleccione el paquete descargado y haga clic en cargar. Después de cargar el paquete, haga clic en el nombre del paquete y, a continuación, en **Instalar.**

1. Después de instalar el paquete, se le pedirá que reinicie la instancia de AEM. **No reinicie el servidor inmediatamente.** Antes de detener el servidor de AEM Forms, espere hasta que los mensajes ServiceEvent REGISTERED y ServiceEvent UNREGISTER dejen de aparecer en el archivo [AEM-Installation-Directory]/crx-quickstart/logs/error.log y el registro sea estable.
1. Repita los pasos del 1 al 4 en todas las instancias de Autor y Publicación.

## Configuraciones posteriores a la instalación {#post-installation-configurations}

AEM Forms tiene algunas configuraciones obligatorias y opcionales. Las configuraciones obligatorias incluyen la configuración de las bibliotecas de BouncyCastle y el agente de serialización. Las configuraciones opcionales incluyen la configuración de distribuidor y Adobe Target.

### Configuraciones posteriores a la instalación obligatorias {#mandatory-post-installation-configurations}

#### Configuración de bibliotecas RSA y BouncyCastle {#configure-rsa-and-bouncycastle-libraries}

Realice los siguientes pasos en todas las instancias de Autor y Publicación para iniciar las bibliotecas delegadas:

1. Detenga la instancia de AEM subyacente.
1. Abra el directorio [\crx-quickstart\conf\sling.properties de instalación de]AEM para editarlo.

   Si ha utilizado el directorio [de instalación de]AEM\crx-quickstart\bin\start.bat para iniciar AEM, edite el archivo sling.properties ubicado en [AEM_root]\crx-quickstart\.

1. Agregue las siguientes propiedades al archivo sling.properties:

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. Guarde y cierre el archivo e inicie la instancia de AEM.
1. Repita los pasos del 1 al 4 en todas las instancias de Autor y Publicación.

#### Configurar el agente de serialización {#configure-the-serialization-agent}

Realice los siguientes pasos en todas las instancias de Autor y Publicación para incluir el paquete en la lista blanca:

1. Abra AEM Configuration Manager en una ventana del explorador. La dirección URL predeterminada es https://[server]:[port]/system/console/configMgr.
1. Busque y abra **Deserialization Firewall Configuration**.
1. Agregue el paquete **sun.util.calendar** al campo de la **lista blanca** . Haga clic en Guardar.
1. Repita los pasos del 1 al 3 en todas las instancias de Autor y Publicación.

### Configuraciones posteriores a la instalación opcionales {#optional-post-installation-configurations}

#### Configurar Dispatcher {#configure-dispatcher}

Dispatcher es una herramienta de almacenamiento en caché y equilibrio de carga para AEM. AEM Dispatcher también ayuda a proteger el servidor AEM de los ataques. Puede aumentar la seguridad de la instancia de AEM mediante Dispatcher junto con un servidor web de clase empresarial. Si utiliza [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html), realice las siguientes configuraciones para AEM Forms:

1. Configuración del acceso para AEM Forms:

   Abra el archivo dispatcher.any para editarlo. Vaya a la sección de filtros y agregue el siguiente filtro a la sección de filtros:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Guarde y cierre el archivo. Para obtener información detallada sobre los filtros, consulte la documentación [de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configure el servicio de filtros de referente:

   Inicie sesión en el administrador de configuración de Apache Felix como administrador. La dirección URL predeterminada del administrador de configuración es https://[server]:[port_number]/system/console/configMgr. En el menú **Configuraciones** , seleccione la opción Filtro **de referente Sling de** Apache. En el campo Permitir hosts, escriba el nombre de host del despachante para que se pueda utilizar como referente y haga clic en **Guardar**. El formato de la entrada es `https://[server]:[port]`.

#### Configurar caché {#configure-cache}

El almacenamiento en caché es un mecanismo para reducir los tiempos de acceso a los datos, reducir la latencia y mejorar las velocidades de entrada y salida (E/S). La caché de formularios adaptables almacena solo el contenido HTML y la estructura JSON de un formulario adaptable sin guardar datos precargados. Ayuda a reducir el tiempo necesario para procesar un formulario adaptable.

* Al utilizar la caché de formularios adaptables, utilice [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) para almacenar en caché las bibliotecas de cliente (CSS y JavaScript) de un formulario adaptable.
* Al desarrollar componentes personalizados, mantenga la caché de formularios adaptables deshabilitada en el servidor que se utiliza para el desarrollo.

Realice los siguientes pasos para configurar la caché de formularios adaptables:

1. Vaya al administrador de configuración de la consola web de AEM en `https://[server]:[port]/system/console/configMgr`.
1. Haga clic en **Servicio** de configuración de formulario adaptable para editar sus valores de configuración. En el cuadro de diálogo Editar valores de configuración, especifique el número máximo de formularios o documentos que una instancia del servidor de AEM Forms puede almacenar en caché en el campo **Número de formularios** adaptables. El valor predeterminado es 100. Haga clic en **Guardar**.

   >[!NOTE]
   >
   >Para deshabilitar la caché, establezca el valor en **0** en el campo Número de formularios adaptables. La caché se restablece y todos los formularios y documentos se eliminan de la caché cuando se deshabilita o cambia la configuración de la caché.

#### Configurar Adobe Sign {#configure-adobe-sign}

Adobe Sign habilita los flujos de trabajo de firma electrónica para formularios adaptables. Las firmas electrónicas mejoran los flujos de trabajo para procesar documentos para áreas legales, de ventas, de nómina, de gestión de recursos humanos y muchas más.

En un flujo de trabajo típico de Adobe Sign y Forms centrado en OSGi, un usuario rellena un formulario adaptable para **solicitar un servicio**. Por ejemplo, una solicitud de tarjeta de crédito y un formulario de beneficios para el ciudadano. Cuando un usuario rellena, envía y firma el formulario de solicitud, se inicia un flujo de trabajo de aprobación/rechazo. El proveedor de servicios revisa la aplicación en la Bandeja de entrada de AEM y utiliza Adobe Sign para firmar electrónicamente la aplicación. Para habilitar flujos de trabajo de firma electrónica similares, puede integrar Adobe Sign con AEM Forms.

Para utilizar Adobe Sign con AEM Forms, [integre Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## Pasos siguientes {#next-steps}

Ha configurado un entorno para utilizar el flujo de trabajo centrado en formularios en las capacidades de OSGi. Ahora, los pasos hacia el uso de la capacidad son:

* [Uso del flujo de trabajo centrado en formularios en OSGi](../../forms/using/aem-forms-workflow.md)
* [Referencia de pasos de flujo de trabajo](/help/sites-developing/workflows-step-ref.md)
* [Postprocesamiento de cartas y comunicaciones interactivas](../../forms/using/submit-letter-topostprocess.md)

