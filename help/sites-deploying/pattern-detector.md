---
title: Evaluación de la complejidad de la actualización con el detector de patrones
seo-title: Evaluación de la complejidad de la actualización con el detector de patrones
description: Aprenda a utilizar el detector de patrones para evaluar la complejidad de la actualización.
seo-description: Aprenda a utilizar el detector de patrones para evaluar la complejidad de la actualización.
uuid: 84d0add9-3123-4188-9877-758911b1899f
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: b5607343-a13b-4520-a771-f1a555bfcc7b
docset: aem65
translation-type: tm+mt
source-git-commit: ba7ac70858b7b2fd610d63355a22a69c3a7586e3
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 1%

---


# Evaluación de la complejidad de la actualización con el detector de patrones

## Información general {#overview}

Esta función le permite comprobar la capacidad de actualización de las instancias de AEM existentes mediante la detección de patrones en uso que:

1. Violar ciertas reglas y se realizan en áreas que se verán afectadas o sobrescritas por la actualización
1. Utilice una función AEM 6.x o una API que no sea compatible con versiones anteriores en AEM 6.5 y que pueda romperse tras la actualización.

Esto podría servir como una evaluación de las actividades de desarrollo que entrañan la mejora a la AEM 6.5.

## Configuración {#how-to-set-up}

El detector de patrones se libera por separado como [un paquete](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/compatpack/pd-all-aem65) que funciona en cualquier versión de origen AEM de 6.1 a 6.5 que tenga como objetivo AEM actualización 6.5. Se puede instalar mediante el [Administrador de paquetes](/help/sites-administering/package-manager.md).

## Usos {#how-to-use}

>[!NOTE]
>
>El detector de patrones se puede ejecutar en cualquier entorno, incluidas las instancias de desarrollo local. Sin embargo, para:
>
>* aumentar la velocidad de detección
>* evitar cualquier desaceleración en instancias críticas del negocio

>
>
al mismo tiempo, se recomienda ejecutarlo **en entornos de ensayo** que estén lo más cerca posible de los de producción en las áreas de aplicaciones de usuario, contenido y configuraciones.

Puede utilizar varios métodos para comprobar la salida del detector de patrones:

* **A través de la consola de Felix Inventory:**

1. Vaya a la consola web de AEM navegando a *https://serveraddress:serverport/system/console/configMgr*
1. Seleccione **Estado - Detector de patrones** como se muestra en la siguiente imagen:

   ![captura de pantalla: detector de patrones 2-5-2-2018](assets/screenshot-2018-2-5pattern-detector.png)

* **Mediante una interfaz JSON normal o basada en texto reactivo**
* **Mediante una interfaz de líneas JSON reactiva, **que genera un documento JSON independiente en cada línea.

Ambos métodos se detallan a continuación:

## Interfaz reactiva {#reactive-interface}

La interfaz reactiva permite el procesamiento del informe de infracción tan pronto como se detecta una sospecha.

El resultado está disponible actualmente en 2 direcciones URL:

1. Interfaz de texto sin formato
1. Interfaz JSON

## Administración de la interfaz de texto sin formato {#handling-the-plain-text-interface}

La información del resultado tiene un formato de serie de entradas de evento. Hay dos canales: uno para publicar infracciones y otro para publicar el progreso actual.

Se pueden obtener mediante los siguientes comandos:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

El resultado será el siguiente:

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

El progreso se puede filtrar mediante el comando `grep`:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

El resultado es el siguiente:

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## Gestión de la interfaz JSON {#handling-the-json-interface}

Del mismo modo, JSON puede procesarse con la [herramienta jq](https://stedolan.github.io/jq/) tan pronto como se publique.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

Con el resultado:

```
{
  "timestamp": "2018-02-13T14:20:18.894+01:00",
  "suspicion": true,
  "pattern": {
    "code": "ECU",
    "type": "extraneous.content.usage",
    "detective": "ContentAccessDetector",
    "moreInfo": "https://www.adobe.com/go/aem6_ECU"
  },
  "item": {
    "id": "a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f",
    "message": "Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid"
  }
}
```

El progreso se informa cada 5 segundos y se puede recuperar excluyendo otros mensajes que no sean los marcados como sospechas:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

Con el resultado:

```
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:17.279+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 57209,
    "itemsAnalysedSize": "26 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT5.003S",
    "elapsedTimeMilliseconds": 5003,
    "itemsPerSecond": 36965
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:22.276+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 113194,
    "itemsAnalysedSize": "46 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT10S",
    "elapsedTimeMilliseconds": 10000,
    "itemsPerSecond": 24092
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:25.762+01:00",
  "type": "FINISHED",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 140744,
    "itemsAnalysedSize": "63 MB",
    "suspicionsFound": 1
  },
  "progress": {
    "elapsedTime": "PT13.486S",
    "elapsedTimeMilliseconds": 13486,
    "itemsPerSecond": 19907
  }
}
{
  "suspicion": false,
  "type": "SUMMARY",
  "suspicionsFound": 1,
  "totalTime": "PT13.487S"
}
```

>[!NOTE]
>
>El método recomendado es guardar todo el resultado de curl en el archivo y luego procesarlo mediante `jq` o `grep` para filtrar el tipo de información.

## Ámbito de detección {#scope}

El detector de patrones actual permite comprobar:

* Los paquetes OSGi exportan e importan no coinciden
* Creación de supertipos y tipos de recursos (con superposiciones de contenido de ruta de búsqueda)
* definiciones de índices Oak (compatibilidad)
* Paquetes VLT (sobreutilización)
* rep:Compatibilidad de nodos de usuario (en el contexto de la configuración de OAuth)

>[!NOTE]
>
>Tenga en cuenta que el Detector de patrones intenta predecir con precisión las advertencias de actualización. Sin embargo, puede generar falsos positivos en algunos casos.
