---
title: Gestor de trabajo y regulación
seo-title: Work Manager and throttling
description: Este documento proporciona información básica sobre Work Manager y proporciona instrucciones sobre cómo configurar las opciones de regulación de Work Manager.
seo-description: This document provides background information on Work Manager, and provides instructions on configuring Work Manager throttling options.
uuid: b90998bc-e3d4-493a-9371-55ccb44da20d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9a8b4e3a-f416-4dc6-a90a-9018df5c844e
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# Gestor de trabajo y regulación{#work-manager-and-throttling}

AEM formularios (y versiones anteriores) utilizaban colas JMS para ejecutar operaciones asincrónicamente. En AEM formularios, las colas de JMS se han sustituido por Work Manager. Este documento proporciona información básica sobre Work Manager y proporciona instrucciones sobre cómo configurar las opciones de regulación de Work Manager.

## Acerca de las operaciones de larga duración (asincrónicas) {#about-long-lived-asynchronous-operations}

En AEM formularios, las operaciones realizadas por los servicios pueden durar poco (síncrono) o durar mucho (asíncrono). Las operaciones de corta duración se completan sincrónicamente en el mismo subproceso desde el que se invocaron. Estas operaciones esperan una respuesta antes de continuar.

Las operaciones de larga duración pueden abarcar sistemas o incluso extenderse más allá de la organización, como cuando un cliente debe completar y enviar un formulario de solicitud de préstamo como parte de una solución más amplia que integra múltiples tareas automatizadas y humanas. Esas operaciones deben continuar mientras esperan una respuesta. Las operaciones de larga duración realizan su trabajo subyacente de forma asíncrona, lo que permite que los recursos se comprometan de otro modo mientras esperan su finalización. A diferencia de una operación de corta duración, Work Manager no considera que una operación de larga duración se complete una vez que se invoca. Debe producirse un déclencheur externo, como un sistema que solicite otra operación en el mismo servicio o un usuario que envíe un formulario, para completar la operación.

## Acerca de Work Manager {#about-work-manager}

AEM formularios (y versiones anteriores) utilizaban colas JMS para ejecutar operaciones asincrónicamente. AEM formularios utilizan Work Manager para programar y ejecutar operaciones asincrónicas mediante subprocesos administrados.

Las operaciones asincrónicas se gestionan de esta manera:

1. Work Manager recibe un elemento de trabajo para su ejecución.
1. Work Manager almacena el elemento de trabajo en una tabla de base de datos y asigna un identificador único al elemento de trabajo. El registro de base de datos contiene toda la información necesaria para ejecutar el elemento de trabajo.
1. Los subprocesos de Work Manager extraen elementos de trabajo cuando los subprocesos quedan libres. Antes de extraer los elementos de trabajo, los subprocesos pueden comprobar si se inician los servicios necesarios, si hay suficiente tamaño de pila para extraer el siguiente elemento de trabajo y si hay suficientes ciclos de CPU para procesar el elemento de trabajo. Work Manager también evalúa los atributos del elemento de trabajo (como su prioridad) al programar su ejecución.

AEM administradores de formularios pueden utilizar el Monitor de estado para comprobar las estadísticas del Administrador de trabajo, como el número de elementos de trabajo en la cola y sus estados. También puede utilizar el Monitor de estado para pausar, reanudar, reintentar o eliminar elementos de trabajo. (Consulte [Ver estadísticas relacionadas con Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## Configuración de las opciones de regulación del Gestor de Trabajo {#configuring-work-manager-throttling-options}

Puede configurar la regulación de Work Manager, de modo que los elementos de trabajo solo se programen cuando haya suficientes recursos de memoria disponibles. La regulación se configura con las siguientes opciones de JVM en el servidor de aplicaciones.

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
   <td><p>Especifica el intervalo de tiempo, en milisegundos, que utiliza Work Manager al comprobar si hay nuevos elementos en la cola.</p><p>El valor de esta opción es un número entero. El valor predeterminado es <code>1000</code> milisegundos (1 segundo). </p><p>Si el volumen de invocaciones asincrónicas es bajo, puede aumentar este valor. Por ejemplo, puede aumentarla a un valor comprendido entre 2000 y 5000 (de 2 a 5 segundos). </p><p>Si el volumen de invocaciones asincrónicas es alto, el valor predeterminado debe ser suficiente, pero puede utilizar un valor inferior si es necesario. Reducir demasiado este valor (por ejemplo, por debajo de 50, lo que resulta en una frecuencia de sondeo de 20 veces por segundo) causa una sobrecarga sustancial en el sistema.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>Establezca esta opción como <code>true</code> para habilitar el modo de depuración o para false para deshabilitarlo. </p><p>En el modo de depuración, se registran los mensajes relacionados con las violaciones de la directiva de Work Manager y las acciones de pausa/reanudación de Work Manager. Establezca esta opción como true solo cuando solucione problemas.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>Establezca esta opción como <code>true</code> para habilitar la regulación basada en la configuración de control de memoria que se describe a continuación, o para <code>false</code> para desactivar la restricción.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>Especifica el porcentaje máximo de memoria que se puede utilizar antes de que Work Manager limite los trabajos entrantes.</p><p>El valor predeterminado de esta opción es <code>95</code>. Este valor debería estar bien para la mayoría de los sistemas. Aumente sólo si su sistema necesita impulsar su capacidad máxima. Pero tenga en cuenta que a medida que aumenta este valor, también aumenta el riesgo de problemas de Memoria insuficiente.</p><p>Si está ejecutando AEM formularios en un entorno agrupado, puede que desee establecer la configuración del límite de control de memoria de forma diferente en diferentes nodos del clúster. Por ejemplo, podría tener un límite alto inferior en los nodos A y B, que están programados en el equilibrador de carga para el trabajo interactivo. Y podría tener límites altos más altos establecidos en los nodos C y D, que no son utilizados por el equilibrador de carga, pero reservados para trabajo asincrónico.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>Especifica el porcentaje máximo de memoria que se puede utilizar antes de que el Administrador de trabajos deje de limitar los trabajos entrantes.</p><p>El valor predeterminado de esta opción es <code>20</code>. Este valor debería estar bien para la mayoría de los sistemas.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>Especifica el tamaño máximo del lote para workmanager. El tamaño predeterminado del lote es 10.</p><p>Si el estado de un proceso en el administrador de trabajos no se actualiza incluso después de completar la tarea, establezca el tamaño del lote en 1.</p></td>
  </tr>
 </tbody>
</table>

**Agregar opciones de Java a JBoss**

1. Detenga el servidor de aplicaciones JBoss.
1. Abra el *[raíz de appserver]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) en un editor y añada cualquiera de las opciones de Java según sea necesario, con el formato `-Dproperty=value`.
1. Reiniciar el servidor.

**Añadir opciones de Java a WebLogic**

1. Inicie la consola de administración de WebLogic escribiendo `https://[host name]:[port]/console` en un explorador web.
1. Escriba el nombre de usuario y la contraseña que creó para el dominio de WebLogic Server y haga clic en Registro en el Centro de cambios, haga clic en Bloquear y editar.
1. En Estructura del dominio, haga clic en Entorno > Servidores y, en el panel derecho, haga clic en el nombre del servidor administrado.
1. En la siguiente pantalla, haga clic en la ficha Configuración > Inicio del servidor .
1. En el cuadro Argumentos , anexe los argumentos que necesite al final del contenido actual. Por ejemplo, para deshabilitar el Monitor de estado, agregue:

   `-Dadobe.healthmonitor.enabled=false` deshabilita el Monitor de estado.

1. Haga clic en Guardar y, a continuación, en Activar cambios.
1. Reinicie el servidor administrado por WebLogic.

**Agregar opciones de Java a WebSphere**

1. En el árbol de navegación de la Consola administrativa de WebSphere, haga clic en Servidores > Tipos de servidor > Servidores de aplicaciones de WebSphere.
1. En el panel derecho, haga clic en el nombre del servidor.
1. En Infraestructura de servidor, haga clic en Java y flujo de trabajo de formularios > Definición del proceso.
1. En Propiedades adicionales, haga clic en Máquina virtual Java.
1. En el cuadro Argumentos genéricos de JVM, escriba los argumentos que necesite.
1. Haga clic en Aceptar o en Aplicar y, a continuación, haga clic en Guardar directamente en la configuración maestra.
