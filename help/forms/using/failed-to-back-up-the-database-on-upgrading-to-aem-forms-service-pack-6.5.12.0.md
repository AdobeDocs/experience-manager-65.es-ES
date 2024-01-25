---
title: Error al realizar una copia de seguridad de la base de datos anterior en AEM Forms 6.5.12.0.
description: Cuando un usuario actualiza a Experience Manager 6.5.12.0 y hace clic en "Actualizar MySQL", el administrador de configuración no realiza una copia de seguridad de la base de datos de Experience Manager Forms anterior.
source-git-commit: d232bfdad7b8413eb015f6fe5dd3442cebf1001d
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 7%

---

# Problema (#issue)

Cuando un usuario actualiza a Experience Manager 6.5.12.0 y hace clic en &quot;Actualizar MySQL&quot;, el administrador de configuración no realiza una copia de seguridad de la base de datos de Experience Manager Forms anterior, muestra el error:

`Failed to backup the previous Adobe Experience Manager Forms Database`


## Aplicable a {#applies-to}

* Experience Manager 6.5 Forms

## Solución {#solution}

Para resolver el problema, aumente el max_packet_size de la base de datos a 100 M o según sea necesario en el archivo my.ini ubicado en {AEM_HOME}/mysql.
