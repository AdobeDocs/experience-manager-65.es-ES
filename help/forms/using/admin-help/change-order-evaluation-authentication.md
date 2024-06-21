---
title: Cambiar el orden de evaluación para la autenticación
description: AEM Puede cambiar el orden en el que los formularios de evalúan varios proveedores de autenticación.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 9%

---

# Cambiar el orden de evaluación para la autenticación {#change-the-order-of-evaluation-for-authentication}

AEM Si ha configurado varios proveedores de autenticación, puede cambiar el orden en que los formularios de los evalúan para la autenticación. El orden de los proveedores de autenticación que se enumeran en el archivo config.xml determina el orden de evaluación para la autenticación.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Para exportar la configuración actual a un archivo, haga clic en Exportar y guarde el archivo de configuración en otra ubicación.
1. Busque el siguiente nodo en el archivo:

   ```xml
    <node name="AuthSchemes">
        <map />
            <node name="CertificateAuth">
                <map>
                    <entry key="order" value="3" />
                    <entry key="name" value="edc.server.auth.scheme.certificate" />
                </map>
        </node>
        <node name="Kerberos">
            <map>
                <entry key="kerberosSPN" value="defaultSPN" />
                <entry key="order" value="1" />
                <entry key="name" value="edc.server.auth.scheme.kerberos" />
            </map>
    </node>
   ```

   Entrada `<entry key="order" value="3" />`, edite el valor de cada nodo para establecer el orden de evaluación de la autenticación.

1. Para importar el archivo actualizado, en Administración de usuarios, haga clic en Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Examinar para buscar el archivo, en Importar y, a continuación, en Aceptar.
