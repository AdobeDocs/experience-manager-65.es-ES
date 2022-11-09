---
title: Instalación y configuración del flujo de trabajo centrado en Forms en OSGi
seo-title: Installing and Configuring Forms-centric workflow on OSGi
description: Instale y configure AEM Forms Interactive Communications para crear correspondencia comercial, documentos, declaraciones, avisos de beneficios, correos de marketing, facturas y kits de bienvenida.
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
role: Admin
exl-id: 4b24a38a-c1f0-4c81-bb3a-39ce2c4892b1
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 12%

---

# Instalación y configuración del flujo de trabajo centrado en Forms en OSGi{#installing-and-configuring-forms-centric-workflow-on-osgi}

## Introducción {#introduction}

Las empresas recopilan y procesan datos de varios formularios, sistemas back-end y otras fuentes de datos. El procesamiento de datos implica procedimientos de revisión y aprobación, tareas repetitivas y archiving de datos. Por ejemplo, al revisar un formulario y convertirlo en un documento de PDF. Cuando se realiza manualmente, las tareas repetitivas pueden tardar mucho tiempo y recursos.

Puede usar [Flujo de trabajo centrado en Forms en OSGi](../../forms/using/aem-forms-workflow.md) para crear rápidamente flujos de trabajo basados en formularios adaptables. Estos flujos de trabajo pueden ayudarle a automatizar los flujos de trabajo de revisión y aprobación, los flujos de trabajo de procesos empresariales y otras tareas repetitivas. Estos flujos de trabajo también ayudan a procesar documentos (crear, ensamblar, distribuir y archivar documentos de PDF, agregar firmas digitales para limitar el acceso a documentos, descodificar formularios con códigos de barras, etc.) y utilizar el flujo de trabajo de firma de Adobe Sign con formularios y documentos.

Una vez configurados, estos flujos de trabajo se pueden activar manualmente para completar un proceso definido o ejecutarse mediante programación cuando los usuarios envían un formulario o una comunicación interactiva. La funcionalidad se incluye en el paquete de complementos de AEM Forms.

AEM Forms es una potente plataforma de clase empresarial. El flujo de trabajo centrado en Forms en OSGi es solo una de las capacidades de AEM Forms. Para obtener la lista completa de funcionalidades, consulte [Introducción a AEM Forms](introduction-aem-forms.md).

>[!NOTE]
>
>Con el flujo de trabajo centrado en formularios en OSGi, puede generar e implementar rápidamente flujos de trabajo para diversas tareas en la pila OSGi, sin tener que instalar la funcionalidad de administración de procesos completa en la pila JEE. Consulte una [comparación](capabilities-osgi-jee-workflows.md) de los flujos de trabajo de AEM centrados en Forms en OSGi y Process Management en JEE para conocer las diferencias y similitudes en las capacidades.
>
>Después de la comparación, si elige instalar la capacidad de administración de procesos en la pila de JEE, consulte [Instalación o actualización de AEM Forms en JEE](/help/forms/home.md) para obtener información detallada sobre la instalación y configuración de la pila JEE y las capacidades de administración de procesos.

## Topología de implementación {#deployment-topology}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. Solo necesita un mínimo de una instancia de AEM Author o Processing (autor de producción) para ejecutar el flujo de trabajo centrado en Forms en la capacidad OSGi. Una instancia de procesamiento es [Autor de AEM enriquecido](/help/forms/using/hardening-securing-aem-forms-environment.md) instancia. No realice ninguna creación real, como la creación de flujos de trabajo o formularios adaptables, en el autor de producción.

La siguiente topología es una topología indicativa para ejecutar AEM Forms Interactive Communications, Correspondence Management, AEM Forms Data Capture y el flujo de trabajo Forms-Centric en las funcionalidades OSGi. Para obtener información detallada sobre la topología, consulte [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topología recomendada](assets/recommended-topology.png)

El flujo de trabajo centrado en AEM Forms Forms en OSGi ejecuta AEM Bandeja de entrada y AEM IU de creación del Modelo de flujo de trabajo en las instancias Autor de AEM Forms.

## Requisitos del sistema {#system-requirements}

>[!NOTE]
>
>Pasar a la [Pasos siguientes](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) del documento, si ya ha instalado AEM Forms en OSGi como se explica en la sección [instalación y configuración de las funcionalidades de captura de datos](../../forms/using/installing-configuring-aem-forms-osgi.md) artículo.

Antes de empezar a instalar y configurar el flujo de trabajo centrado en Forms en OSGi, asegúrese de que:

* La infraestructura de hardware y software está implementada. Para obtener una lista detallada del hardware y software compatibles, consulte [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* La ruta de instalación de la instancia de AEM no contiene espacios en blanco.
* Se está ejecutando una instancia de AEM. En AEM terminología, una &quot;instancia&quot; es una copia de AEM que se ejecuta en un servidor en modo de autor o publicación. Se necesita al menos una instancia de AEM (Autor o Procesamiento) para ejecutar el flujo de trabajo centrado en Forms en OSGi:

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

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. El paquete contiene un flujo de trabajo centrado en Forms en OSGi y otras funcionalidades. Siga estos pasos para instalar el paquete de complementos:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Pulse **[!UICONTROL Adobe Experience Manager]**, disponible en el menú del encabezado.
1. En el **[!UICONTROL Filtros]** sección:
   1. Select **[!UICONTROL Forms]** de la variable **[!UICONTROL Solución]** lista desplegable.
   2. Seleccione la versión y el tipo del paquete. También puede usar la variable **[!UICONTROL Descargas de búsqueda]** para filtrar los resultados.
1. Pulse el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y toque **[!UICONTROL Descargar]**.
1. Abra [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
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

#### Configurar Dispatcher {#configure-dispatcher}

Dispatcher es una herramienta de almacenamiento en caché y equilibrio de carga para AEM. AEM Dispatcher también ayuda a proteger AEM servidor de los ataques. Puede aumentar la seguridad de la instancia de AEM utilizando Dispatcher junto con un servidor web de clase empresarial. Si usa [Dispatcher](https://helpx.adobe.com/es/experience-manager/dispatcher/using/dispatcher-configuration.html)y, a continuación, realice las siguientes configuraciones para AEM Forms:

1. Configure el acceso para AEM Forms:

   Abra el archivo dispatcher.any para editarlo. Vaya a la sección de filtros y añada el siguiente filtro a la sección de filtros:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Guarde y cierre el archivo. Para obtener información detallada sobre los filtros, consulte [Documentación de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configure el servicio de filtros del referente:

   Inicie sesión en el gestor de configuración de Apache Felix como administrador. La dirección URL predeterminada del administrador de configuración es https://&#39;server&#39;:[port_number]/system/console/configMgr. En el **Configuraciones** seleccione **Filtro de referente de Apache Sling** . En el campo Permitir hosts , introduzca el nombre de host del Dispatcher para permitirlo como referente y haga clic en **Guardar**. El formato de la entrada es `https://'[server]:[port]'`.

#### Configurar caché {#configure-cache}

El almacenamiento en caché es un mecanismo para reducir los tiempos de acceso a los datos, reducir la latencia y mejorar las velocidades de entrada y salida (E/S). La caché de formularios adaptables almacena únicamente el contenido del HTML y la estructura JSON de un formulario adaptable sin guardar ningún dato prerellenado. Ayuda a reducir el tiempo necesario para procesar un formulario adaptable.

* Al utilizar la caché de formularios adaptables, utilice la variable [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) para almacenar en caché las bibliotecas de cliente (CSS y JavaScript) de un formulario adaptable.
* Mientras desarrolla componentes personalizados, mantenga deshabilitada la caché de formularios adaptables en el servidor utilizado para el desarrollo.

Realice los siguientes pasos para configurar la caché de formularios adaptables:

1. Vaya al Administrador de configuración de la consola web de AEM en `https://'[server]:[port]'/system/console/configMgr`.
1. Haga clic en **[!UICONTROL Configuración del canal web de comunicaciones interactivas y formularios adaptables]** para editar sus valores de configuración. En el cuadro de diálogo editar valores de configuración, especifique el número máximo de formularios o documentos que una instancia del servidor de AEM Forms puede almacenar en caché en la variable **Número de Forms adaptable** campo . El valor predeterminado es 100. Haga clic en **Guardar**.

   >[!NOTE]
   >
   >Para desactivar la caché, establezca el valor del campo Número de formularios adaptables en **0**. La caché se restablece y todos los formularios y documentos se eliminan de ella cuando se desactiva o cambia su configuración.

#### Configuración de Adobe Sign {#configure-adobe-sign}

Adobe Sign permite los flujos de trabajo de firma electrónica para formularios adaptables. Las firmas electrónicas mejoran los flujos de trabajo para procesar documentos para el área legal, ventas, nóminas, administración de recursos humanos y muchas más.

En un flujo de trabajo típico de Adobe Sign y Forms centrado en OSGi, un usuario rellena un formulario adaptable a **solicitud de un servicio**. Por ejemplo, una solicitud de tarjeta de crédito y un formulario de solicitud para una prestación. Cuando un usuario rellena, envía y firma el formulario de solicitud, se inicia un flujo de trabajo de aprobación/rechazo. El proveedor de servicios revisa la aplicación en AEM Bandeja de entrada y utiliza Adobe Sign para firmar electrónicamente la aplicación. Para habilitar flujos de trabajo de firma electrónica similares, puede integrar Adobe Sign con AEM Forms.

Para usar Adobe Sign con AEM Forms, [Integración de Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## Pasos siguientes {#next-steps}

Ha configurado un entorno para utilizar el flujo de trabajo centrado en Forms en las funciones OSGi. Ahora, los pasos para utilizar esta capacidad son:

* [Uso del flujo de trabajo centrado en Forms en OSGi](../../forms/using/aem-forms-workflow.md)
* [Referencia de pasos de flujo de trabajo](/help/sites-developing/workflows-step-ref.md)
* [Procesamiento posterior de cartas y comunicaciones interactivas](../../forms/using/submit-letter-topostprocess.md)
