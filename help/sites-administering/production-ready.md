---
title: AEM Ejecución en modo listo para la producción
seo-title: Running AEM in Production Ready Mode
description: AEM Obtenga información sobre cómo ejecutar la en el modo Producción lista.
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

# AEM Ejecución en modo listo para la producción{#running-aem-in-production-ready-mode}

AEM Con la versión 6.1, Adobe presenta la nueva `"nosamplecontent"` AEM modo de ejecución para automatizar los pasos necesarios para preparar una instancia de para su implementación en un entorno de producción.

El nuevo modo de ejecución no solo configurará automáticamente la instancia para adherirse a las prácticas recomendadas de seguridad descritas en la lista de comprobación de seguridad, sino que también eliminará todas las aplicaciones y configuraciones de geometrixx de ejemplo en el proceso.

>[!NOTE]
>
>AEM Dado que, por motivos prácticos, el modo listo para la producción de la solo cubre la mayoría de las tareas necesarias para proteger una instancia, es muy recomendable que consulte la [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md) antes de lanzarse al entorno de producción.
>
>AEM Además, tenga en cuenta que ejecutar el modo de producción lista para la producción deshabilitará de forma eficaz el acceso a CRXDE Lite. Si lo necesita para depurar, consulte [Activación del CRXDE Lite AEM en la](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

AEM Para ejecutar la ejecución en modo listo para la producción, todo lo que debe hacer es agregar el `nosamplecontent` a través de `-r` modo de ejecución cambie a los argumentos de inicio existentes:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Por ejemplo, puede utilizar la producción lista para iniciar una instancia de autor con persistencia MongoDB de esta manera:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Cambia parte del modo Producción lista {#changes-part-of-the-production-ready-mode}

AEM Más específicamente, se realizarán los siguientes cambios de configuración cuando se ejecute en modo de producción lista:

1. El **Paquete de soporte de CRXDE** ( `com.adobe.granite.crxde-support`) está desactivado de forma predeterminada en el modo listo para la producción. Se puede instalar en cualquier momento desde el repositorio Maven público de Adobe. AEM Se requiere la versión 3.0.0 para la versión 6.1 de.

1. El **Acceso simple de Apache Sling WebDAV a repositorios** ( `org.apache.sling.jcr.webdav`) paquete solo estará disponible en **autor** instancias.

1. Los usuarios recién creados deberán cambiar la contraseña la primera vez que inicien sesión. Esto no se aplica al usuario administrador.
1. **Generar información de depuración** está deshabilitado para **Apache Sling Java Script Handler**.

1. **Contenido asignado** y **Generar información de depuración** están desactivadas para la **Apache Sling JSP Script Handler**.

1. El **Filtro de WCM de CQ de día** se establece en `edit` el **autor** y `disabled` el **publicar** instancias.

1. El **Administrador de bibliotecas de Adobe Granite HTML** se configura con la siguiente configuración:

   1. **Minificar:** `enabled`
   1. **Depurar:** `disabled`
   1. **Gzip:** `enabled`
   1. **Horario:** `disabled`

1. El **Apache Sling GET Servlet** está configurada para admitir configuraciones seguras de forma predeterminada, de la siguiente manera:

| **Configuración** | **Autor** | **Publicación** |
|---|---|---|
| Representación TXT | desactivado | desactivado |
| representación del HTML | desactivado | desactivado |
| Representación JSON | enabled | enabled |
| Representación XML | desactivado | desactivado |
| json.maximumresults | 1000 | 100 |
| Índice automático | desactivado | desactivado |
