---
title: El componente RemotePage
description: El componente RemotePage es un componente de página personalizado para editar SPA React remoto dentro de AEM.
translation-type: tm+mt
source-git-commit: 431bed450ed5b0239d9191dcf061f01e64b8981a
workflow-type: tm+mt
source-wordcount: '261'
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

## Restricciones     {#limitations}

* La implementación actual del componente RemotePage solo admite aplicaciones React remotas.
* El CSS interno definido en el archivo HTML raíz de la aplicación, así como el CSS en línea en el nodo DOM raíz, no estarán disponibles al realizar el procesamiento remoto en AEM.

## Detalles técnicos {#technical-details}

Al igual que el resto del proyecto AEM SPA, el componente RemotePage es de código abierto. Para obtener todos los detalles técnicos del componente RemotePage, [consulte el repositorio de GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
