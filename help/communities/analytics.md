---
title: Funciones de Configuración de Analytics para Comunidades
seo-title: Funciones de Configuración de Analytics para Comunidades
description: Configuración de análisis para comunidades
seo-description: Configuración de análisis para comunidades
uuid: 5a083645-9de6-4ecd-a94e-a40143f92edf
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e6fdaf56-402f-418d-96d8-e46bd3ad1e8c
docset: aem65
translation-type: tm+mt
source-git-commit: 8279cd590244a7f2d20cfaf1c7505a3ef57fae4a
workflow-type: tm+mt
source-wordcount: '2760'
ht-degree: 4%

---


# Funciones de Configuración de Analytics para Comunidades {#analytics-configuration-for-communities-features}

## Información general {#overview}

Adobe Analytics y Adobe Experience Manager (AEM) son soluciones de Adobe Marketing Cloud.

Adobe Analytics se puede configurar para AEM Communities de modo que, al interactuar un miembro con las funciones admitidas de Communities, se envíen eventos a Adobe Analytics desde donde se generan informes.

Por ejemplo, cuando un miembro de un sitio de comunidad de habilitación vista un recurso de vídeo asignado a él, el reproductor de recursos enviará eventos a Analytics, incluidos datos de Video Heartbeat. Desde el sitio de la comunidad, los administradores pueden ver varios informes sobre la reproducción del video.

Además, es necesario realizar análisis para:

* En el entorno de publicación:

   * Sistema de informes sobre [las tendencias de la comunidad](/help/communities/trends.md)
   * Permitir que los visitantes del sitio ordenen por &quot;más visitados&quot;, &quot;más activos&quot;, &quot;más apreciados&quot;
   * Recuentos de Vistas en listas UGC

* En el entorno del autor:

   * Visualización de datos de participación en la consola [de administración de](/help/communities/members.md) miembros (vistas, publicaciones, siguientes, &quot;Me gusta&quot;)
   * Resumen de tendencias, monitoreo de vídeo y dispositivo de vídeo para habilitar [informes de recursos](/help/communities/reports.md)

Las funciones de comunidades admitidas incluyen:

* [Recursos de habilitación](/help/communities/resources.md)
* [Foro](/help/communities/forum.md)
* [P y R](/help/communities/working-with-qna.md)
* [Blog](/help/communities/blog-feature.md)
* [Biblioteca de archivos](/help/communities/file-library.md)
* [Calendario](/help/communities/calendar.md)

Esta sección de la documentación describe cómo conectar un grupo de informes de Analytics con las funciones de Comunidades. Los pasos básicos son:

1. [Replicar la clave](#replicate-the-crypto-key) criptográfica para garantizar que el cifrado/descifrado se produce correctamente en todas las instancias de AEM
1. Preparación de un grupo de [informes de Adobe Analytics](#adobe-analytics-report-suite-for-video-reporting)
1. Creación de un servicio [y un](#aem-analytics-cloud-service-configuration) [marco de trabajo en la nube de Analytics para AEM](#aem-analytics-framework-configuration)

1. [Habilitar Analytics](#enable-analytics-for-a-community-site) para un sitio de comunidad
1. [**Verificar **](#verify-analytics-to-aem-variable-mapping)la asignación de variables de Analytics a AEM
1. Identifique al publicador [principal](#primary-publisher)
1. [Publicar](#publish-community-site-and-analytics-cloud-service) el sitio de la comunidad
1. Configurar la [importación de datos](#obtaining-reports-from-analytics) de informes desde Adobe Analytics al sitio de la comunidad

## Requisitos previos {#prerequisites}

Para configurar las funciones de Analytics para las comunidades, es necesario trabajar con el representante de cuentas para configurar una cuenta de Adobe Analytics y un grupo de [informes](#adobe-analytics-report-suite-for-video-reporting). Una vez establecida, debe disponerse de la siguiente información:

* **Nombre de Compañía**

   compañía asociada a la cuenta de Analytics de Adobe.

* **Nombre de usuario**

   El nombre de usuario de inicio de sesión del usuario autorizado para administrar la cuenta de Analytics (debe incluir privilegios de acceso a servicios Web).

* **Contraseña**

   La contraseña de inicio de sesión del usuario autorizado.

* **Analytics Data Center**

   Dirección URL del centro de datos de Analytics para la cuenta.

* **Grupo de informes**

   Nombre del grupo de informes de Analytics que se va a utilizar.

## Grupo de informes de Adobe Analytics para Sistema de informes de vídeo {#adobe-analytics-report-suite-for-video-reporting}

Con el Administrador [de grupos de](https://docs.adobe.com/content/help/en/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html)informes del Adobe Marketing Cloud, los grupos de informes de Analytics se pueden configurar para que un sitio de comunidad se pueda habilitar para proporcionar informes para las funciones de comunidades.

Al iniciar sesión en [Adobe Experience Cloud](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/home.html) con nombre de [Compañía y nombre](/help/communities/analytics.md#prerequisites)de usuario, es posible configurar un grupo de informes nuevo o existente para que tenga:

* [11 Variables](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html) de conversión (eVars)

   * **`evar1`** mediante **`evar11`** activación

   * Puede reutilizar (cambiar el nombre) las eVars existentes o crear otras nuevas para utilizarlas en las funciones de Communities

* [7 Eventos](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/success-events/success-event.html) de éxito (eventos)

   * **`event1`** mediante **`event7`** activación

   * tipo **`Counter`**

      * not **`Counter (no subrelations)`**
   * Puede reutilizar (cambiar el nombre de los eventos existentes o crear otros nuevos para utilizarlos en las funciones de Communities


* [Administración de vídeo](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)

   * Consola de Sistema de informes de vídeo

      * Habilitar `Video Core`
      * Seleccione Guardar
   * Consola de medición de Video Core

      * Seleccione `Use Solution Variables`
      * Seleccione Guardar


Si utiliza un **nuevo grupo** de informes, tenga en cuenta que un nuevo grupo de informes solo puede tener 4 eVars y 6 variables de evento, mientras que para las comunidades se requieren 11 eVars y 7 variables de evento.

Si utiliza un grupo **de informes** existente, puede ser necesario [modificar la asignación](#modifying-analytics-variable-mapping) de variables antes de activar el marco de Analytics para un sitio de comunidad. Póngase en contacto con el representante de cuentas para conocer cualquier inquietud relacionada con las variables dedicadas a las comunidades.

>[!CAUTION]
>
>**Si utiliza un grupo de informes existente que ya utiliza variables dentro de**
>
>* **`evar1`** hasta **`evar11`**
   >
   >
* **`event1`** hasta **`event7`**
>
>
**Después, antes de publicar el sitio de la comunidad,** es importante restaurar la asignación preexistente moviendo las variables de AEM que se asignaron automáticamente a variables de Analytics cuando Analytics estaba habilitado para un sitio de la comunidad.
>
>Para restaurar la asignación preexistente y mover variables de AEM a otras variables de Analytics, consulte la sección sobre [modificación de la asignación](#modifying-analytics-variable-mapping)de variables de Analytics.
>
>Si no lo hace, puede producirse una pérdida de datos irrecuperable.

### Video Heartbeat Analytics {#video-heartbeat-analytics}

Cuando Analytics de Video Heartbeat tiene licencia, `Marketing Cloud Org Id` se asigna una.

Para habilitar el sistema de informes de Video Heartbeat después de [configurar el grupo de informes de Analytics para el sistema de informes](#adobe-analytics-report-suite-for-video-reporting)de vídeo:

* Creación de un servicio de nube de [Analytics](#aem-analytics-cloud-service-configuration)
* Habilitar [Analytics para un sitio de comunidad](#enable-analytics-for-a-community-site)
* Asociar el `Marketing Cloud Org Id` sitio con el sitio de la comunidad

El `Marketing Cloud Org Id` se puede ingresar en el momento de la creación [del sitio de la](/help/communities/sites-console.md#enablement) comunidad o posteriormente [modificando](/help/communities/sites-console.md#modifying-site-properties) las propiedades del sitio de la comunidad. [](#aem-analytics-cloud-service-configuration)

![chlimage_1-264](assets/chlimage_1-264.png)

Cuando Video Heartbeat Analytics está habilitado, el código JavaScript (JS) del reproductor de vídeo crea una instancia del código de Video Heartbeat Library (también en JS), que controla toda la lógica para enviar actualizaciones de estado de vídeo a los servidores de seguimiento de vídeo de Analytics cada 10 segundos (no configurables) y, finalmente, envía un informe acumulativo de la sesión de vídeo a los servidores principales de Analytics.

Si no está habilitado, nunca se crea una instancia del código de Video Heartbeat y solo el seguimiento de progreso del vídeo y de la posición de reanudación se mantiene en SRP para sistema de informes.

## Configuración de AEM Analytics Cloud Service {#aem-analytics-cloud-service-configuration}

Para crear una nueva integración de Analytics que integre Adobe Analytics con el sitio de la comunidad de AEM, utilice la IU estándar en la instancia de creación:

* Desde la navegación global: **[!UICONTROL Herramientas > Implementación > Cloud Service]**
* Desplácese hacia abajo hasta **[!UICONTROL Adobe Analytics]**
* Seleccione **[!UICONTROL Configurar ahora]** o **[!UICONTROL Mostrar configuraciones]**

![chlimage_1-265](assets/chlimage_1-265.png)

### Cuadro de diálogo Crear configuración {#create-configuration-dialog}

* Seleccione `[+]` el icono junto a **[!UICONTROL Configuraciones]** disponibles para crear una nueva configuración

En el cuadro de diálogo Crear configuración, los valores que se introducen identifican la configuración.

![chlimage_1-266](assets/chlimage_1-266.png)

* **Título**

   (Requerido) Un título de visualización para la configuración.
Por ejemplo, escriba *Habilitación Comunidad Analytics*

* **Nombre**

   (Opcional) Si no se especifica, el nombre pasará de forma predeterminada a un nombre de nodo válido derivado del título.
For example, enter *communities*

* **Plantilla**

   Seleccione `Adobe Analytics Configuration`

* Seleccione **Crear**

   * Inicia la página de configuración y abre `Analytics Settings` el cuadro de diálogo

### Cuadro de diálogo Configuración de Analytics {#analytics-settings-dialog}

La creación inicial de una nueva configuración de Analytics da como resultado la visualización de la configuración y un nuevo cuadro de diálogo para la entrada de la Configuración de Analytics. Este cuadro de diálogo requiere la información [](#prerequisites) previa de la cuenta obtenida del representante de la cuenta.

![chlimage_1-267](assets/chlimage_1-267.png)

* **Empresa**

   compañía asociada a la cuenta de Analytics de Adobe.

* **Nombre de usuario**

   Nombre de usuario de inicio de sesión del usuario autorizado para administrar la cuenta de Analytics.

* **Contraseña**

   La contraseña de inicio de sesión del usuario autorizado.

* **Centro de datos**

   Seleccione el centro de datos de Analytics que aloja el grupo de informes.

* **No añadir etiqueta de seguimiento a la página**

   Déjelo como predeterminado (no seleccionado).

* **Utilizar AppMeasurement**

   Déjelo como predeterminado (no seleccionado).

* **No importar las impresiones de la página cada noche (Author)**

   Déjelo como predeterminado (no seleccionado).

* **No importar las impresiones de la página cada noche (Publish)**

   Déjelo como predeterminado (no seleccionado).

Para guardar la configuración:

* Seleccione **Conectar a Analytics**

   * Si no es exitoso,

      * Verifique que las entradas no contengan espacios de interlineado.
      * Pruebe con otro centro de datos.
      * Póngase en contacto con su representante de cuentas.

* Seleccione **Aceptar**.

   ![chlimage_1-268](assets/chlimage_1-268.png)

### Crear módulo {#create-framework}

Después de configurar correctamente la conexión básica a Adobe Analytics, es necesario crear o editar un marco para el sitio de la comunidad. El propósito de la estructura es asignar variables de la función Comunidades (AEM) a variables de Analytics (grupo de informes).

* Seleccione `[+]` el icono junto a **[!UICONTROL Marcos]** disponibles para crear un nuevo marco

   ![chlimage_1-269](assets/chlimage_1-269.png)

* **Título**

   (Requerido) Un título de visualización para el marcoPor ejemplo, introduzca *Habilitación de marco* de comunidad.

* **Nombre**

   (Opcional) Si no se especifica, el nombre pasará de forma predeterminada a un nombre de nodo válido derivado del título.
For example, enter *communities*.

* *Plantilla*

   Seleccione `Adobe Analytics Framework`.

* Seleccione **Crear**.

La creación de Analytics Framework abre el marco para la configuración.

## Configuración de AEM Analytics Framework {#aem-analytics-framework-configuration}

El propósito de la estructura es asignar variables de AEM a variables de Analytics (eVars y eventos). Las variables de Analytics disponibles para la asignación se [definen en el grupo](#adobe-analytics-report-suite-for-video-reporting)de informes.

![chlimage_1-270](assets/chlimage_1-270.png)

### Seleccionar grupo de informes {#select-report-suite}

Seleccione el grupo de informes configurado para el sistema de informes de vídeo.

Si un grupo de informes aún no se ha creado o no se ha configurado correctamente, consulte la sección anterior:
[Grupo de informes de Adobe Analytics para Sistema de informes de vídeo](#adobe-analytics-report-suite-for-video-reporting)

La barra de tareas no es necesaria y puede minimizarse para que no obstruya el acceso a la configuración de los grupos de informes.

#### Cuadro de diálogo Grupos de informes antes y después de seleccionar &#39;Añadir elemento&#39; {#report-suites-dialog-before-and-after-selecting-add-item}

![chlimage_1-271](assets/chlimage_1-271.png)

1. Seleccione **Añadir elemento +**.

   Aparecen dos cuadros desplegables.

1. Elija un `Report suite.`

   Los grupos de informes asociados con la cuenta de Compañía están disponibles para su selección.

1. Seleccione **Sí** en el cuadro de diálogo que se abre:

   ```
   Load default server settings?
    Do you want to load the default server settings and overwrite current values in the Server section?
   ```

1. Elija un `Run Mode`.

1. Seleccione **Publicar**.

![chlimage_1-272](assets/chlimage_1-272.png)

El servicio y el marco de trabajo de Analytics cloud ya están completos. Las asignaciones se definirán una vez que se haya creado un sitio de comunidad con este servicio de Analytics habilitado.

## Habilitar Analytics para un sitio de comunidad {#enable-analytics-for-a-community-site}

### Habilitar para nuevo sitio de comunidad {#enable-for-new-community-site}

Para agregar el servicio en la nube de Analytics al [crear un nuevo sitio](/help/communities/sites-console.md)de comunidad:

* En el paso 3, en la ficha [](/help/communities/sites-console.md#analytics)ANALYTICS:
   * Active la casilla de verificación **Habilitar Analytics** .
   * Seleccione el marco en el cuadro desplegable.

* Opcionalmente, vuelva a la configuración del marco de trabajo de Analytics para ajustar las asignaciones de variables.

### Habilitar para sitio de comunidad existente {#enable-for-existing-community-site}

Para agregar el servicio en la nube de Analytics a un sitio [de comunidad](/help/communities/sites-console.md#modifying-site-properties)existente:

* Vaya a la consola **Comunidades > Sitios** .
* Seleccione el icono Editar sitio del sitio de la comunidad.
* Seleccione la CONFIGURACIÓN.
* En la sección Analytics:
   * Active la casilla de verificación **Habilitar Analytics** .
   * Elija el marco en el cuadro desplegable.

* Opcionalmente, vuelva a la configuración del marco de trabajo de Analytics para ajustar las asignaciones de variables.

### Habilitar para sitios personalizados {#enable-for-customized-sites}

Para que el seguimiento y la importación de Analytics funcionen correctamente en un sitio de comunidad, debe haber un elemento de página con los atributos class y href `scf-js-site-title` . Solo debe existir un elemento de este tipo en la página, como lo hace en una secuencia de comandos `sitepage.hbs` sin modificar para un sitio de comunidad. El valor de `siteUrl` se extrae y se envía a Adobe Analytics como ruta *del* sitio.

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

Para un sitio **de comunidad** personalizado que superponga la `sitepage.hbs` secuencia de comandos, asegúrese de que el elemento está presente. La `siteUrl` variable se configurará cuando se procese en el servidor antes de servir en el cliente.

Para un sitio **AEM** genérico que incluya componentes de Communities pero no se cree con el asistente [de creación de](/help/communities/sites-console.md)sitio, es necesario agregar el elemento . El valor de href debe ser la ruta al sitio. Por ejemplo: si la ruta del sitio es `/content/my/company/en`, utilice:

```xml
<div
    class="navbar-brand scf-js-site-title"
    href="/content/my/company/en.html"
    style="visibility: hidden;"
>
</div>
```

## Funciones de Analytics para Comunidades {#analytics-for-communities-features}

Analytics se utiliza automáticamente para varias funciones de Communities.

La configuración [](/help/sites-deploying/configuring-osgi.md)OSGi del entorno autor `AEM Communities Analytics Component Configuration`, proporciona una lista de los componentes instrumentados para Analytics. La asignación automática de variables viene determinada por los componentes enumerados.

Si se crean nuevos componentes personalizados instrumentados para Analytics, deben agregarse a esta lista de componentes configurados.

### Configuración de componentes {#component-configuration}

![chlimage_1-273](assets/chlimage_1-273.png)

>[!NOTE]
>
>Los componentes de historial se utilizan para implementar la función de blog.


### Asignación de Analytics a variables de AEM {#mapped-analytics-to-aem-variables}

Una vez guardado el sitio de la comunidad con Analytics habilitado y seleccionado el marco de configuración de la nube, las variables de AEM se asignarán automáticamente a las eVars y eventos de Analytics que comiencen por evar1 y evento1, respectivamente, e incrementarán en 1.

Si se utiliza un grupo de informes existente que asignó cualquiera de las variables de evar1 a evar11 y evento1 a evento7, será necesario [reasignar las variables](#modifying-analytics-variable-mapping) de AEM y restaurar la asignación original.

A continuación se muestra un ejemplo de asignaciones predeterminadas después de seguir el tutorial [de](/help/communities/getting-started-enablement.md)introducción:

![chlimage_1-274](assets/chlimage_1-274.png)

#### Mapa de eVars enviadas con cada evento {#map-of-evars-sent-with-each-event}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Tipo de recurso<br /> de habilitación<br /></strong></td>
   <td><strong>Título del sitio<br /></strong></td>
   <td><strong>Tipo de función<br /></strong></td>
   <td><strong>Título del grupo<br /></strong></td>
   <td><strong>Group<br /> Path</strong></td>
   <td><strong>Tipo UGC<br /></strong></td>
   <td><strong>Título UGC<br /></strong></td>
   <td><strong>Usuario<br /> (miembro)</strong></td>
   <td><strong>Ruta UGC<br /></strong></td>
   <td><strong>Ruta del sitio<br /></strong></td>
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
   <td><strong>Reproducción de recursos de evento1<br /></strong></td>
   <td><em>(una)</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>-</em></td>
   <td><em>i)</em></td>
   <td><em>-</em></td>
  </tr>
  <tr>
   <td><strong>evento2<br /> SCFView</strong></td>
   <td><em>(una)</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>evento3<br /> SCFCreate (Post)</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>evento4<br /> SCFFollow</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>evento5<br /> SCFVoteUp</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>evento6<br /> SCFVoteDown</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
  <tr>
   <td><strong>evento7<br /> SCFRate</strong></td>
   <td><em>-</em></td>
   <td><em>b)</em></td>
   <td><em>c)</em></td>
   <td><em>(d)</em></td>
   <td><em>(e)</em></td>
   <td><em>(f)</em></td>
   <td><em>(g)</em></td>
   <td><em>(h)</em></td>
   <td><em>i)</em></td>
   <td><em>j)</em></td>
  </tr>
 </tbody>
</table>

**Ejemplos de valores de eVar:**

* *[Tipo](https://www.iana.org/assignments/media-types)*MIME: vídeo/mp4
* *[título](/help/communities/sites-console.md#step13asitetemplate)*del sitio de la comunidad: Geometrixx Communities
* *[nombre](/help/communities/functions.md)*de función de comunidad: Foro
* *[nombre](/help/communities/creating-groups.md#creating-a-new-group)*del grupo de comunidad: Senderismo
* *ruta al contenido* del grupo de comunidad: `/content/sites/<site name>/en/groups/hiking`
* *[RecursoTipo](/help/communities/essentials.md)*del componente UGC:`social/forum/components/hbs/topic`
* *Título* del componente UGC: Senderismo por temas
* *login (autorizableId)*: `aaron.mcdonald@mailinator.com`
* *Ruta de SRP a UGC*: `/content/usergenerated/asi/.../forum/jmtz-topic3`
o 
*ruta del componente a seguir*: `/content/sites/<site name>/en/jcr:content/content/primary/forum`

* *ruta al contenido* del sitio de la comunidad: `/content/sites/<site name>/en`

### Modificación de la asignación de variables de Analytics {#modifying-analytics-variable-mapping}

La asignación de eVars y eventos de Analytics a variables de AEM es visible desde la configuración del marco de trabajo después de habilitar Analytics para un sitio de comunidad.

Después de habilitar Analytics y antes de publicar el sitio de la comunidad, la asignación se puede modificar en el marco arrastrando la eVar o el evento de Analytics deseados desde el carril izquierdo y soltándolos en la fila pertinente de la tabla de asignación.

Para evitar las asignaciones de duplicados, asegúrese de eliminar la eVar o el evento de Analytics reemplazados de la fila pasando el ratón sobre ella y seleccionando la &quot;X&quot; que aparece a la derecha del elemento de variable de Analytics.

Si las eVars y los eventos de Communities sobrescriben las asignaciones que existían previamente en el grupo de informes, asigne las variables de AEM para las funciones de Communities a otras eVars o eventos de Analytics y restaure las asignaciones originales.

>[!CAUTION]
>
>Es importante reasignar antes de que el sitio de la comunidad se [publique](#publishing-the-community-site) con Analytics habilitado, de lo contrario se corre el riesgo de perder datos.

#### Ejemplo de paso 1: Arrastrar Analytics evar14 a la tabla de asignación {#example-step-dragging-analytics-evar-into-mapping-table}

![chlimage_1-275](assets/chlimage_1-275.png)

#### Ejemplo de paso 2: Seleccionar &#39;x&#39; para eliminar evar11 reemplazada {#example-step-selecting-x-to-remove-replaced-evar}

![chlimage_1-276](assets/chlimage_1-276.png)

#### Ejemplo del paso 3: AEM var eventdata.siteId reasignado a Analytics evar14 {#example-step-aem-var-eventdata-siteid-remapped-to-analytics-evar}

![chlimage_1-277](assets/chlimage_1-277.png)

## Publicación del sitio de la comunidad {#publishing-the-community-site}

### Verificar la asignación de Analytics a la variable AEM {#verify-analytics-to-aem-variable-mapping}

Es aconsejable verificar la asignación de variables antes de publicar el sitio de la comunidad, que también publica el servicio en la nube y el marco de trabajo de Analytics.

Consulte las secciones:

* [Asignación de Analytics a variables de AEM](#mapped-analytics-to-aem-variables)
* [Modificación de la asignación de variables de Analytics](#modifying-analytics-variable-mapping)

>[!CAUTION]
>
>**Si utiliza un grupo de informes existente que ya utiliza variables dentro de**
>
>* **`evar1`** hasta **`evar11`**
   >
   >
* **`event1`** hasta **`event7`**
>
>
**A continuación, antes de publicar el sitio de la comunidad,** es importante restaurar la asignación preexistente y mover las variables AEM de Communities que se asignaron automáticamente (cuando se habilitó Analytics para el sitio de la comunidad) a otras variables de Analytics. Esta reasignación debe ser coherente en todos los componentes de Comunidades.
>
>Si no lo hace, puede producirse una pérdida de datos irrecuperable.

### Editor principal {#primary-publisher}

Cuando la implementación elegida es un conjunto de servidores [de](/help/communities/topologies.md#tarmk-publish-farm)publicación, se debe identificar una instancia de publicación de AEM como el editor principal para sondear Adobe Analytics para que los datos del informe se escriban en [SRP](/help/communities/working-with-srp.md).

De forma predeterminada, la configuración de `AEM Communities Publisher Configuration` OSGi identifica su instancia de publicación como el publicador principal, de modo que todas las instancias de publicación de un conjunto de servidores de publicación se identificarían como principales.

Por lo tanto, es necesario editar la configuración en todas las instancias de publicación secundarias para anular la selección de la casilla de verificación Publicador **** principal.

Para obtener instrucciones específicas, consulte la sección del editor principal de [Implementación de comunidades](/help/communities/deploy-communities.md#primary-publisher).

>[!CAUTION]
>
>Es importante que el editor principal esté configurado para evitar que las encuestas se realicen desde varias instancias de publicación.

### Replicar la clave de cifrado {#replicate-the-crypto-key}

Las credenciales de Adobe Analytics están cifradas. Para facilitar la replicación o transmisión de credenciales de análisis cifradas entre creadores y editores, todas las instancias de AEM deben compartir la misma clave de cifrado principal.

Para ello, siga las instrucciones de [Replicar la clave](/help/communities/deploy-communities.md#replicate-the-crypto-key)de cifrado.

### Publicar sitio de comunidad y Cloud Service de Analytics {#publish-community-site-and-analytics-cloud-service}

Una vez que el servicio en la nube de Analytics se ha habilitado para un sitio de la comunidad y, si es necesario, se ha ajustado [la](#mapped-analytics-to-aem-variables)asignación de Analytics a las variables de AEM, es necesario replicar la configuración en el entorno de publicación [(re)publicando el sitio](/help/communities/sites-console.md#publishing-the-site)de la comunidad.

## Obtención de informes de Analytics {#obtaining-reports-from-analytics}

### Administración de informes {#report-management}

La configuración [](/help/sites-deploying/configuring-osgi.md)OSGi del autor y del editor principal, `AEM Communities Analytics Report Management`, se utiliza para la consulta de Analytics.

En el autor, las consultas son para los informes en tiempo real.

En el publicador principal, las consultas se utilizan para proporcionar información como preparación para la importación de datos analíticos del importador de informes.

El intervalo de consulta predeterminado es de 10 segundos.

### Importador de informes {#report-importer}

Una vez que se ha publicado un sitio de comunidad habilitado para Analytics, la configuración [](/help/sites-deploying/configuring-osgi.md)OSGi del editor principal, `AEM Communities Analytics Report Importer`, puede configurarse para establecer el intervalo de sondeo predeterminado para aquellas configuraciones que no estén configuradas individualmente en CRXDE.

El intervalo de sondeo controla la frecuencia de las solicitudes a Adobe Analytics para que los datos se extraigan y guarden en [SRP](/help/communities/working-with-srp.md).

Cuando los datos pueden clasificarse como &quot;grandes datos&quot;, las encuestas más frecuentes pueden causar una gran carga en el sitio de la comunidad.

El intervalo **predeterminado de** importación de encuestas está establecido en 12 horas.

![chlimage_1-278](assets/chlimage_1-278.png)

### Personalización del informe de componentes {#component-report-customization}

Actualmente, para personalizar las métricas de seguimiento, los nodos se crean en el repositorio que define los períodos de tiempo para los cuales se genera un informe sobre esa métrica.

El tema del foro es actualmente el único ejemplo de esta personalización:

* En el editor principal, inicie sesión con privilegios de administrador.
* Vaya a [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Por ejemplo, [https://localhost:4503/crx/de](https://localhost:4503/crx/de).

* En el nodo jcr:content de la raíz del idioma (por ejemplo, `/content/sites/engage/en/jcr:content),`navegue al componente configurado para Analytics sistema de informes.
Por ejemplo, **`analytics/reportConfigs/social_forum_components_hbs_topic`**

* Observe los períodos de tiempo creados:

   * `last30Days`
   * `last90Days`
   * `thisYear`

* Observe el `total`nodo.

   * Si se modifica la **`interval`** propiedad, se anula el intervalo del importador de informes.
   * El valor se expresa en segundos y se establece en 4 horas (14.400 segundos).

![chlimage_1-279](assets/chlimage_1-279.png)

## Administrar datos de usuario en Analytics {#manage-user-data-in-analytics}

Adobe Analytics proporciona API que le permiten acceder, exportar y eliminar datos de usuario. Para obtener más información, consulte [Enviar solicitudes](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)de acceso y eliminación.

## Medios {#resources}

* Adobe Experience Cloud: [Ayuda y referencia de Analytics](https://docs.adobe.com/content/help/en/analytics/landing/home.html)
* AEM: [Integrating with Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* AEM: [Analytics con proveedores externos](/help/sites-administering/external-providers.md)
