---
title: Solución de problemas AEM durante la creación
description: La sección siguiente trata ciertos problemas que pueden producirse al utilizar AEM, así como sugerencias para solucionarlos.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 29%

---

# Resolución de problemas de AEM durante la creación{#troubleshooting-aem-when-authoring}

La sección siguiente trata ciertos problemas que pueden producirse al utilizar AEM, así como sugerencias para solucionarlos.

>[!NOTE]
>
>Cuando experimenta problemas, también vale la pena comprobar la lista de [Problemas conocidos](/help/release-notes/release-notes.md) para su instancia (versión y service packs).

>[!NOTE]
>
>Los usuarios que tengan privilegios de administrador y que deseen solucionar problemas con AEM, pueden utilizar los métodos de resolución de problemas descritos en [Solución de problemas de AEM (para administradores)](/help/sites-administering/troubleshoot.md). Si no dispone de suficientes privilegios, consulte con el administrador del sistema sobre la resolución de problemas AEM.

## La versión anterior de la página sigue en el sitio publicado {#old-page-version-still-on-published-site}

* **Problema**:

   * Ha realizado cambios en una página y replicado la página en el sitio de publicación, pero la variable *old* la versión de la página sigue mostrándose en el sitio de publicación.

* **Motivo**:

   * Esto puede tener varias causas, la mayoría de las veces la caché (su navegador local o Dispatcher), aunque a veces puede ser un problema con la cola de replicación.

* **Soluciones**:

   * Aquí hay varias posibilidades:
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

   * En casos excepcionales, es posible que haya colocado el encabezado de la barra de tareas fuera del ámbito de la ventana actual. Esto significa que no puede volver a colocarlo.

* **Solución**:

   * Cierre la sesión actual y vuelva a iniciarla. La barra de tareas volverá a la posición predeterminada.

## Buscar y reemplazar: no se reemplazan todas las instancias {#find-replace-not-all-instances-are-replaced}

* **Problema:**

   * Al usar la variable **Buscar y reemplazar** puede suceder que no todas las instancias de la variable `find` en una página.

* **Motivo**:

   * La capacidad de **Buscar y reemplazar** depende de cómo se guarde el contenido y de si se puede buscar. Por ejemplo, un texto de blog se almacena en `jcr:text` que no está configurada para ser buscada. El ámbito predeterminado para el servlet de buscar y reemplazar cubre las siguientes propiedades:

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Solución**:

   * Estas definiciones se pueden cambiar con la configuración de **Servlet Find Replace Day CQ WCM** usando la variable **Consola web**; por ejemplo, en

      `http://localhost:4502/system/console/configMgr`
