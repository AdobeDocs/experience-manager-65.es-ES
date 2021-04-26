---
title: Cambios importantes del complemento Commerce Integration Framework (CIF)
description: Cambios importantes del complemento Commerce Integration Framework (CIF) en comparación con las versiones anteriores del CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
translation-type: tm+mt
source-git-commit: a8dba82029168660b84b085ab46d0406b19961ef
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# Cambios importantes en el complemento Commerce Integration Framework (CIF){#notable-changes}

Este documento destaca las importantes diferencias entre el complemento Commerce Integration Framework (CIF) y las versiones anteriores del CIF, conocidas principalmente como CIF Classic (Quickstart) y CIF Open-source.

## Instalación y actualizaciones

El paquete de complementos del CIF de AEM se instala y actualiza con AEM administrador de paquetes.

**Versiones anteriores del CIF**

* CIF Classic: No se necesita instalación, CIF era parte de Quickstart. Las actualizaciones del CIF formaban parte de actualizaciones AEM o service pack normales
* CIF Open-source: Instalación a través de GitHub. Las actualizaciones formaban parte del trabajo de actualización/mantenimiento manual.

## Configuración de extremo

El punto final se configura mediante la consola OSGi.

**Versiones anteriores del CIF**

* CIF Classic: A través de la configuración OSGi en AEM
* CIF Open-source: A través del navegador de configuración del CIF

## Implementación del proyecto CIF Venia

Proyecto disponible en [Guías de AEM de GitHub - Proyecto Venia del CIF](https://github.com/adobe/aem-cif-guides-venia) e implementación realizada mediante el administrador de AEM de paquetes

**Versiones anteriores del CIF**

* CIF Classic: A través de AEM instalación del paquete

## Datos del catálogo de productos

Los datos del catálogo de productos se solicitan bajo demanda mediante llamadas en tiempo real a un extremo externo que admite las API de GraphQL necesarias. Estas API admiten el acceso a los datos activos o por etapas en cualquier fecha determinada. No se necesita replicación.

**Versiones anteriores del CIF**

* CIF Classic: Los datos de productos activos y por etapas se importan y persisten en JCR en AEM Author mediante la importación completa o delta de productos. Los datos del producto activo se replican en AEM Publish.

## Experiencias del catálogo de productos con AEM renderización

AEM procesa las experiencias del catálogo de productos sobre la marcha mediante AEM plantillas de catálogo que se han asignado a productos y categorías. No se necesita replicación.

**Versiones anteriores del CIF**

* CIF Classic: AEM Author crea una página AEM para cada categoría o producto con la herramienta de modelo del catálogo. Estas páginas se replican en AEM Publish.

>[!NOTE]
>
>Para obtener documentación adicional sobre cómo utilizar CIF con AEM servicio administrado o AEM local, consulte [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
