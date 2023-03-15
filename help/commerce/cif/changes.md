---
title: Cambios importantes en el complemento del marco de integración comercial (CIF)
description: Cambios importantes del complemento Commerce Integration Framework (CIF) en comparación con las versiones anteriores del CIF.
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
source-git-commit: a2ababa9dd9115e963b91a7271d204d287557c40
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# Cambios importantes en el complemento Commerce Integration Framework (CIF){#notable-changes}

Este documento destaca las importantes diferencias entre el complemento Commerce Integration Framework (CIF) y las versiones antiguas del CIF, conocidas principalmente como CIF clásico (Quickstart) y CIF de código abierto.

## Instalación y actualizaciones

AEM AEM El paquete de complementos CIF de la se instala y actualiza con el Administrador de paquetes de la aplicación.

**Versiones anteriores del CIF**

* CIF clásico: no se necesita instalación, CIF era parte de Quickstart. AEM Las actualizaciones del CIF formaban parte de las actualizaciones regulares de los paquetes de servicio o de los programas de servicio
* CIF Open-source: instalación a través de GitHub. Las actualizaciones formaban parte del trabajo de actualización/mantenimiento manual.

## Configuración de extremo

El extremo se configura mediante la consola OSGi.

**Versiones anteriores del CIF**

* AEM CIF clásico: a través de la configuración OSGi en el
* CIF Open-source: a través del explorador de configuración del CIF

## Implementación del proyecto CIF Venia

Proyecto disponible en [AEM Guías de GitHub para el usuario de GitHub - Proyecto Venia CIF](https://github.com/adobe/aem-cif-guides-venia) AEM e implementación realizada mediante el Administrador de paquetes de.

**Versiones anteriores del CIF**

* AEM CIF Classic: mediante la instalación del paquete de

## Datos del catálogo de productos

Los datos del catálogo de productos se solicitan bajo demanda mediante llamadas en tiempo real a un extremo externo que admite las API de GraphQL requeridas. Estas API admiten el acceso a datos activos o clasificados en cualquier fecha determinada. No se necesita replicación.

**Versiones anteriores del CIF**

* CIF clásico: los datos de productos en vivo y clasificados se importan y persisten en JCR en AEM Author a través de la importación completa o delta de productos. Los datos del producto activos se replican en AEM Publish.

## AEM Experiencias del catálogo de productos con procesamiento de la

AEM AEM La función de procesamiento de experiencias de catálogo de productos se procesa sobre la marcha utilizando plantillas de catálogo de productos que se han asignado a productos y categorías, y que se pueden usar para crear experiencias de catálogo de productos. No se necesita replicación.

**Versiones anteriores del CIF**

* AEM CIF clásico: AEM Author crea una página de para cada categoría/producto mediante la herramienta de modelo de catálogo. Estas páginas se replican en AEM Publish.

>[!NOTE]
>
>AEM AEM Para obtener documentación adicional sobre cómo utilizar CIF con el servicio administrado por el usuario o el servicio administrado por el usuario en las instalaciones, consulte la sección sobre cómo utilizar CIF con el servicio administrado por el usuario o el servicio administrado en las instalaciones, en la sección [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
