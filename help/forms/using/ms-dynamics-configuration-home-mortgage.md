---
title: Configuración de Microsoft Dynamics 365 para el flujo de trabajo de la hipoteca de origen del sitio de referencia de We.Finance
seo-title: Configure Microsoft Dynamics 365 for the home mortgage workflow of the We.Finance reference site
description: Aprenda a aprovechar los servicios de Microsoft® Dynamics 365 a través de formularios adaptables para el flujo de trabajo de la hipoteca para el hogar del sitio de referencia de We.Finance
seo-description: Learn how to leverage the Microsoft® Dynamics 365 services through adaptive forms for the home mortgage workflow of the We.Finance Reference site
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: develop, Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
exl-id: 2ac37dc5-d88d-4f98-8576-cd2ca6f0ea3a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# Configuración de Microsoft Dynamics 365 para el flujo de trabajo de la hipoteca de origen del sitio de referencia de We.Finance {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

Aprenda a aprovechar los servicios de Microsoft® Dynamics 365 a través de formularios adaptables para el flujo de trabajo de la hipoteca para el hogar del sitio de referencia de We.Finance

## Información general {#overview}

Microsoft® Dynamics 365 es un software de Administración de la relación con los clientes (CRM) y Planificación de recursos empresariales (ERP) que proporciona soluciones empresariales para crear y administrar cuentas de clientes, contactos, posibles clientes, oportunidades y casos.

AEM Forms proporciona un servicio en la nube para integrar Dynamics 365 con [Integración de datos de Forms](/help/forms/using/data-integration.md) módulo. Antes de poder usar el tutorial de la aplicación hipotecaria doméstica con Microsoft® Dynamics, debe configurar Microsoft® Dynamics 365 para que se utilice con el sitio de referencia de We.Finance.

## Requisitos previos {#prerequisites}

Antes de empezar a configurar Dynamics 365, asegúrese de que:

* AEM 6.3 Forms Service Pack 1 y posterior
* Cuenta de Microsoft® Dynamics 365
* Aplicación registrada para el servicio Dynamics 365 con Microsoft® Azure Active Directory
* ID de cliente y secreto de cliente para la aplicación registrada

## Vincule la calculadora de hipoteca de origen con la página de inicio del sitio {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. En la instancia de autor, vaya a la siguiente página:

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. Desplácese hacia abajo hasta la Calculadora de Hipotecas Domésticas.
1. Resalte el panel de la columna derecha (calculadora) y pulse para mostrar el menú emergente. En el menú emergente, pulse Configurar. Aparecerá el cuadro de diálogo Editar contenedor de AEM Forms.

   ![calculatorconfigurepanel](assets/calculatorconfigurepanel.png)

1. En el cuadro de diálogo Editar contenedor de AEM Forms , busque la ruta del recurso y seleccione la calculadora de hipotecas domésticas en la siguiente ruta y pulse **Confirmar**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. Pulse **Listo**.
1. Publique la página editada.

   >[!NOTE]
   >
   >El enlace de los campos de la calculadora con el FDM está preconfigurado a través del paquete del sitio de referencia We.Finance. Para ver el enlace, puede abrir el formulario en el modo de creación y ver las referencias de enlace de campo.

1. Para crear una entidad personalizada para almacenar el registro de solicitante para la aplicación de hipoteca, importe el paquete de la solución AEMFormsFSIRefsite_1_0.zip a su instancia de Microsoft® Dynamics:

   1. Descargue el paquete desde:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. Importe el paquete de soluciones a la instancia de Microsoft® Dynamics. En la instancia de Microsoft® Dynamics, vaya a **Configuración** > **Soluciones** y, a continuación, toque **Importar**.

1. Para configurar los detalles de contacto del usuario utilizados en el refsite, importe el paquete Sarah Rose Contact.CSV a su instancia de Microsoft® Dynamics:

   1. Descargue el paquete desde:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. Importe el paquete a la instancia de Microsoft® Dynamics. En la instancia de Microsoft® Dynamics, vaya a **Ventas** > **Contactos** y, a continuación, toque **Importar datos**.
