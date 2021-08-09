---
title: 'Migración de Dynamic Media: modo híbrido a Dynamic Media: modo S7'
description: Obtenga información sobre cómo migrar su instancia de Dynamic Media - Modo híbrido a Dynamic Media - Modo S7
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Modo Scene7,Modo híbrido
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 2%

---

# Acerca del paso de Dynamic Media-Hybrid a Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid es una versión anterior de la integración de Dynamic Media con Adobe Experience Manager. La versión híbrida se introdujo por primera vez en Adobe Experience Manager 6.1. Aunque el Adobe sigue admitiendo el modo híbrido, no es el modo preferido; Dynamic Media-Scene7 es el modo preferido para usar. El modo híbrido tampoco admite nuevas funciones como Recorte inteligente e imágenes panorámicas, mientras que Dynamic Media-Scene7 sí las admite.

Entre las diferencias clave adicionales entre Dynamic Media-Hybrid y Dynamic Media-Scene7 se incluyen las siguientes:

* Estructura de las direcciones URL.
* Ingesta de vídeos.
* Creación y almacenamiento de representaciones de imágenes.
* Configuración y credenciales de Cloud (aprovisionamiento).

Hay dos opciones disponibles al pasar de Dynamic Media-Hybrid a Dynamic Media-Scene7. La primera opción es simplemente aprovisionar una nueva instancia de Dynamic Media-Scene7 en el Experience Manager. La segunda opción es migrar la instancia existente de Dynamic Media-Hybrid a Dynamic Media-Scene7. Esta opción describe, en el formulario de la tabla siguiente, los pasos y las consideraciones que debe realizar durante el desplazamiento.

>[!IMPORTANT]
>
>Adobe recomienda que no migre una implementación híbrida de Dynamic Media a Dynamic Media-Scene7 en instancias de producción activas.

## Opción 1: Aprovisionar una nueva instancia de Dynamic Media-Scene7 en el Experience Manager {#provision-new-dms7}

Considere simplemente comenzar de nuevo con una nueva instancia aprovisionada de Dynamic Media-Scene7 en Adobe Experience Manager. Además de la ingesta y el procesamiento de recursos mediante Dynamic Media Cloud Service, se recomienda realizar una auditoría de Adobe del uso de recursos, los flujos de trabajo y los componentes. A menudo, puede reemplazar componentes personalizados y flujos de trabajo mediante el uso de funciones nuevas integradas.

## Opción 2: Migre la instancia existente de Dynamic Media-Hybrid a Dynamic Media-Scene7 {#process-for-migrating}

| Etapa | Tarea | Consideraciones |
|---|---|---|
| 1 | Clona la instancia de Autor híbrido de Dynamic Media. | Mantenga la instancia existente de Dynamic Media-Hybrid Author con fines de reserva hasta que los pasos restantes de este proceso de migración se completen correctamente. |
| 2 | Inicie la instancia de Autor clonada en el modo Dynamic Media-Scene7. |  |
| 3 | En los Cloud Services de Adobe Experience Manager, configure Dynamic Media con las credenciales de Dynamic Media-Scene7. | Adobe debe aprobar el aprovisionamiento Dynamic Media-Scene7. Como tal, tiene entornos dinámicos MediaM-híbridos y Dynamic Media-Scene7 simultáneos compatibles con el Adobe, pero solo durante un tiempo limitado. |
| 4 | Cree un paquete de migración para que pueda ingerir los recursos según sea necesario.<br>Elimine los PTIFF locales que se crearon durante la ingesta inicial en Dynamic Media-Hybrid. | Si todos los recursos están disponibles actualmente en su instancia Dynamic Media-Hybrid, un clon de que ya los incluye a todos. Por lo tanto, no se necesita ningún paquete. |
| 5 | Ejecute el flujo de trabajo de actualización de recursos para poder sincronizar recursos con el Cloud Service de Dynamic Media. | Adobe recomienda realizar el flujo de trabajo de actualización en lotes para permitir la compactación. |
| 6 | Migre los ajustes preestablecidos de visor, imagen y vídeo. |  |
| 7 | Vaya por cada recurso al que se hace referencia en la Administración de contenido web y actualice sus direcciones URL asociadas. |  |
| 8 | Migre cualquier flujo de trabajo personalizado que desee que admita el nuevo modo Dynamic Media-Scene7 (actualizaciones manuales). |  |
| 9 | Compruebe la carga y la configuración de la administración de contenido web. |  |
| 10 | Después de la verificación, obtenga una aprobación para deshabilitar Dynamic Media-Hybrid Author (mantenga como alternativa). |  |
| 11 | Elimine la instancia Dynamic Media-Hybrid Author después de aproximadamente un mes de uso correcto de Dynamic Media-Scene7. |  |
