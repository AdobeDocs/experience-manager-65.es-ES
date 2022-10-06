---
title: Inclusión en Adobe Analytics y Adobe Target
seo-title: Opting Into Adobe Analytics and Adobe Target
description: Obtenga información sobre cómo participar en Adobe Analytics y Adobe Target.
seo-description: Learn how to opt into Adobe Analytics and Adobe Target.
uuid: 9090a0f3-d373-4826-aa68-6aa82c0fbfbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: de466511-d82f-4ddb-8f6a-7ca9240fdeab
exl-id: 3603e929-2aa1-4c25-ad9a-b10ff52a59f4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 10%

---

# Inclusión en Adobe Analytics y Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

AEM tiene un procedimiento de inclusión que le ayuda a integrarse con Adobe Analytics y Adobe Target. Esta opción está disponible de forma predeterminada, como una tarea precargada asignada al grupo de usuarios administradores.

Cuando inicia sesión como administrador, esta tarea (**Configuración de Analytics y Targeting**) está disponible en el [Bandeja de entrada](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks). En función de las credenciales que proporcione, le ayuda a configurar e integrar estos servicios.

Tiene las siguientes opciones para configurar la integración:

* Configure la integración mediante la tarea.

   Esto se puede hacer inmediatamente o más tarde, la tarea permanecerá en la Bandeja de entrada hasta que se realice alguna acción. En cualquier caso, la configuración se puede realizar directamente en la interfaz de usuario o con el uso de un `.properties` archivo.

* Desactivar la integración.

   Tenga en cuenta esta opción si prefiere [configurar manualmente la integración](/help/sites-administering/marketing-cloud.md). Consulte también [Integración de AEM con Adobe Target y Adobe Analytics mediante DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

* Configure la configuración y el aprovisionamiento mediante una secuencia de comandos.

## Configuración de la integración {#configuring-the-integration}

Participe en la integración con:

* Analytics para permitir el uso de sus capacidades de seguimiento y análisis de página.
* Target para habilitar el uso de sus capacidades de personalización.

Para cualquiera de estas opciones, debe proporcionar la información de la cuenta de usuario y especificar las páginas de las que se realiza un seguimiento.

>[!NOTE]
>
>Si lo desea, puede proporcionar información de la cuenta de Analytics y Target mediante un archivo de propiedades que se lee al iniciar el servidor. Consulte [Proporcionar información de la cuenta mediante un archivo de propiedades](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file).

Al optar por la integración, AEM realiza las siguientes tareas:

* Crea las configuraciones de nube que habilitan la conexión con Analytics y Target.
* Crea los marcos que determinan los datos de los que se realiza un seguimiento.
* Configura las páginas web para utilizar estos servicios.

>[!NOTE]
>
>AT.js es la biblioteca de cliente predeterminada. Esto se configura en la sección [configuración de target cloud services](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration).
>
>Adobe recomienda usar AT.js como biblioteca de cliente.

Para incluirse en la tarea precargada y lista para usar:

1. Desde su [Bandeja de entrada, seleccione y **Apertura** Configurar Analytics y Targeting](/help/sites-authoring/inbox.md#taking-action-on-an-item) tarea.

   ![optin-01](assets/optin-01.png)

1. Para Analytics:

   1. Introduzca la información de la cuenta de usuario de Analytics y, a continuación, haga clic en la **Agregar** botón.
   1. Se autentican las credenciales adecuadas.
   1. Cuando la cuenta de Analytics esté autenticada, seleccione el grupo de informes de Analytics que desea utilizar. AEM recupera esos grupos de informes de Analytics. El estado se actualiza a **Se ha añadido**.

1. Para Target:

   1. Introduzca la información de la cuenta de usuario de Target y haga clic en el **Agregar** botón.
   1. Se autentican las credenciales adecuadas. El estado se actualiza a **Se ha añadido**.

1. Seleccione **Siguiente**.
1. Seleccione los sitios para los que deben usarse Analytics o Target.

1. Select **Listo** para completar.

   >[!CAUTION]
   >
   >Después de incluirse en la configuración, debe publicar el sitio o páginas afectadas para replicar estos cambios en la instancia de publicación.

## Exclusión de la integración {#opting-out-of-the-integration}

Desactivar la integración con Analytics y Target cuando:

* No desea integrarse con estos productos.
* Prefiera configurar las integraciones manualmente.

   Para obtener información sobre la configuración manual de las integraciones, consulte [Integración con Adobe Analytics](/help/sites-administering/adobeanalytics.md) y [Integración con Adobe Target](/help/sites-administering/target.md).

Para desactivar , debe completar la tarea precargada:

* Desde su [Bandeja de entrada, seleccione y **Completar** Configurar Analytics y Targeting](/help/sites-authoring/inbox.md#taking-action-on-an-item) tarea.

## Proporcionar información de la cuenta mediante un archivo de propiedades {#providing-account-information-using-a-properties-file}

Instale un archivo de propiedades que AEM lea al iniciar el servidor para configurar las propiedades de la cuenta para la integración con Analytics y Target. Al utilizar el archivo de propiedades, el asistente de inclusión utiliza automáticamente las propiedades del archivo y la configuración de nube se crea en consecuencia.

El archivo de propiedades es un archivo de texto llamado marketingcloud.properties que se guarda en el directorio de trabajo que está utilizando el proceso de AEM (normalmente el mismo directorio que el archivo JAR). El archivo incluye las siguientes propiedades:

* analytics.server: La dirección URL del centro de datos de Analytics que utilice.
* analytics.company: Empresa asociada a su cuenta de usuario de Analytics.
* analytics.username: Su nombre de usuario de Analytics.
* analytics.secret: El secreto asociado al nombre de usuario de Analytics.
* analytics.reportsuite: Nombre del grupo de informes de Analytics que se va a usar.
* target.clientcode: El código de cliente asociado a su cuenta de Target.
* target.email: La dirección de correo electrónico que utiliza para autenticar su cuenta de Target.
* target.password: La contraseña asociada a su dirección de correo electrónico.

Las propiedades y los valores se separan con signos iguales (=). A las propiedades de Analytics se les agregará el prefijo `analytics`, y las propiedades de Target tienen el prefijo `target`. Para configurar un servicio, proporcione valores para todas las propiedades de ese servicio. Si no desea configurar un servicio, no proporcione valores para ese servicio.

El siguiente ejemplo `.properties` incluye los valores de propiedad para crear una configuración de nube para Analytics:

```xml
analytics.server=https://test.omniture.com/login/
analytics.company=MyCompany
analytics.username=sbroders
analytics.secret=12345678
analytics.reportsuite=myreportsuite
target.clientcode=
target.email=
target.password=
```

El siguiente procedimiento describe cómo participar en la integración mediante el archivo de propiedades.

1. Cree la variable `marketingcloud.properties` en el directorio de trabajo que utiliza el proceso de AEM (instancia de autor).

   >[!NOTE]
   >
   >El directorio de trabajo suele ser el directorio que contiene el jar o `license.properties` archivo.
   >
   >Sin embargo, también se puede definir como una ruta absoluta mediante la propiedad del sistema:
   >
   >`mac.provisioning.file.container`

1. Agregue los valores de propiedad según sus cuentas de Analytics o Target.
1. Inicie o reinicie el servidor y, a continuación, inicie sesión con una cuenta de administrador.
1. Abra la tarea Configurar Analytics y Targeting como se describe en [Configuración de la integración](/help/sites-administering/opt-in.md#configuring-the-integration). En lugar de solicitar la información de la cuenta, el asistente utiliza los valores de la variable `.properties` archivo.

   Select **Agregar** para obtener el servicio adecuado, continúe con el asistente.

   ![optin-02](assets/optin-02.png)

## Acerca de las configuraciones de Cloud {#about-the-cloud-configurations}

Al configurar la integración con Analytics y Target, AEM crea automáticamente las configuraciones y los marcos de nube necesarios. Por ejemplo, la configuración de nube de Analytics se denomina Cuenta de Analytics aprovisionada.

No es necesario modificar las configuraciones de nube. Sin embargo, puede configurar los marcos según sea necesario. (Consulte [Asignación de datos de componente con propiedades de Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md) y [Agregar un marco de destino](/help/sites-administering/target.md).)

>[!NOTE]
>
>De forma predeterminada, al entrar en el asistente de configuración de Adobe Target, el direccionamiento preciso está habilitado.
>
>El direccionamiento preciso significa que la configuración del servicio en la nube espera a que el contexto se cargue antes de cargar el contenido. Como resultado, en términos de rendimiento, un direccionamiento preciso puede provocar un retraso de unos milisegundos antes de cargar el contenido.
>
>El direccionamiento preciso siempre está habilitado en la instancia de autor. Sin embargo, en la instancia de publicación puede optar por desactivar el direccionamiento preciso globalmente, desactivando la marca de verificación junto al direccionamiento preciso en la configuración del servicio en la nube (**http://localhost:4502/etc/cloudservices.html**). También puede activar y desactivar el direccionamiento preciso para componentes individuales independientemente de la configuración del servicio en la nube.
>
>Si ***ya*** ha creado componentes de destino y cambia esta configuración, los cambios no afectan a esos componentes. Debe realizar cualquier cambio en esos componentes directamente.

>[!CAUTION]
>
>Al optar por la configuración de Analytics y por una `reportsuite` está seleccionado, el marco está restringido al modo de ejecución de publicación. Esto significa que el seguimiento solo funciona en la instancia de publicación.
>
>Si se necesita realizar el seguimiento en una instancia de creación, también se debe cambiar el valor a `all`.

## Configuración del programa de instalación y aprovisionamiento mediante script {#configuring-the-setup-and-provisioning-via-script}

Como administrador, es posible que desee configurar y aprovisionar con un script en lugar de pasar manualmente por el asistente. Para ello, haga lo siguiente:

* Envío de una solicitud de POST a **/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json** con los parámetros requeridos.

Los parámetros que envíe dependerán de lo siguiente:

* Si desea usar la variable **marketingcloud.properties** rellenado con todas las credenciales necesarias, debe enviar los siguientes parámetros:

   * `automaticProvisioning`= `true`
   * `servicename`= `analytics|target`
   * `path`=ruta a una página AEM para adjuntar las configuraciones de los servicios en la nube creadas

   Por ejemplo, una solicitud curl que crea configuraciones de Analytics y Target y las adjunta a la página we.retail sería:

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```

* Si no desea usar la variable **marketingcloud.properties** a continuación, deberá enviar las credenciales, así como los parámetros; por ejemplo:

   * automaticProvisioning= `true`
   * servicename= `analytics|target`
   * path=path a una página AEM para adjuntar las configuraciones de servicios en la nube creadas; se pueden definir varias rutas
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`

   En este caso, la solicitud curl que crea las configuraciones de Analytics y Target y las adjunta a la página web-retail sería:

   ```shell
   curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
   ```
