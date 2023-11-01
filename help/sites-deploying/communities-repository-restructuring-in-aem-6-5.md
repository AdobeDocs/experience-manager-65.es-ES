---
title: Reestructuración de repositorios para AEM Communities en 6.4
description: AEM Aprenda a realizar los cambios necesarios para migrar a la nueva estructura de repositorios en la versión 6.4 para comunidades de la versión de la versión de.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 4d2bdd45-a29a-4936-b8da-f7e011d81e83
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 3%

---

# Reestructuración de repositorios para AEM Communities en 6.5 {#repository-restructuring-for-aem-communities-in}

Como se describe en el elemento principal [AEM Reestructuración de repositorios en 6.4](/help/sites-deploying/repository-restructuring.md) AEM , los clientes que actualicen a la versión 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado con los cambios del repositorio que afectan a la solución de AEM Communities. AEM Algunos cambios requieren un esfuerzo durante el proceso de actualización de la versión 6.5 de la, mientras que otros se pueden aplazar hasta una actualización futura.

**Con actualización a 6.5**

* [Plantillas de notificación de correo electrónico](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [Configuraciones de suscripción](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**Antes de una actualización futura**

* [Configuraciones de distintivos](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [Diseños de consola de comunidades clásicos](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Configuraciones de inicio de sesión social de facebook](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [Configuraciones de opciones de idioma](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Configuraciones de inicio de sesión social de pinterest](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [Configuraciones de puntuación](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Twitter Configuraciones de inicio de sesión social](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [Varios](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## Con actualización a 6.5 {#with-upgrade}

### Plantillas de notificación de correo electrónico {#e-mail-notification-templates}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>La migración manual es necesaria si desea pasar a la nueva ruta en "<code>/apps/settings</code>". Puede utilizar el Administrador de configuración de Granite para realizar la migración.</p> <p>Puede realizar la migración estableciendo la propiedad <code>mergeList</code> hasta <code>true</code> en el "<code>/libs/settings/community/subscriptions</code>" y añada un <code>nt:unstructured</code> nodo secundario.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configuraciones de suscripción {#subscription-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>La migración manual es necesaria si desea pasar a la nueva ruta en "<code>/apps/settings</code>". Puede utilizar el Administrador de configuración de Granite para realizar la migración.</p> <p>Puede realizar la migración estableciendo la propiedad <code>mergeList</code> hasta <code>true</code> en el "<code>/libs/settings/community/subscriptions</code>" y añada un <code>nt:unstructured</code> nodo secundario.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configuraciones de Watchwords {#watchwords-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td>/etc/watchwords</td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td>Hay disponible una tarea Migración diferida para limpiar las Configuraciones de las comunidades.<br /> <p>La tarea mueve palabras observadas de <code>/etc/watchwords</code> hasta <code>/conf/global/settings/community/watchwords</code>.</p> <p>Si las palabras observadas personalizadas se almacenan en SCM, se deben implementar en <code>/apps/settings/...</code> y debe asegurarse de que no haya una superposición <code>/conf/global/settings/...</code> que tendrían prioridad.</p> <p>La tarea de migración elimina <code>/etc</code> ubicaciones.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

## Antes de una actualización futura {#prior-to-upgrade}

### Configuraciones de distintivos {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><strong>Reglas de distintivo:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Imágenes de distintivo:</strong></p> <p>Para imágenes predeterminadas: <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>Para imágenes personalizadas: <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Se requiere la migración manual.</p> <p>Si la instancia ha personalizado las reglas de distintivo/puntuación, no hay una forma automatizada de colocar todas las reglas debajo de un bloque. Necesita las entradas del cliente sobre el bloque conf (global o específico del sitio) que desea utilizar para su sitio.</p> <p>No hay ninguna interfaz de usuario disponible para configurar las insignias y la puntuación de un sitio.</p> <p>Para alinearse con la nueva estructura del repositorio:</p>
    <ol>
     <li>Cree un bloque de contexto de sitio con <strong>Explorador de configuración</strong> bajo <strong>Herramientas</strong></li>
     <li>Ir a la raíz del sitio</li>
     <li>Establecer <code>cq:confproperty</code> hasta la ruta del contenedor en la que desea almacenar todos los ajustes. Lo mismo se puede configurar a través del sitio <strong>Asistente de edición: Establecer entrada de configuración de nube</strong>.</li>
     <li>Mover las reglas de distintivo y de puntuación relevantes de <code>/etc/community/*</code> al bloque de contexto de sitio creado en el paso anterior.</li>
     <li>Ajuste las propiedades de las reglas de identificación y de las reglas de puntuación en la raíz del sitio para tener referencias relativas a las nuevas ubicaciones de reglas.
      <ol>
       <li>Por ejemplo, si la propiedad para <code>cq:conf = /conf/we-retail</code>, entonces <code>badgingRules [] = community/badging/rules</code> si las reglas se mueven ahora a este nuevo bloque.</li>
      </ol> </li>
     <li>Del mismo modo, ajuste las referencias a las reglas de puntuación en un nodo de regla de identificación para que tengan una ruta relativa.</li>
    </ol> <p> </p> <p>Finalmente, limpie eliminando el recurso <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Diseños de consola de comunidades clásicos {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/social/console</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code>/libs/settings/wcm/designs/social/console</code></p> <p><code>/apps/settings/wcm/designs/social/console</code></p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configuraciones de inicio de sesión social de facebook {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudservices/facebookconnect</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier nueva configuración de nube de Facebook debe migrarse a la nueva ubicación.</p>
    <ol>
     <li>Migre las configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ol>
       <li>Vuelva a crear manualmente las nuevas configuraciones de inicio de sesión social de Facebook AEM mediante la interfaz de usuario de creación de en <strong>Herramientas &gt; Cloud Service &gt; Configuración de inicio de sesión social de Facebook</strong>.<br /> o <br /> </li>
       <li>Copie cualquier configuración de nube de Facebook nueva de la ubicación anterior a la ubicación nueva correspondiente, en <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Actualice cualquier raíz del sitio de AEM Communities para hacer referencia a la nueva configuración de inicio de sesión social de Facebook estableciendo el <code>[cq:Page]/jcr:content@cq:conf</code> a la ruta absoluta en la Nueva ubicación.</li>
     <li>Desasocie el Cloud Service de Facebook Connect heredado de cualquier raíz del sitio de AEM Communities actualizada para hacer referencia a la nueva ubicación.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configuraciones de opciones de idioma {#language-options-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/social/config/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td>N/D<br /> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configuraciones de inicio de sesión social de pinterest {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudservices/pinterestconnect</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier nueva configuración de nube de Pinterest debe migrarse a la nueva ubicación.</p>
    <ol>
     <li>Migre las configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ol>
       <li>Vuelva a crear manualmente las nuevas configuraciones de inicio de sesión social de Pinterest AEM mediante la interfaz de usuario de creación de en <strong>Herramientas &gt; Cloud Service &gt; Configuración de inicio de sesión social de Pinterest</strong>.<br /> o</li>
       <li>Copie cualquier nueva configuración de nube de Pinterest de la ubicación anterior a la ubicación nueva correspondiente en <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Actualice cualquier raíz del sitio de AEM Communities para hacer referencia a la nueva configuración de inicio de sesión social de Pinterest mediante la configuración de <code>[cq:Page]/jcr:content@cq:conf</code> a la ruta absoluta en la Nueva ubicación.</li>
     <li>Desasocie el Cloud Service de Pinterest Connect heredado de cualquier raíz del sitio de AEM Communities actualizada para hacer referencia a la nueva ubicación.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configuraciones de puntuación {#scoring-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para alinearse con la nueva estructura del repositorio, las reglas de puntuación se pueden almacenar en <code>/apps/settings/</code> o /<code>conf/.../settings</code></p>
    <ol>
     <li>Para <code>/apps/settings</code>, esto actuaría como reglas globales o predeterminadas administradas en SCM.</li>
    </ol> <p>Creación de configuraciones según el contexto en <code>/conf/</code> mediante CRXDELite:</p>
    <ol>
     <li>Cree las configuraciones en el <code>/conf/.../settings</code> ubicación<br /> </li>
     <li>El sitio de comunidades debe tener <code>cq:conf </code>propiedad conjunto de propiedades.
      <ol>
       <li>Si no <code>cq:conf</code> , las reglas de puntuación se leerían directamente desde la ruta dada para la propiedad '<code>scoringRules</code>' en el nodo raíz del sitio, por ejemplo: <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>Limpieza: elimine el recurso <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Twitter Configuraciones de inicio de sesión social {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudservices/twitterconnect</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier nueva configuración de nube de Twitter debe migrarse a la nueva ubicación.</p>
    <ol>
     <li>Migre las configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ol>
       <li>Vuelva a crear manualmente las nuevas configuraciones de inicio de sesión social de Twitter AEM a través de la IU de creación de en <strong>Herramientas &gt; Cloud Service &gt; Configuración de inicio de sesión social de Twitter</strong>.<br /> o <br /> </li>
       <li>Copie cualquier nueva configuración de nube de Twitter de la ubicación anterior a la ubicación nueva correspondiente, en <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Actualice cualquier raíz del sitio de AEM Communities para hacer referencia a la nueva configuración de inicio de sesión social de Twitter estableciendo el <code>[cq:Page]/jcr:content@cq:conf</code> a la ruta absoluta en la Nueva ubicación.</li>
     <li>Desasocie el Cloud Service de Twitter Connect heredado de cualquier raíz del sitio de AEM Communities actualizada para hacer referencia a la nueva ubicación.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Varios {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Nueva ubicación(es)</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>El Adobe ha proporcionado una utilidad de migración en:</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Las plantillas personalizadas existentes pasarían a <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>
