---
title: Habilitar CRXDE Lite en AEM
seo-title: Habilitar CRXDE Lite en AEM
description: Obtenga información sobre cómo activar el CRXDE Lite en AEM.
seo-description: Obtenga información sobre cómo activar el CRXDE Lite en AEM.
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
translation-type: tm+mt
source-git-commit: a833a34bbeb938c72cdb851a46b2ffd97aee9f6d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Habilitando CRXDE Lite en AEM{#enabling-crxde-lite-in-aem}

Para garantizar que las instalaciones AEM sean lo más seguras posible, la lista de comprobación de seguridad recomienda [deshabilitar WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) en los entornos de producción.

Sin embargo, el CRXDE Lite depende del paquete `org.apache.sling.jcr.davex` para funcionar correctamente, por lo que la desactivación de WebDAV también deshabilitará el CRXDE Lite.

Cuando esto sucede, al navegar a `https://serveraddress:4502/crx/de/index.jsp` se muestra un nodo raíz vacío y todas las solicitudes HTTP a los recursos CRXDE Lite fallan:

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

Aunque esta recomendación tiene por objeto reducir al máximo las superficies de ataque, es posible que los administradores de sistemas necesiten acceder a CRXDE Lite para examinar el contenido o depurar problemas en las instancias de producción.

Si está desactivado, puede activar el CRXDE Lite siguiendo el procedimiento siguiente:

1. Vaya a la consola Componentes OSGi en `http://localhost:4502/system/console/components`
1. Busque el siguiente componente:

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. Haga clic en el icono de llave inglesa que hay junto a él para ver las opciones de configuración:

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. Cree la siguiente configuración:

   * **Ruta raíz:** `/crx/server`
   * Haga clic en la casilla en **Usar URI absolutos**.

1. Cuando termine de usar CRXDE Lite, asegúrese de volver a deshabilitar WebDAV.

También puede habilitar CRXDE Lite mediante cURL, ejecutando este comando:

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## Otros recursos {#other-resources}

Para obtener más información sobre las funciones de seguridad de AEM 6, consulte las páginas siguientes:

* [Lista de comprobación de seguridad AEM](/help/sites-administering/security-checklist.md)
* [Ejecución de AEM en modo listo para la producción](/help/sites-administering/production-ready.md)

