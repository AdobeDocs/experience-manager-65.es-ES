---
title: Integración con Livefyre
seo-title: Integrating with Livefyre
description: AEM Aprenda a integrar las capacidades de gestión de contenido líderes en el sector de Livefyre con su instancia de 6.5, lo que le permite publicar contenido de valor generado por el usuario (UGC) desde las redes sociales en su sitio en cuestión de minutos.
seo-description: Learn how to integrate and use Livefyre with AEM 6.5.
uuid: c355705d-6e0f-4a33-aa1f-d2d1c818aac0
contentOwner: ind14750
content-type: reference
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: bb3fcb53-b8c3-4b1d-9125-4715f34ceb0b
exl-id: 6327b571-4c7f-4a5e-ba93-45d0a064aa1f
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 6%

---

# Integración con Livefyre{#integrating-with-livefyre}

AEM Aprenda a integrar las capacidades de gestión de contenido líderes en el sector de Livefyre con su instancia de 6.5, lo que le permite publicar contenido de valor generado por el usuario (UGC) desde las redes sociales en su sitio en cuestión de minutos.

## Introducción {#getting-started}

### AEM Instalación del paquete de Livefyre para la {#install-livefyre-package-for-aem}

AEM La versión 6.5 de viene con el paquete de funciones 1.2.6 de Livefyre preinstalado. Este paquete solo incluye la integración limitada de Livefyre con AEM Sites y debe desinstalarse antes de instalar un paquete actualizado. AEM Con el último paquete, puede experimentar la integración completa de Livefyre con, incluidos los sitios, los activos y el comercio.

>[!NOTE]
>
>AEM Algunas funciones del paquete de-LF dependen del Marco de componentes sociales (SCF). Si utiliza el paquete de funciones de Livefyre como parte de un sitio que no pertenece a ninguna comunidad, debe declarar *cq.social.scf* como dependencia en los clientlibs de autor del sitio web. Si utiliza el paquete de funciones LF como parte de un sitio web de comunidades, ya debería declarar esta dependencia.

1. AEM En la página de inicio de la, haga clic en **Herramientas** en el carril izquierdo.
1. Vaya a **Implementación > Paquetes**.
1. En el Administrador de paquetes, desplácese hasta que vea el paquete de funciones preinstalado de Livefyre y haga clic en el título del paquete **cq-social-livefyre-pkg-1.2.6.zip** para expandir las opciones.
1. Clic **Más > Desinstalar**.

   ![livefyre-aem-uninstall-64](assets/livefyre-aem-uninstall-64.png)

1. Descargar paquete de Livefyre desde [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html).

1. En el Administrador de paquetes, instale el paquete descargado. Consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md) AEM para obtener más información sobre el uso de Distribución de software y paquetes en la

   ![livefyre-aem4-6-4](assets/livefyre-aem4-6-4.png)

   AEM Ya está instalado el paquete Livefyre-. AEM Para poder empezar a utilizar las funciones de integración, debe Configurar la configuración de para que utilice.

   Para obtener más información y notas de la versión de los paquetes de funciones, consulte [Paquetes de funciones](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/home.html).

### AEM Configurar para utilizar Livefyre: Crear una carpeta de configuración {#configure-aem-to-use-livefyre-create-a-configuration-folder}

1. AEM En la página de inicio de la, haga clic en **Herramientas** en el carril izquierdo y, a continuación, vaya a **General > Explorador de configuración**.
   * Consulte la documentación del [Explorador de configuración](/help/sites-administering/configurations.md) para obtener más información.
1. Clic **Crear** para abrir el diálogo Crear configuración.
1. Asigne un nombre a la configuración y compruebe **Configuraciones de nube** casilla de verificación

   Esto creará una carpeta en **Herramientas > Implementación > Configuración de Livefyre** con el nombre proporcionado.

   ![livefyre-aem-create-config-folder](assets/livefyre-aem-create-config-folder.png)

### AEM Configurar para utilizar Livefyre: crear una configuración de Livefyre {#configure-aem-to-use-livefyre-create-a-livefyre-configuration}

AEM AEM Configure para utilizar las credenciales de licencia de Livefyre de su organización, lo que permite la comunicación entre Livefyre y el usuario de la licencia de.

1. AEM En la página de inicio de la, haga clic en **Herramientas** en el carril izquierdo y, a continuación, vaya a **Implementación > Configuración de Livefyre**.
1. Seleccione la carpeta de configuración en la que desea crear una nueva configuración de Livefyre y haga clic en **Crear**.

   ![create-livefyre-configuration1](assets/create-livefyre-configuration1.png)

   >[!NOTE]
   >
   >Las carpetas deben tener habilitadas las configuraciones de nube en sus propiedades para poder agregarles configuraciones de Livefyre. Las carpetas de configuración se crean y administran en [Explorador de configuración.](/help/sites-administering/configurations.md)
   >
   >No puede crear un nombre para una configuración; se hace referencia a él por la ruta de la carpeta en la que se encuentra. Solo puede tener una configuración por carpeta.

1. Seleccione la tarjeta de configuración de Livefyre recién creada y haga clic en **Propiedades**.

   ![create-livefyre-configuration2](assets/create-livefyre-configuration2.png)

1. Introduzca las credenciales de Livefyre de su organización y haga clic en **OK**.

   ![configure-aem2](assets/configure-aem2.png)

   Para acceder a esta información, abra el estudio de Livefyre y vaya a **Configuración > Configuración de integración > Credenciales**.

   AEM La instancia de está configurada para utilizar Livefyre y puede utilizar las funciones de integración de ahora en adelante.

### Personalizar integración de inicio de sesión único {#customize-single-sign-on-integration}

AEM El paquete de Livefyre para la incluye una integración predeterminada entre los perfiles de AEM Communities y el servicio SSO de Livefyre.

AEM Cuando los usuarios inician sesión en el sitio de, también inician sesión en los componentes sociales de Livefyre. Cuando un usuario que ha iniciado sesión intenta utilizar una función de componente de Livefyre que requiere autenticación (como cargar una fotografía), el componente Livefyre inicia la autenticación de usuario.

Es posible que la integración de autenticación predeterminada no sea perfecta para cada sitio. Para que coincida mejor con el flujo de autenticación en las plantillas de sitio, puede anular el delegado de autenticación predeterminado de Livefyre para satisfacer sus necesidades. Siga estos pasos:

1. Con el CRXDE Lite, copie */libs/social/integrations/livefyre/components/authorizablecomponent/authclientlib* hasta */apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib*.
1. Editar y guardar */apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib/auth.js* para implementar un delegado de autenticación de Livefyre que satisfaga sus necesidades.

   Para obtener más información sobre cómo personalizar un delegado de autenticación, consulte [Integración de identidad](https://answers.livefyre.com/developers/identity-integration/).

   AEM Para obtener más información sobre el uso de Clientlibs, consulte [Uso de bibliotecas del lado del cliente](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html?lang=es).

## Uso de Livefyre con AEM Sites {#use-livefyre-with-aem-sites}

### Añadir componentes de Livefyre a una página {#add-livefyre-components-to-a-page}

Antes de añadir componentes de Livefyre a una página de Sites, debe habilitar Livefyre para la página heredando una configuración de nube de Livefyre de una página principal o agregando la configuración directamente a la página. Consulte la implementación para incluir servicios en la nube en el sitio.

Una vez habilitado Livefyre para la página, los contenedores deben configurarse para permitir los componentes de Livefyre. Consulte [Configuración de componentes en modo de diseño](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/default-components-designmode.html) para obtener instrucciones sobre cómo habilitar distintos componentes.

>[!NOTE]
>
>Las aplicaciones que requieren autenticación para publicar no funcionan hasta que se configura la autenticación en Personalizar integración de inicio de sesión único.

1. Desde el **Componentes** panel lateral en modo de diseño, seleccione **Livefyre** en el menú para limitar la lista a los componentes de Livefyre disponibles.

   ![livefyre-add](assets/livefyre-add.png)

1. Seleccione un componente de Livefyre y arrástrelo a su posición en la página.
1. Seleccione si desea crear una nueva aplicación de Livefyre o incrustar una existente.

   AEM Si integra una aplicación existente, le pide que seleccione la aplicación. Si se crea una aplicación nueva, esta deberá rellenarse antes de que aparezca contenido. La aplicación se creará en el sitio y la red de Livefyre seleccionados cuando la configuración de nube de Livefyre se haya habilitado para la página.

   Para obtener más información sobre cómo insertar componentes, consulte [Edición del contenido de página](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/authoring/editing-content.html).

### AEM Editar un componente de Livefyre para una página de. {#edit-a-livefyre-component-for-an-aem-page}

Solo se puede configurar y editar un componente de Livefyre en Livefyre Studio. AEM Desde el:

1. Haga clic en el componente Livefyre para configurarlo.
1. Haga clic en **Configurar** para abrir el cuadro de diálogo de configuración.
1. Clic **Para editar este componente, vaya a Livefyre Studio**.
1. Edite la aplicación en Livefyre Studio.

## Uso de Livefyre con AEM Assets {#use-livefyre-with-aem-assets}

### Solicitar derechos e importar UGC en AEM Assets {#request-rights-and-import-ugc-into-aem-assets}

Puede importar contenido generado por el usuario (UGC) de Twitter y Instagram de Livefyre Studio a AEM Assets mediante el importador de UGC. Después de seleccionar el contenido que desea importar, debe solicitar derechos sobre el contenido para poder completar la importación.

>[!NOTE]
>
>Antes de usar Assets para importar UGC, debe configurar cuentas de cuentas de Social y cuentas de solicitudes de derechos en Livefyre Studio. Consulte [Configuración: Solicitudes de derechos](https://experienceleague.adobe.com/docs/livefyre/using/rights-requests/c-how-requesting-rights-works.html) para obtener más información.

Para importar UGC en AEM Assets:

1. AEM En la página de inicio de la, vaya a **Recursos > Archivos**.
1. Clic **Crear**, luego haga clic en **Importe UGC.**

   ![livefyre-aem-import-ugc](assets/livefyre-aem-import-ugc.png)

1. Buscar contenido:

   * En Livefyre, haga clic en la pestaña Biblioteca UGC. Utilice los filtros y busque para encontrar contenido de la biblioteca UGC.
   * En Twitter y Instagram, haga clic en la pestaña Twitter o Instagram. Utilice la búsqueda o los filtros para buscar contenido.

1. Seleccione los recursos que desea importar. Los recursos que seleccione se contabilizan automáticamente y se guardan en **Seleccionado** pestaña.
1. **Opcional**: haga clic en **Seleccionado** y revise el contenido UGC seleccionado para importar.
1. Haga clic en **Siguiente**.

   ![livefyre-aem-import-ugc2](assets/livefyre-aem-import-ugc2.png)

1. Para las solicitudes de derechos, elija una de las siguientes opciones para cada recurso:

   Para Instagram:

   * **Solicitar los derechos manualmente** para obtener un mensaje que se pueda copiar y pegar, y que se envíe manualmente a los propietarios de contenido a través de Instagram.
   * **Conceder los derechos del contenido manualmente** para anular los derechos de recursos individuales.

   >[!NOTE]
   >
   >Debido a las actualizaciones que afectan a la agregación de contenido desde cuentas de usuario no empresariales, ya no podemos publicar comentarios en su nombre ni comprobar automáticamente las respuestas del autor. [Haga clic aquí para obtener más información](https://developers.facebook.com/blog/post/2018/04/04/facebook-api-platform-product-changes/).

   ![livefyre-aem-import-ugc3-6-4](assets/livefyre-aem-import-ugc3-6-4.png)

   Para Twitter:

   * **Autor del mensaje** para enviar un mensaje al propietario del contenido solicitando derechos sobre el recurso.
   * **Conceder los derechos del contenido manualmente** para anular los derechos de recursos individuales.


1. Haga clic en **Importar**.

   Si ha enviado una solicitud de derechos de Twitter, el propietario del contenido verá el mensaje de solicitud de derechos en su cuenta:

   ![livefyre-aem-rights-request-twitter](assets/livefyre-aem-rights-request-twitter.png)

   >[!NOTE]
   >
   >Twitter tiene límites en solicitudes idénticas procedentes de la misma cuenta. Cuando importe más de un par de recursos, modifique los mensajes individualmente para evitar que se les marque.

1. Clic **Listo** en la esquina superior derecha para finalizar el flujo de trabajo de la solicitud de derechos.

   Puede ver el estado de una solicitud de derechos pendiente para un recurso en Livefyre Studio. Si el contenido está pendiente de una solicitud de derechos, el recurso no se mostrará en AEM Assets hasta que se concedan los derechos. El recurso aparece automáticamente en AEM Assets cuando se concede una solicitud de derechos.

   Para Instagram, debe rastrear la respuesta del propietario del contenido y conceder derechos manualmente si se le otorgan derechos sobre el contenido.

## AEM Uso de Livefyre con comercio de {#use-livefyre-with-aem-commerce}

### AEM Importación de catálogos de producto en Livefyre con Comercio de la {#import-product-catalogs-into-livefyre-with-aem-commerce}

AEM Los usuarios de Commerce de pueden integrar perfectamente su catálogo de productos existente en Livefyre para aumentar la participación del usuario en las aplicaciones de visualización de Livefyre.

Después de importar el catálogo de productos, los productos se muestran en tiempo real en la instancia de Livefyre. AEM Si edita o elimina elementos en el catálogo de productos de Comercio de, los cambios se actualizarán automáticamente en Livefyre.

1. AEM AEM Asegúrese de que tiene instalado el paquete Livefyre para la más reciente en la instancia de la instancia de la aplicación.
1. AEM En la página de inicio de la, vaya a **AEM Comercio de**.
1. Cree una nueva colección o utilice una colección existente.
1. Pase el ratón sobre la colección y haga clic en **Propiedades de colección** (icono de lápiz).
1. Marque **Sincronización a Livefyre**.
1. Completar en **Prefijo de página de Livefyre** AEM para vincular esta colección a una página específica en la lista de distribución de.

   El prefijo de página define la ruta raíz del entorno donde comienza la búsqueda de páginas de productos. Livefyre elige la primera página que tiene asociado un producto correspondiente. Para obtener diferentes páginas para diferentes productos, se necesitan varias colecciones.

## AEM Matriz de soporte para aplicaciones de Livefyre {#aem-support-matrix-for-livefyre-apps}

| Aplicaciones de Livefyre | AEM 6.1 | AEM 6.2 | AEM 6.3 | AEM 6.4 |
|---|---|---|---|---|
| Carrusel | X | X | X | X |
| Chat | X | X | X | X |
| Comentarios | X | X | X | X |
| Filmstrip |  | X | X | X |
| LiveBlog | X | X | X | X |
| Asignar | X | X | X | X |
| Muro de medios | X | X | X | X |
| Mosaico | X | X | X | X |
| Encuesta |  | X | X | X |
| Críticas |  | X | X | X |
| Tarjeta única | X | X | X | X |
| Storify 2 |  | X | X | X |
| Tendencias |  | X | X | X |
| Upload Button |  | X | X | X |
