---
title: '"Gestión de correspondencia: Resolución de problemas"'
seo-title: Solución de problemas de gestión de correspondencia
description: Solución de problemas de gestión de correspondencia
seo-description: Solución de problemas de gestión de correspondencia
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 6%

---


# Gestión de correspondencia: Solución de problemas {#correspondence-management-troubleshooting}

## Errores al guardar una carta {#errors-when-saving-a-letter}

### Problema {#issue}

Se muestra uno de los siguientes errores al guardar una carta:

* El enlace de datos no está presente para el módulo de texto
* Proporcione la información de la propiedad necesaria para lo siguiente

### Motivo {#reason}

Estos errores pueden producirse debido a uno de los siguientes factores:

* Un diccionario de datos está enlazado a la carta pero no está presente en el servidor.
* Un diccionario de datos está enlazado a la letra pero tiene un guión bajo (_) en su nombre.

### Solución {#workaround}

Asegúrese de que el diccionario de datos que está utilizando en la carta esté presente en el servidor y no tenga un guión bajo (_) en su nombre.

## Error al obtener una vista previa de una carta {#error-when-previewing-a-letter}

### Problema {#issue-1}

Al previsualizar una carta, aparece el error Error en la carta de carga: No se pudo importar el recurso desde la entrada XML&quot; aparece incluso cuando se publica un recurso de texto previamente no publicado en la carta.

### Solución {#workaround-1}

Restablezca la caché de letras en la instancia de publicación siguiendo los pasos siguientes y vuelva a intentar ver la carta:

1. Vaya a **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** e inicie sesión como administrador.
1. Seleccione **Correspondence Management Configurations**.
1. En **Configuraciones de administración de correspondencia**, deshabilite **Habilitar caché de cartas** y haga clic en **Guardar.**
1. Habilite **Habilitar caché de letras** y luego haga clic en **Guardar**.
1. Vuelva a intentar ver la carta.

