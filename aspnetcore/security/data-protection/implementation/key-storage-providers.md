---
title: Provedores de armazenamento de chaves no ASP.NET Core
author: rick-anderson
description: Saiba mais sobre provedores de armazenamento de chaves no ASP.NET Core e como configurar locais de armazenamento de chaves.
ms.author: riande
ms.date: 12/19/2018
uid: security/data-protection/implementation/key-storage-providers
ms.openlocfilehash: d6dabc9e4581e0891d1dd14f73e086d50b45bba4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054443"
---
# <a name="key-storage-providers-in-aspnet-core"></a><span data-ttu-id="cb5de-103">Provedores de armazenamento de chaves no ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="cb5de-103">Key storage providers in ASP.NET Core</span></span>

<span data-ttu-id="cb5de-104">O sistema de proteção de dados [emprega um mecanismo de descoberta por padrão](xref:security/data-protection/configuration/default-settings) para determinar onde as chaves de criptografia devem ser persistente.</span><span class="sxs-lookup"><span data-stu-id="cb5de-104">The data protection system [employs a discovery mechanism by default](xref:security/data-protection/configuration/default-settings) to determine where cryptographic keys should be persisted.</span></span> <span data-ttu-id="cb5de-105">O desenvolvedor pode substituir o mecanismo de descoberta padrão e especificar manualmente o local.</span><span class="sxs-lookup"><span data-stu-id="cb5de-105">The developer can override the default discovery mechanism and manually specify the location.</span></span>

> [!WARNING]
> <span data-ttu-id="cb5de-106">Se você especificar um local de persistência de chave explícita, o sistema de proteção de dados cancela o registro a criptografia de chave padrão no mecanismo de rest, portanto, as chaves não são criptografadas em repouso.</span><span class="sxs-lookup"><span data-stu-id="cb5de-106">If you specify an explicit key persistence location, the data protection system deregisters the default key encryption at rest mechanism, so keys are no longer encrypted at rest.</span></span> <span data-ttu-id="cb5de-107">É recomendável que você adicionalmente [especificar um mecanismo de criptografia de chave explícita](xref:security/data-protection/implementation/key-encryption-at-rest) para implantações de produção.</span><span class="sxs-lookup"><span data-stu-id="cb5de-107">It's recommended that you additionally [specify an explicit key encryption mechanism](xref:security/data-protection/implementation/key-encryption-at-rest) for production deployments.</span></span>

## <a name="file-system"></a><span data-ttu-id="cb5de-108">Sistema de arquivos</span><span class="sxs-lookup"><span data-stu-id="cb5de-108">File system</span></span>

<span data-ttu-id="cb5de-109">Para configurar um repositório chave baseadas no sistema de arquivos, chame o [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) rotina de configuração, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="cb5de-109">To configure a file system-based key repository, call the [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) configuration routine as shown below.</span></span> <span data-ttu-id="cb5de-110">Fornecer um [DirectoryInfo](/dotnet/api/system.io.directoryinfo) apontando para o repositório em que as chaves devem ser armazenadas:</span><span class="sxs-lookup"><span data-stu-id="cb5de-110">Provide a [DirectoryInfo](/dotnet/api/system.io.directoryinfo) pointing to the repository where keys should be stored:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"c:\temp-keys\"));
}
```

<span data-ttu-id="cb5de-111">O `DirectoryInfo` pode apontar para um diretório no computador local, ou ele pode apontar para uma pasta em um compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="cb5de-111">The `DirectoryInfo` can point to a directory on the local machine, or it can point to a folder on a network share.</span></span> <span data-ttu-id="cb5de-112">Se apontando para um diretório no computador local (e o cenário é que apenas os aplicativos no computador local exigem acesso para usar esse repositório), considere o uso de [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) (no Windows) para criptografar as chaves em repouso.</span><span class="sxs-lookup"><span data-stu-id="cb5de-112">If pointing to a directory on the local machine (and the scenario is that only apps on the local machine require access to use this repository), consider using [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) (on Windows) to encrypt the keys at rest.</span></span> <span data-ttu-id="cb5de-113">Caso contrário, considere o uso de um [certificado x. 509](xref:security/data-protection/implementation/key-encryption-at-rest) para criptografar as chaves em repouso.</span><span class="sxs-lookup"><span data-stu-id="cb5de-113">Otherwise, consider using an [X.509 certificate](xref:security/data-protection/implementation/key-encryption-at-rest) to encrypt keys at rest.</span></span>

## <a name="azure-and-redis"></a><span data-ttu-id="cb5de-114">O Azure e Redis</span><span class="sxs-lookup"><span data-stu-id="cb5de-114">Azure and Redis</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="cb5de-115">O [Microsoft.AspNetCore.DataProtection.AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/) e [Microsoft.AspNetCore.DataProtection.StackExchangeRedis](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.StackExchangeRedis/) pacotes permitem armazenar chaves de proteção de dados no armazenamento do Azure ou de um Redis cache.</span><span class="sxs-lookup"><span data-stu-id="cb5de-115">The [Microsoft.AspNetCore.DataProtection.AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/) and [Microsoft.AspNetCore.DataProtection.StackExchangeRedis](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.StackExchangeRedis/) packages allow storing data protection keys in Azure Storage or a Redis cache.</span></span> <span data-ttu-id="cb5de-116">As chaves podem ser compartilhadas entre várias instâncias de um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="cb5de-116">Keys can be shared across several instances of a web app.</span></span> <span data-ttu-id="cb5de-117">Aplicativos podem compartilhar cookies de autenticação ou proteção CSRF em vários servidores.</span><span class="sxs-lookup"><span data-stu-id="cb5de-117">Apps can share authentication cookies or CSRF protection across multiple servers.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="cb5de-118">O [Microsoft.AspNetCore.DataProtection.AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/) e [Microsoft.AspNetCore.DataProtection.Redis](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Redis/) pacotes permitem armazenar chaves de proteção de dados no armazenamento do Azure ou um cache Redis.</span><span class="sxs-lookup"><span data-stu-id="cb5de-118">The [Microsoft.AspNetCore.DataProtection.AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/) and [Microsoft.AspNetCore.DataProtection.Redis](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Redis/) packages allow storing data protection keys in Azure Storage or a Redis cache.</span></span> <span data-ttu-id="cb5de-119">As chaves podem ser compartilhadas entre várias instâncias de um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="cb5de-119">Keys can be shared across several instances of a web app.</span></span> <span data-ttu-id="cb5de-120">Aplicativos podem compartilhar cookies de autenticação ou proteção CSRF em vários servidores.</span><span class="sxs-lookup"><span data-stu-id="cb5de-120">Apps can share authentication cookies or CSRF protection across multiple servers.</span></span>

::: moniker-end

<span data-ttu-id="cb5de-121">Para configurar o provedor de armazenamento de BLOBs do Azure, chame um dos [PersistKeysToAzureBlobStorage](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.persistkeystoazureblobstorage) sobrecargas:</span><span class="sxs-lookup"><span data-stu-id="cb5de-121">To configure the Azure Blob Storage provider, call one of the [PersistKeysToAzureBlobStorage](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.persistkeystoazureblobstorage) overloads:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToAzureBlobStorage(new Uri("<blob URI including SAS token>"));
}
```

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="cb5de-122">Para configurar o Redis, chame um dos [PersistKeysToStackExchangeRedis](/dotnet/api/microsoft.aspnetcore.dataprotection.stackexchangeredisdataprotectionbuilderextensions.persistkeystostackexchangeredis) sobrecargas:</span><span class="sxs-lookup"><span data-stu-id="cb5de-122">To configure on Redis, call one of the [PersistKeysToStackExchangeRedis](/dotnet/api/microsoft.aspnetcore.dataprotection.stackexchangeredisdataprotectionbuilderextensions.persistkeystostackexchangeredis) overloads:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    var redis = ConnectionMultiplexer.Connect("<URI>");
    services.AddDataProtection()
        .PersistKeysToStackExchangeRedis(redis, "DataProtection-Keys");
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="cb5de-123">Para configurar o Redis, chame um dos [PersistKeysToRedis](/dotnet/api/microsoft.aspnetcore.dataprotection.redisdataprotectionbuilderextensions.persistkeystoredis) sobrecargas:</span><span class="sxs-lookup"><span data-stu-id="cb5de-123">To configure on Redis, call one of the [PersistKeysToRedis](/dotnet/api/microsoft.aspnetcore.dataprotection.redisdataprotectionbuilderextensions.persistkeystoredis) overloads:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    var redis = ConnectionMultiplexer.Connect("<URI>");
    services.AddDataProtection()
        .PersistKeysToRedis(redis, "DataProtection-Keys");
}
```

::: moniker-end

<span data-ttu-id="cb5de-124">Para mais informações, consulte os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="cb5de-124">For more information, see the following topics:</span></span>

* [<span data-ttu-id="cb5de-125">ConnectionMultiplexer stackexchange. Redis</span><span class="sxs-lookup"><span data-stu-id="cb5de-125">StackExchange.Redis ConnectionMultiplexer</span></span>](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Basics.md)
* [<span data-ttu-id="cb5de-126">Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="cb5de-126">Azure Redis Cache</span></span>](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache#connect-to-the-cache)
* [<span data-ttu-id="cb5de-127">exemplos de ASPNET/DataProtection</span><span class="sxs-lookup"><span data-stu-id="cb5de-127">aspnet/DataProtection samples</span></span>](https://github.com/aspnet/AspNetCore/tree/2.2.0/src/DataProtection/samples)

## <a name="registry"></a><span data-ttu-id="cb5de-128">Registro</span><span class="sxs-lookup"><span data-stu-id="cb5de-128">Registry</span></span>

<span data-ttu-id="cb5de-129">**Só se aplica às implantações do Windows.**</span><span class="sxs-lookup"><span data-stu-id="cb5de-129">**Only applies to Windows deployments.**</span></span>

<span data-ttu-id="cb5de-130">Às vezes, o aplicativo pode não ter acesso de gravação para o sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="cb5de-130">Sometimes the app might not have write access to the file system.</span></span> <span data-ttu-id="cb5de-131">Considere um cenário em que um aplicativo é executado como uma conta de serviço virtual (como *w3wp.exe*da identidade do pool de aplicativo).</span><span class="sxs-lookup"><span data-stu-id="cb5de-131">Consider a scenario where an app is running as a virtual service account (such as *w3wp.exe*'s app pool identity).</span></span> <span data-ttu-id="cb5de-132">Nesses casos, o administrador pode provisionar uma chave do registro que seja acessível pela identidade da conta de serviço.</span><span class="sxs-lookup"><span data-stu-id="cb5de-132">In these cases, the administrator can provision a registry key that's accessible by the service account identity.</span></span> <span data-ttu-id="cb5de-133">Chame o [PersistKeysToRegistry](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystoregistry) método de extensão, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="cb5de-133">Call the [PersistKeysToRegistry](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystoregistry) extension method as shown below.</span></span> <span data-ttu-id="cb5de-134">Fornecer um [RegistryKey](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.registryxmlrepository.registrykey) apontando para o local onde as chaves de criptografia devem ser armazenadas:</span><span class="sxs-lookup"><span data-stu-id="cb5de-134">Provide a [RegistryKey](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.registryxmlrepository.registrykey) pointing to the location where cryptographic keys should be stored:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToRegistry(Registry.CurrentUser.OpenSubKey(@"SOFTWARE\Sample\keys"));
}
```

> [!IMPORTANT]
> <span data-ttu-id="cb5de-135">É recomendável usar [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) para criptografar as chaves em repouso.</span><span class="sxs-lookup"><span data-stu-id="cb5de-135">We recommend using [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) to encrypt the keys at rest.</span></span>

::: moniker range=">= aspnetcore-2.2"

## <a name="entity-framework-core"></a><span data-ttu-id="cb5de-136">Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="cb5de-136">Entity Framework Core</span></span>

<span data-ttu-id="cb5de-137">O [Microsoft.AspNetCore.DataProtection.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.EntityFrameworkCore/) pacote fornece um mecanismo para armazenar chaves de proteção de dados para um banco de dados usando o Entity Framework Core.</span><span class="sxs-lookup"><span data-stu-id="cb5de-137">The [Microsoft.AspNetCore.DataProtection.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.EntityFrameworkCore/) package provides a mechanism for storing data protection keys to a database using Entity Framework Core.</span></span> <span data-ttu-id="cb5de-138">O `Microsoft.AspNetCore.DataProtection.EntityFrameworkCore` pacote do NuGet deve ser adicionado ao arquivo de projeto, ele não é parte do [metapacote Microsoft](xref:fundamentals/metapackage-app).</span><span class="sxs-lookup"><span data-stu-id="cb5de-138">The `Microsoft.AspNetCore.DataProtection.EntityFrameworkCore` NuGet package must be added to the project file, it's not part of the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>

<span data-ttu-id="cb5de-139">Com esse pacote, as chaves podem ser compartilhadas entre várias instâncias de um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="cb5de-139">With this package, keys can be shared across multiple instances of a web app.</span></span>

<span data-ttu-id="cb5de-140">Para configurar o provedor do EF Core, chame o [ `PersistKeysToDbContext<TContext>` ](/dotnet/api/microsoft.aspnetcore.dataprotection.entityframeworkcoredataprotectionextensions.persistkeystodbcontext) método:</span><span class="sxs-lookup"><span data-stu-id="cb5de-140">To configure the EF Core provider, call the [`PersistKeysToDbContext<TContext>`](/dotnet/api/microsoft.aspnetcore.dataprotection.entityframeworkcoredataprotectionextensions.persistkeystodbcontext) method:</span></span>

[!code-csharp[Main](key-storage-providers/sample/Startup.cs?name=snippet&highlight=13-15)]

<span data-ttu-id="cb5de-141">O parâmetro genérico, `TContext`, deve herdar de [DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext) e [IDataProtectionKeyContext](/dotnet/api/microsoft.aspnetcore.dataprotection.entityframeworkcore.idataprotectionkeycontext):</span><span class="sxs-lookup"><span data-stu-id="cb5de-141">The generic parameter, `TContext`, must inherit from [DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext) and [IDataProtectionKeyContext](/dotnet/api/microsoft.aspnetcore.dataprotection.entityframeworkcore.idataprotectionkeycontext):</span></span>

[!code-csharp[Main](key-storage-providers/sample/MyKeysContext.cs)]

<span data-ttu-id="cb5de-142">Criar o `DataProtectionKeys` tabela.</span><span class="sxs-lookup"><span data-stu-id="cb5de-142">Create the `DataProtectionKeys` table.</span></span> 

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="cb5de-143">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb5de-143">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="cb5de-144">Execute os seguintes comandos na **Package Manager Console** janela (PMC):</span><span class="sxs-lookup"><span data-stu-id="cb5de-144">Execute the following commands in the **Package Manager Console** (PMC) window:</span></span>

```PowerShell
Add-Migration AddDataProtectionKeys -Context MyKeysContext
Update-Database -Context MyKeysContext
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="cb5de-145">CLI do .NET Core</span><span class="sxs-lookup"><span data-stu-id="cb5de-145">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="cb5de-146">Execute os seguintes comandos em um shell de comando:</span><span class="sxs-lookup"><span data-stu-id="cb5de-146">Execute the following commands in a command shell:</span></span>

```console
dotnet ef migrations add AddDataProtectionKeys --context MyKeysContext
dotnet ef database update --context MyKeysContext
```

---

<span data-ttu-id="cb5de-147">`MyKeysContext` é o `DbContext` definido no exemplo de código anterior.</span><span class="sxs-lookup"><span data-stu-id="cb5de-147">`MyKeysContext` is the `DbContext` defined in the preceding code sample.</span></span> <span data-ttu-id="cb5de-148">Se você estiver usando um `DbContext` com um nome diferente, substitua seu `DbContext` nome do `MyKeysContext`.</span><span class="sxs-lookup"><span data-stu-id="cb5de-148">If you're using a `DbContext` with a different name, substitute your `DbContext` name for `MyKeysContext`.</span></span>

<span data-ttu-id="cb5de-149">O `DataProtectionKeys` classe/entidade adota a estrutura mostrada na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="cb5de-149">The `DataProtectionKeys` class/entity adopts the structure shown in the following table.</span></span>

| <span data-ttu-id="cb5de-150">Campo/propriedade</span><span class="sxs-lookup"><span data-stu-id="cb5de-150">Property/Field</span></span> | <span data-ttu-id="cb5de-151">Tipo CLR</span><span class="sxs-lookup"><span data-stu-id="cb5de-151">CLR Type</span></span> | <span data-ttu-id="cb5de-152">Tipo SQL</span><span class="sxs-lookup"><span data-stu-id="cb5de-152">SQL Type</span></span>              |
| -------------- | -------- | --------------------- |
| `Id`           | `int`    | <span data-ttu-id="cb5de-153">`int`, PK, não nulo</span><span class="sxs-lookup"><span data-stu-id="cb5de-153">`int`, PK, not null</span></span>   |
| `FriendlyName` | `string` | <span data-ttu-id="cb5de-154">`nvarchar(MAX)`, nulo</span><span class="sxs-lookup"><span data-stu-id="cb5de-154">`nvarchar(MAX)`, null</span></span> |
| `Xml`          | `string` | <span data-ttu-id="cb5de-155">`nvarchar(MAX)`, nulo</span><span class="sxs-lookup"><span data-stu-id="cb5de-155">`nvarchar(MAX)`, null</span></span> |

::: moniker-end

## <a name="custom-key-repository"></a><span data-ttu-id="cb5de-156">Repositório de chave personalizado</span><span class="sxs-lookup"><span data-stu-id="cb5de-156">Custom key repository</span></span>

<span data-ttu-id="cb5de-157">Se os mecanismos de caixa de entrada não forem apropriados, o desenvolvedor pode especificar seu próprio mecanismo de persistência de chave, fornecendo um personalizado [IXmlRepository](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.ixmlrepository).</span><span class="sxs-lookup"><span data-stu-id="cb5de-157">If the in-box mechanisms aren't appropriate, the developer can specify their own key persistence mechanism by providing a custom [IXmlRepository](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.ixmlrepository).</span></span>
