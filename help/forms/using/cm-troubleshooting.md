---
title: '"Gestión de la correspondencia: Resolución de problemas"'
seo-title: Resolución de problemas de la administración de correspondencia
description: Resolución de problemas de la administración de correspondencia
seo-description: Resolución de problemas de la administración de correspondencia
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 5%

---


# Administración de correspondencia: Solución de problemas {#correspondence-management-troubleshooting}

## Errores al guardar una carta {#errors-when-saving-a-letter}

### Problema {#issue}

Se muestra uno de los siguientes errores al guardar una carta:

* Enlace de datos no presente para el módulo de texto
* Proporcione la información de la propiedad necesaria para lo siguiente

### Motivo {#reason}

Estos errores se pueden producir debido a uno de los siguientes factores:

* Un diccionario de datos está enlazado a la letra pero no está presente en el servidor.
* Un diccionario de datos está enlazado a la letra pero tiene un guión bajo (_) en su nombre.

### Solución alternativa {#workaround}

Asegúrese de que el diccionario de datos que está utilizando en la carta está presente en el servidor y no tiene un guión bajo (_) en su nombre.

## Error al obtener la vista previa de una letra {#error-when-previewing-a-letter}

### Problema {#issue-1}

Al obtener la vista previa de una carta, aparece el error &quot;Error en la carta de carga: No se pudo importar el recurso desde la entrada XML&quot; aparece incluso cuando se publica un recurso de texto sin publicar previamente en la carta.

### Solución alternativa {#workaround-1}

Restaure la caché de letras en la instancia de publicación siguiendo los pasos siguientes y vuelva a intentar ver la letra:

1. Vaya a **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** e inicie sesión como administrador.
1. Seleccione **Configuraciones de administración de correspondencia**.
1. En **Configuraciones de administración de correspondencia**, deshabilite **Habilitar caché de letras** y haga clic en **Guardar.**
1. Habilite **Habilitar caché de letras** y luego haga clic en **Guardar**.
1. Vuelva a intentar ver la carta.

