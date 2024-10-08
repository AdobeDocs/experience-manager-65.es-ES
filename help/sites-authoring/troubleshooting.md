---
title: AEM Solución de problemas durante la creación en la
description: AEM Algunos problemas que pueden producirse al utilizar el servicio de asistencia de la aplicación de.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 41%

---

# Resolución de problemas de AEM durante la creación{#troubleshooting-aem-when-authoring}

La sección siguiente trata ciertos problemas que pueden producirse al utilizar AEM, así como sugerencias para solucionarlos.

>[!NOTE]
>
>Cuando tenga problemas, también vale la pena comprobar la lista de [Problemas conocidos](/help/release-notes/release-notes.md) de su instancia (versiones y paquetes de servicio).

>[!NOTE]
>
>AEM AEM Los usuarios que tengan privilegios de administrador y que deseen solucionar problemas con los recursos de administración, pueden utilizar los métodos de solución de problemas descritos en [Solución de problemas de los usuarios (para los administradores)](/help/sites-administering/troubleshoot.md). AEM Si no tiene privilegios suficientes, consulte al administrador del sistema para obtener información sobre la solución de problemas de la solución de problemas de la.

## La versión anterior de la página sigue en el sitio publicado {#old-page-version-still-on-published-site}

* **Problema**:

   * Ha realizado cambios en una página y replicado la página en el sitio de publicación, pero la versión *antigua* de la página se sigue mostrando en el sitio de publicación.

* **Motivo**:

   * Esto puede tener varias causas, la mayoría de las veces la memoria caché (el explorador local o el Dispatcher), aunque a veces puede ser un problema con la cola de replicación.

* **Soluciones**:

   * Aquí hay varias posibilidades:
   * Confirme que la página se ha duplicado correctamente. Compruebe el estado de la página y, si es necesario, el estado de la cola de replicación.
   * Borre la caché del navegador local y vuelva a acceder a la página.
   * Añada `?` al final de la URL de la página. Por ejemplo:

      * `http://localhost:4502/sites.html/content?`
      * Esta acción solicitará la página directamente desde AEM y omitirá a Dispatcher. Si recibe la página actualizada quiere decir que debe borrar la caché de Dispatcher.

   * Póngase en contacto con el administrador del sistema si hay problemas con las colas de replicación.

## Acciones aplicables a los componentes no visibles en la barra de herramientas {#component-actions-not-visible-on-toolbar}

* **Problema**:

   * La gama completa de acciones aplicables a los componentes no aparece visible al editar una página de contenido en el entorno de creación. 

* **Motivo**:

   * En casos excepcionales, una acción anterior podría afectar a la barra de herramientas.

* **Solución**:

   * Actualice la página.
