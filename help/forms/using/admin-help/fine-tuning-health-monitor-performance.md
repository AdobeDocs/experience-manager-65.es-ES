---
title: Mejora del rendimiento del monitor de mantenimiento
seo-title: Mejora del rendimiento del monitor de mantenimiento
description: Aprenda a ajustar el rendimiento del monitor de estado
seo-description: Aprenda a ajustar el rendimiento del monitor de estado
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---


# Mejora del rendimiento del monitor de estado{#fine-tuning-health-monitor-performance}

La recopilación de estadísticas del sistema que rellenan el Monitor de estado tiene cierto impacto en el rendimiento del entorno de formularios AEM. Este impacto se puede controlar configurando las opciones de Java que se enumeran a continuación en el servidor de aplicaciones.

<table>
 <thead>
  <tr>
   <th><p>Propiedad</p></th>
   <th><p>Función</p></th>
   <th><p>Valor predeterminado</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe.healthmonitor.enabled</p></td>
   <td><p>Activar o desactivar el subproceso del monitor de estado</p></td>
   <td><p>verdadero</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>Activar o desactivar la caché de Gemfire</p></td>
   <td><p>verdadero</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>Intervalo en milisegundos después del cual el subproceso del monitor de estado recopila las estadísticas</p></td>
   <td><p>10 minutos (600.000 milisegundos)</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>El puerto de multidifusión utilizado para comunicarse con otros miembros del sistema distribuido. Si se establece en cero, la multidifusión está deshabilitada tanto para la detección de miembros como para la distribución. </p><p>Nota: Seleccione diferentes direcciones y puertos de multidifusión para diferentes sistemas distribuidos. No utilice direcciones distintas únicamente.</p></td>
   <td><p>No hay ningún valor predeterminado. Los valores válidos van de 0 a 65535.</p></td>
  </tr>
  <tr>
   <td><p>tasa de muestra estadística</p></td>
   <td><p>Frecuencia en milisegundos a la que se muestrean las estadísticas. Las estadísticas del sistema operativo solo se actualizan cuando se toma una muestra.</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>Esta propiedad habilita o deshabilita la recopilación de estadísticas de Work Manager, como el recuento de elementos de trabajo o de trabajo.</p></td>
   <td><p>verdadero</p></td>
  </tr>
 </tbody>
</table>

## Añadir las opciones de Java a JBoss {#add-java-options-to-jboss}

1. Detenga el servidor de aplicaciones JBoss.
1. Abra *[appserver root]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) en un editor y agregue cualquiera de las opciones de Java según sea necesario.
1. Reinicie el servidor.

## Añadir las opciones de Java a WebLogic {#add-java-options-to-weblogic}

1. Inicio la consola de administración WebLogic escribiendo https://[nombre de host]:&#39;puerto&#39;/consola en la línea URL de un explorador Web.
1. Escriba el nombre de usuario y la contraseña que creó para el dominio de WebLogic Server y haga clic en Registro en Centro de cambios, haga clic en Bloquear y editar.
1. En Estructura de dominio, haga clic en Entorno > Servidores y, en el panel derecho, haga clic en el nombre del servidor administrado.
1. En la pantalla siguiente, haga clic en la ficha Configuración > Inicio del servidor.
1. En el cuadro Argumentos, anexe los argumentos necesarios al final del contenido actual. Por ejemplo, si agrega - `Dadobe.healthmonitor.enabled=false` se deshabilita el Monitor de estado.
1. Haga clic en Guardar y, a continuación, en Activar cambios.
1. Reinicie el servidor administrado por WebLogic.

## Añadir las opciones de Java a WebSphere {#add-java-options-to-websphere}

1. En el árbol de navegación de la Consola administrativa de WebSphere, haga lo siguiente para el servidor de aplicaciones:

   (WebSphere 6.x) Haga clic en Servidores > Servidores de aplicaciones

   (WebSphere 7.x) Haga clic en Servidores > Tipos de servidor > Servidores de aplicaciones WebSphere

1. En el panel derecho, haga clic en el nombre del servidor.
1. En Infraestructura de servidor, haga clic en Java y flujo de trabajo de formularios > Definición de proceso.
1. En Propiedades adicionales, haga clic en Máquina virtual Java.
1. En el cuadro Argumentos genéricos de JVM, escriba los argumentos que necesite.
1. Haga clic en Aceptar o Aplicar y, a continuación, haga clic en Guardar directamente en la configuración maestra.

