---
title: Administrador de trabajo y limitación
seo-title: Administrador de trabajo y limitación
description: Este documento proporciona información general sobre el Administrador de trabajo y proporciona instrucciones sobre cómo configurar las opciones de limitación del Administrador de trabajo.
seo-description: Este documento proporciona información general sobre el Administrador de trabajo y proporciona instrucciones sobre cómo configurar las opciones de limitación del Administrador de trabajo.
uuid: b90998bc-e3d4-493a-9371-55ccb44da20d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9a8b4e3a-f416-4dc6-a90a-9018df5c844e
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 0%

---


# Administrador de trabajo y limitación{#work-manager-and-throttling}

AEM formularios (y versiones anteriores) utilizaban colas JMS para ejecutar operaciones de forma asíncrona. En AEM formularios, las colas de JMS han sido reemplazadas por el Administrador de trabajos. Este documento proporciona información general sobre el Administrador de trabajo y proporciona instrucciones sobre cómo configurar las opciones de limitación del Administrador de trabajo.

## Acerca de las operaciones de larga duración (asincrónicas) {#about-long-lived-asynchronous-operations}

En AEM formularios, las operaciones realizadas por los servicios pueden durar poco (sincrónicas) o durar mucho (asincrónicas). Las operaciones de corta duración se completan sincrónicamente en el mismo subproceso desde el que se invocaron. Estas operaciones esperan una respuesta antes de continuar.

Las operaciones de larga duración pueden abarcar sistemas o incluso extenderse más allá de la organización, como cuando un cliente debe completar y enviar un formulario de solicitud de préstamo como parte de una solución más amplia que integra múltiples tareas automatizadas y humanas. Esas operaciones deben continuar mientras se espera una respuesta. Las operaciones de larga duración realizan su trabajo subyacente de forma asíncrona, lo que permite que los recursos se utilicen de otro modo mientras se espera la finalización. A diferencia de una operación de corta duración, Work Manager no considera que una operación de larga duración se complete una vez que se ha invocado. Para completar la operación debe producirse un déclencheur externo, como un sistema que solicite otra operación en el mismo servicio o un usuario que envíe un formulario.

## Acerca de Work Manager {#about-work-manager}

AEM formularios (y versiones anteriores) utilizaban colas JMS para ejecutar operaciones de forma asíncrona. AEM formularios utiliza Work Manager para programar y ejecutar operaciones asincrónicas mediante subprocesos administrados.

Las operaciones asincrónicas se gestionan de esta manera:

1. El Administrador de trabajos recibe un elemento de trabajo para su ejecución.
1. El Administrador de trabajo almacena el elemento de trabajo en una tabla de base de datos y asigna un identificador único al elemento de trabajo. El registro de base de datos contiene toda la información necesaria para ejecutar el elemento de trabajo.
1. Los subprocesos del Administrador de trabajo extraen elementos de trabajo cuando los subprocesos se liberan. Antes de extraer los elementos de trabajo, los subprocesos pueden comprobar si se inician los servicios necesarios, si hay suficiente tamaño de pila para extraer el siguiente elemento de trabajo y si hay suficientes ciclos de CPU para procesar el elemento de trabajo. El Administrador de trabajo también evalúa los atributos del elemento de trabajo (como su prioridad) al programar su ejecución.

Los administradores de formularios AEM pueden utilizar el Monitor de estado para comprobar las estadísticas del Administrador de trabajo, como el número de elementos de trabajo en la cola y sus estados. También puede utilizar el Monitor de estado para pausar, reanudar, reintentar o eliminar elementos de trabajo. (Consulte [Estadísticas de Vista relacionadas con el Administrador de trabajo](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## Configuración de las opciones de limitación del Administrador de trabajo {#configuring-work-manager-throttling-options}

Puede configurar la limitación para el Administrador de trabajo, de modo que los elementos de trabajo solo se programen cuando haya suficientes recursos de memoria disponibles. La limitación se configura estableciendo las siguientes opciones de JVM en el servidor de aplicaciones.

<table>
 <thead>
  <tr>
   <th><p>Propiedad</p></th>
   <th><p>Descripción</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code> adobe.work-manager.queue-refill-interval</code></td>
   <td><p>Especifica el intervalo de tiempo, en milisegundos, que utiliza el Administrador de trabajo al comprobar si hay nuevos elementos en la cola.</p><p>El valor de esta opción es un entero. El valor predeterminado es <code>1000</code> milisegundos (1 segundo). </p><p>Si el volumen de invocaciones asincrónicas es bajo, puede aumentar este valor. Por ejemplo, puede aumentarla a un valor entre 2000 y 5000 (de 2 a 5 segundos). </p><p>Si el volumen de invocaciones asincrónicas es alto, el valor predeterminado debe ser suficiente, pero puede utilizar un valor inferior si es necesario. Reducir demasiado este valor (por ejemplo, por debajo de 50, lo que resulta en una frecuencia de encuesta de 20 veces por segundo) causa una sobrecarga sustancial en el sistema.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>Establezca esta opción en <code>true</code> para habilitar el modo de depuración o en false para deshabilitarlo. </p><p>En el modo de depuración, se registran los mensajes relativos a las violaciones de la directiva de Administrador de trabajo y a las acciones de pausa/reanudación del Administrador de trabajo. Establezca esta opción en true solo cuando se solucione el problema.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>Establezca esta opción en <code>true</code> para habilitar la limitación en función de la configuración de control de memoria que se describe a continuación o en <code>false</code> para deshabilitar la limitación.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>Especifica el porcentaje máximo de memoria que se puede utilizar antes de que el Administrador de trabajos regule los trabajos entrantes.</p><p>El valor predeterminado de esta opción es <code>95</code>. Este valor debería estar bien para la mayoría de los sistemas. Aumente sólo si su sistema necesita impulsar su capacidad máxima. Pero tenga en cuenta que a medida que aumenta este valor, también aumenta el riesgo de problemas de memoria insuficiente.</p><p>Si está ejecutando AEM formularios en un entorno agrupado, puede que desee establecer la configuración del límite de control de memoria de forma diferente en los diferentes nodos del clúster. Por ejemplo, podría tener un límite máximo inferior en los nodos A y B, que se programan en el equilibrador de carga para el trabajo interactivo. Y se podrían establecer límites altos más altos en los nodos C y D, que no son utilizados por el equilibrador de carga, sino reservados para el trabajo asincrónico.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>Especifica el porcentaje máximo de memoria que se puede utilizar antes de que el Administrador de trabajo deje de limitar los trabajos entrantes.</p><p>El valor predeterminado de esta opción es <code>20</code>. Este valor debería estar bien para la mayoría de los sistemas.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>Especifica el tamaño máximo del lote para el administrador de trabajos. El tamaño predeterminado del lote es 10.</p><p>Si el estado de un proceso en el administrador de trabajos no se actualiza incluso después de completar la tarea, establezca el tamaño del lote en 1.</p></td>
  </tr>
 </tbody>
</table>

**Añadir las opciones de Java a JBoss**

1. Detenga el servidor de aplicaciones JBoss.
1. Abra *[appserver root]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) en un editor y agregue cualquiera de las opciones de Java según sea necesario, con el formato `-Dproperty=value`.
1. Reinicie el servidor.

**Añadir las opciones de Java a WebLogic**

1. Escriba `https://[host name]:[port]/console` en un explorador Web para inicio de la Consola de administración de WebLogic.
1. Escriba el nombre de usuario y la contraseña que creó para el dominio de WebLogic Server y haga clic en Registro en Centro de cambios, haga clic en Bloquear y editar.
1. En Estructura de dominio, haga clic en Entorno > Servidores y, en el panel derecho, haga clic en el nombre del servidor administrado.
1. En la pantalla siguiente, haga clic en la ficha Configuración > Inicio del servidor.
1. En el cuadro Argumentos, anexe los argumentos necesarios al final del contenido actual. Por ejemplo, para deshabilitar el Monitor de estado, agregue:

   `-Dadobe.healthmonitor.enabled=false` deshabilita el Monitor de estado.

1. Haga clic en Guardar y, a continuación, en Activar cambios.
1. Reinicie el servidor administrado por WebLogic.

**Añadir las opciones de Java a WebSphere**

1. En el árbol de navegación de la Consola administrativa de WebSphere, haga clic en Servidores > Tipos de servidor > Servidores de aplicaciones de WebSphere.
1. En el panel derecho, haga clic en el nombre del servidor.
1. En Infraestructura de servidor, haga clic en Java y flujo de trabajo de formularios > Definición de proceso.
1. En Propiedades adicionales, haga clic en Máquina virtual Java.
1. En el cuadro Argumentos genéricos de JVM, escriba los argumentos que necesite.
1. Haga clic en Aceptar o Aplicar y, a continuación, haga clic en Guardar directamente en la configuración maestra.

