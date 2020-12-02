---
title: Instalación y configuración de capacidades de captura de datos
seo-title: Instalación y configuración de capacidades de captura de datos
description: Instale y configure formularios adaptables, PDF forms y HTML5 Forms. Configure Adobe Analytics y Adobe Target para formularios adaptables a fin de analizar el uso de formularios y usuarios de destinatario en función de su perfil.
seo-description: Instale y configure formularios adaptables, PDF forms y HTML5 Forms. Configure Adobe Analytics y Adobe Target para formularios adaptables a fin de analizar el uso de formularios y usuarios de destinatario en función de su perfil.
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
translation-type: tm+mt
source-git-commit: 35b2c9c8c79b3cc3d81e0b92ea17cd7d599fa7ee
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 1%

---


# Instalar y configurar las capacidades de captura de datos{#install-and-configure-data-capture-capabilities}

## Introducción {#introduction}

AEM Forms proporciona un conjunto de formularios para obtener datos del usuario final: formularios adaptables, HTML5 Forms y PDF forms. También proporciona herramientas para la lista de todos los formularios disponibles en una página web, el análisis del uso de los formularios y el destinatario de los usuarios en función de su perfil. Estas funciones se incluyen en el paquete de complementos de AEM Forms. El paquete de complemento se implementa en una instancia de Autor o Publicación de AEM.

**Formularios adaptables:** Estos formularios cambian de apariencia en función del tamaño de pantalla del dispositivo, son atractivos e interactivos. Forms adaptable también se puede integrar con Adobe Analytics, Adobe Sign y Adobe Target. Esto le permitió ofrecer formularios personalizados y experiencias orientadas al proceso a los usuarios en función de su demografía y otras características. También puede integrar formularios adaptables con Adobe Sign.

**Los** formularios PDF son adecuados para la impresión y la captura de información digital en un documento PDF. En el avatar digital, puede utilizar Adobe Acrobat o Acrobat Reader para rellenar estos formularios. Puede alojar estos formularios en su sitio web o utilizar el portal de formularios para la lista de estos formularios en un sitio AEM. También puede enviar estos formularios por correo electrónico a otros usuarios como archivos adjuntos. Estos formularios son los más adecuados para entornos de escritorio.

**Los formularios HTML5** son la versión de PDF forms compatible con el explorador. HTML5 Forms es adecuado para entornos que no admiten complementos PDF. HTML5 Forms permite procesar formularios basados en XFA en dispositivos móviles y navegadores de escritorio en los que no se admite PDF basados en XFA. Estos formularios son los más adecuados para tablets y entornos de escritorio.

AEM Forms es una potente plataforma de clase empresarial y la captura de datos (formularios adaptables, PDF forms y HTML5 Forms) es sólo una de las funciones de AEM Forms. Para obtener la lista completa de las capacidades, consulte [Introducción a AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topología de implementación {#deployment-topology}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. Solo se necesita un mínimo de una instancia de AEM Author y AEM Publish para ejecutar las funciones de captura de datos de AEM Forms. Se sugiere la siguiente topología para ejecutar las capacidades de captura de datos de AEM Forms AEM Forms. Para obtener información detallada sobre la topología, consulte [Topologías de arquitectura e implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topología recomendada](assets/recommended-topology.png)

## Requisitos del sistema {#system-requirements}

Antes de empezar a instalar y configurar la capacidad de captura de datos de AEM Forms, asegúrese de que:

* La infraestructura de hardware y software está establecida. Para obtener una lista detallada del hardware y el software admitidos, consulte [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* La ruta de instalación de la instancia de AEM no contiene espacios en blanco.
* Se está ejecutando una instancia de AEM. Para los usuarios de Windows, instale la instancia de AEM en modo elevado. En AEM terminología, una &quot;instancia&quot; es una copia de AEM que se ejecuta en un servidor en el modo de autor o publicación. Se requieren por lo menos dos [instancias de AEM (un autor y una publicación)](/help/sites-deploying/deploy.md) para ejecutar las capacidades de captura de datos de AEM Forms:

   * **Autor**: Instancia de AEM utilizada para crear, cargar y editar contenido y administrar el sitio web. Una vez que el contenido está listo para activarse, se replica en la instancia de publicación.
   * **Publicar**: Una instancia de AEM que sirve el contenido publicado al público a través de Internet o de una red interna.

* Se cumplen los requisitos de memoria. El paquete de complementos de AEM Forms requiere:

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

## Instalación del paquete de complementos de AEM Forms {#install-aem-forms-add-on-package}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. El paquete contiene captura de datos de AEM Forms y otras funciones. Realice los siguientes pasos para instalar el paquete de complemento:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesita un Adobe ID para iniciar sesión en la distribución de software.
1. Toque **[!UICONTROL Adobe Experience Manager]** disponible en el menú del encabezado.
1. En la sección **[!UICONTROL Filtros]**:
   1. Seleccione **[!UICONTROL Forms]** en la lista desplegable **[!UICONTROL Solución]**.
   2. Seleccione la versión y escriba el paquete. También puede utilizar la opción **[!UICONTROL Buscar descargas]** para filtrar los resultados.
1. Toque el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar los términos del EULA]** y toque **[!UICONTROL Descargar]**.
1. Abra [Administrador de paquetes](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

   También puede descargar el paquete a través del vínculo directo que aparece en el artículo [AEM Forms releases](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html).
1. Después de instalar el paquete, se le pedirá que reinicie la instancia de AEM. **No reinicie el servidor inmediatamente.** Antes de detener el servidor de AEM Forms, espere hasta que los mensajes ServiceEvent REGISTERED y ServiceEvent UNREGISTER dejen de aparecer en el  `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` archivo y el registro sea estable.
1. Repita los pasos del 1 al 7 en todas las instancias de Autor y Publicación.

### (Solo Windows) Instalación automática de redistribuibles de Visual Studio {#automatic-installation-visual-studio-redistributables}

Si instala una instancia de AEM en modo elevado, los redistribuibles de Visual Studio que faltan se instalan automáticamente durante la instalación del paquete del complemento de AEM Forms.

Para evaluar si los redistribuibles de Visual Studio se instalan automáticamente, abra el archivo `error.log` disponible en el directorio `/crx-repository/logs/`. Los registros incluyen el siguiente mensaje:

`Redist <service name> already installed on system, will not attempt re-installation`

Si los redistribuibles no se pueden instalar, los registros incluyen el siguiente mensaje:

`Current user does not have elevated privileges, aborting installation of redist <service name>`

Para resolver el problema, reinicie el servidor de AEM, instale AEM en modo elevado y, a continuación, instale el paquete del complemento de AEM Forms.

Si la comprobación de privilegios falla, los registros incluyen el siguiente mensaje:

`Privilege escalation check failed with error: <error message>`

## Configuraciones posteriores a la instalación {#post-installation-configurations}

AEM Forms tiene algunas configuraciones obligatorias y opcionales. Las configuraciones obligatorias incluyen la configuración de las bibliotecas de BouncyCastle y el agente de serialización. Las configuraciones opcionales incluyen la configuración del despachante, el portal de Forms, Adobe Sign, Adobe Analytics y Adobe Target.

### Configuraciones posteriores a la instalación obligatorias {#mandatory-post-installation-configurations}

#### Configurar las bibliotecas RSA y BouncyCastle {#configure-rsa-and-bouncycastle-libraries}

Realice los siguientes pasos en todas las instancias de Autor y Publicación para iniciar las bibliotecas delegadas:

1. Detenga la instancia de AEM subyacente.
1. Abra el archivo `[AEM installation directory]\crx-quickstart\conf\sling.properties` para editarlo.

   Si ha utilizado `[AEM installation directory]\crx-quickstart\bin\start.bat` en el AEM de inicio, edite el archivo sling.properties ubicado en `[AEM_root]\crx-quickstart\`.

1. Añada las siguientes propiedades en el archivo sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Guarde y cierre el archivo y inicio la instancia de AEM.
1. Repita los pasos del 1 al 4 en todas las instancias de Autor y Publicación.

#### Configurar el agente de serialización {#configure-the-serialization-agent}

Realice los siguientes pasos en todas las instancias de Autor y Publicación para agregar el paquete a la lista de permitidos:

1. Abra AEM Administrador de configuración en una ventana del explorador. La dirección URL predeterminada es `https://'[server]:[port]'/system/console/configMgr`.
1. Busque **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** y abra la configuración.
1. Añada el paquete **sun.util.calendar** al campo **lista de permitidos**. Haga clic en **Guardar**.
1. Repita los pasos del 1 al 3 en todas las instancias de Autor y Publicación.

### Configuraciones posteriores a la instalación opcionales {#optional-post-installation-configurations}

#### Configurar Dispatcher {#configure-dispatcher}

Dispatcher es una herramienta de almacenamiento en caché y/o equilibrio de carga de Adobe Experience Manager que se puede utilizar junto con un servidor web de clase empresarial. Si utiliza [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html), realice las siguientes configuraciones para AEM Forms:

1. Configurar el acceso para AEM Forms:

   Abra el archivo dispatcher.any para editarlo. Vaya a la sección de filtros y agregue el siguiente filtro a la sección de filtros:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Guarde y cierre el archivo. Para obtener información detallada sobre filtros, consulte [documentación de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configure el servicio de filtros de remitente del reenvío:

   Inicie sesión en el administrador de configuración de Apache Felix como administrador. La dirección URL predeterminada del administrador de configuración es `https://[server]:[port_number]/system/console/configMgr`. En el menú **Configuraciones**, seleccione la opción **Filtro de Remitente del reenvío Sling de Apache**. En el campo Permitir hosts, escriba el nombre de host del despachante para que se lo permita como remitente del reenvío y haga clic en **Guardar**. El formato de la entrada es `https://[server]:[port]&#39;.

#### Configurar caché {#configure-cache}

El almacenamiento en caché es un mecanismo para reducir los tiempos de acceso a los datos, reducir la latencia y mejorar las velocidades de entrada y salida (E/S). La caché de formularios adaptables almacena solo el contenido HTML y la estructura JSON de un formulario adaptable sin guardar datos precargados. Ayuda a reducir el tiempo necesario para procesar un formulario adaptable.

* Al utilizar la caché de formularios adaptables, utilice el [AEM despachante](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) para almacenar en caché las bibliotecas cliente (CSS y JavaScript) de un formulario adaptable.
* Al desarrollar componentes personalizados, mantenga la caché de formularios adaptables deshabilitada en el servidor que se utiliza para el desarrollo.

Realice los siguientes pasos para configurar la caché de formularios adaptables:

1. Vaya a AEM administrador de configuración de consola web en https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Haga clic en **Configuración del Canal Web de comunicación interactiva y formulario adaptable** para editar sus valores de configuración. En el cuadro de diálogo Editar valores de configuración, especifique el número máximo de formularios o documentos que una instancia del servidor de AEM Forms puede almacenar en caché en el campo **Número de Forms adaptable**. El valor predeterminado es 100. Haga clic en **Guardar**.

   >[!NOTE]
   >
   >Para deshabilitar la caché, establezca el valor en el campo Número de Forms adaptable en **0**. La caché se restablece y todos los formularios y documentos se eliminan de la caché cuando se deshabilita o cambia la configuración de la caché.

#### Configurar la comunicación SSL para el modelo de datos de formulario {#configure-ssl-communcation-for-form-data-model}

Puede habilitar la comunicación SSL para el modelo de datos de formulario. Para habilitar la comunicación SSL para el modelo de datos de formulario, antes de iniciar cualquier instancia de AEM Forms, agregue certificados al almacén de confianza de Java de todas las instancias. Puede ejecutar el comando siguiente para agregar los certificados: &quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Configurar Adobe Sign {#configure-adobe-sign}

Adobe Sign permite flujos de trabajo de firma electrónica para formularios adaptables. Las firmas electrónicas mejoran los flujos de trabajo para procesar documentos legales, de ventas, de nómina de pagos, de gestión de recursos humanos y muchas otras áreas.

En un escenario típico de Adobe Sign y formularios adaptables, un usuario rellena un formulario adaptable para **solicitar un servicio**. Por ejemplo, una solicitud de tarjeta de crédito y un formulario de beneficios para el ciudadano. Cuando un usuario rellena, envía y firma el formulario de solicitud, éste se envía al proveedor de servicio para que realice más acciones. Proveedor de servicio revisa la aplicación y utiliza Adobe Sign para marcar la aplicación aprobada. Para habilitar flujos de trabajo de firma electrónica similares, puede integrar Adobe Sign con AEM Forms.

Para utilizar Adobe Sign con AEM Forms, [Integre Adobe Sign con AEM Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Configurar Adobe Analytics {#configure-adobe-analytics}

AEM Forms se integra con Adobe Analytics que le permite capturar y rastrear las métricas de rendimiento de los formularios y documentos publicados. El objetivo detrás del análisis de estas métricas es tomar decisiones informadas en base a los datos sobre los cambios necesarios para que los formularios o documentos sean más utilizables.

Para utilizar Adobe Analytics con AEM Forms, consulte [Configuración de análisis e informes](/help/forms/using/configure-analytics-forms-documents.md).

#### Integrar Adobe Target {#integrate-adobe-target}

Es probable que sus clientes abandonen un formulario si la experiencia que ofrece no es atractiva. Aunque resulta frustrante para los clientes, también puede aumentar el volumen de asistencia y el costo de su organización. Es fundamental, además de todo un desafío, identificar y proporcionar la experiencia adecuada del cliente que aumenta la tasa de conversión. AEM formularios contiene la clave para este problema.

AEM formularios se integra con Adobe Target, una solución de Adobe Marketing Cloud, para ofrecer experiencias personalizadas y atractivas a los clientes en varios canales digitales. Para utilizar formularios adaptables de prueba A/B de Adobe Target, [integre Adobe Target con AEM Forms](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## Próximos pasos {#next-steps}

Ha configurado un entorno para utilizar las funciones de captura de datos de AEM Forms. Ahora, los siguientes pasos hacia el uso de la capacidad son:

* [Crear el primer formulario adaptable](/help/forms/using/create-your-first-adaptive-form.md)
* [Crear el primer formulario PDF](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [Introducción a HTML5 Forms](/help/forms/using/introduction.md)

