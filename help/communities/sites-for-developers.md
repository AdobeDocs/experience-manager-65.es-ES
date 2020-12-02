---
title: Elementos esenciales del sitio de la comunidad
seo-title: Elementos esenciales del sitio de la comunidad
description: Exportación y eliminación de sitios de comunidad y creación de plantillas de sitio personalizadas
seo-description: Exportación y eliminación de sitios de comunidad y creación de plantillas de sitio personalizadas
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---


# Community Site Essentials {#community-site-essentials}

## Plantilla de sitio personalizada {#custom-site-template}

Se puede especificar una plantilla de sitio personalizada por separado para cada copia de idioma de un sitio de comunidad.

Para ello:

* Cree una plantilla personalizada.
* Superponga la ruta de la plantilla de sitio predeterminada.
* Añada la plantilla personalizada en la ruta de superposición.
* Especifique la plantilla personalizada agregando una propiedad `page-template` al nodo `configuration`.

**Plantilla** predeterminada:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**Plantilla personalizada en ruta** de superposición:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**Propiedad**: page-template

**Tipo**: Cadena

**Valor**:  `template-name` (sin extensión)

**Nodo** de configuración:

`/content/community site path/lang/configuration`

Por ejemplo: `/content/sites/engage/en/configuration`

>[!NOTE]
>
>Todos los nodos de la ruta superpuesta sólo deben ser del tipo `Folder`.

>[!CAUTION]
>
>Si la plantilla personalizada recibe el nombre *sitepage.hbs*, se personalizarán todos los sitios de la comunidad.

### Ejemplo de plantilla de sitio personalizada {#custom-site-template-example}

Como ejemplo, `vertical-sitepage.hbs` es una plantilla de sitio que resulta en la colocación de vínculos de menú verticalmente en el lado izquierdo de la página, en lugar de horizontalmente debajo del titular.

[Obtener ](assets/vertical-sitepage.hbs)
archivoColoque la plantilla de sitio personalizada en la carpeta de superposiciones:

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

Identifique la plantilla personalizada agregando una propiedad `page-template` al nodo de configuración:

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

Asegúrese de **Guardar todo** y replicar código personalizado en todas las instancias de AEM (el código personalizado no se incluye cuando el contenido del sitio de comunidad se publica desde la consola).

La práctica recomendada para replicar código personalizado es [crear un paquete](../../help/sites-administering/package-manager.md#creating-a-new-package) e implementarlo en todas las instancias.

## Exportación de un sitio de comunidad {#exporting-a-community-site}

Una vez creado un sitio de comunidad, es posible exportar el sitio como paquete de AEM almacenado en el administrador de paquetes y disponible para su descarga y carga.

Esto está disponible en la consola [Sitios de comunidades](sites-console.md#exporting-the-site).

Tenga en cuenta que UGC y el código personalizado no se incluyen en el paquete del sitio de la comunidad.

Para exportar UGC, utilice la [Herramienta de migración UGC de AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration), una herramienta de migración de código abierto disponible en GitHub.

## Eliminación de un sitio de comunidad {#deleting-a-community-site}

A partir de AEM Communities 6.3 Service Pack 1, el icono Eliminar sitio aparece al pasar el ratón por encima del sitio de la comunidad desde la consola **[!UICONTROL Communities]** > **[!UICONTROL Sites]**. Durante el desarrollo, si desea eliminar un sitio de comunidad y un inicio nuevo, puede utilizar esta funcionalidad. Al eliminar un sitio de comunidad, se eliminan los siguientes elementos asociados con dicho sitio:

* [UGC](#user-generated-content)
* [Grupos de usuarios](#community-user-groups)
* [Assets](#enablement-assets)
* [Registros de base de datos](#database-records)

### ID del sitio único de la comunidad {#community-unique-site-id}

Para identificar la ID única del sitio asociada con el sitio de la comunidad, utilice CRXDE:

* Navegue hasta la raíz de idioma del sitio, como `/content/sites/*<site name>*/en/rep:policy`.

* Busque el nodo `allow<#>` con un `rep:principalName` en este formato `rep:principalName = *community-enable-nrh9h-members*`.

* La ID del sitio es el tercer componente de `rep:principalName`

   Por ejemplo, si `rep:principalName = community-enable-nrh9h-members`

   * **site name** =  *enable*
   * **ID**  del sitio=  *nrh9h*
   * **ID**  de sitio único=  *enable-nrh9h*

### Contenido generado por el usuario {#user-generated-content}

Obtenga el proyecto comunidades-srp-tools de Github:

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

Contiene un servlet para eliminar todo UGC de cualquier SRP.

Se puede eliminar todo el contenido generado por usuarios o para un sitio específico, por ejemplo:

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

Esto solo elimina el contenido generado por el usuario (introducido en la publicación) y no el contenido creado (introducido en el autor). Por lo tanto, [nodos de sombra](srp.md#shadownodes) no se ven afectados.

### Grupos de usuarios de la comunidad {#community-user-groups}

En todas las instancias de creación y publicación, desde la [consola de seguridad](../../help/sites-administering/security.md), busque y elimine los [grupos de usuarios](users.md) que son:

* Prefijo con `community`
* Seguido por [identificación única del sitio](#community-unique-site-id)

Por ejemplo, `community-engage-x0e11-members`.

### Recursos de habilitación {#enablement-assets}

Desde la consola principal:

* Seleccione **[!UICONTROL Recursos]**.
* Introduzca el modo **[!UICONTROL Seleccionar]**.
* Seleccione la carpeta con el [identificador único del sitio](#community-unique-site-id).
* Seleccione **[!UICONTROL Eliminar]** (puede que necesite seleccionar entre **[!UICONTROL Más...]**).

### Registros de base de datos {#database-records}

No hay ninguna herramienta para eliminar de forma selectiva las entradas de base de datos para un sitio de comunidad de habilitación específico.

Cuando se eliminen todos los sitios de la comunidad, suelte los campos de habilitación db y scormenginedb usando MySQL Workbench.
