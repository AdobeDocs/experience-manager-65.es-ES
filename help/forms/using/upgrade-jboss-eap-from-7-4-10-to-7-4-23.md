---
title: Actualice JBoss EAP de 7.4.10 a 7.4.23 para AEM Forms en JEE
description: Pasos para actualizar JBoss EAP de 7.4.10 a 7.4.23 para AEM Forms en entornos independientes JEE.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
exl-id: 8f4c2a91-6b3d-4e7f-9c12-5d8e1f0a2b34
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms Upgrade,AEM Forms on JEE
role: User, Developer
source-git-commit: 652162941dd716ae797ce50709e91757dad99054
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 3%

---

# Actualice JBoss EAP de 7.4.10 a 7.4.23 para AEM Forms en JEE {#upgrade-jboss-eap-from-7-4-10-to-7-4-23}

## Información general {#overview}

Actualice JBoss EAP de la versión 7.4.10 a la 7.4.23 en un entorno independiente de AEM Forms en JEE. La actualización requiere la migración de los archivos de configuración, las credenciales de la base de datos y el repositorio de CRX a la nueva instalación de JBoss y la ejecución del Administrador de configuración para completar la instalación.

## Se aplica a {#applies-to}

Este artículo se aplica a:

* AEM Forms en JEE que se ejecuta en JBoss EAP 7.4.10 en un entorno independiente
* Modos de instalación llave en mano y llave en mano parcial en Windows y Linux

>[!NOTE]
>
> Si va a actualizar un entorno de clúster de JBoss, complete primero los pasos de este artículo y, a continuación, realice los pasos adicionales de [Actualizar el clúster EAP JBoss de la versión 7.4.10 a la versión 7.4.23 para AEM Forms en JEE](/help/forms/using/upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23.md).

## Requisitos previos {#prerequisites}

Antes de empezar:

* Descargue el paquete JBoss 7.4.23 desde el [Portal de distribución de software de Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html).
* Asegúrese de que tiene acceso administrativo al entorno de destino.
* Realice una copia de seguridad completa de la instalación de JBoss existente.

## Etapas {#steps}

Para actualizar JBoss EAP de 7.4.10 a 7.4.23, realice los siguientes pasos:

### Descargar y extraer JBoss {#download-and-extract-jboss}

1. Descargue el paquete JBoss 7.4.23 ZIP desde el Portal de distribución de software de Adobe.
1. Extraiga el archivo ZIP en un directorio local.
1. Cambie el nombre de la carpeta JBoss extraída para que coincida con el nombre exacto del directorio de instalación de JBoss existente.

### Realizar una copia de seguridad de la instalación existente {#back-up-the-existing-installation}

1. Cree una copia de seguridad completa del directorio de instalación de JBoss actual.
1. Compruebe que la copia de seguridad incluye todos los archivos de configuración y personalizaciones.

### Configurar archivos de base de datos {#configure-database-files}

1. Vaya al directorio de configuración:

   * Windows: `<JBoss_Home>\standalone\configuration`
   * Linux: `<JBoss_Home>/standalone/configuration`

1. Configure los archivos de base de datos en función del modo de instalación:

   **Modo llave en mano:**

   1. Cambiar el nombre de `lc_mysql.xml` a `lc_turnkey.xml`.
   1. Elimine los siguientes archivos:

      * `lc_oracle.xml`
      * `lc_mssql.xml`

   **Modo llave en mano parcial:**

   1. Mantener solamente el archivo `lc_db.xml` que corresponde al motor de base de datos.
   1. Eliminar los otros dos archivos de configuración de `lc_db.xml`.

### Actualizar credenciales de base de datos {#update-database-credentials}

1. Abra el archivo `lc_turnkey.xml` desde la instalación de JBoss de la copia de seguridad.
1. Copie los siguientes valores:

   * URL de origen de datos
   * Nombre de base de datos
   * Contraseña de base de datos

1. Actualizar las entradas correspondientes en el nuevo archivo `lc_turnkey.xml`.

### Migrar repositorio de CRX {#migrate-crx-repository}

1. Vaya al siguiente directorio de la instalación antigua de JBoss:

   `<old_jboss>\bin\`

1. Copie la carpeta `crx-quickstart`.
1. Pegue la carpeta en:

   `<new_jboss>\bin\`

### Ejecutar el Administrador de configuración {#run-configuration-manager}

1. Inicie el entorno JBoss actualizado.
1. Inicie el Administrador de configuración de LiveCycle (LCM).
1. Ejecute el flujo de trabajo completo e integral de Configuration Manager.
1. Compruebe que todas las tareas de configuración se hayan completado correctamente.

### Validación posterior a la actualización {#post-upgrade-validation}

Después de la actualización, confirme lo siguiente:

* Todos los servicios se inician correctamente.
* Conectividad de la base de datos verificada.
* Se valida la funcionalidad de la aplicación.
