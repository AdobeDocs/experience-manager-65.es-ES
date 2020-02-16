---
title: Alimentación de productos
seo-title: Alimentación de productos
description: Obtenga información sobre la fuente de productos de AEM.
seo-description: Obtenga información sobre la fuente de productos de AEM.
uuid: 99eb9bdc-2717-45d4-9203-6394b7d7ddc6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 1f920892-c52e-42ca-900c-2c7ab3c503b3
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Product Feed {#product-feed}

AEM se integra con [Search&amp;Promote](https://www.adobe.com/solutions/testing-targeting/searchandpromote.html) y le permite:

* utilice la API de comercio electrónico, independientemente de la estructura de repositorio subyacente y la plataforma de comercio.
* aproveche la función Conector de índice de Search&amp;Promote para proporcionar una fuente de producto en formato XML.
* aproveche la función de control remoto de Search&amp;Promote para realizar solicitudes programadas o a petición de la fuente de productos
* generación de fuentes para distintas cuentas de Search&amp;Promote, configuradas como configuraciones de servicios en la nube.

Debe tener una cuenta válida y [configurar la conexión con Search&amp;Promote](/help/sites-administering/search-and-promote.md#configuring-the-connection-to-search-promote). También debe comprobar que está utilizando el centro [de](/help/sites-administering/search-and-promote.md#configuring-the-data-center) datos correcto y asegurarse de que el **URI del servidor remoto **está configurado.

## Configuración de la fuente de productos {#set-up-the-product-feed}

Primero debe introducir una raíz del sitio Web y un atributo de identificador. Para ello:

1. Vaya a la configuración de Search&amp;Promote.
1. Haga clic en **[!UICONTROL Editar]**.
1. Haga clic en la ficha Configuración **[!UICONTROL de fuente del conector]** de índice.
1. Introduzca el atributo raíz **[!UICONTROL e]** identificador del sitio **[!UICONTROL Web]**.

   >[!NOTE]
   >
   >La raíz **[!UICONTROL del sitio]** Web es la raíz del sitio Web de comercio electrónico, por ejemplo `/content/geometrixx-outdoors/en`.
   >
   >El atributo **** Identifier es una propiedad JCR que identifica de forma única al producto: `identifier`.

1. Haga clic en **[!UICONTROL Aceptar]**.

A continuación, también debe editar dos configuraciones en la consola web para poder generar fuentes de productos.

### Configuración de la implementación de CQ Search&amp;Promote Products Crawler para Geometrixx en el día {#configuring-the-day-cq-search-promote-products-crawler-implementation-for-geometrixx}

1. Vaya a [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Haga clic en **[!UICONTROL Día de implementación del buscador de productos CQ Search&amp;Promote para Geometrixx]**.
1. Especifique el número de cuenta de Search&amp;Promote al que está vinculado este explorador. Se utilizará para buscar la configuración de servicios en la nube utilizada por este buscador.
1. Haga clic en **[!UICONTROL Guardar]**.

### Configuración del Generador de fuentes de productos CQ Search&amp;Promote para Geometrixx {#configuring-the-day-cq-search-promote-products-feed-generator-for-geometrixx}

1. Vaya a [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Haga clic en **[!UICONTROL Día Generador de fuentes de productos CQ Search&amp;Promote para Geometrixx]**.
1. Especifique el número de cuenta de Search&amp;Promote al que está vinculado este generador. Se utilizará para buscar la configuración de servicios en la nube utilizada por este generador.
1. Haga clic en **[!UICONTROL Guardar]**.

## Programar la fuente de productos {#schedule-the-product-feed}

Para habilitar la generación de fuentes programadas, debe configurar un programador para ella.
Un programador se configura como una configuración secundaria de la configuración de servicios en la nube de Search&amp;Promote específica.

1. Vaya a la configuración de Search&amp;Promote.
1. Haga clic en **[!UICONTROL +]** junto a la configuración **[!UICONTROL de]** Programador.
1. Introduzca un **[!UICONTROL Título]** reconocible para los autores de páginas y un **[!UICONTROL Nombre]**&#x200B;único.
1. Haga clic en **[!UICONTROL Crear]**. Se abre un cuadro de diálogo.

   ![chlimage_1-108](assets/chlimage_1-108a.png)

1. Introduzca la contraseña **[!UICONTROL de control]** remoto. Es la contraseña que configuró en su cuenta de Search&amp;Pronote.

   >[!NOTE]
   >
   >No es la contraseña de su cuenta de Search&amp;Promote. Puede encontrar y cambiar esta contraseña iniciando sesión en su cuenta de Search&amp;Promote y yendo a **[!UICONTROL Index]** y luego a **[!UICONTROL Remote Control]**.

1. Marque **[!UICONTROL Habilitar programación]** .
1. Seleccione una **[!UICONTROL programación]**. Es el programa de generación de fuentes real.
1. Habilite o no la indexación **[!UICONTROL a]** petición. Esta función se utiliza para llamar manualmente al índice de Search&amp;Promote. Si se selecciona **[!UICONTROL Solicitar fuente]** de productos completa, Search&amp;Promote solicitará una fuente de productos completa. De lo contrario, se solicita una fuente de productos incremental.

   >[!NOTE]
   >
   >La función de indexación a petición utiliza la función de control remoto de Search&amp;Promote. Cuando se llama a una indexación remota, la indexación no se iniciará inmediatamente, pero se publicará una solicitud de indización en Search&amp;Promote mediante la función de control remoto.

1. Haga clic en **[!UICONTROL Aceptar]**.

Ahora que ha configurado todo, puede ver una página XML que contiene todos los productos bajo la raíz del sitio web configurada: [http://localhost:4502/etc/commerce/searchpromote/feed/full](http://localhost:4502/etc/commerce/searchpromote/feed/full).
