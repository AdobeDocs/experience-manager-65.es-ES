---
title: Solución de problemas
seo-title: Troubleshooting
description: Resolución de problemas de la comunidad, incluidos los problemas conocidos
seo-description: Troubleshooting Community including Known Issues
uuid: 99225430-fa2a-4393-ae5a-18b19541c358
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cdb2d80a-2fbf-4ee6-b89b-b5d74e6d3bfc
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 1%

---

# Solución de problemas {#troubleshooting}

Esta sección contiene preocupaciones comunes y problemas conocidos.

## Problemas conocidos {#known-issues}

### Falla la recuperación de Dispatcher {#dispatcher-refetch-fails}

Cuando se utiliza Dispatcher 4.1.5 con una versión más reciente de Jetty, una recuperación puede resultar en &quot;No se puede recibir la respuesta del servidor remoto&quot; después de esperar a que la solicitud se agote.

Si utiliza Dispatcher 4.1.6 o posterior, se solucionará este problema.

### No se puede acceder a la publicación de foro después de actualizar desde CQ 5.4 {#cannot-access-forum-post-after-upgrading-from-cq}

Si se creó un foro en CQ5.4 y se publicaron temas, y luego el sitio se actualizó a AEM 5.6.1 o posterior, intentar ver las publicaciones existentes puede resultar en un error en la página:

Carácter de patrón no válido &#39;a&#39; No se puede servir la solicitud a `/content/demoforums/forum-test.html` en este servidor y los registros contienen lo siguiente:

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

El problema es que la cadena de formato para com.day.cq.commons.date.RelativeTimeFormat se cambió entre 5.4 y 5.5 de forma que ya no se acepta la &quot;a&quot; para &quot;ago&quot;.

Por lo tanto, cualquier código que utilice la API RelativeTimeFormat() tendría que cambiar:

* De: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* A: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

El error es diferente al crear y publicar. Al autor, falla silenciosamente y simplemente no muestra los temas del foro. Al publicar, aparece el error en la página.

Consulte la [com.day.cq.commons.date.RelativeTimeFormat](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API para obtener más información.

## Preocupaciones comunes {#common-concerns}

### Advertencia en registros: Manillares obsoletos {#warning-in-logs-handlebars-deprecated}

Durante el inicio (no el primero, pero cada uno después de eso) se puede ver la siguiente advertencia en los registros:

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` se ha reemplazado por `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

Esta advertencia se puede ignorar de forma segura como `jknack.handlebars.Handlebars`, utilizado por [SCF](scf.md#handlebarsjavascripttemplatinglanguage), viene con su propia utilidad de ayuda para i18n. Al inicio, se reemplaza por un AEM específico [Ayuda de i18n](handlebars-helpers.md#i-n). Esta advertencia la genera la biblioteca de terceros para confirmar la anulación de un asistente existente.

### Advertencia en registros: OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

La publicación de varios temas del foro de Comunidades sociales puede resultar en enormes cantidades de registros de advertencia e información del proceso OakResourceListenerOsgiEventQueue.

Estas advertencias se pueden ignorar con seguridad.

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### Error en registros: NoClassDefFoundError para IndexElementFactory {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

La actualización de AEM 5.6.1 GA a la última cq-socialcommunities-pkg-1.4.x o a la AEM 6.0 da como resultado errores en el archivo de registro durante el inicio para una condición que se resuelva como se demuestra por el error que no se ve al reiniciar.

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
