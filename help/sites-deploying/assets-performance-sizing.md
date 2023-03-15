---
title: Guía de rendimiento de Assets
seo-title: Assets Performance Guide
description: Obtenga información sobre cómo determinar el tamaño de hardware óptimo para una nueva configuración de administración de activos digitales (DAM) y cómo solucionar problemas de rendimiento
seo-description: Learn how to determine the optimal hardware sizing for a new Digital Asset Management (DAM) setup and how to troubleshoot performance issues
uuid: 8291c5b9-c543-41cf-8754-445826200930
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: a79839e2-be39-418b-a3bd-f5457e555172
exl-id: fbe15e1b-830b-4752-bd02-0d239a90bc68
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 0%

---

# Guía de rendimiento de Assets{#assets-performance-guide}

La administración de recursos digitales se utiliza a menudo en casos en los que el rendimiento es importante; sin embargo, la configuración típica de DAM contiene una serie de componentes de hardware y software que pueden afectar al rendimiento. Este documento proporciona lo siguiente:

* Información para administradores de sistemas sobre cómo determinar el tamaño de hardware óptimo para una nueva configuración de administración de activos digitales
* Información para desarrolladores de software que buscan solucionar problemas de instancias de DAM con problemas de rendimiento

## Problemas de rendimiento {#performance-issues}

Un rendimiento deficiente en la administración de recursos digitales puede afectar a la experiencia del usuario de tres formas: rendimiento interactivo, procesamiento de recursos y velocidad de descarga. Para mejorar el rendimiento, es importante medir correctamente el rendimiento observado y establecer métricas objetivo.

**1. Búsqueda y exploración interactivas** Los usuarios están buscando recursos o explorando el buscador de DAM y se quejan de los tiempos de respuesta lentos o de que los resultados de la búsqueda no se muestran inmediatamente. Este es un problema de rendimiento interactivo.

El rendimiento interactivo se mide en términos de tiempo de respuesta de la página. Este es el tiempo que se tarda en recibir la solicitud HTTP en cerrar la respuesta HTTP, que se puede determinar a partir de los archivos de registro de solicitud. El rendimiento de destino típico es un tiempo de respuesta de página inferior a dos segundos.

**2. Procesamiento de recursos** AEM Un problema de procesamiento de recursos se produce cuando los usuarios cargan recursos y tardan minutos hasta que los recursos se convierten y se incorporan fácilmente en DAM de.

El rendimiento del procesamiento de recursos se mide en términos del tiempo promedio de finalización del proceso de flujo de trabajo. Este es el tiempo que se tarda en invocar el proceso de flujo de trabajo de actualización de recursos hasta su finalización, que se puede determinar desde la interfaz de usuario de los informes de flujo de trabajo. El rendimiento habitual del objetivo depende del tamaño y el tipo de recursos procesados y del número de representaciones. Algunos ejemplos de rendimiento de destino pueden ser los siguientes:

* menos de diez segundos para imágenes de menos de 1280 x 1280 píxeles con representaciones estándar
* menos de un minuto para imágenes de menos de 100 MB con representaciones estándar
* menos de cinco minutos para clips de vídeo HD de menos de un minuto

**3. Velocidad de descarga** AEM Un problema de rendimiento se produce cuando la descarga desde DAM tarda mucho tiempo y las miniaturas no se muestran inmediatamente al navegar por el administrador de DAM o el buscador de DAM.

El rendimiento se mide en términos de tasa de descarga en kilobits por segundo. El rendimiento objetivo típico es de 300 kilobits por segundo para 100 descargas simultáneas.

**4. Factores que influyen en el rendimiento del procesamiento de recursos**

Para poder calcular qué hardware necesita para procesar los recursos, es necesario tener en cuenta los siguientes aspectos:

* Resolución de las imágenes en píxeles
* AEM La pila asignada a un proceso de

La cantidad de píxeles contenidos en la imagen determina el tiempo de procesamiento: más píxeles significa que el procesamiento tarda más tiempo.
El tipo de imagen, la tasa de compresión o el tamaño relacionado del archivo en el que se almacena la imagen no influyen significativamente en el rendimiento general.

Se ha determinado que el montón es el factor limitante más importante. Siempre que el recurso supera la memoria libre disponible, el rendimiento de procesamiento disminuye rápidamente.

Los procesos DAM son adecuados para realizarse en paralelo en grandes cantidades. La carga de recursos en un lote y en procesadores de núcleo múltiple acelera el tiempo absoluto empleado por recurso.

**5. Calcular los requisitos de hardware para realizar el procesamiento de recursos**

El procesamiento extensivo de recursos digitales requiere recursos de hardware optimizados, los factores más relevantes son el tamaño de la imagen y el rendimiento máximo de las imágenes procesadas.

Asigne al menos 16 GB de pila y configure el [!UICONTROL Recurso de actualización DAM] flujo de trabajo para utilizar [paquete Camera Raw](/help/assets/camera-raw.md) para la ingesta de imágenes sin procesar.

## Explicación del sistema {#understanding-the-system}

Una configuración típica de DAM consiste en que los usuarios finales acceden a DAM a través de un equilibrador de carga. La instancia de DAM puede formar parte de una configuración agrupada, en la que cada instancia de DAM se ejecuta en un proceso de máquina virtual Java en una máquina física o virtual. El almacenamiento DAM lo proporciona un disco RAID en el caso de configuraciones de una sola máquina o un almacenamiento conectado a la red administrado en el caso de configuraciones agrupadas.

La siguiente leyenda describe las posibles áreas de escollo de rendimiento con algunas soluciones, según corresponda.

**Conexión de red con el usuario final** Una conexión de red lenta puede causar problemas de rendimiento, en algunos casos también de latencia. A veces, el usuario tiene una conexión lenta desde el ISP, especialmente en las intranets. Esto es un signo de topología de red incorrecta.

**Sistema de archivos temporal** Un sistema de archivos local lento puede causar problemas de rendimiento interactivo, especialmente cuando se trata de búsquedas, ya que los índices de búsqueda se almacenan en el disco local. Además, puede causar problemas de procesamiento de recursos si se utiliza el proceso de línea de comandos.

**AEM Buscador de DAM** Los problemas de rendimiento interactivos, que a menudo se experimentan en las búsquedas, están causados por un alto uso de CPU debido a muchos usuarios simultáneos u otros procesos que consumen CPU en la misma instancia. Pasar de máquinas virtuales a máquinas dedicadas y asegurarse de que no se ejecuten otros servicios en la máquina puede ayudar a mejorar el rendimiento. Si la carga de CPU alta se debe al procesamiento de recursos y a muchos usuarios simultáneos, Day recomienda agregar nodos de clúster adicionales.

**AEM Flujo de trabajo de DAM** Los procesos de flujo de trabajo de larga duración durante la ingesta de recursos causan problemas de rendimiento de procesamiento de recursos. Según el tipo de recursos que se procesen, esto puede indicar un uso excesivo de la CPU. Day recomienda reducir el número de otros procesos que se ejecutan en el sistema y aumentar el número de CPU disponibles agregando nodos de clúster.

**Conectividad NAS** La mala conectividad de red con el NAS causa problemas de rendimiento interactivo, ya que el acceso a los nuevos nodos durante el procesamiento de recursos se ralentiza debido a la latencia de la red. Además, el rendimiento de red lento afecta negativamente al rendimiento, pero también al rendimiento del procesamiento de recursos, porque la carga y el guardado de representaciones se ralentizan.

Las razones de la latencia y el rendimiento incorrectos en un NAS suelen ser la topología de red o la sobreutilización de NAS por otros servicios.

**Almacenamiento con conexión a red** Los sistemas de almacenamiento con conexión a red sobreutilizados pueden causar una serie de problemas:

* Un espacio en disco bajo es un problema que se encuentra con frecuencia y que se puede evitar ajustando correctamente el tamaño de un proyecto DAM.
* La latencia alta del disco se propagará a tiempos de acceso lentos para CRX y puede resultar en problemas de rendimiento interactivos.
* Un rendimiento de disco bajo puede resultar en un rendimiento bajo para CQ5 DAM.

## Pruebas de rendimiento {#testing-for-performance}

Para cada proyecto DAM, asegúrese de establecer un régimen de pruebas de rendimiento que pueda identificar y resolver cuellos de botella rápidamente. Para ello, tenga en cuenta los siguientes puntos de comprobación:

1. Pruebas de rendimiento de extremo a extremo con JMeter: simule una sesión de búsqueda y exploración de ejemplo para detectar problemas de rendimiento interactivos.
1. Pruebas de rendimiento y latencia con JMeter: la ejecución en un equipo cliente garantiza que no haya problemas relacionados con la topología.
1. Pruebas de procesamiento de recursos estandarizadas: Introduzca un pequeño número de recursos de ejemplo y mida el tiempo. Esto debe incluir la integración de flujos de trabajo externos.
1. Supervise el uso de CPU, disco y memoria de cada nodo del clúster.
1. Diagnósticos de rendimiento de lectura y escritura CRX para identificar problemas relacionados con el no procesamiento.
1. Supervise la latencia y el rendimiento de la red desde el clúster DAM a su NAS.
1. Pruebe el rendimiento de lectura y escritura, así como la latencia del disco directamente en el NAS, si es posible.

## Retorcimiento de cuellos de botella {#tweaking-bottlenecks}

Hasta ahora, se han utilizado los siguientes ajustes de rendimiento en los proyectos:

* Generación selectiva de representaciones: genere solo las representaciones que necesite añadiendo condiciones al flujo de trabajo de procesamiento de recursos, de modo que las representaciones más costosas solo se generen para los recursos seleccionados.
* Almacén de datos compartido entre instancias: cuando se agota el espacio en disco, esto puede reducir considerablemente la cantidad de espacio en disco necesario a costa de mayores esfuerzos de configuración y de perder la limpieza automática del almacén de datos.

## Lectura adicional {#further-reading}

* [Análisis de procesos lentos y bloqueados](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)
