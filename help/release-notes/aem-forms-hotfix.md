---
title: Revisiones para AEM Forms
description: Proporciona información sobre cómo descargar e instalar una revisión para AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
source-git-commit: 0aa929021aa724e4ec18d49fea26f8c0b0538bdc
workflow-type: tm+mt
source-wordcount: '322'
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
    <td><strong>AEM Vínculo de descarga de revisión (vínculo de distribución de software de)</strong></td>
    <td><strong>Problemas solucionados</strong></td>
  </tr>
  <tr>
    <td>martes, 29 de enero de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">AEM Revisión para el paquete de servicio 6.5.19.0 de para Windows en el servidor JEE</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>En AEM Forms en el servidor JEE, no se puede procesar el Forms de HTML5 que utiliza la ruta de contexto. (FORMS-12485, FORMS-12691).</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>martes, 29 de enero de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">AEM Revisión para el paquete de servicio 6.5.18.0 de para Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">AEM Revisión para el paquete de servicio 6.5.18.0 de para Linux</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">AEM Revisión para el paquete de servicio 6.5.18.0 de para Apple macOS</a></li>
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
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">AEM Revisión para el paquete de servicio 6.5.18.0 de para Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">AEM Revisión para el paquete de servicio 6.5.18.0 de para Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">AEM Revisión para el paquete de servicio 6.5.18.0 de para Apple macOS</a></li>
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

1. Descargar [Revisión](#hotfix-for-adaptive-forms) desde el vínculo Distribución de software.
1. Extraiga el archivo de revisión para poder obtener un paquete de Experience Manager (.zip) y archivos de paquete (.jar).
1. Cargue e instale el paquete (.zip) mediante el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Abra los paquetes del administrador de configuración `https://server:host/system/console/bundles`, cargue e instale el paquete (.jar). La revisión está instalada.
