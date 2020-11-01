---
title: Integración con Adobe Sign | Gestión de datos de usuario
seo-title: Integración con Adobe Sign | Gestión de datos de usuario
description: Integración con Adobe Sign | Gestión de datos de usuario
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Integración con Adobe Sign | Gestión de datos de usuario {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] se integra con[!DNL  Adobe Sign] para permitir flujos de trabajo de firma electrónica en formularios adaptables para procesar formularios o acuerdos para flujos de trabajo legales, de ventas, de nóminas y de gestión de recursos humanos. Permite la firma de un solo usuario y de varios usuarios, flujos de trabajo de firma secuenciales y simultáneas, la firma de formularios como un usuario anónimo o que ha iniciado sesión, y varias formas de autenticar a los usuarios.

Cuando un firmante o varios firmantes firman y envían un formulario adaptable, se genera un [!DNL Adobe Sign] acuerdo que incluye información sobre los firmantes.

Para obtener más información sobre [!DNL AEM Forms] la integración con [!DNL Adobe Sign], consulte [Uso de Adobe Sign en un formulario](/help/forms/using/working-with-adobe-sign.md)adaptable.

## Almacenes de datos y datos de usuarios {#data}

[!DNL Adobe Sign] el formulario adaptable habilitado incluye información sobre los firmantes y puede incluir otros datos de usuario recopilados por el formulario adaptable. El [!DNL Adobe Sign] servicio guarda los datos del usuario con la firma dentro del acuerdo. El acuerdo se guarda en [!DNL Adobe Sign] el servidor configurado en los servicios [!DNL AEM Forms] en la nube. Además, si el formulario adaptable está configurado para utilizar la acción de envío de Forms Portal, los datos del acuerdo se guardan en el almacén de datos del portal de formularios junto con los datos del formulario.

## Acceso y eliminación de datos de usuario {#access-and-delete-user-data}

Los datos del usuario se recopilan dentro del acuerdo pero no se guardan en ninguna de las tablas de servicios. [!DNL Adobe Sign] permite a los administradores elegir sus propias opciones en la administración de los datos que controlan en el servicio. Los administradores de privacidad del [!DNL Adobe Sign] servicio pueden lista o eliminación de acuerdos en función de la dirección de correo electrónico de un solicitante.

[!DNL Adobe Sign] oferta una aplicación web que permite la búsqueda de acuerdos por parte de los participantes y, si es necesario, su eliminación. Para obtener más información, consulte [Adobe Sign: Función: Eliminar información](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html)del usuario.

Los datos de acuerdos para formularios adaptables configurados para utilizar la acción de envío de Forms Portal también se guardan en el almacén de datos del portal de formularios. Para acceder y eliminar datos del almacén de datos del portal de formularios, consulte Portal de [Forms | Gestión de datos](/help/forms/using/forms-portal-handling-user-data.md)de usuario.
