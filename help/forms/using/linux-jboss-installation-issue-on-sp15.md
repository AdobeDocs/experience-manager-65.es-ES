---
title: Problema de instalación del Service Pack de AEM Forms JEE 6.5.15.0 en el entorno JBoss® Linux®
description: El Service Pack de AEM Forms JEE 6.5.15.0 no está instalado correctamente en el entorno JBoss® Linux®, los cambios de parche no se aplican al servidor de aplicaciones. Añada el archivo RUP_BOM.xml al directorio XML.
SEO Description: AEM Forms JEE 6.5.15.0 service pack  is not installed properly on the JBoss Linux environment.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 16%
---
# Problema de instalación del paquete de servicio JEE de AEM Forms 6.5.15.0 en el entorno JBoss® {#aem-forms-installation-issue-environment}

## Problema {#issue}

El Service Pack 6.5.15.0 de AEM Forms JEE no está instalado correctamente en el entorno JBoss® Linux®. En el archivo `PatchInstallerProcessing[1-9*].log`, la entrada de registro `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing` está registrada. Esta entrada indica que la instalación del Service Pack 6.5.15.0 de AEM Forms JEE no es correcta.

## Se aplica a {#applies-to}

Esta solución se aplica a:
* Entorno JBoss® Linux®

>[!NOTE]
>
> Asegúrese de que el Service Pack 6.5.15.0 de AEM Forms JEE esté instalado en el servidor de aplicaciones al menos una vez antes de realizar los pasos de [agregar el archivo RUP_BOM.xml al directorio XML](#solution-solution).

## Solución {#solution}

Para solucionar el problema de instalación del Service Pack de AEM Forms JEE 6.5.15.0, agregue el archivo `RUP_BOM.xml` al directorio XML:
1. Vaya a la carpeta donde extrajo el parche `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Vaya a la ubicación `/CDROM_Installers/Linux/Disk1/InstData` y busque el archivo `Resource1.zip`.
1. Copie el archivo `Resource1.zip` en otra ubicación fuera de la carpeta extraída y descomprima el archivo `Resource1.zip`.
1. Vaya a `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` y copie el archivo `RUP_BOM.xml`.
1. Pegue el archivo RUP_BOM.xml en `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Vuelva a instalar el [Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) de AEM Forms JEE 6.5.15.0.
