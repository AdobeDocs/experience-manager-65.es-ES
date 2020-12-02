---
title: Resolución de problemas de AEM durante la creación
seo-title: Resolución de problemas de AEM durante la creación
description: La sección siguiente trata ciertos problemas que pueden producirse al utilizar AEM, así como sugerencias para solucionarlos.
seo-description: La sección siguiente trata ciertos problemas que pueden producirse al utilizar AEM, así como sugerencias para solucionarlos.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 95%

---


# Resolución de problemas de AEM durante la creación{#troubleshooting-aem-when-authoring}

La sección siguiente trata ciertos problemas que pueden producirse al utilizar AEM, así como sugerencias para solucionarlos.

>[!NOTE]
>
>Si está experimentando problemas, puede consultar la lista de [Problemas conocidos](/help/release-notes/known-issues.md) de su instancia (versión y Service Packs).

>[!NOTE]
>
>Los usuarios con privilegios de administrador que deseen solucionar problemas de AEM pueden utilizar los métodos de resolución de problemas descritos en [Resolución de problemas de AEM (para administradores)](/help/sites-administering/troubleshoot.md). Si no dispone de suficientes privilegios, póngase en contacto con el administrador del sistema para la resolución de problemas de AEM.

## La versión anterior de la página sigue en el sitio publicado {#old-page-version-still-on-published-site}

* **Problema**:

   * Ha realizado cambios en una página y replicado la página en el sitio de publicación, pero la versión *antigua* de la página todavía se muestra en el sitio de publicación.

* **Motivo**:

   * Puede haber varios motivos. Normalmente es la caché (su navegador local o Dispatcher), aunque a veces puede haber un problema con la cola de replicación.

* **Soluciones**:

   * Hay varias posibilidades:
   * Confirme que la página se haya replicado correctamente. Compruebe el estado de la página y, si es necesario, el estado de la cola de replicación.
   * Borre la caché del navegador local y vuelva a acceder a la página.
   * Añada `?` al final de la URL de la página. Por ejemplo:

      `http://localhost:4502/sites.html/content?`

      Esta acción solicitará la página directamente desde AEM y omitirá a Dispatcher. Si recibe la página actualizada quiere decir que debe borrar la caché de Dispatcher.

   * Póngase en contacto con el administrador del sistema si hay problemas con las colas de replicación.

## Barra de tareas no visible {#sidekick-not-visible}

* **Problema**:

   * La barra de tareas no está visible al editar una página de contenido en el entorno de creación.

* **Motivo**:

   * En casos muy contados, puede haber colocado el encabezado de la barra de tareas fuera del ámbito de la ventana actual. Esto significa que no puede volver a colocarla.

* **Solución**:

   * Cierre la sesión actual y vuelva a iniciarla. La barra de tareas volverá a la posición predeterminada.

## Buscar y reemplazar: no se reemplazan todas las instancias {#find-replace-not-all-instances-are-replaced}

* **Problema:**

   * Al utilizar la opción **Buscar y reemplazar** puede suceder que no todas las instancias del término `find` se reemplacen en una página.

* **Motivo**:

   * La fiabilidad de **Buscar y reemplazar** depende de cómo se guarde el contenido y si se puede buscar. Por ejemplo, un texto de blog se guarda en la propiedad `jcr:text`, que no está configurada para la búsqueda. El alcance predeterminado para el servlet de buscar y reemplazar cubre las siguientes propiedades:

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Solución**:

   * Estas definiciones pueden cambiarse con la configuración del **Servlet Find Replace Day WCM CQ** mediante la **Consola web**; por ejemplo en

      `http://localhost:4502/system/console/configMgr`

