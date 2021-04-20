---
title: Solución de problemas de replicación
seo-title: Solución de problemas de replicación
description: Este artículo proporciona información sobre cómo solucionar problemas de replicación.
seo-description: Este artículo proporciona información sobre cómo solucionar problemas de replicación.
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---


# Solución de problemas de replicación{#troubleshooting-replication}

Esta página proporciona información sobre cómo solucionar problemas de replicación.

## Problema {#problem}

La replicación (replicación no inversa) está fallando por alguna razón.

## Resolución {#resolution}

Hay varias razones para que la replicación falle. Este artículo explica el enfoque que se podría tomar al analizar estos problemas.

**¿Se activan las réplicas al hacer clic en el botón Activar? Si NO es así, haga lo siguiente:**

1. Vaya a /crx/explorer e inicie sesión como administrador.
1. Abrir &quot;Explorador de contenido&quot;
1. Compruebe si existe un nodo /bin/replicate o /bin/replicate.json. Si el nodo existe, elimínelo y guárdelo.

**¿Las réplicas se ponen en cola en las colas del agente de replicación?**

Para comprobar esto, vaya a /etc/replication/agents.author.html y haga clic en los agentes de replicación para comprobarlo.

**Si hay una cola de agente o unas pocas colas de agente atascadas:**

1. ¿La cola muestra el estado **bloqueado**? Si es así, ¿la instancia de publicación no se está ejecutando o no responde completamente? Compruebe la instancia de publicación para ver qué le sucede (es decir, compruebe los registros y vea si hay un error OutOfMemory o algún otro problema). Entonces, si suele ser lento, tome volcados de subprocesos y analícelos.
1. ¿El estado de la cola muestra que **La cola está activa - # pending**? Básicamente, el trabajo de replicación podría atascarse en una lectura de socket esperando a que responda la instancia pública o Dispatcher. Esto podría significar que la instancia de publicación o Dispatcher está bajo carga alta o atascada en un bloqueo. Tome volcados de subprocesos del autor y publíquelos en este caso.

   * Abra los volcados de subprocesos del autor en un analizador de volcado de subprocesos, compruebe si muestra que el trabajo de eventos de sling del agente de replicación está atascado en un socketRead.
   * Abra los volcados de subprocesos de publicación en un analizador de volcados de subprocesos, analice qué podría estar causando que la instancia de publicación no responda. Debería ver un subproceso con el POST /bin/receive en su nombre, que es el subproceso que recibe la replicación del autor.

**Si todas las colas del agente están atascadas**

1. Es posible que cierto contenido no se pueda serializar en /var/replication/data debido a la corrupción del repositorio o a algún otro problema. Consulte logs/error.log para ver si hay algún error relacionado. Para borrar el elemento de replicación incorrecto, haga lo siguiente:

   1. Vaya a https://&lt;host>:&lt;port>/crx/de e inicie sesión como usuario administrador.
   1. Haga clic en &quot;Herramientas&quot; en el menú superior.
   1. Haga clic en el botón de lupa.
   1. Seleccione &quot;XPath&quot; como Tipo.
   1. En el cuadro &quot;Consulta&quot;, introduzca este orden de consulta /jcr:root/var/eventing/jobs//element(*,slingevent:Job) por @slingevent:created
   1. Haga clic en Buscar
   1. En los resultados, los elementos principales son los últimos trabajos de eventos de sling. Haga clic en cada una de ellas y busque las réplicas atascadas que coinciden con lo que aparece en la parte superior de la cola.

1. Puede haber algún problema con las colas de trabajos del marco de eventos de sling. Intente reiniciar el paquete org.apache.sling.event en /system/console.
1. Puede ser que el procesamiento de trabajos esté completamente desactivado. Puede comprobarlo en la consola Felix en la ficha Evento de Sling. Compruebe si aparece: Evento Apache Sling (EL PROCESAMIENTO DE TRABAJO ESTÁ DESACTIVADO)

   * Si es así, en la pestaña Configuración de la Consola Felix, compruebe el gestor de eventos de trabajo Apache Sling. Puede ser que la casilla de verificación &quot;Procesamiento de trabajos habilitado&quot; esté desmarcada. Si está marcado y sigue mostrando que el procesamiento del trabajo está desactivado, compruebe si hay alguna superposición en /apps/system/config que esté desactivando el procesamiento del trabajo. Intente crear un nodo osgi:config para jobmanager.enabled con un valor booleano como true y vuelva a comprobar si la activación se inició y no hay más trabajos en cola.

1. También puede ocurrir que la configuración de DefaultJobManager entre en un estado incoherente. Esto puede suceder cuando alguien modifica manualmente la configuración del controlador de eventos de trabajo Apache Sling a través de OSGiconsole (Por ejemplo, deshabilitar y volver a habilitar la propiedad &quot;Procesamiento de trabajos habilitado&quot; y Guardar la configuración).

   * En este punto, la configuración de DefaultJobManager que se almacena en crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config obtiene un estado incoherente. Y aunque la propiedad &#39;Apache Sling Job Event Handler&#39; muestra que &#39;Job Processing Enabled&#39; está en estado comprobado, cuando uno navega a la pestaña Sling Event , muestra el mensaje - JOB PROCESSING IS DISABLED y la replicación no funciona.
   * Para resolver este problema, sería necesario navegar a la página Configuración de la consola OSGi y eliminar la configuración &#39;Controlador de eventos de trabajo Apache Sling&#39;. A continuación, reinicie el nodo maestro del clúster para volver a obtener la configuración en un estado coherente. Esto debería solucionar el problema y la replicación empezará a funcionar de nuevo.

**Crear un replication.log**

A veces puede resultar muy útil configurar todos los registros de replicación para que se añadan en un archivo de registro independiente a nivel de depuración. Para ello:

1. Vaya a https://host:port/system/console/configMgr e inicie sesión como administrador.
1. Busque la fábrica Apache Sling Logger y cree una instancia haciendo clic en el botón **+** a la derecha de la configuración de fábrica. Esto creará un nuevo registrador de registros.
1. Establezca la configuración de esta manera:

   * Nivel de registro: DEBUG
   * Ruta del archivo de registro: logs/replication.log
   * Categorías: com.day.cq.replication

1. Si sospecha que el problema está relacionado con eventos/trabajos de sling de alguna manera, también puede agregar este paquete java en categorías:org.apache.sling.event

## Poner en pausa la cola del agente de replicación {#pausing-replication-agent-queue}

En algún momento puede ser adecuado pausar la cola de replicación para reducir la carga en el sistema de creación, sin desactivarla. Actualmente, esto solo es posible si se configura temporalmente un puerto no válido. A partir de la versión 5.4, puede ver el botón de pausa en la cola del agente de replicación que tiene alguna limitación

1. El estado no se mantiene, lo que significa que si reinicia un servidor o el paquete de replicación se recicla, vuelve al estado de ejecución.
1. La pausa está inactiva durante un período más breve (OOB 1 hora después de que no haya actividades con replicación de otros subprocesos) y no durante más tiempo. Porque existe una función en sling que evita subprocesos inactivos. Básicamente, compruebe si un subproceso de cola de trabajos ha estado sin utilizar durante más tiempo, si es así que inicia ciclos de limpieza. Debido al ciclo de limpieza, detiene el subproceso y, por lo tanto, se pierde la configuración pausada. Dado que los trabajos se mantienen, inicia un nuevo subproceso para procesar la cola que no tiene detalles de la configuración pausada. Debido a esto, la cola se convierte en estado de ejecución.

## Los permisos de página no se replican al activar el usuario {#page-permissions-are-not-replicated-on-user-activation}

Los permisos de página no se replican porque se almacenan bajo los nodos a los que se concede acceso, no con el usuario.

En general, los permisos de página no se deben replicar del autor para su publicación y no se deben realizar de forma predeterminada. Esto se debe a que los derechos de acceso deben ser diferentes en esos dos entornos. Por lo tanto, se recomienda configurar las ACL en la publicación por separado del autor.

## Cola de replicación bloqueada al replicar información de espacio de nombres de Author en Publish {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

En algunos casos, la cola de replicación está bloqueada al intentar replicar la información del área de nombres de la instancia de autor en la instancia de publicación. Esto sucede porque el usuario de replicación no tiene privilegios `jcr:namespaceManagement`. Para evitar este problema, asegúrese de que:

* El usuario de replicación (tal como se configura en [Transport](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) tab>User) también existe en la instancia de publicación.
* El usuario tiene privilegios de lectura y escritura en la ruta de acceso donde está instalado el contenido.
* El usuario tiene el privilegio `jcr:namespaceManagement` en el nivel de repositorio. Puede conceder el privilegio de la siguiente manera:

1. Inicie sesión en CRX/DE ( `https://localhost:4502/crx/de/index.jsp`) como administrador.
1. Haga clic en la pestaña **Control de acceso**.
1. Seleccione **Repositorio**.
1. Haga clic en **Agregar entrada** (el icono del signo más).
1. Introduzca el nombre del usuario.
1. Seleccione `jcr:namespaceManagement` en la lista de privilegios.
1. Haga clic en Aceptar.

