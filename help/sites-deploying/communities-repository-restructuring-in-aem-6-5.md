---
title: Reestructuración del repositorio para AEM Communities en 6.4
seo-title: Reestructuración del repositorio para AEM Communities en 6.4
description: Obtenga información sobre cómo realizar los cambios necesarios para migrar a la nueva estructura de repositorio en AEM 6.4 for Communities.
seo-description: Obtenga información sobre cómo realizar los cambios necesarios para migrar a la nueva estructura de repositorio en AEM 6.4 for Communities.
uuid: d161655f-4074-44a7-8d69-38e80934c58b
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 7383265b-0ed4-4ea7-b741-0a417d187bdd
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# Reestructuración del repositorio para AEM Communities en 6.5 {#repository-restructuring-for-aem-communities-in}

Como se describe en la página principal Reestructuración [del repositorio en AEM 6.4](/help/sites-deploying/repository-restructuring.md) , los clientes que actualicen a AEM 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado a los cambios del repositorio que afectan a la solución AEM Communities. Algunos cambios requieren esfuerzo durante el proceso de actualización de AEM 6.5, mientras que otros se pueden aplazar hasta una actualización futura.

**Con actualización a 6.5**

* [Plantillas de notificación de correo electrónico](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#e-mail-notification-templates)
* [Configuraciones de suscripción](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#subscription-configurations)

**Antes de la actualización futura**

* [Configuraciones de distintivos](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#badging-configurations)
* [Diseños de la consola de las comunidades clásicas](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#classic-communities-console-designs)
* [Configuraciones de inicio de sesión social de Facebook](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#facebook-social-login-configurations)
* [Configuraciones de opciones de idioma](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#language-options-configurations)

* [Configuraciones de inicio de sesión de Pinterest Social](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#pinterest-social-login-configurations)
* [Configuraciones de puntuación](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#scoring-configurations)
* [Configuraciones de inicio de sesión social de Twitter](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#twitter-social-login-configurations)
* [Misc](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md#misc)

## Con actualización a 6.5 {#with-upgrade}

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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>La migración manual es necesaria si desea moverse a la nueva ruta en "<code>/apps/settings</code>". Puede utilizar Granite Configuration Manager para realizar la migración.</p> <p>Puede realizar la migración estableciendo la propiedad <code>mergeList</code> en <code>true</code> el nodo "<code>/libs/settings/community/subscriptions</code>" y agregando un nodo <code>nt:unstructured</code> secundario.</p> </td>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>La migración manual es necesaria si desea moverse a la nueva ruta en "<code>/apps/settings</code>". Puede utilizar Granite Configuration Manager para realizar la migración.</p> <p>Puede realizar la migración estableciendo la propiedad <code>mergeList</code> en <code>true</code> el nodo "<code>/libs/settings/community/subscriptions</code>" y agregando un nodo <code>nt:unstructured</code> secundario.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Configuraciones de palabras de observación {#watchwords-configurations}

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
   <td><strong>Orientación de reestructuración</strong></td>
   <td>Hay disponible una tarea de migración diferida para limpiar las configuraciones de comunidades.<br /> <p>La tarea mueve las palabras clave de <code>/etc/watchwords</code> a <code>/conf/global/settings/community/watchwords</code>.</p> <p>Si las palabras clave personalizadas se almacenan en SCM, entonces deben implementarse en <code>/apps/settings/...</code> y debe asegurarse de que no hay una configuración de superposición <code>/conf/global/settings/...</code> que tenga prioridad.</p> <p>La tarea de migración elimina <code>/etc</code> ubicaciones.</p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

## Antes de la actualización futura {#prior-to-upgrade}

### Configuraciones de distintivos {#badging-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>Ubicación anterior</strong></td>
   <td><code>/etc/community/badging</code></td>
  </tr>
  <tr>
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><p><strong>Reglas de distintivo:</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>Imágenes distintivas:</strong></p> <p>Para imágenes predeterminadas: <code>/etc/community/badging/images are moved to /libs/community/badging/images</code></p> <p>Para imágenes personalizadas: <code>/content/community/badging/images</code></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Se requiere la migración manual.</p> <p>Si la instancia ha personalizado las reglas de puntuación/identificación, no hay una forma automatizada de colocar todas las reglas bajo un bucket. Necesita entradas del cliente en el bucket conf (global o específico del sitio) que desea utilizar para su sitio.</p> <p>No hay ninguna interfaz de usuario disponible para configurar el distintivo y la puntuación de un sitio.</p> <p>Para alinear con la nueva estructura de repositorio:</p>
    <ol>
     <li>Creación de un bloque de contexto de sitio mediante el navegador <strong>de</strong> configuración en <strong>Herramientas</strong></li>
     <li>Ir a la raíz del sitio</li>
     <li>Establezca <code>cq:confproperty</code> en la ruta del depósito donde desee almacenar toda la configuración. Lo mismo se puede establecer mediante el Asistente para <strong>edición del sitio: Configurar entrada</strong>de configuración de nube.</li>
     <li>Mueva las reglas de marcado y las reglas de puntuación relevantes desde <code>/etc/community/*</code> al bloque de contexto del sitio creado en el paso anterior.</li>
     <li>Ajuste las propiedades Reglas de marcado y Reglas de puntuación en la raíz del sitio para que tengan referencias relativas a las nuevas ubicaciones de reglas.
      <ol>
       <li>Por ejemplo, si la propiedad de <code>cq:conf = /conf/we-retail</code>, entonces <code>badgingRules [] = community/badging/rules</code> si las reglas ahora se mueven a este nuevo bloque.</li>
      </ol> </li>
     <li>Del mismo modo, ajuste las referencias a las reglas de puntuación en un nodo de regla de marcado para que tenga una ruta relativa.</li>
    </ol> <p> </p> <p>Por último, limpie quitando el recurso <code>/etc/community/badging</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Diseños de la consola de las comunidades clásicas {#classic-communities-console-designs}

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
   <td><strong>Orientación de reestructuración</strong></td>
   <td>N/D</td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Facebook Social Login Configurations {#facebook-social-login-configurations}

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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Todas las configuraciones nuevas de Facebook Cloud deben migrarse a la nueva ubicación.</p>
    <ol>
     <li>Migrar configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ol>
       <li>Vuelva a crear manualmente las nuevas configuraciones de inicio de sesión de Facebook Social mediante la interfaz de usuario de creación de AEM en <strong>Herramientas &gt; Servicios de nube &gt; Configuración</strong>de inicio de sesión de Facebook Social.<br /> o <br /> </li>
       <li>Copie cualquier configuración de nube de Facebook nueva de Ubicación anterior en la Ubicación nueva correspondiente, en <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Actualice cualquier raíz del sitio de comunidades AEM para hacer referencia a la nueva configuración de inicio de sesión social de Facebook estableciendo la propiedad en la ruta absoluta de la nueva ubicación. <code>[cq:Page]/jcr:content@cq:conf</code></li>
     <li>Desasocie el servicio heredado de Facebook Connect Cloud de cualquier raíz de sitio de AEM Communities actualizada para hacer referencia a la nueva ubicación.</li>
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
   <td><strong>Nuevas ubicaciones</strong></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
  </tr>
  <tr>
   <td><strong>Orientación de reestructuración</strong></td>
   <td>N/D<br /> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Pinterest Social Login Configurations {#pinterest-social-login-configurations}

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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Todas las configuraciones nuevas de Pinterest Cloud deben migrarse a la nueva ubicación.</p>
    <ol>
     <li>Migrar configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ol>
       <li>Vuelva a crear manualmente las nuevas configuraciones de inicio de sesión de Pinterest Social mediante la interfaz de usuario de creación de AEM en <strong>Herramientas &gt; Servicios de nube &gt; Configuración</strong>de inicio de sesión de Pinterest Social.<br /> o</li>
       <li>Copie cualquier configuración nueva de Pinterest Cloud desde Ubicación anterior a la Ubicación nueva correspondiente en <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Actualice cualquier raíz del sitio de comunidades de AEM para hacer referencia a la nueva configuración de inicio de sesión social de Pinterest mediante la configuración de la propiedad a la ruta absoluta de la nueva ubicación. <code>[cq:Page]/jcr:content@cq:conf</code></li>
     <li>Desasocie el servicio heredado de Pinterest Connect Cloud de cualquier raíz de sitio de AEM Communities actualizada para hacer referencia a la nueva ubicación.</li>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Para alinearse con la nueva estructura de repositorio, las reglas de puntuación se pueden almacenar en <code>/apps/settings/</code> o /<code>conf/.../settings</code></p>
    <ol>
     <li>Por ejemplo, <code>/apps/settings</code>esto actuaría como reglas globales o predeterminadas administradas en SCM.</li>
    </ol> <p>Cree configuraciones según el contexto en <code>/conf/</code> mediante CRXDELite:</p>
    <ol>
     <li>Cree las configuraciones en la ubicación deseada <code>/conf/.../settings</code><br /> </li>
     <li>El sitio de comunidades debe tener la propiedad <code>cq:conf </code>establecida.
      <ol>
       <li>Si no <code>cq:conf</code> se establece ningún valor, las reglas de puntuación se leerán directamente desde la ruta dada de la propiedad '<code>scoringRules</code>' en el nodo raíz del sitio, por ejemplo: <code>/content/we-retail/us/en/community/jcr:content</code></li>
      </ol> </li>
    </ol> <p>Limpieza: Quitar el recurso <code>/etc/community/scoring</code></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>N/D<br /> </td>
  </tr>
 </tbody>
</table>

### Twitter Social Login Configurations {#twitter-social-login-configurations}

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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Todas las configuraciones nuevas de Twitter Cloud deben migrarse a la nueva ubicación.</p>
    <ol>
     <li>Migrar configuraciones existentes en la ubicación anterior a la nueva ubicación.
      <ol>
       <li>Vuelva a crear manualmente las nuevas configuraciones de inicio de sesión social de Twitter mediante la interfaz de usuario de creación de AEM en <strong>Herramientas &gt; Servicios de nube &gt; Configuración</strong>de inicio de sesión social de Twitter.<br /> o <br /> </li>
       <li>Copie las configuraciones nuevas de Twitter Cloud desde Ubicación anterior a la Ubicación nueva correspondiente, en <code>/conf/global or /conf/&lt;tenant&gt;</code>.</li>
      </ol> </li>
     <li>Actualice cualquier raíz del sitio de comunidades AEM para hacer referencia a la nueva configuración de inicio de sesión social de Twitter estableciendo la propiedad en la ruta absoluta de la nueva ubicación. <code>[cq:Page]/jcr:content@cq:conf</code></li>
     <li>Desasocie el servicio heredado de nube de Twitter Connect de cualquier raíz de sitio de AEM Communities actualizada para hacer referencia a la nueva ubicación.</li>
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
   <td><strong>Orientación de reestructuración</strong></td>
   <td><p>Adobe ha proporcionado una utilidad de migración en:</p> <p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration">https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration</a></p> </td>
  </tr>
  <tr>
   <td><strong>Notas</strong></td>
   <td>Las plantillas personalizadas existentes se moverán a <code>/conf/global/settings/community/template/&lt;groups/sites/functions&gt;</code></td>
  </tr>
 </tbody>
</table>

