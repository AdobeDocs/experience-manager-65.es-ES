---
title: Elementos esenciales del sitio de comunidad
seo-title: Community Site Essentials
description: Exportar y eliminar sitios de la comunidad y crear plantillas de sitio personalizadas
seo-description: Exporting and deleting community sites and creating custom site templates
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 2%

---

# Elementos esenciales del sitio de comunidad {#community-site-essentials}

## Plantilla de sitio personalizada {#custom-site-template}

Se puede especificar una plantilla de sitio personalizada por separado para cada copia de idioma de un sitio de la comunidad.

Para ello:

* Cree una plantilla personalizada.
* Superponga la ruta de la plantilla de sitio predeterminada.
* Añada la plantilla personalizada a la ruta de la superposición.
* Especifique la plantilla personalizada agregando un `page-template` a la propiedad `configuration` nodo.

**Plantilla predeterminada**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**Plantilla personalizada en ruta de superposición**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**Propiedad**: page-template

**Tipo**: cadena

**Valor**: `template-name` (sin extensión)

**Nodo de configuración**:

`/content/community site path/lang/configuration`

Por ejemplo: `/content/sites/engage/en/configuration`

>[!NOTE]
>
>Todos los nodos de la ruta superpuesta solo deben ser del tipo `Folder`.

>[!CAUTION]
>
>Si a la plantilla personalizada se le asigna el nombre *sitepage.hbs*, se personalizarán todos los sitios de la comunidad.

### Ejemplo de plantilla de sitio personalizada {#custom-site-template-example}

A modo de ejemplo, `vertical-sitepage.hbs` es una plantilla de sitio que coloca vínculos de menú verticalmente hacia abajo en el lado izquierdo de la página, en lugar de horizontalmente debajo del titular.

[Obtener archivo](assets/vertical-sitepage.hbs)
Coloque la plantilla de sitio personalizada en la carpeta de superposición:

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

Identificar la plantilla personalizada agregando un `page-template` al nodo de configuración:

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

Asegúrese de **Guardar todo** AEM y replicar el código personalizado en todas las instancias de la comunidad (el código personalizado no se incluye cuando el contenido del sitio de la comunidad se publica desde la consola).

La práctica recomendada para replicar código personalizado es [creación de un paquete](../../help/sites-administering/package-manager.md#creating-a-new-package) e implementarlo en todas las instancias.

## Exportar un sitio de la comunidad {#exporting-a-community-site}

AEM Una vez creado un sitio de la comunidad, es posible exportar el sitio como un paquete de almacenado en el administrador de paquetes y disponible para descargar y cargar.

Esta opción está disponible en [Consola Sitios de Communities](sites-console.md#exporting-the-site).

Tenga en cuenta que UGC y el código personalizado no se incluyen en el paquete del sitio de la comunidad.

Para exportar UGC, utilice el [Herramienta de migración de UGC para AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration), una herramienta de migración de código abierto disponible en GitHub.

## Eliminar un sitio de la comunidad {#deleting-a-community-site}

A partir de AEM Communities 6.3 Service Pack 1, el icono Eliminar sitio aparece al pasar el ratón por encima del sitio de la comunidad desde **[!UICONTROL Communities]** > **[!UICONTROL Sites]** consola. Durante el desarrollo, si desea eliminar un sitio de la comunidad y empezar de nuevo, puede utilizar esta funcionalidad. Al eliminar un sitio de la comunidad, se eliminan los siguientes elementos asociados con ese sitio:

* [UGC](#user-generated-content)
* [Grupos de usuarios](#community-user-groups)
* [Assets](#enablement-assets)
* [Registros de base de datos](#database-records)

### ID de sitio único de comunidad {#community-unique-site-id}

Para identificar el ID único del sitio asociado al sitio de la comunidad mediante CRXDE:

* Vaya a la raíz de idioma del sitio, como `/content/sites/*<site name>*/en/rep:policy`.

* Busque el `allow<#>` nodo con un `rep:principalName` en este formato `rep:principalName = *community-enable-nrh9h-members*`.

* El ID del sitio es el tercer componente de `rep:principalName`

   Por ejemplo, si `rep:principalName = community-enable-nrh9h-members`

   * **nombre del sitio** = *habilitar*
   * **ID del sitio** = *nrh9h*
   * **ID único de sitio** = *enable-nrh9h*

### Contenido generado por el usuario {#user-generated-content}

Obtenga el proyecto communities-srp-tools de Github:

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

Contiene un servlet para eliminar todos los UGC de cualquier SRP.

Se pueden eliminar todos los UGC o para un sitio específico, por ejemplo:

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

Esto solo elimina el contenido generado por el usuario (introducido al publicar) y el contenido no creado (introducido en el autor). Por lo tanto, [nodos en la sombra](srp.md#shadownodes) no se ven afectados.

### Grupos de usuarios de la comunidad {#community-user-groups}

En todas las instancias de autor y publicación, desde el [consola de seguridad](../../help/sites-administering/security.md), busque y elimine el [grupos de usuarios](users.md) que son:

* Con el prefijo `community`
* Seguido de [id de sitio único](#community-unique-site-id)

Por ejemplo, `community-engage-x0e11-members`.

### Recursos de habilitación {#enablement-assets}

Desde la consola principal:

* Seleccionar **[!UICONTROL Assets]**.
* Entrar **[!UICONTROL Seleccionar]** modo.
* Seleccione la carpeta con el nombre [ID de sitio único](#community-unique-site-id).
* Seleccionar **[!UICONTROL Eliminar]** (es posible que deba seleccionar entre **[!UICONTROL Más...]**).

### Registros de base de datos {#database-records}

No hay ninguna herramienta para eliminar selectivamente las entradas de la base de datos de un sitio específico de la comunidad de habilitación.

Cuando se eliminen todos los sitios de la comunidad, suelte enablementdb y scormenginedb con MySQL Workbench.
