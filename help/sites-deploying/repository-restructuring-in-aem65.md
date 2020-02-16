---
title: Reestructuración del repositorio en AEM 6.5
seo-title: Reestructuración del repositorio en AEM 6.5
description: Obtenga información sobre la reestructuración de repositorios en AEM 6.5
seo-description: Obtenga información sobre la reestructuración de repositorios en AEM 6.5
uuid: bc577c82-3279-4ddd-898c-607864868db0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 274a7f5a-d509-4ca9-9ae5-30e48f34f171
docset: aem65
redirecttarget: /content/help/en/experience-manager/6-5/help/sites-deploying/repository-restructuring.html
translation-type: tm+mt
source-git-commit: bd0dc09ea230416ad3544d14440b7b74b80ec406

---


# Reestructuración del repositorio en AEM 6.5 {#repository-restructuring-in-aem}

## Introducción {#introduction}

Antes de AEM 6.5, el código de cliente se implementaba en áreas impredecibles del JCR que estaban sujetas a cambios en las actualizaciones. Debido a esto, las versiones formales de AEM (versiones principales, paquetes de funciones, paquetes de servicios o revisiones) solían sobrescribir el código, la configuración o el contenido personalizados. Además, los cambios de cliente a veces sobrescriben el contenido o el código de producto de AEM, lo que rompe la funcionalidad del producto.

Estos conflictos no siempre se podían resolver automáticamente, lo que requería un tiempo de procesamiento considerable para que se detectaran, y requería la intervención humana para resolverlos, cuya resolución no siempre estaba clara. Al delimitar claramente las jerarquías del código de producto y del código de cliente de AEM, estos conflictos se pueden evitar.

Con este fin, a partir de AEM 6.5 y para continuar en futuras versiones, el contenido se está reestructurando desde `/etc` otras carpetas del repositorio, junto con directrices sobre el contenido que va a donde va, respetando las siguientes normas de alto nivel:

* El código de producto de AEM siempre se colocará en `/libs`, lo que no debe sobrescribirse con el código personalizado
* El código personalizado debe colocarse en `/apps`, `/content`y `/conf`

Este artículo está organizado en tres secciones, que representan el tipo de contenido del que se ha sacado `/etc`:

1. Configuración
1. Bibliotecas del cliente
1. Varios

Cada sección incluye:

* una tabla con las ubicaciones reestructuradas y el contexto adicional. En un futuro próximo, se espera que las tablas tengan un formato más plano para mejorar la legibilidad.
* una estrategia de extensibilidad que permite que el código personalizado extienda correctamente el código de la aplicación AEM que reside en `/libs`.

## Compatibilidad con versiones anteriores {#backwards-compatibility}

En la mayoría de los casos, la compatibilidad con versiones anteriores se mantiene después de actualizar a AEM 6.5. Esto se logra gracias a que el código de producto conserva y respeta las ubicaciones antiguas, además de las nuevas ubicaciones que se agregan. En la mayoría de los casos, la lógica condicional se utiliza para comprobar si existe la carpeta heredada y para leer el contenido desde allí en lugar de la nueva ubicación.

En su propio cronograma después de la actualización a la versión 6.5, se recomienda a los clientes que eliminen las ubicaciones antiguas para que se utilice el contenido en las nuevas ubicaciones. Las tablas siguientes incluyen instrucciones para adherirse a la nueva estructura de contenido por ubicación.

>[!NOTE]
>
>Una instancia actualizada en el lugar incluirá ubicaciones de contenido antiguas además de las nuevas ubicaciones. Una nueva instalación del desarrollador solo incluirá las nuevas ubicaciones.

## Cómo leer las tablas {#how-to-read-the-tables}

La tabla de cada sección incluye:

* la solución AEM (sitios, recursos, formularios, etc.) para la que este contenido es relevante
* la ubicación antigua (6.4 y anteriores)
* la nueva ubicación 6.5
* Instrucciones para alinearse con la nueva estructura de contenido. Por ejemplo, puede ser necesario ejecutar una secuencia de comandos o mover archivos manualmente en las semanas o meses posteriores a una actualización de 6.5
* El método que AEM ha utilizado para mantener la compatibilidad con versiones anteriores de ubicaciones de contenido antiguas para clientes que actualizan a AEM 6.5 desde una versión anterior

## Configuración {#configuration}

Las ubicaciones de contenido de esta sección generalmente hacen referencia a contenido que reside en una `/settings` carpeta en `/libs`, `/apps`o `/conf`.

### Estrategia de extensibilidad {#extensibility-strategy}

En general, pero con algunas excepciones, el contenido de esta sección puede ampliarse con la función de configuración [](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) según el contexto de Apache Sling.

En pocas palabras, la Configuración según el contexto permite que el contenido de una parte del repositorio se superponga varias veces por contenido de otras partes del repositorio. Por ejemplo, el contenido de `/libs` puede superponerse por el contenido de `/apps`, que luego se puede superponer por el contenido de `/conf`. Además, el contenido de una carpeta global debajo de `/conf` puede ser superpuesto por un &quot;inquilino&quot; o &quot;sitio&quot; específico (p. ej. `/conf/we-retail/settings`).

Normalmente, la Configuración según el contexto se utiliza como estrategia para ampliar las configuraciones de funciones, pero hay casos en los que otros tipos de contenido la utilizan.

La siguiente tabla incluye una columna adicional denominada &quot;Tipo de configuración&quot; para explicar en qué medida se puede superponer una configuración. A continuación se proporciona información adicional sobre estos tipos de configuración:

**no según el contexto**

* Los recursos se encuentran en estructuras de carpetas según el contexto (por ejemplo, `/libs/settings`) pero siempre se hace referencia a ellos a través de una ruta absoluta, por lo que no existe conciencia del contexto.
* Los recursos podrían estar en cualquier parte. Por ejemplo, las licencias DRM de Assets podrían estar en `/content/my-customer/licenses/creative-commons.html`
* Ejemplos:

   * Secuencias de comandos de flujo de trabajo -> `/apps/settings/workflow/scripts/noop.ecma`
   * Licencias DRM de recursos -> `/apps/settings/dam/drm/my-license`

**solo global**

* Función con solo configuración global
* Como punto de referencia, tenga prioridad sobre la configuración en este ejemplo: `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global`

* AEM solo admite la configuración global y no las configuraciones personalizadas por el usuario
* AEM siempre empezará a buscar primero configuraciones en el nivel /conf/global

* Ejemplos:

   * Lanzadores de flujo de trabajo -> `/libs/settings/workflow/launcher`
   * Modelos de flujo de trabajo -> `/conf/global/settings/workflow/models`

**inquilino-aware**

* Para las configuraciones con reconocimiento de usuarios, consulte este ejemplo para ver la prioridad de las rutas de configuración: `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global` &lt; `/conf/we-retail`, donde we-Retail es el nombre del inquilino. Las configuraciones con reconocimiento de inquilinos también admiten subinquilinos.

* AEM admite configuraciones tenanciadas. Respeta `cq:conf` la propiedad en la jerarquía
* Ejemplos:

   * Plantillas editables -> `/conf/we-retail/settings/wcm/templates`
   * Configuración de nube -> `/conf/we-retail/settings/cloudsettings`

<table>
 <tbody>
  <tr>
   <td><strong>Solución</strong></td>
   <td><strong>Ubicación anterior</strong><br /> </td>
   <td><strong>Nueva ubicación</strong></td>
   <td><strong>Tipo de configuración según el contexto</strong><br /> </td>
   <td><strong>Enfoque de compatibilidad con versiones anteriores</strong></td>
   <td><strong>Requisitos para alinear con el modelo más reciente</strong></td>
  </tr>
  <tr>
   <td>AEM Sites/AEM Forms</td>
   <td><p><code>/etc/cloudservices/typekit</code></p> <p><code>/etc/cloudservices/recaptcha</code></p> <p><code>/etc/cloudservices/echosign</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/typekit</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/recaptcha</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/echosign</code></p> </td>
   <td>inquilino-aware</td>
   <td><p>Servicios heredados de nubes.</p> <p>Se mantuvo en una actualización in situ. Código para enumerarlos y leerlos aún presentes en AEM como alternativa.</p> </td>
   <td>La interfaz de usuario de migración de formularios puede activar la utilidad de migración de contenido diferido para convertir automáticamente a la nueva ruta.<br /> </td>
  </tr>
  <tr>
   <td>Formularios AEM</td>
   <td><code>/etc/cloudservices/fdm</code></td>
   <td><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/fdm</code></td>
   <td>inquilino-aware</td>
   <td><p>Servicios heredados de nubes.</p> <p>Se ha mantenido una configuración actualizada in situ. Código para enumerarlos y leerlos aún presentes en AEM como alternativa.</p> </td>
   <td>La interfaz de usuario de migración de formularios puede activar la utilidad de migración de contenido diferido para convertir automáticamente a la nueva ruta.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/adhocassetshare</code></td>
   <td><code>/libs/settings/dam/adhocassetshare</code></td>
   <td>inquilino-aware</td>
   <td>Las estructuras de contenido heredadas se respetan con una prioridad mayor que las nuevas, OTB.</td>
   <td>Las personalizaciones de nivel de proyecto deben cortarse y pegarse en las rutas equivalentes <code>/apps</code> o <code>/conf</code> según corresponda.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
   <td><code>/libs/settings/dam/workflow</code></td>
   <td>inquilino-aware</td>
   <td>Las estructuras de contenido heredadas se respetan con una prioridad mayor que las nuevas, OTB.</td>
   <td>Las personalizaciones de nivel de proyecto deben cortarse y pegarse en las rutas equivalentes <code>/apps</code> o <code>/conf</code> según corresponda.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/drm/licenses/</code></td>
   <td><code>/libs/settings/dam/drm</code></td>
   <td>no según el contexto</td>
   <td>Las estructuras de contenido heredadas se respetan con una prioridad mayor que las nuevas, OTB.</td>
   <td>Las personalizaciones de nivel de proyecto deben cortarse y pegarse en las rutas equivalentes <code>/apps</code> o <code>/conf</code> según corresponda.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/indesign/scripts</code></td>
   <td><code>/libs/settings/dam/indesign</code></td>
   <td>inquilino-aware</td>
   <td>Las estructuras de contenido heredadas se respetan con una prioridad mayor que las nuevas, OTB.</td>
   <td><p>Las personalizaciones de nivel de proyecto deben cortarse y pegarse en las rutas equivalentes <code>/apps</code> o <code>/conf</code> según corresponda.</p> <p>Al ejecutar el flujo de trabajo de inserción de recursos personalizado, las referencias a la ubicación antigua en /etc seguirían existiendo en la configuración del proceso de extracción de medios. Junto con mover los scripts de /etc a las rutas /apps y /conf equivalentes, los argumentos personalizados del proceso de extracción de medios deben cambiarse de rutas absolutas a relativas para adaptarse a los cambios.</p> <p>Para obtener más información, consulte <a href="https://helpx.adobe.com/experience-manager/6-2/help/assets/indesign.html">esta página</a>.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video</code></td>
   <td><code>/libs/settings/dam/video</code></td>
   <td>inquilino-aware</td>
   <td>Las estructuras de contenido heredadas se respetan con una prioridad mayor que las nuevas, ya que están listas para usarse.</td>
   <td>Las personalizaciones de nivel de proyecto deben cortarse y pegarse en las rutas equivalentes <code>/apps</code> o <code>/conf</code> según corresponda.</td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/notification/email/default</code></td>
   <td><code>/libs/settings/dam/notification</code></td>
   <td>inquilino-aware</td>
   <td>Las estructuras de contenido heredadas se respetan con una prioridad mayor que las nuevas, ya que están listas para usarse.</td>
   <td>Las personalizaciones de nivel de proyecto deben cortarse y pegarse en las rutas equivalentes <code>/apps</code> o <code>/conf</code> según corresponda.</td>
  </tr>
  <tr>
   <td>AEM Sites/Recursos AEM</td>
   <td><code>/etc/designs</code> </td>
   <td><code>/libs/settings/wcm/designs</code></td>
   <td>no según el contexto</td>
   <td><p>Los servicios de consumo conocen la ubicación antigua.</p> <p>Se consideran las configuraciones de la ubicación heredada</p> </td>
   <td><br /> Mueva el contenido personalizado de <code>/etc/design</code> a <code>/apps/settings/wcm/design</code> para alinearlo con la nueva estructura del repositorio. En el futuro, considere la posibilidad de actualizar sus sitios para utilizar la funcionalidad de plantillas editables, que reemplaza la necesidad del modo de diseño y, por lo tanto, este contenido.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/scaffolding</code></td>
   <td><p><code>/libs/settings/wcm/template-types/scaffolding/scaffolding</code></p> <p><code>/apps/settings/wcm/template-types/scaffolding/scaffolding</code></p> </td>
   <td>no según el contexto</td>
   <td>Los componentes de la ubicación anterior en <code>/etc/scaffolding</code> continuarán funcionando, pero ya no se utilizan.</td>
   <td>Adobe recomienda utilizar los nuevos componentes del scaffold en la nueva ubicación.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/blueprints</code></td>
   <td><p>/libs/msm para las configuraciones de modelo de comercio y pantallas integradas</p> <p> </p> </td>
   <td>no según el contexto</td>
   <td><p>Consuming Services conoce la ubicación antigua.</p> <p>Se tienen en cuenta las configuraciones de la ubicación heredada.</p> </td>
   <td>Las configuraciones deben copiarse en las nuevas ubicaciones.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/mobile</code></td>
   <td><code>/libs/settings/mobile</code></td>
   <td>inquilino-aware</td>
   <td>La función aprovecha Configuration Manager y sigue admitiendo la ubicación antigua como alternativa.</td>
   <td>
    <ol>
     <li>Reubicar las configuraciones de <code>/etc</code> a <code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li>A continuación, actualice la referencia en el contenido como se indica a continuación:</li>
    </ol> <p><code>/content/&lt;tenant&gt;/jcr:content/cq:deviceGroups{String[]}=mobile/groups/responsive</code></p> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/msm/rolloutConfigs</code></td>
   <td><code>/libs/msm/wcm/rolloutconfigs</code></td>
   <td>N/D</td>
   <td><p>Los servicios de consumo conocen la ubicación antigua.</p> <p>Si las configuraciones se detectan en la ubicación heredada, se utilizarán.</p> </td>
   <td>Para alinearse con el nuevo modelo, las configuraciones deben crearse en las nuevas ubicaciones y las antiguas en <code>/etc</code> deben eliminarse.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/segmentation/contexthub</code></td>
   <td><code>/conf/we-retail/settings/wcm/segments</code></td>
   <td>inquilino-aware</td>
   <td><p>Segmentos de la ubicación anterior:</p>
    <ul>
     <li>Permanezca en modo de solo lectura en la consola de audiencias.</li>
     <li>Se sigue cargando en la página (si la ruta dada está seleccionada en Propiedades de la <strong>página &gt; Personalización &gt; Ruta</strong>de segmentos).</li>
     <li>Se puede utilizar para dirigir el contenido.</li>
    </ul> </td>
   <td>Puede utilizar la herramienta <a href="/help/sites-deploying/upgrading-code-and-customizations.md#migrateconfigurations">de migración de</a> segmentos para migrar a la nueva ubicación.</td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/social/config/languageOpts</code></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
   <td>N/D</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/templates</code></td>
   <td><code>/libs/settings/community/templates</code></td>
   <td> </td>
   <td><p>El código conoce la ubicación de la plantilla antigua. Las plantillas existentes seguirán siendo remitidas y de lectura y escritura a partir de <code>/etc</code>.</p> <p><br /> Para las plantillas de correo electrónico, si el cliente ya tenía sus plantillas personalizadas en otra ruta configurando la ruta raíz <strong>de</strong> Plantillas en la configuración <strong>de respuesta de correo electrónico de comunidades de</strong> AEM, permanecería tal cual.</p> </td>
   <td><p>Una utilidad <a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration" target="_blank">de</a> migración puede alinearse con el modelo de plantillas de AEM Communities más reciente.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/badging</code></td>
   <td><p><strong>Reglas de distintivo:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Imágenes distintivas:</strong></p> <p>Las imágenes no incluidas en la ubicación antigua de <code>/etc/community/badging/images</code> se mueven a <code>/libs/community/badging/images </code> </p> <p> </p> <p>Las imágenes personalizadas se mueven a <code>/content/community/badging/images</code>.</p> <p> </p> </td>
   <td>inquilino-aware</td>
   <td><p>El código conoce las rutas de identificación antiguas.</p> <p><br /> Primero comprobará la existencia de rutas<br /> antiguas. Si no están presentes, utilizará las nuevas rutas.</p> </td>
   <td><p>La migración manual es necesaria para alinearse con el modelo más reciente. Siga los pasos a continuación para lograr esto:</p>
    <ol>
     <li>Creación de un bloque de contexto de sitio mediante el navegador de configuración en <strong>Herramientas</strong></li>
     <li>Ir a la raíz del sitio</li>
     <li>Establezca la <code>cq:conf</code> propiedad en la ruta de bucket donde desee almacenar todas las configuraciones. Lo mismo se puede establecer mediante el Asistente para edición <strong>del sitio: Establecer entrada</strong>de configuración de nube y, a continuación, guardar los cambios</li>
     <li>Mover las reglas de marcado y las reglas de puntuación relevantes desde <code>etc/community/*</code> al bloque de contexto del sitio creado en el paso anterior</li>
     <li>Ajuste las propiedades <code>badgingRules</code> y <code>scoringRules</code> de la raíz del sitio para que tengan referencias relativas a las nuevas ubicaciones de reglas. Por ejemplo, si <code>cq:conf</code> se establece en <code>/conf/we-retail</code>, el valor de <code>badgingRules</code> será <code>community/badging/rules</code> si las reglas se mueven a este nuevo bloque</li>
     <li>Del mismo modo, ajuste las referencias a las reglas de puntuación en un nodo de regla de marcado para que tenga una ruta relativa.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/cloudservices/facebookconnect</code></p> <p><code>/etc/cloudservices/twitterconnect</code></p> <p><code>/etc/cloudservices/pinterestconnect</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> </td>
   <td>inquilino-aware</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/scoring</code></td>
   <td><code>/libs/settings/community/scoring</code></td>
   <td> </td>
   <td><p>El código conoce las rutas de identificación antiguas.</p> <p><br /> Primero comprobará la existencia de rutas<br /> antiguas. Si no están presentes, utilizará las nuevas rutas.</p> </td>
   <td><p>Se requieren pasos de migración manual para alinearse con el modelo más reciente.</p> <p>Los pasos son los mismos en las reglas de identificación anteriores.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/notifications</code></td>
   <td><code>/libs/settings/community/notifications</code></td>
   <td>no según el contexto</td>
   <td><p>Estas configuraciones no son compatibles con versiones anteriores. Consulte la columna "Requisitos para alinearse con el modelo más reciente" para ver los pasos sobre cómo migrar a las nuevas ubicaciones.<br /> </p> <br /> </td>
   <td><p>Se requiere una migración manual para alinear con el modelo más reciente. Puede utilizar Granite Configuration Manager para mover las configuraciones a la nueva ruta en <code>/apps/settings</code>.</p> <p>Por lo tanto, debe establecer la <code>mergeList</code> propiedad en true en el <code>/libs/settings/community/subscriptions</code> nodo y luego agregar un nodo <code>nt:unstructured</code> secundario.<br /> </p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/subscriptions</code></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
   <td>no según el contexto</td>
   <td>Estas configuraciones no son compatibles con versiones anteriores. Consulte la columna "Requisitos para alinearse con el modelo más reciente" para ver los pasos sobre cómo migrar a las nuevas ubicaciones.</td>
   <td><p>Se requiere una migración manual para alinear con el modelo más reciente. Puede utilizar Granite Configuration Manager para mover las configuraciones a la nueva ruta en <code>/apps/settings</code>.</p> <p>Por lo tanto, debe establecer la <code>mergeList</code> propiedad en true en el <code>/libs/settings/community/subscriptions</code> nodo y luego agregar un nodo <code>nt:unstructured</code> secundario.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/socialconfig/srpc/defaultconfiguration</code></td>
   <td><code>/conf/global/settings/community/srpc/defaultconfiguration</code></td>
   <td>global</td>
   <td>Estas configuraciones son compatibles con versiones anteriores. Si se detectan las rutas antiguas, se utilizarán. De lo contrario, las nuevas rutas tendrán prioridad.</td>
   <td><p>La tarea de migración de contenido diferido está disponible en forma de <code>CQ64CommunitiesConfigsCleanupTask</code>.</p> <p>Para obtener más información, consulte la documentación <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Migración</a>diferida.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/watchwords</code></td>
   <td><code>/libs/community/watchwords</code></td>
   <td>N/D</td>
   <td>Estas configuraciones son compatibles con versiones anteriores. Si se detectan las rutas antiguas, se utilizarán. De lo contrario, las nuevas rutas tendrán prioridad.</td>
   <td><p>La tarea de migración de contenido diferido está disponible en forma de <code>CQ64CommunitiesConfigsCleanupTask</code>.</p> <p>Las palabras de observación deberán moverse manualmente de <code>/etc/watchwords</code> a <code>/conf/global/settings/community/watchwords</code>.</p> </td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code> </p> <p><code>/var/workflow/models</code></p> </td>
   <td>global</td>
   <td><p>La ubicación heredada se utiliza si está presente y no existe ninguna configuración en <code>/libs</code> o <code>/conf</code>.</p> <p>Al editar modelos de flujo de trabajo de OOTB, se deben crear superposiciones según el contexto <code>/conf</code> para que puedan modificarse.</p> <p>La exportación de paquetes debe incluir el modelo en <code>/libs</code> o <code>/conf</code> y el modelo de tiempo de ejecución en <code>/var/workflow/models.</code></p> </td>
   <td><p>Los modelos recién creados se crearán en la <code>/conf/global/settings</code> ubicación.</p> <p>Cualquier edición en <code>/etc</code> o <code>/libs</code> requiere que cree explícitamente una anulación en <code>/conf/global/settings</code> antes de poder realizar la edición. El botón Editar tiene que estar seleccionado y hará que se cree y se permita la edición de la anulación en <code>/conf</code> el.</p> </td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/workflow/launcher</code></td>
   <td><p><code>/libs/settings/workflow/launcher</code></p> <p><code>/conf/global/settings/workflow/launcher</code></p> </td>
   <td>global</td>
   <td>La ubicación heredada se utiliza si está presente y no existe ninguna configuración<br /> en <code>/libs</code> o <code>/conf</code> ubicaciones. De este modo, se conservan los lanzadores personalizados.</td>
   <td><p>Las configuraciones del iniciador recién creadas o editadas se encuentran en la <code>/conf</code> ubicación.</p> <p>Todos los lanzadores deben moverse de la ubicación heredada <code>/etc</code> a<code> /conf/global/settings/workflow/launcher.</code></p> </td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> </td>
   <td>global</td>
   <td>La ubicación heredada se utiliza si está presente y no existe ninguna configuración<br /> en <code>/libs</code> o <code>/conf</code> ubicaciones. De este modo, se conservan los modelos de flujo de trabajo personalizados.</td>
   <td><p>Todos los modelos de flujo de trabajo deben moverse de la <code>/etc</code> ubicación heredada a <code>/conf/global/settings/workflow/models</code>.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/workflow/notification</code></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
   <td>no según el contexto</td>
   <td><p>Para la compatibilidad con versiones anteriores, se utiliza la ubicación heredada si está presente.</p> <p>Anteriormente, las plantillas de fuera de la caja tenían que anularse editándolas en <code>/etc</code>. Ahora, la anulación debe almacenarse en <code>/conf/global</code>.</p> </td>
   <td>Para obtener más información, consulte la documentación de Flujo de trabajo.<br /> </td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/cloudservices/translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> <p> </p> </td>
   <td>inquilino-aware</td>
   <td>Servicios heredados de nubes. Se mantendrá en una configuración actualizada in-situ. El código para enumerarlos y leerlos aún está presente en el producto como alternativa.</td>
   <td><p>Para mover configuraciones de nube a <code>/conf</code>, puede:</p>
    <ul>
     <li>Cree configuraciones con la nueva IU<br /> táctil o<br /> </li>
     <li>Copie las configuraciones de <code>/etc/cloudservices/translation</code> a sus respectivas nuevas ubicaciones</li>
    </ul> <p>Una vez hecho esto, las configuraciones deben asociarse con Sitios a través de <strong>Sitios &gt; Propiedades</strong> en la interfaz de usuario.</p> <p><em>Nota: Para que esto funcione, los conectores de traducción deben ser compatibles con AEM 6.5.</em></p> </td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/cloudservices/msft-translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/msft-translation</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/msft-translation</code></p> </td>
   <td>inquilino-aware</td>
   <td>Servicios heredados de nubes. Se mantendrá en una configuración actualizada in-situ. El código para enumerarlos y leerlos aún está presente en el producto como alternativa.</td>
   <td><p>Para mover configuraciones de nube a <code>/conf</code>, puede:</p>
    <ul>
     <li>Cree configuraciones con la nueva IU táctil o<br /> </li>
     <li>Copiar configuraciones antiguas de <code>/etc/cloudservices/translation</code> a sus respectivas ubicaciones nuevas</li>
    </ul> <p>Una vez hecho esto, las configuraciones deben asociarse con Sitios a través de <strong>Sitios &gt; Propiedades</strong> en la interfaz de usuario.</p> </td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/cloudsettings</code></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
   <td>inquilino-aware</td>
   <td><p>Las entradas existentes en <code>/etc</code> curso siguen vigentes al actualizar la instancia.</p> <p>El acceso a la interfaz de usuario de configuración de nube después de la actualización se copiará sobre la configuración de nube existente en la nueva estructura de repositorio, conservando el contenido existente para lograr compatibilidad con versiones anteriores.</p> </td>
   <td><p>Los modelos de contenido son los mismos, solo se ha cambiado la ubicación para alinearla con las configuraciones según el contexto.</p> <p>La tarea <a href="/help/sites-deploying/lazy-content-migration.md">Migración</a> diferida que abarca esta configuración de nube realizará las siguientes acciones:</p>
    <ul>
     <li>Copiar la configuración de nube existente en <code>/etc/cloudsettings</code> a <code>/conf/global/settings/cloudsettings</code></li>
     <li>Eliminar todos los elementos secundarios de <code>/etc/cloudsettings</code></li>
    </ul> <p>Sin embargo, se requieren pasos manuales después de la actualización y antes de ejecutar las tareas de migración diferida:</p>
    <ul>
     <li>Todas las referencias que apuntan a <code>/etc/cloudsettings/*</code> deben actualizarse para que apunten a <code>/conf/global</code></li>
    </ul> <p>Advertencia:</p>
    <ul>
     <li>Es necesario conservar el <code>/etc/cloudsettings</code> contenedor</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
   <td>solo global</td>
   <td><p>Configuración de nube para Dynamic Media: la configuración de Scene7 (<code>dynamicmedia_scene7</code> modo de ejecución) permanecerá en la misma ubicación. El proceso funciona tal cual. Si necesita ajustar el valor de configuración de la nube, entonces hay dos opciones para hacerlo:</p>
    <ol>
     <li>Actualice una configuración existente mediante la IU de configuración de nube antigua.</li>
     <li>Cree una nueva configuración de nube mediante la nueva IU táctil. Esto tendrá mayor prioridad que la anterior.</li>
    </ol> </td>
   <td><p>Para alinearse con el modelo más reciente, debe ejecutar la secuencia de comandos ubicada en:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/viewer</code></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
   <td>solo global</td>
   <td><p>Los ajustes preestablecidos de visor OOTB solo estarán disponibles en la nueva ubicación, mientras que el ajuste preestablecido de visor personalizado seguirá estando en funcionamiento <code>/etc</code> hasta que se produzca una modificación.</p> <p>Una vez que se haya modificado, se guardará en la nueva ubicación mediante la migración diferida. El servidor de imágenes incrustado observará tanto la ruta heredada como la nueva ruta al recibir una solicitud. Por lo tanto, no es necesario cambiar el código incrustado o la dirección URL.</p> </td>
   <td><p>El ajuste preestablecido de visor de fuera de la caja solo estará disponible en la nueva ubicación. Para el ajuste preestablecido de visor personalizado, debe ejecutar la secuencia de comandos de migración en esta ubicación:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p>Al igual que en el caso de compatibilidad con versiones anteriores, no es necesario ajustar el código copyURL/embed para que señale <code>/conf</code>. La solicitud existente de <code>/etc</code> se redirigirá debajo del capó al contenido correcto desde <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/imageserver/macros</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
   <td>solo global</td>
   <td>La macro debajo <code>/etc</code> sigue siendo válida. Si lo modifica, el nodo modificado se moverá a la nueva ubicación en <code>/conf</code> mediante una tarea de migración diferida.</td>
   <td><p>Debe ejecutar la secuencia de comandos de migración en esta ubicación:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia/Adaptive Video Encoding</code></td>
   <td><code>/libs/settings/dam/dm/presets/video/jcr:content/Adaptive Video Encoding</code></td>
   <td>N/D</td>
   <td><p>El perfil de vídeo predeterminado se eliminará sin actualizar la propiedad de carpetas de recursos para vincular al perfil.</p> <p>El proceso de codificación tiene una traducción integrada entre la ubicación antigua y la nueva. Convierte la ruta antigua para buscar en la nueva ruta de perfil.</p> </td>
   <td>No se requieren cambios.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
   <td>solo global</td>
   <td><p>El perfil de vídeo personalizado se mantendrá tal cual hasta que lo modifique.</p> <p>A continuación, se moverá a la nueva ubicación mediante una tarea de migración diferida. Esto es similar al ajuste preestablecido de vídeo incorporado en la búsqueda de codificación. El proceso de codificación tiene un traductor de rutas integrado para buscar primero en la ubicación antigua y, a continuación, en la nueva ubicación del perfil de vídeo.</p> </td>
   <td><p>Para alinearse con el modelo más reciente, puede ejecutar la secuencia de comandos de migración en:</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
   <td>solo global</td>
   <td><p>Esta configuración de nube para la configuración híbrida de Dynamic Media (<code>dynamicmedia</code> modo de ejecución) permanecerá en la misma ubicación. El proceso funciona tal cual. Si necesita ajustar el valor de configuración, puede hacerlo de dos maneras.</p>
    <ol>
     <li>Actualice una configuración existente mediante la IU de configuración de nube antigua.</li>
     <li>Cree una nueva configuración de nube mediante la nueva IU táctil. Esto tendrá mayor prioridad que la anterior.</li>
    </ol> </td>
   <td><p>Debe ejecutar la secuencia de comandos de migración para alinearla con el modelo más reciente. Puede encontrar la secuencia de comandos en esta ubicación:<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/youtube</code></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
   <td>solo global</td>
   <td><p>La configuración de nube para la configuración de DM-Youtube permanecerá en la misma ubicación. El proceso funciona tal cual. Si necesita ajustar el valor de configuración de nube, puede hacerlo de dos maneras:</p>
    <ol>
     <li>Actualice una configuración existente a través de la IU de configuración de nube antigua.</li>
     <li>Cree una nueva configuración de nube mediante la nueva IU táctil. Esto tendrá mayor prioridad que la anterior.</li>
    </ol> </td>
   <td><p>Puede ejecutar una secuencia de comandos de migración para alinearla con el modelo más reciente. La secuencia de comandos se encuentra en esta ubicación:<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/analytics</code></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
   <td>solo global</td>
   <td>No se requiere ninguna acción.</td>
   <td><p>Puede ejecutar una secuencia de comandos de migración para alinearla con el modo más reciente. La secuencia de comandos se encuentra en esta ubicación:<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><p><code>/etc/notification/email/default/com.day.cq.replication</code></p> <p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
   <td><code>/libs/settings/notification-templates</code></td>
   <td>solo global</td>
   <td>Las plantillas de <code>/etc/notification/email/default/</code> tienen prioridad sobre las de <code>/libs/settings/notification-templates</code>.</td>
   <td>Para alinear con el modelo más reciente, puede crear nuevas plantillas debajo <code>/apps/settings/notification-templates</code> y realizar nuevas modificaciones en ellas.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/msm/rolloutconfigs/launch</code></p> <p><code>/etc/msm/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td><p><code>/libs/msm/launches/rolloutconfigs/launch</code></p> <p><code>/libs/msm/launches/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td>N/D</td>
   <td><p>Consuming Services conoce la ubicación antigua.</p> <p>Si las configuraciones se detectan en la ubicación heredada, se utilizarán.</p> </td>
   <td>Para alinearse con el nuevo modelo, las configuraciones deben crearse en las nuevas ubicaciones y las antiguas en <code>/etc</code> deben eliminarse.</td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/translation/supportedLanguages</code></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
   <td>no según el contexto</td>
   <td>Una advertencia es que los idiomas personalizados deben agregarse a la lista.<br /> </td>
   <td>Superponga y actualice la nueva lista con idiomas adicionales (si los hay). También funcionaría copiar la lista antigua en la <code>/apps</code> ubicación.</td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
   <td>solo global</td>
   <td>Se conservará en una configuración mejorada in-situ. Código para enumerarlos y leerlos aún presentes en el producto.</td>
   <td>Para conservar los cambios, copie el archivo XML de <code>/etc</code> a <code>/libs</code> o <code>/conf</code>. Como alternativa,<strong> </strong>elimine el archivo de <code>/etc</code>.</td>
  </tr>
 </tbody>
</table>

## Bibliotecas del cliente {#client-side-libraries}

[Las bibliotecas](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/clientlibs.html) del lado del cliente son código JavaScript y CSS procesado en el explorador.

### Estrategia de extensibilidad {#extensibility-strategy-1}

AEM proporciona un marco de extensibilidad para anexar varios archivos JavaScript. Se anexará cualquier archivo con la misma propiedad &quot;categorías&quot;, lo que permitirá que el código personalizado amplíe el código AEM que reside en `/libs`.

<table>
 <tbody>
  <tr>
   <td><strong>Solución</strong></td>
   <td><strong>Ubicación anterior</strong><br /> </td>
   <td><strong>Nueva ubicación</strong></td>
   <td><strong>Enfoque de compatibilidad con versiones anteriores</strong></td>
   <td><strong>Requisitos para alinear con el modelo más reciente</strong></td>
  </tr>
  <tr>
   <td>Formularios AEM</td>
   <td><code>/etc/clientlibs/fd/fp</code></td>
   <td><code>/libs/fd/fp/components</code></td>
   <td><p>clientlib heredada que se mantendrá en una instancia que se haya actualizado mediante una actualización in situ.</p> <p>Los nuevos clientes tienen los mismos nombres de categoría junto con la propiedad "<strong><code>replaces</code></strong>" para evitar la combinación de clientes antiguos y nuevos.</p> </td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>Formularios AEM</td>
   <td><code>/etc/clientlibs/fd/rte</code></td>
   <td><code>/libs/fd/rte</code></td>
   <td><p>Clientes preexistentes que se conservarán en una instancia que se haya actualizado mediante una actualización in situ.</p> <p>Los nuevos clientes tienen los mismos nombres de categoría junto con la propiedad "<strong><code>replaces</code></strong>" para evitar la combinación de clientes antiguos y nuevos.</p> </td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>Formularios AEM</td>
   <td><code>/etc/clientlibs/fd/af</code></td>
   <td><code>/libs/fd/af/authoring/clientlibs</code></td>
   <td>Clientes heredados. Se mantendrá en una instancia que se haya actualizado mediante una actualización in situ. Los nuevos clientes tienen los mismos nombres de categoría junto con la propiedad "<strong><code>replaces</code></strong>" para evitar la combinación de clientes antiguos y nuevos.</td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>Formularios AEM</td>
   <td><code>/etc/clientlibs/fd/themes/themeLibrary</code></td>
   <td>Esto ya no se incluye en el paquete AEM 6.5 incorporado.</td>
   <td><p>Temas predeterminados en formularios adaptables.</p> <p>Se conservará en una configuración mejorada in-situ.</p> </td>
   <td>Se trata en parte de contenido generado por el usuario. Esto se enviará como un paquete de contenido de referencia con el <code>aem-forms-reference-themes</code> nombre.</td>
  </tr>
  <tr>
   <td>Formularios AEM</td>
   <td><code>/etc/clientlibs/fd/expeditor</code></td>
   <td><code>/libs/fd/expeditor/clientlibs</code></td>
   <td>Clientes heredados. Se mantendrá en una instancia que se haya actualizado mediante una actualización in situ. Los nuevos clientes tienen los mismos nombres de categoría junto con la propiedad "<strong><code>replaces</code></strong>" para evitar la combinación de clientes antiguos y nuevos.</td>
   <td>No se requiere ninguna acción.<p> </p> </td>
  </tr>
  <tr>
   <td>Formularios AEM</td>
   <td><code>/etc/clientlibs/fd/fmaddon</code></td>
   <td><code>/libs/fd/fmaddon</code></td>
   <td>Clientes heredados de Analytics y Target que no están destinados a ser consumidos directamente. </td>
   <td>Se limpió después de la actualización mediante un filtro de limpieza.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
   <td><code>/libs/dam/clientlibs</code></td>
   <td>Los clientes preexistentes tienen nombres de categoría de cliente diferentes.</td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td> </td>
   <td><code>/etc/clientlibs/ckeditor</code></td>
   <td><code>/libs/clientlibs/ckeditor</code></td>
   <td>Son clientes heredados. Se mantendrán en una configuración mejorada in situ. Los clientes nuevos tienen los mismos nombres de categoría y la propiedad "<code>replaces</code>" para evitar la combinación de clientes nuevos y antiguos.</td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/sitecatalyst</code></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
   <td><p>Son clientes heredados. Se conservará en una configuración mejorada in-situ.</p> <p>Los clientes nuevos tienen los mismos nombres de categoría.</p> </td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/personalization</code></td>
   <td><code>/libs/cq/personalization/clientlibs/personalization</code></td>
   <td><p>Son clientes heredados. Se conservará en una configuración mejorada in-situ.</p> <p>Los clientes nuevos tienen los mismos nombres de categoría.</p> </td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/searchpromote</code></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
   <td><p>Son clientes heredados. Se conservará en una configuración mejorada in-situ.</p> <p>Los clientes nuevos tienen los mismos nombres de categoría</p> </td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/target</code></td>
   <td><code>/libs/cq/target/clientlibs/target</code></td>
   <td><p>Son clientes heredados. Se conservará en una configuración mejorada in-situ.</p> <p>Los clientes nuevos tienen los mismos nombres de categoría.</p> </td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/address</code></td>
   <td><code>/libs/cq/address/clientlibs</code></td>
   <td>Los clientes nuevos tienen los mismos nombres de categoría.</td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation</code></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
   <td>Clientes heredados. Se conservará en una configuración mejorada in-situ. Los nuevos clientes tienen los mismos nombres de categoría junto con la propiedad "<strong>reemplaza</strong>" para evitar la combinación de clientes nuevos y antiguos.</td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
   <td><p><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></p> </td>
   <td><p>En una actualización in-situ, el archivo heredado (/etc/clientlibs/wcm/..._) permanecerá y no se eliminará automáticamente, por lo que las referencias al archivo heredado /etc/clientlibs/wcm/foundation/grid/grid_base.less se seguirán almacenando en el lugar.</p> <p><em>Tenga en cuenta que es un caso aparte en el que este archivo LESS se hace referencia por ruta absoluta a través de sentencias LESS @import y NO por categoría clientlib.</em></p> <p>Si el cliente LESS que hace referencia a "grid_base.less" apunta a un archivo no existente, se interrumpirá el modo Diseño de plantilla editable y no habrá ningún ajuste realizado con él (por ejemplo: todos los componentes tendrán el ancho completo de la página).</p> </td>
   <td>Actualice las referencias en el código personalizado (es decir, en cualquier archivo LESS que haga referencia al archivo grid_base.less movido) para que apunten a la nueva ubicación y elimine la ubicación heredada.</td>
  </tr>
 </tbody>
</table>

Estas son otras reestructuraciones que no caen dentro de las secciones anteriores.

### Estrategia de extensibilidad {#extensibility-strategy-2}

Consulte cada fila de tabla para ver cualquier modelo de extensibilidad admitido. El contenido de esta sección no suele ampliarse.

## Varios {#miscellaneous}

<table>
 <tbody>
  <tr>
   <td><strong>Solución</strong></td>
   <td><strong>Ubicación anterior</strong><br /> </td>
   <td><strong>Nueva ubicación</strong></td>
   <td><strong>Enfoque de compatibilidad con versiones anteriores</strong></td>
   <td><strong>Requisitos para alinear con el modelo más reciente</strong></td>
  </tr>
  <tr>
   <td>Formularios AEM</td>
   <td><code>/etc/designs/fd/fp</code></td>
   <td><code>/libs/fd/fp</code></td>
   <td><p>Plantillas OTB heredadas de AEM Forms Portal. Estas plantillas permanecerán en /etc después de una configuración actualizada in-situ.</p> <p>En el listado de plantillas, la palabra<em> "desaprobada</em>" se agregará al título de la plantilla para diferenciarlas de las plantillas más nuevas.</p> </td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>Formularios AEM</td>
   <td><code>/etc/aep</code></td>
   <td><code>/var/fd/content/annotations</code></td>
   <td>Archivos de anotación de la gestión de correspondencia heredada. No está destinado a ser consumido directamente. Se limpiará después de la actualización mediante un filtro de limpieza.</td>
   <td>Ubicación heredada borrada después de la actualización mediante un filtro de limpieza.</td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/tags</code></td>
   <td><code>/content/cq:tags</code></td>
   <td>La API del Administrador de etiquetas admite tanto la ubicación heredada como la nueva. Cuando se inicia el componente OSGi de fábrica del Administrador de etiquetas JCR, detecta si se está ejecutando en una instancia actualizada o heredada y utiliza la ubicación adecuada.<br /> </td>
   <td><p>Para alinearse correctamente con el nuevo modelo:</p>
    <ol>
     <li>Reemplace las referencias al modelo antiguo (<code>/etc/tags</code>) por el nuevo (<code>/content/cq:tags</code>) utilizando la variable <code>tagID.</code></li>
     <li>Iniciar sesión en CRXDE Lite</li>
     <li>Mover las etiquetas de <code>/etc/tags</code> a <code>/content/cq:tags</code></li>
     <li>Reinicie el componente OSGi <code class="code">com.day.cq.tagging.impl.JcrTagManagerFactoryImpl.
        </code></li>
    </ol> <p> </p> </td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>Ubicación heredada utilizada en el procesamiento de los<br /> flujos de trabajo en vuelo. Los nuevos flujos de trabajo utilizan la nueva ubicación en <code>/var.</code></td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/workflow/scripts</code></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
   <td><p>Los pasos del modelo de flujo de trabajo existentes que hacen referencia a secuencias de comandos de flujo de trabajo en la ubicación heredada en <code>/etc/workflow/scripts</code> continuarán apuntando a estas secuencias de comandos después de la actualización y se ejecutarán correctamente.</p> <p>Tenga en cuenta la IU de AEM para crear los pasos del flujo de trabajo" (Proceso, Divisiones, etc.) ya no enumera las secuencias de comandos en <code>/etc/workflow/scripts</code> la lista desplegable que se utiliza para seleccionar las secuencias de comandos de flujo de trabajo.</p> </td>
   <td><p>Los flujos de trabajo que aprovechan estos scripts seguirán funcionando como se espera si el paso del proceso de flujo de trabajo asociado no se edita en AEM.</p> <p>Sin embargo, para una compatibilidad total con versiones anteriores, incluso cuando se editan los pasos, es necesario que el cliente realice una acción manual después de la actualización:</p>
    <ul>
     <li>Las secuencias de comandos se deben mover de <code>/etc/workflow/scripts</code> a <code>/apps/workflow/scripts.</code></li>
     <li>Cualquier<strong> </strong>referencia a <code>/etc/workflow/scripts</code> en los pasos del modelo de flujo de trabajo debe actualizarse para hacer referencia a la nueva <code>/apps/workflow/scripts</code> ubicación.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/replication/treeactivation</code></td>
   <td><code>/libs/replication/treeactivation</code></td>
   <td>La página de utilidad ClassicUI permanece en su lugar durante la actualización.</td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/jobs</code></td>
   <td><code>/var/dam/jobs</code></td>
   <td><p>Ubicación temporal para guardar archivos zip generados para invocar la acción de descarga de Recursos AEM.</p> <p>No es necesario actualizar porque cuando el cliente solicita descargar el recurso, generará el archivo en la nueva ubicación.</p> </td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/products</code></td>
   <td><code>/var/commerce/products</code></td>
   <td><p>El contenido antiguo permanece en su lugar y se puede utilizar después de la actualización.</p> <p>Se proporciona una tarea de migración diferida para la migración a la nueva ubicación.</p> </td>
   <td><p>La migración se realiza mediante una tarea de migración diferida: <code>CQ64CommerceMigrationTask.</code></p> <p>Realiza los siguientes pasos:</p>
    <ul>
     <li>Ajusta las referencias de la ubicación antigua para que apunten a la nueva ubicación</li>
     <li>Mueve el contenido de la ubicación antigua a la nueva ubicación</li>
     <li><p>Quita la ubicación antigua para activar finalmente el uso de la nueva ubicación en todo el sistema</p> </li>
    </ul> <p>Las ubicaciones cubiertas por la tarea son:</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collection<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/Shipping-methods<br /> </li>
    </ul> <p>Para catálogos más grandes, se recomienda ejecutar la tarea de migración de comercio individualmente pasando la siguiente propiedad del sistema Java a AEM:</p>
    <ul>
     <li>nombre de propiedad: <code>com.adobe.upgrade.forcemigration</code></li>
     <li>valor de propiedad: <code>com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></li>
    </ul> <p>Después de la migración, AEM requiere un reinicio.</p> </td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/orders</code></td>
   <td><code>/var/commerce/orders</code></td>
   <td><p>El contenido antiguo permanece en su lugar y se puede utilizar después de la actualización.</p> <p>Se proporciona una tarea de migración diferida para la migración a la nueva ubicación.</p> </td>
   <td>Consulte la descripción anterior para <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/collections</code></td>
   <td><code>/var/commerce/collections</code></td>
   <td><p>El contenido antiguo permanece en su lugar y se puede utilizar después de la actualización.</p> <p>Se proporciona una tarea de migración diferida para la migración a la nueva ubicación.</p> </td>
   <td>Consulte la descripción anterior para <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/classifications</code></td>
   <td><code>/var/commerce/classifications</code></td>
   <td>No se requiere ninguna acción.</td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/shipping-methods</code></td>
   <td><code>/var/commerce/shipping-methods</code></td>
   <td><p>El contenido antiguo permanece en su lugar y se puede utilizar después de la actualización.</p> <p>Se proporciona una tarea de migración diferida para la migración a la nueva ubicación.</p> </td>
   <td>Consulte la descripción anterior para <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/payment-methods</code></td>
   <td><code>/var/commerce/payment-methods</code></td>
   <td><p>El contenido antiguo permanece en su lugar y se puede utilizar después de la actualización.</p> <p>Se proporciona una tarea de migración diferida para la migración a la nueva ubicación.</p> </td>
   <td>Consulte la descripción anterior para <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/taskmanagement</code></td>
   <td><code>/var/taskmanagement</code></td>
   <td><p>Las nuevas tareas se crean en <code>/var/taskmanagement</code></p> <p>Las tareas existentes en la ubicación heredada seguirán estando visibles en la bandeja de entrada de AEM.</p> </td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/workflow/packages</code></td>
   <td><code>/var/workflow/packages</code></td>
   <td><p>Los paquetes de AEM creados a través del Administrador de paquetes de AEM aún se almacenan en <code>/etc/workflow/packages.</code></p> <p>Otros paquetes creados mediante Sitios y flujos de trabajo de AEM siguen almacenándose en<code>/var/workflow/packages.</code></p> <p>Los paquetes que se encuentran en <code>/etc/workflow/packages</code> y <code>/var/workflow/packages</code> pueden editarse a través del administrador de paquetes de AEM. </p> </td>
   <td><p>No se requiere ninguna acción.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>Las nuevas instancias de flujo de trabajo se crearán en <code>/var</code> forma automática.</td>
   <td>No se requiere ninguna acción.</td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/commerce/searchpromote</code></td>
   <td><code>/var/cq/searchpromote</code></td>
   <td><p>Nueva ubicación para el contenido de las fuentes de Search and Promote.</p> <p>La URL antigua sigue funcionando y una ServletFilter reenvía la solicitud a la nueva ubicación.</p> </td>
   <td><br /> No se requiere ninguna acción. <br /> </td>
  </tr>
  <tr>
   <td>Todos</td>
   <td><code>/etc/dtm-hook</code></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
   <td><p>Nueva ubicación para los enlaces web de la DTM.</p> <p>La URL antigua sigue funcionando y una ServletFilter reenvía la solicitud a la nueva ubicación.</p> </td>
   <td><br /> No se requiere ninguna acción. <br /> </td>
  </tr>
 </tbody>
</table>

