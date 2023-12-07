---
title: Refactorización de SocialUtils
description: AEM El paquete com.adobe.cq.social.ugcbase.SocialUtils ha quedado obsoleto en la versión 6.1 de
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---

# Refactorización de SocialUtils {#socialutils-refactoring}

## Paquete SocialUtils obsoleto {#socialutils-package-deprecated}

El paquete `com.adobe.cq.social.ugcbase.SocialUtils` AEM quedó obsoleto en la versión 6.1 de.

En las tablas siguientes se enumeran los métodos que se deben utilizar en lugar de `SocialUtils` métodos.

## Paquete SocialResourceUtilities  {#socialresourceutilities-package}

| Métodos en com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities |
|---|
| Boolean checkPermission(Resolución de ResourceResolver, Ruta de cadena, Acción de cadena) |  |
| SocialResourceProvider getSocialResourceProvider(Recurso) |  |
| SocialResourceConfiguration getStorageConfig(recurso) |  |
| Recurso getUGCResource(Recurso userResource) |  |
| Recurso getUGCResource(Recurso userResource, ResourceResolverFactory rrf) | nuevo |
| Recurso getUGCResource(Recurso userResource, ResourceResolverFactory rrf, Cadena resourceTypeHint) | nuevo |
| Recurso getUGCResource(Recurso userResource, Cadena resourceTypeHint) |  |
| El booleano hasModeratePermissions(Recurso) |  |
| Cadena resourceToACLPath(Recurso) |  |
| String resourceToUGCStoragePath(Resource) | reemplaza String resourceToUGCPath(Resource resource) |
| Cadena UGCToResourcePath(Recurso) |  |
| Cadena UGCToResourcePath(Cadena ugcPath) | firma de método modificada |
| String UGCToResourcePath(String ugcPath, resolución de ResourceResolver) | nuevo |

| Métodos en `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(Recurso) | reemplaza a SocialResourceProvider getConficonfiguredProvider(recurso) |

## Paquete de utilidades SCFU {#scfutilities-package}

| Métodos en `com.adobe.cq.social.`utilities.scf.api.SCFUtilites |
|---|
| Cadena getAvatar(UserProperties userProperties) |
| Cadena getAvatar(UserProperties, userProperties, int size) |
| Cadena getAvatar(UserProperties userProperties, Cadena absoluteDefaultAvatar) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE size) |
| Página getContainingPage(Recurso) |
| String getSocialProfileURL(nombre de usuario de cadena, resolución de ResourceResolver, página de página) |
| UserProperties getUserProperties(resolución de ResourceResolver, cadena userId) |

## Solo para uso interno {#for-internal-use-only}

| canAddNode(Session session, String path) booleano |
|---|
| Cadena createUniqueNameHint(Mensaje de cadena) |
| String createUniqueNameHint(Mensaje de cadena, int numRandomChars) |
| Cadena generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(Ruta de cadena, resolución de ResourceResolver) |
| Cadena getPagePath(Recurso) |
| String getPagePath(String path) |
| Cadena getResourceTypeForIncludedResource(Componente de recurso, cadena defaultResourceType, cadena designPropertyName) |
| String getResourceTypeFromDesign(Recurso, String styleProperty, String defaultValue) |
| isResourceOwner(Recurso) booleano |
| String mapUGCPath(Recurso) |
| String mapUGCPath(String ugcPath, resolución de ResourceResolver) |
| booleano mayPost(ResourceResolver resolver, Resource resource) |
| String prepareUserGeneratedContent(Resolución de ResourceResolver, ruta de la cadena) |

## Métodos ya no disponibles {#methods-no-longer-available}

| Nodo createNode(ResourceResolver resolver, String ruta, String nodeType) |
|---|
| Recurso getResourceAtPath(resolución de ResourceResolver, ruta de la cadena) |
| Recurso getResourceAtPath(Resolución de ResourceResolver, Ruta de cadena, Tipo de recurso de cadena) |
| Configuración de getStorageCloudServiceConfig(recurso) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| booleano mayAccessUGC(ResourceResolver resolver) |
