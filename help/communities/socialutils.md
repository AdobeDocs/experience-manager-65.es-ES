---
title: Refactorización de SocialUtils
seo-title: SocialUtils Refactoring
description: El paquete com.adobe.cq.social.ugcbase.SocialUtils quedó obsoleto en AEM 6.1
seo-description: The package com.adobe.cq.social.ugcbase.SocialUtils was deprecated in AEM 6.1
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 1%

---

# Refactorización de SocialUtils {#socialutils-refactoring}

## Paquete SocialUtils obsoleto {#socialutils-package-deprecated}

El paquete `com.adobe.cq.social.ugcbase.SocialUtils` quedó obsoleto en AEM 6.1.

En las tablas siguientes se enumeran los métodos que se deben utilizar en lugar de `SocialUtils` métodos.

## Paquete SocialResourceUtilities  {#socialresourceutilities-package}

| Métodos en com.adobe.cq.social.srp.Utilities.api.SocialResourceUtilities |
|---|
| Boolean checkPermission(ResourceResolver resolver, String path, String action) |  |
| SocialResourceProvider getSocialResourceProvider(recurso de recurso) |  |
| SocialResourceConfiguration getStorageConfig(Recurso) |  |
| Recurso getUGCResource(Recurso usuarioRecurso) |  |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rf) | nuevo |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rf, String resourceTypeHint) | nuevo |
| Resource getUGCResource(Resource userResource, String resourceTypeHint) |  |
| booleano hasModeratePermissions(Resource resource) |  |
| String resourceToACLPath(Resource resource) |  |
| String resourceToUGCStoragePath(Resource resource) | reemplaza a String resourceToUGCPath(Resource resource) |
| String UGCToResourcePath(Recurso) |  |
| String UGCToResourcePath(String ugcPath) | firma de método cambiada |
| String UGCToResourcePath(String ugcPath, ResourceResolver resolver) | nuevo |

| Métodos en `com.adobe.cq.social.`Utilidades.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(recurso de recurso) | reemplaza a SocialResourceProvider getConfiectedProvider(Resource resource) |

## Paquete SCFUtilities {#scfutilities-package}

| Métodos en `com.adobe.cq.social.`Utilidades.scf.api.SCFUtilites |
|---|
| String getAvatar(UserProperties userProperties) |
| String getAvatar(UserProperties userProperties, int size) |
| String getAvatar(UserProperties userProperties, String AbsolutDefaultAvatar) |
| String getAvatar(UserProperties userProperties, String AbsolutDefaultAvatar, SocialUtils.AVATAR_SIZE size) |
| Page getContainPage(Resource resource) |
| String getSocialProfileURL(nombre de usuario de cadena, resolución de ResourceResolver, página) |
| UserProperties getUserProperties(ResourceResolver resolver, String userId) |

## Solo para uso interno {#for-internal-use-only}

| booleano canAddNode(Session session, String path) |
|---|
| String createUniqueNameHint(Mensaje de cadena) |
| String createUniqueNameHint(Mensaje de cadena, int numRandomChars) |
| String generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(String path, ResourceResolver resolver) |
| String getPagePath(Resource resource) |
| String getPagePath(String path) |
| String getResourceTypeForIncludedResource(Componente de recurso, String defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(Resource resource, String styleProperty, String defaultValue) |
| booleano isResourceOwner(Resource resource) |
| String mapUGCPath(Resource resource) |
| String mapUGCPath(String ugcPath, ResourceResolver resolver) |
| boolean mayPost(ResourceResolver resolver, Resource resource) |
| String preparationUserGeneratedContent(ResourceResolver resolver, ruta de acceso de cadena) |

## Métodos que ya no están disponibles {#methods-no-longer-available}

| Node createNode(ResourceResolver resolver, String path, String nodeType) |
|---|
| Recurso getResourceAtPath(ResourceResolver resolver, ruta de acceso de cadena) |
| Resource getResourceAtPath(ResourceResolver resolver, String path, String resourceType) |
| Configuración getStorageCloudServiceConfig(recurso de recurso) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| booleano mayAccessUGC(ResourceResolver resolver) |
