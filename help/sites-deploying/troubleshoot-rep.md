---
title: Resolución de problemas de replicación
seo-title: Resolución de problemas de replicación
description: Este artículo proporciona información sobre cómo solucionar problemas de replicación.
seo-description: Este artículo proporciona información sobre cómo solucionar problemas de replicación.
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 0%

---


# Solución de problemas de replicación{#troubleshooting-replication}

Esta página proporciona información sobre cómo solucionar problemas de replicación.

## Problema {#problem}

La replicación (replicación no inversa) está fallando por alguna razón.

## Resolución {#resolution}

Existen varias razones para que la replicación falle. En este artículo se explica el enfoque que se podría adoptar al analizar estos problemas.

**¿Se activan las replicaciones al hacer clic en el botón Activar? Si NO, haga lo siguiente:**

1. Vaya a /crx/explorer e inicie sesión como administrador.
1. Abrir &quot;Explorador de contenido&quot;
1. Consulte si existe un nodo /bin/replicate o /bin/replicate.json. Si el nodo existe, elimínelo y guárdelo.

**¿Las replicaciones se ponen en cola en las colas del agente de replicación?**

Consulte esto en /etc/replication/agents.author.html y luego haga clic en los agentes de replicación para comprobarlo.

**Si hay una cola de agente o unas pocas colas de agentes atascadas:**

1. ¿La cola muestra el estado **bloqueado**? Si es así, ¿la instancia de publicación no se está ejecutando o no responde totalmente? Compruebe la instancia de publicación para ver qué tiene de malo (es decir, compruebe los registros y vea si hay un error OutOfMemory o algún otro problema. Entonces, si por lo general es lenta, tome los vertederos y analícelos.
1. ¿El estado de la cola muestra que **La cola está activa - # pendiente**? Básicamente, el trabajo de replicación se podría atascar en un socket en espera de que la instancia pública o el despachante respondan. Esto podría significar que la instancia de publicación o el despachante están bajo carga alta o bloqueados. Tome los archivos de subproceso del autor y publíquelos en este caso.

   * Abra los volcados de subprocesos del autor en un analizador de volcado de subprocesos, compruebe si muestra que el trabajo de eventos de sling del agente de replicación está atascado en un socketRead.
   * Abra los volcados de subproceso de la publicación en un analizador de volcado de subprocesos, analice qué podría estar causando que la instancia de publicación no responda. Debe ver un subproceso con el nombre POST /bin/received, es decir, el subproceso que recibe la replicación del autor.

**Si todas las colas de agentes están atascadas**

1. Es posible que un determinado fragmento de contenido no se pueda serializar en /var/Replication/data debido a daños en el repositorio o a algún otro problema. Consulte logs/error.log para ver si hay algún error relacionado. Para borrar el elemento de replicación incorrecto, haga lo siguiente:

   1. Vaya a https://&lt;host>:&lt;puerto>/crx/de e inicie sesión como usuario administrador.
   1. Haga clic en &quot;Herramientas&quot; en el menú superior.
   1. Haga clic en el botón de la lupa.
   1. Seleccione &quot;XPath&quot; como Tipo.
   1. En el cuadro &quot;Consulta&quot;, introduzca el orden de consulta /jcr:root/var/eventing/job//element(*,slingevent:Job) de @slingevent:created
   1. Haga clic en &quot;Buscar&quot;
   1. En los resultados, los elementos principales son los últimos trabajos de eventos de ventas. Haga clic en cada una de ellas y busque las réplicas que coinciden con lo que aparece en la parte superior de la cola.

1. Podría haber algún problema con la venta de colas de trabajos de marco de eventos. Intente reiniciar el paquete org.apache.sling.evento en la consola/system/console.
1. Es posible que el procesamiento de trabajos esté completamente desactivado. Puede comprobarlo en la consola Félix, en la ficha Eventos de Sling. Compruebe si se muestra - Acontecimiento de Apache Sling (EL PROCESAMIENTO DE TRABAJO ESTÁ DESHABILITADO)

   * Si es así, compruebe el controlador de Evento de trabajo de Apache Sling en la ficha Configuración de la consola Felix. Podría ser que la casilla de verificación &#39;Procesamiento de trabajos activado&#39; esté desactivada. Si está marcado y sigue mostrando que &#39;el procesamiento de trabajos está deshabilitado&#39;, compruebe si hay alguna superposición en /apps/system/config que esté desactivando el procesamiento de trabajos. Intente crear un nodo osgi:config para jobmanager.enabled con un valor booleano en true y vuelva a comprobar si la activación se ha iniciado y no hay más trabajos en cola.

1. También es posible que la configuración de DefaultJobManager tenga un estado incoherente. Esto puede suceder cuando alguien modifica manualmente la configuración del controlador de Evento de trabajo de Apache Sling mediante OSGiconsole (por ejemplo, deshabilitar y volver a habilitar la propiedad &#39;Job Processing Enabled&#39; y Guardar la configuración).

   * En este punto, la configuración de DefaultJobManager que se almacena en crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config pasa a un estado incoherente. Y aunque la propiedad &#39;Apache Sling Job Evento Handler&#39; muestra que &#39;Job Processing Enabled&#39; está en estado marcado, cuando uno navega a la ficha Sling Eventing, muestra el mensaje - JOB PROCESSING IS DESHABILITADO y la replicación no funciona.
   * Para resolver este problema, es necesario desplazarse a la página Configuración de la consola OSGi y eliminar la configuración &#39;Controlador de Evento de trabajo Apache Sling&#39;. A continuación, reinicie el nodo maestro del clúster para volver a colocar la configuración en un estado coherente. Esto debería solucionar el problema y la replicación tendrá inicios para volver a funcionar.

**Crear un archivo Replication.log**

A veces puede resultar muy útil configurar todos los registros de replicación para que se agreguen en un archivo de registro independiente a nivel DEBUG. Para ello:

1. Vaya a https://host:port/system/console/configMgr e inicie sesión como administrador.
1. Busque la fábrica Apache Sling Logging Logger y cree una instancia haciendo clic en el botón **+** a la derecha de la configuración de fábrica. Esto creará un nuevo registrador.
1. Configure la configuración de esta manera:

   * Nivel de registro: DEPURAR
   * Ruta del archivo de registro: logs/replication.log
   * Categorías: com.day.cq.replication

1. Si sospecha que el problema está relacionado con la venta de eventos/trabajos de cualquier manera, también puede agregar este paquete java en categorías:org.apache.sling.evento

## Pausa de la Cola del Agente de Replicación {#pausing-replication-agent-queue}

En algún momento puede ser adecuado pausar la cola de replicación para reducir la carga en el sistema de creación, sin deshabilitarlo. Actualmente, esto solo es posible si se configura temporalmente un puerto no válido. A partir de 5.4, puede ver el botón de pausa en la cola del agente de replicación que tiene alguna limitación

1. El estado no persiste, lo que significa que si reinicia un servidor o se recicla un paquete de replicación, vuelve a estar en estado de ejecución.
1. La pausa está inactiva durante un período más corto (OOB 1 hora después de no haber actividades con la replicación por otros subprocesos) y no durante un período más largo. Porque existe una característica en sling que evita roscas inactivas. Básicamente, compruebe si un subproceso de cola de trabajos no se ha utilizado durante más tiempo, si es así, inicia ciclos de limpieza. Debido al ciclo de limpieza, detiene el subproceso y, por lo tanto, se pierde la configuración pausada. Dado que los trabajos se mantienen, inicia un nuevo subproceso para procesar la cola que no tiene detalles de la configuración pausada. Debido a esto, la cola se convierte en estado de ejecución.

## Los permisos de página no se replican en la Activación del usuario {#page-permissions-are-not-replicated-on-user-activation}

Los permisos de página no se replican porque se almacenan bajo los nodos a los que se concede acceso, no con el usuario.

En general, los permisos de página no se deben replicar del autor para publicar y no se pueden realizar de forma predeterminada. Esto se debe a que los derechos de acceso deberían ser diferentes en esos dos entornos. Por lo tanto, se recomienda configurar las ACL en la publicación por separado del autor.

## Cola de replicación bloqueada al replicar información de Área de nombres de Author to Publish {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

En algunos casos, la cola de replicación se bloquea al intentar replicar información de Área de nombres de la instancia de creación a la instancia de publicación. Esto sucede porque el usuario de replicación no tiene `jcr:namespaceManagement` privilegios. Para evitar este problema, asegúrese de que:

* El usuario de replicación (según la configuración de la ficha [Transporte](/help/sites-deploying/replication.md#replication-agents-configuration-parameters)> Usuario) también existe en la instancia Publicar.
* El usuario tiene privilegios de lectura y escritura en la ruta de acceso donde está instalado el contenido.
* El usuario tiene `jcr:namespaceManagement` privilegios en el nivel de repositorio. Puede otorgar el privilegio de la siguiente manera:

1. Inicie sesión en CRX/DE ( `https://localhost:4502/crx/de/index.jsp`) como administrador.
1. Haga clic en la ficha **Control de acceso**.
1. Seleccione **Repositorio**.
1. Haga clic en **Añadir entrada** (el icono del signo más).
1. Escriba el nombre del usuario.
1. Seleccione `jcr:namespaceManagement` en la lista de privilegios.
1. Haga clic en Aceptar.

