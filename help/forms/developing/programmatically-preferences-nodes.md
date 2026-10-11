---
title: Administración programática de PreferencesNodes
description: Utilice la API del servicio Administrador de preferencias (Java) para administrar mediante programación los nodos de preferencias.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 108eb249-879b-4e4f-b431-8118b8656e62
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 516393bc-fa69-5e74-a04e-f7ec9ffe2c5e
    internal-label: APIs & Integrations
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%
---
# Administración programática de los nodos de preferencias {#programmatically-managing-the-preferencesnodes}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

En este tema se describe cómo se puede utilizar la API del servicio Administrador de preferencias (Java) para administrar mediante programación los nodos de preferencias.

Puede cambiar manualmente las opciones de configuración desde la IU del administrador. Para cambiar las opciones, vaya a `Home>Settings>User Management> Configuration>Manual Configuration`. Importe `config.xml` después de realizar los cambios, observará que se pierden todos los cambios excepto los realizados en el nodo `/Adobe/Adobe Experience Manager Forms/Config/UM persist`. La vista previa de Administración de usuarios Importar y exportar no admite el cambio de los valores de configuración de otros componentes. Ahora, estos cambios se pueden realizar usando las API `PreferencesManagerServiceClient`.

**Resumen de pasos** Para administrar mediante programación los nodos de preferencias, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un cliente PreferencesManagerService
1. Invocar las operaciones de rol o permiso adecuadas

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente de PreferencesManagerService**

Para poder realizar mediante programación una operación de User Management PreferencesManagerService, debe crear un cliente PreferencesManagerService. Con la API de Java, esto se logra creando un objeto PreferencesManagerServiceClient.

**Invocar las operaciones de rol o permiso correspondientes**

Una vez creado el cliente de servicio, puede invocar las operaciones del Administrador de preferencias. El cliente de servicio le permite leer y establecer permisos.
