---
title: Ejecución de AEM en modo listo para la producción
seo-title: Ejecución de AEM en modo listo para la producción
description: Obtenga información sobre cómo ejecutar AEM en modo listo para la producción.
seo-description: Obtenga información sobre cómo ejecutar AEM en modo listo para la producción.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
translation-type: tm+mt
source-git-commit: 730a690bcbf5935ca00ed69c27ce108cb2664c22
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 3%

---


# Ejecución de AEM en modo listo para producción{#running-aem-in-production-ready-mode}

Con AEM 6.1, Adobe presenta el nuevo modo de ejecución `"nosamplecontent"`, que tiene como objetivo automatizar los pasos necesarios para preparar una instancia de AEM para la implementación en un entorno de producción.

El nuevo modo de ejecución no sólo configurará automáticamente la instancia para atenerse a las optimizaciones de seguridad descritas en la lista de comprobación de seguridad, sino que también eliminará todas las aplicaciones y configuraciones de geometrixx de muestra en el proceso.

>[!NOTE]
>
>Debido a que, por razones prácticas, el modo AEM listo para la producción solo cubrirá la mayoría de las tareas necesarias para asegurar una instancia, es muy recomendable que consulte la [lista de comprobación de seguridad](/help/sites-administering/security-checklist.md) antes de empezar a usar el entorno de producción.
>
>Además, tenga en cuenta que la ejecución de AEM en modo listo para la producción deshabilitará efectivamente el acceso al CRXDE Lite. Si lo necesita para la depuración, consulte [Activación del CRXDE Lite en AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

Para ejecutar AEM en modo listo para la producción, todo lo que debe hacer es agregar el `nosamplecontent` mediante el conmutador de modo de ejecución `-r` a los argumentos de inicio existentes:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Por ejemplo, puede utilizar la producción lista para iniciar una instancia de autor con persistencia MongoDB como esta:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Cambia parte del modo de preparación para producción {#changes-part-of-the-production-ready-mode}

Más concretamente, se realizarán los siguientes cambios en la configuración cuando se ejecute AEM en modo listo para la producción:

1. El **paquete de soporte de CRXDE** ( `com.adobe.granite.crxde-support`) está deshabilitado de forma predeterminada en modo listo para producción. Puede instalarse en cualquier momento desde el repositorio público de Maven de Adobe. Se requiere la versión 3.0.0 para AEM 6.1.

1. El paquete **Apache Sling Simple WebDAV Access to repositorios** ( `org.apache.sling.jcr.webdav`) sólo estará disponible en instancias de **autor**.

1. Los usuarios recién creados deberán cambiar la contraseña en el primer inicio de sesión. Esto no se aplica al usuario administrador.
1. **Genere** información de depuración deshabilitada para el controlador de secuencias de comandos  **Apache Sling JavaScript**.

1. **Contenido asignado** y  **Generar** información de depuración deshabilitada para el controlador de secuencias de comandos  **Apache Sling JSP**.

1. El **Filtro CQ WCM de día** se establece en `edit` en **autor** y `disabled` en **instancias de publicación**.

1. El **Administrador de biblioteca HTML de Adobe Granite** está configurado con la siguiente configuración:

   1. **Minimizar:** `enabled`
   1. **Depurar:** `disabled`
   1. **Gzip:** `enabled`
   1. **Temporización:** `disabled`

1. El **Servlet de GET Apache Sling** está configurado para admitir configuraciones seguras de manera predeterminada, de la siguiente manera:

| **Configuración** | **Autor** | **Publicación** |
|---|---|---|
| Representación TXT | desactivado | desactivado |
| Representación HTML | desactivado | desactivado |
| Representación JSON | activado | activado |
| Representación XML | desactivado | desactivado |
| json.maximumresults | 1000 | 100 |
| Índice automático | desactivado | desactivado |

