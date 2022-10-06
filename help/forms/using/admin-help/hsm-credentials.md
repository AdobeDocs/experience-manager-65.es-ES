---
title: Administración de credenciales HSM
seo-title: Managing HSM credentials
description: Obtenga información sobre cómo administrar las credenciales de HSM.
seo-description: Learn how to manage HSM credentials.
uuid: 30ddcd4a-f771-44d5-bdef-4826adcd0c44
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5f17ba8-8aab-4449-811a-20ad33de1c6f
exl-id: facbeab2-de95-4778-894c-faa771d3391e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 0%

---

# Administración de credenciales HSM {#managing-hsm-credentials}

Desde la página Administración de almacén de confianza, puede administrar las credenciales del Módulo de seguridad de hardware (HSM). Un HSM es un dispositivo PKCS#11 de terceros que puede utilizar para generar y almacenar claves privadas de forma segura. El HSM protege físicamente el acceso a las claves privadas y su uso.

El software cliente es necesario para comunicarse con el HSM. El software cliente HSM debe estar instalado y configurado en el mismo equipo que AEM formularios.

AEM formularios Digital Signatures puede utilizar credenciales almacenadas en un HSM para aplicar firmas digitales del lado del servidor. Siga las instrucciones de esta sección para crear un alias para cada credencial de HSM que utilizarán las firmas digitales. El alias contiene todos los parámetros requeridos por el HSM.

>[!NOTE]
>
>Después de cambiar la configuración de HSM, reinicie el servidor de AEM forms.

## Crear un alias para una credencial HSM cuando el dispositivo HSM está en línea {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM y, a continuación, haga clic en Agregar.
1. En el cuadro Nombre de perfil, escriba una cadena utilizada para identificar el alias. Este valor se utiliza como propiedad para algunas operaciones de firmas digitales, como la operación Firmar campo de firma .
1. En el cuadro Biblioteca PKCS11, escriba la ruta completa de su biblioteca de cliente HSM en el servidor. Por ejemplo, `c:\Program Files\LunaSA\cryptoki.dll`. En un entorno agrupado, esta ruta debe ser idéntica para todos los servidores del clúster.
1. Haga clic en Probar conectividad HSM. Si AEM formularios pueden conectarse al dispositivo HSM, aparece un mensaje que indica que el HSM está disponible. Haga clic en Siguiente.
1. Utilice el Nombre del token, el ID de ranura o el Índice de lista de ranuras para identificar dónde se almacenan las credenciales en el HSM.

   * **Nombre del token:** Corresponde al nombre de la partición HSM que se va a utilizar (por ejemplo, HSMPART1).
   * **Id De Ranura:** El ID de ranura es un identificador de ranura del tipo de datos long.
   * **Índice de lista de ranuras:** Si selecciona Índice de lista de ranuras, establezca la información de ranura en un número entero que corresponda a la ranura. Se trata de un índice basado en 0, lo que significa que si el cliente está registrado primero con la partición HSMPART1, se hará referencia a HSMPART1 utilizando el valor 0 de SlotListIndex.

1. En el cuadro Token Pin, escriba la contraseña necesaria para acceder a la clave HSM y haga clic en Next.
1. En el cuadro Credenciales, seleccione una credencial. Haga clic en Guardar.

## Crear un alias para una credencial HSM cuando el dispositivo HSM está sin conexión {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM y, a continuación, haga clic en Agregar.
1. En el cuadro Nombre de perfil, escriba una cadena utilizada para identificar el alias. Este valor se utiliza como propiedad para algunas operaciones de firmas digitales, como la operación Firmar campo de firma .
1. En el cuadro Biblioteca PKCS11, escriba la ruta completa de su biblioteca de cliente HSM en el servidor. Por ejemplo, `c:\Program Files\LunaSA\cryptoki.dll`. En un entorno agrupado, esta ruta debe ser idéntica para todos los servidores del clúster.
1. Active la casilla de verificación Creación de perfiles sin conexión . Haga clic en Siguiente.
1. En la lista de dispositivos HSM, seleccione el fabricante del dispositivo HSM en el que se almacena la credencial.
1. En la lista Tipo de ranura, seleccione Id. de ranura, Índice de ranura o Nombre de token y especifique un valor en el cuadro Información de ranura. AEM formularios utiliza esta configuración para determinar dónde se almacenan las credenciales en el HSM.

   * **Nombre del token:** Corresponde a un nombre de partición (por ejemplo, HSMPART1).
   * **Id De Ranura:** El ID de ranura es un número entero que corresponde a la ranura, que a su vez corresponde a una partición. Por ejemplo, el cliente (servidor de formularios) registrado primero con la partición HSMPART1. Esto asigna la ranura 1 a la partición HSMPART1, para este cliente. Como HSMPART1 es la primera partición registrada, el ID de ranura es 1 y usted establecería Información de ranura en 1.

      El ID de ranura se establece cliente por cliente. Si ha registrado una segunda máquina en una partición diferente (por ejemplo, HSMPART2 en el mismo dispositivo HSM), la ranura 1 se asociará con la partición HSMPART2 para ese cliente.

   * **Índice de ranura:** Si selecciona Índice de ranura, establezca la información de ranura en un número entero que corresponda a la ranura. Este es un índice basado en 0, lo que significa que si el cliente está registrado primero con la partición HSMPART1, la ranura 1 está asignada al HSMPART1 para este cliente. Como HSMPART1 es la primera partición registrada, el Índice de ranuras es 0.

1. Seleccione una de estas opciones y proporcione la ruta:

   * **Certificado**: (No es necesario si se utiliza SHA1) Haga clic en Examinar y busque la ruta a la clave pública de las credenciales que está utilizando.
   * **Certificado SHA1:** (No es necesario si se utiliza un certificado físico) Valor SHA1 (huella digital) del archivo de clave pública (.cer) para la credencial que se está utilizando. Asegúrese de que no haya espacios utilizados en el valor SHA1.

1. En el cuadro Contraseña, escriba la contraseña necesaria para acceder a la clave HSM de la información de ranura dada y, a continuación, haga clic en Guardar.

## Ver propiedades de alias de credenciales de HSM {#view-hsm-credential-alias-properties}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Haga clic en el nombre del alias de la credencial para ver las propiedades y, a continuación, haga clic en Aceptar.

## Comprobar el estado de una credencial HSM {#check-the-status-of-an-hsm-credential}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Haga clic en la casilla de verificación situada junto a las credenciales que desea comprobar y haga clic en Comprobar estado.

La columna Estado refleja el estado actual de la credencial. En caso de error, se muestra una X roja en la columna Estado. Pase el ratón sobre la X para mostrar una información del objeto que contenga el motivo del error.

## Actualización de las propiedades de alias de credenciales de HSM {#update-hsm-credential-alias-properties}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Haga clic en el nombre de alias del alias de credenciales.
1. Haga clic en Actualizar credencial y actualice la configuración según sea necesario.

## Restablecer todas las conexiones HSM {#reset-all-hsm-connections}

Restablezca las conexiones abiertas a un dispositivo HSM después de cualquier interrupción en la sesión de red entre el servidor de formularios y el dispositivo HSM. Por ejemplo, pueden producirse interrupciones debido a una interrupción de la red o al desconexión del dispositivo HSM para una actualización de software. Después de una interrupción, las conexiones existentes están obsoletas y cualquier solicitud de firma contra esas conexiones falla. Al utilizar la opción Restablecer todas las conexiones HSM, se borran las conexiones antiguas.

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Haga clic en Restablecer todas las conexiones HSM.

## Eliminar un alias de credenciales HSM {#delete-an-hsm-credential-alias}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Seleccione las casillas de verificación de las credenciales de HSM que desea eliminar, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

## Configuración de la compatibilidad con HSM remoto {#configure-remote-hsm-support}

AEM formularios utiliza un mecanismo IPC/RPC basado en Web Services. Este mecanismo permite que AEM formularios utilicen un HSM instalado en un equipo remoto. Para utilizar esta funcionalidad, instale el servicio web en el equipo remoto en el que está instalado el HSM. Consulte [Configuración de la compatibilidad con HSM para formularios AEM ES mediante Sun JDK en una plataforma Windows de 64 bits](https://kb2.adobe.com/cps/808/cpsid_80835.html)para obtener más información.

Este mecanismo no admite la creación en línea de perfiles HSM o comprobaciones de estado. Sin embargo, existen dos formas de crear perfiles HSM y realizar comprobaciones de estado:

* Cree una credencial de cliente de formularios AEM pasándola al Certificado del firmante. Siga los pasos indicados en [Configuración de la compatibilidad con HSM para formularios AEM ES mediante Sun JDK en una plataforma Windows de 64 bits](https://kb2.adobe.com/cps/808/cpsid_80835.html). La ubicación del servicio web se transfiere como propiedad Credential. También se admiten perfiles HSM sin conexión creados con el certificado SHA-1 hexadecimal o con el certificado SHA-1. Sin embargo, si ha actualizado a AEM formularios desde una versión anterior de AEM formularios, realice cambios en el cliente porque las credenciales conllevan información de certificado y servicio Web.
* La ubicación del servicio web se especifica en la consola de administración para el servicio de firma. (Consulte [Configuración del servicio de firma](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings).) En este caso, el cliente solo llevaba el alias del perfil HSM en el almacén de confianza. Puede utilizar esta opción sin problemas sin ningún cambio del cliente, incluso si ha actualizado a AEM formularios de una versión anterior de AEM formularios. Esta opción no admite perfiles HSM que utilicen el certificado SHA-1.
