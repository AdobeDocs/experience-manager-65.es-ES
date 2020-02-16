---
title: Funciones en desuso y eliminadas
description: Notas de versión específicas de las funciones en desuso y eliminadas de Adobe Experience Manager 6.5.
uuid: 81d9a064-e712-4eff-bd3b-6e15513a5435
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: e8e2e01b-0117-48c3-86d8-609d29a147be
docset: aem65
translation-type: tm+mt
source-git-commit: 471b57a52efc849eb57201e6397221fa4f88c746

---


# Funciones en desuso y eliminadas {#deprecated-and-removed-features}

Adobe evalúa constantemente las capacidades del producto para reinventar o reemplazar con el tiempo las funciones antiguas con alternativas más modernas a fin de mejorar el valor general del cliente, siempre teniendo en cuenta la compatibilidad con versiones anteriores.

Para comunicar la eliminación o el reemplazo inminente de las capacidades de AEM, se aplican las siguientes reglas:

1. Primero se anuncia el desuso. Aunque están en desuso, las capacidades siguen estando disponibles, pero no se mejorarán aún más.
1. La eliminación de las capacidades en desuso ocurrirá en la siguiente versión principal, como mínimo. Se anunciará la fecha real de la eliminación.

Este proceso proporciona a los clientes un ciclo de lanzamiento para adaptar su implementación a una nueva versión o a la siguiente versión de una capacidad en desuso, antes de eliminarla.

## Funciones en desuso {#deprecated-features}

Esta sección detalla las funciones y capacidades en desuso de AEM 6.5. Normalmente, las funciones que se quieren eliminar de una versión futura se establecen primero en desuso y, a continuación, se proporciona una alternativa.

Se recomienda a los clientes que comprueben si utilizan la función o capacidad en su implementación actual, y que planifiquen el cambio de la implementación y usen la alternativa proporcionada.

<table>
 <tbody>
  <tr>
   <td><b>Área</b></td>
   <td><b>Función</b></td>
   <td><b>Reemplazo</b></td>
  </tr>
  <tr>
   <td>Ingregación de Creative Cloud</td>
   <td><p><a href="/help/assets/aem-cc-folder-sharing-best-practices.md">AEM to Creative Cloud Folder Sharing</a> se introdujo en AEM 6.2 como forma de proporcionar a los usuarios creativos acceso a los recursos de AEM para que puedan abrirlos en aplicaciones CC y cargar nuevos archivos o guardar cambios en AEM. Adobe Asset Link, la nueva capacidad de la aplicación Creative Cloud, proporciona experiencia de usuario mejorada y un acceso más eficaz a los recursos de AEM directamente desde Photoshop, InDesign e Illustrator.</p> <p>Adobe no tiene previsto realizar más mejoras en la integración del uso compartido de carpetas de Creative Cloud en AEM. Aunque la función se incluye en AEM, se recomienda a los clientes utilizar soluciones alternativas.</p> </td>
   <td>Se recomienda a los clientes que cambien a las nuevas funciones de integración de Creative Cloud, incluidas Adobe Asset Link o la aplicación de escritorio AEM. Consulte las <a href="/help/assets/aem-cc-integration-best-practices.md">prácticas recomendadas de integración de AEM y Creative Cloud</a> para obtener más información.</td>
  </tr>
  <tr>
   <td>Recursos</td>
   <td>
    <ol>
     <li>AssetDownloadServlet está desactivado de forma predeterminada para las instancias publicadas. Para obtener más información, consulte la <a href="/help/sites-administering/security-checklist.md">AEM security checklist (lista de comprobación de seguridad de AEM)</a>.</li>
     <li>Si un usuario no tiene los permisos (de lectura y escritura) suficientes en /content/dam/collections, el usuario no puede crear una colección.</li>
    </ol> </td>
   <td>
    <ol>
     <li>Configuración descrita en la <a href="/help/sites-administering/security-checklist.md">AEM Security checklist (lista de comprobación de seguridad de AEM)</a>.</li>
     <li>Coincidir con la configuración de control de acceso del usuario y comprobar los permisos adecuados.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Adobe Search &amp; Promote</td>
   <td><p>La integración con Adobe Search &amp; Promote está en desuso.</p> <p>Adobe no tiene previsto realizar más mejoras en la integración de Search &amp; Promote. Tenga en cuenta que la integración de Search &amp; Promote será totalmente compatible mientras esté en desuso.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Administrador de etiquetas DTM</td>
   <td>La integración con DTM (Dynamic Tag Manager) está en desuso.</td>
   <td>Utilice Adobe Experience Platform Launch como administrador de etiquetas</td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>Al añadir la capacidad de AEM para conectarse al servicio de Adobe Target mediante la API Adobe Target Standard basada en Adobe E/S (API de Rest) en AEM 6.5, el método de la API de Target Classic (XML) quedará en desuso.</td>
   <td><a href="https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html">Vuelva a configurar la integración para utilizar la nueva API</a></td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>El uso de mbox.js basado en la integración con Adobe Target en AEM está en desuso.</td>
   <td>Utilice at.js 1.x</td>
  </tr>
  <tr>
   <td>Comercio</td>
   <td><p><a href="https://github.com/adobe/commerce-cif-api" target="_blank">CIF REST</a> se proporcionó en 2018 como un conjunto de microservicios para permitir integraciones entre AEM y motores de comercio.</p> <p>Después de que Adobe adquirió Magento a mediados de 2018, Adobe decidió cambiar su enfoque por dos motivos: </p> <p><strong>1.</strong> Magento tiene su propio conjunto de API de comercio (REST y GraphQL) y no es recomendable mantener dos conjuntos de API </p> <p><strong>2.</strong> Las tendencias del mercado indicaban que los clientes avanzaban hacia GraphQL, ya que es una forma más eficiente de consultar datos. En 2019, Adobe lanzó el nuevo Commerce Integration Framework utilizando las API GraphQL de Magento como fuente de verdad.</p> <p>Adobe no planea realizar ninguna inversión adicional en CIF REST. Se recomienda encarecidamente a los clientes que utilicen la solución de reemplazo.</p> </td>
   <td><p>Para las integraciones de AEM-Magento, cambie a <a href="https://github.com/adobe/aem-cif-project-archetype" target="_blank">AEM CIF Archetype</a>y componentes principales de CIF de <a href="https://github.com/adobe/aem-core-cif-components" target="_blank">AEM</a></p> <p>Consulte la Integración de <a href="https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md" target="_blank">AEM y Magento mediante Commerce Integration Framework</a> para obtener más información.</p> <p>El apoyo a integraciones de terceros (distintas de Magento) con el nuevo enfoque está en nuestra hoja de ruta.</p> </td>
  </tr>
  <tr>
   <td>Componentes (AEM Sites)</td>
   <td><p>Adobe no tiene previsto realizar mejoras adicionales en la mayoría de los componentes de base almacenados en /libs/foundation/components.</p> <p>Busque las propiedades <strong>cq:deprecated</strong> y <strong>cq:deprecatedReason</strong> en la carpeta de componentes.</p> <p>AEM 6.5 incluye los componentes de base y los clientes que actualicen desde versiones anteriores pueden seguir utilizándolos tal cual. Además, los componentes de base siguen siendo totalmente compatibles mientras están en desuso. </p> </td>
   <td>Se recomienda a los clientes que utilicen los componentes principales para futuros proyectos. Existing sites can remain as is or use the <a href="https://github.com/adobe/aem-modernize-tools">AEM Modernize Tools Suite</a> to refactor the site to use Core Components.</td>
  </tr>
  <tr>
   <td>Componentes (AEM Sites)</td>
   <td>Los componentes del Importador de diseños /libs/wcm/designimporter/components se han marcado "en desuso" a partir de la versión 6.5. Igualmente, Adobe no tiene previsto realizar mejoras adicionales en la implementación del importador de diseños.</td>
   <td>Adobe planea proporcionar una implementación alternativa del caso de uso en próximas versiones.</td>
  </tr>
  <tr>
   <td>Componentes (AEM Forms)</td>
   <td><p>El paso Firma permite a los usuarios comprobar y firmar un formulario adaptable. En versiones anteriores, el paso de firma podía utilizar los componentes Adobe Sign y Scribble Signature como campos de firma. En AEM 6.5 Forms, la experiencia de firma basada en firma Scribble de Signature Step está obsoleta.</p> </td>
   <td>
    <ul>
     <li>Si ha realizado una instalación nueva:
      <ul>
       <li>Utilice la experiencia de firma basada en Adobe Sign en un paso de firma en un formulario adaptable.</li>
       <li>Utilice el componente de firma manuscrita en un formulario adaptable, una comunicación interactiva y formularios HTML5.</li>
      </ul> </li>
     <li>Si ha actualizado una versión anterior a AEM 6.5 Forms:<br />
      <ul>
       <li>Continúe utilizando la experiencia de firma basada en la firma Scribble de Signature Step con formularios que ya utilizan la función.<br /> </li>
       <li>Cuando cree un nuevo formulario, utilice el componente de firma independiente Scribble o la experiencia de firma basada en Adobe Sign en un paso de firma. </li>
      </ul> </li>
    </ul> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>Foundation</td>
   <td><p>Marco de descarga de Granite</p> <p>Adobe no tiene previsto realizar más mejoras en el marco de descarga introducido en la versión 5.6.1 para externalizar el procesamiento de recursos. </p> </td>
   <td>Adobe trabaja en un marco de descarga nativo de la nube de próxima generación.</td>
  </tr>
  <tr>
   <td>Desarrolladores</td>
   <td><p>Hobbes.js</p> <p>Adobe no planea realizar más mejoras en el marco de pruebas de la interfaz de usuario de hobbes.js.</p> </td>
   <td>Adobe recomienda que los clientes utilicen la automatización Selenium.</td>
  </tr>
  <tr>
   <td>Desarrolladores</td>
   <td><p>Biblioteca de cliente de la interfaz de usuario de jQuery</p> <p>Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de la interfaz de usuario de jQuery incluida como parte de la distribución (Quickstart)</p> </td>
   <td>Adobe recomienda a los clientes que aún necesitan la IU de jQuery para que su código se añada a su base de código de proyecto.</td>
  </tr>
  <tr>
   <td>Desarrolladores</td>
   <td><p>Biblioteca de cliente de jQuery Animation (granite.jquery.activation)</p> <p>Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de animación de jQuery incluida como parte de la distribución (Quickstart)</p> </td>
   <td>Adobe recomienda a los clientes que aún necesitan jQuery Animations para que su código se añada a su base de código de proyecto.</td>
  </tr>
  <tr>
   <td>Desarrolladores</td>
   <td><p>Biblioteca de cliente de Handlebars</p> <p>Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de Handlebars incluida como parte de la distribución (Quickstart)</p> </td>
   <td>Adobe recomienda a los clientes que aún necesitan Handlebars para su código que lo añadan a su base de código de proyecto.</td>
  </tr>
  <tr>
   <td>Desarrolladores</td>
   <td><p>Biblioteca de cliente de Lawnchair</p> <p>Adobe no tiene previsto seguir manteniendo ni actualizando la biblioteca de cliente de Lawnchair incluida como parte de la distribución (Quickstart)</p> </td>
   <td>Adobe recomienda a los clientes que aún necesitan Lawnsilla para su código que lo añadan a su base de código de proyecto.</td>
  </tr>
  <tr>
   <td>Desarrolladores</td>
   <td><p>Biblioteca de cliente de Granite.Sling.js</p> <p>Adobe no tiene previsto mejorar la biblioteca de cliente de Granite.Sling.js incluida como parte de la distribución (Quickstart)</p> </td>
   <td>Adobe recomienda a los clientes que dependen de la capacidad de la biblioteca para cambiar el factor de su código y dejar de utilizarlo.</td>
  </tr>
  <tr>
   <td>Desarrolladores</td>
   <td>Usar YUI para comprimir o minimizar las bibliotecas de cliente de JavaScript. Adobe no tiene previsto actualizar la biblioteca de YUI. Hasta AEM 6.4, la IU era la predeterminada para reducir el código JavaScript con la opción de cambiar a Google Closure Compiler (GCC). A partir de AEM 6.5, la opción GCC es la opción predeterminada.</td>
   <td>Adobe recomienda a los clientes que actualicen a AEM 6.5 para cambiar a GCC para su implementación</td>
  </tr>
  <tr>
   <td>Desarrolladores</td>
   <td><p>Editor de diálogos estándar de interfaz de usuario en CRXDE Lite</p> <p>Adobe no tiene previsto mejorar el editor de diálogos estándar de interfaz de usuario incluido como parte de la distribución (Quickstart)</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Funciones eliminadas {#removed-features}

Esta sección enumera las funciones y funciones que se han eliminado de AEM 6.5. Las versiones anteriores tenían estas capacidades marcadas como obsoletas.

| Área | Función | Reemplazo |
|--- |--- |--- |
| Activity Map de Analytics | Versión del Activity Map que se incluye en AEM. | Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM. Utilice el complemento [ActivityMap proporcionado por Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |
| Integraciones | La integración de ExactTarget se ha eliminado de la distribución predeterminada (QuickStart) y ya no está disponible. | Sin reemplazo |
| Integraciones | Se ha eliminado la integración de Salesforce Force API de la distribución predeterminada (Quickstart) y ahora es un paquete adicional para instalar desde PackageShare. | Esta función aún se encuentra disponible. |
| Formularios | Se ha eliminado la compatibilidad con el servicio Adobe Central Migration Bridge, ya que el producto Adobe Central ya no es compatible. | Sin reemplazo |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | Sin reemplazo |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | Sin reemplazo |
| Desarrolladores | Se ha eliminado Firebug Lite de la distribución predeterminada (Quickstart) | Usar las consolas de desarrollador incorporadas en el navegador |
| Desarrolladores | Remove `customJavaScriptPath` support in HTML Client Library Manager. | Sin reemplazo |
| Recursos | La función de descarga de recursos se ha eliminado en AEM 6.5 | Sin reemplazo |
| Caché | `system/console/slingjsp` ya no está disponible en AEM 6.5. | Clases y ligero caché se almacena en el paquete Apache Sling Commons FileSystem ClassLoader. Puede comprobar el número de paquete en la consola web de AEM y quitar la carpeta de caché directamente del sistema de archivos (`crx-quickstart/launchpad/felix/bundle<ID>`). |

## Anuncio previo para la siguiente versión {#pre-announcement-for-next-release}

Esta sección se utiliza para anunciar con antelación los cambios en futuras versiones, que no se consideran en desuso, pero que afectarán a los clientes. Se proporcionan con fines de planificación.

| Área | Función | Anuncio |
|--- |--- |--- |
| Foundation | Marco de interfaz de usuario | Adobe tiene previsto dejar de utilizar los componentes de Coral UI 2 en 2019. Coral UI 3 se ha introducido con AEM 6.2 y AEM 6.5 se basa completamente en Coral 3. Adobe recomienda a los clientes y socios que hayan creado interfaces de usuario personalizadas con Coral 2 que las actualicen a Coral 3. Adobe proporciona una herramienta para convertir los cuadros de diálogo de Coral 2 a Coral 3 [Más información](/help/sites-developing/dialog-conversion.md). |
