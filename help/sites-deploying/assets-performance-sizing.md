---
title: Guía de rendimiento de recursos
seo-title: Assets Performance Guide
description: Obtenga información sobre cómo determinar el tamaño de hardware óptimo para una nueva configuración de la administración de activos digitales (DAM) y cómo solucionar problemas de rendimiento
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

# Guía de rendimiento de recursos{#assets-performance-guide}

La administración de activos digitales se utiliza a menudo en casos en que el rendimiento es importante; sin embargo, la configuración típica de DAM contiene varios componentes de hardware y software que pueden afectar al rendimiento. Este documento proporciona lo siguiente:

* Información para administradores de sistemas sobre cómo determinar el tamaño de hardware óptimo para una nueva configuración de la administración de activos digitales
* Información para desarrolladores de software que buscan solucionar problemas de instancias DAM con problemas de rendimiento

## Problemas de rendimiento {#performance-issues}

Un rendimiento deficiente en la administración de recursos digitales puede afectar a la experiencia del usuario de tres maneras: rendimiento interactivo, procesamiento de recursos y velocidad de descarga. Para mejorar el rendimiento, es importante medir el rendimiento observado correctamente y establecer métricas de objetivo.

**1. Búsqueda y exploración interactivas** Los usuarios están buscando recursos o explorando el buscador de DAM y se quejan de los tiempos de respuesta lentos o de que los resultados de búsqueda no aparecen inmediatamente. Este es un problema de rendimiento interactivo.

El rendimiento interactivo se mide en términos del tiempo de respuesta de la página. Este es el tiempo que se tarda en recibir la solicitud HTTP para cerrar la respuesta HTTP, que se puede determinar a partir de los archivos de registro de la solicitud. El rendimiento típico del objetivo es un tiempo de respuesta de página inferior a dos segundos.

**2. Procesamiento de recursos** Un problema con el procesamiento de recursos es cuando los usuarios cargan recursos y tardan minutos en convertirse e ingerirse fácilmente en AEM DAM.

El rendimiento del procesamiento de recursos se mide en términos del tiempo promedio de finalización del proceso del flujo de trabajo. Este es el tiempo que tarda desde invocar el proceso de flujo de trabajo de actualización de recursos hasta su finalización, que se puede determinar desde la interfaz de usuario de informes de flujo de trabajo. El rendimiento típico de los objetivos depende del tamaño y el tipo de recursos procesados y del número de representaciones. Los ejemplos de rendimiento de destino podrían ser los siguientes:

* menos de diez segundos para imágenes menores de 1280 x 1280 píxeles con representaciones estándar
* menos de un minuto para imágenes menores de 100 MB que utilizan representaciones estándar
* menos de cinco minutos para clips de vídeo HD de menos de un minuto

**3. Velocidad de descarga** Un problema de rendimiento se produce cuando la descarga desde AEM DAM tarda mucho y las miniaturas no aparecen inmediatamente al examinar el administrador de DAM o el buscador de DAM.

El rendimiento del rendimiento de rendimiento se mide en términos de la tasa de descarga en kilobits por segundo. El rendimiento típico de Target es de 300 kilobits por segundo para 100 descargas simultáneas.

**4. Factores que influyen en el rendimiento del procesamiento de recursos**

Para poder estimar qué hardware necesita para procesar los activos, es necesario tener en cuenta los siguientes aspectos:

* Resolución de las imágenes en píxeles
* La pila asignada a AEM proceso

La cantidad de píxeles contenidos en la imagen determina el tiempo de procesamiento: más píxeles significa que el procesamiento tarda más tiempo.
El tipo de imagen, la tasa de compresión o el tamaño relacionado del archivo en el que se almacena la imagen no influye significativamente en el rendimiento general.

Se ha determinado que el montón es el factor limitante más importante. Siempre que el recurso supera la memoria libre disponible, el rendimiento de procesamiento disminuye rápidamente.

Los procesos DAM son ideales para su realización en paralelo en grandes cantidades. La carga de recursos en un lote y en procesadores de núcleo múltiple acelera el tiempo absoluto empleado por recurso.

**5. Calcular los requisitos de hardware para realizar el procesamiento de recursos**

El procesamiento extensivo de recursos digitales requiere recursos de hardware optimizados, los factores más relevantes son el tamaño de la imagen y el rendimiento máximo de las imágenes procesadas.

Asigne al menos 16 GB de memoria y configure la variable [!UICONTROL Recurso de actualización DAM] flujo de trabajo para usar la variable [paquete Camera Raw](/help/assets/camera-raw.md) para la ingesta de imágenes sin procesar.

## Explicación del sistema {#understanding-the-system}

Una configuración típica de DAM consiste en usuarios finales que acceden a DAM mediante un equilibrador de carga. La instancia de DAM puede formar parte de una configuración agrupada, en la que cada instancia de DAM se ejecuta en un proceso de máquina virtual Java en una máquina física o una máquina virtual. El almacenamiento DAM se proporciona mediante un disco RAID en casos de configuraciones de una sola máquina o de almacenamiento conectado a una red administrada en caso de configuraciones en clúster.

La leyenda siguiente describe las posibles áreas de riesgo de rendimiento con algunas soluciones, según corresponda.

**Conexión de red al usuario final** Una conexión de red lenta puede causar problemas de rendimiento, en algunos casos también problemas de latencia. A veces, el usuario tiene una conexión lenta desde el ISP, especialmente en los intranets. Es un signo de topología de red incorrecta.

**Sistema de archivos temporales** Un sistema de archivos local lento puede causar problemas de rendimiento interactivos, especialmente cuando se trata de buscar, ya que los índices de búsqueda se almacenan en el disco local. Además, puede causar problemas de procesamiento de recursos si se está utilizando el proceso de línea de comandos.

**Buscador AEM DAM** Los problemas interactivos de rendimiento, que a menudo se experimentan en las búsquedas, son causados por la alta utilización de la CPU debido a muchos usuarios simultáneos u otros procesos que consumen CPU en la misma instancia. Pasar de máquinas virtuales a máquinas dedicadas y asegurarse de que no se ejecutan otros servicios en la máquina puede ayudar a mejorar el rendimiento. Si la carga de CPU es alta debido al procesamiento de recursos y a muchos usuarios simultáneos, Day recomienda agregar nodos de clúster adicionales.

**Flujo de trabajo AEM DAM** Los procesos de flujo de trabajo de larga duración durante la ingesta de recursos causan problemas de rendimiento en el procesamiento de recursos. Según el tipo de recursos que se procesen, esto puede indicar una sobreutilización de la CPU. Day recomienda reducir el número de otros procesos que se ejecutan en el sistema y aumentar el número de CPU disponibles añadiendo nodos de clúster.

**Conectividad NAS** La mala conectividad de red con NAS causa problemas interactivos de performance, ya que el acceso a nuevos nodos durante el procesamiento de recursos se ralentiza debido a la latencia de la red. Además, el rendimiento lento de la red afecta negativamente al rendimiento, pero también al rendimiento del procesamiento de recursos, ya que la carga y el guardado de representaciones se ralentizan.

Las razones para una mala latencia y rendimiento en un NAS son generalmente la topología de red o la sobreutilización de NAS por otros servicios.

**Almacenamiento conectado en red** Los sistemas de almacenamiento de información conectado en red que se utilizan en exceso pueden causar una serie de problemas:

* El espacio en disco bajo es un problema que se encuentra con frecuencia y que se puede prevenir mediante el tamaño adecuado de un proyecto DAM.
* La latencia de alto disco se propagará a tiempos de acceso lentos para CRX y puede causar problemas interactivos de rendimiento.
* El bajo rendimiento del disco puede resultar en un bajo rendimiento para CQ5 DAM.

## Pruebas para el rendimiento {#testing-for-performance}

Para cada proyecto DAM, asegúrese de establecer un régimen de pruebas de rendimiento que pueda identificar y resolver los cuellos de botella rápidamente. Para ello, tenga en cuenta los siguientes puntos de comprobación:

1. Pruebas de rendimiento end-to-end utilizando JMeter : Simule una sesión de búsqueda y exploración de ejemplo para detectar problemas interactivos de rendimiento.
1. Pruebas de rendimiento y latencia utilizando JMeter: la ejecución en un equipo cliente garantiza que no haya problemas relacionados con la topología.
1. Pruebas de procesamiento de recursos estandarizadas: incorpore un número reducido de recursos de ejemplo y mida el tiempo. Esto debe incluir la integración de flujo de trabajo externo.
1. Monitorice la utilización de CPU, disco y memoria de cada nodo de cluster.
1. Diagnósticos de rendimiento de lectura y escritura CRX para identificar los problemas relacionados con el no procesamiento.
1. Monitorice la latencia y el rendimiento de la red desde el cluster DAM a su NAS.
1. Pruebe el performance de lectura y escritura, así como la latencia de disco directamente en el NAS, si es posible.

## Cuellos de botella de tejido {#tweaking-bottlenecks}

Hasta ahora, se han utilizado los siguientes ajustes de rendimiento en los proyectos:

* Generación selectiva de representaciones: genere únicamente las representaciones que necesite añadiendo condiciones al flujo de trabajo del procesamiento de recursos, de modo que solo se generen representaciones más costosas para determinados recursos.
* Almacenamiento de datos compartidos entre instancias: cuando el espacio en disco es bajo, esto puede reducir considerablemente la cantidad de espacio en disco necesario a costa de mayores esfuerzos de configuración y perder la limpieza automática del almacén de datos.

## Lectura adicional {#further-reading}

* [Análisis de procesos lentos y bloqueados](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)
