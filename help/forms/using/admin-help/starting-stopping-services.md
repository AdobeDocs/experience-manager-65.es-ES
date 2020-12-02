---
title: Inicio y parada de servicios
seo-title: Inicio y parada de servicios
description: Obtenga información sobre cómo inicio y parada de servicios asociados con módulos de AEM Forms y el servidor de aplicaciones y la base de datos.
seo-description: Obtenga información sobre cómo inicio y parada de servicios asociados con módulos de AEM Forms y el servidor de aplicaciones y la base de datos.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Inicio y parada de servicios {#starting-and-stopping-services}

Existen dos tipos de servicios que forman parte de AEM formularios:

* Servicios que controlan la base de datos y el servidor de aplicaciones de formularios AEM.
* Servicios que controlan módulos de formularios AEM

## Inicio o parada de los servicios asociados con los módulos de formularios AEM {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM módulos de formularios (por ejemplo, Forms, Rights Management, Output) funcionan como servicios. A veces, es posible que necesite detener o inicio los servicios para estos módulos de formularios AEM. Por ejemplo, debe detener y, a continuación, reiniciar un servicio de formularios AEM después de cambiar una configuración para el servicio.

1. En la consola de administración, haga clic en **Servicios** > **Aplicaciones y servicios** > **Administración de servicios**.
1. En la página Administración de servicios, active la casilla de verificación situada junto al servicio para detener o inicio y haga clic en Detener o Inicio.

## Servicios de inicio o parada para el servidor de aplicaciones y la base de datos {#start-or-stop-services-for-the-application-server-and-database}

Una implementación completa de AEM formularios incluye un servidor de aplicaciones y servicios de base de datos:

* *`[application server]`* para formularios AEM
* *`[database]`* para formularios AEM

En Windows, se puede acceder a estos servicios a través del **panel Herramientas administrativas** > **Servicios**. Por ejemplo, si ha instalado AEM formularios en JBoss mediante el método llave en mano, el sistema dispone de los siguientes servicios:

* Formularios de JBoss para Adobe Experience Manager
* Formularios de MySQL para Adobe Experience Manager

Para inicio o detener estos servicios, selecciónelos en la lista del panel Servicios y haga clic en el botón de acción correspondiente del panel.

En UNIX® o Linux, escriba el siguiente texto desde una línea de comandos, donde *`[service name]`* es el nombre del servicio que está verificando:

```java
     ps -A | grep [service name]
```

