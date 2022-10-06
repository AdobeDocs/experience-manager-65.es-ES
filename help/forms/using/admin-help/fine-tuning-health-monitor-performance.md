---
title: Ajuste del rendimiento del Monitor de estado
seo-title: Fine-tuning Health Monitor performance
description: Aprenda a ajustar el rendimiento del Monitor de estado
seo-description: Learn how to fine-tune Health Monitor performance
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
exl-id: 41042e08-5e14-4809-89b7-16d98a72d1b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 2%

---

# Ajuste del rendimiento del Monitor de estado{#fine-tuning-health-monitor-performance}

La recopilación de estadísticas del sistema que rellenan el Monitor de estado tiene algún impacto en el rendimiento del entorno de formularios AEM. Este impacto se puede controlar configurando las opciones de Java que se enumeran a continuación en el servidor de aplicaciones.

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
   <td><p>Activar o desactivar el subproceso del Monitor de estado</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>Activar o desactivar el almacenamiento en caché de Gemfire</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>Intervalo en milisegundos después del cual el subproceso del Monitor de estado recopila las estadísticas</p></td>
   <td><p>10 minutos (600.000 milisegundos)</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>Puerto de multidifusión utilizado para comunicarse con otros miembros del sistema distribuido. Si se establece en cero, la multidifusión está deshabilitada tanto para la detección de miembros como para la distribución. </p><p>Nota: Seleccione diferentes direcciones y puertos de multidifusión para diferentes sistemas distribuidos. No utilice solo direcciones diferentes.</p></td>
   <td><p>No hay ningún valor predeterminado. Los valores válidos van del 0 al 65535.</p></td>
  </tr>
  <tr>
   <td><p>tasa estadística-muestra</p></td>
   <td><p>Tasa en milisegundos a la que se muestrean las estadísticas. Las estadísticas del sistema operativo solo se actualizan cuando se toma una muestra.</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>Esta propiedad habilita o deshabilita la recopilación de estadísticas de Work Manager, como el recuento de artículos de trabajo o de trabajo.</p></td>
   <td><p>true</p></td>
  </tr>
 </tbody>
</table>

## Agregar opciones de Java a JBoss {#add-java-options-to-jboss}

1. Detenga el servidor de aplicaciones JBoss.
1. Abra el *[raíz de appserver]*/bin/run.bat (Windows) o run.sh (Linux o UNIX) en un editor y añada cualquiera de las opciones de Java según sea necesario.
1. Reiniciar el servidor.

## Añadir opciones de Java a WebLogic {#add-java-options-to-weblogic}

1. Inicie la consola de administración de WebLogic escribiendo https://[nombre de host]: &quot;puerto&quot;/consola en la línea URL de un explorador web.
1. Escriba el nombre de usuario y la contraseña que creó para el dominio de WebLogic Server y haga clic en Registro en el Centro de cambios, haga clic en Bloquear y editar.
1. En Estructura del dominio, haga clic en Entorno > Servidores y, en el panel derecho, haga clic en el nombre del servidor administrado.
1. En la siguiente pantalla, haga clic en la ficha Configuración > Inicio del servidor .
1. En el cuadro Argumentos , anexe los argumentos que necesite al final del contenido actual. Por ejemplo, si agrega `Dadobe.healthmonitor.enabled=false` deshabilita el Monitor de estado.
1. Haga clic en Guardar y, a continuación, en Activar cambios.
1. Reinicie el servidor administrado por WebLogic.

## Agregar opciones de Java a WebSphere {#add-java-options-to-websphere}

1. En el árbol de navegación de la Consola administrativa de WebSphere, haga lo siguiente para su servidor de aplicaciones:

   (WebSphere 6.x) Haga clic en Servidores > Servidores de aplicaciones

   (WebSphere 7.x) Haga clic en Servidores > Tipos de servidor > Servidores de aplicaciones WebSphere

1. En el panel derecho, haga clic en el nombre del servidor.
1. En Infraestructura de servidor, haga clic en Java y flujo de trabajo de formularios > Definición del proceso.
1. En Propiedades adicionales, haga clic en Máquina virtual Java.
1. En el cuadro Argumentos genéricos de JVM, escriba los argumentos que necesite.
1. Haga clic en Aceptar o en Aplicar y, a continuación, haga clic en Guardar directamente en la configuración maestra.
