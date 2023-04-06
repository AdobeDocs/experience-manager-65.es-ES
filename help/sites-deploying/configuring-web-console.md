---
title: Consola web en AEM
description: Aprenda a utilizar la consola web en AEM.
uuid: 047274ff-4d7d-4c7d-95be-06f363beae2e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: f934eb02-1f84-44f2-9f14-3f17250c9a90
exl-id: bdfeaf85-e832-40c1-8769-7d027cdb021e
source-git-commit: a17b25e55a0bf16a0df42a7ba4768503618a19e2
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---

# Consola web{#web-console}

La consola web de AEM (Adobe Experience Manager) se basa en la variable [Consola de administración web Apache Felix](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix es un esfuerzo comunitario para implementar la plataforma de servicio OSGi R4, que incluye el marco de OSGi y los servicios estándar.

>[!NOTE]
>
>En la consola web, cualquier descripción que mencione la configuración predeterminada está relacionada con los valores predeterminados de Sling.
>
>AEM tiene sus propios valores predeterminados, por lo que los valores predeterminados establecidos pueden diferir de los documentados en la consola.

La consola web ofrece una selección de pestañas para mantener los paquetes OSGi, que incluyen:

* [Configuración](#configuration): se utiliza para configurar los paquetes OSGi y, por lo tanto, es el mecanismo subyacente para configurar AEM parámetros del sistema
* [Paquetes](#bundles): se utiliza para instalar paquetes
* [Componentes](#components): se utiliza para controlar el estado de los componentes necesarios para AEM

Cualquier cambio realizado se aplica inmediatamente al sistema en ejecución. No es necesario reiniciar.

Se puede acceder a la consola desde `../system/console`; por ejemplo:

`http://localhost:4502/system/console/components`

## Configuración {#configuration}

La variable **Configuración** se utiliza para configurar los paquetes OSGi y, por lo tanto, es el mecanismo subyacente para configurar AEM parámetros del sistema.

>[!NOTE]
>
>Consulte [Configuración de OSGi con la consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) para obtener más información.

La variable **Configuración** se puede acceder a través de:

* El menú desplegable:

   **OSGi >**

* La URL; por ejemplo:

   `http://localhost:4502/system/console/configMgr`

Se mostrará una lista de configuraciones:

![screen_shot_2012-02-15at52308pm-1](assets/screen_shot_2012-02-15at52308pm-1.png)

Hay dos tipos de configuraciones disponibles en las listas desplegables de esta pantalla:

* **Configuraciones**

   Permite actualizar las configuraciones existentes. Tienen una identidad persistente (PID) y pueden ser:

   * estándar e integral para AEM; son obligatorios, si se eliminan, los valores vuelven a la configuración predeterminada.
   * instancias creadas a partir de Configuraciones de fábrica; el usuario crea estas instancias, la eliminación elimina la instancia.

* **Configuraciones de fábrica**

   Permite crear una instancia del objeto de funcionalidad requerido.

   Se le asignará una identidad persistente y, a continuación, se incluirá en la lista desplegable Configuraciones .

Al seleccionar cualquier entrada de las listas, se mostrarán los parámetros relacionados con esa configuración:

![climage_1-61](assets/chlimage_1-61.png)

A continuación, puede actualizar los parámetros según sea necesario y:

* **Guardar**

   Guarde los cambios realizados.

   Para una configuración de fábrica, se creará una nueva instancia con una identidad persistente. La nueva instancia aparece luego en Configuraciones.

* **Restablecer**

   Restablezca los parámetros mostrados en pantalla a los guardados en último lugar.

* **Eliminar**

   Elimine la configuración actual. Si es estándar, los parámetros se devuelven a la configuración predeterminada. Si se crea a partir de una configuración de fábrica, se elimina la instancia específica.

* **Desenlazar**

   Desvincule la configuración actual del paquete.

* **Cancelar**

   Cancelar cualquier cambio actual.

## Paquetes {#bundles}

La variable **Paquetes** es el mecanismo para instalar los paquetes OSGi necesarios para AEM. Se puede acceder a la pestaña mediante cualquiera de los métodos siguientes:

* El menú desplegable:

   **OSGi >**

* La URL; por ejemplo:

   `http://localhost:4502/system/console/bundles`

Se mostrará una lista de paquetes:

![screen_shot_2012-02-15at44740pm-1](assets/screen_shot_2012-02-15at44740pm-1.png)

Con esta ficha puede:

* **Instalar o actualizar**

   Puede **Examinar** para buscar el archivo que contiene el paquete y especificar si debe **Inicio** inmediatamente y **Nivel de inicio**.

* **Volver a cargar**

   Actualiza la lista mostrada.

* **Actualizar paquetes**

   Esto comprobará las referencias de todos los paquetes y se actualizará según sea necesario.

   Por ejemplo, después de una actualización, la versión antigua y la nueva pueden seguir ejecutándose debido a referencias anteriores. Esta opción comprobará y moverá todas las referencias a la nueva versión, permitiendo que se detenga la versión antigua.

* **Inicial**

   Inicia un paquete según el nivel de inicio especificado.

* **Detener**

   Detiene el paquete.

* **Desinstalar**

   Desinstala el paquete del sistema.

* **ver el estado**

   La lista especifica el estado actual del paquete; al hacer clic en el nombre de un paquete específico con mostrar más información.

>[!NOTE]
>
>Después **Actualizar** se recomienda realizar un **Actualizar paquetes**.

## Componentes {#components}

La variable **Componentes** le permite activar o desactivar los distintos componentes. Puede acceder a ella desde:

* El menú desplegable:

   **Principal >**

* La URL; por ejemplo:

   `http://localhost:4502/system/console/components`

Se mostrará una lista de componentes. Hay varios iconos disponibles para permitirle habilitar, deshabilitar o (cuando corresponda) abrir detalles de configuración de un componente específico.

![screen_shot_2012-02-15at52144pm-1](assets/screen_shot_2012-02-15at52144pm-1.png)

Al hacer clic en el nombre de un componente en particular, se mostrará más información sobre su estado. Aquí también puede habilitar, deshabilitar o volver a cargar el componente.

![imagen_1-62](assets/chlimage_1-62.png)

>[!NOTE]
>
>Habilitar o deshabilitar un componente solo se aplicará hasta que se reinicie AEM/CRX.
>
>El estado de inicio se define dentro del descriptor de componente, que se genera durante el desarrollo y se almacena en el paquete en el momento de la creación del paquete.
