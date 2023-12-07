---
title: Administración programática de PreferencesNodes
description: Utilice la API del servicio Administrador de preferencias (Java) para administrar mediante programación los nodos de preferencias.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 108eb249-879b-4e4f-b431-8118b8656e62
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 2%

---

# Administración programática de los nodos de preferencias {#programmatically-managing-the-preferencesnodes}

**Los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

En este tema se describe cómo se puede utilizar la API del servicio Administrador de preferencias (Java) para administrar mediante programación los nodos de preferencias.

Puede cambiar manualmente las opciones de configuración desde la IU del administrador. Para cambiar las opciones, vaya a `Home>Settings>User Management> Configuration>Manual Configuration`. Importar `config.xml` después de realizar los cambios, observará que todos los cambios excepto los realizados en el nodo `/Adobe/Adobe Experience Manager Forms/Config/UM persist` se pierden. La vista previa de Administración de usuarios Importar y exportar no admite el cambio de los valores de configuración de otros componentes. Ahora, estos cambios se pueden realizar utilizando `PreferencesManagerServiceClient` API.

**Resumen de los pasos** Para administrar mediante programación los nodos de preferencias, realice los siguientes pasos:

1. Incluir archivos de proyecto.
1. Crear un cliente PreferencesManagerService
1. Invocar las operaciones de rol o permiso adecuadas

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente mediante Java, incluya los archivos JAR necesarios. Si utiliza servicios web, asegúrese de incluir los archivos proxy.

**Crear un cliente PreferencesManagerService**

Para poder realizar mediante programación una operación de User Management PreferencesManagerService, debe crear un cliente PreferencesManagerService. Con la API de Java, esto se logra creando un objeto PreferencesManagerServiceClient.

**Invocar las operaciones de rol o permiso adecuadas**

Una vez creado el cliente de servicio, puede invocar las operaciones del Administrador de preferencias. El cliente de servicio le permite leer y establecer permisos.
