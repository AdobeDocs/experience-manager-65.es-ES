---
title: Ejecución de AEM en modo de producción lista
seo-title: Ejecución de AEM en modo de producción lista
description: Obtenga información sobre cómo ejecutar AEM en modo listo para la producción.
seo-description: Obtenga información sobre cómo ejecutar AEM en modo listo para la producción.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Ejecución de AEM en modo de producción lista{#running-aem-in-production-ready-mode}

Con AEM 6.1, Adobe introduce el nuevo `"nosamplecontent"` modo de ejecución para automatizar los pasos necesarios para preparar una instancia de AEM para la implementación en un entorno de producción.

El nuevo modo de ejecución no sólo configurará automáticamente la instancia para atenerse a las optimizaciones de seguridad descritas en la lista de comprobación de seguridad, sino que también eliminará todas las aplicaciones y configuraciones de geometrixx de muestra en el proceso.

>[!NOTE]
>
>Debido a que, por razones prácticas, el modo AEM Production Ready solo cubrirá la mayoría de las tareas necesarias para asegurar una instancia, es muy recomendable que consulte la lista [de comprobación de](/help/sites-administering/security-checklist.md) seguridad antes de empezar a trabajar con el entorno de producción.
>
>Además, tenga en cuenta que la ejecución de AEM en modo listo para la producción deshabilitará efectivamente el acceso a CRXDE Lite. Si lo necesita para la depuración, consulte [Activación de CRXDE Lite en AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

Para ejecutar AEM en modo listo para la producción, todo lo que debe hacer es agregar el `nosamplecontent` mediante el conmutador de `-r` modo de ejecución a los argumentos de inicio existentes:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Por ejemplo, puede utilizar la producción lista para iniciar una instancia de autor con persistencia MongoDB como esta:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Cambia parte del modo listo para la producción {#changes-part-of-the-production-ready-mode}

Más concretamente, se realizarán los siguientes cambios en la configuración cuando AEM se ejecute en modo listo para la producción:

1. El paquete **de compatibilidad con CRXDE** ( `com.adobe.granite.crxde-support`) está desactivado de forma predeterminada en el modo listo para la producción. Puede instalarse en cualquier momento desde el repositorio público de Adobe Maven. Se requiere la versión 3.0.0 para AEM 6.1.

1. El paquete **Apache Sling Simple WebDAV Acceso a repositorios** ( `org.apache.sling.jcr.webdav`) sólo estará disponible en instancias de **creación** .

1. Los usuarios recién creados deberán cambiar la contraseña en el primer inicio de sesión. Esto no se aplica al usuario administrador.
1. **La generación de información** de depuración está deshabilitada para el controlador de secuencias de comandos **Apache JavaScript**.

1. **El contenido** asignado y **Generar información** de depuración están desactivados para el controlador de secuencias de comandos JSP de **Apache Sling**.

1. El filtro **CQ WCM de** día se establece `edit` en instancias de **autor** y `disabled` publicación **** .

1. **El Administrador** de bibliotecas HTML de Adobe Granite está configurado con la siguiente configuración:

   1. **** Minimizar: `enabled`
   1. **** Depurar: `disabled`
   1. **** Gzip: `enabled`
   1. **** Temporización: `disabled`

1. El servlet **Apache Sling GET** está configurado para admitir configuraciones seguras de forma predeterminada, como se indica a continuación:

| **Configuración** | **Creación** | **Publicación** |
|---|---|---|
| Representación TXT | desactivado | desactivado |
| Representación HTML | desactivado | desactivado |
| Representación JSON | activado | activado |
| Representación XML | desactivado | desactivado |
| json.maximumresults | 1000 | 100 |
| Índice automático | desactivado | desactivado |

