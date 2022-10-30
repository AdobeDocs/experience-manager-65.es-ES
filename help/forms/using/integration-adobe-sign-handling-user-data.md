---
title: Integración con Adobe Sign | Gestión de datos de usuario
seo-title: Integration with Adobe Sign | Handling user data
description: Integración con Adobe Sign | Gestión de datos de usuario
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: 28d092a7713438c27213766f0bb702b699305b88
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 3%

---

# Integración con Adobe Sign | Gestión de datos de usuario {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] se integra con[!DNL  Adobe Sign] para permitir flujos de trabajo de firma electrónica en formularios adaptables para procesar formularios o acuerdos para flujos de trabajo legales, de ventas, de nóminas y de gestión de recursos humanos. Permite la firma de un solo usuario y de varios usuarios, flujos de trabajo de firma secuenciales y simultáneos, la firma de formularios como usuario anónimo o que ha iniciado sesión y múltiples formas de autenticar a los usuarios.

Cuando un firmante o varios firmantes firmen y envíen un formulario adaptable, [!DNL Adobe Sign] se genera un acuerdo que incluye información sobre los firmantes.

Para obtener más información, consulte [!DNL AEM Forms] integración con [!DNL Adobe Sign], consulte [Uso de Adobe Sign en un formulario adaptable](/help/forms/using/working-with-adobe-sign.md).

## Almacenamiento de datos y datos de usuarios {#data}

[!DNL Adobe Sign] el formulario adaptable habilitado incluye información sobre los firmantes y puede incluir otros datos de usuario recopilados por el formulario adaptable. La variable [!DNL Adobe Sign] guarda los datos de usuario con la firma del acuerdo. El acuerdo se guarda en [!DNL Adobe Sign] servidor configurado en [!DNL AEM Forms] servicios en la nube. Además, si el formulario adaptable está configurado para utilizar la acción de envío de Forms Portal, los datos del acuerdo se guardan en el almacén de datos del portal de formularios junto con los datos del formulario.

## Acceso y eliminación de datos de usuario {#access-and-delete-user-data}

Los datos de usuario se recopilan dentro del acuerdo, pero no se guardan en ninguna de las tablas de servicios. [!DNL Adobe Sign] permite a los administradores realizar sus propias elecciones en la administración de datos que controlan en el servicio. Administradores de privacidad en la [!DNL Adobe Sign] puede enumerar o eliminar acuerdos basados en la dirección de correo electrónico de un solicitante.

[!DNL Adobe Sign] ofrece una aplicación web que permite buscar acuerdos por parte de los participantes y, si es necesario, eliminarlos. Para obtener más información, consulte [Adobe Sign: función: Eliminar información del usuario](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

Los datos de acuerdos para formularios adaptables configurados para utilizar la acción de envío de Forms Portal también se guardan en el almacén de datos del portal de formularios. Para acceder y eliminar datos del almacén de datos del portal de formularios, consulte [Portal de Forms | Gestión de datos de usuario](/help/forms/using/forms-portal-handling-user-data.md).
