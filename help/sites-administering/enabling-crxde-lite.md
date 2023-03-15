---
title: Activación del CRXDE Lite AEM en la
seo-title: Enabling CRXDE Lite in AEM
description: Obtenga información sobre cómo habilitar CRXDE Lite AEM en la aplicación de.
seo-description: Learn how to enable CRXDE Lite in AEM.
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
source-git-commit: a4183bb9d72763ebea3b464c77fce978c723e053
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Activación del CRXDE Lite AEM en la{#enabling-crxde-lite-in-aem}

AEM Para garantizar que las instalaciones de la sean lo más seguras posible, la lista de comprobación de seguridad recomienda [deshabilitar WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) en entornos de producción.

Sin embargo, el CRXDE Lite depende del `org.apache.sling.jcr.davex` paquete para funcionar correctamente, por lo que deshabilitar WebDAV también deshabilitará el CRXDE Lite.

Cuando esto sucede, vaya a `https://serveraddress:4502/crx/de/index.jsp` mostrará un nodo raíz vacío y todas las solicitudes HTTP a los recursos del CRXDE Lite producirán un error:

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

Aunque esta recomendación pretende reducir las superficies de ataque en la medida de lo posible, los administradores del sistema a veces pueden necesitar acceso a CRXDE Lite para examinar el contenido o depurar problemas en instancias de producción.

Puede habilitar CRXDE Lite con las siguientes opciones [Configuración de OSGi](#enabling-crxde-lite-osgi) o con un [cURL, comando](#enabling-crxde-lite-curl).

>[!WARNING]
>
>Debido a las pequeñas diferencias en la forma en que funcionan estos métodos, debe utilizar ***o bien*** OSGI ***o*** cURL.
>
>Los dos métodos son ***no*** intercambiable.

## Habilitar el CRXDE Lite con OSGI {#enabling-crxde-lite-osgi}

Si está desactivado, puede activar el CRXDE Lite siguiendo el siguiente procedimiento:

1. Vaya a la consola Componentes de OSGi en `http://localhost:4502/system/console/components`
1. Busque el siguiente componente:

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. Haga clic en el icono de la llave inglesa junto a ella para ver sus opciones de configuración:

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. Cree la siguiente configuración:

   * **Ruta raíz:** `/crx/server`
   * Marque la casilla debajo de **Usar URI absolutos**.

1. Cuando termine de usar CRXDE Lite, asegúrese de volver a deshabilitar WebDAV.

## Habilitar el CRXDE Lite con cURL {#enabling-crxde-lite-curl}

También puede habilitar CRXDE Lite mediante cURL si ejecuta este comando:

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## Otros recursos {#other-resources}

AEM Para obtener más información sobre las funciones de seguridad de la versión 6 de la aplicación, consulte las páginas siguientes:

* [AEM La lista de comprobación de seguridad](/help/sites-administering/security-checklist.md)
* [AEM Ejecución en modo listo para la producción](/help/sites-administering/production-ready.md)
