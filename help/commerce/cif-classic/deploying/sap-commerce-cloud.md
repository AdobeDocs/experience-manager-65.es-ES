---
title: Commerce Cloud SAP
seo-title: Commerce Cloud SAP
description: Aprenda a implementar eCommerce con el Commerce Cloud SAP.
seo-description: Aprenda a implementar eCommerce con el Commerce Cloud SAP.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---

# Commerce Cloud SAP{#sap-commerce-cloud}

>[!NOTE]
>
>Esta página contiene enlaces al sitio web de hybris. Para determinadas páginas necesitará una cuenta para iniciar sesión.

## Implementar eCommerce con el Commerce Cloud SAP {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>Los siguientes procedimientos utilizan el siguiente catálogo de demostración para ilustrar la implementación:
>
>`Geometrixx Outdoors Site English (US)`

La implementación de los [paquetes de comercio electrónico necesarios](#packages-needed-for-ecommerce-with-hybris) proporcionará la funcionalidad completa del marco de comercio electrónico, junto con una implementación de referencia de la funcionalidad de comercio electrónico que se proporciona con una implementación de híbrido (incluido un catálogo de demostración)

Esta opción está disponible en la rama en inglés (EE. UU.) ( `/content/geometrixx-outdoors/en_US`) del sitio de Geometrixx Outdoors:

* [Información del producto](#productinformationwithcolorvariants)  (con variantes de color cuando corresponda)

* [Resumen del contenido del carro de compras](#shoppingcartcontentoverview)
* [Inicio de sesión de cliente ](#customersignup) y  [inicio de sesión de cliente](#customersignin)

* [Acceso a la consola de administración de híbridos](#accesstothehybrismanagementconsole)

### Requisitos técnicos: servidor híbrido {#technical-requirements-hybris-server}

La extensión híbris del eCommerce Integration Framework se ha actualizado para admitir Hybris 5 (como predeterminado), manteniendo al mismo tiempo la compatibilidad con [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* Admite las versiones 18.11 y posteriores.
>* Necesitará Java 7 para ejecutar el servidor [hybris 5.](https://www.hybris.com/en/architecture-technology)
>* El complemento híbris, el [Acelerador de telecomunicaciones](https://www.hybris.com/en/products/telecommunication), no es compatible con la extensión AEM.

>



### Paquetes necesarios para el comercio electrónico con híbridos {#packages-needed-for-ecommerce-with-hybris}

Para instalar la funcionalidad de comercio electrónico necesita:

* Su servidor híbrido
* AEM marco de comercio electrónico:

   * esto forma parte de una instalación AEM estándar

* AEM paquete todo:

   * `cq-geometrixx-all-pkg`

* AEM paquetes de contenido híbrido:

   * `cq-hybris-content-6.3.2`
   * implementación de API específica de híbrido
   * `cq-geometrixx-hybris-content-6.3.2`
   * una implementación de referencia para ilustrar el uso de hybris ( `geometrixx-outdoors/en_US`)

### Instalación de comercio electrónico con híbridos {#installation-of-ecommerce-with-hybris}

Para instalar una configuración completa (con el catálogo de Geometrixx Outdoors de demostración), los pasos básicos son:

1. [Instalar AEM](/help/sites-deploying/deploy.md).
1. Instalación del paquete Geometrixx-todo

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Instale los paquetes de contenido de demostración utilizando el [administrador de paquetes](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Descargue y cree su servidor híbrido](#download-and-build-your-hybris-server).
1. Cree su catálogo en el motor de comercio electrónico:

   1. [Configure la Tienda al aire libre de Geometrixx](#setup-the-geometrixx-outdoors-store).

1. [](/help/sites-authoring/qg-page-authoring.md) Autorice las páginas adicionales que necesite en AEM.

>[!CAUTION]
>
>El uso del servidor hybris requiere una licencia de híbris independiente.

>[!NOTE]
>
>Para los desarrolladores [documentación de API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) también está disponible para su descarga.

### Descargue y cree su servidor híbrido {#download-and-build-your-hybris-server}

Los pasos de este procedimiento descargarán y construirán el servidor híbrido. También hará las configuraciones iniciales necesarias para las conexiones entre hybris y cq. La extensión se puede utilizar con la configuración predeterminada.

>[!CAUTION]
>
>Las versiones anteriores a la 5.5.1 de Hybris no son compatibles.

>[!NOTE]
>
>Para completar esto, necesitará [Groovy](https://groovy-lang.org/) instalado en su sistema.

1. Descargue la distribución **hybris Commerce Suite** del sitio de descarga de hybris.

   >[!CAUTION]
   >
   >Necesitará una cuenta (de hybris) para acceder a esta.

1. Descomprima el archivo de distribución a la ubicación requerida (denominada &lt;hybris-root-directory>).
1. Desde la línea de comandos, ejecute lo siguiente:

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   >Al ejecutar:
   >
   >`ant clean all`
   >
   >Pulse `Return` cuando sea necesario.

1. Descargue los siguientes archivos a la carpeta raíz de su distribución de híbridos extraída,

   ```
       <hybris-root-directory>
   ```


   [Obtener archivo](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >Para hybris 5.6.0 y versiones posteriores, utilice el siguiente setup.groovy.

   5.6.0 y posterior

   [Obtener archivo](/help/sites-deploying/assets/setup-1.groovy)

1. Desde la línea de comandos, ejecute lo siguiente para:

   * actualizar la configuración del servidor hybris (como requiere la extensión)
   * reconstruir el servidor hybris con la configuración modificada
   * iniciar el servidor

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >Según el sistema, varios de estos pasos pueden tardar varios minutos en completarse.

1. En el explorador, vaya a la **consola de administración de híbridos** en:

   [http://localhost:9002](http://localhost:9002)

1. Haga clic en **Inicializar** y confirme la acción de inicialización (ya que eliminará los datos existentes).

   El progreso se mostrará en la consola, con `FINISHED` indicando que se ha completado.

   >[!NOTE]
   >
   >En función del sistema, esto puede tardar varios minutos en completarse.

### Configuración del almacén de Geometrixx Outdoors {#setup-the-geometrixx-outdoors-store}

Este procedimiento cargará y configurará el almacén de demostración: Geometrixx en línea.

1. Inicie su instancia de hybris. Desde la línea de comandos, ejecute lo siguiente:

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. En el explorador, vaya a la **consola de administración de híbridos** en:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   Utilice estas credenciales:
   * nombre de usuario: admin
   * contraseña: nimda

1. Desde la navegación de la barra lateral, expanda **System** y **Tools**. A continuación, seleccione **Import** para abrir el **Asistente: Importación de CSV**.
1. En la pestaña **Configuration**, **Upload**, el siguiente **Import file**:

   [Obtener archivo](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. Establezca la **Configuración regional** en:

   `en_US - English (United States)`

1. Abra la pestaña **Resources**.
1. **** Cargue el siguiente  **código postal**:

   [Obtener archivo](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. Haga clic en **Start** para importar los archivos especificados. La pestaña **Result** mostrará las entradas de registro.

1. Haga clic en **Listo** para cerrar la ventana de importación.

1. En la barra lateral, seleccione **Sistema**, luego **Herramientas** y, a continuación, **Importar**.

1. **** Cargue el siguiente archivo  **de importación**:

   [Obtener archivo](/help/sites-deploying/assets/base-store.csv)

   Para hybris 5.7, utilice lo siguiente:

   [Obtener archivo](/help/sites-deploying/assets/base-store-5_7.csv)

1. Establezca la **Configuración regional** en:

   `en_US - English (United States)`

1. Haga clic en **Start** para importar los archivos especificados. La pestaña **Result** mostrará las entradas de registro.

1. Haga clic en **Listo** para cerrar la ventana de importación.

1. Ahora puede utilizar la cabina de productos para ver los catálogos y productos importados:

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
