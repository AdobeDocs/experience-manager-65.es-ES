---
title: Actualizar el tipo de licencia para la implementación
seo-title: Update the license type for the deployment
description: Actualice el tipo de licencia para la implementación mediante la página Cambiar licencia en la consola de administración.
seo-description: Update the license type for the deployment by using the Change License page in administration console.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 5%

---

# Actualizar el tipo de licencia para la implementación {#update-the-license-type-for-the-deployment}

AEM AEM Como parte del proceso de instalación de los formularios de, se ha utilizado el Administrador de configuración para configurar e implementar los módulos de formularios de formulario de que se necesita. De forma predeterminada, estos módulos se configuran con una licencia de evaluación de 60 días. Utilice la página Cambiar licencia de la consola de administración para cambiar el tipo de licencia de la implementación. Los módulos implementados actualmente se muestran en la página Cambiar licencia.

La página Cambiar licencia muestra información sobre la licencia:

* El tipo de licencia actual
* La fecha y hora de la última actualización de la licencia
* Quién realizó la última actualización
* El estado actual de la licencia
* AEM La fecha en la que se instalaron los formularios de la
* La fecha en la que caducará la licencia actual

>[!NOTE]
>
>El cambio de licencia se aplica a todos los módulos implementados. Antes de cambiar el tipo de licencia, anule la implementación de los módulos sin licencia. No seleccione el tipo de licencia de producción si la lista de módulos implementados contiene módulos distintos de los adquiridos en el Adobe.

## Actualizar el tipo de licencia {#update-the-license-type}

1. En la consola de administración, haga clic en Licencias.
1. AEM Lea el contrato de licencia para el usuario final de formularios de la plantilla, seleccione Acepto si está de acuerdo con los términos del contrato y, a continuación, haga clic en Siguiente.
1. En la página Cambiar licencia, seleccione un tipo de licencia:

   * **EVAL:** Licencia de evaluación de 60 días
   * **DESARROLLO:** Licencia de desarrollo permanente
   * **NFR:** Licencia de evaluación de 2 años
   * **IDEV:** Suscripción de 1 año al programa Adobe Developer
   * **Producción:** Licencia permanente

1. Seleccione Sí, El Cambio De Licencia Es Válido Para Todos Los Módulos Implementados.
1. Haga clic en Confirmar cambio de licencia. Aparece un mensaje que indica que la licencia se ha actualizado correctamente.
