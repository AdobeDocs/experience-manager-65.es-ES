---
title: Guía de rendimiento de recursos
seo-title: Guía de rendimiento de recursos
description: Descubra cómo determinar el tamaño de hardware óptimo para una nueva configuración de Digital Asset Management (DAM) y cómo solucionar problemas de rendimiento
seo-description: Descubra cómo determinar el tamaño de hardware óptimo para una nueva configuración de Digital Asset Management (DAM) y cómo solucionar problemas de rendimiento
uuid: 8291c5b9-c543-41cf-8754-445826200930
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: a79839e2-be39-418b-a3bd-f5457e555172
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 0%

---


# Guía de rendimiento de recursos{#assets-performance-guide}

La gestión de activos digitales se utiliza con frecuencia en los casos en que el rendimiento es importante; sin embargo, la configuración típica de DAM contiene una serie de componentes de hardware y software que pueden afectar al rendimiento. Este documento proporciona lo siguiente:

* Información para los administradores de sistemas sobre cómo determinar el tamaño de hardware óptimo para una nueva configuración de Digital Asset Management
* Información para desarrolladores de software que buscan solucionar problemas de las instancias de DAM con problemas de rendimiento

## Problemas de rendimiento {#performance-issues}

El rendimiento deficiente en la administración de recursos digitales puede afectar a la experiencia del usuario de tres maneras: rendimiento interactivo, procesamiento de recursos y velocidad de descarga. Para mejorar el rendimiento, es importante medir el rendimiento observado correctamente y establecer métricas de destinatario.

**1. Búsqueda y exploración interactivas** Los usuarios buscan recursos o exploran el Buscador de DAM y se quejan de los tiempos de respuesta lentos o de que los resultados de búsqueda no se muestran inmediatamente. Se trata de un problema de rendimiento interactivo.

El rendimiento interactivo se mide en términos del tiempo de respuesta de la página. Este es el tiempo que transcurre desde la recepción de la solicitud HTTP hasta el cierre de la respuesta HTTP, que se puede determinar a partir de los archivos de registro de la solicitud. El rendimiento de destinatario típico es un tiempo de respuesta de página inferior a dos segundos.

**2. Procesamiento de recursos** Un problema de procesamiento de recursos se produce cuando los usuarios cargan recursos y tarda unos minutos en convertirse los recursos e ingerirlos fácilmente en AEM DAM.

El rendimiento del procesamiento de recursos se mide en términos del tiempo medio de finalización del proceso de flujo de trabajo. Este es el tiempo que tarda desde invocar el proceso de flujo de trabajo de actualización de recursos hasta su finalización, que se puede determinar desde la interfaz de usuario de los informes de flujo de trabajo. El rendimiento típico del destinatario depende del tamaño y el tipo de recursos procesados y del número de representaciones. Los ejemplos de rendimiento de destinatarios podrían ser los siguientes:

* menos de diez segundos para imágenes menores de 1280 x 1280 píxeles que utilizan representaciones estándar
* menos de un minuto para imágenes menores de 100 MB que utilizan representaciones estándar
* menos de cinco minutos para clips de vídeo HD de menos de un minuto

**3. Velocidad de descarga** Un problema de rendimiento se produce al descargar desde AEM DAM lleva mucho tiempo y las miniaturas no se muestran inmediatamente al explorar el Administrador de DAM o el Buscador de DAM.

El rendimiento del rendimiento del rendimiento se mide en términos de velocidad de descarga en kilobits por segundo. El rendimiento típico del destinatario es de 300 kilobits por segundo para 100 descargas simultáneas.

**4. Factores que influyen en el rendimiento del procesamiento de recursos**

Para poder calcular el hardware necesario para procesar los recursos, es necesario tener en cuenta los siguientes aspectos:

* Resolución de las imágenes en cantidad de píxeles
* El montón asignado a AEM proceso

La cantidad de píxeles que contiene la imagen determina el tiempo de procesamiento; más píxeles significa que el procesamiento tarda más tiempo.
El tipo de imagen, la velocidad de compresión o el tamaño relacionado del archivo en el que se almacena la imagen no influye significativamente en el rendimiento global.

Se ha determinado que el montón es el factor limitante más importante. Siempre que el recurso supere la memoria libre disponible, el rendimiento de procesamiento se reduce rápidamente.

Los procesos DAM están bien adaptados para ser ejecutados en paralelo en grandes cantidades. La carga de recursos en un lote y en procesadores de varios núcleos acelera el tiempo absoluto empleado por recurso.

**5. Estimación de los requisitos de hardware para el procesamiento de recursos**

El procesamiento extensivo de recursos digitales requiere recursos de hardware optimizados, los factores más relevantes son el tamaño de la imagen y el rendimiento máximo de las imágenes procesadas.

Asigne al menos 16 GB de pila y configure el [!UICONTROL recurso de actualización de DAM] flujo de trabajo para utilizar el [paquete Camera Raw](/help/assets/camera-raw.md) para la ingestión de imágenes sin procesar.

## Explicación del sistema {#understanding-the-system}

Una configuración DAM típica consiste en usuarios finales que acceden a DAM mediante un equilibrador de carga. La instancia de DAM puede formar parte de una configuración agrupada, donde cada instancia de DAM se ejecuta en un proceso de máquina virtual Java en una máquina física o una máquina virtual. El almacenamiento DAM lo proporciona un disco RAID en casos de configuración de una sola máquina o un almacenamiento de conexión de red administrado en caso de configuración en clúster.

La leyenda siguiente describe las posibles áreas de riesgo de rendimiento con algunas soluciones, según corresponda.

**Conexión de red al** usuario finalUna conexión de red lenta puede causar problemas de rendimiento, en algunos casos también problemas de latencia. A veces el usuario tiene una conexión lenta del ISP, especialmente en intranets. Es un signo de topología de red incorrecta.

**Sistema** de archivos temporalUn sistema de archivos local lento puede causar problemas de rendimiento interactivos, especialmente cuando se trata de buscar, ya que los índices de búsqueda se almacenan en el disco local. Además, puede causar problemas de procesamiento de recursos si se utiliza el proceso de la línea de comandos.

**AEM DAM** FinderLos problemas de rendimiento interactivos, que a menudo se experimentan en las búsquedas, se deben a la alta utilización de la CPU debido a que muchos usuarios simultáneos u otros procesos que consumen CPU en la misma instancia. Pasar de las máquinas virtuales a las máquinas dedicadas y asegurarse de que ningún otro servicio se ejecute en la máquina puede ayudar a mejorar el rendimiento. Si la carga de CPU es alta debido al procesamiento de recursos y a muchos usuarios simultáneos, Day recomienda agregar nodos de clúster adicionales.

**AEM** Flujo de trabajo DAMLos procesos de flujo de trabajo de larga duración durante la ingesta de recursos causan problemas de rendimiento de procesamiento de recursos. Según el tipo de recursos que se procesen, esto puede indicar una sobreutilización de la CPU. Day recomienda reducir el número de otros procesos que se ejecutan en el sistema y aumentar el número de CPU disponibles agregando nodos de clúster.

**Conectividad** de NAS La conectividad deficiente de la red con NAS causa problemas de performance interactivos, ya que el acceso a nuevos nodos durante el procesamiento de recursos se ralentiza debido a la latencia de la red. Además, el lento rendimiento de la red afecta negativamente al rendimiento, pero también al rendimiento del procesamiento de recursos, ya que la carga y el almacenamiento de las representaciones se ralentizan.

Las razones para una mala latencia y rendimiento en un NAS son generalmente la topología de red o la sobreutilización de NAS por parte de otros servicios.

**Almacenamiento conectado** a la redLos sistemas de almacenamiento conectado a la red sobreutilizados pueden causar una serie de problemas:

* El espacio en disco reducido es un problema que se puede evitar con frecuencia a través del tamaño adecuado de un proyecto DAM.
* La latencia de disco alto se propagará a los tiempos de acceso lento para CRX y puede provocar problemas de rendimiento interactivos.
* El bajo rendimiento del disco puede resultar en un bajo rendimiento para CQ5 DAM.

## Prueba para el rendimiento {#testing-for-performance}

Para cada proyecto DAM, asegúrese de establecer un régimen de pruebas de rendimiento que pueda identificar y resolver rápidamente los cuellos de botella. Para ello, considere los siguientes puntos de comprobación:

1. Pruebas de rendimiento end-to-end con JMeter: simule una sesión de búsqueda y exploración de ejemplo para detectar problemas de rendimiento interactivos.
1. Pruebas de latencia y rendimiento mediante JMeter: la ejecución en un equipo cliente garantiza que no haya problemas relacionados con la topología.
1. Pruebas de procesamiento de recursos estandarizadas: ingrese un pequeño número de recursos de ejemplo y mida el tiempo. Esto debe incluir la integración de flujos de trabajo externos.
1. Monitoree la utilización de CPU, disco y memoria de cada nodo de clúster.
1. Diagnósticos de rendimiento de lectura y escritura de CRX para identificar problemas no relacionados con el procesamiento.
1. Monitoree la latencia y el rendimiento de la red desde el cluster DAM a su NAS.
1. Pruebe el performance de lectura y escritura, así como la latencia del disco directamente en el NAS, si es posible.

## Cuellos de botella de tejido {#tweaking-bottlenecks}

Hasta ahora, se han utilizado los siguientes ajustes de rendimiento en los proyectos:

* Generación selectiva de representaciones: solo genere las representaciones que necesite agregando condiciones al flujo de trabajo de procesamiento de recursos, de modo que las representaciones más costosas solo se generen para los recursos seleccionados.
* Almacén de datos compartidos entre instancias: cuando el espacio en disco es reducido, esto puede reducir considerablemente la cantidad de espacio en disco necesario a costa de mayores esfuerzos de configuración y perder la limpieza automática del almacén de datos.

## Lectura adicional {#further-reading}

* [Análisis de procesos lentos y bloqueados](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

