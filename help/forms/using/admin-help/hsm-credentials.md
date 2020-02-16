---
title: Administración de credenciales de HSM
seo-title: Administración de credenciales de HSM
description: Obtenga información sobre cómo administrar las credenciales de HSM.
seo-description: Obtenga información sobre cómo administrar las credenciales de HSM.
uuid: 30ddcd4a-f771-44d5-bdef-4826adcd0c44
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5f17ba8-8aab-4449-811a-20ad33de1c6f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Administración de credenciales de HSM {#managing-hsm-credentials}

Desde la página Administración de almacén de confianza, puede administrar las credenciales del Módulo de seguridad de hardware (HSM). Un HSM es un dispositivo PKCS#11 de terceros que puede utilizar para generar y almacenar claves privadas de forma segura. El HSM protege físicamente el acceso a las claves privadas y su uso.

El software cliente es necesario para comunicarse con el HSM. El software cliente HSM debe estar instalado y configurado en el mismo equipo que los formularios AEM.

Las firmas digitales de formularios AEM pueden utilizar las credenciales almacenadas en un HSM para aplicar firmas digitales de servidor. Siga las instrucciones de esta sección para crear un alias para cada credencial de HSM que usará Digital Signatures. El alias contiene todos los parámetros requeridos por el HSM.

>[!NOTE]
>
>Después de cambiar la configuración de HSM, reinicie el servidor de formularios AEM.

## Crear un alias para una credencial HSM cuando el dispositivo HSM está en línea {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM y, a continuación, haga clic en Agregar.
1. En el cuadro Nombre de perfil, escriba una cadena que se utilice para identificar el alias. Este valor se utiliza como propiedad para algunas operaciones de firmas digitales, como la operación Firmar campo de firma.
1. En el cuadro Biblioteca PKCS11, escriba la ruta completa de la biblioteca de cliente HSM en el servidor. Por ejemplo, `c:\Program Files\LunaSA\cryptoki.dll`. En un entorno agrupado, esta ruta debe ser idéntica para todos los servidores del clúster.
1. Haga clic en Probar conectividad HSM. Si los formularios AEM pueden conectarse al dispositivo HSM, aparece un mensaje que indica que el HSM está disponible. Haga clic en Siguiente.
1. Utilice el Nombre del token, ID de ranura o Índice de lista de ranuras para identificar dónde se almacenan las credenciales en el HSM.

   * **** Nombre del token: Corresponde al nombre de la partición HSM que se va a utilizar (por ejemplo, HSMPART1).
   * **** Id. de ranura: El ID de ranura es un identificador de ranura de tipo de datos largo.
   * **** Índice de lista de ranuras: Si selecciona Índice de lista de ranuras, establezca la Información de ranura en un entero que corresponda a la ranura. Es un índice basado en 0, lo que significa que si el cliente está registrado primero con la partición HSMPART1, HSMPART1 se referirá usando el valor 0 de SlotListIndex.

1. En el cuadro Pin de token, escriba la contraseña necesaria para acceder a la clave HSM y haga clic en Siguiente.
1. En el cuadro Credenciales, seleccione una credencial. Haga clic en Guardar.

## Crear un alias para una credencial HSM cuando el dispositivo HSM está sin conexión {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM y, a continuación, haga clic en Agregar.
1. En el cuadro Nombre de perfil, escriba una cadena que se utilice para identificar el alias. Este valor se utiliza como propiedad para algunas operaciones de firmas digitales, como la operación Firmar campo de firma.
1. En el cuadro Biblioteca PKCS11, escriba la ruta completa de la biblioteca de cliente HSM en el servidor. Por ejemplo, `c:\Program Files\LunaSA\cryptoki.dll`. En un entorno agrupado, esta ruta debe ser idéntica para todos los servidores del clúster.
1. Active la casilla de verificación Creación de perfil sin conexión. Haga clic en Siguiente.
1. En la lista de dispositivos HSM, seleccione el fabricante del dispositivo HSM donde se almacena la credencial.
1. En la lista Tipo de ranura, seleccione Id. de ranura, Índice de ranura o Nombre de token y especifique un valor en el cuadro Información de ranura. Los formularios AEM utilizan esta configuración para determinar dónde se almacenan las credenciales en el HSM.

   * **** Nombre del token: Corresponde a un nombre de partición (por ejemplo, HSMPART1).
   * **** Id. de ranura: El ID de ranura es un entero que corresponde a la ranura, que a su vez corresponde a una partición. Por ejemplo, el cliente (servidor de formularios) se registró primero con la partición HSMPART1. Esto asigna la ranura 1 a la partición HSMPART1, para este cliente. Debido a que HSMPART1 es la primera partición registrada, el ID de ranura es 1 y usted establecería Información de ranura en 1.

      El ID de ranura se establece cliente por cliente. Si ha registrado una segunda máquina en una partición diferente (por ejemplo, HSMPART2 en el mismo dispositivo HSM), entonces la ranura 1 se asociará con la partición HSMPART2 para ese cliente.

   * **** Índice de ranuras: Si selecciona Índice de ranura, establezca la Información de ranura en un entero que corresponda a la ranura. Es un índice basado en 0, lo que significa que si el cliente está registrado primero con la partición HSMPART1, la ranura 1 se asigna a HSMPART1 para este cliente. Debido a que HSMPART1 es la primera partición registrada, el Índice de ranuras es 0.

1. Seleccione una de estas opciones y proporcione la ruta:

   * **Certificado**: (No es necesario si se utiliza SHA1) Haga clic en Examinar y busque la ruta a la clave pública para las credenciales que está utilizando.
   * **** Certificado SHA1: (No es necesario si se utiliza un certificado físico) Escriba el valor SHA1 (huella digital) del archivo de clave pública (.cer) para la credencial que está utilizando. Asegúrese de que no hay espacios utilizados en el valor SHA1.

1. En el cuadro Contraseña, escriba la contraseña necesaria para acceder a la clave HSM de la información de ranura dada y, a continuación, haga clic en Guardar.

## Ver propiedades de alias de credenciales de HSM {#view-hsm-credential-alias-properties}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Haga clic en el nombre de alias del alias de credenciales para ver las propiedades y, a continuación, haga clic en Aceptar.

## Compruebe el estado de una credencial HSM {#check-the-status-of-an-hsm-credential}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Haga clic en la casilla de verificación situada junto a las credenciales que desee comprobar y haga clic en Comprobar estado.

La columna Estado refleja el estado actual de la credencial. En caso de error, se muestra una X roja en la columna Estado. Pase el ratón sobre la X para mostrar una información del objeto que contenga el motivo del error.

## Actualizar propiedades de alias de credenciales HSM {#update-hsm-credential-alias-properties}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Haga clic en el nombre de alias del alias de credenciales.
1. Haga clic en Actualizar credenciales y actualice la configuración según sea necesario.

## Restablecer todas las conexiones HSM {#reset-all-hsm-connections}

Restablezca las conexiones abiertas a un dispositivo HSM después de cualquier interrupción en la sesión de red entre el servidor de formularios y el dispositivo HSM. Por ejemplo, pueden producirse interrupciones debido a una interrupción de la red o al desconexión del dispositivo HSM para una actualización de software. Después de una interrupción, las conexiones existentes están obsoletas y cualquier solicitud de firma contra dichas conexiones falla. Al utilizar la opción Restablecer todas las conexiones HSM, se borran las conexiones antiguas.

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Haga clic en Restablecer todas las conexiones HSM.

## Eliminar un alias de credenciales HSM {#delete-an-hsm-credential-alias}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Seleccione las casillas de verificación de las credenciales de HSM que desee eliminar, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

## Configuración de la compatibilidad remota con HSM {#configure-remote-hsm-support}

Los formularios AEM utilizan un mecanismo IPC/RPC basado en servicios Web. Este mecanismo permite que los formularios AEM utilicen un HSM instalado en un equipo remoto. Para utilizar esta funcionalidad, instale el servicio Web en el equipo remoto en el que esté instalado el HSM. Consulte [Configuración de la compatibilidad con HSM para formularios AEM ES mediante Sun JDK en plataformas Windows de 64 bits para](https://kb2.adobe.com/cps/808/cpsid_80835.html)obtener más información.

Este mecanismo no admite la creación en línea de perfiles de HSM ni comprobaciones de estado. Sin embargo, existen dos formas de crear perfiles HSM y realizar comprobaciones de estado:

* Cree una credencial de cliente de formularios AEM pasándole el certificado del firmante. Siga los pasos que se describen en [Configuración de la compatibilidad con HSM para formularios AEM ES mediante Sun JDK en una plataforma](https://kb2.adobe.com/cps/808/cpsid_80835.html)de Windows de 64 bits. La ubicación del servicio Web se transfiere como propiedad Credential. También se admiten perfiles HSM sin conexión que se crean con el certificado de identificación o el certificado SHA-1 hexadecimal. Sin embargo, si ha actualizado los formularios AEM desde una versión anterior de los formularios AEM, realice cambios en el cliente porque las credenciales contenían información sobre el certificado y el servicio Web.
* La ubicación del servicio Web se especifica en la consola de administración para el servicio Signature. (Consulte Configuración [del servicio](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings)de firma). Aquí, el cliente solo llevaba el alias del perfil de HSM en el almacén de confianza. Puede utilizar esta opción sin problemas sin ningún cambio de cliente, incluso si ha actualizado los formularios AEM a partir de una versión anterior de los formularios AEM. Esta opción no admite perfiles HSM con el certificado SHA-1.

