---
title: Integración con ExactTarget
seo-title: Integración con ExactTarget
description: Descubra cómo integrar AEM con ExactTarget.
seo-description: Descubra cómo integrar AEM con ExactTarget.
uuid: a53bbdaa-98f7-4035-b842-aa7ea63712ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5b2f624d-e5b8-4484-a773-7784ebce58bd
docset: aem65
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# Integración con ExactTarget{#integrating-with-exacttarget}

La integración de AEM con Exact Destinatario le permite administrar y enviar correos electrónicos creados en AEM mediante Exact Destinatario. También le permite utilizar las funciones de administración de posibles clientes de Exact Destinatario a través de formularios AEM en páginas AEM.

La integración proporciona las siguientes funciones:

* La capacidad de crear correos electrónicos en AEM y publicarlos en Exact Destinatario para su distribución.
* La capacidad de definir la acción de un formulario AEM para crear un suscriptor de Exact Destinatario.

Una vez configurado ExactTarget, puede publicar newsletters o correos electrónicos en ExactTarget. Consulte [Publicación de newsletters en un servicio de correo electrónico](/help/sites-authoring/personalization.md).

## Creación de una configuración de ExactTarget {#creating-an-exacttarget-configuration}

Las configuraciones de ExactTarget se pueden agregar mediante Cloudservices o Herramientas. Ambos métodos se describen en esta sección.

### Configuración de ExactTarget mediante Cloudservices {#configuring-exacttarget-via-cloudservices}

Para crear una configuración de ExactTarget en Cloud Services:

1. En la página de bienvenida, haga clic en **Cloud Services**. (O acceso directo a `https://<hostname>:<port>/etc/cloudservices.html`).
1. Haga clic en **ExactTarget** y luego **Configurar**. Se abre la ventana de configuración de ExactTarget.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Escriba un título y, opcionalmente, un nombre y haga clic en **Crear**. Se abre la ventana de configuración **ExactTarget Settings**.

   ![chlimage_1](assets/chlimage_1.jpeg)

1. Introduzca el nombre de usuario, la contraseña y seleccione un punto final de API (por ejemplo, **https://webservice.exacttarget.com/Service.asmx**).
1. Haga clic en **Conectar con ExactTarget.** Cuando se ha conectado correctamente, se muestra un cuadro de diálogo de éxito. Haga clic en **Aceptar** para salir de la ventana.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Seleccione una cuenta, si está disponible. La cuenta es para clientes de Enterprise 2.0. Haga clic en **Aceptar**.

   ExactTarget se ha configurado. Puede editar la configuración haciendo clic en **Editar**. Puede ir a ExactTarget haciendo clic en **Ir a ExactTarget**.

1. AEM ahora proporciona una función de extensión de datos. Puede importar columnas de extensión de datos de ExactTarget. Esto se puede configurar haciendo clic en el signo &quot;+&quot; que aparece además de crear correctamente la configuración de ExactTarget. Se puede seleccionar cualquiera de las extensiones de datos existentes en la lista desplegable. Para obtener más información sobre cómo configurar las extensiones de datos, consulte la [documentación de ExactTarget](https://help.exacttarget.com/en/documentation/exacttarget/subscribers/data_extensions_and_data_relationships).

   Las columnas de extensión de datos importadas se pueden utilizar posteriormente mediante el componente **Texto y personalización**.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### Configuración de ExactTarget mediante Herramientas {#configuring-exacttarget-via-tools}

Para crear una configuración de ExactTarget en Herramientas:

1. En la página de bienvenida, haga clic en **Herramientas**. O navegue hasta allí directamente yendo a `https://<hostname>:<port>/misadmin#/etc`.
1. Seleccione **Herramientas**, luego **Configuraciones de Cloud Services,** y luego **ExactTarget**.
1. Haga clic en **Nuevo** para abrir la ventana **Crear página **ventana.

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. Introduzca el **Título** y, opcionalmente, el **Nombre** y haga clic en **Crear**.
1. Introduzca la información de configuración como se indica en el paso 4 del procedimiento anterior. Siga ese procedimiento para finalizar la configuración de ExactTarget.

### Añadir varias configuraciones {#adding-multiple-configurations}

Para agregar varias configuraciones:

1. En la página de bienvenida, haga clic en **Cloud Services** y haga clic en **ExactTarget**. Haga clic en el botón **Mostrar configuraciones** que aparece si hay una o más configuraciones de ExactTarget disponibles. Se enumeran todas las configuraciones disponibles.
1. Haga clic en el signo **+** junto a Configuraciones disponibles. Se abre la ventana **Crear configuraciones**. Siga el procedimiento de configuración anterior para crear una nueva configuración.