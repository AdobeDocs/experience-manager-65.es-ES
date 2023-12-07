---
title: Configurar puntos finales remotos
description: Obtenga información sobre cómo configurar extremos remotos. En este documento se explica cómo habilitar la aplicación generada con Flex AEM para invocar el servicio mediante los formularios Remoting de la aplicación de forma remota de la aplicación de la aplicación de formularios de la aplicación de forma remota.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 4%

---

# Configurar puntos finales remotos {#configuring-remoting-endpoints}

Un extremo de comunicación remota permite que una aplicación creada con Flex AEM AEM invoque el servicio mediante (obsoleto para formularios de datos) la comunicación remota a través de formularios de datos de la aplicación (obsoleto) de los formularios de la aplicación de comunicación remota. Se crea automáticamente un extremo remoto para cada servicio activado. Se crea un destino de Flex con el mismo nombre que el extremo y los clientes de Flex pueden crear objetos remotos que apunten a este destino para invocar operaciones en el servicio correspondiente.

## Configuración del extremo remoto {#remoting-endpoint-settings}

**Método de autenticación de cliente de Flex:** Determina el tipo de respuesta que el servidor devuelve al cliente cuando el servicio invocado está habilitado para la seguridad, la operación invocada no admite invocaciones anónimas y el cliente pasa credenciales no válidas o no válidas.
