---
title: SPA Enrutamiento de modelo de
description: AEM Para las aplicaciones de una sola página en la, la aplicación es responsable del enrutamiento. Este documento describe el mecanismo de ruta, el contrato y las opciones disponibles.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: eaef65ec-2e4d-490f-8158-d48d738e3409
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 6d961456e0e1f7a26121da9be493308a62c53e04
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# SPA Enrutamiento de modelo de{#spa-model-routing}

AEM Para las aplicaciones de una sola página en la, la aplicación es responsable del enrutamiento. Este documento describe el mecanismo de ruta, el contrato y las opciones disponibles.

{{ue-over-spa}}

## Enrutamiento de proyectos {#project-routing}

La aplicación es propietaria del enrutamiento y luego la implementan los desarrolladores de front-end del proyecto. AEM Este documento describe la ruta específica del modelo devuelto por el servidor de la. La estructura de datos del modelo de página expone la dirección URL del recurso subyacente. El proyecto front-end puede utilizar cualquier biblioteca personalizada o de terceros que proporcione funcionalidades de enrutamiento. Cuando una ruta espera un fragmento de modelo, se puede realizar una llamada a la función `PageModelManager.getData()`. Cuando la ruta de un modelo ha cambiado, se debe activar un evento para advertir a las bibliotecas que escuchan, como el Editor de páginas.

## Arquitectura {#architecture}

SPA Para obtener una descripción detallada, consulte la sección [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) del documento de modelo de la página de inicio de la página de la página de inicio de la página de inicio de la página de.

## ModelRouter {#modelrouter}

`ModelRouter`, cuando está habilitado, encapsula las funciones `pushState` y `replaceState` de la API History de HTML5 para garantizar que un fragmento determinado del modelo se obtenga previamente y sea accesible. A continuación, notifica al componente front-end registrado que el modelo se ha modificado.

## Enrutamiento manual frente al automático del modelo {#manual-vs-automatic-model-routing}

`ModelRouter` automatiza la captura de fragmentos del modelo. Pero como cualquier herramienta automatizada, viene con limitaciones. SPA Cuando sea necesario, `ModelRouter` se puede deshabilitar o configurar para que ignore las rutas mediante metapropiedades (consulte la sección de metapropiedades del documento [Componente de página](/help/sites-developing/spa-page-component.md)). Los desarrolladores de front-end pueden implementar su propia capa de enrutamiento de modelos solicitando a `PageModelManager` que cargue cualquier fragmento de modelo mediante la función `getData()`.

>[!NOTE]
>
>El proyecto React de muestra de [We.Retail Journal](https://github.com/adobe/aem-sample-we-retail-journal) ilustra el enfoque automatizado, mientras que el proyecto de Angular ilustra el manual. Un enfoque semiautomatizado también sería un caso de uso válido.

>[!CAUTION]
>
>La versión actual de `ModelRouter` solo admite el uso de direcciones URL que apunten a la ruta de recursos real de los puntos de entrada del modelo Sling. No admite el uso de direcciones URL o alias de vanidad.

## Contrato de enrutamiento {#routing-contract}

SPA La implementación actual se basa en la suposición de que el proyecto de utiliza la API Historial de HTML5 para el enrutamiento a las diferentes páginas de la aplicación.

### Configuración {#configuration}

El `ModelRouter` admite el concepto de enrutamiento de modelos a medida que escucha llamadas de `pushState` y `replaceState` para recuperar previamente fragmentos de modelos. Internamente, déclencheur `PageModelManager` para cargar el modelo que corresponde a una URL determinada y activa un evento `cq-pagemodel-route-changed` que otros módulos pueden escuchar.

De forma predeterminada, este comportamiento se habilita automáticamente. SPA Para deshabilitarlo, el usuario debe procesar la siguiente propiedad meta:

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

SPA AEM Tenga en cuenta que cada ruta de la debe corresponder a un recurso accesible en la (por ejemplo, &quot;`/content/mysite/mypage"`&quot;), ya que `PageModelManager` intentará cargar automáticamente el modelo de página correspondiente una vez seleccionada la ruta. SPA Sin embargo, si es necesario, el también puede definir una &quot;lista de bloqueados&quot; de rutas que `PageModelManager` debe ignorar:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
