---
title: Ejecución de AEM en el modo Producción lista
seo-title: Running AEM in Production Ready Mode
description: Aprenda a ejecutar AEM en el modo Producción lista .
seo-description: Learn how to run AEM in Production Ready Mode.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# Ejecución de AEM en el modo Producción lista{#running-aem-in-production-ready-mode}

Con AEM 6.1, Adobe presenta el nuevo `"nosamplecontent"` runmode tiene como objetivo automatizar los pasos necesarios para preparar una instancia de AEM para la implementación en un entorno de producción.

El nuevo modo de ejecución no solo configurará automáticamente la instancia para adherirse a las prácticas recomendadas de seguridad descritas en la lista de comprobación de seguridad, sino que también eliminará todas las aplicaciones y configuraciones de geometrixx de muestra en el proceso.

>[!NOTE]
>
>Dado que, por razones prácticas, el modo listo para la producción de AEM solo cubrirá la mayoría de las tareas necesarias para proteger una instancia, se recomienda consultar la [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md) antes de lanzarse al entorno de producción.
>
>Además, tenga en cuenta que la ejecución de AEM en el modo Producción lista deshabilitará efectivamente el acceso al CRXDE Lite. Si lo necesita con fines de depuración, consulte [Activación del CRXDE Lite en AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

Para ejecutar AEM en modo listo para la producción, todo lo que debe hacer es agregar la variable `nosamplecontent` a través de la variable `-r` el conmutador runmode pasa a sus argumentos de inicio existentes:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Por ejemplo, puede utilizar la producción lista para iniciar una instancia de autor con persistencia MongoDB de esta manera:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Cambia parte del modo Producción lista {#changes-part-of-the-production-ready-mode}

Más específicamente, los siguientes cambios de configuración se realizarán cuando AEM se ejecute en el modo listo para la producción:

1. La variable **Paquete de soporte CRXDE** ( `com.adobe.granite.crxde-support`) está desactivado de forma predeterminada en el modo listo para la producción. Se puede instalar en cualquier momento desde el repositorio Maven público de Adobe. Se requiere la versión 3.0.0 para AEM 6.1.

1. La variable **Apache Sling Simple WebDAV Acceso a repositorios** ( `org.apache.sling.jcr.webdav`) paquete solo estará disponible en **author** instancias.

1. Los usuarios recién creados deberán cambiar la contraseña en el primer inicio de sesión. Esto no se aplica al usuario administrador.
1. **Generar información de depuración** está desactivado para la variable **Controlador de Java Script de Apache Sling**.

1. **Contenido asignado** y **Generar información de depuración** están deshabilitadas para la variable **Controlador de scripts JSP de Apache Sling**.

1. La variable **Filtro WCM Day CQ** está configurado como `edit` en **author** y `disabled` en **publicar** instancias.

1. La variable **Administrador de biblioteca de HTML de Adobe Granite** está configurado con la siguiente configuración:

   1. **Minificar:** `enabled`
   1. **Depuración:** `disabled`
   1. **Gzip:** `enabled`
   1. **Temporización:** `disabled`

1. La variable **Servlet de GET Apache Sling** está configurada para admitir configuraciones seguras de forma predeterminada, de la siguiente manera:

| **Configuración** | **Autor** | **Publicación** |
|---|---|---|
| Representación TXT | desactivado | desactivado |
| Representación del HTML | desactivado | desactivado |
| Representación JSON | enabled | enabled |
| Representación XML | desactivado | desactivado |
| json.maximumresults | 1000 | 100 |
| Índice automático | desactivado | desactivado |
