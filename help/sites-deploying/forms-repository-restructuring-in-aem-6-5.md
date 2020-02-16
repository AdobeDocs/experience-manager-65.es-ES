---
title: Reestructuración del repositorio de formularios en AEM 6.5
seo-title: Reestructuración del repositorio de formularios en AEM 6.5
description: Obtenga información sobre cómo realizar los cambios necesarios para migrar a la nueva estructura de repositorio en AEM 6.5 for Forms.
seo-description: Obtenga información sobre cómo realizar los cambios necesarios para migrar a la nueva estructura de repositorio en AEM 6.5 for Forms.
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb

---


# Reestructuración del repositorio de formularios en AEM 6.5{#forms-repository-restructuring-in-aem}

Como se describe en la página principal Reestructuración [del repositorio en AEM 6.5](/help/sites-deploying/repository-restructuring.md) , los clientes que actualicen a AEM 6.5 deben utilizar esta página para evaluar el esfuerzo de trabajo asociado a los cambios del repositorio que afectan a la solución AEM Forms. Algunos cambios requieren esfuerzo durante el proceso de actualización de AEM 6.5, mientras que otros se pueden aplazar hasta una actualización futura.

**Con actualización a 6.5**

* [Misc](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**Antes de la actualización futura**

* [Configuración del servicio de Echosign Cloud](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Configuraciones del servicio de nube de Recaptcha](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Configuraciones del servicio de nube de Typekit](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Misc](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## Con actualización a 6.5 {#with-upgrade}

### Misc {#misc}

| **Ubicación anterior** | `/etc/clientlibs/fd/fp` |
|---|---|
| **Nuevas ubicaciones** | `/libs/fd/fp/components` |
| **Orientación de reestructuración** | Todas las referencias explícitas del código personalizado a la ubicación heredada deben actualizarse a la nueva ubicación. |
| **Notas** | Estas bibliotecas de cliente no deben modificarse ni ampliarse. |

| **Ubicación anterior** | `/etc/clientlibs/fd/rte` |
|---|---|
| **Nuevas ubicaciones** | `/libs/fd/rte` |
| **Orientación de reestructuración** | Para los recursos de las bibliotecas de cliente a los que se puede hacer referencia mediante rutas absolutas, debe utilizar rutas más nuevas en recursos nuevos. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuevas ubicaciones** | `/libs/fd/af/authoring/clientlibs` |
| **Orientación de reestructuración** | Para los recursos de las bibliotecas de cliente a los que se puede hacer referencia mediante rutas absolutas, debe utilizar rutas más nuevas en recursos nuevos. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **Nuevas ubicaciones** | `/libs/fd/xfaforms/clientlibs/` |
| **Orientación de reestructuración** | Para los recursos de las bibliotecas de cliente a los que se puede hacer referencia mediante rutas absolutas, debe utilizar rutas más nuevas en recursos nuevos. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuevas ubicaciones** | `/libs/fd/af/runtime/clientlibs` |
| **Orientación de reestructuración** | Para los recursos de las bibliotecas de cliente a los que se puede hacer referencia mediante rutas absolutas, debe utilizar rutas más nuevas en recursos nuevos. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/clientlibs/fd/af` |
|---|---|
| **Nuevas ubicaciones** | `/libs/fd/af/runtime/clientlibs` |
| **Orientación de reestructuración** | Para los recursos de las bibliotecas de cliente a los que se puede hacer referencia mediante rutas absolutas, debe utilizar rutas más nuevas en recursos nuevos. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **Nuevas ubicaciones** | `/libs/fd/expeditor/clientlibs` |
| **Orientación de reestructuración** | Para los recursos de las bibliotecas de cliente a los que se puede hacer referencia mediante rutas absolutas, debe utilizar rutas más nuevas en recursos nuevos. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **Nuevas ubicaciones** | `/libs/fd/fmaddon` |
| **Orientación de reestructuración** | Nunca se recomendó ni se admitió el cambio de estos clientes. Si se han realizado modificaciones en estos clientes, deben revertirse para utilizar el código proporcionado por AEM. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/aep` |
|---|---|
| **Nuevas ubicaciones** | `/var/fd/content/annotations` |
| **Orientación de reestructuración** | Nunca se recomendó ni se admitió el cambio de estos clientes. Si se han realizado modificaciones en estos clientes, deben revertirse para utilizar el código proporcionado por AEM. |
| **Notas** | N/D |

## Antes de la actualización futura {#prior-to-upgrade}

### Configuración del servicio de Echosign Cloud {#echosign-cloud-service-configuration}

| **Ubicación anterior** | `/etc/cloudservices/echosign` |
|---|---|
| **Nuevas ubicaciones** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **Orientación de reestructuración** | La [utilidad de migración](/help/sites-deploying/lazy-content-migration.md) de contenido diferida que se activará desde la interfaz de usuario de migración de formularios. |
| **Notas** | N/D |

### Configuraciones del servicio de nube de Recaptcha {#recaptcha-cloud-service-configurations}

| **Ubicación anterior** | `/etc/cloudservices/recaptcha` |
|---|---|
| **Nuevas ubicaciones** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **Orientación de reestructuración** | La [utilidad de migración](/help/sites-deploying/lazy-content-migration.md) de contenido diferida que se activará desde la interfaz de usuario de migración de formularios. |
| **Notas** | N/D |

### Configuraciones del servicio de nube de Typekit {#typekit-cloud-service-configurations}

| **Ubicación anterior** | `/etc/cloudservices/typekit` |
|---|---|
| **Nuevas ubicaciones** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **Orientación de reestructuración** | La [utilidad de migración](/help/sites-deploying/lazy-content-migration.md) de contenido diferida que se activará desde la interfaz de usuario de migración de formularios. |
| **Notas** | N/D |

### Misc {#misc-1}

| **Ubicación anterior** | `/etc/cloudservices/fdm` |
|---|---|
| **Nuevas ubicaciones** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **Orientación de reestructuración** | La [utilidad de migración](/help/sites-deploying/lazy-content-migration.md) de contenido diferida que se activará desde la interfaz de usuario de migración de formularios. |
| **Notas** | N/D |

| **Ubicación anterior** | `/etc/designs/fd/fp` |
|---|---|
| **Nuevas ubicaciones** | `/libs/fd/fp` |
| **Orientación de reestructuración** | Cualquier referencia a las plantillas /etc debería actualizarse para que apunten a sus `/libs` homólogos. |
| **Notas** | N/D |

