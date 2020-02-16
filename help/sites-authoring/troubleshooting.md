---
title: Resolución de problemas de AEM durante la creación
seo-title: Resolución de problemas de AEM durante la creación
description: Algunos problemas que pueden producirse al utilizar AEM
seo-description: Algunos problemas que pueden producirse al utilizar AEM
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

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
   * Add `?` to the end of the page URL. For example:

      * `http://localhost:4502/sites.html/content?`
      * Esta acción solicitará la página directamente desde AEM y omitirá el despachante. Si recibe la página actualizada quiere decir que debe borrar la caché de Dispatcher.
   * Póngase en contacto con el administrador del sistema si hay problemas con las colas de replicación.


## Acciones aplicables a los componentes no visibles en la barra de herramientas {#component-actions-not-visible-on-toolbar}

* **Problema**:

   * La gama completa de acciones aplicables a los componentes no aparece visible al editar una página de contenido en el entorno de creación. 

* **Motivo**:

   * En casos excepcionales, una acción anterior podría afectar a la barra de herramientas.

* **Solución**:

   * Actualice la página.

