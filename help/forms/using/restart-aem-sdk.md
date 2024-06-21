---
title: AEM ¿Cómo reiniciar el SDK de la?
description: AEM Prácticas recomendadas para reiniciar el SDK de la
role: Admin, Developer, User
feature: Adaptive Forms, Troubleshooting
exl-id: f5d69d04-b842-4329-b1b3-57b88266d13d
solution: Experience Manager, Experience Manager Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 15%

---

# AEM Reinicio del SDK de la

AEM AEM Si reinicia el SDK de la deteniendo los procesos de Java™, puede provocar incoherencias en el entorno de desarrollo de la y se producirá un error como el siguiente:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/using/assets/restart-sdk-error.png)

## Solución

AEM Para reiniciar el SDK de la, vaya a la ventana de comandos activa y pulse `Ctrl + C` para reiniciar el SDK.

Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. AEM AEM El reinicio del SDK de la con métodos alternativos, como detener los procesos de Java™, puede generar incoherencias en el entorno de desarrollo de la.
