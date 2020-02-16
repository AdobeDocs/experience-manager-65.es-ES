---
title: Instalación y configuración de capacidades de captura de datos
seo-title: Instalación y configuración de capacidades de captura de datos
description: Instale y configure formularios adaptables, formularios PDF y formularios HTML5. Configure Adobe Analytics y Adobe Target para formularios adaptables a fin de analizar el uso de formularios y dirigir a los usuarios en función de su perfil.
seo-description: Instale y configure formularios adaptables, formularios PDF y formularios HTML5. Configure Adobe Analytics y Adobe Target para formularios adaptables a fin de analizar el uso de formularios y dirigir a los usuarios en función de su perfil.
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# Instalación y configuración de capacidades de captura de datos{#install-and-configure-data-capture-capabilities}

## Introducción {#introduction}

AEM Forms proporciona un conjunto de formularios para obtener datos del usuario final: formularios adaptables, formularios HTML5 y formularios PDF. También proporciona herramientas para enumerar todos los formularios disponibles en una página web, analizar el uso de los formularios y dirigirse a los usuarios en función de su perfil. Estas funciones se incluyen en el paquete de complementos de AEM Forms. El paquete de complemento se implementa en una instancia de creación o publicación de AEM.

**** Formularios adaptables: Estos formularios cambian de apariencia según el tamaño de pantalla del dispositivo, son atractivos e interactivos. Los formularios adaptables también se pueden integrar con Adobe Analytics, Adobe Sign y Adobe Target. Esto le permitió ofrecer formularios personalizados y experiencias orientadas al proceso a los usuarios en función de su demografía y otras características. También puede integrar formularios adaptables con Adobe Sign.

**Los formularios** PDF son adecuados para una impresión perfecta y la captura de información digital dentro de un documento PDF. En el avatar digital, puede utilizar Adobe Acrobat o Acrobat Reader para rellenar estos formularios. Puede alojar estos formularios en su sitio web o utilizar el portal de formularios para enumerarlos en un sitio de AEM. También puede enviar estos formularios por correo electrónico a otros usuarios como archivos adjuntos. Estos formularios son los más adecuados para entornos de escritorio.

**Los formularios** HTML5 son la versión compatible con el explorador de los formularios PDF. Los formularios HTML5 son adecuados para entornos que no admiten complementos PDF. HTML5 Forms permite procesar formularios basados en XFA en dispositivos móviles y navegadores de escritorio en los que no se admite PDF basados en XFA. Estos formularios son los más adecuados para tablets y entornos de escritorio.

AEM Forms es una potente plataforma de clase empresarial y la captura de datos (formularios adaptables, formularios PDF y formularios HTML5) es solo una de las funciones de AEM Forms. Para obtener la lista completa de funciones, consulte [Introducción a AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topología de implementación {#deployment-topology}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. Solo se necesita un mínimo de una instancia de AEM Author y AEM Publish para ejecutar las funciones de captura de datos de AEM Forms. Se recomienda la siguiente topología para ejecutar las funciones de captura de datos de AEM Forms en AEM Forms. Para obtener información detallada sobre la topología, consulte [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topología recomendada](assets/recommended-topology.png)

## Requisitos del sistema {#system-requirements}

Antes de empezar a instalar y configurar la capacidad de captura de datos de AEM Forms, asegúrese de que:

* La infraestructura de hardware y software está establecida. Para obtener una lista detallada de hardware y software compatibles, consulte Requisitos [técnicos](/help/sites-deploying/technical-requirements.md).

* La ruta de instalación de la instancia de AEM no contiene espacios en blanco.
* Se está ejecutando una instancia de AEM. En la terminología de AEM, una &quot;instancia&quot; es una copia de AEM que se ejecuta en un servidor en el modo de creación o publicación. Se requieren al menos dos instancias de [AEM (un autor y una publicación)](/help/sites-deploying/deploy.md) para ejecutar las funciones de captura de datos de AEM Forms:

   * **Autor**: Instancia de AEM que se utiliza para crear, cargar y editar contenido y administrar el sitio web. Una vez que el contenido está listo para activarse, se replica en la instancia de publicación.
   * **Publicar**: Instancia de AEM que sirve el contenido publicado al público a través de Internet o de una red interna.

* Se cumplen los requisitos de memoria. El paquete adicional de AEM Forms requiere:

   * 15 GB de espacio temporal para instalaciones basadas en Microsoft Windows.
   * 6 GB de espacio temporal para instalaciones basadas en UNIX.

* Se establece la replicación y la replicación inversa para las instancias de autor y publicación. Para obtener más información, consulte [Replicación](/help/sites-deploying/replication.md).
* Para sistemas basados en UNIX:

   * Instale los siguientes paquetes de 32 bits desde el medio de instalación:

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>fontconfig</td>
   <td>freetype</td>
   <td>glibc</td>
  </tr>
  <tr>
   <td>libcurl</td>
   <td>libICE</td>
   <td>libicu</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>libuuid</td>
   <td>libX11</td>
   <td><p>libXau</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>libXinerama</td>
   <td>libXrandr</td>
   <td>libXoutput</td>
  </tr>
  <tr>
   <td>nss-softokn-freebl</td>
   <td>OpenSSL</td>
   <td>zlib</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Si OpenSSL ya está instalado en el servidor, actualícelo a la versión más reciente.
>* Cree enlaces simbólicos libcurl.so, libcrypto.so y libssl.so que apunten a la última versión de las bibliotecas libcurl, libcrypto y libssl respectivamente.
>



* Instale el siguiente paquete de 64 bits desde el medio de instalación:

   * libicu

## Install AEM Forms add-on package {#install-aem-forms-add-on-package}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. El paquete contiene captura de datos de AEM Forms y otras funciones. Realice los siguientes pasos para instalar el paquete de complemento:

1. Inicie sesión en el servidor [de](https://localhost:4502) AEM como administrador y abra el recurso compartido [de](https://localhost:4502/crx/packageshare)paquetes. Necesita un ID de Adobe para iniciar sesión en el recurso compartido de paquetes.
1. En Uso compartido [de paquetes de](https://localhost:4502/crx/packageshare/login.html)AEM, busque los paquetes **de complementos de formularios de** AEM 6.5, haga clic en el paquete aplicable a su sistema operativo y, a continuación, haga clic en **Descargar**. Lea y acepte el contrato de licencia y haga clic en **Aceptar**. Se inicia la descarga. Una vez descargado, la palabra **Descargado** aparece junto al paquete.

   También puede utilizar el número de versión para buscar un paquete de complemento. Para ver el número de versión del paquete más reciente, consulte el artículo de la versión [de](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms.

1. Una vez finalizada la descarga, haga clic en **Descargado**. Se le redirige al administrador de paquetes. En el administrador de paquetes, busque el paquete descargado y haga clic en **Instalar**.

   Si descarga manualmente el paquete mediante el vínculo directo que aparece en el artículo de la versión [de AEM Forms, inicie sesión en el administrador de paquetes, haga clic en](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) Cargar paquete ****, seleccione el paquete descargado y haga clic en cargar. Después de cargar el paquete, haga clic en el nombre del paquete y, a continuación, en **Instalar.**

1. Después de instalar el paquete, se le pedirá que reinicie la instancia de AEM. **No reinicie el servidor inmediatamente.** Antes de detener el servidor de AEM Forms, espere hasta que los mensajes ServiceEvent REGISTRARED y ServiceEvent UNREGISTER dejen de aparecer en el `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` archivo y el registro sea estable.
1. Repita los pasos del 1 al 4 en todas las instancias de Autor y Publicación.

## Configuraciones posteriores a la instalación {#post-installation-configurations}

AEM Forms tiene algunas configuraciones obligatorias y opcionales. Las configuraciones obligatorias incluyen la configuración de las bibliotecas de BouncyCastle y el agente de serialización. Las configuraciones opcionales incluyen la configuración de distribuidor, portal de formularios, Adobe Sign, Adobe Analytics y Adobe Target.

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

1. Abra AEM Configuration Manager en una ventana del explorador. La dirección URL predeterminada es `https://[server]:[port]/system/console/configMgr`.
1. Busque **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** y abra la configuración.
1. Agregue el paquete **sun.util.calendar** al campo de la **lista blanca** . Haga clic en **Guardar**.
1. Repita los pasos del 1 al 3 en todas las instancias de Autor y Publicación.

### Configuraciones posteriores a la instalación opcionales {#optional-post-installation-configurations}

#### Configurar Dispatcher {#configure-dispatcher}

Dispatcher es una herramienta de almacenamiento en caché y equilibrio de carga para AEM. AEM Dispatcher también ayuda a proteger el servidor AEM de los ataques. Puede aumentar la seguridad de la instancia de AEM mediante Dispatcher junto con un servidor web de clase empresarial. Si utiliza [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html), realice las siguientes configuraciones para AEM Forms:

1. Configuración del acceso para AEM Forms:

   Abra el archivo dispatcher.any para editarlo. Vaya a la sección de filtros y agregue el siguiente filtro a la sección de filtros:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Guarde y cierre el archivo. Para obtener información detallada sobre los filtros, consulte la documentación [de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configure el servicio de filtros de referente:

   Inicie sesión en el administrador de configuración de Apache Felix como administrador. La dirección URL predeterminada del administrador de configuración es https://[server]:[port_number]/system/console/configMgr. En el menú **Configuraciones **, seleccione la opción Filtro **de referente Sling de** Apache. En el campo Permitir hosts, escriba el nombre de host del despachante para que se pueda utilizar como referente y haga clic en **Guardar**. El formato de la entrada es https://[server]:[port].

#### Configurar caché {#configure-cache}

El almacenamiento en caché es un mecanismo para reducir los tiempos de acceso a los datos, reducir la latencia y mejorar las velocidades de entrada y salida (E/S). La caché de formularios adaptables almacena solo el contenido HTML y la estructura JSON de un formulario adaptable sin guardar datos precargados. Ayuda a reducir el tiempo necesario para procesar un formulario adaptable.

* Al utilizar la caché de formularios adaptables, utilice [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) para almacenar en caché las bibliotecas de cliente (CSS y JavaScript) de un formulario adaptable.
* Al desarrollar componentes personalizados, mantenga la caché de formularios adaptables deshabilitada en el servidor que se utiliza para el desarrollo.

Realice los siguientes pasos para configurar la caché de formularios adaptables:

1. Vaya al administrador de configuración de la consola web de AEM en https://[server]:[port]/system/console/configMgr.
1. Haga clic en Configuración **de canal web de comunicación interactiva y formulario** adaptable para editar sus valores de configuración. En el cuadro de diálogo Editar valores de configuración, especifique el número máximo de formularios o documentos que una instancia del servidor de AEM Forms puede almacenar en caché en el campo **Número de formularios** adaptables. El valor predeterminado es 100. Haga clic en **Guardar**.

   >[!NOTE]
   >
   >Para deshabilitar la caché, establezca el valor en **0** en el campo Número de formularios adaptables. La caché se restablece y todos los formularios y documentos se eliminan de la caché cuando se deshabilita o cambia la configuración de la caché.

#### Configurar la comunicación SSL para el modelo de datos de formulario {#configure-ssl-communcation-for-form-data-model}

Puede habilitar la comunicación SSL para el modelo de datos de formulario. Para habilitar la comunicación SSL para el modelo de datos de formulario, antes de iniciar una instancia de AEM Forms, agregue certificados al almacén de confianza de Java de todas las instancias. Puede ejecutar el comando siguiente para agregar los certificados: &quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Configurar Adobe Sign {#configure-adobe-sign}

Adobe Sign habilita los flujos de trabajo de firma electrónica para formularios adaptables. Las firmas electrónicas mejoran los flujos de trabajo para procesar documentos para áreas legales, de ventas, de nómina, de gestión de recursos humanos y muchas más.

En un escenario típico de formularios adaptables y Adobe Sign, un usuario rellena un formulario adaptable para **aplicar a un servicio**. Por ejemplo, una solicitud de tarjeta de crédito y un formulario de beneficios para el ciudadano. Cuando un usuario rellena, envía y firma el formulario de solicitud, éste se envía al proveedor de servicios para que realice más acciones. El proveedor de servicios revisa la aplicación y utiliza Adobe Sign para marcar la aplicación aprobada. Para habilitar flujos de trabajo de firma electrónica similares, puede integrar Adobe Sign con AEM Forms.

Para utilizar Adobe Sign con AEM Forms, [integre Adobe Sign con AEM Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Configurar Adobe Analytics {#configure-adobe-analytics}

AEM Forms se integra con Adobe Analytics, lo que le permite capturar y rastrear métricas de rendimiento para los formularios y documentos publicados. El objetivo detrás del análisis de estas métricas es tomar decisiones informadas basadas en datos sobre los cambios necesarios para que los formularios o documentos sean más utilizables.

Para utilizar Adobe Analytics con AEM Forms, consulte [Configuración de análisis e informes](/help/forms/using/configure-analytics-forms-documents.md).

#### Integrar Adobe Target {#integrate-adobe-target}

Es probable que sus clientes abandonen un formulario si la experiencia que ofrece no es atractiva. Aunque resulta frustrante para los clientes, también puede aumentar el volumen de asistencia y el costo de su organización. Es fundamental, al mismo tiempo que resulta difícil identificar y proporcionar la experiencia adecuada del cliente que aumenta la tasa de conversión. Los formularios AEM son la clave para este problema.

Los formularios AEM se integran con Adobe Target, una solución de Adobe Marketing Cloud, para ofrecer experiencias de cliente personalizadas y atractivas en varios canales digitales. Para utilizar Adobe Target en formularios adaptables de prueba A/B, [integre Adobe Target con AEM Forms](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## Pasos siguientes {#next-steps}

Ha configurado un entorno para utilizar las funciones de captura de datos de AEM Forms. Ahora, los siguientes pasos hacia el uso de la capacidad son:

* [Crear el primer formulario adaptable](/help/forms/using/create-your-first-adaptive-form.md)
* [Crear el primer formulario PDF](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [Introducción a los formularios HTML5](/help/forms/using/introduction.md)

