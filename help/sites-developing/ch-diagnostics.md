---
title: Diagnósticos de ContextHub
seo-title: Diagnósticos de ContextHub
description: ContextHub proporciona una página de diagnóstico en la que puede ver una descripción general del marco de ContextHub
seo-description: ContextHub proporciona una página de diagnóstico en la que puede ver una descripción general del marco de ContextHub
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: e37ff1c9e657c580c607f2656adca01a2b39f81f

---


# Diagnósticos de ContextHub {#contexthub-diagnostics}

ContextHub proporciona una página de diagnóstico donde puede ver una descripción general del marco de ContextHub. Para abrir la página, vaya a la `contexthub.diagnostics.html` página de la instancia de creación de AEM, por ejemplo:

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

La página Diagnósticos de ContextHub proporciona información sobre las tiendas y los módulos de interfaz de usuario que se han creado, las carpetas de la biblioteca de cliente que se han cargado y los vínculos a páginas útiles.

>[!NOTE]
>
>Para que se devuelva la información de diagnóstico, debe habilitarse el modo de depuración; de lo contrario, la página de diagnóstico estará en blanco. Consulte [este documento](/help/sites-administering/contexthub-config.md#debugging-contexthub) para obtener detalles sobre cómo habilitar el modo de depuración.

>[!NOTE]
>
>En el caso de las configuraciones de ContextHub que siguen ubicadas bajo sus rutas heredadas, la ubicación de la página de diagnóstico es `http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`.

## Tiendas {#stores}

La sección Tiendas muestra todas las tiendas de ContextHub que se han configurado. Cada elemento de la lista consta de la siguiente información:

* **** Título: Tipo [de](/help/sites-developing/ch-samplestores.md) tienda en el que se basa la tienda.
* **** path: Ruta al nodo del repositorio que contiene la configuración.
* **** resourceType: Ruta del nodo del repositorio donde se define el tipo de almacén.
* **** clientlibs: Las categorías de las bibliotecas de cliente que se cargan que implementan el tipo de tienda.

## Módulos {#modules}

La sección Módulos enumera todos los módulos de interfaz de usuario de ContextHub que se han configurado. Cada elemento de la lista consta de la siguiente información:

* **** Título: Tipo [de módulo de](/help/sites-developing/ch-samplemodules.md) interfaz de usuario en el que se basa el módulo de interfaz de usuario.
* **** path: Ruta al nodo del repositorio que contiene la configuración.
* **** resourceType: Ruta del nodo del repositorio donde se define el tipo de módulo de interfaz de usuario.
* **** clientlibs: Las categorías de las bibliotecas de cliente que se cargan que implementan el tipo de módulo de interfaz de usuario.

## Clientlibs {#clientlibs}

La sección Clientlibs enumera todas las carpetas de la biblioteca del cliente que ha cargado ContextHub. Las bibliotecas de cliente están clasificadas:

* **** kernel.js: Bibliotecas de clientes que implementan el marco de ContextHub, el motor de segmentos y los tipos de tiendas.
* **** ui.js: Bibliotecas de clientes que implementan los tipos de módulos UI y UI de ContextHub.
* **** style.css: Archivos CSS que se cargan desde bibliotecas de cliente.

## URL {#urls}

La sección de direcciones URL contiene vínculos a las funciones de ContextHub:

* **** Editor de configuración: Abre la página [de configuración de](/help/sites-administering/contexthub-config.md) ContextHub, donde puede configurar tiendas, modos de interfaz de usuario y módulos de interfaz de usuario.

* **** Configuración de los módulos de ContextHub: Abre el archivo /etc/cloudsettings/default/contexthub.config.kernel.js, que contiene la representación del objeto Javascript de las configuraciones del almacén de ContextHub.
* **** Configuración de la interfaz de usuario de ContextHub: Abre el archivo /etc/cloudsettings/default/contexthub.config.ui.js, que contiene la representación de objeto Javascript de las configuraciones del modo de IU de ContextHub.
* **** kernel.js: Abre el archivo /etc/cloudsettings/default/contexthub.kernel.js, que contiene el código fuente de las bibliotecas cliente que implementan el marco de ContextHub, el motor de segmentos y los tipos de tienda.
* **** ui.js: Abre el archivo /etc/cloudsettings/default/contexthub.ui.js, que contiene el código fuente de las bibliotecas cliente que implementan los tipos de módulos UI y UI de ContextHub.
* **** style.css: Abre el archivo /etc/cloudsettings/default/contexthub.styles.css, que contiene los estilos CSS de la interfaz de usuario y los módulos de interfaz de usuario de ContextHub.