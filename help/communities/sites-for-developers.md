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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Elementos esenciales del sitio de la comunidad {#community-site-essentials}

## Plantilla de sitio personalizada {#custom-site-template}

Se puede especificar una plantilla de sitio personalizada por separado para cada copia de idioma de un sitio de comunidad.

Para ello,

* Creación de una plantilla personalizada
* Superponer la ruta predeterminada de la plantilla del sitio
* Agregar la plantilla personalizada a la ruta de superposición
* Especifique la plantilla personalizada agregando una `page-template` propiedad al `configuration` nodo

**Plantilla** predeterminada:

/**libs**/social/console/components/hbs/sitepage/**sitepage**.hbs

**Plantilla personalizada en ruta** de superposición:

/es/**apps**/social/console/components/hbs/sitepage/**&lt;*template-name*>**.hbs

**Propiedad**: page-template **Type**: String **Value**: &lt;*template-name*> (sin extensión)

**Nodo** de configuración:

/content/&lt;ruta *del sitio* de la comunidad>/&lt;*lang*>/configuration

Por ejemplo: /content/sites/engagement/es/configuration

>[!NOTE]
>
>Todos los nodos de la ruta superpuesta solo deben ser de tipo `Folder`.

>[!CAUTION]
>
>Si la plantilla personalizada recibe el nombre *sitepage.hbs,* todos los sitios de comunidad se personalizarán.

### Ejemplo de plantilla de sitio personalizada {#custom-site-template-example}

Por ejemplo, `vertical-sitepage.hbs` es una plantilla de sitio que resulta en la colocación de vínculos de menú verticalmente hacia abajo en el lado izquierdo de la página, en lugar de horizontalmente debajo de la pancarta.

[Obtener archivo](assets/vertical-sitepage.hbs)Coloque la plantilla de sitio personalizada en la carpeta de superposiciones:

/es/**apps**/social/console/components/hbs/sitepage/**vertical-sitepage**.hbs

Identifique la plantilla personalizada agregando una `page-template` propiedad al nodo de configuración:

/content/sites/sample/es/configuration

![chlimage_1-80](assets/chlimage_1-80.png)

Asegúrese de **guardar todo** y replicar código personalizado en todas las instancias de AEM (el código personalizado no se incluye cuando el contenido del sitio de la comunidad se publica desde la consola).

La práctica recomendada para replicar código personalizado es [crear un paquete](../../help/sites-administering/package-manager.md#creating-a-new-package) e implementarlo en todas las instancias.

## Exportación de un sitio de comunidad {#exporting-a-community-site}

Una vez creado un sitio de comunidad, es posible exportar el sitio como un paquete de AEM almacenado en el administrador de paquetes y disponible para su descarga y carga.

Esta opción está disponible en la consola Sitios de [comunidades](sites-console.md#exporting-the-site).

Tenga en cuenta que UGC y el código personalizado no se incluyen en el paquete del sitio de la comunidad.

Para exportar UGC, utilice la herramienta [de migración UGC de comunidades](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)AEM, una herramienta de migración de código abierto disponible en GitHub.

## Eliminación de un sitio de comunidad {#deleting-a-community-site}

A partir de AEM Communities 6.3 Service Pack 1, el icono Eliminar sitio aparece al pasar el ratón sobre el sitio de la comunidad desde la consola Comunidades > Sitios. Durante el desarrollo, si se desea eliminar un sitio de comunidad y empezar de nuevo, puede utilizar esta funcionalidad. Al eliminar un sitio de comunidad, se eliminan los siguientes elementos asociados con dicho sitio:

* [UGC](#user-generated-content)
* [Grupos de usuarios](#community-user-groups)
* [Recursos](#enablement-assets)
* [Registros de base de datos](#database-records)

### ID del sitio único de la comunidad {#community-unique-site-id}

Para identificar la ID única del sitio asociada con el sitio de la comunidad, utilice CRXDE:

* Navegue hasta la raíz de idioma del sitio, como `/content/sites/*<site name>*/en/rep:policy`

* Buscar el `allow<#>` nodo con un `rep:principalName` en este formato `rep:principalName = *community-enable-nrh9h-members*`

* El ID del sitio es el tercer componente de `rep:principalName`Por ejemplo, si `rep:principalName = community-enable-nrh9h-members`

   * **nombre** del sitio = *habilitar*
   * **ID** del sitio = *nrh9h*
   * **ID** de sitio único = *enable-nrh9h*

### Contenido generado por el usuario {#user-generated-content}

Obtenga el proyecto comunidades-srp-tools de Github:

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

Contiene un servlet para eliminar todo UGC de cualquier SRP.

Se puede eliminar todo el contenido generado por usuarios o para un sitio específico, por ejemplo:

* path=/content/usergenerate/asi/mongo/content/sites/engagement

Esto solo elimina el contenido generado por el usuario (introducido en la publicación) y no el contenido creado (introducido en el autor). Por lo tanto, los nodos [de](srp.md#shadownodes) sombra no se ven afectados.

### Grupos de usuarios de la comunidad {#community-user-groups}

En todas las instancias de creación y publicación, desde la consola [de](../../help/sites-administering/security.md)seguridad, busque y elimine los grupos [de](users.md) usuarios que:

* Prefijo con `community`
* Seguido por una ID de sitio [única](#community-unique-site-id)

Por ejemplo, `community-engage-x0e11-members`.

### Recursos de habilitación {#enablement-assets}

Desde la consola principal:

* Select **[!UICONTROL Assets]**
* Entrar en el modo **[!UICONTROL Seleccionar]**
* Seleccione la carpeta con el nombre del ID de sitio [único](#community-unique-site-id)
* Seleccione **[!UICONTROL Eliminar]** (puede que sea necesario seleccionar entre **[!UICONTROL Más...]**)

### Registros de base de datos {#database-records}

No hay ninguna herramienta para eliminar de forma selectiva las entradas de base de datos para un sitio de comunidad de habilitación específico.

Cuando se eliminen todos los sitios de la comunidad, suelte los campos de habilitación db y scormenginedb usando MySQL Workbench.
