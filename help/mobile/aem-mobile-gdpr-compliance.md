---
title: 'Adobe Experience Manager Mobile: Preparación para el RGPD'
description: Obtenga información sobre cómo Adobe Experience Manager está preparado para ayudarle con sus obligaciones de cumplimiento del RGPD.
contentOwner: trushton
exl-id: d06e675f-fb61-47da-85de-e0b50dd44153
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# AEM Mobile: Preparación para el RGPD {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones siguientes, pero los detalles cubiertos son aplicables a todas las regulaciones de protección de datos y privacidad; como el RGPD y la CCPA.

{{ue-over-mobile}}

## Compatibilidad con RGPD de AEM Mobile {#aem-mobile-gdpr-support}

AEM Mobile está preparado para ayudar a los clientes con sus obligaciones de cumplimiento del RGPD. En AEM Mobile no se almacenan datos personales. Si está aprovisionado, puede iniciar sesión en Adobe Experience Mobile con su Adobe ID.

<!-- [https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html) -->

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

El producto de publicación digital de Adobe (que precede a AEM Mobile) es compatible con las iniciativas de preparación para el RGPD de Adobe. Consulte [https://business.adobe.com/privacy/general-data-protection-regulation.html](https://business.adobe.com/privacy/general-data-protection-regulation.html). A continuación se proporcionan detalles específicos sobre la compatibilidad con las funciones relevantes del RGPD en el producto de Digital Publishing Suite, incluido cómo trabajar con Adobe para iniciar solicitudes de RGPD.

Para asegurarse de que no confunde AEM Mobile con el producto de Digital Publishing Suite anterior, puede iniciar sesión en el producto de Digital Publishing Suite aquí:

[https://acrobat.adobe.com/us/en/](https://acrobat.adobe.com/us/en/)

### Inicio de una solicitud de RGPD {#initiating-a-gdpr-request}

Póngase en contacto con el Servicio de atención al cliente de Adobe para poder iniciar una solicitud de RGPD para el Digital Publishing Suite.

Se requieren los siguientes ID para localizar los datos del cliente. Cualquier subconjunto recibido implica que los demás ID no eran aplicables a este usuario.

Obligatorio:

* Id. de contrato del cliente: *dpsc-ContractId*

Proporcione al menos una de las siguientes opciones:

* ID de OAuth proporcionado por el cliente del usuario final (el ID utilizado en el sistema de derechos directos del cliente): *dpsc-directEntitlementId*
* Para usuarios de aplicaciones Windows, el App Store ID del usuario final: *dpsc-windowsAppStoreId*
* La dirección de correo electrónico que el usuario final usó para interactuar con la aplicación DPS: *email*

### Preguntas más frecuentes (FAQ) {#frequently-asked-questions-faq}

**¿Hay Adobes al eliminar mis compras de App Store al iniciar una solicitud de DELETE?**

El Adobe elimina la información que tiene sobre las compras en la tienda de aplicaciones (suscripciones, etc.), pero las compras siguen registradas en las tiendas de aplicaciones. Si la aplicación (usuario final) ha iniciado sesión en la tienda de aplicaciones, esos recibos se recogen de nuevo y se envían al Adobe. Más adelante, se consideran nuevas compras y son restauradas por la aplicación, con acceso de nuevo.

**¿El Adobe está eliminando los derechos proporcionados por el cliente al iniciar una solicitud de DELETE?**

El Adobe elimina la información que tiene de las asignaciones de derechos directos adicionales del cliente. Si la aplicación (usuario final) inicia sesión en el mecanismo de OAuth que el cliente ha utilizado, envía información al Adobe y los servicios vuelven a recoger los derechos adicionales.

**¿Qué se espera del usuario final?**

Dado que la clave para asignar derechos a la aplicación reside en el dispositivo como parte del software del visualizador, el usuario final debe desinstalar la aplicación. El usuario final debe tener en cuenta que, si vuelve a instalar la aplicación, las compras existentes (asociadas al usuario de la tienda de aplicaciones) y las asignaciones de derechos directos (asociadas al usuario de OAuth del cliente) se restauran.

**¿Qué sucede cuando se comparte una aplicación entre personas de un dispositivo?**

El Adobe tiene una información mínima que se asocia directamente con un usuario específico. Asocia los datos mediante un UUID creado aleatoriamente que se almacena en los datos de la aplicación y se pasa en cada solicitud que inicia la aplicación. Esto significa que los usuarios finales que comparten la aplicación en el mismo dispositivo utilizan el mismo UUID y que todos los datos se consideran propiedad de la persona que realiza la solicitud de RGPD. Tanto para las solicitudes de acceso como para las de eliminación, DPSC considera que las personas que comparten una aplicación son una sola persona.

**¿Qué datos personales se rastrean con Analytics?**

Ninguna. Hay datos de los que se está realizando un seguimiento, pero es a nivel de aplicación (no personal). Esto incluye eventos como lanzamientos, bloqueos, cierres, actividades, compras o superposiciones de publicación. No se realiza un seguimiento de las ubicaciones geográficas, los nombres, los ID de dispositivo ni las direcciones IP.

**El usuario final proporcionó su información, pero no se encontró nada. ¿Por qué no?**

A medida que evolucionaba el producto de Digital Publishing Suite, las implementaciones de servicios cambiaban y se ofuscaban más datos. Si no se encontraron datos utilizando los datos proporcionados por el usuario, significa que los datos del usuario no se pueden rastrear hasta esa persona.

### Ejemplos {#example}

Póngase en contacto con el Servicio de atención al cliente de Adobe para iniciar una solicitud de RGPD.

Este es un ejemplo de las entradas y las salidas resultantes de una solicitud de RGPD de Digital Publishing Suite:

#### Entradas: {#inputs}

```
dpsc-contractId = "12345-1234-12416234" 
directEntitlementId = "1234-1234-1234" 
windowsAppStoreId = "testWinAppStoreId" 
email = "test@what.com"
```

#### Salidas {#outputs}

```
{

    "jobId": "test-1524750204384",

    "product": "DPSC",

    "action": "access",

    "userIDS": [

        {

        "namespace": "email",

        "value": "test@what.com"

        },

        {

        "namespace": "windowsAppStoreId",

        "value": "testWinAppStoreId"

        },

        {

        "namespace": "directEntitlementId",

        "value": "1234-1234-1234"

        }

    ],

    "receiptData": {

    "recordsFound": 6,

    "recordsAffected": 0,

    "tablesModified": 0,

    "subscriptionsFound": 24,

    "entitlementsFound": 24

    },

    "records": {

        "DPS_Stage_EntitlementUserDevices": [

        {

            "user_id": "testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "device_id": "appleStore:test1b16-f032-4d9c-9200-0d19999405c4",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test967d-5179-4dc6-958c-facd9d94da38",

            "device_id": "appleStore:test3f07-d5aa-4b32-8fac-b2b690b7ccd7",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test1838-6494-4e74-912c-1edf61581d0e",

            "device_id": "appleStore:test3813-f8cc-49ce-b021-50eb0814a3bb",

            "account_id": "1234-1234-1234"

        },

        {

            "user_id": "test5468-1a11-4e4c-be43-274181a9ef81",

            "device_id": "appleStore:testf082-2783-498d-ab62-b1b2e3eb67ae",

            "account_id": "1234-1234-1234"

        }

        ],

            "DPS_Stage_EntitlementUsers": [

        {

            "id": "store:test04a7-33a3-4b90-863d-79981ead0f19:appleStore",

            "part_id": "0",

            "alias_user_id": "testWinAppStoreId"

        },

        {

            "id": "internal:testd2da-0606-4444-87ef-0d5a1d4a121d:adobe",

            "part_id": "0",

            "user_id": "test@what.com"

        }

        ],

            "DPS_Stage_Subscriptions": [

        {

            "id": "appleStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test3531-a209-4391-beb9-951c7822244e",

            "overflow": "test4e59-86a8-4b75-b699-77e980c287ab",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "test491b-379e-4d24-96ef-e481bf8d3062",

            "overflow": "test931b-7422-485d-85a5-134828187b6c",

            "entitlement_count": "12"

        }

        ],

            "DPS_Stage_Entitlements": [

        {

            "id": "samsungStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test7332-60a0-42b8-a508-474668d83d2e",

            "overflow": "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "testf766-102a-460d-8f5a-42f7bb9d68b7",

            "overflow": "test4d96-2197-45a8-9caf-2aa2846b770c",

            "entitlement_count": "12"

        }

        ],

            "s3Buckets": {

            "name": "DPS-Entitlements-Overflow",

            "folder": "stage/",

            "overflows": {

            "subscriptions": [

            "test4e59-86a8-4b75-b699-77e980c287ab",

            "test931b-7422-485d-85a5-134828187b6c"

        ],

            "entitlements": [

            "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "test4d96-2197-45a8-9caf-2aa2846b770c"

                ]

            }

        }

    }

}
```
