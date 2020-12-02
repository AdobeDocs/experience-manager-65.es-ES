---
title: Administración de campañas
seo-title: Administración de campañas
description: La administración de campañas permite que los especialistas en marketing digital ofrezcan contenido personalizado y creen experiencias dedicadas para los visitantes. Le permite organizar sus campañas de marketing en Internet, correo electrónico y servicios móviles para interactuar con los clientes.
seo-description: La administración de campañas permite que los especialistas en marketing digital ofrezcan contenido personalizado y creen experiencias dedicadas para los visitantes. Le permite organizar sus campañas de marketing en Internet, correo electrónico y servicios móviles para interactuar con los clientes.
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 94%

---


# Administración de campañas{#campaign-management}

La administración de campañas permite que los especialistas en marketing digital ofrezcan contenido personalizado y creen experiencias dedicadas para los visitantes.

Le permite organizar sus campañas de marketing en Internet, correo electrónico y servicios móviles para interactuar con los clientes. Puede crear contenido, segmentar a los visitantes, enviar y promocionar contenido orientado a perfiles de usuario específicos y administrar campañas en varios canales.

Este documento describe los elementos diversos que componen las campañas. Tiene disponible más información detallada en los siguientes documentos:

* [Teasers y estrategias](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [Marketing por correo electrónico](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [Páginas de aterrizaje](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Ofertas de destino](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Uso del administrador de campañas de marketing](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [Información acerca de la segmentación](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [Configuración de la campaña](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

La administración de campañas consta de varios elementos:

* **Marcas**
En AEM, las marcas son la unidad de nivel superior y forman una colección de 
**Campañas**.

* ****
Campañas Una campaña es una colección de elementos individuales 
**Experiencias**.

* ****
ExperienciasEl contenido centrado forma las distintas experiencias, presentadas al visitante en 
**Touchpoints**. Existen varios tipos de experiencia:

   * **Teasers**
      [Las páginas o los párrafos de teaser](#teasers) se utilizan para dirigir **Segmentos** de visitantes específicos a contenido centrado en sus intereses.

      Las páginas de teaser pueden:

      * presentar una gama de opciones que los visitantes pueden elegir
      * mostrar solo un párrafo de teaser basado en un segmento de visitantes específico; por ejemplo, puede ser que el párrafo de teaser que se muestre dependa de la edad del visitante.

      Generalmente una página de teaser es una acción temporal que durará un período específico de tiempo, hasta que se sustituya por la siguiente página.

   * **Boletines**

      [Las comunicaciones por correo electrónico ](#emailmarketing) se usan para atraer usuarios y animarlos a que visiten su sitio web. Normalmente se formulan como un boletín que se envía a los **Posibles clientes** (que suelen agruparse en **Listas**). **Nota:** Adobe no tiene previsto mejorar esta capacidad. La recomendación es [ aprovechar Adobe Campaign y la integración a AEM](/help/sites-administering/campaign.md).

   * **Adobe Target**

      Permite la integración con Adobe Target (antes conocido como Test&amp;Target), lo que proporciona a los especialistas en marketing una herramienta de optimización de sitio web de conversión con las capacidades necesarias para que las ofertas y el contenido en línea sigan siendo relevantes para los clientes, lo que resulta en más conversiones. Adobe Target ofrece una interfaz intuitiva para diseñar y ejecutar pruebas, crear segmentos de audiencia y contenido de segmentación, todo ello desde una sola aplicación.


* **Touchpoints**

   Son puntos de contacto entre el visitante y la campaña. Los touchpoints están conectados con las experiencias creadas.

   Por ejemplo, para los teasers, es la página de contenido en la que está situado el párrafo de teaser; para una newsletter, la lista de correo.

* **Posibles clientes**

   La información recopilada sobre los visitantes y cómo ponerse en contacto con ellos forma la base de los posibles clientes. **Nota:** Adobe no tiene previsto mejorar esta capacidad.

   La recomendación es [ aprovechar Adobe Campaign y la integración a AEM](/help/sites-administering/campaign.md).

* **Listas**

   Normalmente, los posibles clientes se agrupan en listas para que pueda aplicar una acción colectiva. **Nota:** Adobe no tiene previsto mejorar esta capacidad.

   La recomendación es [ aprovechar Adobe Campaign y la integración a AEM.](/help/sites-administering/campaign.md)

* **Segmentos**

   Los visitantes del sitio tienen diferentes intereses y objetivos cuando acceden al sitio. Si se analizan según factores como la actividad del sitio web, la información de perfil registrada y las actividades en otros sitios web, se podrán definir segmentos. A continuación, se podrá mostrar contenido que satisfará las necesidades y los intereses específicos de los visitantes según los segmentos con los que coincidan.

* **MCM**

   Marketing Campaign Manager (MCM) es una consola que le permite acceder a la funcionalidad necesaria para crear y controlar sus campañas, marcas, experiencias, touchpoints, posibles clientes, listas, segmentos e informes.

   Se puede acceder a MCM desde varias ubicaciones (denominadas **Campañas** o, por ejemplo, con la URL:

   `http://localhost:4502/libs/mcm/content/admin.html`

