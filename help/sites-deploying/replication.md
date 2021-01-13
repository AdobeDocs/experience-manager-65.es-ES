---
title: Replicación
seo-title: Replicación
description: Obtenga información sobre cómo configurar y monitorear los agentes de replicación en AEM.
seo-description: Obtenga información sobre cómo configurar y monitorear los agentes de replicación en AEM.
uuid: 6c0bc2fe-523a-401f-8d93-e5795f2e88b9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 3cae081e-93e3-4317-b307-1316283c307a
docset: aem65
translation-type: tm+mt
source-git-commit: 17d70e532ab5d825dd4dc0ea4c891c5b7cb8d345
workflow-type: tm+mt
source-wordcount: '3443'
ht-degree: 3%

---


# Replicación{#replication}

Los agentes de replicación son centrales para Adobe Experience Manager (AEM) como mecanismo utilizado para:

* [Publique (active)](/help/sites-authoring/publishing-pages.md#activatingcontent) contenido de un autor en un entorno de publicación.
* Borre contenido explícitamente de la caché de Dispatcher.
* Devolver los datos introducidos por el usuario (por ejemplo, los datos introducidos en el formulario) desde el entorno de publicación al entorno de creación (bajo el control del entorno de creación).

Las solicitudes se [ponen en cola](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) al agente correspondiente para su procesamiento.

>[!NOTE]
>
>Los datos de usuario (usuarios, grupos de usuarios y perfiles de usuario) no se replican entre instancias de autor y publicación.
>
>Para varias instancias de publicación, los datos de usuario se distribuyen en Sling cuando [Sincronización de usuario](/help/sites-administering/sync.md) está habilitada.

## Replicar desde el autor para publicar {#replicating-from-author-to-publish}

La replicación, en una instancia de publicación o un despachante, se realiza en varios pasos:

* el autor solicita que se publique determinado contenido (se active); esto puede iniciarse mediante una solicitud manual o mediante déclencheur automáticos preconfigurados.
* la solicitud se pasa al agente de replicación predeterminado apropiado; un entorno puede tener varios agentes predeterminados que siempre se seleccionarán para dichas acciones.
* el agente de replicación &quot;empaqueta&quot; el contenido y lo coloca en la cola de replicación.
* en la ficha Sitios web, se establece el [indicador de estado de color](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) para las páginas individuales.
* el contenido se levanta de la cola y se transporta al entorno de publicación mediante el protocolo configurado; normalmente es HTTP.
* un servlet del entorno de publicación recibe la solicitud y publica el contenido recibido; el servlet predeterminado es `https://localhost:4503/bin/receive`.

* se pueden configurar varios entornos de creación y publicación.

![chlimage_1-21](assets/chlimage_1-21.png)

### Replicando desde Publicar en Autor {#replicating-from-publish-to-author}

Algunas funciones permiten a los usuarios introducir datos en una instancia de publicación.

En algunos casos, se necesita un tipo de replicación conocido como replicación inversa para devolver estos datos al entorno de creación desde donde se redistribuye a otros entornos de publicación. Debido a consideraciones de seguridad, cualquier tráfico desde la publicación hasta el entorno del autor debe estar estrictamente controlado.

La replicación inversa utiliza un agente en el entorno de publicación que hace referencia al entorno del autor. Este agente coloca los datos en una bandeja de salida. Esta bandeja de salida se compara con los oyentes de replicación en el entorno de creación. Los oyentes sondean las bandejas de salida para recopilar los datos introducidos y luego distribuirlos según sea necesario. Esto garantiza que el entorno de creación controle todo el tráfico.

En otros casos, como en el caso de las funciones de Comunidades (por ejemplo, foros, blogs, comentarios y revisiones), la cantidad de contenido generado por el usuario (UGC) que se introduce en el entorno de publicación resulta difícil de sincronizar de forma eficaz en AEM instancias que utilizan la replicación.

AEM [Communities](/help/communities/overview.md) nunca utiliza la replicación para UGC. En su lugar, la implementación para Comunidades requiere un almacén común para UGC (consulte [Almacenamiento de contenido de la comunidad](/help/communities/working-with-srp.md)).

### Replicación: lista para usar {#replication-out-of-the-box}

El sitio Web-minorista que se incluye en una instalación estándar de AEM puede utilizarse para ilustrar la replicación.

Para seguir este ejemplo y utilizar los agentes de replicación predeterminados debe [instalar AEM](/help/sites-deploying/deploy.md) con:

* el entorno de creación en el puerto `4502`
* el entorno de publicación en el puerto `4503`

>[!NOTE]
>
>Habilitado de manera predeterminada :
>
>* Agentes del autor: Agente predeterminado (publicación)
>
>
Efectivamente deshabilitada de forma predeterminada (a partir de AEM 6.1):
>
>* Agentes del autor: Agente de replicación inversa (publish_reverse)
>* Agentes en la publicación: Replicación inversa (outbox)

>
>
Para comprobar el estado del agente o de la cola, utilice la consola **Tools**.
>Consulte [Monitoreo de los agentes de replicación](#monitoring-your-replication-agents).

#### Replicación (Autor para publicar) {#replication-author-to-publish}

1. Vaya a la página de asistencia técnica del entorno de creación.
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. Edite la página para agregar texto nuevo.
1. **Active** Página para publicar los cambios.
1. Abra la página de asistencia técnica en el entorno de publicación:
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. Ahora puede ver los cambios introducidos en el autor.

Esta replicación se mide desde el entorno de creación mediante:

* **Agente predeterminado (publicación)**
Este agente replica contenido en la instancia de publicación predeterminada.
Se puede acceder a los detalles de este proceso (configuración y registros) desde la consola Herramientas del entorno de creación; o bien:

   `https://localhost:4502/etc/replication/agents.author/publish.html`.

#### Agentes de replicación: listos para usar {#replication-agents-out-of-the-box}

Los siguientes agentes están disponibles en una instalación AEM estándar:

* [Agente ](#replication-author-to-publish)
predeterminadoSe utiliza para replicar desde el autor hasta la publicación.

* Dispatcher Flush
Se utiliza para administrar la caché de Dispatcher. Consulte [Invalidación de la caché del despachante desde el Entorno de creación](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) y [Invalidación de la caché del despachante desde una instancia de publicación](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) para obtener más información.

* [Replicación inversaSe utiliza para replicar desde la publicación hasta el autor. ](#reverse-replication-publish-to-author)
La replicación inversa no se utiliza para las funciones de Comunidades, como foros, blogs y comentarios. Se desactiva de forma efectiva, ya que la bandeja de salida no está habilitada. El uso de la replicación inversa requeriría una configuración personalizada.

* Agente estático
Es un &quot;Agente que almacena una representación estática de un nodo en el sistema de archivos&quot;.
Por ejemplo, con la configuración predeterminada, las páginas de contenido y los recursos de presa se almacenan en `/tmp`, ya sea como HTML o como el formato de recurso adecuado. Consulte las fichas `Settings` y `Rules` para ver la configuración.
Esto se solicitó para que, cuando la página se solicite directamente del servidor de aplicaciones, se pueda ver el contenido. Se trata de un agente especializado y (probablemente) no será necesario en la mayoría de los casos.

## Agentes de replicación: Parámetros de configuración {#replication-agents-configuration-parameters}

Al configurar un agente de replicación desde la consola Herramientas, hay cuatro fichas disponibles en el cuadro de diálogo:

### Configuración {#settings}

* **Nombre**

   Un nombre único para el agente de replicación.

* **Descripción**

   Descripción del propósito que servirá este agente de replicación.

* **Activado**

   Indica si el agente de replicación está habilitado actualmente.

   Cuando el agente esté **habilitado**, la cola se mostrará como:

   * **** Se activa cuando se procesan elementos.
   * **** Indica si la cola está vacía.
   * **** Bloqueado cuando los elementos están en la cola, pero no se pueden procesar; por ejemplo, cuando la cola de recepción está deshabilitada.

* **Tipo de serialización**

   Tipo de serialización:

   * **Predeterminado**: Se establece si el agente se va a seleccionar automáticamente.
   * **Dispatcher Flush**: Seleccione esta opción si el agente se va a utilizar para vaciar la caché del despachante.

* **Intervalo entre reintentos**

   El retraso (tiempo de espera en milisegundos) entre dos reintentos, en caso de que se produzca un problema.

   Valor predeterminado: `60000`

* **ID de usuario agente**

   Según el entorno, el agente utilizará esta cuenta de usuario para:

   * recopilar y empaquetar el contenido del entorno de creación
   * crear y escribir el contenido en el entorno de publicación

   Deje este campo vacío para utilizar la cuenta de usuario del sistema (la cuenta definida en sling como usuario administrador; de forma predeterminada, es `admin`).

   >[!CAUTION]
   >
   >Para un agente en el entorno de creación, esta cuenta *debe* tener acceso de lectura a todas las rutas que desee replicar.

   >[!CAUTION]
   >
   >Para un agente en el entorno de publicación, esta cuenta *debe* tener el acceso de creación/escritura necesario para replicar el contenido.

   >[!NOTE]
   >
   >Se puede utilizar como mecanismo para seleccionar contenido específico para la replicación.

* **Nivel de registro**

   Especifica el nivel de detalle que se utilizará para los mensajes de registro.

   * `Error`:: solo se registrarán errores
   * `Info`:: se registrarán errores, advertencias y otros mensajes informativos
   * `Debug`:: se utilizará un alto nivel de detalle en los mensajes, principalmente con fines de depuración

   Valor predeterminado: `Info`

* **Utilizar para replicación inversa**

   Indica si este agente se utilizará para la replicación inversa; devuelve los datos introducidos por el usuario desde el entorno de publicación al autor.

* **Actualización de alias**

   Al seleccionar esta opción, se habilitan las solicitudes de invalidación de alias o de ruta de vanidad en Dispatcher. Consulte también [Configuración de un agente de vaciado de despachante](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### Transporte {#transport}

* **URI**

   Esto especifica el servlet receptor en la ubicación del destinatario. En concreto, puede especificar aquí el nombre de host (o alias) y la ruta de contexto a la instancia de destinatario.

   Por ejemplo:

   * Un agente predeterminado puede replicarse en `https://localhost:4503/bin/receive`
   * Un agente Dispatcher Flush puede replicarse en `https://localhost:8000/dispatcher/invalidate.cache`

   El protocolo especificado aquí (HTTP o HTTPS) determinará el método de transporte.

   En el caso de los agentes Dispatcher Flush, la propiedad URI solo se utiliza si se utilizan entradas virtualhost basadas en rutas de acceso para diferenciar entre granjas, se utiliza este campo para destinatario de la granja de servidores para invalidar. Por ejemplo, la granja #1 tiene un host virtual de `www.mysite.com/path1/*` y la granja #2 tiene un host virtual de `www.mysite.com/path2/*`. Puede utilizar una dirección URL de `/path1/invalidate.cache` para el destinatario del primer conjunto de servidores y `/path2/invalidate.cache` para el destinatario del segundo conjunto de servidores.

* **Usuario**

   Nombre de usuario de la cuenta que se va a utilizar para acceder al destinatario.

* **Contraseña**

   Contraseña de la cuenta que se va a utilizar para acceder al destinatario.

* **Dominio NTLM**

   Dominio para autenticación NTML.

* **Host NTLM**

   Host para autenticación NTML.

* **Habilitar SSL relajado**

   Active esta opción si desea que se acepten certificados SSL autocertificados.

* **Permitir certificados caducados**

   Active esta opción si desea que se acepten certificados SSL caducados.

#### Proxy {#proxy}

Solo se necesita la siguiente configuración si se necesita un proxy:

* **Host de proxy**

   Nombre de host del proxy utilizado para el transporte.

* **Puerto de proxy**

   Puerto del proxy.

* **Usuario de proxy**

   Nombre de usuario de la cuenta que se va a utilizar.

* **Contraseña de proxy**

   Contraseña de la cuenta que se va a utilizar.

* **Dominio NTLM de proxy**

   Dominio NTLM proxy.

* **Host NTLM de proxy**

   Dominio NTLM proxy.

#### Ampliado {#extended}

* **Interfaz**

   Aquí puede definir la interfaz de socket a la que desea enlazar.

   Esto establece la dirección local que se utilizará al crear conexiones. Si no se establece, se utilizará la dirección predeterminada. Esto resulta útil para especificar la interfaz que se va a utilizar en sistemas de varios hogares o agrupados.

* **Método HTTP**

   El método HTTP que se va a utilizar.

   Para un agente Dispatcher Flush, esto es casi siempre GET y no debe cambiarse (el POST sería otro valor posible).

* **Encabezados HTTP**

   Estos se utilizan para los agentes de Dispatcher Flush y especifican los elementos que deben vaciarse.

   Para un agente Dispatcher Flush, no es necesario cambiar las tres entradas estándar:

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

   Estos se utilizan, según proceda, para indicar la acción que debe utilizarse al vaciar el asa o la ruta. Los subparámetros son dinámicos:

   * `{action}` indica una acción de replicación

   * `{path}` indica una ruta

   Se sustituyen por la ruta/acción pertinente a la solicitud y, por lo tanto, no necesitan estar &quot;codificados&quot;:

   >[!NOTE]
   >
   >Si ha instalado AEM en un contexto que no sea el predeterminado recomendado, deberá registrar el contexto en los encabezados HTTP. Por ejemplo:
   >`CQ-Handle:/<*yourContext*>{path}`

* **Cerrar conexión**

   Active esta opción para cerrar la conexión después de cada solicitud.

* **Tiempo de espera de conexión**

   Tiempo de espera (en milisegundos) que se debe aplicar al intentar establecer una conexión.

* **Tiempo de espera de socket**

   Tiempo de espera (en milisegundos) que se debe aplicar al esperar tráfico después de establecer una conexión.

* **Versión del protocolo**

   Versión del protocolo; por ejemplo `1.0` para HTTP/1.0.

#### Desencadenadores {#triggers}

Estas configuraciones se utilizan para definir déclencheur para la replicación automatizada:

* **Omitir predeterminado**

   Si se selecciona, el agente se excluye de la replicación predeterminada; esto significa que no se utilizará si un autor de contenido emite una acción de replicación.

* **En la modificación**

   Aquí se activará automáticamente una replicación de este agente cuando se modifique una página. Esto se utiliza principalmente para agentes Dispatcher Flush, pero también para replicación inversa.

* **En distribución**

   Si se selecciona, el agente replicará automáticamente cualquier contenido marcado para distribución cuando se modifique.

* **Tiempo de activación/desactivación alcanzado**

   Esto déclencheur la replicación automática (para activar o desactivar una página según corresponda) cuando se produzcan las veces u horas de inactividad definidas para una página. Esto se utiliza principalmente para agentes Dispatcher Flush.

* **En estado de recepción**

   Si se selecciona, el agente realizará una replicación en cadena cada vez que reciba eventos de replicación.

* **No hay actualización de estado**

   Cuando se selecciona, el agente no fuerza una actualización del estado de replicación.

* **No hay asignación de versiones**

   Cuando se selecciona, el agente no fuerza el control de versiones de las páginas activadas.

## Configuración de los agentes de replicación {#configuring-your-replication-agents}

Para obtener información sobre la conexión de agentes de replicación a la instancia de publicación mediante MSSL, consulte [Replicación mediante SSL mutuo](/help/sites-deploying/mssl-replication.md).

### Configuración de los agentes de replicación desde el Entorno de creación {#configuring-your-replication-agents-from-the-author-environment}

Desde la ficha Herramientas del entorno de creación puede configurar los agentes de replicación que residen en el entorno de creación (**Agentes en el autor**) o en el entorno de publicación (**Agentes en la publicación**). Los siguientes procedimientos ilustran la configuración de un agente para el entorno de creación, pero se pueden utilizar para ambos.

>[!NOTE]
>
>Cuando un distribuidor gestiona solicitudes HTTP para instancias de autor o publicación, la solicitud HTTP del agente de replicación debe incluir el encabezado PATH. Además del siguiente procedimiento, debe agregar el encabezado PATH a la lista de despachantes de encabezados de cliente. (Consulte [/clientheaders (Encabezados de cliente)](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders). [](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders)


1. Acceda a la ficha **Herramientas** en AEM.
1. Haga clic en **Replicación** (panel izquierdo para abrir la carpeta).
1. Haga clic con el doble **Agentes en el autor** (a la izquierda o al panel derecho).
1. Haga clic en el nombre del agente correspondiente (que es un vínculo) para mostrar información detallada sobre ese agente.
1. Haga clic en **Editar** para abrir el cuadro de diálogo de configuración:

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. Los valores proporcionados deben ser suficientes para una instalación predeterminada. Si realiza cambios, haga clic en **Aceptar** para guardarlos (consulte [Agentes de replicación - Parámetros de configuración](#replication-agents-configuration-parameters) para obtener más detalles de los parámetros individuales).

>[!NOTE]
>
>Una instalación estándar de AEM especifica `admin` como usuario para las credenciales de transporte dentro de los agentes de replicación predeterminados.
>
>Esto debe cambiarse a una cuenta de usuario de replicación específica del sitio con privilegios para replicar las rutas requeridas.

### Configuración de la Replicación Inversa {#configuring-reverse-replication}

La replicación inversa se utiliza para volver a generar contenido de usuario en una instancia de publicación en una instancia de autor. Esto se utiliza generalmente para funciones como encuestas y formularios de registro.

Por motivos de seguridad, la mayoría de las topologías de red no permiten conexiones *desde* la &quot;Zona desmilitarizada&quot; (una subred que expone los servicios externos a una red no confiable, como Internet).

Como el entorno de publicación suele estar en DMZ, para recuperar el contenido en el entorno de creación, la conexión debe iniciarse desde la instancia de creación. Esto se lleva a cabo con:

* una *bandeja de salida* en el entorno de publicación donde se coloca el contenido.
* un agente (publicación) en el entorno de creación que sondea periódicamente la bandeja de salida para obtener contenido nuevo.

>[!NOTE]
>
>Para AEM [Comunidades](/help/communities/overview.md), la replicación no se utiliza para el contenido generado por el usuario en una instancia de publicación. Consulte [Almacenamiento de contenido de comunidad](/help/communities/working-with-srp.md).

Para ello, necesita:

**Agente de replicación inversa en el** entorno de creaciónActúa como componente activo para recopilar información de la bandeja de salida en el entorno de publicación:

Si desea utilizar la replicación inversa, asegúrese de que este agente esté activado.

![chlimage_1-23](assets/chlimage_1-23.png)

**Un agente de replicación inversa en el entorno de publicación (una bandeja de salida)** Este es el elemento pasivo ya que actúa como una &quot;bandeja de salida&quot;. La entrada del usuario se coloca aquí, desde donde la recopila el agente en el entorno del autor.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### Configuración de la replicación para varias instancias de publicación {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>Solo se replica el contenido: los datos de usuario no (usuarios, grupos de usuarios y perfiles de usuarios).
>
>Para sincronizar datos de usuario en varias instancias de publicación, habilite [Sincronización de usuario](/help/sites-administering/sync.md).

Tras la instalación, ya se ha configurado un agente predeterminado para la replicación de contenido en una instancia de publicación que se ejecuta en el puerto 4503 del host local.

Para configurar la replicación de contenido para una instancia de publicación adicional, debe crear y configurar un nuevo agente de replicación:

1. Abra la ficha **Herramientas** en AEM.
1. Seleccione **Replicación**, luego **Agentes en el autor** en el panel izquierdo.
1. Seleccionar **Nuevo...**.
1. Configure los **Título** y **Nombre**, luego seleccione **Agente de replicación**.
1. Haga clic en **Crear** para crear el nuevo agente.
1. Haga clic con el doble en el nuevo elemento del agente para abrir el panel de configuración.
1. Haga clic en **Editar** - se abrirá el cuadro de diálogo **Configuración del agente** - el **Tipo de serialización** ya está definido como Predeterminado, debe seguir siéndolo.

   * En la ficha **Configuración**:

      * Activar **Habilitado**.
      * Especificar una **Descripción**.
      * Establezca el **retraso de reintento** en `60000`.

      * Deje el **Tipo de serialización** como `Default`.
   * En la ficha **Transporte**:

      * Introduzca el URI necesario para la nueva instancia de publicación; por ejemplo,
         `https://localhost:4504/bin/receive`.

      * Introduzca la cuenta de usuario específica del sitio que se utiliza para la replicación.
      * Puede configurar otros parámetros según sea necesario.


1. Haga clic en **Aceptar** para guardar la configuración.

A continuación, puede probar la operación actualizando y publicando una página en el entorno de creación.

Las actualizaciones aparecerán en todas las instancias de publicación que se hayan configurado como se ha indicado anteriormente.

Si tiene algún problema, puede comprobar los registros de la instancia de creación. Según el nivel de detalle requerido, también puede establecer el **Nivel de registro** en `Debug` mediante el cuadro de diálogo **Configuración del agente** como se muestra arriba.

>[!NOTE]
>
>Esto se puede combinar con el uso del [ID de usuario del agente](#agentuserid) para seleccionar diferente contenido para replicar en los entornos de publicación individuales. Para cada entorno de publicación:
>
>1. Configure un agente de replicación para replicar en ese entorno de publicación.
>1. Configurar una cuenta de usuario; con los derechos de acceso necesarios para leer el contenido que se replicará en ese entorno de publicación específico.
>1. Asigne la cuenta de usuario como **ID de usuario del agente** para el agente de replicación.

>



### Configuración de un agente Dispatcher Flush {#configuring-a-dispatcher-flush-agent}

Los agentes predeterminados se incluyen en la instalación. Sin embargo, se necesita cierta configuración y lo mismo se aplica si se está definiendo un nuevo agente:

1. Abra la ficha **Herramientas** en AEM.
1. Haga clic en **Implementación**.
1. Seleccione **Replicación** y luego **Agentes al publicar**.
1. Haga clic con el botón doble en el elemento **Despachado del despachante** para abrir la descripción general.
1. Haga clic en **Editar**. Se abrirá el cuadro de diálogo **Configuración del agente**:

   * En la ficha **Configuración**:

      * Activar **Habilitado**.
      * Especificar una **Descripción**.
      * Deje el **Tipo de serialización** como `Dispatcher Flush` o configúrelo como tal si crea un nuevo agente.

      * (opcional) Seleccione **Actualización de alias** para habilitar las solicitudes de invalidación de alias o de ruta de vanidad en Dispatcher.
   * En la ficha **Transporte**:

      * Introduzca el URI necesario para la nueva instancia de publicación; por ejemplo,
         `https://localhost:80/dispatcher/invalidate.cache`.

      * Introduzca la cuenta de usuario específica del sitio que se utiliza para la replicación.
      * Puede configurar otros parámetros según sea necesario.

   En el caso de los agentes Dispatcher Flush, la propiedad URI solo se utiliza si se utilizan entradas virtualhost basadas en rutas de acceso para diferenciar entre granjas, se utiliza este campo para destinatario de la granja de servidores para invalidar. Por ejemplo, la granja #1 tiene un host virtual de `www.mysite.com/path1/*` y la granja #2 tiene un host virtual de `www.mysite.com/path2/*`. Puede utilizar una dirección URL de `/path1/invalidate.cache` para el destinatario del primer conjunto de servidores y `/path2/invalidate.cache` para el destinatario del segundo conjunto de servidores.

   >[!NOTE]
   >
   >Si ha instalado AEM en un contexto que no sea el predeterminado recomendado, deberá configurar los [encabezados HTTP](#extended) en la ficha **Extended**.

1. Haga clic en **Aceptar** para guardar los cambios.
1. Vuelva a la ficha **Herramientas**, desde aquí puede **Activar** el agente de **vaciado del despachante** (**agentes en la publicación**).

El agente de replicación **Dispatcher Flush** no está activo en el autor. Puede acceder a la misma página en el entorno de publicación mediante el uso del URI equivalente; por ejemplo, `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### Control del acceso a los agentes de replicación {#controlling-access-to-replication-agents}

El acceso a las páginas utilizadas para configurar los agentes de replicación se puede controlar mediante el uso de permisos de página de usuario y/o grupo en el nodo `etc/replication`.

>[!NOTE]
>
>La configuración de estos permisos no afectará a los usuarios que replicen contenido (por ejemplo, desde la consola Sitios web o la opción de la barra de tareas). El marco de replicación no utiliza la &quot;sesión de usuario&quot; del usuario actual para acceder a los agentes de replicación al replicar páginas.

### Configuración de los agentes de replicación desde el CRXDE Lite {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>La creación de agentes de replicación sólo se admite en la ubicación del repositorio `/etc/replication`. Esto es necesario para que las ACL asociadas se gestionen correctamente. La creación de un agente de replicación en otra ubicación del árbol podría generar acceso no autorizado.

Se pueden configurar varios parámetros de los agentes de replicación mediante CRXDE Lite.

Si se desplaza a `/etc/replication` puede ver los tres nodos siguientes:

* `agents.author`
* `agents.publish`
* `treeactivation`

Los dos `agents` contienen información de configuración sobre el entorno apropiado y solo están activos cuando ese entorno se está ejecutando. Por ejemplo, `agents.publish` solo se utilizará en el entorno de publicación. La siguiente captura de pantalla muestra el agente de publicación en el entorno del autor, tal como se incluye con AEM WCM:

![chlimage_1-24](assets/chlimage_1-24.png)

## Monitoreo de los agentes de replicación {#monitoring-your-replication-agents}

Para monitorear un agente de replicación:

1. Acceda a la ficha **Herramientas** en AEM.
1. Haga clic en **Replicación**.
1. Haga clic con el botón doble en el vínculo a los agentes para el entorno correspondiente (a la izquierda o al panel derecho); por ejemplo **Agentes en el autor**.

   La ventana resultante muestra una visión general de todos los agentes de replicación para el entorno de creación, incluidos su destinatario y estado.

1. Haga clic en el nombre del agente correspondiente (que es un vínculo) para mostrar información detallada sobre ese agente:

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   Aquí puede hacer lo siguiente:

   * Ver si el agente está habilitado.
   * Consulte el destinatario de las replicaciones.
   * Ver si la cola de replicación está activa actualmente (habilitada).
   * Ver si hay elementos en la cola.
   * **** Actualizar o  **** Borrar para actualizar la visualización de las entradas de cola; esto le ayuda a ver los elementos entrar y salir de la cola.

   * **Vista** Logs para acceder al registro de cualquier acción realizada por el agente de replicación.
   * **Probar** conexión con la instancia de destinatario.
   * **Forzar** Reintentar en cualquier elemento de la cola si es necesario.

   >[!CAUTION]
   >
   >No utilice el vínculo &quot;Probar conexión&quot; para la bandeja de salida de replicación inversa en una instancia de publicación.
   >
   >
   >Si se realiza una prueba de replicación para una cola de Outbox, todos los elementos que sean más antiguos que la replicación de prueba se volverán a procesar con cada replicación inversa.
   >
   >
   >Si estos elementos ya existen en una cola, se pueden encontrar con la siguiente consulta de JCR XPath y deben eliminarse.
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## Replicación por lotes {#batch-replication}

La replicación por lotes no replica páginas o recursos individuales, pero espera el primer umbral de los dos, según el tiempo o el tamaño, que se activará.

Luego empaqueta todos los elementos de replicación en un paquete, que luego se replica como un solo archivo al editor.

El editor descomprimirá todos los elementos, los guardará y se informará al autor.

### Configuración de la replicación por lotes {#configuring-batch-replication}

1. Ir a `http://serveraddress:serverport/siteadmin`
1. Pulse el icono **[!UICONTROL Herramientas]** en la parte superior de la pantalla
1. Desde el carril de navegación del lado izquierdo, vaya a **[!UICONTROL Replicación - Agentes en Autor]** y haga clic en el doble **[!UICONTROL Agente predeterminado]**.
   * También puede llegar al agente de replicación de publicación predeterminado si ingresa directamente a `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
1. Presione el botón **[!UICONTROL Editar]** sobre la cola de replicación.
1. En la siguiente ventana, vaya a la ficha **[!UICONTROL Lote]**:
   ![replicación de lotes](assets/batchreplication.png)
1. Configure el agente.

### Parámetros {#parameters}

* `[!UICONTROL Enable Batch Mode]` - habilita o deshabilita el modo de replicación por lotes
* `[!UICONTROL Max Wait Time]` - Tiempo de espera máximo hasta que se inicie una solicitud por lotes, en segundos. El valor predeterminado es de 2 segundos.
* `[!UICONTROL Trigger Size]` - Inicios de replicación por lotes cuando este límite de tamaño

## Recursos adicionales {#additional-resources}

Para obtener más información sobre la solución de problemas, puede leer la página [Resolución de problemas de replicación](/help/sites-deploying/troubleshoot-rep.md).