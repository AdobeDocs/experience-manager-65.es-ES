---
title: Activación del CRXDE Lite en AEM
seo-title: Enabling CRXDE Lite in AEM
description: Obtenga información sobre cómo habilitar el CRXDE Lite en AEM.
seo-description: Learn how to enable CRXDE Lite in AEM.
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# Activación del CRXDE Lite en AEM{#enabling-crxde-lite-in-aem}

Para garantizar que las instalaciones de AEM sean lo más seguras posible, la lista de comprobación de seguridad recomienda [desactivación de WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) en entornos de producción.

Sin embargo, el CRXDE Lite depende de la variable `org.apache.sling.jcr.davex` paquete para funcionar correctamente, por lo que deshabilitar WebDAV también deshabilitará el CRXDE Lite.

Cuando esto sucede, vaya a `https://serveraddress:4502/crx/de/index.jsp` mostrará un nodo raíz vacío y todas las solicitudes HTTP a los recursos del CRXDE Lite darán error:

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

Aunque esta recomendación está pensada para reducir al máximo las superficies de ataque, es posible que los administradores de sistemas necesiten a veces acceder al CRXDE Lite para examinar el contenido o depurar problemas en las instancias de producción.

Si está desactivado, puede activar el CRXDE Lite siguiendo el siguiente procedimiento:

1. Vaya a la consola Componentes de OSGi en `http://localhost:4502/system/console/components`
1. Busque el siguiente componente:

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. Haga clic en el icono de llave inglesa que hay junto a él para ver sus opciones de configuración:

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. Cree la siguiente configuración:

   * **Ruta raíz:** `/crx/server`
   * Marque la casilla debajo de **Usar URI absolutos**.

1. Cuando termine de usar CRXDE Lite, asegúrese de desactivar WebDAV de nuevo.

También puede habilitar el CRXDE Lite a través de cURL, ejecutando este comando:

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## Otros recursos {#other-resources}

Para obtener más información sobre AEM 6 funciones de seguridad, consulte las siguientes páginas:

* [Lista de comprobación de seguridad AEM](/help/sites-administering/security-checklist.md)
* [Ejecución de AEM en el modo Producción lista](/help/sites-administering/production-ready.md)
