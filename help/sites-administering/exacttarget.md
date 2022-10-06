---
title: Integración con ExactTarget
seo-title: Integrating with ExactTarget
description: Aprenda a integrar AEM con ExactTarget.
seo-description: Learn how to integrate AEM with ExactTarget.
uuid: a53bbdaa-98f7-4035-b842-aa7ea63712ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5b2f624d-e5b8-4484-a773-7784ebce58bd
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Integración con ExactTarget{#integrating-with-exacttarget}

Al integrar AEM con ExactTarget, puede administrar y enviar correos electrónicos creados en AEM mediante ExactTarget. También le permite utilizar las funciones de administración de posibles clientes de ExactTarget a través de AEM formularios en AEM páginas.

La integración le ofrece las siguientes funciones:

* La capacidad de crear correos electrónicos en AEM y publicarlos en ExactTarget para su distribución.
* La capacidad de configurar la acción de un formulario AEM para crear un suscriptor de ExactTarget.

Una vez configurado ExactTarget, puede publicar newsletters o correos electrónicos en ExactTarget. Consulte [Publicación de newsletters en un servicio de correo electrónico](/help/sites-authoring/personalization.md).

## Creación de una configuración de ExactTarget {#creating-an-exacttarget-configuration}

Las configuraciones de ExactTarget se pueden agregar mediante Cloud Services o Herramientas. Ambos métodos se describen en esta sección.

### Configuración de ExactTarget mediante Cloudservices {#configuring-exacttarget-via-cloudservices}

Para crear una configuración de ExactTarget en Cloud Services:

1. En la página de bienvenida, haga clic en **Cloud Services**. (O acceder directamente a `https://<hostname>:<port>/etc/cloudservices.html`.)
1. Haga clic en **ExactTarget** y luego **Configurar**. Se abre la ventana de configuración ExactTarget.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Introduzca un título y, opcionalmente, un nombre y haga clic en **Crear**. La variable **Configuración de ExactTarget** se abre la ventana de configuración.

   ![imagen_1](assets/chlimage_1.jpeg)

1. Introduzca el nombre de usuario, la contraseña y seleccione un punto final de API (por ejemplo, **https://webservice.exacttarget.com/Service.asmx**).
1. Haga clic en **Conéctese a ExactTarget.** Cuando se haya conectado correctamente, verá un cuadro de diálogo de éxito. Haga clic en **OK** para salir de la ventana.

   ![Chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Seleccione una cuenta, si está disponible. La cuenta es para clientes de Enterprise 2.0. Haga clic en **Aceptar**.

   ExactTarget se ha configurado. Puede editar la configuración haciendo clic en **Editar**. Puede ir a ExactTarget haciendo clic en **Vaya a ExactTarget**.

1. AEM ahora proporciona una función de extensión de datos. Puede importar columnas de extensión de datos de ExactTarget. Esto se puede configurar haciendo clic en el signo &quot;+&quot; que aparece además de la configuración de ExactTarget creada correctamente. Se puede seleccionar cualquiera de las extensiones de datos existentes en la lista desplegable. Para obtener más información sobre cómo configurar extensiones de datos, consulte [Documentación de ExactTarget](https://help.exacttarget.com/en/documentation/exacttarget/subscribers/data_extensions_and_data_relationships).

   Las columnas de extensión de datos importadas se pueden usar posteriormente a través de la variable **Texto y personalización** componente.

   ![Chlimage_1-2](assets/chlimage_1-2.jpeg)

### Configuración de ExactTarget mediante Herramientas {#configuring-exacttarget-via-tools}

Para crear una configuración de ExactTarget en Herramientas:

1. En la página de bienvenida, haga clic en **Herramientas**. O navegue hasta allí directamente yendo a `https://<hostname>:<port>/misadmin#/etc`.
1. Select **Herramientas**, luego **Configuraciones de Cloud Services,** then **ExactTarget**.
1. Haga clic en **Nuevo** para abrir la ventana **Crear página **.

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. Introduzca la variable **Título** y, opcionalmente, la variable **Nombre** y haga clic en **Crear**.
1. Introduzca la información de configuración tal como se indica en el paso 4 del procedimiento anterior. Siga ese procedimiento para finalizar la configuración de ExactTarget.

### Adición de varias configuraciones {#adding-multiple-configurations}

Para agregar varias configuraciones:

1. En la página de bienvenida, haga clic en **Cloud Services** y haga clic en **ExactTarget**. Haga clic en **Mostrar configuraciones** que aparece si hay una o más configuraciones de ExactTarget disponibles. Se enumeran todas las configuraciones disponibles.
1. Haga clic en el **+** junto a Configuraciones disponibles. Esto abre el **Crear configuraciones** ventana. Siga el procedimiento de configuración anterior para crear una configuración nueva.
