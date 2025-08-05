---
title: Mitigación de vulnerabilidades de XE, configuración del modo de desarrollo de Struts y ejecución remota de código para AEM Forms en JEE
description: Mitigación de vulnerabilidades de ejecución de código remoto, configuración y XXE para AEM Forms en JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 9fade12f-a038-4fd6-8767-1c30966574c5
solution: Experience Manager, Experience Manager Forms
release-date: 2025-08-05T00:00:00Z
source-git-commit: 9be9bfc9e20a151afdb9ae2cddcc39b4d2701c1b
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 5%

---

# Mitigación de RCE (CVE-2025-49533), configuración del modo de desarrollo de Struts (CVE-2025-54253), XXE (CVE-2025-54254) y vulnerabilidades para AEM Forms en JEE {#mitigating-xxe-configuration-rce-vulnerabilities-aem-forms}

## Referencia rápida

| **Nivel de impacto** | **Versiones afectadas** | **Acción recomendada** |
|---|---|---|
| **Crítico** | AEM 6.5 Forms en JEE Service Pack 23 (6.5.23.0) | [Instalar la revisión más reciente](#option-1-for-users-on-version-65230-install-latest-hotfix) |
| **Crítico** | AEM 6.5 Forms en JEE Service Pack 18 a 22 (6.5.18.0 - 6.5.22.0) | [Instale manualmente las correcciones](#option-2-for-users-on-65180---65220-manual-hotfix-installation) |
| **Crítico** | AEM 6.5 Forms en JEE Service Pack 17 (6.5.17.0) o anterior | Actualice a una versión de Service Pack compatible y, a continuación, aplique los pasos de mitigación recomendados para su nueva versión |
| **No Afectado** | AEM Forms en OSGi, Workbench, Cloud Service | No se requiere ninguna acción |

**Vulnerabilidades resueltas:**

- Ejecución remota de código (CVE-2025-49533)
- Problemas de seguridad de configuración (CVE-2025-54253)
- Procesamiento de entidad externa XML (XXE) (CVE-2025-54254)

## Información general

### Qué se ve afectado

| Vulnerabilidad | Impacto | Componentes afectados |
|---|---|---|
| **CVE-2025-49533**: ejecución remota de código | Ejecución de código no autenticado en GetDocumentServlet | AEM 6.5 Forms en JEE Service Pack 23 (6.5.23.0) y anteriores |
| **CVE-2025-54253**: Problemas de configuración | Modo de desarrollo de inicios habilitado en la IU de administración | AEM 6.5 Forms en JEE Service Pack 23 (6.5.23.0) y anteriores |
| **CVE-2025-54254**: Procesamiento XXE | El módulo Document Security permite el acceso no autorizado a archivos | AEM 6.5 Forms en JEE Service Pack 23 (6.5.23.0) y anteriores |


### Qué no se ve afectado

- Experience Manager Forms Workbench (todas las versiones)
- Experience Manager Forms en OSGi (todas las versiones)
- Experience Manager Forms as a Cloud Service

## Opciones de resolución


### Antes de comenzar

Antes de realizar cualquier cambio, realice una copia de seguridad del archivo EAR o del archivo DSC que está a punto de modificar o actualizar:

- Busque el archivo EAR o DSC original en el directorio de implementación.
- Copie el archivo en una ubicación de copia de seguridad segura fuera del directorio de implementación.
- Asegúrese de que la copia de seguridad esté completa y accesible antes de continuar con cualquier actualización.

Esta precaución le permite restaurar el estado original en caso de que encuentre algún problema durante el proceso de actualización.

### Opción 1: (para usuarios de la versión 6.5.23.0) Instalar la revisión más reciente

1. [Descargar la revisión de 6.5.23.0](/help/release-notes/aem-forms-hotfix.md).
1. Siga las instrucciones estándar de instalación de [revisión/parche](/help/release-notes/jee-patch-installer-65.md)
1. Si utiliza Document Security (anteriormente Rights Management) en IBM WebSphere o Oracle WebLogic, establezca la siguiente propiedad del sistema Java (argumento JVM) antes de iniciar el servidor de AEM Forms:

   ```
   -Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
   ```

1. Reinicie el servidor de aplicaciones

### Opción 2: (para usuarios de 6.5.18.0 - 6.5.22.0) Instalación manual de revisión

+++Instalación manual de revisión para 6.5.18.0 mediante 6.5.22.0

**Paso 1: Descargar y extraer el paquete de revisión**

- Descargar la revisión [para 6.5.18.0 - 6.5.22.](/help/release-notes/aem-forms-hotfix.md) desde el Portal de distribución de software de Adobe
- Extraerlo localmente

**Paso 2: Vaya a la carpeta de versiones correcta**

- En función de la versión del paquete de servicio instalada en su entorno, vaya a la carpeta correspondiente.

  Ejemplo de Service Pack 20: la carpeta es:

  ```
  <extracted-hotfix>/SP20/
  ```

**Paso 3: Busque el directorio de implementación**

- En el servidor AEM Forms en JEE, vaya a:

  ```
  [AEM installation directory]/deploy
  ```

  Ejemplo: `adobe/adobe-experience-manager-forms/deploy`



**Paso 4: actualizar y reemplazar los archivos EAR**

>[!BEGINTABS]

>[!TAB JBoss]

1. Abra `adobe-core-jboss.ear` y reemplace `adminui.war` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adminui.war
   ```

   Por ejemplo, `adobe-xxe-configuration-hotfix/SP20/jboss/adminui.war`

1. Dentro de `adobe-core-jboss.ear`, vaya a la carpeta `lib/` y reemplace `adobe-uisupport.jar` por:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Por ejemplo, `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. Salva la OREJA. Asegúrese de que los cambios se hayan guardado correctamente.


1. Reemplazar `adobe-edcserver-jboss.ear` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-edcserver-jboss.ear
   ```

   Por ejemplo, `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-edcserver-jboss.ear`

1. Reemplazar `adobe-forms-jboss.ear` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-forms-jboss.ear
   ```

   Por ejemplo, `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-forms-jboss.ear`



>[!TAB WebLogic]

1. Abra `adobe-core-weblogic.ear` y reemplace `adminui.war` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adminui.war
   ```

   Por ejemplo, `adobe-xxe-configuration-hotfix/SP20/weblogic/adminui.war`

1. Dentro de `adobe-core-weblogic.ear`, reemplazar `adobe-uisupport.jar` por:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Por ejemplo, `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. Salva la OREJA. Asegúrese de que los cambios se hayan guardado correctamente.


1. Reemplazar `adobe-edcserver-weblogic.ear` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-edcserver-weblogic.ear
   ```

   Por ejemplo, `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-edcserver-weblogic.ear`

1. Reemplazar `adobe-forms-weblogic.ear` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-forms-weblogic.ear
   ```

   Por ejemplo, `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-forms-weblogic.ear`

>[!TAB WebSphere]

1. Abra `adobe-core-websphere.ear` y reemplace `adminui.war` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adminui.war
   ```

   Por ejemplo, `adobe-xxe-configuration-hotfix/SP20/websphere/adminui.war`

1. Dentro de `adobe-core-websphere.ear`, reemplazar `adobe-uisupport.jar` por:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Por ejemplo, `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. Salva la OREJA. Asegúrese de que los cambios se hayan guardado correctamente.


1. Reemplazar `adobe-edcserver-websphere.ear` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-edcserver-websphere.ear
   ```

   Por ejemplo, `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-edcserver-websphere.ear`

1. Reemplazar `adobe-forms-websphere.ear` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-forms-websphere.ear
   ```

   Por ejemplo, `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-forms-websphere.ear`

>[!ENDTABS]



**Paso 5: actualizar `adobe-rightsmanagement-<appserver>-dsc.jar`archivo con**

```
adobe-xxe-configuration-hotfix/SP[version]/<appserver>/adobe-rightsmanagement-<appserver>-dsc.jar
```

Por ejemplo, `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-rightsmanagement-jboss-dsc.jar`

**Paso 6: Configuración adicional para Document Security en WebSphere y WebLogic**:

Si utiliza Document Security (anteriormente Rights Management), establezca la siguiente propiedad del sistema Java (argumento JVM) antes de iniciar el servidor de AEM Forms:

```
-Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
```


**Paso 7: Vuelva a ejecutar el Administrador de configuración**

- Inicie el Administrador de configuración para volver a implementar el EAR actualizado y aplicar la revisión

+++

### Opción 3: (para usuarios de 6.5.17.0 y versiones anteriores) Ruta de actualización

1. [Actualización a una versión de Service Pack compatible](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)
1. Siga la Opción 1 u Opción 2 según su nueva versión

## Referencias

- [CWE-611: Restricción incorrecta de la referencia de entidad externa XML](https://cwe.mitre.org/data/definitions/611.html)
- [CWE-16: Configuración](https://cwe.mitre.org/data/definitions/16.html)
- [Hoja de características clave de prevención de OWASP XXE](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_XXE_Processing)
- [Prácticas recomendadas de seguridad de Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=es)
