---
title: Reestructuración de repositorios para AEM Communities en la versión 6.4
seo-title: Reestructuración de repositorios para AEM Communities en la versión 6.4
description: Aprenda a realizar los cambios necesarios para migrar a la nueva estructura de repositorios de AEM 6.4 para Communities.
seo-description: Aprenda a realizar los cambios necesarios para migrar a la nueva estructura de repositorios de AEM 6.4 para Communities.
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 3%

---


# Reestructuración de repositorios para AEM Communities en 6.5 {#repository-restructuring-for-aem-communities-in}

Como se describe en la página principal [Reestructuración del repositorio en AEM 6.4](/help/sites-deploying/repository-restructuring.md), los clientes que actualicen a AEM 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado con los cambios del repositorio que afectan a la solución de AEM Communities. Algunos cambios requieren un esfuerzo de trabajo durante el proceso de actualización de AEM 6.5, mientras que otros se pueden aplazar hasta una actualización futura.

**Con actualización a la versión 6.5**

* [Plantillas de notificación por correo electrónico](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [Configuraciones de suscripción](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**Antes de una actualización futura**

* [Configuraciones de distintivos](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [Diseños de la consola de Communities clásicos](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Configuraciones de inicio de sesión social de Facebook](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [Configuraciones de opciones de idioma](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Configuraciones de inicio de sesión de Pinterest Social](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [Configuraciones de puntuación](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Configuraciones de inicio de sesión social de Twitter](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [Misc](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## Con actualización de 6.5 {#with-upgrade}

### Plantillas de notificación de correo electrónico {#e-mail-notification-templates}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/libs/settings/community/notifications</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>La migración manual es necesaria si desea pasar a una nueva ruta en "<code>/apps/settings</code>". Puede utilizar el Administrador de configuración de Granite para realizar la migración.</p> <p>Puede realizar la migración estableciendo la propiedad <code>mergeList</code> en <code>true</code> en el nodo "<code>/libs/settings/community/subscriptions</code>" y agregando un nodo secundario <code>nt:unstructured</code>.</p> </td>
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>La migración manual es necesaria si desea pasar a una nueva ruta en "<code>/apps/settings</code>". Puede utilizar el Administrador de configuración de Granite para realizar la migración.</p> <p>Puede realizar la migración estableciendo la propiedad <code>mergeList</code> en <code>true</code> en el nodo "<code>/libs/settings/community/subscriptions</code>" y agregando un nodo secundario <code>nt:unstructured</code>.</p> </td>
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td>/libs/community/watchwords</td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td>Hay disponible una tarea de migración diferida para limpiar las configuraciones de Communities.<br /> <p>La tarea mueve las palabras clave de <code>/etc/watchwords</code> a <code>/conf/global/settings/community/watchwords</code>.</p> <p>Si las palabras clave personalizadas se almacenan en SCM, deben implementarse en <code>/apps/settings/...</code> y debe asegurarse de que no haya una configuración <code>/conf/global/settings/...</code> superpuesta que tenga prioridad.</p> <p>La tarea de migración elimina <code>/etc</code> ubicaciones.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

## Antes de la actualización futura {#prior-to-upgrade}

### Configuraciones de distintivo {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><strong>Reglas de distintivo:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Imágenes de distintivo:</strong></p> <p>Para imágenes predeterminadas: <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>Para imágenes personalizadas: <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Se requiere la migración manual.</p> <p>Si la instancia ha personalizado las reglas de distintivo/puntuación, no hay una forma automatizada de colocar todas las reglas en un bloque. Necesita entradas del cliente en el bloque conf (global o específico del sitio) que desee utilizar para su sitio.</p> <p>No hay IU disponible para configurar el distintivo y la puntuación de un sitio.</p> <p>Para alinearse con la nueva estructura del repositorio:</p>
    <ol>
     <li>Cree un bloque de contexto del sitio utilizando el <strong>Navegador de configuración</strong> en <strong>Herramientas</strong></li>
     <li>Vaya a la raíz del sitio</li>
     <li>Establezca <code>cq:confproperty</code> en la ruta del compartimento donde desea almacenar toda la configuración. Lo mismo se puede configurar a través del sitio <strong>Edit Wizard - Set cloud config input</strong>.</li>
     <li>Mueva las reglas de distintivo y las reglas de puntuación relevantes de <code>/etc/community/*</code> al bloque de contexto del sitio creado en el paso anterior.</li>
     <li>Ajuste las reglas de distintivo y las propiedades de reglas de puntuación en la raíz del sitio para tener referencias relativas a nuevas ubicaciones de reglas.
      <ol>
       <li>Por ejemplo, si la propiedad para <code>cq:conf = /conf/we-retail</code>, entonces <code>badgingRules [] = community/badging/rules</code> si las reglas ahora se mueven a este nuevo bloque.</li>
      </ol> </li>
     <li>Del mismo modo, ajuste las referencias a las reglas de puntuación en un nodo de regla de distintivo para que tengan una ruta relativa.</li>
    </ol> <p> </p> <p>Finalmente, limpie eliminando el recurso <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Diseños de la consola de comunidades clásicas {#classic-communities-console-designs}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/designs/social/console</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
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

### Configuraciones de inicio de sesión social de Facebook {#facebook-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudservices/facebookconnect</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/facebookconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Cualquier configuración nueva de Facebook Cloud debe migrarse a la ubicación nueva.</p>
    <ol>
     <li>Migrar las configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ol>
       <li>Vuelva a crear manualmente las nuevas configuraciones de inicio de sesión de Facebook Social a través de la IU de creación de AEM en <strong>Herramientas &gt; Cloud Services &gt; Configuración de inicio de sesión social de Facebook</strong>.<br /> o <br /> </li>
       <li>Copie cualquier configuración nueva de Facebook Cloud de la ubicación anterior a la ubicación nueva adecuada, en <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Actualice cualquier raíz del sitio de AEM Communities para hacer referencia a la nueva Configuración de inicio de sesión social de Facebook estableciendo la propiedad <code>[cq:Page]/jcr:content@cq:conf</code> en la ruta absoluta en la Nueva ubicación.</li>
     <li>Desasocie el Cloud Service de Facebook Connect heredado de cualquier raíz de sitio de AEM Communities actualizada para hacer referencia a la Nueva ubicación.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Opciones de idioma Configuraciones {#language-options-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/social/config/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
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

### Configuraciones de inicio de sesión de Pinterest Social {#pinterest-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudservices/pinterestconnect</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/pinterestconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Las configuraciones de Pinterest Cloud nuevas deben migrarse a la ubicación nueva.</p>
    <ol>
     <li>Migrar las configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ol>
       <li>Vuelva a crear manualmente las nuevas configuraciones de inicio de sesión de Pinterest Social a través de la IU de creación de AEM en <strong>Herramientas &gt; Cloud Services &gt; Configuración de inicio de sesión social de Pinterest</strong>.<br /> o</li>
       <li>Copie cualquier configuración nueva de Pinterest Cloud de Ubicación anterior a la Nueva ubicación adecuada en <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Actualice cualquier raíz del sitio de AEM Communities para hacer referencia a la nueva Configuración de inicio de sesión social de Pinterest mediante la configuración de la propiedad <code>[cq:Page]/jcr:content@cq:conf</code> a la ruta absoluta de la Nueva ubicación.</li>
     <li>Desasocie el Cloud Service de Pinterest Connect heredado de cualquier raíz de sitio de AEM Communities actualizada para hacer referencia a la Nueva ubicación.</li>
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/libs/settings/community/scoring</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Para alinearse con la nueva estructura del repositorio, las reglas de puntuación se pueden almacenar en <code>/apps/settings/</code> o /<code>conf/.../settings</code></p>
    <ol>
     <li>Para <code>/apps/settings</code>, esto actuaría como reglas globales o predeterminadas administradas en SCM.</li>
    </ol> <p>Cree configuraciones según el contexto en <code>/conf/</code> usando CRXDELite:</p>
    <ol>
     <li>Cree las configuraciones en la ubicación <code>/conf/.../settings</code><br /> deseada </li>
     <li>El sitio de Communities debe tener la propiedad <code>cq:conf </code>establecida.
      <ol>
       <li>Si no se establece ningún <code>cq:conf</code>, las reglas de puntuación se leerían directamente desde la ruta dada para la propiedad '<code>scoringRules</code>' en el nodo raíz del sitio, por ejemplo: <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>Limpieza: Eliminar el recurso <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configuraciones de inicio de sesión social de Twitter {#twitter-social-login-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/cloudservices/twitterconnect</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><code class="code">/conf/global/settings/cloudconfigs/twitterconnect
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Las configuraciones de Twitter Cloud nuevas deben migrarse a la ubicación nueva.</p>
    <ol>
     <li>Migrar las configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ol>
       <li>Vuelva a crear manualmente las nuevas configuraciones de inicio de sesión social de Twitter mediante la interfaz de usuario de creación de AEM en <strong>Herramientas &gt; Cloud Services &gt; Configuración de inicio de sesión social de Twitter</strong>.<br /> o <br /> </li>
       <li>Copie cualquier configuración nueva de Twitter Cloud de la ubicación anterior a la ubicación nueva adecuada, en <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Actualice cualquier raíz del sitio de AEM Communities para hacer referencia a la nueva Configuración de inicio de sesión social de Twitter estableciendo la propiedad <code>[cq:Page]/jcr:content@cq:conf</code> en la ruta absoluta de la Nueva ubicación.</li>
     <li>Desasocie el Cloud Service heredado de Twitter Connect de cualquier raíz de sitio de AEM Communities actualizada para hacer referencia a la Nueva ubicación.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Misc {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/libs/settings/community/templates</code></td>
  </tr>
  <tr>
   <td><strong>Directrices de reestructuración</strong></td>
   <td><p>Adobe ha proporcionado una utilidad de migración en:</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Las plantillas personalizadas existentes se moverán a <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>

