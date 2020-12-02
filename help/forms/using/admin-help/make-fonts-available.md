---
title: Disponibilidad de fuentes
seo-title: Disponibilidad de fuentes
description: Asegúrese de que las fuentes utilizadas en un formulario están disponibles para su uso en el servidor de aplicaciones J2EE que aloja AEM formularios.
seo-description: Asegúrese de que las fuentes utilizadas en un formulario están disponibles para su uso en el servidor de aplicaciones J2EE que aloja AEM formularios.
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Habilitar fuentes {#make-fonts-available}

Asegúrese de que las fuentes utilizadas en un formulario están disponibles para su uso en el servidor de aplicaciones J2EE que aloja AEM formularios. Por ejemplo, considere el siguiente escenario. Un diseñador de formularios agrega una fuente al directorio de fuentes que utiliza Designer y crea un formulario que utiliza esa fuente en un equipo independiente. Para que el servicio Output utilice la fuente, colóquela en el directorio de fuentes del cliente. Si el directorio de fuentes del cliente no existe, cree un directorio en el servidor de aplicaciones J2EE que aloja AEM formularios.

Para obtener más información sobre la configuración de fuentes adicionales, consulte [Configuración general de los formularios de AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Especifique la ubicación del directorio de fuentes del cliente**

1. En la consola de administración, haga clic en Configuración > Configuración de sistemas principales > Configuraciones.
1. En el cuadro Ubicación del directorio de fuentes del sistema, escriba la ruta del directorio de fuentes del cliente. Se pueden agregar varios directorios separados por un punto y coma **;**
1. Haga clic en Aceptar.
1. Reinicie el sistema en el que están instalados AEM formularios.

>[!NOTE]
>
>Las fuentes se seleccionan de la caché de fuentes del sistema de Windows y es necesario reiniciar el sistema para actualizar la caché. Después de especificar el directorio de fuentes del cliente, asegúrese de reiniciar el sistema en el que se instalan AEM formularios.

