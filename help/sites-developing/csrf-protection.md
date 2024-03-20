---
title: El marco de protección CSRF
description: El marco de trabajo utiliza tokens para garantizar que la solicitud del cliente sea legítima
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# El marco de protección CSRF{#the-csrf-protection-framework}

Además del filtro de referente de Apache Sling, Adobe también proporciona un nuevo marco de protección CSRF para protegerse contra este tipo de ataque.

El marco de trabajo utiliza tokens para garantizar que la solicitud del cliente sea legítima. Los tokens se generan cuando el formulario se envía al cliente y se validan cuando se devuelve al servidor.

>[!NOTE]
>
>No hay tokens en las instancias de publicación para usuarios anónimos.

## Requisitos  {#requirements}

### Dependencias {#dependencies}

Cualquier componente que dependa de `granite.jquery` La dependencia de puede beneficiarse del Marco de protección de CSRF automáticamente. Si no es así, para cualquiera de los componentes, debe declarar una dependencia a `granite.csrf.standalone` antes de poder utilizar el marco de trabajo.

### Duplicación de la clave criptográfica {#replicating-crypto-keys}

Para utilizar los tokens, debe replicar el binario HMAC en todas las instancias de la implementación. Consulte [Duplicación de la clave HMAC](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) para obtener más información.

>[!NOTE]
>
>Asegúrese de hacer lo necesario [Cambios de configuración de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) para utilizar el Marco de protección de CSRF.

>[!NOTE]
>
>Si utiliza la caché de manifiesto con la aplicación web, asegúrese de agregar &quot;**&amp;ast;**&quot; al manifiesto para asegurarse de que el token no desconecte la llamada de generación de tokens CSRF. Para obtener más información, consulte [vincular](https://www.w3.org/TR/offline-webapps/).
>
Para obtener más información sobre los ataques de CSRF y las formas de mitigarlos, consulte la [Falsificación de solicitudes entre sitios página OWASP](https://owasp.org/www-community/attacks/csrf).
