---
title: Inicio y parada de WebLogic Server
seo-title: Inicio y parada de WebLogic Server
description: Varios procedimientos requieren que inicie o detenga la instancia de WebLogic Server en la que desea implementar módulos de formularios AEM. Este documento describe cómo iniciar y detener el servidor WebLogic.
seo-description: Varios procedimientos requieren que inicie o detenga la instancia de WebLogic Server en la que desea implementar módulos de formularios AEM. Este documento describe cómo iniciar y detener el servidor WebLogic.
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%

---


# Inicio y parada de WebLogic Server {#starting-and-stopping-weblogic-server}

Varios procedimientos requieren que inicie o detenga la instancia de WebLogic Server en la que desea implementar módulos de formularios AEM. Asegúrese de que el servidor WebLogic está detenido o en ejecución, según la tarea que esté realizando.

<table>
 <thead>
  <tr>
   <th><p>Actividad</p></th>
   <th><p>Estado requerido de WebLogic</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Creación de un dominio WebLogic</p></td>
   <td><p>Detenido</p></td>
  </tr>
  <tr>
   <td><p>Creación de un servidor administrado por WebLogic</p></td>
   <td><p>En ejecución</p></td>
  </tr>
  <tr>
   <td><p>Aumento del recuento de subprocesos del servidor</p></td>
   <td><p>En ejecución</p></td>
  </tr>
  <tr>
   <td><p>Implementación de productos de formularios AEM</p></td>
   <td><p>En ejecución</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Si ejecuta WebLogic Server en Red Hat® Enterprise Linux Advanced Server 4.0, establezca la variable de entorno `LD_ASSUME_KERNEL` en 2.4.19 utilizando el comando `export LD_ASSUME_KERNEL=2.4.19`. A continuación, ejecute WebLogic Server desde el mismo shell en el que configuró esta variable de entorno.

## Iniciar WebLogic Server {#start-weblogic-server}

1. Desde un símbolo del sistema, vaya a *[appserver root]*/user_projects/domains/*[appserverdomain]*.
1. Introduzca el siguiente comando:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

## Detener el servidor WebLogic {#stop-weblogic-server}

1. Inicie la consola de administración de WebLogic Server escribiendo `https://[host name]:7001/console` en la línea URL de un explorador web.
1. Inicie sesión escribiendo el nombre de usuario y la contraseña que se usaron al crear esta configuración de WebLogic y, a continuación, haga clic en Iniciar sesión.
1. En Centro de cambios, haga clic en Bloquear y editar.
1. En Estructura del dominio, haga clic en Entorno > Servidores.
1. Haga clic en AdminServer y, en el panel Configuración de AdminServer, haga clic en la ficha Control .
1. Asegúrese de que AdminServer está seleccionado en la tabla Estado del servidor y haga clic en Cerrar.
1. Seleccione Cuando el trabajo se complete para apagar correctamente el servidor o seleccione Forzar apagado ahora para detener el servidor inmediatamente sin completar las tareas continuas.
1. En el panel Ayudante de ciclo de vida del servidor, haga clic en Sí para completar el cierre.

La consola de administración del servidor de WebLogic ya no está disponible y el símbolo del sistema desde el que ejecutó el comando de inicio está disponible.

## Inicie la consola de administración de WebLogic {#start-weblogic-administration-console}

1. Si el servidor de administración de WebLogic no se está ejecutando, vaya al directorio *[appserver root]\user_projects\domains\[domainname]* e introduzca el siguiente comando:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

1. Para acceder a la consola de administración de WebLogic Server, escriba `https://[host name]:[port]/console` en la línea URL de un explorador web, donde *[port]* es el puerto de escucha no seguro. De forma predeterminada, este valor de puerto es 7001.
1. En la pantalla de inicio de sesión, escriba su nombre de usuario y contraseña de administrador y haga clic en Iniciar sesión.

## Iniciar administrador de nodos {#start-node-manager}

1. Asegúrese de que el servidor WebLogic se esté ejecutando.
1. Desde un nuevo símbolo del sistema, vaya a *[appserver root]*/server/bin.
1. Introduzca el siguiente comando:

   * (Windows) `startNodeManager.cmd`
   * (Linux, UNIX) `./startNodeManager.sh`

## Detener el administrador de nodos {#stop-node-manager}

Después de cerrar el servidor WebLogic, puede cerrar el símbolo del sistema desde el que llamó al Administrador de nodos.

## Iniciar un servidor administrado por WebLogic {#start-a-weblogic-managed-server}

>[!NOTE]
>
>Esta tarea solo se puede realizar después de crear un dominio WebLogic y un servidor administrado.

1. Asegúrese de que el servidor WebLogic y el administrador de nodos se estén ejecutando.
1. Inicie la consola de administración de WebLogic Server escribiendo `https://host name]:[port]/console` en la línea URL de un explorador web.
1. En Estructura del dominio, haga clic en Entorno > Servidores.
1. En el panel derecho, haga clic en la ficha Control .
1. Seleccione el servidor administrado que desea iniciar.
1. Haga clic en el botón Start situado debajo del servidor administrado que desee iniciar.

## Detener un servidor administrado por WebLogic {#stop-a-weblogic-managed-server}

1. Inicie la consola de administración de WebLogic Server escribiendo `https://`*[host name]:[port ]*`/console` en la línea URL de un explorador web.
1. En Estructura del dominio, haga clic en Entorno > Servidores.
1. En el panel derecho, haga clic en la ficha Control .
1. Seleccione el servidor administrado que desea detener.
1. Haga clic en el botón Apagado situado debajo del servidor administrado que desea detener.
1. Seleccione Cuando el trabajo se complete para apagar correctamente el servidor o seleccione Forzar apagado ahora para detener el servidor inmediatamente sin completar las tareas continuas.
1. En el panel Ayudante de ciclo de vida del servidor, haga clic en Sí para completar el cierre.

