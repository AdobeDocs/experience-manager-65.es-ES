---
title: COMMERCE CLOUD SAP
seo-title: COMMERCE CLOUD SAP
description: Conozca cómo implementar el comercio electrónico con el Commerce Cloud de SAP.
seo-description: Conozca cómo implementar el comercio electrónico con el Commerce Cloud de SAP.
uuid: a16ae42b-9c33-4da8-a130-52b72a779ec7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 44dfa10f-497e-473f-95d4-8dccae7ebf8e
pagetitle: Deploying eCommerce with SAP Commerce Cloud
translation-type: tm+mt
source-git-commit: 328e13eb2ce034b0b1ec7e5e0fb184de9435d1bc
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---


# COMMERCE CLOUD SAP{#sap-commerce-cloud}

>[!NOTE]
>
>Esta página contiene enlaces al sitio web de hybris. Para determinadas páginas necesitará una cuenta para iniciar sesión.

## Implementación de eCommerce con el Commerce Cloud SAP {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>Los siguientes procedimientos utilizan el siguiente catálogo de demostración para ilustrar la implementación:
>
>`Geometrixx Outdoors Site English (US)`

La implementación de los [paquetes de comercio electrónico necesarios](#packages-needed-for-ecommerce-with-hybris) proporcionará toda la funcionalidad del marco de comercio electrónico, junto con una implementación de referencia de la funcionalidad de comercio electrónico, según se proporciona con una implementación de híbris (incluido un catálogo de demostración)

Esta opción está disponible en la rama en inglés (EE.UU.) ( `/content/geometrixx-outdoors/en_US`) del sitio de Geometrixx Outdoors:

* [Información](#productinformationwithcolorvariants)  del producto (con variantes de color cuando proceda)

* [Información general sobre el contenido del carro de compras](#shoppingcartcontentoverview)
* [Inicio de sesión de cliente ](#customersignup) actualizado e inicio de sesión de  [cliente](#customersignin)

* [Acceso a la consola de administración de híbris](#accesstothehybrismanagementconsole)

### Requisitos técnicos: servidor híbrido {#technical-requirements-hybris-server}

La extensión híbris del marco de integración de comercio electrónico se ha actualizado para admitir Hybris 5 (como opción predeterminada), manteniendo al mismo tiempo la compatibilidad con [Hybris 4](/help/sites-developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* Admite las versiones 18.11 y posteriores.
>* Necesitará Java 7 para ejecutar el servidor [hybris 5.](https://www.hybris.com/en/architecture-technology)
>* El complemento de híbris, el [Acelerador de telecomunicaciones](https://www.hybris.com/en/products/telecommunication), no es compatible con la extensión de AEM.

>



### Paquetes necesarios para el comercio electrónico con híbris {#packages-needed-for-ecommerce-with-hybris}

Para instalar la funcionalidad de comercio electrónico necesita:

* Su servidor híbrido
* AEM marco de comercio electrónico:

   * esto forma parte de una instalación AEM estándar

* Paquete todo AEM:

   * `cq-geometrixx-all-pkg`

* AEM paquetes de contenido de híbris:

   * `cq-hybris-content-6.3.2`
   * implementación de API específica para híbris
   * `cq-geometrixx-hybris-content-6.3.2`
   * una implementación de referencia para ilustrar el uso de hibris ( `geometrixx-outdoors/en_US`)

### Instalación del comercio electrónico con híbris {#installation-of-ecommerce-with-hybris}

Para instalar una configuración completa (mediante el catálogo de demostración, Geometrixx Outdoors), los pasos básicos son:

1. [Instale AEM](/help/sites-deploying/deploy.md).
1. Instalar el paquete Geometrixx-all

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Instale los paquetes de contenido de demostración con el [administrador de paquetes](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Descargue y cree su servidor](#download-and-build-your-hybris-server) híbrido.
1. Cree el catálogo en el motor de comercio electrónico:

   1. [Configure la Tienda](#setup-the-geometrixx-outdoors-store) al aire libre de Geometrixx.

1. [](/help/sites-authoring/qg-page-authoring.md) Autorice las páginas complementarias que necesite en AEM.

>[!CAUTION]
>
>El uso del servidor hybris requiere una licencia de híbris independiente.

>[!NOTE]
>
>Para desarrolladores [la documentación de API](/help/sites-developing/ecommerce.md#api-documentation) también está disponible para su descarga.

### Descargue y cree su servidor híbrido {#download-and-build-your-hybris-server}

Los pasos de este procedimiento descargarán y generarán el servidor híbrido. También hará las configuraciones iniciales necesarias para las conexiones entre hybris y cq. La extensión se podrá utilizar con la configuración predeterminada.

>[!CAUTION]
>
>No se admiten versiones de híbridos anteriores a la 5.5.1.

>[!NOTE]
>
>Para completar esto, necesitará [Groovy](https://groovy-lang.org/) instalado en su sistema.

1. Descargue la distribución **hybris Commerce Suite** del sitio de descarga de híbris.

   >[!CAUTION]
   >
   >Necesitarás una cuenta (de hybris) para acceder a ella.

1. Descomprima el archivo de distribución en la ubicación requerida (denominada &lt;hybris-root-directory>).
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

1. Descargue los siguientes archivos en la carpeta raíz de la distribución de híbridos extraídos.

   ```
       <hybris-root-directory>
   ```


   [Obtener archivo](assets/setup.groovy)

   >[!NOTE]
   >
   >Para hybris 5.6.0 y posterior, utilice el siguiente setup.groovy.

   5.6.0 y posterior

   [Obtener archivo](assets/setup-1.groovy)

1. Desde la línea de comandos, ejecute lo siguiente para:

   * actualizar la configuración del servidor híbris (según lo requiera la extensión)
   * vuelva a compilar el servidor híbris con la configuración modificada
   * inicio del servidor

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >Según el sistema, varios de estos pasos pueden tardar varios minutos en completarse.

1. En el explorador, navegue a la **consola de administración de híbris** en:

   [http://localhost:9002](http://localhost:9002)

1. Haga clic en **Inicializar** y confirme la acción de inicialización (ya que eliminará los datos existentes).

   El progreso se mostrará en la consola, con `FINISHED` indicando la finalización.

   >[!NOTE]
   >
   >En función del sistema, esto puede tardar varios minutos en completarse.

### Configurar el almacén de Geometrixx Outdoors {#setup-the-geometrixx-outdoors-store}

Este procedimiento cargará y configurará el almacén de demostración: Geometrixx en línea.

1. Inicio tu hibris. Desde la línea de comandos, ejecute lo siguiente:

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. En el explorador, navegue a la **consola de administración de híbris** en:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   Utilice estas credenciales:
   * username: admin
   * password: nimda

1. Desde la navegación de la barra lateral, explora **System** y **Tools**. A continuación, seleccione **Importar** para abrir el **Asistente: Importación de CSV**.
1. En la ficha **Configuración**, **Cargar** el siguiente **archivo de importación**:

   [Obtener archivo](assets/geometrixx-outdoors-export.csv)

1. Establezca la **configuración regional** en:

   `en_US - English (United States)`

1. Abra la ficha **Recursos**.
1. **** Cargue el siguiente  **código postal**:

   [Obtener archivo](assets/geometrixx-outdoors-images.zip)

1. Haga clic en **Inicio** para importar los archivos especificados. La ficha **Resultado** mostrará cualquier entrada de registro.

1. Haga clic en **Listo** para cerrar la ventana de importación.

1. En la barra lateral, seleccione **Sistema**, luego **Herramientas**, luego **Importar**.

1. **** Cargue el siguiente archivo **de** importación:

   [Obtener archivo](assets/base-store.csv)

   Para hybris 5.7, utilice lo siguiente:

   [Obtener archivo](assets/base-store-5_7.csv)

1. Establezca la **configuración regional** en:

   `en_US - English (United States)`

1. Haga clic en **Inicio** para importar los archivos especificados. La ficha **Resultado** mostrará cualquier entrada de registro.

1. Haga clic en **Listo** para cerrar la ventana de importación.

1. Ahora puede utilizar la cabina de productos para la vista de los catálogos y productos importados:

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)

