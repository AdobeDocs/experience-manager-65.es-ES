---
title: Consideraciones y requisitos de red
description: Analiza las consideraciones de red al diseñar una implementación [!DNL Adobe Experience Manager Assets] .
contentOwner: AG
role: Architect, Admin
feature: Herramientas para desarrolladores
exl-id: 1313842c-18b1-4727-ba63-b454d0f5a2cc
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 0%

---

# [!DNL Assets] consideraciones de red {#assets-network-considerations}

Comprender su red es tan importante como comprender [!DNL Adobe Experience Manager Assets]. La red puede afectar a la carga, descarga y experiencia del usuario. La elaboración de diagramas de topología de red ayuda a identificar los puntos de interrupción y las áreas suboptimizadas de la red que debe corregir para mejorar el rendimiento de la red y la experiencia del usuario.

Asegúrese de incluir lo siguiente en el diagrama de red:

* Conectividad desde el dispositivo cliente (por ejemplo, equipo, móvil y tableta) a la red.
* Topología de la red corporativa.
* Vínculo ascendente a Internet desde la red corporativa y el entorno [!DNL Experience Manager].
* Topología del entorno [!DNL Experience Manager].
* Defina consumidores simultáneos de la interfaz de red [!DNL Experience Manager].
* Flujos de trabajo definidos de la implementación [!DNL Experience Manager].

## Conectividad desde el dispositivo cliente a la red corporativa {#connectivity-from-the-client-device-to-the-corporate-network}

Comience creando un diagrama de la conectividad entre los dispositivos cliente individuales y la red corporativa. En esta etapa, identifique los recursos compartidos, como las conexiones WiFi, en las que varios usuarios acceden al mismo punto o conmutador Ethernet para cargar y descargar recursos.

![chlimage_1-353](assets/chlimage_1-353.png)

Los dispositivos cliente se conectan a la red corporativa de varias maneras, como WiFi compartido, Ethernet a un conmutador compartido y VPN. La identificación y comprensión de los puntos de interrupción en esta red es importante para la planificación [!DNL Assets] y para modificar la red.

En la parte superior izquierda del diagrama, tres dispositivos comparten un punto de acceso WiFi de 48 Mbps. Si todos los dispositivos se cargan simultáneamente, el ancho de banda de red WiFi se comparte entre los dispositivos. En comparación con el sistema en su conjunto, un usuario puede encontrarse con un punto de estrangulamiento diferente para los tres clientes a través de este canal dividido.

Es un desafío medir la verdadera velocidad de una red WiFi porque un dispositivo lento puede afectar a otros clientes en el punto de acceso. Si planea utilizar WiFi para interacciones de recursos, realice una prueba de velocidad de varios clientes simultáneamente para evaluar el rendimiento.

La parte inferior izquierda del diagrama muestra dos dispositivos conectados a la red corporativa a través de canales independientes. Por lo tanto, cada dispositivo puede disponer de una velocidad mínima de 10 Mbps y 100 Mbps.

El equipo mostrado a la derecha tiene un flujo ascendente limitado a la red corporativa a través de una VPN con una velocidad de 1 Mbps. La experiencia del usuario para la conexión de 1Mbps es muy diferente de la experiencia del usuario en la conexión de 1Gbps. Dependiendo del tamaño de los recursos con los que los usuarios interactúan, su enlace ascendente VPN puede ser inadecuado para la tarea.

## Topología de la red corporativa {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

El diagrama muestra velocidades de enlace ascendente más altas dentro de la red corporativa que las utilizadas generalmente. Estas tuberías son recursos compartidos. Si se espera que el conmutador compartido gestione 50 clientes, puede ser un punto de interrupción. En el diagrama inicial, solo dos equipos comparten la conexión concreta.

## Vínculo ascendente a Internet desde la red corporativa y el entorno [!DNL Experience Manager] {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

Es importante tener en cuenta factores desconocidos en Internet y en la conexión VPC porque el ancho de banda en Internet puede verse afectado debido a la carga máxima o a las interrupciones del proveedor a gran escala. En general, la conectividad a Internet es fiable. Sin embargo, a veces puede introducir puntos de estrangulamiento.

En el enlace superior de una red corporativa a Internet, puede haber otros servicios usando el ancho de banda. Es importante comprender cuánto del ancho de banda se puede dedicar o priorizar para Assets. Por ejemplo, si un enlace de 1 Gbps ya se utiliza en un 80%, solo puede asignar un máximo del 20% del ancho de banda para [!DNL Experience Manager Assets].

Los firewalls y los proxies empresariales también pueden dar forma al ancho de banda de muchas maneras diferentes. Este tipo de dispositivo puede priorizar el ancho de banda mediante la calidad del servicio, las limitaciones de ancho de banda por usuario o las limitaciones de velocidad de bits por host. Estos son puntos de interrupción importantes que deben examinarse, ya que pueden afectar significativamente a la experiencia del usuario [!DNL Assets].

En este ejemplo, la empresa tiene un vínculo superior de 10 Gbps. Debería ser lo suficientemente grande para varios clientes. Además, el cortafuegos impone un límite de velocidad de host de 10 Mbps. Esta limitación puede limitar potencialmente el tráfico a un solo host a 10 Mbps, aunque el enlace ascendente a Internet sea de 10 Gbps.

Este es el punto de estrangulamiento más pequeño orientado al cliente. Sin embargo, puede evaluar un cambio o configurar una lista de permitidos con el grupo de operaciones de red a cargo de este cortafuegos.

A partir de los diagramas de ejemplo, puede concluir que seis dispositivos comparten un canal conceptual de 10 Mbps. Según el tamaño de los activos apalancados, esto puede ser inadecuado para satisfacer las expectativas del usuario.

## Topología del entorno [!DNL Experience Manager] {#topology-of-the-aem-environment}

![chlimage_1-356](assets/chlimage_1-356.png)

El diseño de la topología del entorno [!DNL Experience Manager] requiere un conocimiento detallado de la configuración del sistema y de cómo se conecta la red dentro del entorno del usuario.

El escenario de ejemplo incluye un conjunto de servidores de publicación con cinco servidores, un almacén binario S3 y Dynamic Media configurado.

Dispatcher comparte su conexión de 100 Mbps con dos entidades, el mundo exterior y la implementación [!DNL Experience Manager]. Para operaciones de carga y descarga simultáneas, debe dividir este número entre dos. El almacenamiento externo adjunto utiliza una conexión independiente.

La implementación [!DNL Experience Manager] comparte su conexión de 1 Gbps con varios servicios. Desde la perspectiva de la topología de red, equivale a compartir un solo canal con diferentes servicios.

Al revisar la red desde el dispositivo cliente hasta la implementación [!DNL Experience Manager], el punto de interrupción más pequeño parece ser el acelerador de firewall empresarial de 10 Mbit. Puede utilizar estos valores en la calculadora de tamaño de la [Guía de tamaño de los recursos](assets-sizing-guide.md) para determinar la experiencia del usuario.

## Flujos de trabajo definidos de la implementación [!DNL Experience Manager] {#defined-workflows-of-the-aem-deployment}

Al considerar el rendimiento de la red, puede ser importante tener en cuenta los flujos de trabajo y la publicación que se producirán en el sistema. Además, S3 u otro almacenamiento conectado en red que utilice y las solicitudes de E/S consumen ancho de banda de red. Por lo tanto, incluso en una red totalmente optimizada, el rendimiento puede verse limitado por la E/S de disco.

Para optimizar los procesos relacionados con la ingesta de recursos (especialmente al cargar un gran número de recursos), explore los flujos de trabajo de recursos y comprenda más información sobre su configuración.

Al evaluar la topología del flujo de trabajo interno, debe analizar lo siguiente:

* Procedimientos para escribir un activo
* Flujos de trabajo/eventos que generan déclencheur cuando se modifican recursos/metadatos
* Procedimientos para leer un activo

A continuación se presentan algunos aspectos que hay que tener en cuenta:

* XMP metadatos de lectura/escritura
* Activación y replicación automáticas
* Marcas de agua
* Ingesta de subconjuntos/extracción de páginas
* Flujos de trabajo superpuestos.

Este es un ejemplo de cliente para la definición de un flujo de trabajo de recursos.

![chlimage_1-357](assets/chlimage_1-357.png)
