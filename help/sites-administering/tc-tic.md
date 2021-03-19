---
title: Configuración del marco de integración de traducción
seo-title: Configuración del marco de integración de traducción
description: Obtenga información sobre cómo configurar el marco de integración de traducción.
seo-description: Obtenga información sobre cómo configurar el marco de integración de traducción.
uuid: 5ecfe154-732f-4a13-96f8-92f55023c54d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 200f51ab-f9bf-4989-91af-c3904fc673e5
feature: Copiar idioma
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 2%

---


# Configuración del marco de integración de traducción{#configuring-the-translation-integration-framework}

El marco de integración de traducción se integra con los servicios de traducción de terceros para organizar la traducción de AEM contenido.

* Conéctese a su proveedor de servicios de traducción.
* Cree una configuración del marco de integración de traducción.
* Asocie las configuraciones de nube con sus páginas.

Para obtener una descripción general de las funciones de traducción de contenido de AEM, consulte [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md).

## Conexión a un proveedor de servicios de traducción {#connecting-to-a-translation-service-provider}

Cree una configuración de nube que se conecte AEM con su proveedor de servicios de traducción. AEM incluye la capacidad de conectarse a Microsoft Translator de forma predeterminada.
Los siguientes proveedores de traducción proporcionan una implementación de la nueva API para los proyectos de traducción. Vínculos para obtener más información sobre la integración:

* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html)  (Adobe Exchange Premier Partner)
* [Tecnologías para tableta de arcilla](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Palabras clave](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [CrossLang NV](https://exchange.adobe.com/experiencecloud.details.90049.crosslang-xtm-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [Smartling](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [SDL](https://exchange.adobe.com/experiencecloud.details.100110.sdl-translation-management.html)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)
* [Altlang](https://exchange.adobe.com/experiencecloud.details.90222.altlang.html)
* Microsoft (Microsoft Translator está preinstalado en AEM)

>[!NOTE]
>
>Para encontrar la lista más reciente de proveedores de traducción automática y humana, eche un vistazo a estas páginas:
>
>
>* [AEM Traducción humana](https://www.adobe.com/go/aem-human-translation-connectors)
>* [AEM traducción automática](https://www.adobe.com/go/aem-machine-translation-connectors)

>



Después de instalar un paquete de conector, puede crear una configuración de nube para el conector. Normalmente, debe proporcionar sus credenciales para autenticarse con el servicio de traducción. Para obtener información sobre cómo agregar una configuración de nube para el conector de Microsoft Translator, consulte [Integración con Microsoft Translator](/help/sites-administering/tc-msconf.md).

Si es necesario, puede crear varias configuraciones de nube para el mismo conector. Por ejemplo, cree una configuración para cada una de las cuentas o proyectos que tenga con el mismo proveedor.

Después de configurar una conexión, puede crear la configuración del marco de integración de traducción que la utiliza.

## Creación de una configuración de integración de traducción {#creating-a-translation-integration-configuration}

Cree una configuración del marco de integración de traducción para especificar cómo traducir el contenido. La configuración incluye la siguiente información:

* Qué proveedor de servicios de traducción utilizar.
* Indica si se realizará una traducción humana o automática.
* Indica si se deben traducir otros contenidos asociados a una página o un recurso, como las etiquetas.

Después de crear una configuración de marco, asocia la configuración de nube con las páginas que desea traducir según la configuración. Cuando se inicia el proceso de traducción, el flujo de trabajo de traducción se ejecuta según la configuración del marco asociada.

Cuando diferentes secciones del sitio web tengan diferentes requisitos de traducción, cree varias configuraciones de marco según corresponda. Por ejemplo, un sitio web multilingüe incluye copias en inglés, español y japonés. El propietario del sitio utiliza dos proveedores de servicios de traducción diferentes para las traducciones al español y al japonés. Por lo tanto, se configuran dos configuraciones del marco. Cada configuración utiliza un proveedor de servicios de traducción diferente.

Después de configurar un marco de integración de traducción, puede [asociarlo a las páginas](/help/sites-administering/tc-prep.md) que lo utilizan.

**Nota:** Para obtener una descripción general de las funciones de traducción de contenido de AEM, consulte  [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md).

Una sola configuración del marco controla cómo traducir contenido de página, contenido de la comunidad y recursos.
![chlimage_1-386](assets/translation-config-65.jpg)

### Propiedades de configuración de sitios {#sites-configuration-properties}

Las propiedades Sitios controlan cómo se realiza la traducción del contenido de la página.

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>Flujo de trabajo de traducción</td>
   <td><p>Seleccione el método de traducción que realiza el marco para el contenido del sitio:</p>
    <ul>
     <li>Traducción automática: El proveedor de traducción realiza la traducción mediante traducción automática en tiempo real.</li>
     <li>Traducción humana: El contenido se envía al proveedor de traducción para que lo traduzcan los traductores. </li>
     <li>No traducir: El contenido no se envía para su traducción. Esto sirve para omitir ciertas ramas de contenido que no se traducirían, pero que podrían actualizarse con el contenido más reciente.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Proveedor de traducciones</td>
   <td>Seleccione el proveedor de traducción para realizar la traducción. Cuando se instala su conector correspondiente, aparece un proveedor en la lista.</td>
  </tr>
  <tr>
   <td>Categoría de contenido</td>
   <td>(Solo traducción automática) Una categoría que describe el contenido que está traduciendo. La categoría puede afectar a la elección de terminología y frases al traducir contenido.</td>
  </tr>
  <tr>
   <td>Traducir etiquetas</td>
   <td>Seleccione para traducir las etiquetas asociadas a la página.</td>
  </tr>
  <tr>
   <td>Traducir recursos de la página</td>
   <td><p>Seleccione cómo traducir recursos que se agregan a los componentes del sistema de archivos o a los que se hace referencia desde Assets:</p>
    <ul>
     <li>No traducir: Los recursos de página no se traducen.</li>
     <li>Uso del flujo de trabajo de traducción de sitios: Los recursos se gestionan según las propiedades de configuración de la ficha Sitios .</li>
     <li>Uso del flujo de trabajo de traducción de Assets: Los recursos se gestionan según la configuración de las propiedades de la pestaña Recursos .</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Ejecución automática de la traducción</td>
   <td>Seleccione para ejecutar los trabajos de traducción automáticamente después de crear los proyectos de traducción. No tiene la oportunidad de revisar y ampliar el ámbito del trabajo de traducción cuando selecciona esta opción.</td>
  </tr>
 </tbody>
</table>

### Propiedades de configuración de comunidades {#communities-configuration-properties}

Las propiedades de las comunidades controlan cómo se realiza la traducción del contenido generado por el usuario. La traducción del contenido generado por el usuario siempre utiliza la traducción automática. Para obtener más información, consulte [Traducción del contenido generado por el usuario](/help/communities/translate-ugc.md).

| Propiedad | Descripción |
|---|---|
| Proveedor de traducciones | Seleccione el proveedor de traducción para realizar la traducción. El proveedor para el que se crean configuraciones de nube aparece en la lista. |
| Categoría de contenido | Categoría que describe el contenido que está traduciendo. La categoría puede afectar a la elección de terminología y frases al traducir contenido. |
| Elija Una Configuración Regional Para Usar Como Tienda Compartida Global | (Opcional) Al seleccionar una configuración regional para almacenar UGC, las publicaciones de todas las copias de idiomas aparecerán en una conversación global. Por convención, elija la configuración regional para el [idioma base](/help/communities/sites-console.md#translation) del sitio web. Si elige No Common Store , se deshabilitará la traducción global. De forma predeterminada, la traducción global está desactivada. |

### Propiedades de configuración de recursos {#assets-configuration-properties}

Las propiedades de recursos controlan cómo configurar los recursos. Para obtener más información sobre la traducción de recursos, consulte [Creación de copias de idioma para recursos](/help/assets/translation-projects.md).

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>Flujo de trabajo de traducción</td>
   <td><p>Seleccione el tipo de traducción que realiza el marco para los recursos:</p>
    <ul>
     <li>Traducción automática: El proveedor de traducción realiza la traducción inmediatamente mediante traducción automática.</li>
     <li>Traducción humana: El contenido se envía automáticamente al proveedor de traducción para que se traduzca manualmente. </li>
     <li>No traducir: Los recursos no se envían para su traducción.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Proveedor de traducciones</td>
   <td>Seleccione el proveedor de traducción para realizar la traducción. Cuando se instala su conector correspondiente, aparece un proveedor en la lista.</td>
  </tr>
  <tr>
   <td>Categoría de contenido</td>
   <td>(Solo traducción automática) Una categoría que describe el contenido que está traduciendo. La categoría puede afectar a la elección de terminología y frases al traducir contenido.</td>
  </tr>
  <tr>
   <td>Traducir recursos</td>
   <td>Seleccione esta opción para incluir recursos en el proyecto de traducción. </td>
  </tr>
  <tr>
   <td>Traducir metadatos</td>
   <td>Seleccione para traducir metadatos de recursos.</td>
  </tr>
  <tr>
   <td>Traducir etiquetas</td>
   <td>Seleccione para traducir las etiquetas asociadas al recurso.</td>
  </tr>
  <tr>
   <td>Ejecución automática de la traducción</td>
   <td>Seleccione para ejecutar los trabajos de traducción automáticamente después de crear los proyectos de traducción. No tiene la oportunidad de revisar o ampliar el ámbito del trabajo de traducción cuando selecciona esta opción.</td>
  </tr>
 </tbody>
</table>

1. En la barra lateral, pulse o haga clic en Herramientas > Operaciones > Nube > Cloud Services.
1. En el área Integración de traducción , si se ha creado alguna configuración determina qué vínculo aparece:

   * Si no se han creado configuraciones, toque o haga clic en Configurar ahora.
   * Si ya existen configuraciones, toque o haga clic en Mostrar configuraciones y, a continuación, toque o haga clic en el vínculo + que aparece junto a Configuraciones disponibles.

1. Escriba un nombre para la configuración y, a continuación, toque o haga clic en Crear.
1. Configure las propiedades en la ficha Sitios, Comunidades y Recursos y, a continuación, toque o haga clic en Aceptar.

## Configuración de páginas para traducción {#configuring-pages-for-translation}

Para configurar la traducción de las páginas de origen a otros idiomas, asocie las páginas con las siguientes configuraciones de nube:

* La configuración de nube que se conecta AEM con su proveedor de traducción.
* Marco de integración de traducción que configura los detalles de la traducción.

Tenga en cuenta que la configuración de nube del marco de integración de traducción identifica la configuración de nube que se utilizará para conectarse al proveedor de servicios. Cuando asocia una página de origen con una configuración de nube de marco, la página debe asociarse a la configuración de nube del proveedor de servicios que utiliza la configuración de nube de marco.

Cuando asocia una página con una configuración de nube, los descendientes de la página heredan la asociación. Por ejemplo, si asocia la página /content/geometrixx/en/products con un marco de integración de traducción, la página Productos y todas las páginas debajo se traducen según el marco.

Si es necesario, puede anular la asociación en una página descendiente. Por ejemplo, el contenido de un sitio web se trata principalmente de ropa. Sin embargo, una rama de páginas describe la empresa. La página raíz del sitio está asociada con un Marco de integración de traducción que especifica la traducción automática mediante la categoría Ropa. La rama que describe la empresa utiliza un marco que realiza la traducción automática mediante la categoría General .

Además, para cualquier comunidad [SCF components](/help/communities/scf.md) en las páginas, el contenido generado por el usuario (UGC) incluirá la capacidad de los usuarios de traducir contenido. Para obtener más información, consulte [Traducción del contenido generado por el usuario](/help/communities/translate-ugc.md).

### Asociación de una página con un proveedor de traducción {#associating-a-page-with-a-translation-provider}

Asocie una página al proveedor de traducción que esté utilizando para traducir la página y las páginas descendientes.

1. En la consola Sitios , seleccione la página que desea configurar y toque o haga clic en Ver propiedades.
1. Toque o haga clic en Editar y, a continuación, toque o haga clic en la pestaña Cloud Services .
1. Toque o haga clic en Agregar configuración > Integración de traducción.
1. Seleccione el proveedor de traducción que desea utilizar y, a continuación, toque o haga clic en Finalizado.

### Asociación de páginas con un marco de integración de traducción {#associating-pages-with-a-translation-integration-framework}

Asocie una página al marco de integración de traducción que define cómo desea realizar la traducción de la página y de las páginas descendientes.

1. En la consola Sitios , seleccione la página que desea configurar y toque o haga clic en Ver propiedades.
1. Toque o haga clic en Editar y, a continuación, toque o haga clic en la pestaña Cloud Services .
1. Toque o haga clic en Agregar configuración > Integración de traducción.
1. Seleccione el marco de integración de traducción que desea utilizar y, a continuación, toque o haga clic en Finalizado.

