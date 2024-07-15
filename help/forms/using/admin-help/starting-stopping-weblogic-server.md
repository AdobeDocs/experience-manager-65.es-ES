---
title: Iniciar y detener WebLogic Server
description: AEM Varios procedimientos requieren que inicie o detenga la instancia de WebLogic Server en la que desea implementar módulos de formularios de la forma que desee. Este documento describe cómo iniciar y detener WebLogic Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---


# Iniciar y detener WebLogic Server {#starting-and-stopping-weblogic-server}

AEM Varios procedimientos requieren que inicie o detenga la instancia de WebLogic Server en la que desea implementar módulos de formularios de la forma que desee. Asegúrese de que WebLogic Server esté detenido o en ejecución, según la tarea que esté realizando.

<table>
 <thead>
  <tr>
   <th><p>Actividad</p></th>
   <th><p>Estado de WebLogic requerido</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Creación de un dominio de WebLogic</p></td>
   <td><p>Detenido</p></td>
  </tr>
  <tr>
   <td><p>Creación de un servidor administrado por WebLogic</p></td>
   <td><p>En ejecución</p></td>
  </tr>
  <tr>
   <td><p>Aumento del número de subprocesos del servidor</p></td>
   <td><p>En ejecución</p></td>
  </tr>
  <tr>
   <td><p>AEM Implementar productos de formularios de</p></td>
   <td><p>En ejecución</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Si está ejecutando WebLogic Server en Red Hat® Enterprise Linux Advanced Server 4.0, establezca la variable de entorno `LD_ASSUME_KERNEL` en 2.4.19 mediante el comando `export LD_ASSUME_KERNEL=2.4.19`. A continuación, ejecute WebLogic Server desde el mismo shell en el que se configura esta variable de entorno.

## Iniciar WebLogic Server {#start-weblogic-server}

1. Desde un símbolo del sistema, vaya a *[appserver root]*/user_projects/domains/*[appserverdomain]*.
1. Introduzca el siguiente comando:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

## Detener WebLogic Server {#stop-weblogic-server}

1. Inicie la consola de administración de WebLogic Server escribiendo `https://[host name]:7001/console` en la línea URL de un explorador web.
1. Inicie sesión escribiendo el nombre de usuario y la contraseña que utilizó al crear esta configuración de WebLogic y, a continuación, haga clic en Iniciar sesión.
1. En Centro de cambios, haga clic en Bloquear y editar.
1. En Estructura de dominio, haga clic en Entorno > Servidores.
1. Haga clic en AdminServer y, en el panel Configuración de AdminServer, haga clic en la ficha Control.
1. Asegúrese de que AdminServer está seleccionado en la tabla Estado del servidor y haga clic en Apagar.
1. Seleccione Al finalizar el trabajo para apagar correctamente el servidor o seleccione Forzar apagado ahora para detener el servidor inmediatamente sin completar las tareas en curso.
1. En el panel Asistente para ciclos de vida de servidor, haga clic en Sí para completar el apagado.

La consola de administración de WebLogic Server ya no está disponible y el símbolo del sistema desde el que ejecutó el comando start está disponible.

## Iniciar la consola de administración de WebLogic {#start-weblogic-administration-console}

1. Si el servidor de administración de WebLogic aún no se está ejecutando, desde un símbolo del sistema, vaya al directorio *[appserver root]\user_projects\domains\[domainname]* e introduzca el siguiente comando:

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

1. Acceda a la consola de administración de WebLogic Server escribiendo `https://[host name]:[port]/console` en la línea URL de un explorador web, donde *[port]* es el puerto de escucha no seguro. De forma predeterminada, este valor de puerto es 7001.
1. En la pantalla de inicio de sesión, escriba el nombre de usuario y la contraseña del administrador y haga clic en Iniciar sesión.

## Iniciar el administrador de nodos {#start-node-manager}

1. Asegúrese de que WebLogic Server se esté ejecutando.
1. Desde un nuevo símbolo del sistema, vaya a *[appserver root]*/server/bin.
1. Introduzca el siguiente comando:

   * (Windows) `startNodeManager.cmd`
   * (Linux, UNIX) `./startNodeManager.sh`

## Detener el administrador de nodos {#stop-node-manager}

Después de cerrar WebLogic Server, puede cerrar el símbolo del sistema desde el que llamó a Node Manager.

## Inicio de un servidor administrado por WebLogic {#start-a-weblogic-managed-server}

>[!NOTE]
>
>Esta tarea solo se puede realizar después de crear un dominio de WebLogic y un servidor administrado.

1. Asegúrese de que WebLogic Server y el administrador de nodos se estén ejecutando.
1. Inicie la consola de administración de WebLogic Server escribiendo `https://host name]:[port]/console` en la línea URL de un explorador web.
1. En Estructura de dominio, haga clic en Entorno > Servidores.
1. En el panel derecho, haga clic en la ficha Control.
1. Seleccione el servidor administrado que desea iniciar.
1. Haga clic en el botón Inicio situado debajo del servidor administrado que desea iniciar.

## Detener un servidor administrado por WebLogic {#stop-a-weblogic-managed-server}

1. Inicie la consola de administración de WebLogic Server escribiendo `https://`*[nombre de host]:[puerto ]*`/console` en la línea URL de un explorador web.
1. En Estructura de dominio, haga clic en Entorno > Servidores.
1. En el panel derecho, haga clic en la ficha Control.
1. Seleccione el servidor administrado que desea detener.
1. Haga clic en el botón Apagar situado debajo del servidor administrado que desea detener.
1. Seleccione Al finalizar el trabajo para apagar correctamente el servidor o seleccione Forzar apagado ahora para detener el servidor inmediatamente sin completar las tareas en curso.
1. En el panel Asistente para ciclos de vida de servidor, haga clic en Sí para completar el apagado.

