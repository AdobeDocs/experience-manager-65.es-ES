---
title: Elementos esenciales del sitio de comunidad
description: Exportar y eliminar sitios de la comunidad y crear plantillas de sitio personalizadas
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 2%

---

# Elementos esenciales del sitio de comunidad {#community-site-essentials}

## Plantilla de sitio personalizada {#custom-site-template}

Se puede especificar una plantilla de sitio personalizada por separado para cada copia de idioma de un sitio de la comunidad.

Para ello:

* Cree una plantilla personalizada.
* Superponga la ruta de la plantilla de sitio predeterminada.
* Añada la plantilla personalizada a la ruta de la superposición.
* Especifique la plantilla personalizada agregando una propiedad `page-template` al nodo `configuration`.

**Plantilla predeterminada**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**Plantilla personalizada en ruta de superposición**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**Propiedad**: page-template

**Tipo**: Cadena

**Valor**: `template-name` (sin extensión)

**Nodo de configuración**:

`/content/community site path/lang/configuration`

Por ejemplo: `/content/sites/engage/en/configuration`

>[!NOTE]
>
>Todos los nodos de la ruta superpuesta sólo deben ser del tipo `Folder`.

>[!CAUTION]
>
>Si a la plantilla personalizada se le asigna el nombre *sitepage.hbs*, todos los sitios de la comunidad se personalizarán.

### Ejemplo de plantilla de sitio personalizada {#custom-site-template-example}

Por ejemplo, `vertical-sitepage.hbs` es una plantilla de sitio que da como resultado la colocación de vínculos de menú verticalmente hacia abajo en el lado izquierdo de la página, en lugar de horizontalmente debajo del titular.

[Obtener archivo](assets/vertical-sitepage.hbs)
Coloque la plantilla de sitio personalizada en la carpeta de superposición:

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

Identifique la plantilla personalizada agregando una propiedad `page-template` al nodo de configuración:

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

Asegúrese de **Guardar todo** y replicar el código personalizado en todas las instancias de Adobe Experience Manager AEM () (el código personalizado no se incluye cuando el contenido del sitio de la comunidad se publica desde la consola).

La práctica recomendada para replicar el código personalizado es [crear un paquete](../../help/sites-administering/package-manager.md#creating-a-new-package) e implementarlo en todas las instancias.

## Exportar un sitio de la comunidad {#exporting-a-community-site}

AEM Una vez creado un sitio de la comunidad, es posible exportar el sitio como un paquete de almacenado en el Administrador de paquetes y disponible para descargar y cargar.

Está disponible en la [consola Sitios de comunidades](sites-console.md#exporting-the-site).

El código UGC y el código personalizado no se incluyen en el paquete del sitio de la comunidad.

Para exportar UGC, usa la [Herramienta de migración de UGC para AEM Communities](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration), una herramienta de migración de código abierto disponible en GitHub.

## Eliminar un sitio de la comunidad {#deleting-a-community-site}

A partir de AEM Communities 6.3 Service Pack 1, el icono Eliminar sitio aparece al pasar el ratón por encima del sitio de la comunidad desde la consola **[!UICONTROL Communities]** > **[!UICONTROL Sites]**. Durante el desarrollo, si desea eliminar un sitio de la comunidad y empezar de nuevo, puede utilizar esta funcionalidad. Al eliminar un sitio de la comunidad, se eliminan los siguientes elementos asociados con ese sitio:

* [UGC](#user-generated-content)
* [Grupos de usuarios](#community-user-groups)
* [Registros de base de datos](#database-records)

### ID de sitio único de comunidad {#community-unique-site-id}

Para identificar el ID único del sitio asociado al sitio de la comunidad mediante CRXDE:

* Vaya a la raíz de idioma del sitio, como `/content/sites/*<site name>*/en/rep:policy`.

* Busque el nodo `allow<#>` con un `rep:principalName` en este formato `rep:principalName = *community-enable-nrh9h-members*`.

* El identificador del sitio es el tercer componente de `rep:principalName`

  Por ejemplo, si `rep:principalName = community-enable-nrh9h-members`

   * **nombre del sitio** = *habilitar*
   * **Id. de sitio** = *nrh9h*
   * **ID de sitio único** = *enable-nrh9h*

### Contenido generado por el usuario {#user-generated-content}

Obtenga el proyecto communities-srp-tools de GitHub:

* [https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Contiene un servlet para eliminar todos los UGC de cualquier SRP.

Se pueden eliminar todos los UGC o para un sitio específico, por ejemplo:

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

Esto solo elimina el contenido generado por el usuario (introducido al publicar) y el contenido no creado (introducido en el autor). Por lo tanto, [nodos en la sombra](srp.md#shadownodes) no se ven afectados.

### Grupos de usuarios de la comunidad {#community-user-groups}

En todas las instancias de autor y publicación, desde la [consola de seguridad](../../help/sites-administering/security.md), busque y quite los [grupos de usuarios](users.md) que están:

* Con el prefijo `community`
* Seguido de [id. de sitio único](#community-unique-site-id)

Por ejemplo, `community-engage-x0e11-members`.
