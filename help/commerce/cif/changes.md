---
title: Cambios importantes en el complemento de Commerce integration framework CIF ()
description: Cambios importantes en el complemento de Commerce integration framework CIF CIF () en comparación con las versiones anteriores de la versión de la versión de la.
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Cambios importantes en el complemento de Commerce integration framework CIF (){#notable-changes}

En este documento se destacan las importantes diferencias entre el complemento de Commerce integration framework CIF CIF CIF CIF () y las versiones de antiguas, conocidas principalmente como Classic (Quickstart) y las versiones de código abierto de la aplicación de código abierto de la aplicación de código abierto de la aplicación de código abierto de la aplicación de código abierto de la.

## Instalación y actualizaciones

AEM CIF AEM El paquete de complementos de se instala y actualiza con el Administrador de paquetes de.

CIF **Versiones anteriores**

* CIF CIF Clásico: no se necesita instalación, ya que el inicio rápido era parte de la instalación de, por lo tanto, no se requiere instalación. CIF AEM Las actualizaciones de la versión de la aplicación de datos formaban parte de las actualizaciones regulares de los paquetes de servicio o de la
* CIF Código abierto: instalación a través de GitHub. Las actualizaciones formaban parte del trabajo de actualización/mantenimiento manual.

## Configuración de extremo

El extremo se configura mediante la consola OSGi.

CIF **Versiones anteriores**

* CIF AEM Clásico: configuración mediante OSGi en el
* CIF CIF Código abierto: A través del explorador de configuración de la

## CIF Implementación del proyecto Venia de la

El proyecto está disponible en [GitHub AEM Guides CIF AEM - Proyecto Venia de la](https://github.com/adobe/aem-cif-guides-venia) y la implementación se realizó mediante el Administrador de paquetes de la aplicación de GitHub.

CIF **Versiones anteriores**

* CIF AEM Clásico: mediante la instalación del paquete de

## Datos del catálogo de productos

Los datos del catálogo de productos se solicitan bajo demanda mediante llamadas en tiempo real a un extremo externo que admite las API de GraphQL requeridas. Estas API admiten el acceso a datos activos o clasificados en cualquier fecha determinada. No se necesita replicación.

CIF **Versiones anteriores**

* CIF AEM Clásico: los datos de producto en vivo y clasificados se importan y persisten en JCR en el autor de la a través de la importación completa o delta del producto. AEM Los datos del producto activo se replican en Publish de forma.

## AEM Experiencias del catálogo de productos con procesamiento de la

AEM AEM La función de procesamiento de experiencias de catálogo de productos se procesa sobre la marcha utilizando plantillas de catálogo de productos que se han asignado a productos y categorías, y que se pueden usar para crear experiencias de catálogo de productos. No se necesita replicación.

CIF **Versiones anteriores**

* CIF AEM AEM Clásico de la: Autor de la publicación crea una página de la publicación para cada categoría / producto usando la herramienta de modelo del catálogo. AEM Estas páginas se replican en Publish de forma.

>[!NOTE]
>
>CIF AEM AEM Para obtener documentación adicional sobre cómo usar el servicio administrado por el usuario o el servicio administrado por el usuario en las instalaciones, consulte [Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html) para obtener más información sobre cómo usar el servicio administrado por el usuario o el servicio administrado por el usuario en las instalaciones del usuario de forma local
