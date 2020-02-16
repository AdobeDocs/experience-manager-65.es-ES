---
title: Configuración de los extremos de Remoting
seo-title: Configuración de los extremos de Remoting
description: Obtenga información sobre cómo configurar los extremos remotos.
seo-description: Obtenga información sobre cómo configurar los extremos remotos.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuración de los extremos de Remoting {#configuring-remoting-endpoints}

Un extremo remoto permite que una aplicación creada con Flex invoque el servicio mediante AEM forms Remoting (obsoleto para formularios AEM). Se crea automáticamente un extremo remoto para cada servicio activado. Se crea un destino de Flex con el mismo nombre que el extremo y los clientes de Flex pueden crear objetos remotos que apunten a este destino para invocar operaciones en el servicio correspondiente.

## Configuración de punto final remoto {#remoting-endpoint-settings}

**** Método de autenticación del cliente de Flex: Determina el tipo de respuesta que el servidor devuelve al cliente cuando el servicio invocado está habilitado para la seguridad, la operación invocada no admite invocaciones anónimas y el cliente pasa credenciales no válidas o no válidas.
