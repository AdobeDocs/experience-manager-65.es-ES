---
title: Este artículo incluye las instrucciones para desinstalar el paquete de complementos de Forms mediante el Administrador de paquetes de CRX.
description: Obtenga información sobre los pasos para desinstalar el paquete de complementos de Forms mediante el Administrador de paquetes de CRX.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 2755e414ea23ebc1472e9c08d832eca93f28311b
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---


# Desinstalar el paquete de complementos de AEM Forms AEM de la instancia de

Este artículo describe los pasos necesarios para desinstalar correctamente el paquete de complementos de AEM Forms de una instancia del SDK de AEM Forms. Siga estos pasos para asegurarse de eliminar el paquete de complementos de Forms AEM y evitar posibles problemas con su entorno de.

## Requisito previo

Asegúrese de realizar una copia de seguridad para evitar la pérdida de datos.

## Para desinstalar el paquete de complementos de AEM Forms

Para desinstalar el paquete de complementos de AEM Forms, realice los siguientes pasos:

1. **Desinstalar el paquete de complementos de AEM Forms:**
   1. Vaya a `http://[host]:[port]/crx/de/index.jsp`.
   1. Busque y desinstale `AEM Forms add-on package`.

   ![Desinstalar paquete](/help/forms/using/assets/uninstall-aem-forms-package.png)

1. **Eliminar la carpeta nativa de CRXDE:**
   1. Vaya a `http://[host]:[port]/crx/de/index.jsp`.
   1. Vaya a `/libs/fd/native/install` y elimine la carpeta `native` en CRXDE.

      ![Eliminar nodo nativo de CRX/de](/help/forms/using/assets/native-install-folder-crxde.png)
   1. Guarde los cambios.

1. **Detener el SDK de AEM Forms:**
   1. Detenga la instancia del SDK de AEM Forms mediante el comando &quot;Ctrl + C&quot;.

1. **Busque la base e instale carpetas en la carpeta crx-quickstart**
   1. Vaya a la carpeta `..author\crx-quickstart` en la instancia del SDK para AEM Forms.
   1. Busque carpetas con los nombres `bedrock` y `install`.
Si se encuentran, asegúrese de que se eliminen de la carpeta `crx-quickstart` en la instancia del SDK de AEM Forms.

   >[!NOTE]
   >
   > La carpeta `bedrock` se vuelve a crear automáticamente al reiniciar la instancia del SDK de AEM Forms.

1. AEM **Reiniciar la instancia de la:**
   1. Una vez completados todos los pasos anteriores, [reinicie la instancia del SDK para AEM Forms](/help/forms/using/restart-aem-sdk.md).




