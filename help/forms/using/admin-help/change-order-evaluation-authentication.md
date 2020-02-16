---
title: Cambiar el orden de evaluación para la autenticación
seo-title: Cambiar el orden de evaluación para la autenticación
description: Puede cambiar el orden en que los formularios AEM evalúan varios proveedores de autenticación.
seo-description: Puede cambiar el orden en que los formularios AEM evalúan varios proveedores de autenticación.
uuid: c2693e5b-cf09-4bb8-815a-2b20ebf6eea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5434df9c-ecf6-450a-aa7e-d9ab69b66fe6
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Cambiar el orden de evaluación para la autenticación {#change-the-order-of-evaluation-for-authentication}

Si ha configurado varios proveedores de autenticación, puede cambiar el orden en que los formularios AEM los evalúan para la autenticación. El orden de los proveedores de autenticación enumerados en el archivo config.xml determina el orden de evaluación para la autenticación.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Para exportar la configuración actual a un archivo, haga clic en Exportar y guarde el archivo de configuración en otra ubicación.
1. Busque el nodo siguiente en el archivo:

   ```as3
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

   En `<entry key="order" value="3" />`, edite el valor de cada nodo para establecer el orden de la evaluación de autenticación.

1. Para importar el archivo actualizado, en Administración de usuarios, haga clic en Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Examinar para buscar el archivo, haga clic en Importar y, a continuación, en Aceptar.

