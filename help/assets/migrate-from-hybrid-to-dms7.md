---
title: 'Migración de Dynamic Media: modo híbrido a Dynamic Media: modo S7'
description: Obtenga información sobre cómo migrar su instancia de Dynamic Media - Modo híbrido a Dynamic Media - Modo S7
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: Business Practitioner, Administrator
feature: Modo Scene7,Modo híbrido
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
translation-type: tm+mt
source-git-commit: 61e703e73b831a9b4e7045e5d5fffeef5be7ed6d
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# Acerca del paso de Dynamic Media-Hybrid a Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid es una versión anterior de la integración de Dynamic Media con Adobe Experience Manager. La versión híbrida se introdujo por primera vez en AEM (Adobe Experience Manager) 6.1. Aunque el Adobe sigue admitiendo el modo híbrido, no es el modo preferido (Dynamic Media-Scene7 es el modo preferido). Tampoco admite nuevas funciones como Recorte inteligente e imágenes panorámicas. Mientras que Dynamic Media-Scene7 sí lo hace.

Entre las diferencias clave adicionales entre Dynamic Media-Hybrid y Dynamic Media-Scene7 se incluyen las siguientes:

* Estructura de las direcciones URL.
* Ingesta de vídeos.
* Creación y almacenamiento de representaciones de imágenes.
* Configuración y credenciales de Cloud (aprovisionamiento).

Hay dos opciones disponibles al pasar de Dynamic Media-Hybrid a Dynamic Media-Scene7. La primera opción es simplemente aprovisionar una nueva instancia de Dynamic Media-Scene7 en AEM. La segunda opción es migrar la instancia existente de Dynamic Media-Hybrid a Dynamic Media-Scene7. Esta opción describe, en el formulario de la tabla siguiente, los pasos y las consideraciones que debe realizar durante el desplazamiento.

>[!IMPORTANT]
>
>Adobe recomienda que no migre una implementación híbrida de Dynamic Media a Dynamic Media-Scene7 en instancias de producción activas.

## Opción 1: Aprovisionamiento de una nueva instancia de Dynamic Media-Scene7 en AEM {#provision-new-dms7}

Considere simplemente comenzar de nuevo con una nueva instancia aprovisionada de Dynamic Media-Scene7 en Adobe Experience Manager. Además de la ingesta y el procesamiento de recursos mediante Dynamic Media Cloud Service, se recomienda realizar una auditoría de Adobe del uso de recursos, los flujos de trabajo y los componentes. En muchos casos, los componentes personalizados y los flujos de trabajo se pueden sustituir por funciones nuevas integradas.

## Opción 2: Migración de la instancia existente de Dynamic Media-Hybrid a Dynamic Media-Scene7 {#process-for-migrating}

| Etapa | Tarea | Consideraciones |
|---|---|---|
| 1 | Clona la instancia de Autor híbrido de Dynamic Media. | Debe mantener la instancia existente de Dynamic Media-Hybrid Author con fines de reserva hasta que los pasos restantes de este proceso de migración se completen correctamente. |
| 2 | Inicie la instancia de Autor clonada en el modo Dynamic Media-Scene7. |  |
| 3 | En los Cloud Services de Adobe Experience Manager, configure Dynamic Media con las credenciales de Dynamic Media-Scene7. | Adobe debe aprobar el aprovisionamiento Dynamic Media-Scene7. Tendrá entornos simultáneos de Dynamic MediaM-Hybrid y Dynamic Media-Scene7 que serán compatibles durante un tiempo limitado. |
| 4 | Cree un paquete de migración para ingerir recursos según sea necesario.<br>Elimine los PTIFF locales que se crearon durante la ingesta inicial en Dynamic Media-Hybrid. | Si todos los recursos están disponibles actualmente en su instancia Dynamic Media-Hybrid, un clon de que ya los incluye a todos. Por lo tanto, no se necesita ningún paquete. |
| 5 | Ejecute el flujo de trabajo de actualización de recursos para sincronizar recursos con el Cloud Service de Dynamic Media. | Adobe recomienda que el flujo de trabajo de actualización se realice por lotes para permitir la compactación. |
| 6 | Migre los ajustes preestablecidos de visor, imagen y vídeo. |  |
| 7 | Vaya por cada recurso al que se hace referencia en la Administración de contenido web y actualice sus direcciones URL asociadas. |  |
| 8 | Migre cualquier flujo de trabajo personalizado para admitir el nuevo modo Dynamic Media-Scene7 (actualizaciones manuales). |  |
| 9 | Compruebe la carga y la configuración de la administración de contenido web. |  |
| 10 | Después de la verificación, obtenga una aprobación para deshabilitar Dynamic Media-Hybrid Author (mantenga como una visita en el orden previsto). |  |
| 11 | Elimine la instancia Dynamic Media-Hybrid Author después de aproximadamente un mes de uso correcto de Dynamic Media-Scene7. |  |
