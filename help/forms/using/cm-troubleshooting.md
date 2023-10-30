---
title: '“Administración de correspondencia: Solución de problemas”'
description: Gestionar los errores que puedan surgir durante el proceso de guardar una carta en un entorno de AEM Forms.
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: 68a1edf5f62d7a988094fceb3f762504711dc2f1
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 92%

---

# Administración de correspondencia: Resolución de problemas {#correspondence-management-troubleshooting}

## Errores al guardar una carta {#errors-when-saving-a-letter}

### Problema {#issue}

Se muestra uno de los siguientes errores al guardar una carta:

* El enlace de datos no está presente para el módulo de texto.
* Proporcione la información de la propiedad necesaria para lo siguiente.

### Motivo {#reason}

Estos errores pueden producirse debido a uno de los siguientes factores:

* Un diccionario de datos está enlazado a la carta pero no está presente en el servidor.
* Un diccionario de datos está enlazado a la carta, pero incluye un guion bajo (_) en su nombre.

### Solución alternativa {#workaround}

Asegúrese de que el diccionario de datos que utiliza en la carta esté presente en el servidor y que no incluya guiones bajos (_) en su nombre.

## Error al previsualizar una carta {#error-when-previewing-a-letter}

### Problema {#issue-1}

Al previsualizar una carta, aparece el error “Error al cargar la carta: no se pudo importar el recurso desde la entrada XML” incluso cuando se publica un recurso de texto que n no se ha publicado previamente en la carta.

### Solución alternativa {#workaround-1}

Restablezca la memoria caché de la carta en la instancia de publicación mediante los siguientes pasos y vuelva a intentar visualizar la carta:

1. Vaya a **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** e inicie sesión como administrador.
1. Seleccione **Configuraciones de Administración de correspondencia**.
1. En **Configuraciones de Administración de correspondencia**, deshabilite **Habilitar memoria caché de la carta** y haga clic en **Guardar**.
1. Habilite **Habilitar memoria caché de la carta** y haga clic en **Guardar**.
1. Vuelva a intentar visualizar la carta.
