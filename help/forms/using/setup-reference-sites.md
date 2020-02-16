---
title: Configurar y configurar sitios de referencia de autoservicio de We.Finance y Empleados
seo-title: Configurar y configurar sitios de referencia de autoservicio de We.Finance y Empleados
description: Los sitios de referencia de AEM Forms muestran cómo puede utilizar AEM Forms para implementar un flujo de trabajo completo en una organización.
seo-description: Los sitios de referencia de AEM Forms muestran cómo puede utilizar AEM Forms para implementar un flujo de trabajo completo en una organización.
uuid: 199349b7-97bd-4eca-a2e7-19d6708fcbee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 03886dd3-5873-4908-912b-fbbddb26c322
docset: aem65
translation-type: tm+mt
source-git-commit: 709d8fe467f5449eb1e844a49126535a4a4a6e7a

---


# Configurar y configurar sitios de referencia de autoservicio de We.Finance y Empleados{#set-up-and-configure-we-finance-and-employee-self-service-reference-sites}

AEM Forms proporciona una implementación de sitio de referencia para demostrar cómo AEM Forms ayuda a las organizaciones del sector de servicios financieros y del gobierno a transformar sus complejas transacciones en experiencias digitales sencillas y atractivas en cualquier lugar, en cualquier momento y en cualquier dispositivo.

El sitio de referencia de We.Finance dibuja casos de uso de la vida real para interactuar con clientes existentes y potenciales, desde el primer toque hasta la administración de correspondencias y transacciones de una manera personalizada y rentable.

Los sitios de referencia le permiten explorar y mostrar las siguientes funciones clave de AEM Forms.

* Experiencia de creación simplificada de formularios adaptables interactivos y atractivos y comunicaciones interactivas.
* Comunicaciones interactivas para crear comunicaciones interactivas, personalizadas y adaptables con el cliente que se adapten a la configuración y el diseño del dispositivo.
* Integración de datos para conectarse a orígenes de datos dispares para rellenar y enviar datos de formulario mediante un modelo de datos de formulario.
* Flujo de trabajo de formularios para automatizar procesos y flujos de trabajo empresariales.
* Funciones avanzadas de administración y procesamiento de datos de usuario.
* Integración con Adobe Sign para firmar y enviar formularios adaptables de forma segura.
* Integración con Adobe Target para ofrecer recomendaciones específicas y realizar pruebas A/B para maximizar el ROI de un formulario.
* Integración con Adobe Analytics para medir el rendimiento de un formulario o una campaña y tomar decisiones informadas.
* Se ha mejorado la experiencia de cumplimentación de formularios.

Los sitios de referencia proporcionan recursos reutilizables que puede utilizar como plantillas para crear sus propios recursos.

* Integración con Adobe Sign para firmar y enviar formularios adaptables de forma segura.

* Integración con Adobe Sign para firmar y enviar formularios adaptables de forma segura.

## Requisitos previos y pasos para configurar sitios de referencia {#prerequisites-and-steps-to-set-up-reference-sites}

Antes de configurar el sitio de referencia, asegúrese de que dispone de lo siguiente:

* **AEM Essentials** AEM QuickStart, AEM Forms Add-on package y paquetes de sitios de referencia. Consulte las versiones [de](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) AEM Forms para obtener información detallada sobre los paquetes de complementos y sitios de referencia.

* **Un servicio** SMTP Puede utilizar cualquier servicio SMTP.

* **Cuenta de desarrollador de Adobe Sign y aplicación** API de Adobe Sign Para utilizar las funciones de firma digital, se requiere la cuenta de desarrollador de Adobe Sign. Consulte [Adobe Sign](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html).

* Instancia en ejecución de Microsoft Dynamics 365 para integrarla con AEM Forms. Para ejecutar el sitio de referencia, importe los datos de ejemplo en la instancia de Microsoft Dynamics para rellenar previamente la comunicación interactiva utilizada en el sitio de referencia.
* Una instancia en ejecución de AEM con el paquete del complemento Forms. Para obtener más información, consulte [Instalación y configuración de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

Realice los siguientes pasos en la secuencia recomendada para configurar y configurar los sitios de referencia.

<table>
 <tbody>
  <tr>
   <th><strong>Etapa</strong></th>
   <th><strong>Configurar</strong></th>
   <th><strong>Notas</strong></th>
  </tr>
  <tr>
   <td><a href="#installandconfigureaemform">Instalación y configuración de AEM Forms</a></td>
   <td>Autor y publicación</td>
   <td>Instale y configure instancias de creación y publicación de AEM Forms.</td>
  </tr>
  <tr>
   <td><a href="#ssl">Configurar SSL</a></td>
   <td>Autor y publicación<br /> </td>
   <td>Habilite HTTP sobre SSL para comunicaciones seguras con Adobe Sign.</td>
  </tr>
  <tr>
   <td><p><a href="#externalizer">Configuración de Day CQ Link Externalizer</a></p> </td>
   <td>Autor y publicación<br /> </td>
   <td><p>Los casos de uso del sitio de referencia envían correos electrónicos para diferentes transacciones. Esta configuración es necesaria para el envío de la newsletter por correo electrónico. Garantiza que las URL y las imágenes apunten a la instancia de publicación. </p> </td>
  </tr>
  <tr>
   <td><a href="#cqmail">Configurar el servicio de correo CQ Day</a></td>
   <td>Autor y publicación</td>
   <td>Necesario para la comunicación por correo electrónico.</td>
  </tr>
  <tr>
   <td><a href="#xss">Anular configuración XSS predeterminada</a></td>
   <td>Publicación</td>
   <td>Se utiliza para anular los caracteres $, { y } bloqueados por xss security.</td>
  </tr>
  <tr>
   <td><a href="#aemds">Configuración de la configuración de AEM DS</a></td>
   <td>Creación</td>
   <td>Configure AEM DS para el envío de formularios en instancias de publicación y flujos de trabajo de procesamiento en la instancia de creación.</td>
  </tr>
  <tr>
   <td><a href="#refsite">Implementación de paquetes de sitios de referencia</a></td>
   <td>Creación</td>
   <td>Implemente paquetes de sitios de referencia en la instancia de creación de AEM Forms.</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#optional-import-sample-data-into-microsoft-dynamics">Importar datos de ejemplo en Microsoft Dynamics</a></td>
   <td>Autor y publicación</td>
   <td>Importar datos de muestra para solicitud de tarjeta de crédito, solicitud de hipoteca de origen y tutorial de solicitud de seguro de vivienda</td>
  </tr>
  <tr>
   <td><a href="../../forms/using/setup-reference-sites.md#configure-oauth-cloud-service-for-microsoft-dynamics">Configurar el servicio de nube OAuth para Microsoft Dynamics</a></td>
   <td>Autor y publicación</td>
   <td>Configure el servicio de nube OAuth en AEM Forms para habilitar la comunicación entre AEM Forms y Microsoft Dynamics. </td>
  </tr>
  <tr>
   <td><a href="#scheduler">Configuración del programador de Adobe Sign</a></td>
   <td>Autor y publicación<br /> </td>
   <td>Cambie la configuración del programador para comprobar el estado cada dos minutos.</td>
  </tr>
  <tr>
   <td><a href="#sign-service">Configurar el servicio de referencia de Adobe Sign Cloud del sitio</a></td>
   <td>Autor y publicación<br /> </td>
   <td>Una configuración que viene con paquetes de sitios de referencia y necesita una reconfiguración con credenciales válidas.</td>
  </tr>
  <tr>
   <td><a href="#anonymous">Configuración del servicio de configuración común de formularios para usuarios anónimos</a></td>
   <td>Publicación</td>
   <td>La configuración permite el envío, la firma y la generación de documentos de registro para usuarios anónimos.</td>
  </tr>
  <tr>
   <td><a href="#fdm">Modificar el archivo de intercambio de servicios restantes para el modelo de datos de formulario</a></td>
   <td>Autor y publicación<br /> </td>
   <td>Modifique el servicio para su entorno.</td>
  </tr>
 </tbody>
</table>

## Instalación y configuración de AEM Forms {#installandconfigureaemform}

Instale e implemente AEM Forms como se describe en [Instalación y configuración de AEM Forms en OSGi](../../forms/using/installing-configuring-aem-forms-osgi.md).

>[!NOTE]
>
>Configure los agentes de replicación y de replicación inversa si hay más de una instancia de publicación o si las instancias de creación y publicación están en equipos diferentes.

## Configurar SSL {#ssl}

La configuración SSL es necesaria para comunicarse con los servidores de Adobe Sign. Para ver los pasos detallados, consulte [Activación de HTTP sobre SSL](/help/sites-administering/ssl-by-default.md).

>[!CAUTION]
>
>No configure la fuerza SSL en la `/etc/map` carpeta.

## Configuración de Day CQ Link Externalizer {#externalizer}

En AEM, el **Externalizador** es un servicio OSGI que le permite transformar mediante programación una ruta de recursos (p. ej. /path/to/my/page) en una dirección URL externa y absoluta (por ejemplo, https://www.mycompany.com/path/to/my/page) prefiriendo la ruta con un DNS preconfigurado. Consulte [Externalización de direcciones URL](/help/sites-developing/externalizer.md).

>[!CAUTION]
>
>No externalice a URL HTTPS si utiliza un certificado autofirmado para SSL.
>
>Además, utilice localhost en lugar de su nombre de host para el servidor local.

Realice los siguientes pasos en las instancias de creación y publicación:

1. Vaya a Configuración de OSGi en https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr.
1. Toque y busque la configuración **de Day CQ Link Externalizer** .
Se abre el cuadro de diálogo Externalizador de vínculo CQ de día para editar la configuración.
1. En el cuadro de diálogo Externalizador de vínculo CQ de día, en el campo Dominios:

   * En la instancia de autor, especifique una URL de publicación a la que se pueda acceder desde un sistema externo. Por ejemplo, un nombre de host o un servidor web de publicación.
   * En la instancia de publicación, especifique las direcciones URL de creación y publicación.

1. Tanto en las instancias de autor como de publicación, asegúrese de que la URL del servidor local está especificada en el campo Dominios.
1. Toque **Guardar**. Espere un momento para que se reinicien todos los servicios.

## Configurar el servicio de correo CQ Day {#cqmail}

La implementación del sitio de referencia requiere que los mensajes de correo electrónico se envíen a los usuarios de ejemplo cuando rellenen y envíen formularios. La configuración del servicio de correo de CQ Day le permite proporcionar detalles del servicio SMTP para enviar correos electrónicos automatizados a los clientes. See [Configuring Email Notifications](/help/sites-administering/notification.md).

Realice los siguientes pasos para configurar el servicio de correo en la instancia de publicación:

1. Vaya a Configuración de OSGi en https://&lt;*hostname>*:&lt;*port>*/system/console/configMgr.
1. Toque y busque **Day CQ Mail Service** para abrirlo y configurarlo.
1. Proporcione valores de puerto y nombre de host del servidor SMTP.
1. Toque **Guardar.**

>[!NOTE]
>
>Puede utilizar su servicio SMTP corporativo o servicios públicos como Gmail. Para configurar el servicio SMTP, consulte la documentación del servicio SMTP.

## Anular configuración XSS predeterminada {#xss}

Las plantillas de correo electrónico del sitio de referencia de We.Finance contienen vínculos personalizados en los correos electrónicos. Estos vínculos tienen un marcador de posición como `${placeholder}`. Estos marcadores de posición se reemplazan por valores reales antes de enviar correos electrónicos. La configuración de protección XSS predeterminada para AEM no permite llaves (**{}**) en la dirección URL en el contenido HTML. Sin embargo, puede anular la configuración predeterminada realizando los siguientes pasos en la instancia de publicación:

1. Copiar `/libs/cq/xssprotection/config.xml` a `/apps/cq/xssprotection/config.xml`.
1. Abra `/apps/cq/xssprotection/config.xml`.
1. En la `common-regexps` sección , modifique la `onsiteURL` entrada como se indica a continuación y guarde el archivo.

   `<regexp name="onsiteURL" value="([\p{L}\p{N}\\\.\#@\$\{\}%\+&;\-_~,\?=/!\*\(\)]*|\#(\w)+)"/>`

>[!NOTE]
>
>Las llaves (**{}**) se incluyen como caracteres aceptados en la dirección URL en el contenido HTML.

Después de configurar el servidor SMTP, intente rellenar un formulario con el personaje de Sarah Rose y guardarlo como borrador. Al guardar como borrador, se obtiene una opción para recibir el borrador por correo electrónico. Al tocar el botón **Enviar correo electrónico** , si recibe un correo electrónico con un vínculo al borrador de la aplicación, la configuración del correo electrónico se realizará correctamente. Asegúrese de iniciar sesión con las credenciales de Sarah para ver el borrador.

## Configuración de la configuración de AEM DS {#aemds}

La configuración del servicio AEM DS es obligatoria en la instancia de publicación para las comunicaciones por correo electrónico en los casos de uso del sitio de referencia. Para ver los pasos detallados para configurar el servicio AEM DS en la instancia de Publish, consulte [Configuración](../../forms/using/configuring-the-processing-server-url-.md)de AEM DS.

Para los sitios de referencia de AEM Forms, en el servicio de configuración de AEM DS, especifique la URL del servidor de publicación en lugar de la URL del servidor de procesamiento.

>[!CAUTION]
>
>No inserte `/lc` la URL del servidor de procesamiento si está configurándola para OSGi de AEM Forms.

## Implementación de paquetes de sitios de referencia {#refsite}

Instale los paquetes de sitios de referencia mediante el uso compartido de paquetes.

* [Paquete de sitio de referencia de AEM Forms FSI](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/fd/AEM-FORMS-6.5-FSI-REF-SITE)
* [Paquete de sitio de referencia de AEM Forms para el gobierno](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/fd/AEM-FORMS-6.5-GOV-REF-SITE)

Para obtener más información sobre cómo utilizar paquetes y compartir paquetes, consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md).

Después de instalar los paquetes e iniciar las instancias de creación y publicación, visite las siguientes URL en el explorador:

* https://[server]:[port]/wegov
* https://[server]:[port]/weFinance

Si la instalación se realiza correctamente, puede acceder a las páginas de aterrizaje de los sitios de referencia y We.Finance.

## (Opcional) Importación de datos de ejemplo en Microsoft Dynamics {#optional-import-sample-data-into-microsoft-dynamics}

Los sitios de referencia de la aplicación de hipoteca principal y la aplicación de seguro automático están configurados para utilizar registros de Microsoft Dynamics. El paquete de sitio de referencia instala una entidad personalizada y registros de muestra que puede importar en Microsoft Dynamics para ejecutar el sitio de referencia. Realice los siguientes pasos para migrar y configurar los datos de ejemplo:

Para importar la entidad personalizada para la aplicación de seguro automático:

1. Descargue el paquete de la solución **WeFinanceAutoInsurance_1_0.zip** de https://[server]:[port]/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/WeFinanceAutoInsurance_1_0.zip en su instancia de creación de AEM.
1. En la instancia de Microsoft Dynamics, vaya a **Configuración > Soluciones** y haga clic en **Importar**. Seleccione e importe el paquete.

Para importar la entidad personalizada para la aplicación de seguro automático:

1. Descargue el paquete **AEMFormsFSIRefsite_1_0.zip** de https://[author]:[port]/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip. Seleccione e importe el paquete.

1. En la instancia de Microsoft Dynamics, vaya a **Configuración > Soluciones** y haga clic en **Importar**. Seleccione e importe el paquete.

Para importar los registros de pólizas de seguro y de cliente:

1. Descargue los archivos de datos **We.Finance Customers.csv, We.Finance Auto Insurance Renewals.csv** y de hipoteca **** doméstica desde las siguientes ubicaciones en la instancia de creación de AEM:

   * https://[server]:[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Customers.csv
   * https://[server]:[port/content/aemforms-refsite-collaterals/we-finance/auto-insurance/ms-dynamics/We.Finance Auto Insurance Renewals.csv
   * https://[server]:[port]/content/aemforms-refsite-collaterals/we-finance/home-hipoteca/ms-ddynamic/Sarah%20Rose%20Contact.csv

1. En la instancia de Microsoft Dynamics, haga lo siguiente:

   * Vaya a **Ventas** > Clientes **de** We.Finance y haga clic en **Importar**.

   * Vaya a **Ventas** > Seguro **automático de** We.Finance y haga clic en **Importar**.

   * Vaya a **Ventas** > Hipoteca **doméstica** We.Finance y haga clic en **Importar**.

## Configurar el servicio de nube OAuth para Microsoft Dynamics {#configure-oauth-cloud-service-for-microsoft-dynamics}

Configure el servicio de nube OAuth en AEM Forms para habilitar la comunicación entre AEM Forms y Microsoft Dynamics. Realice los siguientes pasos para configurar el servicio de nube OAuth en instancias de creación y publicación de AEM:

1. En la instancia de creación de AEM, vaya a **Herramientas** > Servicios **de** nube > Fuentes **** de datos > **global**. Toque el icono **Refsite Dynamics Integration** y Propiedades.
1. Vaya a la cuenta de Microsoft Azure Active Directory. Agregue la URL de configuración del servicio en la nube copiada en la configuración de URL **de** respuesta para la aplicación registrada. Guarde la configuración.
1. En la ficha Ajustes de autenticación, especifique la raíz **** del servicio, el ID **** del cliente, el secreto **** del cliente y la URL **** del recurso para la instancia de Microsoft Dynamics. Haga clic en **Conectar con OAuth** que redirige a la página de inicio de sesión de Microsoft Dynamics.
1. Proporcione sus credenciales de inicio de sesión. Una vez que haya iniciado sesión, se le redirigirá a la página de configuración del servicio en la nube de AEM Forms. Haga clic en **Guardar y cerrar**. Se guardó la configuración del servicio de nube.
1. Vaya a **Formularios** > Integraciones **de datos** > **We.Finance**. Seleccione Auto Insurance (Dynamics) y haga clic en Editar. Las entidades de Microsoft Dynamics se muestran en la ficha Fuentes de datos. Espere hasta que se recuperen todas las entidades de Microsoft Dynamics y se incluyan en la ficha de orígenes de datos.
1. Seleccione la entidad **AutoInsuranceRenewal y haga clic en Objeto** del modelo **** de prueba. En la sección de solicitud de entrada, especifique el valor del ID de cliente como &quot;900001&quot; y haga clic en **Prueba**. La sección Salida muestra los registros recuperados de Microsoft Dynamics para el ID de cliente 900001.
1. En la sección de solicitud de entrada, especifique el valor del ID de cliente como &quot;900001&quot; y haga clic en **Prueba**. La sección Salida muestra los registros recuperados de Microsoft Dynamics para el ID de cliente 900001.
1. Repita los pasos del 1 al 6 en la instancia de publicación.

## Configuración del programador de Adobe Sign {#scheduler}

Realice lo siguiente en las instancias de creación y publicación:

1. Vaya a la consola de configuración web de AEM en https://[server]:[host]/system/console/configMgr.
1. Toque y busque **[!UICONTROL Adobe Sign Configuration Service]** para abrirlo y configurarlo.
1. Configure **[!UICONTROL Status Update Scheduler Expression]** como **0 0/2 * * * ?**.

   >[!NOTE]
   >
   >La configuración del programador anterior comprueba el estado del servicio Adobe Sign cada dos minutos.

1. Toque **[!UICONTROL Guardar]**.

## Configurar el servicio de nube de Adobe Sign del sitio de referencia {#sign-service}

Realice lo siguiente en las instancias de creación y publicación:

1. Vaya a **Herramientas** > Servicios **de** nube > **Adobe Sign** > **global**. Seleccione **AEM Forms Reference Site Sign** y toque Propiedades.

   >[!CAUTION]
   >
   >Asegúrese de que la dirección URL se agrega a la lista de direcciones URL de redirección de la configuración OAuth de la aplicación API de Adobe Sign. `https://[host]:[ssl_port]/mnt/overlay/adobesign/cloudservices/adobesign/properties.html`

1. Especifique el ID de cliente y el secreto de la configuración OAuth de la aplicación Adobe Sign.
1. (Opcional) Seleccione la opción **[!UICONTROL Activar Adobe Sign para archivos adjuntos también]** y toque **[!UICONTROL Conectar con Adobe Sign]**. Agrega los archivos adjuntos a un formulario adaptable al documento correspondiente de Adobe Sign enviado para firmar.
1. Toque **[!UICONTROL Conectar con Adobe Sign]** e inicie sesión con sus credenciales de Adobe Sign.

## Configurar Forms Common Configuration Service {#anonymous}

Realice lo siguiente en la instancia de publicación para permitir el acceso a usuarios anónimos:

1. Vaya a la consola de configuración web de AEM en `https://[server]:[port]/system/console/configMgr`.
1. Toque y busque **[!UICONTROL Forms Common Configuration Service]** para abrirlo y configurarlo.
1. Configure el campo **[!UICONTROL Permitir]** para **[!UICONTROL todos los usuarios]**.
1. Toque **[!UICONTROL Guardar]**.

## Modificar el servicio de descanso para el modelo de datos de formulario {#fdm}

Realice lo siguiente en las instancias de creación y publicación:

1. Vaya a CRXDE en `https://[server]:[port]/crx/de/index.jsp`.
1. Vaya a **/conf/global/settings/cloudconfigs/fdm/roi-rest/jcr:content/swaggerFile** y abra el archivo swagger.
1. Actualice la configuración de host y puerto según su entorno.
1. Guarde la configuración.
1. (Solo **para** instancias de autor) Vaya a **Herramientas** > Servicios **de** nube > Fuentes **** de datos > **global**. Seleccione **reposabrazos** y toque **Propiedades**.Toque Configuración **de** autenticación y defina el tipo **de** autenticación como Autenticación **** básica. Especifique `admin`/ `admin`como nombre de usuario/contraseña para acceder al servicio. Toque **Guardar y cerrar**.

## Integración con Marketing Cloud {#integrate-with-marketing-cloud}

Puede integrar AEM Forms con Adobe Analytics y Adobe Target. Aunque Adobe Analytics le ayuda a generar informes y a analizar el rendimiento de los formularios adaptables, Adobe Target le ayuda a ofrecer experiencias personalizadas y a realizar pruebas A/B en formularios adaptables.

Para configurar Adobe Analytics y Adobe Target en AEM Forms, haga lo siguiente.

### Configurar Adobe Analytics {#configureanalytics}

La integración de AEM Forms con Adobe Analytics le permite supervisar y analizar la forma en que los clientes interactúan con los formularios y documentos. Le ayuda a identificar y corregir áreas problemáticas y a aumentar la tasa de conversión.

Para experimentar esta funcionalidad en el sitio de referencia, configure su cuenta de Analytics como se describe en [Configuración de análisis e informes](../../forms/using/configure-analytics-forms-documents.md).

Para generar un informe, los datos de inicialización se incluyen en los sitios de referencia. Antes de utilizar los datos de raíz, haga lo siguiente:

1. Asegúrese de que las configuraciones de análisis de We.Finance están disponibles en los servicios de nube de AEM. Puede encontrar servicios en la nube de una de las siguientes maneras:

   * Vaya a **[!UICONTROL Herramientas>Servicios de nube>Servicios]** de nube heredados o vaya a https://&lt;host>:&lt;puerto>/libs/cq/core/content/tools/cloudservices.html.
   * En la página Servicios **[!UICONTROL de]** nube, en la sección **[!UICONTROL Adobe Analytics]** , haga clic en `Show Configurations`. Puede ver las configuraciones de We.Finance disponibles. Haga clic para abrir la configuración. En la página de configuración, haga clic en **[!UICONTROL Editar]**. Proporcione una empresa, un nombre de usuario, un secreto compartido (contraseña) y un centro de datos válidos y haga clic en **[!UICONTROL Conectar con Analytics]**. Una vez que la conexión se haya establecido correctamente, haga clic en **[!UICONTROL Aceptar]** en el cuadro de diálogo de configuración. Configure el marco en la configuración de Analytics como se describe en [Configuración de análisis e informes](../../forms/using/configure-analytics-forms-documents.md).

1. Vaya a https://&lt;*host*>:&lt;*puerto*>/system/console/configMgr y haga lo siguiente:

   * En la página Configuración **[!UICONTROL de la consola]** web, busque y haga clic en Configuración **[!UICONTROL de análisis de]** AEM Forms.

   * En el campo **[!UICONTROL Marco]** de SiteCatalyst del cuadro de diálogo Configuración de análisis de AEM Forms, seleccione we-Finance(we-Finance) o we-gov(we-gov).
   * Haga clic en **[!UICONTROL Guardar]** y deje que la página se actualice.

1. Vaya a Forms Manager en https://&lt;host>:&lt;puerto>/aem/forms y haga lo siguiente:

   * Abra la carpeta We.Finance y seleccione el formulario para el que desea ver el informe.
   * Haga clic en Habilitar análisis en la barra de herramientas Acciones. Después de habilitar los análisis para el formulario, haga clic en Informe de Analytics. Puede ver un informe en blanco generado. Después de generar un informe en blanco, debe proporcionar los datos de inicialización enviados con el paquete refsite para generar un informe de análisis con fines de demostración.
   Los sitios de referencia proporcionan informes analíticos con datos de inicialización para casos de uso de tarjetas de crédito, hipotecas y alimentos.

### Configurar Target {#configure-target}

El sitio de referencia muestra la integración de AEM Forms con Adobe Target que le permite incluir contenido personalizado y dirigido en documentos adaptables. También permite crear pruebas A/B para formularios adaptables.

Para experimentar la integración en el sitio de referencia, haga lo siguiente para configurar Target en AEM:

1. Inicie el inicio rápido del autor con el argumento jvm `-Dabtesting.enabled=true` para habilitar la prueba A/B en el servidor.
   **Nota**: Si la instancia de AEM se está ejecutando en JBoss, que se inicia como un servicio desde la instalación de Turnkey, agregue el `-Dabtesting.enabled=true` parámetro en la siguiente entrada del `jboss\bin\standalone.conf.bat` archivo:
   `set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

1. Acceso `https://<hostname>:<port>/libs/cq/core/content/tools/cloudservices.html`.

1. En la sección **[!UICONTROL Adobe Target]** , haga clic en **[!UICONTROL Mostrar configuraciones]**. Puede ver la configuración de objetivo de We.Finance disponible. Haga clic para abrir la configuración. En la página de configuración, haga clic en **[!UICONTROL Editar]**. Se abre el cuadro de diálogo **[!UICONTROL Editar componente]** para la configuración.

1. Especifique el código de cliente, el correo electrónico y la contraseña asociados a la cuenta de Target. Seleccione el tipo de API como **[!UICONTROL REST]**.
1. Click **[!UICONTROL Connect to Adobe target]**. Una vez configurada correctamente la cuenta de Target, haga clic en **[!UICONTROL Aceptar]**. Puede ver que la configuración empaquetada tiene Target Framework.

1. Ir a `https://<hostname>:<port>/system/console/configMgr`.

1. Haga clic en Configuración **[!UICONTROL de destino de]** AEM Forms.
1. Seleccione un marco de Target.
1. En el campo Direcciones URL **[!UICONTROL de Target]** , especifique la dirección URL de AEM Forms. Por ejemplo: `https://<hostname>:<port>/`.

1. Haga clic en **[!UICONTROL Guardar]**.

Los casos de uso de aplicaciones de aplicación de tarjeta de crédito y de aplicación hipotecaria doméstica muestran cómo realizar pruebas A/B y muestran un informe con fines de demostración. Para obtener tutoriales, consulte [Tutorial del sitio de referencia We.Finance](../../forms/using/finance-reference-site-walkthrough.md).

## Next step {#next-step}

Ahora todos están listos para explorar el sitio de referencia. Para obtener más información sobre los pasos y el flujo de trabajo del sitio de referencia, consulte:

* [Recorrido por el sitio de referencia de We.Finance](../../forms/using/finance-reference-site-walkthrough.md)
* [Recorrido por el sitio de referencia de autoservicio de los empleados](../../forms/using/employee-self-service-reference-site.md)

