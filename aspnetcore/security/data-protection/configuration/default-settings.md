---
title: Gerenciamento de chaves de proteção de dados e o tempo de vida no ASP.NET Core
author: rick-anderson
description: Saiba mais sobre o gerenciamento de chaves de proteção de dados e o tempo de vida no ASP.NET Core.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/configuration/default-settings
ms.openlocfilehash: 2f022a4c7519485fe629ce47c27d214c8c27d5bc
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036553"
---
# <a name="data-protection-key-management-and-lifetime-in-aspnet-core"></a><span data-ttu-id="f7de4-103">Gerenciamento de chaves de proteção de dados e o tempo de vida no ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="f7de4-103">Data Protection key management and lifetime in ASP.NET Core</span></span>

<span data-ttu-id="f7de4-104">Por [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="f7de4-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="key-management"></a><span data-ttu-id="f7de4-105">Gerenciamento de chaves</span><span class="sxs-lookup"><span data-stu-id="f7de4-105">Key management</span></span>

<span data-ttu-id="f7de4-106">O aplicativo tenta detectar seu ambiente operacional e lidar com a configuração de chave por conta própria.</span><span class="sxs-lookup"><span data-stu-id="f7de4-106">The app attempts to detect its operational environment and handle key configuration on its own.</span></span>

1. <span data-ttu-id="f7de4-107">Se o aplicativo estiver hospedado em [aplicativos do Azure](https://azure.microsoft.com/services/app-service/), as chaves são persistidas para o *%HOME%\ASP.NET\DataProtection-Keys* pasta.</span><span class="sxs-lookup"><span data-stu-id="f7de4-107">If the app is hosted in [Azure Apps](https://azure.microsoft.com/services/app-service/), keys are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="f7de4-108">Essa pasta é apoiada pelo repositório de rede e é sincronizada em todos os computadores que hospedam o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7de4-108">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span>
   * <span data-ttu-id="f7de4-109">As chaves não são protegidas em repouso.</span><span class="sxs-lookup"><span data-stu-id="f7de4-109">Keys aren't protected at rest.</span></span>
   * <span data-ttu-id="f7de4-110">O *DataProtection chaves* pasta fornece o anel de chave a todas as instâncias de um aplicativo em um único slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="f7de4-110">The *DataProtection-Keys* folder supplies the key ring to all instances of an app in a single deployment slot.</span></span>
   * <span data-ttu-id="f7de4-111">Slots de implantação separados, como de preparo e produção, não compartilham um anel de chave.</span><span class="sxs-lookup"><span data-stu-id="f7de4-111">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span> <span data-ttu-id="f7de4-112">Quando você alternar entre os slots de implantação, por exemplo, trocar o preparo e produção ou usando um teste a / B, qualquer aplicativo usando a proteção de dados não será capaz de descriptografar dados armazenados usando o anel de chave dentro do slot anterior.</span><span class="sxs-lookup"><span data-stu-id="f7de4-112">When you swap between deployment slots, for example swapping Staging to Production or using A/B testing, any app using Data Protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="f7de4-113">Isso leva a usuários que estão sendo conectados fora de um aplicativo que usa a autenticação de cookie padrão do ASP.NET Core, pois ele usa a proteção de dados para proteger seus cookies.</span><span class="sxs-lookup"><span data-stu-id="f7de4-113">This leads to users being logged out of an app that uses the standard ASP.NET Core cookie authentication, as it uses Data Protection to protect its cookies.</span></span> <span data-ttu-id="f7de4-114">Se desejar que os anéis de chave independente de slot, use um provedor de anel de chave externo, como o armazenamento de BLOBs Azure, Azure Key Vault, um repositório SQL ou do cache Redis.</span><span class="sxs-lookup"><span data-stu-id="f7de4-114">If you desire slot-independent key rings, use an external key ring provider, such as Azure Blob Storage, Azure Key Vault, a SQL store, or Redis cache.</span></span>

1. <span data-ttu-id="f7de4-115">Se o perfil do usuário estiver disponível, as chaves são persistidas para o *%LOCALAPPDATA%\ASP.NET\DataProtection-Keys* pasta.</span><span class="sxs-lookup"><span data-stu-id="f7de4-115">If the user profile is available, keys are persisted to the *%LOCALAPPDATA%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="f7de4-116">Se o sistema operacional for Windows, as chaves são criptografadas em repouso usando a DPAPI.</span><span class="sxs-lookup"><span data-stu-id="f7de4-116">If the operating system is Windows, the keys are encrypted at rest using DPAPI.</span></span>

   <span data-ttu-id="f7de4-117">O [atributo setProfileEnvironment](/iis/configuration/system.applicationhost/applicationpools/add/processmodel#configuration) do pool de aplicativos também deve ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="f7de4-117">The app pool's [setProfileEnvironment attribute](/iis/configuration/system.applicationhost/applicationpools/add/processmodel#configuration) must also be enabled.</span></span> <span data-ttu-id="f7de4-118">O valor padrão de `setProfileEnvironment` é `true`.</span><span class="sxs-lookup"><span data-stu-id="f7de4-118">The default value of `setProfileEnvironment` is `true`.</span></span> <span data-ttu-id="f7de4-119">Em alguns cenários (por exemplo, um SO Windows), `setProfileEnvironment` é definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="f7de4-119">In some scenarios (for example, Windows OS), `setProfileEnvironment` is set to `false`.</span></span> <span data-ttu-id="f7de4-120">Se as chaves não estiverem armazenadas no diretório do perfil do usuário como esperado:</span><span class="sxs-lookup"><span data-stu-id="f7de4-120">If keys aren't stored in the user profile directory as expected:</span></span>

   1. <span data-ttu-id="f7de4-121">navegue até a pasta *%windir%/system32/inetsrv/config*.</span><span class="sxs-lookup"><span data-stu-id="f7de4-121">Navigate to the *%windir%/system32/inetsrv/config* folder.</span></span>
   1. <span data-ttu-id="f7de4-122">Abra o arquivo *applicationHost.config*.</span><span class="sxs-lookup"><span data-stu-id="f7de4-122">Open the *applicationHost.config* file.</span></span>
   1. <span data-ttu-id="f7de4-123">Localize o elemento `<system.applicationHost><applicationPools><applicationPoolDefaults><processModel>`.</span><span class="sxs-lookup"><span data-stu-id="f7de4-123">Locate the `<system.applicationHost><applicationPools><applicationPoolDefaults><processModel>` element.</span></span>
   1. <span data-ttu-id="f7de4-124">Confirme se o atributo `setProfileEnvironment` não está presente, que tem como padrão o valor `true`, ou defina explicitamente o valor do atributo como `true`.</span><span class="sxs-lookup"><span data-stu-id="f7de4-124">Confirm that the `setProfileEnvironment` attribute isn't present, which defaults the value to `true`, or explicitly set the attribute's value to `true`.</span></span>

1. <span data-ttu-id="f7de4-125">Se o aplicativo estiver hospedado no IIS, as chaves são mantidas no registro HKLM em uma chave de registro especial que tem a ACL acessível apenas para a conta de processo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f7de4-125">If the app is hosted in IIS, keys are persisted to the HKLM registry in a special registry key that's ACLed only to the worker process account.</span></span> <span data-ttu-id="f7de4-126">As chaves são criptografadas em repouso usando a DPAPI.</span><span class="sxs-lookup"><span data-stu-id="f7de4-126">Keys are encrypted at rest using DPAPI.</span></span>

1. <span data-ttu-id="f7de4-127">Se nenhuma dessas condições corresponderem, as chaves não são persistidas fora do processo atual.</span><span class="sxs-lookup"><span data-stu-id="f7de4-127">If none of these conditions match, keys aren't persisted outside of the current process.</span></span> <span data-ttu-id="f7de4-128">Quando o processo é encerrado, todas geradas chaves forem perdidas.</span><span class="sxs-lookup"><span data-stu-id="f7de4-128">When the process shuts down, all generated keys are lost.</span></span>

<span data-ttu-id="f7de4-129">O desenvolvedor está sempre no controle total e pode substituir como e onde as chaves são armazenadas.</span><span class="sxs-lookup"><span data-stu-id="f7de4-129">The developer is always in full control and can override how and where keys are stored.</span></span> <span data-ttu-id="f7de4-130">As três primeiras opções acima devem fornecer bons padrões para a maioria dos aplicativos de forma semelhante a como o ASP.NET  **\<machineKey >** rotinas de geração automática funcionavam no passado.</span><span class="sxs-lookup"><span data-stu-id="f7de4-130">The first three options above should provide good defaults for most apps similar to how the ASP.NET **\<machineKey>** auto-generation routines worked in the past.</span></span> <span data-ttu-id="f7de4-131">A opção de fallback final é o único cenário que exige que o desenvolvedor especifique [configuração](xref:security/data-protection/configuration/overview) antecipado se quiserem persistência de chave, mas essa fallback só ocorre em situações raras.</span><span class="sxs-lookup"><span data-stu-id="f7de4-131">The final, fallback option is the only scenario that requires the developer to specify [configuration](xref:security/data-protection/configuration/overview) upfront if they want key persistence, but this fallback only occurs in rare situations.</span></span>

<span data-ttu-id="f7de4-132">Ao hospedar em um contêiner do Docker, as chaves devem ser persistentes em uma pasta que é um volume do Docker (um volume compartilhado ou um volume montado de host que persiste além do tempo de vida do contêiner) ou em um provedor externo, como [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) ou [Redis](https://redis.io/).</span><span class="sxs-lookup"><span data-stu-id="f7de4-132">When hosting in a Docker container, keys should be persisted in a folder that's a Docker volume (a shared volume or a host-mounted volume that persists beyond the container's lifetime) or in an external provider, such as [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) or [Redis](https://redis.io/).</span></span> <span data-ttu-id="f7de4-133">Um provedor externo também é útil em cenários de web farm se os aplicativos não podem acessar um volume compartilhado de rede (consulte [PersistKeysToFileSystem](xref:security/data-protection/configuration/overview#persistkeystofilesystem) para obter mais informações).</span><span class="sxs-lookup"><span data-stu-id="f7de4-133">An external provider is also useful in web farm scenarios if apps can't access a shared network volume (see [PersistKeysToFileSystem](xref:security/data-protection/configuration/overview#persistkeystofilesystem) for more information).</span></span>

> [!WARNING]
> <span data-ttu-id="f7de4-134">Se o desenvolvedor substitui as regras descritas acima e aponta o sistema de proteção de dados em um repositório de chave específico, a criptografia automática de chaves em repouso está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="f7de4-134">If the developer overrides the rules outlined above and points the Data Protection system at a specific key repository, automatic encryption of keys at rest is disabled.</span></span> <span data-ttu-id="f7de4-135">Proteção em repouso pode ser reabilitada por meio [configuração](xref:security/data-protection/configuration/overview).</span><span class="sxs-lookup"><span data-stu-id="f7de4-135">At-rest protection can be re-enabled via [configuration](xref:security/data-protection/configuration/overview).</span></span>

## <a name="key-lifetime"></a><span data-ttu-id="f7de4-136">Vida útil da chave</span><span class="sxs-lookup"><span data-stu-id="f7de4-136">Key lifetime</span></span>

<span data-ttu-id="f7de4-137">Por padrão, as chaves têm um tempo de vida de 90 dias.</span><span class="sxs-lookup"><span data-stu-id="f7de4-137">Keys have a 90-day lifetime by default.</span></span> <span data-ttu-id="f7de4-138">Quando uma chave expira, o aplicativo gera uma nova chave automaticamente e define a nova chave como a chave ativa.</span><span class="sxs-lookup"><span data-stu-id="f7de4-138">When a key expires, the app automatically generates a new key and sets the new key as the active key.</span></span> <span data-ttu-id="f7de4-139">Chaves obsoletos permanecerão no sistema, desde que seu aplicativo pode descriptografar todos os dados protegidos com eles.</span><span class="sxs-lookup"><span data-stu-id="f7de4-139">As long as retired keys remain on the system, your app can decrypt any data protected with them.</span></span> <span data-ttu-id="f7de4-140">Ver [gerenciamento de chaves](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="f7de4-140">See [key management](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling) for more information.</span></span>

## <a name="default-algorithms"></a><span data-ttu-id="f7de4-141">Algoritmos padrão</span><span class="sxs-lookup"><span data-stu-id="f7de4-141">Default algorithms</span></span>

<span data-ttu-id="f7de4-142">O algoritmo de proteção de conteúdo padrão usado é AES-256-CBC para confidencialidade e HMACSHA256 autenticidade.</span><span class="sxs-lookup"><span data-stu-id="f7de4-142">The default payload protection algorithm used is AES-256-CBC for confidentiality and HMACSHA256 for authenticity.</span></span> <span data-ttu-id="f7de4-143">Uma chave mestra de 512 bits, alterada a cada 90 dias, é usada para derivar as duas chaves de subpropriedades usadas para esses algoritmos em uma base por carga.</span><span class="sxs-lookup"><span data-stu-id="f7de4-143">A 512-bit master key, changed every 90 days, is used to derive the two sub-keys used for these algorithms on a per-payload basis.</span></span> <span data-ttu-id="f7de4-144">Ver [subchave derivação](xref:security/data-protection/implementation/subkeyderivation#additional-authenticated-data-and-subkey-derivation) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="f7de4-144">See [subkey derivation](xref:security/data-protection/implementation/subkeyderivation#additional-authenticated-data-and-subkey-derivation) for more information.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f7de4-145">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f7de4-145">Additional resources</span></span>

* <xref:security/data-protection/extensibility/key-management>
* <xref:host-and-deploy/web-farm>