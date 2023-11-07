---
title: Integración con Adobe Dynamic Tag Management
seo-title: Integrating with Adobe Dynamic Tag Management
description: Obtenga información sobre la integración con Dynamic Tag Management de Adobe.
seo-description: Learn about integration with Adobe Dynamic Tag Management.
uuid: cbb9f942-44e3-4cd5-b07d-4298a7a08376
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b8c7a20a-7694-4a49-b66a-060720f17dad
exl-id: 1e0821f5-627f-4262-ba76-62303890e112
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '2205'
ht-degree: 3%

---

# Integración con Adobe Dynamic Tag Management {#integrating-with-adobe-dynamic-tag-management}

Integrar [Adobe Dynamic Tag Management](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) AEM con para que pueda utilizar sus propiedades web de Dynamic Tag Management AEM para realizar un seguimiento de los sitios de la. Dynamic Tag Management permite a los especialistas en marketing administrar etiquetas para recopilar datos y distribuir datos entre sistemas de marketing digital. Por ejemplo, utilice Dynamic Tag Management AEM para recopilar datos de uso para su sitio web de y distribuir los datos para su análisis en Adobe Analytics o Adobe Target.

Antes de realizar la integración, debe crear Dynamic Tag Management [propiedad web](https://microsite.omniture.com/t2/help/en_US/dtm/#Web_Properties) AEM que realiza un seguimiento del dominio del sitio de la. El [opciones de alojamiento](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) AEM La configuración de la propiedad web debe configurarse para que pueda configurar el acceso a las bibliotecas de Dynamic Tag Management de forma que se pueda configurar el acceso a las mismas.

Después de configurar la integración, los cambios en las herramientas y reglas de implementación de Dynamic Tag Management no requieren que cambie la configuración de Dynamic Tag Management AEM en la. AEM Los cambios estarán disponibles automáticamente para su.

>[!NOTE]
>
>AEM Si utiliza DTM con una configuración proxy personalizada, debe configurar ambas configuraciones proxy del cliente HTTP, ya que algunas funcionalidades de las API 3.x y otras de las API 4.x se utilizan en las que se utilizan las API 3.x.
>
>* 3.x está configurado con [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado con [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

## Opciones de implementación {#deployment-options}

Las siguientes opciones de implementación afectan a la configuración de la integración con Dynamic Tag Management.

### Alojamiento de Dynamic Tag Management {#dynamic-tag-management-hosting}

AEM La aplicación admite Dynamic Tag Management AEM que está alojado en la nube o en el servidor de correo de.

* Alojado en la nube: las bibliotecas de JavaScript de Dynamic Tag Management AEM se almacenan en la nube y las páginas del usuario hacen referencia a ellas directamente.
* AEM alojadas: Dynamic Tag Management genera bibliotecas de javascript. AEM utiliza un modelo de flujo de trabajo para obtener e instalar las bibliotecas.

El tipo de alojamiento que utiliza la implementación determina algunas de las tareas de configuración e implementación que realiza. Para obtener información sobre las opciones de alojamiento, consulte [Alojamiento: ficha Insertar](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) en la Ayuda de Dynamic Tag Management.

### Biblioteca de ensayo y producción {#staging-and-production-library}

AEM Decida si la instancia de autor de la utiliza el código de ensayo o producción de Dynamic Tag Management.

Normalmente, la instancia de autor utiliza las bibliotecas de ensayo de Dynamic Tag Management y la instancia de producción utiliza las bibliotecas de producción. Este escenario le permite utilizar la instancia de autor para probar configuraciones de Dynamic Tag Management no aprobadas.

Si lo desea, la instancia de autor puede utilizar las bibliotecas de producción. Hay disponibles complementos de explorador web que permiten cambiar entre el uso de bibliotecas de ensayo para realizar pruebas cuando las bibliotecas están alojadas en la nube.

### Uso del vínculo de implementación de Dynamic Tag Management {#using-the-dynamic-tag-management-deployment-hook}

AEM Cuando aloja las bibliotecas de Dynamic Tag Management, puede utilizar el servicio de enlace de implementación de Dynamic Tag Management AEM para insertar automáticamente las actualizaciones de la biblioteca en el. Las actualizaciones de la biblioteca se insertan cuando se realizan cambios en las bibliotecas, como cuando se editan las propiedades web de Dynamic Tag Management.

Para utilizar el vínculo de implementación, Dynamic Tag Management AEM debe poder conectarse a la instancia de implementación que aloja las bibliotecas de. Usted debe [AEM habilitar el acceso a la](/help/sites-administering/dtm.md#enabling-access-for-the-deployment-hook-service) para los servidores de Dynamic Tag Management.

AEM AEM En algunas circunstancias, no se puede acceder a los servidores de seguridad, por ejemplo, cuando se encuentran detrás de un servidor de seguridad, por ejemplo, cuando se encuentran en el mismo lugar, se puede acceder a los. AEM En estos casos, puede utilizar la opción del importador de encuestas de para recuperar periódicamente las bibliotecas. Una expresión de trabajo cron dicta la programación de las descargas de biblioteca.

## Habilitar el acceso al servicio de enlace de implementación {#enabling-access-for-the-deployment-hook-service}

Habilite el servicio de enlace de implementación de Dynamic Tag Management AEM AEM para acceder a las bibliotecas de para que el servicio pueda actualizar las bibliotecas alojadas en el servidor de la aplicación de manera que puedan acceder a las bibliotecas alojadas en el sitio de la aplicación de la implementación de la. Especifique la dirección IP de los servidores de Dynamic Tag Management que actualizan las bibliotecas de ensayo y producción según sea necesario:

* Ensayo: `107.21.99.31`
* Producción: `23.23.225.112` y `204.236.240.48`

Realice la configuración utilizando el [Consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o una [`sling:OsgiConfig`](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) nodo:

* En la consola web, utilice el elemento Configuración de enlace de implementación de DTM de Adobe de la página Configuración.
* Para una configuración OSGi, el PID de servicio es `com.adobe.cq.dtm.impl.servlets.DTMDeployHookServlet`.

En la tabla siguiente se describen las propiedades que se deben configurar.

| Propiedad de la consola web | Propiedad OSGi | Descripción |
|---|---|---|
| Lista blanca de IP de DTM de ensayo | `dtm.staging.ip.whitelist` | La dirección IP del servidor de Dynamic Tag Management que actualiza las bibliotecas de ensayo. |
| Lista blanca de IP de DTM de producción | `dtm.production.ip.whitelist` | La dirección IP del servidor de Dynamic Tag Management que actualiza las bibliotecas de producción. |

## Creación de la configuración de Dynamic Tag Management {#creating-the-dynamic-tag-management-configuration}

AEM Cree una configuración en la nube para que la instancia de pueda autenticarse con Dynamic Tag Management e interactuar con la propiedad web.

>[!NOTE]
>
>Evite la inclusión de dos códigos de seguimiento de Adobe Analytics en las páginas cuando la propiedad web de DTM incluya la herramienta Adobe Analytics y también esté utilizando [Perspectiva de contenido](/help/sites-authoring/content-insights.md). En su [Configuración de nube de Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md#configuring-the-connection-to-adobe-analytics), seleccione la opción No incluir código de seguimiento.

### Configuración general {#general-settings}

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>Testigo API</td>
   <td>El valor de la propiedad Token de API de su cuenta de usuario de Dynamic Tag Management. AEM utiliza esta propiedad para autenticarse con Dynamic Tag Management.</td>
  </tr>
  <tr>
   <td>Compañía</td>
   <td>La empresa con la que está asociado su ID de inicio de sesión.</td>
  </tr>
  <tr>
   <td>Propiedad</td>
   <td>AEM Nombre de la propiedad web que ha creado para administrar las etiquetas del sitio de la.</td>
  </tr>
  <tr>
   <td>Incluir el código de producción en el campo Autor</td>
   <td><p>AEM Seleccione esta opción para que las instancias de autor y publicación de la utilicen la versión de producción de las bibliotecas de Dynamic Tag Management. </p> <p>Cuando esta opción no está seleccionada, la configuración de ensayo se aplica a la instancia de autor y la configuración de producción se aplica a la instancia de publicación.</p> </td>
  </tr>
 </tbody>
</table>

### Propiedades de alojamiento propio: ensayo y producción {#self-hosting-properties-staging-and-production}

Las siguientes propiedades de la configuración de Dynamic Tag Management AEM permiten a los usuarios de alojar las bibliotecas de Dynamic Tag Management. AEM Las propiedades permiten a los usuarios descargar e instalar las bibliotecas de. De forma opcional, puede actualizar automáticamente las bibliotecas para asegurarse de que reflejen los cambios realizados en la aplicación de administración Dynamic Tag Management.

Algunas propiedades utilizan valores que se obtienen de la sección Descarga de biblioteca de la pestaña Insertar para la propiedad web de Dynamic Tag Management. Para obtener más información, consulte [Descarga de biblioteca](https://microsite.omniture.com/t2/help/en_US/dtm/#Library_Download) en la Ayuda de Dynamic Tag Management.

>[!NOTE]
>
>Cuando aloje el paquete Dynamic Tag Management en la aplicación de la biblioteca, la descarga de la biblioteca debe estar habilitada en Dynamic Tag Management para poder crear la configuración de, por lo que debe habilitarse la opción de descarga de biblioteca de la aplicación de AEM. Además, Akamai debe estar habilitado, ya que Akamai proporciona las bibliotecas para la descarga.

Al alojar las bibliotecas de Dynamic Tag Management AEM AEM en la, configura automáticamente algunas propiedades de la propiedad web según su configuración. Consulte las descripciones de la tabla siguiente.

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>Utilizar el alojamiento propio</td>
   <td>Seleccione cuando aloje el archivo de biblioteca de Dynamic Tag Management AEM en el archivo de la biblioteca de la biblioteca de la biblioteca de la biblioteca de. Si selecciona esta opción, aparecerán las demás propiedades de esta tabla.</td>
  </tr>
  <tr>
   <td>URL del paquete DTM</td>
   <td>Dirección URL que se utilizará para descargar la biblioteca de Dynamic Tag Management. Obtenga este valor de la sección Descargar direcciones URL de la página Descarga de biblioteca de Dynamic Tag Management. Por motivos de seguridad, este valor debe configurarse manualmente.</td>
  </tr>
  <tr>
   <td>Flujo de trabajo de descarga</td>
   <td><p>Modelo de flujo de trabajo que se utiliza para descargar e instalar la biblioteca de Dynamic Tag Management. El modelo predeterminado es Descarga del paquete DTM predeterminado. Utilice este modelo a menos que haya creado uno personalizado.</p> <p>El flujo de trabajo de descarga predeterminado activa automáticamente las bibliotecas cuando se descargan.</p> </td>
  </tr>
  <tr>
   <td>Sugerencia de dominio</td>
   <td><p>AEM (Opcional) El dominio del servidor de que aloja la biblioteca de Dynamic Tag Management. Especifique un valor para anular el dominio predeterminado configurado para <a href="/help/sites-developing/externalizer.md">Servicio Day CQ Link Externalizer</a>.</p> <p>Cuando se conecta a Dynamic Tag Management AEM, utiliza este valor para configurar la ruta HTTP de ensayo o la ruta HTTP de producción de las propiedades de descarga de biblioteca de la propiedad web de Dynamic Tag Management.</p> </td>
  </tr>
  <tr>
   <td>Sugerencia de dominio seguro</td>
   <td><p>AEM (Opcional) El dominio del servidor de que aloja la biblioteca de Dynamic Tag Management a través de HTTPS. Especifique un valor para anular el dominio predeterminado configurado para <a href="/help/sites-developing/externalizer.md">Servicio Day CQ Link Externalizer</a>.</p> <p>Cuando se conecta a Dynamic Tag Management AEM, utiliza este valor para configurar la ruta HTTPS de ensayo o la ruta HTTPS de producción de las propiedades de descarga de biblioteca de la propiedad web de Dynamic Tag Management.</p> </td>
  </tr>
  <tr>
   <td>Secreto compartido</td>
   <td><p>(Opcional) Secreto compartido que se utilizará para descifrar la descarga. Obtenga este valor del campo Secreto compartido de la página Descarga de biblioteca de Dynamic Tag Management.</p> <p><strong>Nota:</strong> Debe tener el <a href="https://www.openssl.org/docs/apps/openssl.html">OpenSSL</a> AEM AEM bibliotecas instaladas en el equipo en el que se ha instalado la aplicación de modo que se puedan descifrar las bibliotecas descargadas, de manera que se puedan descifrar las bibliotecas que se han descargado.</p> </td>
  </tr>
  <tr>
   <td>Habilitar el importador de encuestas</td>
   <td><p>(Opcional) Seleccione para descargar e instalar periódicamente la biblioteca de Dynamic Tag Management y asegurarse de que está utilizando una versión actualizada. Cuando se selecciona, Dynamic Tag Management no envía solicitudes de POST HTTP a la dirección URL del vínculo de implementación.</p> <p>AEM La configuración automática de la propiedad Implementación de URL de enlace de las propiedades de Descarga de biblioteca de la propiedad web de Dynamic Tag Management se configura automáticamente. Cuando se selecciona, la propiedad se configura sin valor. Cuando no se selecciona, la propiedad se configura con la dirección URL de la configuración de Dynamic Tag Management.</p> <p>Habilite el importador de encuestas cuando el vínculo de implementación de Dynamic Tag Management AEM AEM no se pueda conectar a la red, por ejemplo, cuando el usuario esté detrás de un cortafuegos, o cuando el vínculo de implementación de Dynamic no se pueda conectar a la red de seguridad.</p> </td>
  </tr>
  <tr>
   <td>Expresión de programación</td>
   <td>(Aparece y es necesario cuando se selecciona Habilitar el importador de encuestas). Expresión cron que controla cuándo se descargan las bibliotecas de Dynamic Tag Management.</td>
  </tr>
 </tbody>
</table>

![chlimage_1-352](assets/chlimage_1-352.png)

### Propiedades de alojamiento en la nube: ensayo y producción {#cloud-hosting-properties-staging-and-production}

Configure las siguientes propiedades para la configuración de Dynamic Tag Management cuando Dynamic Tag Configuration está alojada en la nube.

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>Utilizar el alojamiento propio</td>
   <td>Desactive esta opción cuando el archivo de biblioteca de Dynamic Tag Management esté alojado en la nube.</td>
  </tr>
  <tr>
   <td>Código de encabezado</td>
   <td><p>El código de encabezado para el ensayo que se obtiene de Dynamic Tag Management para su host. Este valor se rellena automáticamente al conectarse a Dynamic Tag Management.</p> <p> Para ver el código en Dynamic Tag Management, haga clic en la pestaña Insertar y, a continuación, haga clic en el nombre de host. Expanda la sección Código de encabezado y haga clic en el área Copiar código incrustado del código incrustado de ensayo o del código incrustado de producción según sea necesario.</p> </td>
  </tr>
  <tr>
   <td>Código de pie de página</td>
   <td><p>El código de pie de página para el ensayo que se obtiene de Dynamic Tag Management para su host. Este valor se rellena automáticamente al conectarse a Dynamic Tag Management.</p> <p>Para ver el código en Dynamic Tag Management, haga clic en la pestaña Insertar y, a continuación, haga clic en el nombre de host. Expanda la sección Código de pie de página y haga clic en el área Copiar código incrustado del código incrustado de ensayo o del código incrustado de producción según sea necesario.</p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-353](assets/chlimage_1-353.png)

El siguiente procedimiento utiliza la interfaz de usuario táctil para configurar la integración con Dynamic Tag Management.

1. En el carril, haga clic en Herramientas > Operaciones > Cloud > Cloud Service.
1. En el área de Dynamic Tag Management, aparece uno de los siguientes vínculos para agregar una configuración:

   * Haga clic en Configurar ahora si esta es la primera configuración que agrega.
   * Haga clic en Mostrar configuraciones y, a continuación, haga clic en el vínculo + situado junto a Configuraciones disponibles si se han creado una o varias configuraciones.

   ![chlimage_1-354](assets/chlimage_1-354.png)

1. Escriba un título para la configuración y haga clic en Crear.
1. En el campo Token de API, introduzca el valor de la propiedad Token de API de su cuenta de usuario de Dynamic Tag Management.

   Para obtener el valor de su token de API, póngase en contacto con el servicio de atención al cliente de DTM.

   >[!NOTE]
   >
   >El token de API no caduca hasta que el usuario de Dynamic Tag Management lo solicita explícitamente.

   ![chlimage_1-355](assets/chlimage_1-355.png)

1. Haga clic en Conectarse a DTM. AEM Se autentica con Dynamic Tag Management y recupera la lista de empresas a las que está asociada su cuenta.
1. AEM Seleccione la Empresa y, a continuación, seleccione la Propiedad que está utilizando para realizar un seguimiento del sitio de.
1. Si utiliza código de ensayo en la instancia de autor, anule la selección de Incluir código de producción en Author.
1. Proporcione valores para las propiedades de las pestañas Configuración de ensayo y Configuración de producción si es necesario y, a continuación, haga clic en Aceptar.

## Descarga manual de la biblioteca de Dynamic Tag Management {#manually-downloading-the-dynamic-tag-management-library}

Descargue manualmente las bibliotecas de Dynamic Tag Management AEM para actualizarlas inmediatamente en el momento en que lo haga de forma. Por ejemplo, realice la descarga manual si desea probar una biblioteca actualizada antes de que el importador de encuestas programe la descarga automática de la biblioteca.

1. En el carril, haga clic en Herramientas > Operaciones > Cloud > Cloud Service.
1. En el área de Dynamic Tag Management, haga clic en Mostrar configuraciones y, a continuación, haga clic en la configuración.
1. En el área Configuración de ensayo o Configuración de producción, haga clic en el botón Déclencheur Descargar flujo de trabajo para descargar e implementar el paquete de biblioteca.

   ![chlimage_1-356](assets/chlimage_1-356.png)

>[!NOTE]
>
>Los archivos descargados se almacenan en `/etc/clientlibs/dtm/my config/companyID/propertyID/servertype`.
>
>Las siguientes se toman directamente de su [Configuración de DTM](#creating-the-dynamic-tag-management-configuration).
>
>* `myconfig`
>* `companyID`
>* `propertyID`
>* `servertype`
>

## Asociación de una configuración de Dynamic Tag Management al sitio {#associating-a-dynamic-tag-management-configuration-with-your-site}

Asocie la configuración de Dynamic Tag Management AEM con las páginas del sitio web para que agregue la secuencia de comandos necesaria a las páginas. Asocie la página raíz del sitio con la configuración. Todos los descendientes de esa página heredan la asociación. Si es necesario, puede anular la asociación en una página descendiente.

Utilice el siguiente procedimiento para asociar una página y sus descendientes a una configuración de Dynamic Tag Management.

1. Abra la página raíz del sitio en la IU clásica.
1. Utilice el Sidekick para abrir las propiedades de la página.
1. En la pestaña Cloud Service, haga clic en Agregar servicio, seleccione Dynamic Tag Management y, a continuación, haga clic en Aceptar.

   ![chlimage_1-357](assets/chlimage_1-357.png)

1. Utilice el menú desplegable Dynamic Tag Management para seleccionar la configuración y, a continuación, haga clic en Aceptar.

Utilice el siguiente procedimiento para anular la asociación de configuración heredada de una página. La anulación afecta a la página y a todos sus descendientes.

1. Abra la página en la IU clásica.
1. Utilice el Sidekick para abrir las propiedades de la página.
1. En la ficha Cloud Service, haga clic en el icono de candado situado junto a la propiedad Heredado de y, a continuación, haga clic en Sí en el cuadro de diálogo de confirmación.

   ![chlimage_1-358](assets/chlimage_1-358.png)

1. Elimine o seleccione una configuración de Dynamic Tag Management diferente y, a continuación, haga clic en Aceptar.
