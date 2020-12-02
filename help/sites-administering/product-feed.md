---
title: Alimentación de productos
seo-title: Alimentación de productos
description: Obtenga información sobre la fuente de productos AEM.
seo-description: Obtenga información sobre la fuente de productos AEM.
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 2%

---


# Alimentación de productos {#product-feed}

AEM se integra con [Search&amp;Promote](https://www.adobe.com/solutions/testing-targeting/searchandpromote.html) y le permite:

* utilice la API de comercio electrónico, independientemente de la estructura de repositorio subyacente y la plataforma de comercio.
* aproveche la función Conector de índice de Search&amp;Promote para proporcionar una fuente de producto en formato XML.
* aproveche la función de control remoto de Search&amp;Promote para realizar solicitudes a petición o programadas de la fuente de productos
* generación de fuentes para distintas cuentas de Search&amp;Promote, configuradas como configuraciones de servicios en la nube.

Debe tener una cuenta válida y [configurar la conexión a Search&amp;Promote](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote). También debe comprobar que está utilizando el [centro de datos](/help/sites-administering/search-and-promote.md#configuring-the-data-center) correcto y asegurarse de que el **URI del servidor remoto **está configurado.

## Configurar la fuente de productos {#set-up-the-product-feed}

Primero debe introducir una raíz del sitio Web y un atributo de identificador. Para ello:

1. Vaya a la configuración de la Search&amp;Promote.
1. Haga clic en **[!UICONTROL Editar]**.
1. Haga clic en la ficha **[!UICONTROL Configuración de fuente del conector de índice]**.
1. Escriba el **[!UICONTROL atributo de identificador]** y **[!UICONTROL raíz del sitio Web]**.

   >[!NOTE]
   >
   >La **[!UICONTROL raíz del sitio Web]** es la raíz del sitio Web de comercio electrónico, por ejemplo `/content/geometrixx-outdoors/en`.
   >
   >El atributo **[!UICONTROL identificador]** es una propiedad JCR que identifica de forma única al producto: `identifier`.

1. Haga clic en **[!UICONTROL Aceptar]**.

A continuación, también debe editar dos configuraciones en la consola web para poder generar fuentes de productos.

### Configuración de la implementación de Crawler de productos de CQ Day para Geometrixx {#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}

1. Vaya a [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Haga clic en **[!UICONTROL Implementación del explorador de productos de CQ de día para Geometrixx]**.
1. Especifique el número de cuenta de Search&amp;Promote al que está vinculado este explorador. Se utilizará para buscar la configuración de servicios en la nube utilizada por este buscador.
1. Haga clic en **[!UICONTROL Guardar]**.

### Configuración del generador de fuentes de productos de CQ para el día de Search&amp;Promote para Geometrixx {#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}

1. Vaya a [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Haga clic en **[!UICONTROL Generador de fuentes de productos de Search&amp;Promote CQ para Geometrixx]**.
1. Especifique el número de cuenta de Search&amp;Promote al que está vinculado este generador. Se utilizará para buscar la configuración de servicios en la nube utilizada por este generador.
1. Haga clic en **[!UICONTROL Guardar]**.

## Programar la fuente de productos {#schedule-the-product-feed}

Para habilitar la generación programada de fuentes, debe configurar un Planificador para ella.
Un Planificador se configura como una configuración secundaria de la configuración de servicios de Search&amp;Promote cloud específica.

1. Vaya a la configuración de la Search&amp;Promote.
1. Haga clic en **[!UICONTROL +]** junto a **[!UICONTROL configuración del Planificador]**.
1. Escriba un **[!UICONTROL Título]** reconocible para los autores de la página y un **[!UICONTROL Nombre]** único.
1. Haga clic en **[!UICONTROL Crear]**. Se abre un cuadro de diálogo.

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. Introduzca la **[!UICONTROL Contraseña de control remoto]**. Es la contraseña que configuró en su cuenta de Search&amp;Pronote.

   >[!NOTE]
   >
   >Esta no es la contraseña de su cuenta de Search&amp;Promote. Puede encontrar y cambiar esta contraseña iniciando sesión en su cuenta de Search&amp;Promote y yendo a **[!UICONTROL Index]** y luego a **[!UICONTROL Remote Control]**.

1. Marque la casilla **[!UICONTROL Habilitar programación]**.
1. Seleccione una **[!UICONTROL Programación]**. Es el programa de generación de fuentes real.
1. Habilite la **[!UICONTROL indexación bajo demanda]** o no. Esta función se utiliza para llamar manualmente al índice de Search&amp;Promote. Si **[!UICONTROL solicita una fuente de productos completa]** está marcada, Search&amp;Promote solicitará una fuente de productos completa. De lo contrario, se solicita una fuente de productos incremental.

   >[!NOTE]
   >
   >La función de indexación a petición utiliza la función de control remoto de Search&amp;Promote. Cuando se llama a una indexación remota, la indexación no se inicio inmediatamente, pero se publicará una solicitud de indización en Search&amp;Promote mediante la función de control remoto.

1. Haga clic en **[!UICONTROL Aceptar]**.

Ahora que ha configurado todo, puede ver una página XML que contiene todos los productos bajo la raíz del sitio web configurada: [http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full).
