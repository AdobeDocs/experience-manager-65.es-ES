---
title: Configurar puntos finales remotos
description: Obtenga información sobre cómo configurar extremos remotos. En este documento se explica cómo habilitar la aplicación generada con Flex AEM para invocar el servicio mediante los formularios Remoting de la aplicación de forma remota de la aplicación de la aplicación de formularios de la aplicación de forma remota.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 4%

---

# Configurar puntos finales remotos {#configuring-remoting-endpoints}

Un extremo de comunicación remota permite que una aplicación creada con Flex AEM AEM invoque el servicio mediante (obsoleto para formularios de datos) la comunicación remota a través de formularios de datos de la aplicación (obsoleto) de los formularios de la aplicación de comunicación remota. Se crea automáticamente un extremo remoto para cada servicio activado. Se crea un destino de Flex con el mismo nombre que el extremo y los clientes de Flex pueden crear objetos remotos que apunten a este destino para invocar operaciones en el servicio correspondiente.

## Configuración del extremo remoto {#remoting-endpoint-settings}

**Método de autenticación de cliente de Flex:** Determina el tipo de respuesta que el servidor devuelve al cliente cuando el servicio invocado está habilitado para la seguridad, la operación invocada no admite invocaciones anónimas y el cliente pasa credenciales no válidas o no válidas.
