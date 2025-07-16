---
title: Revisiones para AEM Forms
description: Proporciona información sobre cómo descargar e instalar una revisión para AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 80482da847b86c91963dbb0d37375e370a503588
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 1%

---

# Revisiones de Adobe Experience Manager Forms{#aem-form-hotfix}

Este artículo enumera las correcciones esenciales implementadas para abordar problemas conocidos, mejorar la estabilidad del sistema y mejorar el rendimiento general de AEM Forms.

>[!NOTE]
>
> Las revisiones están diseñadas para ser acumulativas, e incluyen todas las correcciones anteriores. Al aplicar la revisión más reciente a una versión de, no solo se aborda el problema más reciente, sino que también incorpora todas las correcciones de errores y mejoras anteriores.

## Revisiones para Forms adaptable {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Fecha</strong></td>
    <td><strong>Vínculo de descarga de revisión (vínculo de distribución de software de AEM)</strong></td>
    <td><strong>Problemas solucionados</strong></td>
  </tr>
  <tr>
    <td>Revisión SP23 cargada en SD-</td>
    <td>
    <ul>
    <li><strong>Jboss:</strong></li>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-win-jboss.zip">revisión para el paquete de servicio 6.5.23.0 de AEM en el servidor JEE de Windows para JBoss</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-jboss.tar.gz">revisión para AEM Service Pack 6.5.23.0 en Linux para el servidor JEE de JBoss</a></li>
    <li><strong>Weblogic:</strong></li>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-win-weblogic.zip">revisión para AEM Service Pack 6.5.23.0 en el servidor JEE de Windows para Weblogic</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-weblogic.tar.gz">revisión para AEM Service Pack 6.5.23.0 en Linux para el servidor JEE de Weblogic</a></li>
    <li><strong>Websphere:</strong></li>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-win-websphere.zip">revisión para el paquete de servicio 6.5.23.0 de AEM en el servidor JEE de Windows para Websphere</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-websphere.tar.gz">revisión para AEM Service Pack 6.5.23.0 en Linux para el servidor JEE de Websphere</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>Revisión del SP23 para AEM Forms en JEE</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>26 de marzo de 2025 </br> </br> Para instalar esta corrección, siga las instrucciones <a href="/help/forms/using/mitigating-spring-framework-vulnerabilities-for-aem-forms-on-jee.md"> Mitigación de vulnerabilidades de módulo de primavera para AEM Forms en JEE</a>.</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-win-jboss.tar.gz">Revisión para el paquete de servicio 6.5.22.0 de AEM en el servidor JEE de Windows para JBoss </a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-jboss.tar.gz">Revisión para el paquete de servicio 6.5.22.0 de AEM en Linux para el servidor JEE de JBoss </a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-win-weblogic.tar.gz">Revisión para el paquete de servicio 6.5.22.0 de AEM en el servidor JEE de Windows para Weblogic </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-weblogic.tar.gz">Revisión para el paquete de servicio 6.5.22.0 de AEM en Linux para el servidor JEE de Weblogic</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-win-websphere.tar.gz">Revisión para el paquete de servicio 6.5.22.0 de AEM en el servidor JEE de Windows para Websphere </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-websphere.tar.gz">Revisión para el paquete de servicio 6.5.22.0 de AEM en Linux para el servidor JEE de Websphere</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Mitigación de vulnerabilidades de Spring Framework para AEM Forms en JEE</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>jueves, 10 de julio de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-jboss.zip.zip">Revisión para el paquete de servicio 6.5.21.0 de AEM en el servidor JEE de Windows para JBoss </a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz">Revisión para el paquete de servicio 6.5.21.0 de AEM en Linux para el servidor JEE de JBoss </a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-websphere.zip.zip">Revisión para el paquete de servicio 6.5.21.0 de AEM en el servidor JEE de Windows para Websphere </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-websphere.tar.gz">Revisión para el paquete de servicio 6.5.21.0 de AEM en Linux para el servidor JEE de Websphere</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-weblogic.zip.zip">Revisión para el paquete de servicio 6.5.21.0 de AEM en el servidor JEE de Windows para Weblogic </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-weblogic.tar.gz">Revisión para el paquete de servicio 6.5.21.0 de AEM en Linux para el servidor JEE de Weblogic</a> </li>
     </ul>
     </td>
    <td>
    <ul><li>Cuando un usuario actualiza al paquete de servicio 20 de AEM Forms (6.5.20.0) en el servidor JEE y genera archivos PDF mediante los servicios de salida, los archivos PDF se representan con problemas de accesibilidad. (LC-3922112)</li><li>Los PDF etiquetados generados mediante el servicio de salida en AEM Forms JEE muestran "Advertencia de estructura inadecuada". (LC-3922038)</li><li>Cuando se envía un formulario en AEM Forms JEE, las instancias de un elemento XML repetitivo se eliminan de los datos. (LC-3922017)</li><li>Cuando un usuario en un entorno Linux procesa un formulario adaptable (en JEE) en HTML, no se procesa correctamente. (LC-3921957)</li><li>Cuando un usuario convierte un archivo XTG al formato PostScript mediante el servicio de salida en AEM Forms JEE, se produce el siguiente error: AEM_OUT_001_003: Excepción inesperada: Error de PAExecute: XFA_RENDER_FAILURE. (LC-3921720)</li><li>Después de actualizar al paquete de servicio 18 de AEM Forms (6.5.18.0) en el servidor JEE, cuando un usuario envía un formulario, no puede procesar bloqueos de HTML5 o PDF forms y XMLFM. (LC-3921718)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>sábado, 21 de junio de 2024</td>
     <td>
     <ul>
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Revisión para el paquete de servicio 6.5.21.0 de AEM o el paquete de servicio 6.5.22.0 de AEM Forms en el servidor JEE de JBoss </a> </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Revisión para el paquete de servicio 6.5.21.0 de AEM o el paquete de servicio 6.5.22.0 de AEM Forms en el servidor JEE de Weblogic </a> </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Revisión para el paquete de servicio 6.5.21.0 de AEM o el paquete de servicio 6.5.22.0 de AEM Forms en el servidor JEE de Webshop </a> </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Revisión para el paquete de servicio 6.5.21.0 de AEM o el paquete de servicio 6.5.22.0 de AEM Forms en el servidor OSGi </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> Después de actualizar a AEM Forms Service Pack 6.5.21.0 o AEM Forms Service Pack 6.5.22.0, el servicio PaperCapture no realiza operaciones de OCR (reconocimiento óptico de caracteres) en archivos PDF. Para obtener instrucciones de instalación, consulte el artículo <a href="/help/forms/using/papercapture-service-resolution.md"> solución de problemas</a>.(CQDOC-21680) </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>sábado, 21 de junio de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fccm-ccr-content-10.0.206.zip">Revisión para el paquete de servicio 6.5.21.0 de AEM </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Los borradores de cartas con datos XML se quedan atascados en el estado de carga durante la vista previa. Para obtener instrucciones de descarga e instalación de la revisión, consulte la sección <a href="#install-hotfix"> Descargar e instalar la revisión para el número de borrador de la carta </a>.(FORMS-14521)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>viernes, 16 de mayo de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">Revisión para AEM Service Pack 6.5.20.0 para Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">Revisión para AEM Service Pack 6.5.20.0 para Linux </a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">Revisión para el paquete de servicio 6.5.20.0 de AEM para Apple macOS</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>En un formulario adaptable basado en un XDP con scripts incrustados en casillas de verificación, los scripts no se ejecutan para elementos después de esas casillas de verificación. Hay una revisión disponible para este problema. (FORMS-14244) </li>
     <li> Las filas del widget selector de fechas se truncan al recorrer meses en el widget emergente de los campos con el patrón Editar/Mostrar. Hay una revisión disponible para este problema. (FORMS-13620) </li>
     <li>Los envíos de formularios fallan al intentar utilizar el servicio DOR (documento de registro) en el backend. El mensaje de error encontrado es: "No se pudo completar la acción de envío porque el recurso de formulario no se ha asignado correctamente". (FORMS-13798) </li>
     <li>Cuando se envía un formulario adaptable desde una instancia de publicación de Adobe Experience Manager a un flujo de trabajo de Adobe Experience Manager, el flujo de trabajo no puede guardar los archivos adjuntos.  (FORMS-14209) </li>
     <li> Al instalar el paquete de servicio 20 de AEM 6.5 Forms (paquete de complemento de AEM Forms para SP20), la interfaz de usuario (IU) de AEM Sites muestra una degradación significativa del rendimiento.  (FORMS-13791) </li>
     <li>El servicio de relleno previo falla con una excepción de puntero nulo en las comunicaciones interactivas. (CQDOC-21355)</li>
     <li>Las configuraciones que utilizan el servicio en la nube heredado para Adobe Analytics con autenticación basada en credenciales de usuario no funcionan correctamente, lo que provoca que no se ejecuten las reglas de Analytics. (FORMS-15428)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>martes, 29 de enero de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">Revisión para AEM Service Pack 6.5.19.0 para Windows en el servidor JEE</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>En AEM Forms en el servidor JEE, no se pueden procesar los Forms de HTML5 que utilizan la ruta de contexto. (FORMS-12485, FORMS-12691).</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>martes, 29 de enero de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">Revisión para AEM Service Pack 6.5.18.0 para Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">Revisión para AEM Service Pack 6.5.18.0 para Linux</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">Revisión para AEM Service Pack 6.5.18.0 para Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> El componente Firma manuscrita predeterminado no se puede procesar para una vista previa en un formulario adaptable. (FORMS-12073).</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>martes, 20 de noviembre de 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Revisión para AEM Service Pack 6.5.18.0 para Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Revisión para AEM Service Pack 6.5.18.0 para Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Revisión para AEM Service Pack 6.5.18.0 para Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>La firma en línea deja de funcionar cuando se establece una URL de redireccionamiento en el contenedor de guía de un formulario adaptable. (FORMS-10493)</li>
    <li>Las plantillas de documento de registro (DoR) no se pueden publicar para Forms adaptable localizado. (FORMS-10535)</li>
    <li>La comunicación interactiva con imágenes en línea grandes no se puede abrir en modo de edición. (FORMS-10578)</li>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## Descargar e instalar una revisión {#download-install-hotfix}

Siga estos pasos para descargar e instalar la revisión:

1. Descargar [revisión](#hotfix-for-adaptive-forms) desde el vínculo de distribución de software.
1. Extraiga el archivo de revisión para poder obtener un paquete Experience Manager (.zip) y archivos de paquete (.jar).
1. Cargue e instale el paquete (.zip) mediante [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Abra los paquetes del administrador de configuración `https://server:host/system/console/bundles`, cargue e instale el paquete (.jar). La revisión está instalada.


## Descargar e instalar la revisión para un problema de carta borrador {#install-hotfix}

Para resolver el problema, realice los siguientes pasos:

1. Descargue la [revisión](#hotfix-for-adaptive-forms) del Portal de distribución de software.
2. Cargue e instale el paquete (.zip) utilizando [CRX Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).