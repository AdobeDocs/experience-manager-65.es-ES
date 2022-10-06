---
title: "Gestión de correspondencia: Resolución de problemas"
seo-title: Correspondence Management Troubleshooting
description: Solución de problemas de gestión de correspondencia
seo-description: Correspondence Management Troubleshooting
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 6%

---

# Gestión de correspondencia: Resolución de problemas {#correspondence-management-troubleshooting}

## Errores al guardar una carta {#errors-when-saving-a-letter}

### Problema {#issue}

Se muestra uno de los siguientes errores al guardar una carta:

* El enlace de datos no está presente para el módulo de texto
* Proporcione la información de la propiedad necesaria para lo siguiente

### Motivo {#reason}

Estos errores pueden producirse debido a uno de los siguientes factores:

* Un diccionario de datos está enlazado a la carta pero no está presente en el servidor.
* Un diccionario de datos está enlazado a la letra pero tiene un guión bajo (_) en su nombre.

### Solución alternativa {#workaround}

Asegúrese de que el diccionario de datos que está utilizando en la carta esté presente en el servidor y no tenga un guión bajo (_) en su nombre.

## Error al previsualizar una carta {#error-when-previewing-a-letter}

### Problema {#issue-1}

Al previsualizar una carta, aparece el error Error en la carta de carga: No se pudo importar el recurso desde la entrada XML&quot; aparece incluso cuando se publica un recurso de texto previamente no publicado en la carta.

### Solución alternativa {#workaround-1}

Restablezca la caché de letras en la instancia de publicación siguiendo los pasos siguientes y vuelva a intentar ver la carta:

1. Vaya a **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** e inicie sesión como administrador.
1. Select **Configuraciones de administración de correspondencia**.
1. En **Configuraciones de administración de correspondencia**, disable **Habilitar caché de letras** y haga clic en **Guardar.**
1. Habilitar **Habilitar caché de letras** y haga clic en **Guardar**.
1. Vuelva a intentar ver la carta.
