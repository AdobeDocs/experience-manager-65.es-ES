---
title: Solución de problemas de comunidad
description: Obtenga información acerca de la solución de problemas de la comunidad, incluidos problemas y preocupaciones conocidos.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# Solución de problemas de comunidad {#troubleshooting}

Esta sección contiene preocupaciones comunes y problemas conocidos al solucionar problemas de la comunidad.

## Problemas conocidos {#known-issues}

### Error de recuperación de Dispatcher {#dispatcher-refetch-fails}

Al utilizar Dispatcher 4.1.5 con una versión más reciente de Jetty, una recuperación puede dar como resultado &quot;No se puede recibir respuesta del servidor remoto&quot; después de esperar a que se agote el tiempo de espera de la solicitud.

El uso de Dispatcher 4.1.6 o posterior resuelve este problema.

### No se puede acceder al foro de Post después de actualizar desde CQ 5.4 {#cannot-access-forum-post-after-upgrading-from-cq}

AEM Si se crea un foro sobre CQ 5.4 y se publican temas y, a continuación, el sitio se actualiza a la versión 5.6.1 o posterior de, intentar ver las publicaciones existentes puede provocar un error en la página:

Carácter de patrón no válido &#39;a&#39;
No se puede entregar la solicitud a `/content/demoforums/forum-test.html` en este servidor y los registros contienen lo siguiente:

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

El problema es que la cadena de formato para com.day.cq.commons.date.RelativeTimeFormat se cambió entre 5.4 y 5.5, de modo que ya no se acepta la &quot;a&quot; para &quot;ago&quot;.

Por lo tanto, cualquier código que utilice la API RelativeTimeFormat() debe cambiar:

* De: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* Para: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

El error es diferente en Autor y Publish. En Autor, falla de forma silenciosa y simplemente no muestra los temas del foro. En Publish, genera el error en la página.

Consulte la API [com.day.cq.commons.date.RelativeTimeFormat](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) para obtener más información.

## Inquietudes comunes {#common-concerns}

### Advertencia en los registros: Handlebars obsoleto {#warning-in-logs-handlebars-deprecated}

Durante el inicio (no el primero, sino todos los posteriores), se puede ver la siguiente advertencia en los registros:

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` ha sido reemplazado por `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

Esta advertencia se puede ignorar de forma segura, ya que `jknack.handlebars.Handlebars`, utilizada por [SCF](scf.md#handlebarsjavascripttemplatinglanguage), viene con su propia utilidad de ayuda i18n. AEM Al iniciarse, se reemplaza con un [ayudante i18n](handlebars-helpers.md#i-n) específico de la. Esta advertencia la genera la biblioteca de terceros para confirmar la anulación de un asistente existente.

### Advertencia en registros: OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

La publicación de varios temas de foros de comunidades sociales puede dar como resultado enormes cantidades de registros de advertencia e información de OakResourceListener processOsgiEventQueue.

Estas advertencias se pueden ignorar sin problemas.

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### Error en los registros: NoClassDefFoundError para IndexElementFactory {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

AEM AEM La actualización de la versión 5.6.1 a la última versión cq-socialcommunities-pkg-1.4.x o a la versión 6.0 da como resultado errores en el archivo de registro. Esto ocurre durante el inicio de una condición que se resuelve a sí misma como lo demuestra el error que no se ve al reiniciar.

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
