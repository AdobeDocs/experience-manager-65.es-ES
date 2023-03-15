---
title: Solución de problemas de replicación
seo-title: Troubleshooting Replication
description: Este artículo proporciona información sobre cómo solucionar problemas de replicación.
seo-description: This article provides information on how to troubleshoot replication issues.
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
feature: Configuring
exl-id: cfa822c8-f9a9-4122-9eac-0293d525f6b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 0%

---

# Solución de problemas de replicación{#troubleshooting-replication}

Esta página proporciona información sobre cómo solucionar problemas de replicación.

## Problema {#problem}

La replicación (replicación no inversa) da error por algún motivo.

## Resolución {#resolution}

Existen varias razones para que la replicación falle. Este artículo explica el enfoque que se puede seguir al analizar estos problemas.

**¿Se activan las replicaciones al hacer clic en el botón Activar? Si NO es así, haga lo siguiente:**

1. Vaya a /crx/explorer e inicie sesión como administrador.
1. Abra &quot;Explorador de contenido&quot;
1. Vea si existe un nodo /bin/replicate o /bin/replicate.json. Si el nodo existe, elimínelo y guárdelo.

**¿Las replicaciones se están poniendo en cola en las colas del agente de replicación?**

Para comprobar esto, vaya a /etc/replication/agents.author.html y haga clic en los agentes de replicación.

**Si una o varias colas de agentes están atascadas:**

1. Muestra la cola **tapado** ¿status? Si es así, ¿la instancia de publicación no se está ejecutando o no responde por completo? Compruebe la instancia de publicación para ver qué le sucede (es decir, compruebe los registros y vea si hay un error OutOfMemory o algún otro problema). Entonces, si es solo lento en general, tome volcados de hilos y analícelos.
1. ¿Se muestra el estado de la cola? **La cola está activa: n.º pendiente**? Básicamente, el trabajo de replicación se podría quedar atascado en una lectura de socket esperando a que responda la instancia de publicación o el distribuidor. Esto podría significar que la instancia de publicación o el despachante están bajo carga alta o atascados en un bloqueo. Tome los volcados de hilos del autor y publíquelos en este caso.

   * Abra los volcados de hilos del autor en un analizador de volcado de hilos y compruebe si muestra que el trabajo de evento de sling del agente de replicación está atascado en un socketRead.
   * Abra los volcados de hilos de la publicación en un analizador de volcado de hilos y analice qué podría estar causando que la instancia de publicación no responda. Debería ver un subproceso con el POST /bin/receive en su nombre, que es el subproceso que recibe la replicación del autor.

**Si todas las colas del agente están atascadas**

1. Es posible que un fragmento de contenido determinado no se pueda serializar en /var/replication/data debido a que el repositorio está dañado o a algún otro problema. Compruebe si hay algún error relacionado en logs/error.log. Para borrar el elemento de replicación incorrecto, haga lo siguiente:

   1. Vaya a https://&lt;host>:&lt;port>/crx/de e inicie sesión como usuario administrador.
   1. Haga clic en &quot;Herramientas&quot; en el menú superior.
   1. Haga clic en el botón de lupa.
   1. Seleccione &quot;XPath&quot; como Tipo.
   1. En el cuadro &quot;Consulta&quot;, introduzca esta consulta /jcr:root/var/eventing/jobs//element(&#42;,slingevent:Job) ordenar por @slingevent:created
   1. Haga clic en Buscar
   1. En los resultados, los elementos principales son los últimos trabajos de eventos de Sling. Haga clic en cada una de ellas y busque las réplicas atascadas que coincidan con lo que aparece en la parte superior de la cola.

1. Puede haber algún problema con las colas de trabajos del marco de eventos de Sling. Intente reiniciar el paquete org.apache.sling.event en /system/console.
1. Puede ser que el procesamiento del trabajo esté completamente desactivado. Puede comprobarlo en la Consola Felix, en la pestaña Evento de Sling. Compruebe si se muestra: Evento de Apache Sling (EL PROCESAMIENTO DEL TRABAJO ESTÁ DESHABILITADO)

   * Si es así, compruebe el controlador de eventos del trabajo Apache Sling en la pestaña Configuración en la consola Felix. Es posible que la casilla &quot;Procesamiento de trabajos activado&quot; esté desmarcada. Si está marcado y sigue mostrando que &quot;el procesamiento del trabajo está deshabilitado&quot;, compruebe si hay alguna superposición en /apps/system/config que esté deshabilitando el procesamiento del trabajo. Intente crear un nodo osgi:config para jobmanager.enabled con un valor booleano en true y vuelva a comprobar si la activación se ha iniciado y no hay más trabajos en cola.

1. También puede ocurrir que la configuración de DefaultJobManager pase a un estado incoherente. Esto puede suceder cuando alguien modifica manualmente la configuración del &quot;Controlador de eventos de trabajos de Apache Sling&quot; a través de la consola OSG (por ejemplo, deshabilita y vuelve a habilitar la propiedad &quot;Procesamiento de trabajos habilitado&quot; y guarda la configuración).

   * En este punto, la configuración de DefaultJobManager almacenada en crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config entra en un estado incoherente. Y aunque la propiedad &quot;Apache Sling Job Event Handler&quot; muestra que &quot;Procesamiento de trabajos activado&quot; está en estado activado, cuando se navega a la pestaña Eventos de Sling, muestra el mensaje: EL PROCESAMIENTO DE TRABAJOS ESTÁ DESHABILITADO y la replicación no funciona.
   * Para resolver este problema, se tendría que navegar a la página Configuración de la consola OSGi y eliminar la configuración &quot;Controlador de eventos de trabajo de Apache Sling&quot;. A continuación, reinicie el nodo principal del clúster para volver a poner la configuración en un estado coherente. Esto debería solucionar el problema y la replicación volverá a funcionar.

**Crear un archivo replication.log**

A veces puede resultar muy útil configurar todos los registros de replicación para agregarlos en un archivo de registro independiente en el nivel DEBUG. Para ello, haga lo siguiente:

1. Vaya a https://host:port/system/console/configMgr e inicie sesión como administrador.
1. Busque la fábrica del registrador de Apache Sling y cree una instancia haciendo clic en **+** a la derecha de la configuración de fábrica. Esto creará un nuevo registrador.
1. Establezca la configuración de esta manera:

   * Nivel de registro: DEPURAR
   * Ruta del archivo de registro: logs/replication.log
   * Categorías: com.day.cq.replication

1. Si sospecha que el problema está relacionado con eventos/trabajos de sling de alguna manera, también puede agregar este paquete java en categorías:org.apache.sling.event

## Pausa de cola del agente de replicación  {#pausing-replication-agent-queue}

A veces puede ser adecuado pausar la cola de replicación para reducir la carga en el sistema de creación, sin deshabilitarla. Actualmente esto solo es posible por un hackeo de la configuración temporal de un puerto no válido. A partir de la versión 5.4, puede ver el botón de pausa en la cola del agente de replicación. Tiene algunas limitaciones

1. El estado no es persistente, lo que significa que si reinicia un servidor o se recicla un paquete de replicación, vuelve al estado de ejecución.
1. La pausa está inactiva durante un período más corto (OOB 1 hora después de que no haya actividades con replicación de otros subprocesos) y no durante un tiempo más largo. Porque hay una función en sling que evita las roscas inactivas. Básicamente, compruebe si un hilo de cola de trabajos se ha utilizado durante un tiempo más largo, si es así, inicia ciclos de limpieza. Debido al ciclo de limpieza, detiene el hilo y, por lo tanto, se pierde el ajuste en pausa. Dado que los trabajos se mantienen, inicia un nuevo subproceso para procesar la cola que no tiene detalles de la configuración en pausa. Debido a esto, la cola se convierte en estado de ejecución.

## Los permisos de la página no se replican en la activación del usuario {#page-permissions-are-not-replicated-on-user-activation}

Los permisos de página no se replican porque se almacenan en los nodos a los que se concede acceso, no con el usuario.

En general, los permisos de página no deben replicarse del autor a la publicación y no están disponibles de forma predeterminada. Esto se debe a que los derechos de acceso deben ser diferentes en esos dos entornos. Por lo tanto, se recomienda configurar las ACL en la publicación por separado del autor.

## Cola de replicación bloqueada al replicar información de área de nombres de Autor a Publicar {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

En algunos casos, la cola de replicación se bloquea al intentar replicar la información del área de nombres de la instancia de autor a la instancia de publicación. Esto sucede porque el usuario de replicación no tiene `jcr:namespaceManagement` privilegio. Para evitar este problema, asegúrese de que:

* El usuario de replicación (como se configura en la [Transporte](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) (pestaña > Usuario) también existe en la instancia de publicación.
* El usuario tiene privilegios de lectura y escritura en la ruta donde está instalado el contenido.
* El usuario tiene `jcr:namespaceManagement` en el nivel de repositorio. Puede otorgar el privilegio de la siguiente manera:

1. Iniciar sesión en CRX/DE ( `https://localhost:4502/crx/de/index.jsp`) como administrador.
1. Haga clic en **Control de acceso** pestaña.
1. Seleccionar **Repositorio**.
1. Clic **Agregar entrada** (el icono &quot;+&quot;).
1. Introduzca el nombre del usuario.
1. Seleccionar `jcr:namespaceManagement` de la lista de privilegios.
1. Haga clic en Aceptar.
