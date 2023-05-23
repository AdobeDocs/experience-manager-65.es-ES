---
title: Implementar eCommerce con el Commerce Cloud de SAP
description: Aprenda a implementar eCommerce con SAP Commerce Cloud.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 2%

---

# COMMERCE CLOUD SAP{#sap-commerce-cloud}

>[!NOTE]
>
>Esta página contiene enlaces al sitio web de hybris. Para ciertas páginas necesitará una cuenta para iniciar sesión.

## Implementación de eCommerce con SAP Commerce Cloud {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>Los siguientes procedimientos utilizan el siguiente catálogo de demostración para ilustrar la implementación:
>
>`Geometrixx Outdoors Site English (US)`

Implementación de [Paquetes de comercio electrónico necesarios](#packages-needed-for-ecommerce-with-hybris) proporcionará la funcionalidad completa del marco de comercio electrónico, junto con una implementación de referencia de la funcionalidad de comercio electrónico, tal como se proporciona con una implementación de hybris (incluido un catálogo de demostración)

Esta opción está disponible en la rama en inglés (EE.UU.) ( `/content/geometrixx-outdoors/en_US`) del sitio de Geometrixx Outdoors:

* [Información del producto](#productinformationwithcolorvariants) (con variantes de color cuando corresponda)

* [Resumen del contenido del carro de compras](#shoppingcartcontentoverview)
* [Registro de cliente](#customersignup) y [Inicio de sesión de cliente](#customersignin)

* [Acceso a la consola de administración de hybris](#accesstothehybrismanagementconsole)

### Requisitos técnicos - hybris Server {#technical-requirements-hybris-server}

La extensión hybris del marco de integración de comercio electrónico se ha actualizado para admitir Hybris 5 (de forma predeterminada), aunque se mantiene la compatibilidad con versiones anteriores de [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* Compatible con las versiones 18.11 y posteriores.
>* Necesitará Java 7 para ejecutar el [servidor hybris 5.](https://www.hybris.com/en/architecture-technology)
>* El complemento hybris, el [Acelerador de telecomunicaciones](https://www.hybris.com/en/products/telecommunication)AEM , no es compatible con la extensión de.
>


### Paquetes necesarios para el comercio electrónico con hybris {#packages-needed-for-ecommerce-with-hybris}

Para instalar la funcionalidad de comercio electrónico necesita:

* Su servidor hybris
* AEM Marco de eCommerce de:

   * AEM esto forma parte de una instalación estándar de la

* AEM Paquete de todo el Geometrixx:

   * `cq-geometrixx-all-pkg`

* AEM paquetes de contenido de hybris:

   * `cq-hybris-content-6.3.2`
   * implementación de API específica de hybris
   * `cq-geometrixx-hybris-content-6.3.2`
   * una implementación de referencia para ilustrar el uso de hybris ( `geometrixx-outdoors/en_US`)

### Instalación de comercio electrónico con hybris {#installation-of-ecommerce-with-hybris}

Para instalar una configuración completa (con el catálogo de demostración, Geometrixx Outdoors), los pasos básicos son los siguientes:

1. [AEM Instalación de](/help/sites-deploying/deploy.md).
1. Instalación del paquete Geometrixx-all

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Instale los paquetes de contenido de demostración con la variable [administrador de paquetes](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Descargue y cree su servidor hybris](#download-and-build-your-hybris-server).
1. Construya su catálogo en su motor de comercio electrónico:

   1. [Configurar la tienda de Geometrixx al aire libre](#setup-the-geometrixx-outdoors-store).

1. [Autor](/help/sites-authoring/qg-page-authoring.md) AEM cualquier página complementaria que necesite en la creación de la página de.

>[!CAUTION]
>
>El uso del servidor hybris requiere una licencia hybris independiente.

>[!NOTE]
>
>Para desarrolladores [Documentación de API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) también está disponible para descargar.

### Descargue y cree su servidor hybris {#download-and-build-your-hybris-server}

Los pasos de este procedimiento descargarán y crearán el servidor hybris. También realizará las configuraciones iniciales requeridas para las conexiones entre hybris y cq. La extensión se puede utilizar con la configuración predeterminada.

>[!CAUTION]
>
>No se admiten las versiones de Hybris anteriores a la 5.5.1.

>[!NOTE]
>
>Para completar esto, necesitará lo siguiente [Fantástico](https://groovy-lang.org/) instalado en el sistema.

1. Descargue la **hybris Commerce Suite** distribución desde el sitio de descarga de hybris.

   >[!CAUTION]
   >
   >Necesitará una cuenta (de hybris) para acceder a esto.

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
   >Prensa `Return` cuando sea necesario.

1. Descargue los siguientes archivos en la carpeta raíz de la distribución de hybris extraída,

   ```
       <hybris-root-directory>
   ```


[Obtener archivo](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >Para hybris 5.6.0 y versiones posteriores, utilice el siguiente setup.groovy.

   5.6.0 y versiones posteriores

[Obtener archivo](/help/sites-deploying/assets/setup-1.groovy)

1. Desde la línea de comandos, ejecute lo siguiente en:

   * actualice la configuración del servidor hybris (según requiera la extensión)
   * reconstruya el servidor hybris con la configuración modificada
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

1. En el explorador, vaya a **consola de administración de hybris** a las:

   [http://localhost:9002](http://localhost:9002)

1. Clic **Inicializar** y, a continuación, confirme la acción de inicialización (ya que eliminará los datos existentes).

   El progreso se mostrará en la consola, con `FINISHED` que indica finalización.

   >[!NOTE]
   >
   >En función del sistema, esta operación puede tardar varios minutos en completarse.

### Configuración del almacén de Geometrixx Outdoors {#setup-the-geometrixx-outdoors-store}

Geometrixx Este procedimiento cargará y configurará el almacén de demostración: en línea.

1. Inicie la instancia de hybris. Desde la línea de comandos, ejecute lo siguiente:

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. En el explorador, vaya a **consola de administración de hybris** a las:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   Utilice estas credenciales:
   * nombre de usuario: admin
   * contraseña: nimda

1. En la barra lateral de navegación, expanda **Sistema** y **Herramientas**. A continuación seleccione **Importar** para abrir **Asistente: importación de CSV** ventana.
1. En el **Configuración** pestaña, **Cargar** lo siguiente **Importar archivo**:

[Obtener archivo](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. Configure las variables **Configuración regional** hasta:

   `en_US - English (United States)`

1. Abra el **Recursos** pestaña.
1. **Cargar** lo siguiente **Media-Zip**:

[Obtener archivo](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. Clic **Inicio** para importar los archivos especificados. El **Resultado** La pestaña muestra todas las entradas de registro.

1. Clic **Listo** para cerrar la ventana de importación.

1. En la barra lateral, seleccione **Sistema**, entonces **Herramientas**, entonces **Importar**.

1. **Cargar** lo siguiente **Importar archivo**:

[Obtener archivo](/help/sites-deploying/assets/base-store.csv)

   Para hybris 5.7, utilice lo siguiente:

[Obtener archivo](/help/sites-deploying/assets/base-store-5_7.csv)

1. Configure las variables **Configuración regional** hasta:

   `en_US - English (United States)`

1. Clic **Inicio** para importar los archivos especificados. El **Resultado** La pestaña muestra todas las entradas de registro.

1. Clic **Listo** para cerrar la ventana de importación.

1. Ahora puede utilizar la cabina de productos para ver los catálogos y los productos importados:

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
