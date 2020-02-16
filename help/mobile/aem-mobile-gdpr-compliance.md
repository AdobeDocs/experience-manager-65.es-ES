---
title: 'AEM Mobile: preparación para RGPD'
seo-title: 'AEM Mobile: preparación para RGPD'
description: nulo
seo-description: nulo
uuid: 817c434f-4b78-40f7-99d6-6efafdedb77e
contentOwner: trushton
discoiquuid: 9399dd3d-a485-4f53-a6f2-7b190da4235b
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# AEM Mobile: preparación para RGPD {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>El RGPD se utiliza como ejemplo en las secciones que figuran a continuación, pero los detalles abarcados son aplicables a todas las normas de protección de datos y privacidad; como el RGPD, la CCPA, etc.

## Compatibilidad con GDPR de AEM Mobile {#aem-mobile-gdpr-support}

AEM Mobile está listo para ayudar a los clientes con sus obligaciones de cumplimiento de GDPR. No se almacenan datos personales en AEM Mobile. Si está aprovisionado, puede iniciar sesión en Adobe Experience Mobile con su Adobe ID.

[https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html)

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

El producto de publicación digital de Adobe (que precede a AEM Mobile) es compatible con las iniciativas de preparación para el RGPD de Adobe. Consulte [https://www.adobe.com/privacy/general-data-protection-regulation.html](https://www.adobe.com/privacy/general-data-protection-regulation.html). A continuación se proporcionan detalles específicos sobre la compatibilidad con las funciones relevantes del RGPD en el producto de Digital Publishing Suite, incluida la forma de trabajar con Adobe para iniciar solicitudes del RGPD.

Para asegurarse de que no confunde AEM Mobile con el producto anterior de Digital Publishing Suite, puede iniciar sesión en el producto de Digital Publishing Suite aquí:

[https://digitalpublishing.acrobat.com/welcome.html](https://digitalpublishing.acrobat.com/welcome.html)

### Inicio de una solicitud de RGPD {#initiating-a-gdpr-request}

Póngase en contacto con el servicio de atención al cliente de Adobe para iniciar una solicitud de RGPD para Digital Publishing Suite.

Se requieren los siguientes ID para localizar los datos de cliente. Cualquier subconjunto recibido implicará que los demás ID no eran aplicables a este usuario.

Obligatorio:

* ID del contrato del cliente: *dpsc-ContractId*

Proporcione al menos 1 de los siguientes datos:

* ID de OAuth proporcionada por el cliente final (el ID que se utiliza en el sistema de asignación directa de derechos del cliente): *dpsc-directEntitlementId*
* Para los usuarios de la aplicación de Windows, el ID de App Store del usuario final: *dpsc-windowsAppStoreId*
* La dirección de correo electrónico que el usuario final utilizó para interactuar con la aplicación de DPS: *correo electrónico*

### Preguntas más frecuentes {#frequently-asked-questions-faq}

**¿Adobe eliminará mis compras de App Store al iniciar una solicitud de ELIMINACIÓN?**

Adobe eliminará la información que tiene de las compras de App Store (suscripciones, etc.) pero las compras seguirán registrándose en las tiendas de aplicaciones. Si la aplicación (usuario final) ha iniciado sesión en el App Store, esos recibos se recuperarán y se enviarán de nuevo a Adobe y, posteriormente, se considerarán nuevas compras y la aplicación los restaurará para que tengan acceso de nuevo.

**¿Adobe eliminará los derechos proporcionados por el cliente al iniciar una solicitud de ELIMINACIÓN?**

Adobe eliminará la información que tiene de las asignaciones de asignación de derechos directas adicionales del cliente. Si la aplicación (usuario final) inicia sesión en el mecanismo OAuth que ha utilizado el cliente, enviará información a Adobe y los servicios recogerán los derechos adicionales de nuevo.

**¿Qué se espera del usuario final?**

Dado que la clave para asignar derechos a la aplicación reside en el dispositivo como parte del software del visor, el usuario final debe desinstalar la aplicación. El usuario final debe darse cuenta de que, si vuelve a instalar la aplicación, se restaurarán las compras existentes (asociadas con el usuario del almacén de aplicaciones) y las asignaciones de asignación de derechos directas (asociadas con el usuario de OAuth del cliente).

**¿Qué ocurre cuando se comparte una aplicación entre personas de un dispositivo?**

Adobe tiene muy poca información que se asocia directamente a un usuario específico. Asocia los datos mediante un UUID creado al azar que se retiene en los datos de la aplicación y se pasa en cada solicitud que inicia la aplicación. Esto significa que los usuarios finales que compartan la aplicación en el mismo dispositivo utilizarán el mismo UUID y que todos los datos se considerarán propiedad de la persona que realiza la solicitud del RGPD. Para las solicitudes de acceso y eliminación, DPSC considerará a las personas que comparten una aplicación como una sola persona.

**¿Qué datos personales se rastrean con Analytics?**

Ninguna. Se está realizando un seguimiento de los datos, pero están en el nivel de la aplicación (no personales). Esto incluye eventos como inicios, bloqueos, cierres, actividades, compras o superposiciones de publicaciones. No se realiza el seguimiento de ubicaciones geográficas, nombres, ID de dispositivos o direcciones IP.

**El usuario final proporcionó su información, pero no se encontró nada. ¿Por qué no?**

A medida que evolucionaba el producto de Digital Publishing Suite, las implementaciones de servicios cambiaban y se confundían más datos. Si no se encontraron datos con los datos proporcionados por el usuario, significa que no se puede realizar un seguimiento de los datos del usuario a esa persona.

### Ejemplo {#example}

Póngase en contacto con el Servicio de atención al cliente de Adobe para iniciar una solicitud de RGPD.

A continuación se muestra un ejemplo de las entradas y los resultados de una solicitud GDPR de Digital Publishing Suite:

#### Entradas: {#inputs}

```
dpsc-contractId = “12345-1234-12416234” 
directEntitlementId = “1234-1234-1234” 
windowsAppStoreId = “testWinAppStoreId” 
email = “test@what.com”
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

