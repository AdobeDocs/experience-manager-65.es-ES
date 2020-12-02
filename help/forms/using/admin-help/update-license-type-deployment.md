---
title: Actualizar el tipo de licencia para la implementación
seo-title: Actualizar el tipo de licencia para la implementación
description: Actualice el tipo de licencia para la implementación mediante la página Cambiar licencia de la consola de administración.
seo-description: Actualice el tipo de licencia para la implementación mediante la página Cambiar licencia de la consola de administración.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# Actualice el tipo de licencia para la implementación {#update-the-license-type-for-the-deployment}

Como parte del proceso de instalación de formularios AEM, se ha utilizado Configuration Manager para configurar e implementar los módulos de formularios AEM que se requieren. De forma predeterminada, estos módulos se configuran con una licencia de evaluación de 60 días. Utilice la página Cambiar licencia de la consola de administración para cambiar el tipo de licencia de la implementación. Los módulos implementados actualmente se muestran en la página Cambiar licencia.

La página Cambiar licencia muestra información sobre la licencia:

* El tipo de licencia actual
* Fecha y hora de la última actualización de la licencia
* Quién realizó la última actualización
* Estado actual de la licencia
* La fecha en que se instalaron AEM formularios
* La fecha de caducidad de la licencia actual

>[!NOTE]
>
>El cambio de licencia se aplica a todos los módulos implementados. Antes de cambiar el tipo de licencia, anule la implementación de los módulos que no tengan licencia. No seleccione el tipo de licencia de producción si la lista de los módulos implementados contiene módulos distintos de los adquiridos en Adobe.

## Actualice el tipo de licencia {#update-the-license-type}

1. En la consola de administración, haga clic en Licencias.
1. Lea el contrato de licencia de usuario final de los formularios AEM, seleccione Acepto si está de acuerdo con los términos del acuerdo y, a continuación, haga clic en Siguiente.
1. En la página Cambiar licencia, seleccione un tipo de licencia:

   * **EVAL: licencia de evaluación de** 60 días
   * **DEV:Licencia** de desarrollo permanente
   * **NFR:licencia de evaluación de** dos años
   * **IDEV:** 1 año de suscripción al Programa de desarrolladores de Adobe
   * **Producción:Licencia** perpetua

1. Seleccione Sí, el cambio de licencia es válido para todos los módulos implementados.
1. Haga clic en Confirmar cambio de licencia. Aparece un mensaje que indica que la licencia se ha actualizado correctamente.

