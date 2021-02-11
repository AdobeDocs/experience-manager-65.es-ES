---
title: Consola web
seo-title: Consola web
description: Aprenda a utilizar la consola web AEM.
seo-description: Aprenda a utilizar la consola web AEM.
uuid: 7856b2b3-4216-421d-a315-cd9a55936362
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 4a33fddd-0399-40e4-8687-564fb6765b76
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 2%

---


# Consola web{#web-console}

La consola web de AEM se basa en la [consola de administración web Apache Felix](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix es un esfuerzo comunitario para implementar la plataforma de servicio OSGi R4, que incluye el marco de trabajo OSGi y los servicios estándar.

>[!NOTE]
>
>En la consola web, cualquier descripción que mencione la configuración predeterminada se relaciona con los valores predeterminados de Sling.
>
>AEM tiene sus propios valores predeterminados, por lo que los valores predeterminados establecidos pueden diferir de los documentados en la consola.

La consola web oferta una selección de fichas para mantener los paquetes OSGi, que incluyen:

* [Configuración](#configuration): se utiliza para configurar los paquetes OSGi y, por lo tanto, es el mecanismo subyacente para configurar los parámetros AEM sistema
* [Paquetes](#bundles): utilizado para instalar paquetes
* [Componentes](#components): se utiliza para controlar el estado de los componentes necesarios para la AEM

Cualquier cambio realizado se aplica inmediatamente al sistema en ejecución. No es necesario reiniciar.

Se puede acceder a la consola desde `../system/console`; por ejemplo:

`http://localhost:4502/system/console/components`

## Configuración {#configuration}

La ficha **Configuration** se utiliza para configurar los paquetes OSGi y, por lo tanto, es el mecanismo subyacente para configurar AEM parámetros del sistema.

>[!NOTE]
>
>Consulte [Configuración de OSGi con la Consola Web](/help/sites-deploying/configuring-osgi.md) para obtener más detalles.

Se puede acceder a la ficha **Configuración** desde:

* Menú desplegable:

   **los paquetes >**

* La dirección URL; por ejemplo:

   `http://localhost:4502/system/console/configMgr`

Se mostrará una lista de las configuraciones:

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

Existen dos tipos de configuraciones disponibles en las listas desplegables de esta pantalla:

* ****
ConfiguracionesPermite actualizar las configuraciones existentes. Tienen una identidad persistente (PID) y pueden ser:

   * estándar e integral para AEM; son obligatorios, si se eliminan, los valores vuelven a la configuración predeterminada.
   * instancias creadas a partir de configuraciones de fábrica; estas instancias son creadas por el usuario, la eliminación elimina la instancia.

* ****
Configuraciones de fábricaPermite crear una instancia del objeto de funcionalidad requerido.

   Se asignará una identidad persistente y, a continuación, se incluirá en la lista desplegable Configuraciones.

Al seleccionar cualquier entrada de las listas se mostrarán los parámetros relacionados con esa configuración:

![chlimage_1-29](assets/chlimage_1-21a.png)

A continuación, puede actualizar los parámetros según sea necesario y:

* **Guardar**

   Guarde los cambios realizados.

   Para una configuración de fábrica, se creará una nueva instancia con una identidad persistente. La nueva instancia se mostrará en Configuraciones.

* **Restablecer**

   Restablezca los parámetros que se muestran en pantalla a los guardados en último lugar.

* **Eliminar**

   Elimine la configuración actual. Si es estándar, los parámetros se devuelven a la configuración predeterminada. Si se crea a partir de una configuración de fábrica, se elimina la instancia específica.

* **Desenlazar**

   Desenlazar la configuración actual del paquete.

* **Cancelar**

   Cancelar los cambios actuales.

## Paquetes {#bundles}

La ficha **Bundles** es el mecanismo para instalar los paquetes OSGi necesarios para AEM. Se puede acceder a la ficha mediante cualquiera de los siguientes métodos:

* Menú desplegable:

   **los paquetes >**

* La dirección URL; por ejemplo:

   `http://localhost:4502/system/console/bundles`

Se mostrará una lista de paquetes:

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

Con esta ficha puede:

* **Instalar o actualizar**

   Puede **Examinar** para encontrar el archivo que contiene el paquete y especificar si debe **Inicio** inmediatamente y en qué **nivel de Inicio**.

* **Volver a cargar**

   Actualiza la lista mostrada.

* **Actualizar paquetes**

   Esto comprobará las referencias de todos los paquetes y se actualizará según sea necesario.

   Por ejemplo, después de una actualización, es posible que tanto la versión antigua como la nueva sigan ejecutándose debido a referencias anteriores. Esta opción comprueba y mueve todas las referencias a la nueva versión, permitiendo que se detenga la versión anterior.

* **Inicial**

   Inicio un paquete según el nivel de inicio especificado.

* **Detener**

   Detiene el paquete.

* **Desinstalar**

   Desinstala el paquete del sistema.

* **ver el estado**

   La lista especifica el estado actual del paquete; hacer clic en el nombre de un paquete específico con mostrar más información.

>[!NOTE]
>
>Después de **Actualizar** se recomienda realizar un **Actualizar paquetes**.

## Componentes {#components}

La ficha **Componentes** permite activar y/o desactivar los distintos componentes. Se puede acceder a ella desde:

* Menú desplegable:

   **Principal >**

* La dirección URL; por ejemplo:

   `http://localhost:4502/system/console/components`

Se mostrará una lista de los componentes. Hay varios iconos disponibles para permitirle habilitar, deshabilitar o (cuando corresponda) abrir detalles de configuración para un componente específico.

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

Al hacer clic en el nombre de un componente en particular se mostrará más información sobre su estado. Aquí también puede habilitar, deshabilitar o volver a cargar el componente.

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>Habilitar o deshabilitar un componente solo se aplicará hasta que se reinicie AEM/CRX.
>
>El estado de inicio se define dentro del descriptor de componente, que se genera durante el desarrollo y se almacena en el paquete en el momento de la creación del paquete.

