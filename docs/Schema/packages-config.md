---
# required metadata

title: NuGet packages.config File Reference | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
#ms.service:
ms.technology: nuget
ms.assetid: 207b9547-4558-41dc-9f3f-4bbdfb1d74e3

# optional metadata

description: In some project types, packages.config maintains the list of NuGet packages used in the project.
keywords: NuGet packages.config file, NuGet package references, NuGet dependencies
#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
- karann
- unnir
#ms.suite:
#ms.tgt_pltfrm:
#ms.custom:

---

# packages.config reference

The `packages.config` is used in some project types to maintain the list of packages referenced by the project.

The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference. Each `<package>` element can have the following attributes:

| Attribute | Required | Description |
| --- | --- | --- |
| id | Yes | |The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc. | 
| version | Yes | The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta. A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix. Ranges are not allowed. | 
| targetFramework | No | The [target framework moniker (TFM)](Target-Frameworks.md) to apply when installing the package. This is initially set to the project's target when a package is installed. As a result, different `<package>` elements can have different TFMs. For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452. If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46. A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages. | 
| allowedVersions | No | A range of allowed versions for this package in case the specific value in `version` cannot be found. | 
| developmentDependency | No | If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created. The default is `false`. | 

## Examples

The following `packages.config` refers to two dependencies:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
