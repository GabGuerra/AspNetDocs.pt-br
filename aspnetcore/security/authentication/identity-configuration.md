---
title: Configurar a identidade do ASP.NET Core
author: AdrienTorris
description: Entender os valores padrão de identidade do ASP.NET Core e saiba como configurar propriedades de identidade para usar valores personalizados.
ms.author: riande
ms.date: 02/11/2019
uid: security/authentication/identity-configuration
ms.openlocfilehash: 3213f669cbfccdcda7cc7c0142b8101e696678e6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044753"
---
# <a name="configure-aspnet-core-identity"></a><span data-ttu-id="15259-103">Configurar a identidade do ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="15259-103">Configure ASP.NET Core Identity</span></span>

<span data-ttu-id="15259-104">Identidade do ASP.NET Core usa valores padrão para configurações como a política de senha, bloqueio e configuração de cookie.</span><span class="sxs-lookup"><span data-stu-id="15259-104">ASP.NET Core Identity uses default values for settings such as password policy, lockout, and cookie configuration.</span></span> <span data-ttu-id="15259-105">Essas configurações podem ser substituídas no `Startup` classe.</span><span class="sxs-lookup"><span data-stu-id="15259-105">These settings can be overridden in the `Startup` class.</span></span>

## <a name="identity-options"></a><span data-ttu-id="15259-106">Opções de identidade</span><span class="sxs-lookup"><span data-stu-id="15259-106">Identity options</span></span>

<span data-ttu-id="15259-107">O [IdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.identityoptions) classe representa as opções que podem ser usadas para configurar o sistema de identidade.</span><span class="sxs-lookup"><span data-stu-id="15259-107">The [IdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.identityoptions) class represents the options that can be used to configure the Identity system.</span></span> <span data-ttu-id="15259-108">`IdentityOptions` deve ser definido **após** chamando `AddIdentity` ou `AddDefaultIdentity`.</span><span class="sxs-lookup"><span data-stu-id="15259-108">`IdentityOptions` must be set **after** calling `AddIdentity` or `AddDefaultIdentity`.</span></span>

### <a name="claims-identity"></a><span data-ttu-id="15259-109">Identidade baseada em declarações</span><span class="sxs-lookup"><span data-stu-id="15259-109">Claims Identity</span></span>

<span data-ttu-id="15259-110">[IdentityOptions.ClaimsIdentity](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.claimsidentity) Especifica o [ClaimsIdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions) com as propriedades mostradas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="15259-110">[IdentityOptions.ClaimsIdentity](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.claimsidentity) specifies the [ClaimsIdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions) with the properties shown in the following table.</span></span>

| <span data-ttu-id="15259-111">Propriedade</span><span class="sxs-lookup"><span data-stu-id="15259-111">Property</span></span> | <span data-ttu-id="15259-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="15259-112">Description</span></span> | <span data-ttu-id="15259-113">Padrão</span><span class="sxs-lookup"><span data-stu-id="15259-113">Default</span></span> |
| -------- | ----------- | :-----: |
| [<span data-ttu-id="15259-114">RoleClaimType</span><span class="sxs-lookup"><span data-stu-id="15259-114">RoleClaimType</span></span>](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions.roleclaimtype) | <span data-ttu-id="15259-115">Obtém ou define o tipo de declaração usado para uma declaração de função.</span><span class="sxs-lookup"><span data-stu-id="15259-115">Gets or sets the claim type used for a role claim.</span></span> | [<span data-ttu-id="15259-116">ClaimTypes.Role</span><span class="sxs-lookup"><span data-stu-id="15259-116">ClaimTypes.Role</span></span>](/dotnet/api/system.security.claims.claimtypes.role) |
| [<span data-ttu-id="15259-117">SecurityStampClaimType</span><span class="sxs-lookup"><span data-stu-id="15259-117">SecurityStampClaimType</span></span>](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions.securitystampclaimtype) | <span data-ttu-id="15259-118">Obtém ou define o tipo de declaração usado para a declaração de carimbo de segurança.</span><span class="sxs-lookup"><span data-stu-id="15259-118">Gets or sets the claim type used for the security stamp claim.</span></span> | `AspNet.Identity.SecurityStamp` |
| [<span data-ttu-id="15259-119">UserIdClaimType</span><span class="sxs-lookup"><span data-stu-id="15259-119">UserIdClaimType</span></span>](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions.useridclaimtype) | <span data-ttu-id="15259-120">Obtém ou define o tipo de declaração usado para a declaração do identificador de usuário.</span><span class="sxs-lookup"><span data-stu-id="15259-120">Gets or sets the claim type used for the user identifier claim.</span></span> | [<span data-ttu-id="15259-121">ClaimTypes.NameIdentifier</span><span class="sxs-lookup"><span data-stu-id="15259-121">ClaimTypes.NameIdentifier</span></span>](/dotnet/api/system.security.claims.claimtypes.nameidentifier) |
| [<span data-ttu-id="15259-122">UserNameClaimType</span><span class="sxs-lookup"><span data-stu-id="15259-122">UserNameClaimType</span></span>](/dotnet/api/microsoft.aspnetcore.identity.claimsidentityoptions.usernameclaimtype) | <span data-ttu-id="15259-123">Obtém ou define o tipo de declaração usado para a declaração de nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="15259-123">Gets or sets the claim type used for the user name claim.</span></span> | [<span data-ttu-id="15259-124">ClaimTypes.Name</span><span class="sxs-lookup"><span data-stu-id="15259-124">ClaimTypes.Name</span></span>](/dotnet/api/system.security.claims.claimtypes.name) |

### <a name="lockout"></a><span data-ttu-id="15259-125">Bloqueio</span><span class="sxs-lookup"><span data-stu-id="15259-125">Lockout</span></span>

<span data-ttu-id="15259-126">O bloqueio é definido na [PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync#Microsoft_AspNetCore_Identity_SignInManager_1_PasswordSignInAsync_System_String_System_String_System_Boolean_System_Boolean_) método:</span><span class="sxs-lookup"><span data-stu-id="15259-126">Lockout is set in the [PasswordSignInAsync](/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1.passwordsigninasync#Microsoft_AspNetCore_Identity_SignInManager_1_PasswordSignInAsync_System_String_System_String_System_Boolean_System_Boolean_) method:</span></span>

[!code-csharp[](identity-configuration/sample/Areas/Identity/Pages/Account/Login.cshtml.cs?name=snippet&highlight=9)]

<span data-ttu-id="15259-127">O código anterior se baseia o `Login` modelo de identidade.</span><span class="sxs-lookup"><span data-stu-id="15259-127">The preceding code is based on the `Login` Identity template.</span></span> 

<span data-ttu-id="15259-128">Opções de bloqueio são definidas na `StartUp.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="15259-128">Lockout options are set in `StartUp.ConfigureServices`:</span></span>

[!code-csharp[](identity-configuration/sample/Startup.cs?name=snippet_lock)]

<span data-ttu-id="15259-129">O código anterior define o [IdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.identityoptions) [LockoutOptions](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions) com valores padrão.</span><span class="sxs-lookup"><span data-stu-id="15259-129">The preceding code sets the [IdentityOptions](/dotnet/api/microsoft.aspnetcore.identity.identityoptions) [LockoutOptions](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions) with default values.</span></span>

<span data-ttu-id="15259-130">Uma autenticação bem-sucedida redefine a contagem de tentativas de acesso com falha e redefine o relógio.</span><span class="sxs-lookup"><span data-stu-id="15259-130">A successful authentication resets the failed access attempts count and resets the clock.</span></span>

<span data-ttu-id="15259-131">[IdentityOptions.Lockout](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.lockout) Especifica o [LockoutOptions](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions) com as propriedades mostradas na tabela.</span><span class="sxs-lookup"><span data-stu-id="15259-131">[IdentityOptions.Lockout](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.lockout) specifies the [LockoutOptions](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions) with the properties shown in the table.</span></span>

| <span data-ttu-id="15259-132">Propriedade</span><span class="sxs-lookup"><span data-stu-id="15259-132">Property</span></span> | <span data-ttu-id="15259-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="15259-133">Description</span></span> | <span data-ttu-id="15259-134">Padrão</span><span class="sxs-lookup"><span data-stu-id="15259-134">Default</span></span> |
| -------- | ----------- | :-----: |
| [<span data-ttu-id="15259-135">AllowedForNewUsers</span><span class="sxs-lookup"><span data-stu-id="15259-135">AllowedForNewUsers</span></span>](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.allowedfornewusers) | <span data-ttu-id="15259-136">Determina se um novo usuário poderá ser bloqueado.</span><span class="sxs-lookup"><span data-stu-id="15259-136">Determines if a new user can be locked out.</span></span> | `true` |
| [<span data-ttu-id="15259-137">DefaultLockoutTimeSpan</span><span class="sxs-lookup"><span data-stu-id="15259-137">DefaultLockoutTimeSpan</span></span>](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.defaultlockouttimespan) | <span data-ttu-id="15259-138">A quantidade de tempo um usuário está bloqueado quando ocorre um bloqueio.</span><span class="sxs-lookup"><span data-stu-id="15259-138">The amount of time a user is locked out when a lockout occurs.</span></span> | <span data-ttu-id="15259-139">5 minutos</span><span class="sxs-lookup"><span data-stu-id="15259-139">5 minutes</span></span> |
| [<span data-ttu-id="15259-140">MaxFailedAccessAttempts</span><span class="sxs-lookup"><span data-stu-id="15259-140">MaxFailedAccessAttempts</span></span>](/dotnet/api/microsoft.aspnetcore.identity.lockoutoptions.maxfailedaccessattempts) | <span data-ttu-id="15259-141">O número de tentativas de acesso com falha até que um usuário está bloqueado, se o bloqueio está habilitado.</span><span class="sxs-lookup"><span data-stu-id="15259-141">The number of failed access attempts until a user is locked out, if lockout is enabled.</span></span> | <span data-ttu-id="15259-142">5</span><span class="sxs-lookup"><span data-stu-id="15259-142">5</span></span> |

### <a name="password"></a><span data-ttu-id="15259-143">Senha</span><span class="sxs-lookup"><span data-stu-id="15259-143">Password</span></span>

<span data-ttu-id="15259-144">Por padrão, a identidade requer que as senhas conter um caractere maiusculo, caractere minúsculo, um dígito e um caractere não alfanumérico.</span><span class="sxs-lookup"><span data-stu-id="15259-144">By default, Identity requires that passwords contain an uppercase character, lowercase character, a digit, and a non-alphanumeric character.</span></span> <span data-ttu-id="15259-145">As senhas devem ter pelo menos seis caracteres.</span><span class="sxs-lookup"><span data-stu-id="15259-145">Passwords must be at least six characters long.</span></span> <span data-ttu-id="15259-146">[PasswordOptions](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions) podem ser definidas na `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="15259-146">[PasswordOptions](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions) can be set in `Startup.ConfigureServices`.</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](identity-configuration/sample/Startup.cs?name=snippet_pw)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-37,50-52)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-csharp[](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-65,84)]

::: moniker-end

<span data-ttu-id="15259-147">[IdentityOptions.Password](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.password) Especifica o [PasswordOptions](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions) com as propriedades mostradas na tabela.</span><span class="sxs-lookup"><span data-stu-id="15259-147">[IdentityOptions.Password](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.password) specifies the [PasswordOptions](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions) with the properties shown in the table.</span></span>

::: moniker range=">= aspnetcore-2.0"

| <span data-ttu-id="15259-148">Propriedade</span><span class="sxs-lookup"><span data-stu-id="15259-148">Property</span></span> | <span data-ttu-id="15259-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="15259-149">Description</span></span> | <span data-ttu-id="15259-150">Padrão</span><span class="sxs-lookup"><span data-stu-id="15259-150">Default</span></span> |
| -------- | ----------- | :-----: |
| [<span data-ttu-id="15259-151">RequireDigit</span><span class="sxs-lookup"><span data-stu-id="15259-151">RequireDigit</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requiredigit) | <span data-ttu-id="15259-152">Requer um número entre 0 a 9 na senha.</span><span class="sxs-lookup"><span data-stu-id="15259-152">Requires a number between 0-9 in the password.</span></span> | `true` |
| [<span data-ttu-id="15259-153">RequiredLength</span><span class="sxs-lookup"><span data-stu-id="15259-153">RequiredLength</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requiredlength) | <span data-ttu-id="15259-154">O comprimento mínimo da senha.</span><span class="sxs-lookup"><span data-stu-id="15259-154">The minimum length of the password.</span></span> | <span data-ttu-id="15259-155">6</span><span class="sxs-lookup"><span data-stu-id="15259-155">6</span></span> |
| [<span data-ttu-id="15259-156">RequireLowercase</span><span class="sxs-lookup"><span data-stu-id="15259-156">RequireLowercase</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requirelowercase) | <span data-ttu-id="15259-157">Requer um caractere minúsculo na senha.</span><span class="sxs-lookup"><span data-stu-id="15259-157">Requires a lowercase character in the password.</span></span> | `true` |
| [<span data-ttu-id="15259-158">RequireNonAlphanumeric</span><span class="sxs-lookup"><span data-stu-id="15259-158">RequireNonAlphanumeric</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requirenonalphanumeric) | <span data-ttu-id="15259-159">Requer um caractere não alfanuméricos na senha.</span><span class="sxs-lookup"><span data-stu-id="15259-159">Requires a non-alphanumeric character in the password.</span></span> | `true` |
| [<span data-ttu-id="15259-160">RequiredUniqueChars</span><span class="sxs-lookup"><span data-stu-id="15259-160">RequiredUniqueChars</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requireduniquechars) | <span data-ttu-id="15259-161">Só se aplica ao ASP.NET Core 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="15259-161">Only applies to ASP.NET Core 2.0 or later.</span></span><br><br> <span data-ttu-id="15259-162">Requer o número de caracteres distintas na senha.</span><span class="sxs-lookup"><span data-stu-id="15259-162">Requires the number of distinct characters in the password.</span></span> | <span data-ttu-id="15259-163">1</span><span class="sxs-lookup"><span data-stu-id="15259-163">1</span></span> |
| [<span data-ttu-id="15259-164">RequireUppercase</span><span class="sxs-lookup"><span data-stu-id="15259-164">RequireUppercase</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requireuppercase) | <span data-ttu-id="15259-165">Requer um caractere maiusculo na senha.</span><span class="sxs-lookup"><span data-stu-id="15259-165">Requires an uppercase character in the password.</span></span> | `true` |

::: moniker-end

::: moniker range="< aspnetcore-2.0"

| <span data-ttu-id="15259-166">Propriedade</span><span class="sxs-lookup"><span data-stu-id="15259-166">Property</span></span> | <span data-ttu-id="15259-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="15259-167">Description</span></span> | <span data-ttu-id="15259-168">Padrão</span><span class="sxs-lookup"><span data-stu-id="15259-168">Default</span></span> |
| -------- | ----------- | :-----: |
| [<span data-ttu-id="15259-169">RequireDigit</span><span class="sxs-lookup"><span data-stu-id="15259-169">RequireDigit</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requiredigit) | <span data-ttu-id="15259-170">Requer um número entre 0 a 9 na senha.</span><span class="sxs-lookup"><span data-stu-id="15259-170">Requires a number between 0-9 in the password.</span></span> | `true` |
| [<span data-ttu-id="15259-171">RequiredLength</span><span class="sxs-lookup"><span data-stu-id="15259-171">RequiredLength</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requiredlength) | <span data-ttu-id="15259-172">O comprimento mínimo da senha.</span><span class="sxs-lookup"><span data-stu-id="15259-172">The minimum length of the password.</span></span> | <span data-ttu-id="15259-173">6</span><span class="sxs-lookup"><span data-stu-id="15259-173">6</span></span> |
| [<span data-ttu-id="15259-174">RequireLowercase</span><span class="sxs-lookup"><span data-stu-id="15259-174">RequireLowercase</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requirelowercase) | <span data-ttu-id="15259-175">Requer um caractere minúsculo na senha.</span><span class="sxs-lookup"><span data-stu-id="15259-175">Requires a lowercase character in the password.</span></span> | `true` |
| [<span data-ttu-id="15259-176">RequireNonAlphanumeric</span><span class="sxs-lookup"><span data-stu-id="15259-176">RequireNonAlphanumeric</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requirenonalphanumeric) | <span data-ttu-id="15259-177">Requer um caractere não alfanuméricos na senha.</span><span class="sxs-lookup"><span data-stu-id="15259-177">Requires a non-alphanumeric character in the password.</span></span> | `true` |
| [<span data-ttu-id="15259-178">RequireUppercase</span><span class="sxs-lookup"><span data-stu-id="15259-178">RequireUppercase</span></span>](/dotnet/api/microsoft.aspnetcore.identity.passwordoptions.requireuppercase) | <span data-ttu-id="15259-179">Requer um caractere maiusculo na senha.</span><span class="sxs-lookup"><span data-stu-id="15259-179">Requires an uppercase character in the password.</span></span> | `true` |

::: moniker-end

### <a name="sign-in"></a><span data-ttu-id="15259-180">Entrar</span><span class="sxs-lookup"><span data-stu-id="15259-180">Sign-in</span></span>

<span data-ttu-id="15259-181">O seguinte código define `SignIn` configurações (para valores padrão):</span><span class="sxs-lookup"><span data-stu-id="15259-181">The following code sets `SignIn` settings (to default values):</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](identity-configuration/sample/Startup.cs?name=snippet_si)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?range=29-30,44-46,50-52)] 

::: moniker-end

<span data-ttu-id="15259-182">[IdentityOptions.SignIn](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.signin) Especifica o [SignInOptions](/dotnet/api/microsoft.aspnetcore.identity.signinoptions) com as propriedades mostradas na tabela.</span><span class="sxs-lookup"><span data-stu-id="15259-182">[IdentityOptions.SignIn](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.signin) specifies the [SignInOptions](/dotnet/api/microsoft.aspnetcore.identity.signinoptions) with the properties shown in the table.</span></span>

| <span data-ttu-id="15259-183">Propriedade</span><span class="sxs-lookup"><span data-stu-id="15259-183">Property</span></span> | <span data-ttu-id="15259-184">Descrição</span><span class="sxs-lookup"><span data-stu-id="15259-184">Description</span></span> | <span data-ttu-id="15259-185">Padrão</span><span class="sxs-lookup"><span data-stu-id="15259-185">Default</span></span> |
| -------- | ----------- | :-----: |
| [<span data-ttu-id="15259-186">RequireConfirmedEmail</span><span class="sxs-lookup"><span data-stu-id="15259-186">RequireConfirmedEmail</span></span>](/dotnet/api/microsoft.aspnetcore.identity.signinoptions.requireconfirmedemail) | <span data-ttu-id="15259-187">Requer um email confirmado para entrar.</span><span class="sxs-lookup"><span data-stu-id="15259-187">Requires a confirmed email to sign in.</span></span> | `false` |
| [<span data-ttu-id="15259-188">RequireConfirmedPhoneNumber</span><span class="sxs-lookup"><span data-stu-id="15259-188">RequireConfirmedPhoneNumber</span></span>](/dotnet/api/microsoft.aspnetcore.identity.signinoptions.requireconfirmedphonenumber) | <span data-ttu-id="15259-189">Requer um número de telefone confirmado entrar.</span><span class="sxs-lookup"><span data-stu-id="15259-189">Requires a confirmed phone number to sign in.</span></span> | `false` |

### <a name="tokens"></a><span data-ttu-id="15259-190">Tokens</span><span class="sxs-lookup"><span data-stu-id="15259-190">Tokens</span></span>

<span data-ttu-id="15259-191">[IdentityOptions.Tokens](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.tokens) Especifica o [TokenOptions](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions) com as propriedades mostradas na tabela.</span><span class="sxs-lookup"><span data-stu-id="15259-191">[IdentityOptions.Tokens](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.tokens) specifies the [TokenOptions](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions) with the properties shown in the table.</span></span>


|                                                        <span data-ttu-id="15259-192">Propriedade</span><span class="sxs-lookup"><span data-stu-id="15259-192">Property</span></span>                                                         |                                                                                      <span data-ttu-id="15259-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="15259-193">Description</span></span>                                                                                      |
|-------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     [<span data-ttu-id="15259-194">AuthenticatorTokenProvider</span><span class="sxs-lookup"><span data-stu-id="15259-194">AuthenticatorTokenProvider</span></span>](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.authenticatortokenprovider)     |                                       <span data-ttu-id="15259-195">Obtém ou define o `AuthenticatorTokenProvider` usado para validar entradas de dois fatores com um autenticador.</span><span class="sxs-lookup"><span data-stu-id="15259-195">Gets or sets the `AuthenticatorTokenProvider` used to validate two-factor sign-ins with an authenticator.</span></span>                                       |
|       [<span data-ttu-id="15259-196">ChangeEmailTokenProvider</span><span class="sxs-lookup"><span data-stu-id="15259-196">ChangeEmailTokenProvider</span></span>](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.changeemailtokenprovider)       |                                     <span data-ttu-id="15259-197">Obtém ou define o `ChangeEmailTokenProvider` usado para gerar tokens usados nos emails de confirmação de alteração de email.</span><span class="sxs-lookup"><span data-stu-id="15259-197">Gets or sets the `ChangeEmailTokenProvider` used to generate tokens used in email change confirmation emails.</span></span>                                     |
| [<span data-ttu-id="15259-198">ChangePhoneNumberTokenProvider</span><span class="sxs-lookup"><span data-stu-id="15259-198">ChangePhoneNumberTokenProvider</span></span>](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.changephonenumbertokenprovider) |                                      <span data-ttu-id="15259-199">Obtém ou define o `ChangePhoneNumberTokenProvider` usada para gerar tokens usados ao alterar os números de telefone.</span><span class="sxs-lookup"><span data-stu-id="15259-199">Gets or sets the `ChangePhoneNumberTokenProvider` used to generate tokens used when changing phone numbers.</span></span>                                      |
| [<span data-ttu-id="15259-200">EmailConfirmationTokenProvider</span><span class="sxs-lookup"><span data-stu-id="15259-200">EmailConfirmationTokenProvider</span></span>](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.emailconfirmationtokenprovider) |                                             <span data-ttu-id="15259-201">Obtém ou define o provedor de token usado para gerar tokens usados nos emails de confirmação de conta.</span><span class="sxs-lookup"><span data-stu-id="15259-201">Gets or sets the token provider used to generate tokens used in account confirmation emails.</span></span>                                              |
|     [<span data-ttu-id="15259-202">PasswordResetTokenProvider</span><span class="sxs-lookup"><span data-stu-id="15259-202">PasswordResetTokenProvider</span></span>](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.passwordresettokenprovider)     | <span data-ttu-id="15259-203">Obtém ou define o [IUserTwoFactorTokenProvider<TUser> ](/dotnet/api/microsoft.aspnetcore.identity.iusertwofactortokenprovider-1) usado para gerar tokens usados nos emails de redefinição de senha.</span><span class="sxs-lookup"><span data-stu-id="15259-203">Gets or sets the [IUserTwoFactorTokenProvider<TUser>](/dotnet/api/microsoft.aspnetcore.identity.iusertwofactortokenprovider-1) used to generate tokens used in password reset emails.</span></span> |
|                    [<span data-ttu-id="15259-204">ProviderMap</span><span class="sxs-lookup"><span data-stu-id="15259-204">ProviderMap</span></span>](/dotnet/api/microsoft.aspnetcore.identity.tokenoptions.providermap)                    |                <span data-ttu-id="15259-205">Usado para construir um [provedor de Token de usuário](/dotnet/api/microsoft.aspnetcore.identity.tokenproviderdescriptor) com a chave usada como o nome do provedor.</span><span class="sxs-lookup"><span data-stu-id="15259-205">Used to construct a [User Token Provider](/dotnet/api/microsoft.aspnetcore.identity.tokenproviderdescriptor) with the key used as the provider's name.</span></span>                 |

### <a name="user"></a><span data-ttu-id="15259-206">User</span><span class="sxs-lookup"><span data-stu-id="15259-206">User</span></span>

[!code-csharp[](identity-configuration/sample/Startup.cs?name=snippet_user)]

<span data-ttu-id="15259-207">[IdentityOptions.User](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.user) Especifica o [UserOptions](/dotnet/api/microsoft.aspnetcore.identity.useroptions) com as propriedades mostradas na tabela.</span><span class="sxs-lookup"><span data-stu-id="15259-207">[IdentityOptions.User](/dotnet/api/microsoft.aspnetcore.identity.identityoptions.user) specifies the [UserOptions](/dotnet/api/microsoft.aspnetcore.identity.useroptions) with the properties shown in the table.</span></span>

| <span data-ttu-id="15259-208">Propriedade</span><span class="sxs-lookup"><span data-stu-id="15259-208">Property</span></span> | <span data-ttu-id="15259-209">Descrição</span><span class="sxs-lookup"><span data-stu-id="15259-209">Description</span></span> | <span data-ttu-id="15259-210">Padrão</span><span class="sxs-lookup"><span data-stu-id="15259-210">Default</span></span> |
| -------- | ----------- | :-----: |
| [<span data-ttu-id="15259-211">AllowedUserNameCharacters</span><span class="sxs-lookup"><span data-stu-id="15259-211">AllowedUserNameCharacters</span></span>](/dotnet/api/microsoft.aspnetcore.identity.useroptions.allowedusernamecharacters) | <span data-ttu-id="15259-212">Caracteres permitidos no nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="15259-212">Allowed characters in the username.</span></span> | <span data-ttu-id="15259-213">abcdefghijklmnopqrstuvwxyz</span><span class="sxs-lookup"><span data-stu-id="15259-213">abcdefghijklmnopqrstuvwxyz</span></span><br><span data-ttu-id="15259-214">ABCDEFGHIJKLMNOPQRSTUVWXYZ</span><span class="sxs-lookup"><span data-stu-id="15259-214">ABCDEFGHIJKLMNOPQRSTUVWXYZ</span></span><br><span data-ttu-id="15259-215">0123456789</span><span class="sxs-lookup"><span data-stu-id="15259-215">0123456789</span></span><br><span data-ttu-id="15259-216">-.\_@+</span><span class="sxs-lookup"><span data-stu-id="15259-216">-.\_@+</span></span> |
| [<span data-ttu-id="15259-217">RequireUniqueEmail</span><span class="sxs-lookup"><span data-stu-id="15259-217">RequireUniqueEmail</span></span>](/dotnet/api/microsoft.aspnetcore.identity.useroptions.requireuniqueemail) | <span data-ttu-id="15259-218">Requer que cada usuário tenha um email exclusivo.</span><span class="sxs-lookup"><span data-stu-id="15259-218">Requires each user to have a unique email.</span></span> | `false` |

### <a name="cookie-settings"></a><span data-ttu-id="15259-219">Configurações de cookie</span><span class="sxs-lookup"><span data-stu-id="15259-219">Cookie settings</span></span>

<span data-ttu-id="15259-220">Configurar o cookie do aplicativo em `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="15259-220">Configure the app's cookie in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="15259-221">[ConfigureApplicationCookie](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.configureapplicationcookie#Microsoft_Extensions_DependencyInjection_IdentityServiceCollectionExtensions_ConfigureApplicationCookie_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Authentication_Cookies_CookieAuthenticationOptions__) deve ser chamado **após** chamando `AddIdentity` ou `AddDefaultIdentity`.</span><span class="sxs-lookup"><span data-stu-id="15259-221">[ConfigureApplicationCookie](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionextensions.configureapplicationcookie#Microsoft_Extensions_DependencyInjection_IdentityServiceCollectionExtensions_ConfigureApplicationCookie_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Authentication_Cookies_CookieAuthenticationOptions__) must be called **after** calling `AddIdentity` or `AddDefaultIdentity`.</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](identity-configuration/sample/Startup.cs?name=snippet_cookie)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](identity/sample/src/ASPNETv2-IdentityDemo-Configuration/Startup.cs?name=snippet_configurecookie)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-csharp[](identity/sample/src/ASPNET-IdentityDemo-PrimaryKeysConfig/Startup.cs?range=58-59,72-80,84)]

::: moniker-end

<span data-ttu-id="15259-222">Para obter mais informações, consulte [CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions).</span><span class="sxs-lookup"><span data-stu-id="15259-222">For more information, see [CookieAuthenticationOptions](/dotnet/api/microsoft.aspnetcore.authentication.cookies.cookieauthenticationoptions).</span></span>

## <a name="password-hasher-options"></a><span data-ttu-id="15259-223">Opções de Hasher de senha</span><span class="sxs-lookup"><span data-stu-id="15259-223">Password Hasher options</span></span>

<span data-ttu-id="15259-224"><xref:Microsoft.AspNetCore.Identity.PasswordHasherOptions> Obtém e define as opções de hash de senha.</span><span class="sxs-lookup"><span data-stu-id="15259-224"><xref:Microsoft.AspNetCore.Identity.PasswordHasherOptions> gets and sets options for password hashing.</span></span>

| <span data-ttu-id="15259-225">Opção</span><span class="sxs-lookup"><span data-stu-id="15259-225">Option</span></span> | <span data-ttu-id="15259-226">Descrição</span><span class="sxs-lookup"><span data-stu-id="15259-226">Description</span></span> |
| ------ | ----------- |
| <xref:Microsoft.AspNetCore.Identity.PasswordHasherOptions.CompatibilityMode> | <span data-ttu-id="15259-227">O modo de compatibilidade usado ao fazer hash de novas senhas.</span><span class="sxs-lookup"><span data-stu-id="15259-227">The compatibility mode used when hashing new passwords.</span></span> <span data-ttu-id="15259-228">Assume o padrão de <xref:Microsoft.AspNetCore.Identity.PasswordHasherCompatibilityMode.IdentityV3>.</span><span class="sxs-lookup"><span data-stu-id="15259-228">Defaults to <xref:Microsoft.AspNetCore.Identity.PasswordHasherCompatibilityMode.IdentityV3>.</span></span> <span data-ttu-id="15259-229">O primeiro byte de uma senha hash, chamado de um *marcador formato*, especifica a versão do algoritmo de hash usado para hash da senha.</span><span class="sxs-lookup"><span data-stu-id="15259-229">The first byte of a hashed password, called a *format marker*, specifies the version of the hashing algorithm used to hash the password.</span></span> <span data-ttu-id="15259-230">Ao verificar uma senha em relação a um hash, o <xref:Microsoft.AspNetCore.Identity.PasswordHasher`1.VerifyHashedPassword*> método seleciona o algoritmo correto com base no primeiro byte.</span><span class="sxs-lookup"><span data-stu-id="15259-230">When verifying a password against a hash, the <xref:Microsoft.AspNetCore.Identity.PasswordHasher`1.VerifyHashedPassword*> method selects the correct algorithm based on the first byte.</span></span> <span data-ttu-id="15259-231">Um cliente é capaz de autenticar, independentemente de qual versão do algoritmo foi usado para hash da senha.</span><span class="sxs-lookup"><span data-stu-id="15259-231">A client is able to authenticate regardless of which version of the algorithm was used to hash the password.</span></span> <span data-ttu-id="15259-232">Definindo o modo de compatibilidade afeta o hash de *novas senhas*.</span><span class="sxs-lookup"><span data-stu-id="15259-232">Setting the compatibility mode affects the hashing of *new passwords*.</span></span> |
| <xref:Microsoft.AspNetCore.Identity.PasswordHasherOptions.IterationCount> | <span data-ttu-id="15259-233">O número de iterações usadas ao fazer hash de senhas usando PBKDF2.</span><span class="sxs-lookup"><span data-stu-id="15259-233">The number of iterations used when hashing passwords using PBKDF2.</span></span> <span data-ttu-id="15259-234">Esse valor é usado apenas quando o <xref:Microsoft.AspNetCore.Identity.PasswordHasherOptions.CompatibilityMode> é definido como <xref:Microsoft.AspNetCore.Identity.PasswordHasherCompatibilityMode.IdentityV3>.</span><span class="sxs-lookup"><span data-stu-id="15259-234">This value is only used when the <xref:Microsoft.AspNetCore.Identity.PasswordHasherOptions.CompatibilityMode> is set to <xref:Microsoft.AspNetCore.Identity.PasswordHasherCompatibilityMode.IdentityV3>.</span></span> <span data-ttu-id="15259-235">O valor deve ser um inteiro positivo e assume como padrão `10000`.</span><span class="sxs-lookup"><span data-stu-id="15259-235">The value must be a positive integer and defaults to `10000`.</span></span> |

<span data-ttu-id="15259-236">No exemplo a seguir, o <xref:Microsoft.AspNetCore.Identity.PasswordHasherOptions.IterationCount> é definido como `12000` em `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="15259-236">In the following example, the <xref:Microsoft.AspNetCore.Identity.PasswordHasherOptions.IterationCount> is set to `12000` in `Startup.ConfigureServices`:</span></span>

```csharp
// using Microsoft.AspNetCore.Identity;

services.Configure<PasswordHasherOptions>(option =>
{
    option.IterationCount = 12000;
});
```
