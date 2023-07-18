---
title: Campaign Management
description: La administración de campañas ofrece a los especialistas en marketing digital la oportunidad de ofrecer contenido personalizado y, por lo tanto, crear experiencias dedicadas para los visitantes. Le permite organizar sus campañas de marketing en la web, el correo electrónico y los servicios móviles, y así atraer a sus visitantes.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: ae08247c7be0824151637d744f17665c3bd82f2d
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---


# Campaign Management{#campaign-management}

La administración de campañas ofrece a los especialistas en marketing digital la oportunidad de ofrecer contenido personalizado y, por lo tanto, crear experiencias dedicadas para los visitantes.

Le permite organizar sus campañas de marketing en la web, el correo electrónico y los servicios móviles, y así atraer a sus visitantes. Puede crear contenido, segmentar visitantes, insertar y promocionar contenido segmentado para perfiles de usuario específicos y administrar campañas en varios canales.

Este documento describe los distintos elementos que componen las campañas. Encontrará información más detallada en los siguientes documentos:

* [Teasers and Strategies](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [Marketing por correo electrónico](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [Páginas de destino](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Ofertas de Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Trabajar con el administrador de campañas de marketing](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [Información acerca de la segmentación](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [Configuración de la campaña](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

La administración de campañas se compone de varios elementos:

* **Marcas**
En Adobe Experience Manager AEM (), las marcas son la unidad de nivel superior y forman una colección de **Campañas**.

* **Campañas**
Una campaña es una colección de individuos **Experiencias**.

* **Experiencias**
El contenido centrado forma las distintas experiencias, presentadas al visitante en **Touchpoints**. Hay varios tipos de experiencia disponibles:

   * **Teasers**
     [Páginas teaser/párrafos](#teasers) se utilizan para dirigir a visitantes específicos **Segmentos** al contenido que se centra en sus intereses.

     Las páginas teaser pueden:

      * presentar una serie de opciones para que el visitante elija entre ellas
      * mostrar solo un párrafo de teaser basado en el segmento específico del visitante. Por ejemplo, el párrafo de teaser que se muestra puede depender de la edad del visitante.

     Normalmente, una página teaser es una acción temporal que dura un período de tiempo específico, hasta que se reemplaza por la siguiente página de teaser.

   * **Newsletters**

     [Comunicaciones por correo electrónico](#emailmarketing) se utilizan para atraer a los usuarios y animarlos a que visiten su sitio web. Normalmente se envían en forma de newsletter a su **Posibles clientes** (agrupadas en **Listas**). **Nota:** El Adobe no tiene previsto seguir mejorando esta capacidad. La recomendación es [uso de Adobe Campaign AEM y la integración para la creación de informes de](/help/sites-administering/campaign.md).

   * **Adobe Target**

     Esto permite la integración con Adobe Target (anteriormente Test&amp;Target), que proporciona a los especialistas en mercadotecnia una herramienta de optimización de sitios web de conversión con las funciones necesarias para garantizar que el contenido y las ofertas en línea sean relevantes para las buenas conversiones que produzcan los clientes. Adobe Target proporciona una interfaz intuitiva para diseñar y ejecutar pruebas, crear segmentos de audiencia y segmentar contenido desde una sola aplicación.

* **Puntos de contacto**

  Estos son los puntos de contacto entre el visitante y la campaña. Los puntos de contacto están conectados a las experiencias que ha creado.

  Por ejemplo, para los teasers, es la página de contenido donde se encuentra el párrafo de teaser; para un boletín, es la lista de correo.

* **posibles clientes**

  La información que ha recopilado sobre sus visitantes y cómo ponerse en contacto con ellos forma la base de sus posibles clientes. **Nota:** El Adobe no tiene previsto seguir mejorando esta capacidad.

  La recomendación es [uso de Adobe Campaign AEM y la integración para la creación de informes de](/help/sites-administering/campaign.md).

* **Listas**

  Los posibles clientes se agrupan en listas para que pueda realizar acciones colectivas en consecuencia. Nota: **Nota:** El Adobe no tiene previsto seguir mejorando esta capacidad.

  La recomendación es [utilice Adobe Campaign AEM y la integración para.](/help/sites-administering/campaign.md)

* **Segmentos**

  Los visitantes del sitio tienen diferentes intereses y objetivos cuando llegan a un sitio. Analizar esto según factores como la actividad en el sitio web, la información de perfil registrada y la actividad en otros sitios web, le ayuda a definir segmentos. El contenido puede personalizarse según las necesidades y los intereses del visitante, según los segmentos con los que coincidan.

* **MCM**

  El Administrador de campañas de marketing (MCM) es una consola que le permite acceder a toda la funcionalidad que necesita para crear y controlar campañas, marcas, experiencias, puntos de contacto, posibles clientes, listas, segmentos e informes.

  Se puede acceder a él desde varias ubicaciones (etiquetadas como **Campañas**) o, por ejemplo, con la dirección URL:

  `http://localhost:4502/libs/mcm/content/admin.html`
