---
title: Integración con ExactTarget
description: Aprenda a integrar Adobe Experience Manager con ExactTarget.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# Integración con ExactTarget{#integrating-with-exacttarget}

Al integrar Adobe Experience Manager AEM AEM () con Exact Target, puede administrar y enviar los correos electrónicos creados en a través de Exact Target. En el caso de los mensajes de correo electrónico, se puede acceder a los mensajes de correo electrónico creados a través de Exact Target. AEM AEM También le permite utilizar las funciones de administración de posibles clientes de Exact Target mediante formularios en forma de.

La integración ofrece las siguientes funciones:

* AEM La capacidad de crear correos electrónicos en las listas de distribución y publicarlos en Exact Target para su distribución.
* AEM La capacidad de establecer la acción de un formulario de para crear un suscriptor de Target exacto.

Una vez configurado ExactTarget, puede publicar boletines informativos o correos electrónicos en ExactTarget. Ver [Publicar boletines en un servicio de correo electrónico](/help/sites-authoring/personalization.md).

## Creación de una configuración de ExactTarget {#creating-an-exacttarget-configuration}

Las configuraciones de ExactTarget se pueden agregar mediante Cloud Services o Herramientas. Ambos métodos se describen en esta sección.

### Configuración de ExactTarget mediante Cloud Services {#configuring-exacttarget-via-cloudservices}

Para crear una configuración de ExactTarget en Cloud Service:

1. En la página de bienvenida, haga clic en **Cloud Service**. (O acceda directamente a en `https://<hostname>:<port>/etc/cloudservices.html`.)
1. Haga clic en **ExactTarget** y luego en **Configurar**. Se abre la ventana de configuración de ExactTarget.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Escriba un título y, opcionalmente, un nombre y haga clic en **Crear**. Se abre la ventana de configuración **Configuración de ExactTarget**.

   ![chlimage_1](assets/chlimage_1.jpeg)

1. Escriba el nombre de usuario y la contraseña, y seleccione un extremo de API (por ejemplo, **https://webservice.exacttarget.com/Service.asmx**).
1. Haga clic en **Conectar con ExactTarget.** Cuando se haya conectado correctamente, verá un cuadro de diálogo de éxito. cuadro Haga clic en **Aceptar** para salir de la ventana.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Seleccione una cuenta, si está disponible. La cuenta es para clientes de Enterprise 2.0. Haga clic en **OK**.

   Se ha configurado ExactTarget. Puede editar la configuración haciendo clic en **Editar**. Para ir a ExactTarget, haga clic en **Ir a ExactTarget**.

1. AEM ahora proporciona una función de extensión de datos de. Puede importar columnas de extensión de datos de ExactTarget. Se puede configurar haciendo clic en el signo &quot;+&quot; que aparece además de la configuración de ExactTarget creada correctamente. Cualquiera de las extensiones de datos existentes se puede seleccionar en la lista desplegable. Para obtener más información sobre cómo configurar extensiones de datos, consulte [Documentación de ExactTarget](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_relationships_classic.htm&amp;type=5).

   Las columnas de extensión de datos importadas se pueden usar posteriormente mediante el componente **Texto y Personalization**.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### Configuración de ExactTarget mediante Herramientas {#configuring-exacttarget-via-tools}

Para crear una configuración de ExactTarget en Herramientas:

1. En la página de bienvenida, haga clic en **Herramientas**. O bien, vaya directamente a `https://<hostname>:<port>/misadmin#/etc`.
1. Seleccione **Herramientas**, luego **Configuraciones de Cloud Service** y después **ExactTarget**.
1. Haga clic en **Nuevo** para abrir la ventana **Crear página &#x200B;**.

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. Escriba **Title** y, opcionalmente, **Name**, y haga clic en **Crear**.
1. Introduzca la información de configuración como se describe en el paso 4 del procedimiento anterior. Siga ese procedimiento para finalizar la configuración de ExactTarget.

### Añadir varias configuraciones {#adding-multiple-configurations}

Para agregar varias configuraciones:

1. En la página de bienvenida, haga clic en **Cloud Service** y luego en **ExactTarget**. Haga clic en **Mostrar configuraciones** que aparece si hay una o más configuraciones de ExactTarget disponibles. Se muestran todas las configuraciones disponibles.
1. Haga clic en el signo **+** junto a Configuraciones disponibles. Esto abre la ventana **Crear configuraciones**. Siga el procedimiento de configuración anterior para crear una configuración.
