---
title: 'Migración desde Dynamic Media: modo híbrido a Dynamic Media: modo S7'
description: 'Obtenga información sobre cómo migrar su instancia de Dynamic Media: modo híbrido a modo Dynamic Media - S7'
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: f466193a259d9e8869d7f79eafda1be20869e4af
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---


# Acerca del cambio de Dynamic Media-Hybrid a Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid es una versión anterior de la integración de Dynamic Media con Adobe Experience Manager. La versión híbrida se introdujo por primera vez en AEM (Adobe Experience Manager) 6.1. Aunque Adobe sigue admitiendo el modo híbrido, no es el modo preferido (Dynamic Media-Scene7 es el modo preferido). Tampoco admite nuevas características como Recorte inteligente e imágenes panorámicas. Mientras que Dynamic Media-Scene7 sí.

Entre las diferencias clave adicionales entre Dynamic Media-Hybrid y Dynamic Media-Scene7 se incluyen las siguientes:

* Estructura de las direcciones URL.
* Ingesta de vídeos.
* Creación y almacenamiento de representaciones de imágenes.
* Configuración y credenciales de la nube (aprovisionamiento).

Hay dos opciones disponibles al pasar de Dynamic Media-Hybrid a Dynamic Media-Scene7. La primera opción es simplemente aprovisionar una nueva instancia de Dynamic Media-Scene7 en AEM. La segunda opción es migrar la instancia existente de Dynamic Media-Hybrid a Dynamic Media-Scene7. Esta opción describe los pasos y las consideraciones que debe realizar durante el movimiento, en el formulario de tabla que se encuentra debajo.

>[!IMPORTANT]
>
>Adobe recomienda que no migre una implementación Dynamic Media-Hybrid a Dynamic Media-Scene7 en instancias de producción en directo.

## Opción 1: Aprovisionamiento de una nueva instancia de Dynamic Media-Scene7 en AEM {#provision-new-dms7}

Considere simplemente empezar de nuevo con una nueva instancia aprovisionada de Dynamic Media-Scene7 en Adobe Experience Manager. Además de la ingestión y el procesamiento de los activos por medio de Dynamic Media Cloud Service, se recomienda realizar una auditoría de Adobe del uso de los recursos, los flujos de trabajo y los componentes. En muchos casos, los componentes y flujos de trabajo personalizados se pueden reemplazar con funciones nuevas integradas.

## Opción 2: Migración de la instancia existente de Dynamic Media-Hybrid a Dynamic Media-Scene7 {#process-for-migrating}

| Etapa | Tarea | Consideraciones |
|---|---|---|
| 1 | Clonar instancia de Dynamic Media-Hybrid Author. | Debe mantener la instancia existente de Dynamic Media-Hybrid Author por motivos de reserva hasta que los pasos restantes de este proceso de migración se completen correctamente. |
| 2 | Inicio clonó la instancia de Author en el modo Dynamic Media-Scene7. |  |
| 3 | En Cloud Services de Adobe Experience Manager, configure Dynamic Media con las credenciales de Dynamic Media-Scene7. | Adobe debe aprobar el aprovisionamiento Dynamic Media-Scene7. Tendrá entornos dinámicos mixtos de Dynamic MediaM y Dynamic Media-Scene7 que se admitirán durante un tiempo limitado. |
| 4 | Cree un paquete de migración para ingestar recursos según sea necesario.<br>Elimine los PTIFF locales que se crearon durante la ingestión inicial en Dynamic Media-Hybrid. | Si todos los recursos están disponibles actualmente en la instancia de Dynamic Media-Hybrid, un clon ya los incluye a todos. Por lo tanto, no se necesita ningún paquete. |
| 5 | Ejecute el flujo de trabajo de actualización de recursos para sincronizar los recursos con Dynamic Media Cloud Service. | Adobe recomienda que el flujo de trabajo de actualización se realice por lotes para permitir la compactación. |
| 6 | Migrar ajustes preestablecidos de visor, imagen y vídeo. |  |
| 7 | Vaya a los recursos a los que hace referencia el Gestor de contenido Web y actualice las direcciones URL asociadas. |  |
| 8 | Migrar cualquier flujos de trabajo personalizado para admitir el nuevo modo Dynamic Media-Scene7 (actualizaciones manuales). |  |
| 9 | Compruebe la carga y la configuración del Gestor de contenido web. |  |
| 10 | Después de la verificación, obtenga una aprobación para deshabilitar Dynamic Media-Hybrid Author (mantener como una devolución). |  |
| 11 | Elimine la instancia de Dynamic Media-Hybrid Author después de aproximadamente un mes de uso correcto de Dynamic Media-Scene7. |  |
