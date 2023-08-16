---
title: Configuración de Analytics para funciones de Communities
seo-title: Analytics Configuration for Communities Features
description: Configurar Analytics para Communities
seo-description: Configure analytics for Communities
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
role: Admin
exl-id: 7d54928b-6512-4da9-a209-eb4488bf2b64
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2693'
ht-degree: 4%

---

# Configuración de Analytics para funciones de Communities {#analytics-configuration-for-communities-features}

## Información general {#overview}

Adobe Analytics y Adobe Experience Manager AEM () son soluciones de Adobe Marketing Cloud.

Adobe Analytics se puede configurar para AEM Communities de modo que, como miembro interactúe con las funciones de las Comunidades admitidas, se envíen eventos a Adobe Analytics desde el cual se generan los informes.

Por ejemplo, desde el sitio de la comunidad, los administradores pueden ver varios informes relacionados con la reproducción del vídeo.

Además, el análisis es necesario para lo siguiente:

* En el entorno de publicación:

   * Informes sobre la comunidad [tendencias](/help/communities/trends.md)
   * Permitir que los visitantes del sitio ordenen por &quot;más visitados&quot;, &quot;más activos&quot;, &quot;más gustados&quot;
   * Ver recuentos en listas UGC

* En el entorno de creación:

   * Visualización de los datos de participación en [consola de administración de miembros](/help/communities/members.md) (vistas, publicaciones, seguimientos, me gusta)
   * Resumen de tendencias, latido de vídeo y dispositivo de vídeo para el recurso de habilitación [informes](/help/communities/reports.md)

Entre las funciones compatibles de Communities se incluyen:

* [Foro](/help/communities/forum.md)
* [P y R](/help/communities/working-with-qna.md)
* [Blog](/help/communities/blog-feature.md)
* [Biblioteca de archivos](/help/communities/file-library.md)
* [Calendario](/help/communities/calendar.md)

En esta sección de la documentación se describe cómo conectar un grupo de informes de Analytics con funciones de Communities. Los pasos básicos son:

1. [Replicar la clave criptográfica](#replicate-the-crypto-key) AEM para garantizar que el cifrado/descifrado se produzca correctamente en todas las instancias de la
1. Preparación de un Adobe Analytics [grupo de informes](#adobe-analytics-report-suite-for-video-reporting)
1. AEM Creación de una lista de análisis de [cloud service](#aem-analytics-cloud-service-configuration) y [marco](#aem-analytics-framework-configuration)

1. [Habilitar Analytics](#enable-analytics-for-a-community-site) para un sitio de la comunidad
1. [**Verificar**](#verify-analytics-to-aem-variable-mapping) AEM Asignación de variables de Analytics a
1. Identificar [editor principal](#primary-publisher)
1. [Publish](#publish-community-site-and-analytics-cloud-service) el sitio de la comunidad
1. Configurar [importación de datos de informes](#obtaining-reports-from-analytics) de Adobe Analytics al sitio de la comunidad

## Requisitos previos {#prerequisites}

Para configurar las funciones de Analytics para Communities, es necesario trabajar con el representante de cuentas para configurar una cuenta de Adobe Analytics y [grupo de informes](#adobe-analytics-report-suite-for-video-reporting). Una vez establecida, debe estar disponible la siguiente información:

* **Nombre de la compañía**

  La compañía asociada a la cuenta de Adobe Analytics.

* **Nombre de usuario**

  El nombre de usuario de inicio de sesión del usuario autorizado para administrar la cuenta de Analytics (debe incluir privilegios de acceso al servicio web).

* **Contraseña**

  La contraseña de inicio de sesión del usuario autorizado.

* **Centro de datos de Analytics**

  La URL del centro de datos de Analytics de la cuenta.

* **Grupo de informes**

  Nombre del grupo de informes de Analytics que se va a utilizar.

## Grupo de informes de Adobe Analytics para informes de vídeo {#adobe-analytics-report-suite-for-video-reporting}

Uso del de Adobe Marketing Cloud [Administrador de grupos de informes](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html), los grupos de informes de Analytics se pueden configurar para que un sitio de la comunidad pueda proporcionar informes para las funciones de las Comunidades.

Iniciando sesión en [Adobe Experience Cloud](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) con [Nombre de empresa y nombre de usuario](/help/communities/analytics.md#prerequisites), es posible configurar un grupo de informes nuevo o existente para que tenga:

* [11 Variables de conversión](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) (eVars)

   * **`evar1`** mediante **`evar11`** activado

   * Puede cambiar el propósito (cambiar el nombre) de las eVars existentes o crear otras nuevas para usarlas en las funciones de Communities

* [7 eventos de éxito](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/success-events/success-event.html) (eventos)

   * **`event1`** mediante **`event7`** activado

   * type **`Counter`**

      * no **`Counter (no subrelations)`**

   * Puede cambiar el propósito (cambiar el nombre) de eventos existentes o crear otros nuevos para usarlos para las funciones de Communities

* [Administración de vídeo](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)

   * Consola de informes de vídeo

      * Habilitar `Video Core`
      * Seleccione Guardar

   * Consola de medición de Video Core

      * Seleccionar `Use Solution Variables`
      * Seleccione Guardar

Si se usa un **nuevo grupo de informes** Sin embargo, tenga en cuenta que un nuevo grupo de informes solo puede tener 4 evars y 6 variables de evento, mientras que se requieren 11 evars y 7 variables de evento para las comunidades.

Si se usa un **grupo de informes existente**, puede que sea necesario [modificación de la asignación de variables](#modifying-analytics-variable-mapping) antes de activar el marco de Analytics para un sitio de la comunidad.

Póngase en contacto con su representante de cuentas para cualquier preocupación relativa a las variables dedicadas a las Comunidades.

>[!CAUTION]
>
>**Si usa un grupo de informes existente que ya usa variables en**
>
>* **`evar1`** hasta **`evar11`**
>
>* **`event1`** hasta **`event7`**
>
>**A continuación, antes de publicar el sitio de la comunidad,** AEM Es importante restaurar la asignación preexistente moviendo las variables de la comunidad que se asignaron automáticamente a las variables de Analytics cuando Analytics estaba habilitado para un sitio de la comunidad.
>
>AEM Para restaurar la asignación preexistente y mover variables de a otras variables de Analytics, consulte la sección sobre [Modificación de la asignación de variables de Analytics](#modifying-analytics-variable-mapping).
>
>Si no lo hace, puede causar una pérdida de datos irrecuperable.

### Video Heartbeat Analytics {#video-heartbeat-analytics}

Cuando Video Heartbeat Analytics tiene licencia, se crea un `Marketing Cloud Org Id` se ha asignado.

Para habilitar los informes de Video Heartbeat después de [configuración del grupo de informes de Analytics para informes de vídeo](#adobe-analytics-report-suite-for-video-reporting):

* Crear un [Analytics Cloud Service](#aem-analytics-cloud-service-configuration)
* Activar [Analytics para un sitio de la comunidad](#enable-analytics-for-a-community-site)
* Asocie el `Marketing Cloud Org Id` con el sitio de la comunidad

El `Marketing Cloud Org Id` puede introducirse en el momento de [creación de sitios de la comunidad](/help/communities/sites-console.md) o más tarde por [modificación](/help/communities/sites-console.md#modifying-site-properties) las propiedades del sitio de la comunidad.

![marketing-org-id](assets/marketing-org-id.png)

Cuando Video Heartbeat Analytics está habilitado, el código JavaScript (JS) del reproductor de vídeo crea una instancia del código de biblioteca de Video Heartbeat (también en JS) que gestiona toda la lógica para enviar actualizaciones de estado de vídeo a los servidores de seguimiento de vídeo de Analytics cada 10 segundos (no configurables) y, finalmente, enviar un informe acumulado de la sesión de vídeo a los servidores principales de Analytics.

Si no está habilitado, el código de latido de vídeo nunca se crea una instancia y solo el progreso del vídeo y el seguimiento de posición de reanudación se mantienen en SRP para la creación de informes.

## AEM Configuración del servicio de Analytics Cloud {#aem-analytics-cloud-service-configuration}

Para crear una nueva integración de Analytics, que integre Adobe Analytics AEM con el sitio de la comunidad de, mediante la interfaz de usuario estándar en la instancia de autor:

* Desde la navegación global: **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Cloud Service]**
* Desplazarse hacia abajo hasta **[!UICONTROL Adobe Analytics]**
* Seleccionar **[!UICONTROL Configurar ahora]** o **[!UICONTROL Mostrar configuraciones]**

![cloud-config](assets/cloud-config1.png)

### Cuadro de diálogo Crear configuración {#create-configuration-dialog}

* Seleccionar `[+]` junto a **[!UICONTROL Configuraciones disponibles]** para crear una nueva configuración

En el cuadro de diálogo Crear configuración, los valores que se van a introducir identifican la configuración.

![create-cloud-config](assets/cloud-config2.png)

* **Título**

  (Obligatorio) Un título para mostrar para la configuración.
Por ejemplo, introduzca *Análisis de comunidad*

* **Nombre**

  (Opcional) Si no se especifica, el nombre tendrá de forma predeterminada un nombre de nodo válido derivado del título.
Por ejemplo, introduzca *comunidades*

* **Plantilla**

  Seleccionar `Adobe Analytics Configuration`

* Seleccione **Crear**

   * Inicia la página de configuración y abre `Analytics Settings` diálogo

### Cuadro de diálogo Configuración de Analytics {#analytics-settings-dialog}

La creación inicial de una nueva configuración de Analytics da como resultado la visualización de la configuración y un nuevo cuadro de diálogo para la entrada de la Configuración de Analytics. Este cuadro de diálogo requiere [información de cuenta de prerrequisito](#prerequisites) obtenido del representante de cuentas.

![analytics-settings](assets/analytics-settings.png)

* **Compañía**

  La compañía asociada a la cuenta de Adobe Analytics.

* **Nombre de usuario**

  El nombre de usuario de inicio de sesión del usuario autorizado para administrar la cuenta de Analytics.

* **Contraseña**

  La contraseña de inicio de sesión del usuario autorizado.

* **Centro de datos**

  Seleccione el centro de datos de Analytics que aloja el grupo de informes.

* **No añadir etiqueta de seguimiento a la página**

  Dejar como predeterminado (sin seleccionar).

* **Utilizar AppMeasurement**

  Dejar como predeterminado (sin seleccionar).

* **No importar las impresiones de la página cada noche (Author)**

  Dejar como predeterminado (sin seleccionar).

* **No importar las impresiones de la página cada noche (Publish)**

  Dejar como predeterminado (sin seleccionar).

Para guardar la configuración:

* Seleccionar **Conectar con Analytics**

   * Si no se realiza correctamente,

      * Compruebe que las entradas no contienen espacios iniciales.
      * Pruebe con otro centro de datos.

* Seleccionar **OK**.

  ![analytics-settings](assets/analytics-settings1.png)

### Crear módulo {#create-framework}

Después de configurar correctamente la conexión básica a Adobe Analytics, es necesario crear o editar un marco de trabajo para el sitio de la comunidad. AEM El propósito del marco de trabajo es asignar variables de características de las comunidades () a variables de Analytics (grupo de informes).

* Seleccionar `[+]` junto a **[!UICONTROL Módulos disponibles]** para crear un nuevo marco

  ![analytics-framework](assets/analytics-framework.png)

* **Título**

  (Obligatorio) Un título para mostrar para el marco de trabajo. Por ejemplo, escriba *Community Framework*.

* **Nombre**

  (Opcional) Si no se especifica, el nombre tendrá de forma predeterminada un nombre de nodo válido derivado del título.
Por ejemplo, introduzca *comunidades*.

* *Plantilla*

  Seleccionar `Adobe Analytics Framework`.

* Seleccione **Crear**.

Al crear el marco de Analytics, se abre el marco de trabajo para la configuración.

## AEM Configuración del marco de análisis de {#aem-analytics-framework-configuration}

AEM El propósito del marco de trabajo es asignar variables de a variables de Analytics (eVars y eventos). Las variables de Analytics disponibles para la asignación son [definido en el grupo de informes](#adobe-analytics-report-suite-for-video-reporting).

![analytics-framework](assets/analytics-framework1.png)

### Seleccionar grupo de informes {#select-report-suite}

Seleccione el grupo de informes que se ha configurado para los informes de vídeo.

Si aún no se ha creado o configurado correctamente un grupo de informes, consulte la sección anterior:
[Grupo de informes de Adobe Analytics para informes de vídeo](#adobe-analytics-report-suite-for-video-reporting)

El Sidekick no es necesario y puede minimizarse para que no obstruya el acceso a la configuración del grupo de informes.

#### Cuadro de diálogo Grupos de informes antes y después de seleccionar &quot;Agregar elemento&quot; {#report-suites-dialog-before-and-after-selecting-add-item}

![grupo de informes](assets/report-suite.png)

1. Seleccionar **Agregar elemento +**.

   Aparecerán dos cuadros desplegables.

1. Elija una `Report suite.`

   Los grupos de informes asociados a la cuenta de la compañía están disponibles para su selección.

1. Seleccionar **Sí** en el cuadro de diálogo que se abre:

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. Elija una `Run Mode`.

1. Seleccionar **Publish**.

![analytics-framework2](assets/analytics-framework2.png)

El servicio en la nube y el marco de Analytics ya están completos. Las asignaciones se definirán una vez que se haya creado un sitio de la comunidad con este servicio de Analytics habilitado.

## Habilitar Analytics para un sitio de la comunidad {#enable-analytics-for-a-community-site}

### Habilitar para el nuevo sitio de la comunidad {#enable-for-new-community-site}

Para añadir el servicio en la nube de Analytics mientras [crear un nuevo sitio de la comunidad](/help/communities/sites-console.md):

* En el paso 3, en la sección [Pestaña ANALYTICS](/help/communities/sites-console.md#analytics):
   * Seleccione el **Habilitar Analytics** casilla de verificación.
   * Seleccione el marco de trabajo en el cuadro desplegable.

* De forma opcional, vuelva a la configuración del marco de trabajo de Analytics para ajustar las asignaciones de variables.

### Habilitar para sitio de comunidad existente {#enable-for-existing-community-site}

Para agregar el servicio en la nube de Analytics a una [sitio de la comunidad existente](/help/communities/sites-console.md#modifying-site-properties):

* Vaya a **Comunidades > Sitios** consola.
* Seleccione el icono de la comunidad Editar sitio.
* Seleccione la opción CONFIGURACIÓN.
* En la sección Analytics:
   * Seleccione el **Habilitar Analytics** casilla de verificación.
   * Elija el marco de trabajo en el cuadro desplegable.

* De forma opcional, vuelva a la configuración del marco de trabajo de Analytics para ajustar las asignaciones de variables.

### Habilitar para sitios personalizados {#enable-for-customized-sites}

Para que el seguimiento y la importación de Analytics funcionen correctamente en un sitio de la comunidad, agregue un elemento de página con el `scf-js-site-title` los atributos class y href deben estar presentes. Solo debe existir un elemento de este tipo en la página, como en una página sin modificar `sitepage.hbs` script para un sitio de la comunidad. El valor de `siteUrl` se extrae y se envía a Adobe Analytics como *ruta del sitio*.

```xml
# present in default sitepage.hbs
# only one scf-js-site-title class should be included
# this example sets it to be hidden as it serves no visual purpose
<div
    class="navbar-brand scf-js-site-title"
    href="{{siteUrl}}.html"
    style="visibility: hidden;"
>
</div>
```

Para un **sitio personalizado de la comunidad** que se superpone a `sitepage.hbs` , asegúrese de que el elemento esté presente. El `siteUrl` se establecerá cuando se represente en el servidor antes de entregarse al cliente.

Para un **AEM sitio genérico** que incluye componentes de Communities, pero no se crea con [asistente de creación de sitios](/help/communities/sites-console.md), es necesario añadir el elemento. El valor del href debe ser la ruta al sitio. Por ejemplo, si la ruta del sitio es `/content/my/company/en`, luego use:

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

## Funciones de Analytics para comunidades {#analytics-for-communities-features}

Analytics se utiliza automáticamente para varias funciones de Communities.

El entorno de creación es [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Component Configuration`, proporciona una lista de los componentes que se han instrumentado para Analytics. La asignación automática de variables viene determinada por los componentes enumerados.

Si se crean nuevos componentes personalizados que están instrumentados para Analytics, deben añadirse a esta lista de componentes configurados.

### Configuración de componentes {#component-configuration}

![component-configuration1](assets/component-configuration1.png)

>[!NOTE]
>
>Los componentes de diario se utilizan para implementar la función de blog.

### AEM Analytics asignado a variables de {#mapped-analytics-to-aem-variables}

AEM Una vez que se guarde el sitio de la comunidad con Analytics habilitado y se seleccione el marco de trabajo de configuración de la nube, las variables de se asignarán automáticamente a las eVars y a los eventos de Analytics que comiencen con evar1 y event1, respectivamente, y se incrementen en 1.

Si utiliza un grupo de informes existente que haya asignado cualquiera de las variables dentro de evar1 a evar11 y de event1 a event7, será necesario [AEM reasignación de las variables de](#modifying-analytics-variable-mapping) y restaure la asignación original.

A continuación se muestra un ejemplo de asignaciones predeterminadas:

![map-analytics](assets/map-analytics1.png)

#### Mapa de eVars enviadas con cada evento {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Habilitación<br /> Recurso<br /> Tipo</strong></td>
   <td><strong>Sitio<br /> Título</strong></td>
   <td><strong>Función<br /> Tipo</strong></td>
   <td><strong>Grupo<br /> Título</strong></td>
   <td><strong>Grupo<br /> Ruta</strong></td>
   <td><strong>UGC<br /> Tipo</strong></td>
   <td><strong>UGC<br /> Título</strong></td>
   <td><strong>Usuario<br /> (Miembro)</strong></td>
   <td><strong>UGC<br /> Ruta</strong></td>
   <td><strong>Sitio<br /> Ruta</strong></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><strong>eVar1</strong></td>
   <td><strong>eVar2</strong></td>
   <td><strong>eVar3</strong></td>
   <td><strong>eVar4</strong></td>
   <td><strong>eVar5</strong></td>
   <td><strong>eVar6</strong></td>
   <td><strong>eVar7</strong></td>
   <td><strong>eVar8</strong></td>
   <td><strong>eVar9</strong></td>
   <td><strong>eVar10</strong></td>
  </tr>
  <tr>
   <td><strong>event1<br /> Reproducción de medios</strong></td>
   <td><em>(a)</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>(i)</em></td>
   <td><em>-</em></td>
  </tr>
  <tr>
   <td><strong>event2<br /> SCFView</strong></td>
   <td><em>(a)</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event3<br /> SCFCreate (Post)</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event5<br /> SCFVoteUp</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
  <tr>
   <td><strong>event7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>(b)</em></td>
   <td><em>(c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>(i)</em></td>
   <td><em>(j)</em></td>
  </tr>
 </tbody>
</table>

**Ejemplos de valores de eVar:**

* *[Tipo MIME](https://www.iana.org/assignments/media-types)*: video/mp4
* *[título del sitio de la comunidad](/help/communities/sites-console.md#step13asitetemplate)*: comunidades de Geometrixx
* *[nombre de función de comunidad](/help/communities/functions.md)*: Foro
* *[nombre del grupo de comunidad](/help/communities/creating-groups.md#creating-a-new-group)*: Senderismo
* *ruta al contenido de grupo de la comunidad*: `/content/sites/<site name>/en/groups/hiking`
* *[ResourceType del componente UGC](/help/communities/essentials.md)*: `social/forum/components/hbs/topic`
* *Título del componente UGC*: Temas de Senderismo
* *inicio de sesión (authorizableId)*: `aaron.mcdonald@mailinator.com`
* *Ruta de SRP a UGC*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
o *ruta del componente a seguir*: `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *ruta al contenido del sitio de la comunidad*: `/content/sites/<site name>/en`

### Modificación de la asignación de variables de Analytics {#modifying-analytics-variable-mapping}

AEM La asignación de eVars y eventos de Analytics a variables de se puede ver desde la configuración del marco de trabajo una vez que Analytics esté habilitado para un sitio de la comunidad.

Una vez habilitado Analytics y antes de que se publique el sitio de la comunidad, la asignación puede modificarse en el marco de trabajo arrastrando la eVar o el evento de Analytics deseado desde el carril izquierdo y soltándolo en la fila correspondiente de la tabla de asignación.

Para evitar asignaciones duplicadas, asegúrese de quitar la eVar o el evento de Analytics reemplazado de la fila pasando el puntero sobre él y seleccionando la &quot;X&quot; que aparece a la derecha del elemento de variable de Analytics.

AEM Si las eVars y los eventos de las comunidades sobrescriben las asignaciones preexistentes en el grupo de informes, para evitar la pérdida de datos, asigne las variables de las comunidades para las características de las comunidades a otras eVars o eventos de Analytics y restaure las asignaciones originales.

>[!CAUTION]
>
>Es importante volver a asignar antes de que se ejecute el sitio de la comunidad [publicado](#publishing-the-community-site) si Analytics está habilitado, existe el riesgo de que se pierdan datos.

#### Ejemplo Paso 1: Arrastrar Analytics evar14 a la tabla de asignación {#example-step-dragging-analytics-evar-into-mapping-table}

![analytics-mapping-evar](assets/analytics-mapping-evar.png)

#### Ejemplo de paso 2: Seleccionar &quot;x&quot; para eliminar el evar11 reemplazado {#example-step-selecting-x-to-remove-replaced-evar}

![analytics-mapping-evar1](assets/analytics-mapping-evar1.png)

#### AEM Ejemplo Paso 3: reasignación de var eventdata.siteId a Analytics evar14 {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![analytics-mapping-evar2](assets/analytics-mapping-evar2.png)

## Publicación del sitio de la comunidad {#publishing-the-community-site}

### AEM Verificar la asignación de Analytics a variables de {#verify-analytics-to-aem-variable-mapping}

Es aconsejable verificar la asignación de variables antes de publicar el sitio de la comunidad, que también publica el marco y el servicio en la nube de Analytics.

Consulte las secciones:

* [AEM Analytics asignado a variables de](#mapped-analytics-to-aem-variables)
* [Modificación de la asignación de variables de Analytics](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**Si usa un grupo de informes existente que ya usa variables en**
>
>* **`evar1`** hasta **`evar11`**
>
>* **`event1`** hasta **`event7`**
>
>**A continuación, antes de publicar el sitio de la comunidad,** AEM Es importante restaurar la asignación preexistente y mover las variables de la comunidad que se asignaron automáticamente (cuando Analytics estaba habilitado para el sitio de la comunidad) a otras variables de Analytics. Esta reasignación debe ser coherente en todos los componentes de las comunidades.
>
>Si no lo hace, puede causar una pérdida de datos irrecuperable.

### Editor principal {#primary-publisher}

Cuando la implementación elegida es una [publicar conjunto de servidores](/help/communities/topologies.md#tarmk-publish-farm)AEM A continuación, se debe identificar una instancia de publicación de como el editor principal para sondear Adobe Analytics y escribir los datos del informe en [SRP](/help/communities/working-with-srp.md).

De forma predeterminada, la variable `AEM Communities Publisher Configuration` La configuración de OSGi identifica su instancia de publicación como el editor principal, de modo que todas las instancias de publicación de un conjunto de servidores de publicación se identificarían automáticamente como el editor principal.

Por lo tanto, es necesario editar la configuración en todas las instancias de publicación secundarias para anular la selección del **Editor principal** casilla de verificación.

Para obtener instrucciones específicas, consulte la sección del editor principal de [Implementación de comunidades](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>Es importante que el editor principal esté configurado para evitar el sondeo de varias instancias de publicación.

### Replicar la clave criptográfica {#replicate-the-crypto-key}

Las credenciales de Adobe Analytics están cifradas. AEM Para facilitar la replicación o transmisión de credenciales de análisis cifradas entre el autor y los editores, todas las instancias de la deben compartir la misma clave de cifrado principal.

Para ello, siga las instrucciones en [Replicar la clave criptográfica](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Publicar sitio de la comunidad y servicio de Analytics Cloud {#publish-community-site-and-analytics-cloud-service}

Una vez habilitado el servicio en la nube de Analytics para un sitio de la comunidad y, si es necesario, la variable [AEM se ha ajustado la asignación de Analytics a variables de](#mapped-analytics-to-aem-variables), es necesario replicar la configuración en el entorno de publicación mediante [volver a publicar el sitio de la comunidad](/help/communities/sites-console.md#publishing-the-site).

## Obtener informes de Analytics {#obtaining-reports-from-analytics}

### Administración de informes {#report-management}

El autor y el editor principal [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Management`, se utiliza para consultar Analytics.

En el autor, las consultas son para informes en tiempo real.

En el editor principal, las consultas se utilizan para proporcionar información como preparación para la importación de datos de Analytics del importador de informes.

El valor predeterminado del intervalo de consulta es de 10 segundos.

### Importador de informes {#report-importer}

Una vez publicado un sitio de la comunidad habilitado para Analytics, el editor principal [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md), `AEM Communities Analytics Report Importer`, se puede configurar para establecer el intervalo de sondeo predeterminado para las configuraciones que no se configuran individualmente en CRXDE.

El intervalo de sondeo controla la frecuencia de las solicitudes a Adobe Analytics para que extraiga y guarde los datos en [SRP](/help/communities/working-with-srp.md).

Cuando los datos se pueden categorizar como &quot;big data&quot;, un sondeo más frecuente puede cargar mucho el sitio de la comunidad.

El sondeo predeterminado **Intervalo de importación** se establece en 12 horas.

![importador de informes](assets/report-importer.png)

### Personalización de informe de componentes {#component-report-customization}

Actualmente, para personalizar las métricas que se van a rastrear, se crean nodos en el repositorio que definen períodos de tiempo para los que generar un informe sobre esa métrica.

El tema del foro es actualmente el único ejemplo de esta personalización:

* En el editor principal, inicie sesión con privilegios administrativos.
* Vaya a [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Por ejemplo, [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* En el nodo jcr:content de la raíz del idioma (por ejemplo, `/content/sites/engage/en/jcr:content),`vaya al componente configurado para los informes de Analytics.
Por ejemplo, **`analytics/reportConfigs/social_forum_components_hbs_topic`**

* Observe los periodos de tiempo creados:

   * `last30Days`
   * `last90Days`
   * `thisYear`

* Observe el `total`nodo.

   * Modificación del **`interval`** anula el intervalo del importador de informes.
   * El valor se establece en 4 horas (14400 segundos) en segundos.

![informe-componente](assets/component-report.png)

## Administración de datos de usuario en Analytics {#manage-user-data-in-analytics}

Adobe Analytics proporciona API que le permiten acceder, exportar y eliminar datos de usuario. Para obtener más información, consulte [Envío de solicitudes de acceso y eliminación](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html).

## Recursos {#resources}

* Adobe Experience Cloud: [Ayuda y referencia de Analytics](https://experienceleague.adobe.com/docs/analytics.html)
* AEM: [Integración con Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* AEM: [Analytics con proveedores externos](/help/sites-administering/external-providers.md)
