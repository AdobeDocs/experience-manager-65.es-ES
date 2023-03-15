---
title: Iniciar y detener servicios
seo-title: Starting and stopping services
description: Obtenga información sobre cómo iniciar y detener servicios asociados a módulos de AEM Forms y al servidor de aplicaciones y la base de datos.
seo-description: Learn how to start and stop services associated with AEM Forms modules and the application server and database.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# Iniciar y detener servicios {#starting-and-stopping-services}

AEM Existen dos tipos de servicios que forman parte de los formularios de:

* AEM Servicios que controlan el servidor de aplicaciones y la base de datos de formularios de la.
* AEM Servicios que controlan los módulos de formularios de

## AEM Iniciar o detener los servicios asociados con módulos de formularios de la {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM Los módulos de formularios de datos (por ejemplo, Forms, Rights Management, Output) funcionan como servicios. AEM A veces, es posible que tenga que detener o iniciar los servicios para estos módulos de formularios de la forma en la que se utilizan los formularios de la. AEM Por ejemplo, debe detener y, a continuación, reiniciar un servicio de formularios de la después de cambiar una configuración del servicio.

1. En la consola de administración, haga clic en **Servicios** > **Aplicaciones y servicios** > **Administración de servicios**.
1. En la página Administración de servicios, active la casilla de verificación situada junto al servicio que desea detener o iniciar y haga clic en Detener o Iniciar.

## Iniciar o detener servicios para el servidor de aplicaciones y la base de datos {#start-or-stop-services-for-the-application-server-and-database}

AEM Una implementación completa de los formularios de incluye un servidor de aplicaciones y servicios de base de datos:

* *`[application server]`* AEM para los formularios
* *`[database]`* AEM para los formularios

En Windows, se puede acceder a estos servicios a través del **Herramientas administrativas** > **Panel Servicios**. AEM Por ejemplo, si ha instalado formularios en JBoss mediante el método llave en mano, los siguientes servicios están disponibles en el sistema:

* JBoss para formularios Adobe Experience Manager
* MySQL para formularios Adobe Experience Manager

Inicie o detenga estos servicios seleccionándolos en la lista del panel Servicios y, a continuación, haciendo clic en el botón de acción correspondiente del panel.

En UNIX® o Linux, introduzca el siguiente texto desde una línea de comandos, donde *`[service name]`* es el nombre del servicio que está verificando:

```java
     ps -A | grep [service name]
```
