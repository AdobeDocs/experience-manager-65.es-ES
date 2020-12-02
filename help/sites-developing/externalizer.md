---
title: Externalización de direcciones URL
seo-title: Externalización de direcciones URL
description: Externalizer es un servicio OSGI que le permite transformar mediante programación una ruta de recursos en una dirección URL externa y absoluta
seo-description: Externalizer es un servicio OSGI que le permite transformar mediante programación una ruta de recursos en una dirección URL externa y absoluta
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---


# Externalización de direcciones URL{#externalizing-urls}

En AEM, el **Externalizador** es un servicio OSGI que le permite transformar mediante programación una ruta de recursos (p. ej. `/path/to/my/page`) en una dirección URL externa y absoluta (por ejemplo, `https://www.mycompany.com/path/to/my/page`) añadiendo un prefijo a la ruta con un DNS preconfigurado.

Debido a que una instancia no puede conocer su URL visible externamente si se está ejecutando detrás de una capa web y, a veces, es necesario crear un vínculo fuera del ámbito de la solicitud, este servicio proporciona un lugar central para configurar dichas URL externas y generarlas.

Esta página explica cómo configurar el servicio **Externalizer** y cómo utilizarlo. Para obtener más información, consulte [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).

## Configuración del servicio Externalizer {#configuring-the-externalizer-service}

El servicio **Externalizer** le permite definir centralmente varios dominios que se pueden utilizar para anteponer programáticamente las rutas de recursos. Cada dominio se identifica con un nombre único que se utiliza para hacer referencia al dominio mediante programación.

Para definir una asignación de dominio para el servicio **Externalizer**:

1. Vaya al administrador de configuración a través de **Herramientas**, luego **Consola Web** o introduzca:

   `https://<host>:<port>/system/console/configMgr`

1. Haga clic en **Day CQ Link Externalizer** para abrir el cuadro de diálogo de configuración.

   >[!NOTE]
   >
   >El vínculo directo a la configuración es `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. Defina una asignación de **dominios**: una asignación consiste en un nombre único que puede utilizarse en el código para hacer referencia al dominio, un espacio y el dominio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Donde:

   * **** los esquemas suelen ser http o https, pero también pueden ser ftp, etc.

      * utilice https para aplicar vínculos https si lo desea
      * se utilizará si el código de cliente no anula el esquema al solicitar la externalización de una dirección URL.
   * **** server es el nombre de host (puede ser un nombre de dominio o una dirección IP).
   * **port**  (opcional) es el número de puerto.
   * **contextpath**  (opcional) solo se establece si AEM está instalado como una aplicación web en una ruta de contexto diferente.

   Por ejemplo: `production https://my.production.instance`

   Los siguientes nombres de asignación están predefinidos y siempre deben configurarse como AEM dependen de ellos:

   * `local` - la instancia local
   * `author` - el DNS del sistema de creación
   * `publish` - el DNS del sitio web de cara pública

   >[!NOTE]
   >
   >Una configuración personalizada le permite agregar una nueva categoría, como `production`, `staging` o incluso sistemas externos no AEM como `my-internal-webservice`. Resulta útil evitar codificar dichas direcciones URL en diferentes lugares del código base de un proyecto.

1. Haga clic en **Guardar** para guardar los cambios.

>[!NOTE]
>
>Adobe recomienda que [agregue la configuración al repositorio](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository).

### Uso del servicio Externalizer {#using-the-externalizer-service}

Esta sección muestra algunos ejemplos de cómo se puede utilizar el servicio **Externalizer**:

1. **Para obtener el servicio Externalizador en un JSP:**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **Para externalizar una ruta con el dominio de &quot;publicación&quot;:**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   Supongamos que se asigna el dominio:

   * `publish https://www.website.com`

   `myExternalizedUrl` termina con el valor:

   * `https://www.website.com/contextpath/my/page.html`


1. **Para externalizar una ruta con el dominio de &quot;autor&quot;:**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   Supongamos que se asigna el dominio:

   * `author https://author.website.com`

   `myExternalizedUrl` termina con el valor:

   * `https://author.website.com/contextpath/my/page.html`


1. **Para externalizar una ruta con el dominio &#39;local&#39;:**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   Supongamos que se asigna el dominio:

   * `local https://publish-3.internal`

   `myExternalizedUrl` termina con el valor:

   * `https://publish-3.internal/contextpath/my/page.html`


1. Puede encontrar más ejemplos en [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).
