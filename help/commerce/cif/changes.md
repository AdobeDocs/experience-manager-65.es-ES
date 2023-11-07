---
title: Cambios importantes en el complemento de Commerce integration framework CIF ()
description: Cambios importantes en el complemento de Commerce integration framework CIF CIF () en comparación con las versiones anteriores de la versión de la versión de la.
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---

# Cambios importantes en el complemento de Commerce integration framework CIF (){#notable-changes}

En este documento se destacan las importantes diferencias entre el complemento de Commerce integration framework CIF CIF CIF CIF () y las versiones de antiguas, conocidas principalmente como Classic (Quickstart) y las versiones de código abierto de la aplicación de código abierto de la aplicación de código abierto de la aplicación de código abierto de la aplicación de código abierto de la.

## Instalación y actualizaciones

AEM CIF AEM El paquete de complementos de se instala y actualiza con el Administrador de paquetes de.

**CIF Versiones anteriores de la aplicación**

* CIF CIF Clásico: no se necesita instalación, ya que el inicio rápido era parte de la instalación de, por lo tanto, no se requiere instalación. CIF AEM Las actualizaciones de la versión de la aplicación de datos formaban parte de las actualizaciones regulares de los paquetes de servicio o de la
* CIF Código abierto: instalación a través de GitHub. Las actualizaciones formaban parte del trabajo de actualización/mantenimiento manual.

## Configuración de extremo

El extremo se configura mediante la consola OSGi.

**CIF Versiones anteriores de la aplicación**

* CIF AEM Clásico: configuración mediante OSGi en el
* CIF CIF Código abierto: A través del explorador de configuración de la

## CIF Implementación del proyecto Venia de la

Proyecto disponible en [AEM CIF Guías de GitHub para la administración de la - Proyecto Venia en](https://github.com/adobe/aem-cif-guides-venia) AEM e implementación realizada mediante el Administrador de paquetes de.

**CIF Versiones anteriores de la aplicación**

* CIF AEM Clásico: mediante la instalación del paquete de

## Datos del catálogo de productos

Los datos del catálogo de productos se solicitan bajo demanda mediante llamadas en tiempo real a un extremo externo que admite las API de GraphQL requeridas. Estas API admiten el acceso a datos activos o clasificados en cualquier fecha determinada. No se necesita replicación.

**CIF Versiones anteriores de la aplicación**

* CIF AEM Clásico: los datos de producto en vivo y clasificados se importan y persisten en JCR en el autor de la a través de la importación completa o delta del producto. AEM Los datos del producto activo se replican en Publicación de la.

## AEM Experiencias del catálogo de productos con procesamiento de la

AEM AEM La función de procesamiento de experiencias de catálogo de productos se procesa sobre la marcha utilizando plantillas de catálogo de productos que se han asignado a productos y categorías, y que se pueden usar para crear experiencias de catálogo de productos. No se necesita replicación.

**CIF Versiones anteriores de la aplicación**

* CIF AEM AEM Clásico de la: Autor de la publicación crea una página de la publicación para cada categoría / producto usando la herramienta de modelo del catálogo. AEM Estas páginas se replican en Publicación de la.

>[!NOTE]
>
>CIF AEM AEM Para obtener documentación adicional sobre cómo utilizar la con el servicio administrado de la o el servicio local de la aplicación, consulte [Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
