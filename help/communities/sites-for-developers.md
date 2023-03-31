---
title: Elementos esenciales del sitio de la comunidad
seo-title: Community Site Essentials
description: Exportación y eliminación de sitios de la comunidad y creación de plantillas de sitio personalizadas
seo-description: Exporting and deleting community sites and creating custom site templates
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
source-git-commit: cc0574ae22758d095a3ca6b91f0ceae4a8691f0e
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 2%

---

# Elementos esenciales del sitio de la comunidad {#community-site-essentials}

## Plantilla de sitio personalizada {#custom-site-template}

Una plantilla de sitio personalizada se puede especificar por separado para cada copia de idioma de un sitio de comunidad.

Para ello:

* Cree una plantilla personalizada.
* Superponga la ruta de plantilla predeterminada del sitio.
* Agregue la plantilla personalizada a la ruta de superposición.
* Especifique la plantilla personalizada agregando una `page-template` a la `configuration` nodo .

**Plantilla predeterminada**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**Plantilla personalizada en la ruta de superposición**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**Propiedad**: page-template

**Tipo**: Cadena

**Valor**: `template-name` (sin extensión)

**Nodo de configuración**:

`/content/community site path/lang/configuration`

Por ejemplo: `/content/sites/engage/en/configuration`

>[!NOTE]
>
>Todos los nodos de la ruta superpuesta solo deben ser del tipo `Folder`.

>[!CAUTION]
>
>Si a la plantilla personalizada se le asigna el nombre *sitepage.hbs*, todos los sitios de la comunidad se personalizarán.

### Ejemplo de plantilla de sitio personalizada {#custom-site-template-example}

Como ejemplo, `vertical-sitepage.hbs` es una plantilla de sitio que resulta en la colocación de vínculos de menú verticalmente en el lado izquierdo de la página, en lugar de horizontalmente debajo del banner.

[Obtener archivo](assets/vertical-sitepage.hbs)
Coloque la plantilla de sitio personalizada en la carpeta de superposición:

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

Identifique la plantilla personalizada agregando una `page-template` a nodo de configuración:

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

Asegúrese de **Guardar todo** y replicar código personalizado en todas las instancias de AEM (el código personalizado no se incluye cuando el contenido del sitio de la comunidad se publica desde la consola).

La práctica recomendada para replicar código personalizado es: [crear un paquete](../../help/sites-administering/package-manager.md#creating-a-new-package) e impleméntelo en todas las instancias.

## Exportación de un sitio de la comunidad {#exporting-a-community-site}

Una vez creado un sitio de comunidad, es posible exportar el sitio como un paquete de AEM almacenado en el administrador de paquetes y disponible para su descarga y carga.

Esta opción está disponible en el [Consola Sitios de Communities](sites-console.md#exporting-the-site).

Tenga en cuenta que UGC y el código personalizado no se incluyen en el paquete del sitio de la comunidad.

Para exportar UGC, utilice la variable [Herramienta de migración UGC de AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration), una herramienta de migración de código abierto disponible en GitHub.

## Eliminación de un sitio de la comunidad {#deleting-a-community-site}

A partir de AEM Communities 6.3 Service Pack 1, el icono Eliminar sitio aparece al pasar el ratón por el sitio de la comunidad desde **[!UICONTROL Comunidades]** > **[!UICONTROL Sitios]** consola. Durante el desarrollo, si desea eliminar un sitio de la comunidad e iniciarlo de nuevo, puede utilizar esta funcionalidad. Al eliminar un sitio de la comunidad, se eliminan los siguientes elementos asociados con dicho sitio:

* [UGC](#user-generated-content)
* [Grupos de usuarios](#community-user-groups)
* [Registros de base de datos](#database-records)

### ID de sitio único de la comunidad {#community-unique-site-id}

Para identificar el ID de sitio único asociado con el sitio de la comunidad, usando CRXDE:

* Vaya a la raíz de idioma del sitio, como `/content/sites/*<site name>*/en/rep:policy`.

* Busque la `allow<#>` nodo con un `rep:principalName` en este formato `rep:principalName = *community-enable-nrh9h-members*`.

* El ID del sitio es el tercer componente de `rep:principalName`

   Por ejemplo, si `rep:principalName = community-enable-nrh9h-members`

   * **nombre del sitio** = *enable*
   * **ID del sitio** = *nrh9h*
   * **ID único del sitio** = *enable-nrh9h*

### Contenido generado por el usuario {#user-generated-content}

Obtenga el proyecto Communities-srp-tools de Github:

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

Contiene un servlet para eliminar todo UGC de cualquier SRP.

Todos los UGC pueden eliminarse o para un sitio específico, por ejemplo:

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

Esto solo elimina el contenido generado por el usuario (introducido en la publicación) y no el contenido creado (introducido en el autor). Por lo tanto, [nodos de sombra](srp.md#shadownodes) no se ven afectados.

### Grupos de usuarios de la comunidad {#community-user-groups}

En todas las instancias de autor y publicación, desde el [consola de seguridad](../../help/sites-administering/security.md), localice y elimine la variable [grupos de usuarios](users.md) que son:

* Con el prefijo `community`
* Seguido de [id de sitio único](#community-unique-site-id)

Por ejemplo, `community-engage-x0e11-members`.
