---
title: Iniciar y detener servicios
description: Obtenga información sobre cómo iniciar y detener servicios asociados a módulos de AEM Forms y al servidor de aplicaciones y la base de datos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 13%

---

# Iniciar y detener servicios {#starting-and-stopping-services}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

AEM Existen dos tipos de servicios que forman parte de los formularios de:

* AEM Servicios que controlan el servidor de aplicaciones y la base de datos de formularios de la.
* AEM Servicios que controlan los módulos de formularios de

## AEM Iniciar o detener los servicios asociados con módulos de formularios de la {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM Los módulos de formularios de datos (por ejemplo, Forms, Rights Management, Output) funcionan como servicios. AEM A veces, es posible que tenga que detener o iniciar los servicios para estos módulos de formularios de la forma en la que se utilizan los formularios de la. AEM Por ejemplo, debe detener y reiniciar un servicio de formularios de la después de cambiar una configuración del servicio.

>[!NOTE]
>
> Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

1. En la consola de administración, haga clic en **Servicios** > **Aplicaciones y servicios** > **Administración de servicios**.
1. En la página Administración de servicios, active la casilla de verificación situada junto al servicio que desea detener o iniciar y haga clic en Detener o Iniciar.

## Iniciar o detener servicios para el servidor de aplicaciones y la base de datos {#start-or-stop-services-for-the-application-server-and-database}

AEM Una implementación completa de los formularios de incluye un servidor de aplicaciones y servicios de base de datos:

* AEM *`[application server]`* para formularios de
* AEM *`[database]`* para formularios de

En Windows, se puede acceder a estos servicios a través de **Herramientas administrativas** > **Panel de servicios**. AEM Por ejemplo, si ha instalado formularios en JBoss mediante el método llave en mano, los siguientes servicios están disponibles en el sistema:

* JBoss para formularios Adobe Experience Manager
* MySQL para formularios Adobe Experience Manager

Inicie o detenga estos servicios seleccionándolos en la lista del panel Servicios y, a continuación, haciendo clic en el botón de acción correspondiente del panel.

En UNIX® o Linux, introduzca el siguiente texto desde una línea de comandos, donde *`[service name]`* es el nombre del servicio que está verificando:

```java
     ps -A | grep [service name]
```
