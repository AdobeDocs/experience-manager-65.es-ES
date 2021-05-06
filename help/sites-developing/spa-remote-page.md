---
title: El componente RemotePage
description: El componente RemotePage es un componente de página personalizado para editar SPA React remoto dentro de AEM.
exl-id: 3f015997-0d42-4241-a890-0f16a19c5e34
translation-type: tm+mt
source-git-commit: a92358d187aa78e05dd9b5a7bd4ae14bf0972f62
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# El componente RemotePage {#remote-page-component}

Al decidir qué nivel de integración desea tener entre el SPA externo y el AEM, a menudo está claro que debe poder ver y editar el SPA dentro de AEM. El componente RemotePage es un componente de página personalizado solo para este fin.

## Información general {#overview}

El componente RemotePage recupera todos los recursos necesarios del `asset-manifest.json` generado por la aplicación y lo utiliza para procesar el SPA dentro de AEM.

* RemotePage permite insertar las secuencias de comandos y las hojas de estilo de una SPA en el cuerpo de un componente Página AEM.
* Los componentes del front-end virtual permiten marcar secciones como editables en AEM editor SPA.
* En conjunto, una SPA alojada en un dominio diferente se puede hacer editable en AEM.

Consulte el artículo [Edición de una SPA externa en AEM](spa-edit-external.md) para obtener más información sobre la SPA externa editable en AEM.

## Requisitos {#requirements}

* Habilitar CORS en desarrollo
* Configuración de URL remota en Propiedades de página
* Procesar el SPA en AEM
* La aplicación web debe utilizar un manifiesto de recurso bundler como uno de los siguientes y exponer un archivo asset-manifest.json en la raíz del dominio que enumera en una propiedad entrypoints todos los archivos CSS y JS que se van a cargar:
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

   ![Puntos de entrada](assets/asset-manifest-entrypoints.png)

* La aplicación debe poder inicializarse en `<div id="root"></div>` debajo del elemento body. Si se espera un marcado diferente para que la aplicación cree una instancia, entonces esto debe ajustarse en consecuencia en los scripts HTL del componente proxy que tiene un `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Restricciones     {#limitations}

* La implementación actual del componente RemotePage solo admite aplicaciones React remotas.
* El CSS interno definido en el archivo HTML raíz de la aplicación, así como el CSS en línea en el nodo DOM raíz, no estarán disponibles al realizar el procesamiento remoto en AEM.

## Detalles técnicos {#technical-details}

Al igual que el resto del proyecto AEM SPA, el componente RemotePage es de código abierto. Para obtener todos los detalles técnicos del componente RemotePage, [consulte el repositorio de GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
