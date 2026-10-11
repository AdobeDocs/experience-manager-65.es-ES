---
title: Cómo generar proyectos AEM con Apache Maven
description: Este documento describe cómo configurar un proyecto de AEM basado en Apache Maven
exl-id: 451913bf-bb1e-4444-aee5-968ac30b5c9d
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 24%
---
# Cómo generar proyectos AEM con Apache Maven {#how-to-build-aem-projects-using-apache-maven}

AEM 6.5 se adhiere a las prácticas recomendadas más recientes para la administración de paquetes y la estructura de proyectos, tal como se implementa mediante el último tipo de archivo del proyecto de AEM, tanto para las implementaciones locales como de AMS.

>[!TIP]
>
>Para obtener más información, consulte:
>
>* El artículo [Estructura del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=es) de la documentación de AEM as a Cloud Service sobre cómo estructurar proyectos AEM modernos.
>* Documentación de [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) para obtener información sobre cómo iniciar un nuevo proyecto de AEM con el arquetipo.
>* Artículo de [Adobe Content Package Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developer-tools/maven-plugin.html?lang=es#developer-tools) en la documentación de AEM as a Cloud Service sobre cómo implementar aplicaciones de AEM.
>
>Los tres documentos se aplican a AEM 6.5.
