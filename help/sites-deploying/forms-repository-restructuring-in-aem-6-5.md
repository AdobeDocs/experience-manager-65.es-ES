---
title: Reestructuración de repositorios de Forms AEM en 6.5
description: AEM Obtenga información sobre cómo realizar los cambios necesarios para migrar a la nueva estructura de repositorios en la versión 6.5 de la versión de para Forms.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 7%

---

# Reestructuración de repositorios de Forms AEM en 6.5{#forms-repository-restructuring-in-aem}

Como se describe en el elemento principal [AEM Reestructuración de repositorios en 6.5](/help/sites-deploying/repository-restructuring.md) AEM , los clientes que actualicen a la versión 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado con los cambios del repositorio que afectan a la solución de AEM Forms. AEM Algunos cambios requieren un esfuerzo durante el proceso de actualización de la versión 6.5 de la, mientras que otros se pueden aplazar hasta una actualización futura.

**Con actualización a 6.5**

* [Varios](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**Antes de una actualización futura**

* [Configuración del Cloud Service Echosign](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Configuraciones del Cloud Service Recaptcha](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Configuraciones del Cloud Service Typekit](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Varios](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## Con actualización a 6.5 {#with-upgrade}

### Varios {#misc}

| **Ubicación anterior** | `/etc/clientlibs/fd/fp` |
|---|---|
| **Nueva ubicación** | `/libs/fd/fp/components` |
| **Directrices de reestructuración** | Cualquier referencia explícita en el código personalizado a la ubicación heredada debe actualizarse a la ubicación nueva. |
| **Notas** | Estas bibliotecas de cliente no deben editarse ni ampliarse. |

| **Ubicación anterior** | `/etc/clientlibs/fd/rte` |
|---|---|
| **Nueva ubicación** | `/libs/fd/rte` |
| **Directrices de reestructuración** | Para los recursos de las bibliotecas de cliente a los que se puede hacer referencia mediante rutas absolutas, debe utilizar rutas más nuevas en los recursos nuevos. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nueva ubicación** | `/libs/fd/af/authoring/clientlibs` |
| **Directrices de reestructuración** | Para los recursos de las bibliotecas de cliente a los que se puede hacer referencia mediante rutas absolutas, debe utilizar rutas más nuevas en los recursos nuevos. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **Nueva ubicación** | `/libs/fd/xfaforms/clientlibs/` |
| **Directrices de reestructuración** | Para los recursos de las bibliotecas de cliente a los que se puede hacer referencia mediante rutas absolutas, debe utilizar rutas más nuevas en los recursos nuevos. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nueva ubicación** | `/libs/fd/af/runtime/clientlibs` |
| **Directrices de reestructuración** | Para los recursos de las bibliotecas de cliente a los que se puede hacer referencia mediante rutas absolutas, debe utilizar rutas más nuevas en los recursos nuevos. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nueva ubicación** | `/libs/fd/af/runtime/clientlibs` |
| **Directrices de reestructuración** | Para los recursos de las bibliotecas de cliente a los que se puede hacer referencia mediante rutas absolutas, debe utilizar rutas más nuevas en los recursos nuevos. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **Nueva ubicación** | `/libs/fd/expeditor/clientlibs` |
| **Directrices de reestructuración** | Para los recursos de las bibliotecas de cliente a los que se puede hacer referencia mediante rutas absolutas, debe utilizar rutas más nuevas en los recursos nuevos. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **Nueva ubicación** | `/libs/fd/fmaddon` |
| **Directrices de reestructuración** | Nunca se recomendó ni se admitió cambiar estos clientlibs. AEM Si se han realizado modificaciones en estos clientlibs, se deben revertir para utilizar el código proporcionado por el usuario, que es el que se proporciona en la. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/aep` |
|---|---|
| **Nueva ubicación** | `/var/fd/content/annotations` |
| **Directrices de reestructuración** | Nunca se recomendó ni se admitió cambiar estos clientlibs. AEM Si se han realizado modificaciones en estos clientlibs, se deben revertir para utilizar el código proporcionado por el usuario, que es el que se proporciona en la. |
| **Notas** | N/D |

## Antes de una actualización futura {#prior-to-upgrade}

### Configuración del Cloud Service Echosign {#echosign-cloud-service-configuration}

| **Ubicación anterior** | `/etc/cloudservices/echosign` |
|---|---|
| **Nueva ubicación** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **Directrices de reestructuración** | El [Migración de contenido diferido](/help/sites-deploying/lazy-content-migration.md) utilidad que se activará desde la interfaz de usuario de la migración de Forms. |
| **Notas** | N/D |

### Configuraciones del Cloud Service Recaptcha {#recaptcha-cloud-service-configurations}

| **Ubicación anterior** | `/etc/cloudservices/recaptcha` |
|---|---|
| **Nueva ubicación** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **Directrices de reestructuración** | El [Migración de contenido diferido](/help/sites-deploying/lazy-content-migration.md) utilidad que se activará desde la interfaz de usuario de la migración de Forms. |
| **Notas** | N/D |

### Configuraciones del Cloud Service Typekit {#typekit-cloud-service-configurations}

| **Ubicación anterior** | `/etc/cloudservices/typekit` |
|---|---|
| **Nueva ubicación** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **Directrices de reestructuración** | El [Migración de contenido diferido](/help/sites-deploying/lazy-content-migration.md) utilidad que se activará desde la interfaz de usuario de la migración de Forms. |
| **Notas** | N/D |

### Varios {#misc-1}

| **Ubicación anterior** | `/etc/cloudservices/fdm` |
|---|---|
| **Nueva ubicación** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **Directrices de reestructuración** | El [Migración de contenido diferido](/help/sites-deploying/lazy-content-migration.md) utilidad que se activará desde la interfaz de usuario de la migración de Forms. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/designs/fd/fp` |
|---|---|
| **Nueva ubicación** | `/libs/fd/fp` |
| **Directrices de reestructuración** | Actualice cualquier referencia a las plantillas /etc para que apunten a su `/libs` homólogos. |
| **Notas** | N/D |
