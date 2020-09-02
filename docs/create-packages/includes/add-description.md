---
ms.openlocfilehash: c604d20c6358b7da5b1294ae48d9b7452794102f
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89359646"
---
<span data-ttu-id="e6304-101">La description facultative du package, affichée sur la page NuGet.org du package, est extraite de la `<description></description>` utilisée dans le `.csproj` fichier ou extraite via le `$description` dans le [fichier. NuSpec](../../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="e6304-101">The package's optional description, displayed on the package's NuGet.org page, is either pulled in from the `<description></description>` used in the `.csproj` file or pulled in via the `$description` in the [.nuspec file](../../reference/nuspec.md).</span></span>

<span data-ttu-id="e6304-102">Un exemple de champ de _Description_ est présenté dans le texte XML suivant du `.csproj` fichier pour un package .net :</span><span class="sxs-lookup"><span data-stu-id="e6304-102">An example of a _description_ field is shown in the following XML text of the `.csproj` file for a .NET package:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <PackageId>Azure.Storage.Blobs</PackageId>
    <Version>12.4.0</Version>
    <PackageTags>Microsoft Azure Storage Blobs;Microsoft;Azure;Blobs;Blob;Storage;StorageScalable</PackageTags>
    <Description>
      This client library enables working with the Microsoft Azure Storage Blob service for storing binary and text data.
      For this release see notes - https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/README.md and https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/CHANGELOG.md
      in addition to the breaking changes https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/BreakingChanges.txt
      Microsoft Azure Storage quickstarts and tutorials - https://docs.microsoft.com/en-us/azure/storage/
      Microsoft Azure Storage REST API Reference - https://docs.microsoft.com/en-us/rest/api/storageservices/
      REST API Reference for Blob Service - https://docs.microsoft.com/en-us/rest/api/storageservices/blob-service-rest-api
    </Description>
  </PropertyGroup>
</Project>
```
