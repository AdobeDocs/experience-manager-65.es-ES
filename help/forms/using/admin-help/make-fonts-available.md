---
title: Hacer que las fuentes estén disponibles
description: AEM Asegúrese de que las fuentes utilizadas en un formulario estén disponibles para su uso en el servidor de aplicaciones J2EE que aloja los formularios de la aplicación de la aplicación de la aplicación de la aplicación de que se trate.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 3%

---

# Hacer que las fuentes estén disponibles {#make-fonts-available}

AEM Asegúrese de que las fuentes utilizadas en un formulario estén disponibles para su uso en el servidor de aplicaciones J2EE que aloja los formularios de la aplicación de la aplicación de la aplicación de la aplicación de que se trate. Por ejemplo, imagine el siguiente escenario. Un diseñador de formularios agrega una fuente al directorio de fuentes que utiliza Designer y crea un formulario que utiliza esa fuente en un equipo independiente. Para que el servicio Output utilice la fuente, colóquela en el directorio de fuentes del cliente. AEM Si el directorio de fuentes del cliente no existe, cree un directorio en el servidor de aplicaciones J2EE que aloje los formularios de la aplicación de la aplicación de.

Para obtener información sobre la configuración de fuentes adicional, consulte [AEM Configurar opciones generales de formularios](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Especifique la ubicación del directorio de fuentes del cliente**

1. En la consola de administración, haga clic en Configuración > Configuración de sistemas principales > Configuraciones.
1. En el cuadro Ubicación del directorio de fuentes del sistema, escriba la ruta de acceso al directorio de fuentes del cliente. Se pueden agregar varios directorios separados por punto y coma **;**
1. Haga clic en Aceptar.
1. AEM Reinicie el sistema en el que se han instalado los formularios de.

>[!NOTE]
>
>Las fuentes se seleccionan de la caché de fuentes del sistema de Windows y es necesario reiniciar el sistema para actualizar la caché. AEM Después de especificar el directorio de fuentes del cliente, asegúrese de reiniciar el sistema en el que está instalado el formulario de la aplicación de la versión de la aplicación de datos de la aplicación de la aplicación de datos de usuario.
