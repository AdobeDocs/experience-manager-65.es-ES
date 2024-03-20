---
title: AEM Solución de problemas durante la creación
description: La sección siguiente trata ciertos problemas que pueden producirse al utilizar AEM, así como sugerencias para solucionarlos.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 27%

---

# Resolución de problemas de AEM durante la creación{#troubleshooting-aem-when-authoring}

La sección siguiente trata ciertos problemas que pueden producirse al utilizar AEM, así como sugerencias para solucionarlos.

>[!NOTE]
>
>Cuando experimenta problemas, también vale la pena comprobar la lista de [Problemas conocidos](/help/release-notes/release-notes.md) para su instancia (versión y paquetes de servicio).

>[!NOTE]
>
>AEM Los usuarios que tienen privilegios de administrador y que desean solucionar problemas con la solución de problemas con la solución de problemas con la solución de problemas, pueden utilizar los métodos de solución de problemas descritos en [AEM Solución de problemas (para administradores)](/help/sites-administering/troubleshoot.md). AEM Si no tiene privilegios suficientes, consulte al administrador del sistema para obtener información sobre la solución de problemas de la solución de problemas de la.

## La versión anterior de la página sigue en el sitio publicado {#old-page-version-still-on-published-site}

* **Problema**:

   * Ha realizado cambios en una página y replicado la página en el sitio de publicación, pero la variable *viejo* La versión de la página se sigue mostrando en el sitio de publicación.

* **Motivo**:

   * Esto puede tener varias causas, la mayoría de las veces la caché (el explorador local o Dispatcher), aunque a veces puede ser un problema con la cola de replicación.

* **Soluciones**:

   * Aquí hay varias posibilidades:
   * Confirme que la página se ha duplicado correctamente. Compruebe el estado de la página y, si es necesario, el estado de la cola de replicación.
   * Borre la caché del navegador local y vuelva a acceder a la página.
   * Añada `?` al final de la URL de la página. Por ejemplo:

     `http://localhost:4502/sites.html/content?`

     Esta acción solicitará la página directamente desde AEM y omitirá a Dispatcher. Si recibe la página actualizada quiere decir que debe borrar la caché de Dispatcher.

   * Póngase en contacto con el administrador del sistema si hay problemas con las colas de replicación.

## Sidekick no visible {#sidekick-not-visible}

* **Problema**:

   * El Sidekick no está visible al editar una página de contenido en el entorno de creación.

* **Motivo**:

   * En casos excepcionales, es posible que haya colocado el encabezado de la barra de tareas fuera del ámbito de la ventana actual. Esto significa que no puede volver a colocarlo.

* **Solución**:

   * Cierre la sesión actual y vuelva a iniciarla. El Sidekick volverá a la posición predeterminada.

## Buscar y reemplazar: no se reemplazan todas las instancias {#find-replace-not-all-instances-are-replaced}

* **Problema:**

   * Al usar el **Buscar y reemplazar** opción puede ocurrir que no todas las instancias de la variable `find` Los términos se reemplazan en una página.

* **Motivo**:

   * La capacidad de **Buscar y reemplazar** depende de cómo se guarde el contenido y de si se puede buscar. Por ejemplo, un texto de blog se almacena en `jcr:text` propiedad que no está configurada para ser buscada. El ámbito predeterminado del servlet de búsqueda y reemplazo cubre las siguientes propiedades:

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **Solución**:

   * Estas definiciones se pueden cambiar con la configuración de **Día en que CQ WCM encuentre el servlet de reemplazo** uso del **Consola web**; por ejemplo, en

     `http://localhost:4502/system/console/configMgr`
