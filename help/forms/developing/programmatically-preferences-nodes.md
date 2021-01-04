---
title: Administración programática de los PreferenciasNodes
seo-title: Administración programática de los PreferenciasNodes
description: Utilice la API de servicio de Administrador de preferencias (Java) para administrar mediante programación los nodos de preferencias.
seo-description: Utilice la API de servicio de Administrador de preferencias (Java) para administrar mediante programación los nodos de preferencias.
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Administración mediante programación de los nodos de preferencias {#programmatically-managing-the-preferencesnodes}

En este tema se describe cómo puede utilizar la API de servicio de Administrador de preferencias (Java) para administrar mediante programación los nodos de preferencias.

Puede cambiar manualmente la configuración desde la interfaz de usuario del administrador. Para cambiar las opciones, vaya a `Home>Settings>User Management> Configuration>Manual Configuration`. Importe `config.xml` después de realizar los cambios, observará que se pierden todos los cambios excepto los realizados en el nodo `/Adobe/Adobe Experience Manager Forms/Config/UM persist`. La previsualización de Importación y exportación de Administración de usuarios no admite el cambio de la configuración de otros componentes. Ahora, estos cambios se pueden realizar mediante `PreferencesManagerServiceClient` API.

**Resumen de** pasosPara administrar mediante programación los nodos de preferencias, lleve a cabo los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un cliente PreferencesManagerService
1. Invocar la función o las operaciones de permisos correspondientes

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si va a crear una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios Web, asegúrese de incluir los archivos proxy.

**Crear un cliente PreferencesManagerService**

Para poder realizar mediante programación una operación User Management PreferencesManagerService, debe crear un cliente PreferencesManagerService. Con la API de Java esto se logra creando un objeto PreferencesManagerServiceClient.

**Invocar la función o las operaciones de permisos correspondientes**

Una vez creado el cliente de servicio, puede invocar las operaciones del Administrador de preferencias. El cliente de servicios le permite leer y establecer permisos.
