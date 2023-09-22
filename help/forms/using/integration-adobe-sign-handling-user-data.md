---
title: Integración con Adobe Sign | Gestión de datos de usuario
description: Integración con Adobe Sign | Gestión de datos de usuario
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Acrobat Sign
role: Admin
exl-id: b43ed9b7-b1ef-4878-ae3b-643b558eed7b
source-git-commit: f7b24617dec77c6907798b1615debdc2329c9d80
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 63%

---

# Integración con Adobe Sign | Gestión de datos de usuario {#integration-with-adobe-sign-handling-user-data}

[!DNL AEM Forms] se integra con [!DNL  Adobe Sign] para permitir flujos de trabajo de firma electrónica en formularios adaptables para procesar formularios o acuerdos para flujos de trabajo legales, de ventas, nóminas y administración de recursos humanos. Permite la firma de un solo usuario y de varios, flujos de trabajo de firma secuenciales y simultáneos, la firma de formularios como un usuario anónimo o con la sesión iniciada, y múltiples formas de autenticar a los usuarios.

Cuando un firmante o varios firmantes firman y envían un formulario adaptable, se genera un acuerdo de [!DNL Adobe Sign] que contiene información sobre los firmantes.

Para obtener más información acerca de la integración de [!DNL AEM Forms] con [!DNL Adobe Sign], consulte [Uso de Adobe Sign en un formulario adaptable](/help/forms/using/working-with-adobe-sign.md).

## Almacenamiento de datos y datos de usuarios {#data}

Un formulario adaptable habilitado de [!DNL Adobe Sign] contiene información sobre los firmantes y puede incluir otros datos de usuario recopilados por el formulario adaptable. El servicio [!DNL Adobe Sign] guarda los datos de usuario con la firma del acuerdo. El acuerdo se guarda en un [!DNL Adobe Sign] servidor configurado en [!DNL AEM Forms] cloud services. Además, si el formulario adaptable está configurado para utilizar la acción de envío del portal de Forms, los datos del acuerdo se guardan en el almacén de datos del portal de Forms junto con los datos del formulario.

## Acceder y eliminar datos de usuario {#access-and-delete-user-data}

Los datos de usuario se recopilan en el acuerdo, pero no se guardan en ninguna de las tablas de los servicios. [!DNL Adobe Sign] permite a los administradores realizar sus propias elecciones en la administración de los datos que controlan en el servicio. Los administradores de privacidad del servicio de [!DNL Adobe Sign] pueden ver una lista de los acuerdos o eliminarlos en función de la dirección de correo electrónico de un solicitante.

[!DNL Adobe Sign] ofrece una aplicación web que permite buscar acuerdos por parte de los participantes y, si es necesario, eliminarlos. Para obtener más información, consulte [Adobe Sign - Función: Eliminar información del usuario](https://helpx.adobe.com/es/sign/using/gdpr-compliance.html).

Los datos de acuerdo de los formularios adaptables configurados para utilizar la acción de envío del portal de Forms también se guardan en el almacén de datos del portal de Forms. Para acceder al almacén de datos del portal de Forms y eliminarlo, consulte [Portal de Forms | Gestión de datos de usuario](/help/forms/using/forms-portal-handling-user-data.md).
