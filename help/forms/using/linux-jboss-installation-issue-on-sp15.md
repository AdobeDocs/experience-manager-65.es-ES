---
title: Problema de instalación del Service Pack de AEM Forms JEE 6.5.15.0 en el entorno JBoss® Linux®
description: El Service Pack de AEM Forms JEE 6.5.15.0 no está instalado correctamente en el entorno JBoss® Linux®, los cambios de parche no se aplican al servidor de aplicaciones. Añada el archivo RUP_BOM.xml al directorio XML.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 2%

---

# Problema de instalación de AEM Forms 6.5.15.0 JEE Service Pack en el entorno JBoss® {#aem-forms-installation-issue-environment}

## Problema {#issue}

El Service Pack de AEM Forms JEE 6.5.15.0 no está instalado correctamente en el entorno JBoss® Linux®. En el archivo `PatchInstallerProcessing[1-9*].log`, la entrada de registro `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing` está registrada. Esta entrada indica que la instalación del Service Pack de AEM Forms JEE 6.5.15.0 no se ha realizado correctamente.

## Se aplica a lo siguiente: {#applies-to}

Esta solución se aplica a:
* Entorno JBoss® Linux®

>[!NOTE]
>
> Asegúrese de que el Service Pack de AEM Forms JEE 6.5.15.0 esté instalado en el servidor de aplicaciones al menos una vez antes de realizar los pasos de [agregar el archivo RUP_BOM.xml al directorio XML](#solution-solution).

## Solución {#solution}

Para solucionar el problema de instalación del Service Pack de AEM Forms JEE 6.5.15.0, agregue el archivo `RUP_BOM.xml` al directorio XML:
1. Vaya a la carpeta donde extrajo el parche `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Vaya a la ubicación `/CDROM_Installers/Linux/Disk1/InstData` y busque el archivo `Resource1.zip`.
1. Copie el archivo `Resource1.zip` en otra ubicación fuera de la carpeta extraída y descomprima el archivo `Resource1.zip`.
1. Vaya a `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` y copie el archivo `RUP_BOM.xml`.
1. Pegue el archivo RUP_BOM.xml en `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Vuelva a instalar el [Service Pack de AEM Forms JEE 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).
