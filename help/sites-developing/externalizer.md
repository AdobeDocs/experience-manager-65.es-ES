---
title: Externalización de direcciones URL
seo-title: Externalizing URLs
description: El externalizador es un servicio OSGI que le permite transformar mediante programación una ruta de recurso en una dirección URL externa y absoluta
seo-description: The Externalizer is an OSGI service that allows you to programmatically transform a resource path into an external and absolute URL
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Externalización de direcciones URL{#externalizing-urls}

AEM En el caso de los **Externalizador** es un servicio OSGI que le permite transformar mediante programación una ruta de recursos (por ejemplo, `/path/to/my/page`) en una dirección URL externa y absoluta (por ejemplo, `https://www.mycompany.com/path/to/my/page`) prefijando la ruta con un DNS preconfigurado.

Dado que una instancia no puede conocer su URL visible externamente si se ejecuta detrás de una capa web y que, a veces, se debe crear un vínculo fuera del ámbito de la solicitud, este servicio proporciona un lugar central para configurar esas URL externas y crearlas.

Esta página explica cómo configurar el **Externalizador** servicio y cómo utilizarlo. Para obtener más información, consulte la [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).

## Configuración del servicio externalizador {#configuring-the-externalizer-service}

El **Externalizador** El servicio le permite definir de forma centralizada varios dominios que se pueden utilizar para prefijar mediante programación las rutas de recursos. Cada dominio se identifica con un nombre único que se utiliza para hacer referencia al dominio mediante programación.

Para definir una asignación de dominio para **Externalizador** servicio:

1. Vaya al administrador de configuración mediante **Herramientas**, entonces **Consola web**, o escriba:

   `https://<host>:<port>/system/console/configMgr`

1. Clic **Externalizador de vínculos CQ de día** para abrir el cuadro de diálogo de configuración.

   >[!NOTE]
   >
   >El vínculo directo a la configuración es `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. Defina un **Domains** asignación: una asignación consta de un nombre único que se puede utilizar en el código para hacer referencia al dominio, un espacio y el dominio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Donde:

   * **confabulación** suele ser http o https, pero también puede ser ftp, etc.

      * utilice https para aplicar vínculos https si lo desea
      * se utiliza si el código de cliente no anula el esquema al solicitar la externalización de una dirección URL.

   * **server** es el nombre de host (puede ser un nombre de dominio o una dirección ip).
   * **puerto** (opcional) es el número de puerto.
   * **contextpath** AEM (opcional) solo se establece si se instala la aplicación web como una aplicación web en una ruta de contexto diferente.

   Por ejemplo: `production https://my.production.instance`

   AEM Los siguientes nombres de asignación están predefinidos y siempre deben configurarse, ya que se basa en ellos:

   * `local` - la instancia local
   * `author` - el sistema de creación DNS
   * `publish` - el sitio web público DNS

   >[!NOTE]
   >
   >Una configuración personalizada le permite agregar una nueva categoría, como `production`, `staging` AEM o incluso sistemas externos no relacionados con el uso de la, como `my-internal-webservice`. Es útil evitar codificar estas URL en diferentes lugares del código base de un proyecto.

1. Clic **Guardar** para guardar los cambios.

>[!NOTE]
>
>El Adobe recomienda que [añadir la configuración al repositorio](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository).

### Uso del servicio externalizador {#using-the-externalizer-service}

En esta sección se muestran algunos ejemplos de cómo se puede usar la función **Externalizador** El servicio se puede utilizar:

1. **Para obtener el servicio externalizador en un JSP:**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **Para externalizar una ruta con el dominio &quot;publicar&quot;:**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   Suponiendo la asignación de dominio:

   * `publish https://www.website.com`

   `myExternalizedUrl` termina con el valor:

   * `https://www.website.com/contextpath/my/page.html`

1. **Para externalizar una ruta con el dominio &quot;author&quot;:**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   Suponiendo la asignación de dominio:

   * `author https://author.website.com`

   `myExternalizedUrl` termina con el valor:

   * `https://author.website.com/contextpath/my/page.html`

1. **Para externalizar una ruta con el dominio &quot;local&quot;:**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   Suponiendo la asignación de dominio:

   * `local https://publish-3.internal`

   `myExternalizedUrl` termina con el valor:

   * `https://publish-3.internal/contextpath/my/page.html`

1. Puede encontrar más ejemplos en la [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).
