---
title: Migrar autenticação e identidade para o ASP.NET Core 2.0
author: scottaddie
description: Este artigo descreve as etapas mais comuns para Migrando do ASP.NET Core 1.x autenticação e identidade para o ASP.NET Core 2.0.
ms.author: scaddie
ms.date: 12/18/2018
uid: migration/1x-to-2x/identity-2x
ms.openlocfilehash: d28b4af483c7ec9d6cff6db3e2f1693e765d4202
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063013"
---
# <a name="migrate-authentication-and-identity-to-aspnet-core-20"></a><span data-ttu-id="80ef2-103">Migrar autenticação e identidade para o ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="80ef2-103">Migrate authentication and Identity to ASP.NET Core 2.0</span></span>

<span data-ttu-id="80ef2-104">Por [Scott Addie](https://github.com/scottaddie) e [Kung Hao](https://github.com/HaoK)</span><span class="sxs-lookup"><span data-stu-id="80ef2-104">By [Scott Addie](https://github.com/scottaddie) and [Hao Kung](https://github.com/HaoK)</span></span>

<span data-ttu-id="80ef2-105">ASP.NET Core 2.0 tem um novo modelo para autenticação e [identidade](xref:security/authentication/identity) que simplifica a configuração por meio de serviços.</span><span class="sxs-lookup"><span data-stu-id="80ef2-105">ASP.NET Core 2.0 has a new model for authentication and [Identity](xref:security/authentication/identity) which simplifies configuration by using services.</span></span> <span data-ttu-id="80ef2-106">Aplicativos ASP.NET Core 1.x que usam autenticação ou a identidade podem ser atualizados para usar o novo modelo, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="80ef2-106">ASP.NET Core 1.x applications that use authentication or Identity can be updated to use the new model as outlined below.</span></span>

<a name="auth-middleware"></a>

## <a name="authentication-middleware-and-services"></a><span data-ttu-id="80ef2-107">Middleware de autenticação e serviços</span><span class="sxs-lookup"><span data-stu-id="80ef2-107">Authentication Middleware and services</span></span>
<span data-ttu-id="80ef2-108">Em projetos 1.x, a autenticação é configurada por meio do middleware.</span><span class="sxs-lookup"><span data-stu-id="80ef2-108">In 1.x projects, authentication is configured via middleware.</span></span> <span data-ttu-id="80ef2-109">Um método de middleware é invocado para cada esquema de autenticação que você deseja dar suporte.</span><span class="sxs-lookup"><span data-stu-id="80ef2-109">A middleware method is invoked for each authentication scheme you want to support.</span></span>

<span data-ttu-id="80ef2-110">O exemplo a seguir 1.x configura a autenticação do Facebook com identidade no *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="80ef2-110">The following 1.x example configures Facebook authentication with Identity in *Startup.cs*:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>();
}

public void Configure(IApplicationBuilder app, ILoggerFactory loggerfactory)
{
    app.UseIdentity();
    app.UseFacebookAuthentication(new FacebookOptions { 
        AppId = Configuration["auth:facebook:appid"],
        AppSecret = Configuration["auth:facebook:appsecret"]
    });
} 
```

<span data-ttu-id="80ef2-111">Em projetos do 2.0, a autenticação é configurada por meio de serviços.</span><span class="sxs-lookup"><span data-stu-id="80ef2-111">In 2.0 projects, authentication is configured via services.</span></span> <span data-ttu-id="80ef2-112">Cada esquema de autenticação é registrada na `ConfigureServices` método de *Startup.cs*.</span><span class="sxs-lookup"><span data-stu-id="80ef2-112">Each authentication scheme is registered in the `ConfigureServices` method of *Startup.cs*.</span></span> <span data-ttu-id="80ef2-113">O `UseIdentity` o método é substituído por `UseAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="80ef2-113">The `UseIdentity` method is replaced with `UseAuthentication`.</span></span>

<span data-ttu-id="80ef2-114">O exemplo a seguir 2.0 configura a autenticação do Facebook com identidade no *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="80ef2-114">The following 2.0 example configures Facebook authentication with Identity in *Startup.cs*:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddIdentity<ApplicationUser, IdentityRole>()
            .AddEntityFrameworkStores<ApplicationDbContext>();

    // If you want to tweak Identity cookies, they're no longer part of IdentityOptions.
    services.ConfigureApplicationCookie(options => options.LoginPath = "/Account/LogIn");
    services.AddAuthentication()
            .AddFacebook(options => 
            {
                options.AppId = Configuration["auth:facebook:appid"];
                options.AppSecret = Configuration["auth:facebook:appsecret"];
            });
}

public void Configure(IApplicationBuilder app, ILoggerFactory loggerfactory) {
    app.UseAuthentication();
}
```

<span data-ttu-id="80ef2-115">O `UseAuthentication` método adiciona um componente de middleware de autenticação único que é responsável pela autenticação automática e o tratamento de solicitações de autenticação remota.</span><span class="sxs-lookup"><span data-stu-id="80ef2-115">The `UseAuthentication` method adds a single authentication middleware component which is responsible for automatic authentication and the handling of remote authentication requests.</span></span> <span data-ttu-id="80ef2-116">Ele substitui todos os componentes de middleware individuais com um componente de middleware simples e comum.</span><span class="sxs-lookup"><span data-stu-id="80ef2-116">It replaces all of the individual middleware components with a single, common middleware component.</span></span>

<span data-ttu-id="80ef2-117">Veja abaixo as instruções de migração de 2.0 para cada esquema de autenticação principal.</span><span class="sxs-lookup"><span data-stu-id="80ef2-117">Below are 2.0 migration instructions for each major authentication scheme.</span></span>

### <a name="cookie-based-authentication"></a><span data-ttu-id="80ef2-118">Autenticação baseada em cookie</span><span class="sxs-lookup"><span data-stu-id="80ef2-118">Cookie-based authentication</span></span>
<span data-ttu-id="80ef2-119">Selecione uma das duas opções abaixo e faça as alterações necessárias na *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="80ef2-119">Select one of the two options below, and make the necessary changes in *Startup.cs*:</span></span>

1. <span data-ttu-id="80ef2-120">Usar cookies com identidade</span><span class="sxs-lookup"><span data-stu-id="80ef2-120">Use cookies with Identity</span></span>
    - <span data-ttu-id="80ef2-121">Substitua `UseIdentity` com `UseAuthentication` no `Configure` método:</span><span class="sxs-lookup"><span data-stu-id="80ef2-121">Replace `UseIdentity` with `UseAuthentication` in the `Configure` method:</span></span>

        ```csharp
        app.UseAuthentication();
        ```

    - <span data-ttu-id="80ef2-122">Invocar o `AddIdentity` método no `ConfigureServices` método para adicionar os serviços de autenticação de cookie.</span><span class="sxs-lookup"><span data-stu-id="80ef2-122">Invoke the `AddIdentity` method in the `ConfigureServices` method to add the cookie authentication services.</span></span>
    - <span data-ttu-id="80ef2-123">Opcionalmente, invocar o `ConfigureApplicationCookie` ou `ConfigureExternalCookie` método no `ConfigureServices` método ajustar as configurações de cookie de identidade.</span><span class="sxs-lookup"><span data-stu-id="80ef2-123">Optionally, invoke the `ConfigureApplicationCookie` or `ConfigureExternalCookie` method in the `ConfigureServices` method to tweak the Identity cookie settings.</span></span>

        ```csharp
        services.AddIdentity<ApplicationUser, IdentityRole>()
                .AddEntityFrameworkStores<ApplicationDbContext>()
                .AddDefaultTokenProviders();
    
        services.ConfigureApplicationCookie(options => options.LoginPath = "/Account/LogIn");
        ```

2. <span data-ttu-id="80ef2-124">Usar cookies sem o Identity</span><span class="sxs-lookup"><span data-stu-id="80ef2-124">Use cookies without Identity</span></span>
    - <span data-ttu-id="80ef2-125">Substitua os `UseCookieAuthentication` chamada de método na `Configure` método com `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="80ef2-125">Replace the `UseCookieAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
  
        ```csharp
        app.UseAuthentication();
        ```
 
    - <span data-ttu-id="80ef2-126">Invocar o `AddAuthentication` e `AddCookie` métodos no `ConfigureServices` método:</span><span class="sxs-lookup"><span data-stu-id="80ef2-126">Invoke the `AddAuthentication` and `AddCookie` methods in the `ConfigureServices` method:</span></span>

        ```csharp
        // If you don't want the cookie to be automatically authenticated and assigned to HttpContext.User, 
        // remove the CookieAuthenticationDefaults.AuthenticationScheme parameter passed to AddAuthentication.
        services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
                .AddCookie(options => 
                {
                    options.LoginPath = "/Account/LogIn";
                    options.LogoutPath = "/Account/LogOff";
                });
        ```

### <a name="jwt-bearer-authentication"></a><span data-ttu-id="80ef2-127">JWT Bearer Authentication</span><span class="sxs-lookup"><span data-stu-id="80ef2-127">JWT Bearer Authentication</span></span>
<span data-ttu-id="80ef2-128">Faça as seguintes alterações na *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="80ef2-128">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="80ef2-129">Substitua os `UseJwtBearerAuthentication` chamada de método na `Configure` método com `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="80ef2-129">Replace the `UseJwtBearerAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
 
    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="80ef2-130">Invocar o `AddJwtBearer` método no `ConfigureServices` método:</span><span class="sxs-lookup"><span data-stu-id="80ef2-130">Invoke the `AddJwtBearer` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
            .AddJwtBearer(options => 
            {
                options.Audience = "http://localhost:5001/";
                options.Authority = "http://localhost:5000/";
            });
    ```

    <span data-ttu-id="80ef2-131">Este trecho de código não usa a identidade, portanto, o esquema padrão deve ser definido, passando `JwtBearerDefaults.AuthenticationScheme` para o `AddAuthentication` método.</span><span class="sxs-lookup"><span data-stu-id="80ef2-131">This code snippet doesn't use Identity, so the default scheme should be set by passing `JwtBearerDefaults.AuthenticationScheme` to the `AddAuthentication` method.</span></span>

### <a name="openid-connect-oidc-authentication"></a><span data-ttu-id="80ef2-132">Autenticação OIDC (OpenID Connect)</span><span class="sxs-lookup"><span data-stu-id="80ef2-132">OpenID Connect (OIDC) authentication</span></span>
<span data-ttu-id="80ef2-133">Faça as seguintes alterações na *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="80ef2-133">Make the following changes in *Startup.cs*:</span></span>

- <span data-ttu-id="80ef2-134">Substitua os `UseOpenIdConnectAuthentication` chamada de método na `Configure` método com `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="80ef2-134">Replace the `UseOpenIdConnectAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>

    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="80ef2-135">Invocar o `AddOpenIdConnect` método no `ConfigureServices` método:</span><span class="sxs-lookup"><span data-stu-id="80ef2-135">Invoke the `AddOpenIdConnect` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication(options => 
    {
        options.DefaultScheme = CookieAuthenticationDefaults.AuthenticationScheme;
        options.DefaultChallengeScheme = OpenIdConnectDefaults.AuthenticationScheme;
    })
    .AddCookie()
    .AddOpenIdConnect(options => 
    {
        options.Authority = Configuration["auth:oidc:authority"];
        options.ClientId = Configuration["auth:oidc:clientid"];
    });
    ```

### <a name="facebook-authentication"></a><span data-ttu-id="80ef2-136">Autenticação do Facebook</span><span class="sxs-lookup"><span data-stu-id="80ef2-136">Facebook authentication</span></span>
<span data-ttu-id="80ef2-137">Faça as seguintes alterações na *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="80ef2-137">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="80ef2-138">Substitua os `UseFacebookAuthentication` chamada de método na `Configure` método com `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="80ef2-138">Replace the `UseFacebookAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
 
    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="80ef2-139">Invocar o `AddFacebook` método no `ConfigureServices` método:</span><span class="sxs-lookup"><span data-stu-id="80ef2-139">Invoke the `AddFacebook` method in the `ConfigureServices` method:</span></span>
    
    ```csharp
    services.AddAuthentication()
            .AddFacebook(options => 
            {
                options.AppId = Configuration["auth:facebook:appid"];
                options.AppSecret = Configuration["auth:facebook:appsecret"];
            });
    ```

### <a name="google-authentication"></a><span data-ttu-id="80ef2-140">Autenticação do Google</span><span class="sxs-lookup"><span data-stu-id="80ef2-140">Google authentication</span></span>
<span data-ttu-id="80ef2-141">Faça as seguintes alterações na *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="80ef2-141">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="80ef2-142">Substitua os `UseGoogleAuthentication` chamada de método na `Configure` método com `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="80ef2-142">Replace the `UseGoogleAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
 
    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="80ef2-143">Invocar o `AddGoogle` método no `ConfigureServices` método:</span><span class="sxs-lookup"><span data-stu-id="80ef2-143">Invoke the `AddGoogle` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication()
            .AddGoogle(options => 
            {
                options.ClientId = Configuration["auth:google:clientid"];
                options.ClientSecret = Configuration["auth:google:clientsecret"];
            });    
    ```

### <a name="microsoft-account-authentication"></a><span data-ttu-id="80ef2-144">Autenticação da Microsoft Account</span><span class="sxs-lookup"><span data-stu-id="80ef2-144">Microsoft Account authentication</span></span>
<span data-ttu-id="80ef2-145">Faça as seguintes alterações na *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="80ef2-145">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="80ef2-146">Substitua os `UseMicrosoftAccountAuthentication` chamada de método na `Configure` método com `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="80ef2-146">Replace the `UseMicrosoftAccountAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>

    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="80ef2-147">Invocar o `AddMicrosoftAccount` método no `ConfigureServices` método:</span><span class="sxs-lookup"><span data-stu-id="80ef2-147">Invoke the `AddMicrosoftAccount` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication()
            .AddMicrosoftAccount(options => 
            {
                options.ClientId = Configuration["auth:microsoft:clientid"];
                options.ClientSecret = Configuration["auth:microsoft:clientsecret"];
            });
    ``` 

### <a name="twitter-authentication"></a><span data-ttu-id="80ef2-148">Autenticação do Twitter</span><span class="sxs-lookup"><span data-stu-id="80ef2-148">Twitter authentication</span></span>
<span data-ttu-id="80ef2-149">Faça as seguintes alterações na *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="80ef2-149">Make the following changes in *Startup.cs*:</span></span>
- <span data-ttu-id="80ef2-150">Substitua os `UseTwitterAuthentication` chamada de método na `Configure` método com `UseAuthentication`:</span><span class="sxs-lookup"><span data-stu-id="80ef2-150">Replace the `UseTwitterAuthentication` method call in the `Configure` method with `UseAuthentication`:</span></span>
 
    ```csharp
    app.UseAuthentication();
    ```

- <span data-ttu-id="80ef2-151">Invocar o `AddTwitter` método no `ConfigureServices` método:</span><span class="sxs-lookup"><span data-stu-id="80ef2-151">Invoke the `AddTwitter` method in the `ConfigureServices` method:</span></span>

    ```csharp
    services.AddAuthentication()
            .AddTwitter(options => 
            {
                options.ConsumerKey = Configuration["auth:twitter:consumerkey"];
                options.ConsumerSecret = Configuration["auth:twitter:consumersecret"];
            });
    ```

### <a name="setting-default-authentication-schemes"></a><span data-ttu-id="80ef2-152">Esquemas de autenticação padrão de configuração</span><span class="sxs-lookup"><span data-stu-id="80ef2-152">Setting default authentication schemes</span></span>
<span data-ttu-id="80ef2-153">No 1.x, o `AutomaticAuthenticate` e `AutomaticChallenge` propriedades da [AuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.AuthenticationOptions?view=aspnetcore-1.1) classe base foram deve ser definida em um esquema de autenticação.</span><span class="sxs-lookup"><span data-stu-id="80ef2-153">In 1.x, the `AutomaticAuthenticate` and `AutomaticChallenge` properties of the [AuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.AuthenticationOptions?view=aspnetcore-1.1) base class were intended to be set on a single authentication scheme.</span></span> <span data-ttu-id="80ef2-154">Não havia nenhuma boa maneira para impor isso.</span><span class="sxs-lookup"><span data-stu-id="80ef2-154">There was no good way to enforce this.</span></span>

<span data-ttu-id="80ef2-155">No 2.0, essas duas propriedades foram removidas como propriedades individual `AuthenticationOptions` instância.</span><span class="sxs-lookup"><span data-stu-id="80ef2-155">In 2.0, these two properties have been removed as properties on the individual `AuthenticationOptions` instance.</span></span> <span data-ttu-id="80ef2-156">Eles podem ser configurados na `AddAuthentication` chamada de método dentro a `ConfigureServices` método de *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="80ef2-156">They can be configured in the `AddAuthentication` method call within the `ConfigureServices` method of *Startup.cs*:</span></span>

```csharp
services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme);
```

<span data-ttu-id="80ef2-157">No trecho de código anterior, o esquema padrão é definido como `CookieAuthenticationDefaults.AuthenticationScheme` ("Cookies").</span><span class="sxs-lookup"><span data-stu-id="80ef2-157">In the preceding code snippet, the default scheme is set to `CookieAuthenticationDefaults.AuthenticationScheme` ("Cookies").</span></span>

<span data-ttu-id="80ef2-158">Como alternativa, use uma versão sobrecarregada do `AddAuthentication` método para definir mais de uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="80ef2-158">Alternatively, use an overloaded version of the `AddAuthentication` method to set more than one property.</span></span> <span data-ttu-id="80ef2-159">No exemplo a seguir o método sobrecarregado, o esquema padrão é definido como `CookieAuthenticationDefaults.AuthenticationScheme`.</span><span class="sxs-lookup"><span data-stu-id="80ef2-159">In the following overloaded method example, the default scheme is set to `CookieAuthenticationDefaults.AuthenticationScheme`.</span></span> <span data-ttu-id="80ef2-160">O esquema de autenticação como alternativa, pode ser especificado dentro de seu indivíduo `[Authorize]` atributos ou as políticas de autorização.</span><span class="sxs-lookup"><span data-stu-id="80ef2-160">The authentication scheme may alternatively be specified within your individual `[Authorize]` attributes or authorization policies.</span></span>

```csharp
services.AddAuthentication(options => 
{
    options.DefaultScheme = CookieAuthenticationDefaults.AuthenticationScheme;
    options.DefaultChallengeScheme = OpenIdConnectDefaults.AuthenticationScheme;
});
```

<span data-ttu-id="80ef2-161">Defina um esquema padrão do 2.0, se uma das seguintes condições for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="80ef2-161">Define a default scheme in 2.0 if one of the following conditions is true:</span></span>
- <span data-ttu-id="80ef2-162">Você deseja que o usuário a ser conectado automaticamente</span><span class="sxs-lookup"><span data-stu-id="80ef2-162">You want the user to be automatically signed in</span></span>
- <span data-ttu-id="80ef2-163">Você usa o `[Authorize]` políticas de autorização ou atributo sem especificar esquemas</span><span class="sxs-lookup"><span data-stu-id="80ef2-163">You use the `[Authorize]` attribute or authorization policies without specifying schemes</span></span>

<span data-ttu-id="80ef2-164">Uma exceção a essa regra é o `AddIdentity` método.</span><span class="sxs-lookup"><span data-stu-id="80ef2-164">An exception to this rule is the `AddIdentity` method.</span></span> <span data-ttu-id="80ef2-165">Esse método adiciona cookies para você e define o padrão autenticar e esquemas de desafio para o cookie do aplicativo `IdentityConstants.ApplicationScheme`.</span><span class="sxs-lookup"><span data-stu-id="80ef2-165">This method adds cookies for you and sets the default authenticate and challenge schemes to the application cookie `IdentityConstants.ApplicationScheme`.</span></span> <span data-ttu-id="80ef2-166">Além disso, ele define o esquema de entrada padrão para o cookie externo `IdentityConstants.ExternalScheme`.</span><span class="sxs-lookup"><span data-stu-id="80ef2-166">Additionally, it sets the default sign-in scheme to the external cookie `IdentityConstants.ExternalScheme`.</span></span>

<a name="obsolete-interface"></a>

## <a name="use-httpcontext-authentication-extensions"></a><span data-ttu-id="80ef2-167">Usar extensões de autenticação HttpContext</span><span class="sxs-lookup"><span data-stu-id="80ef2-167">Use HttpContext authentication extensions</span></span>
<span data-ttu-id="80ef2-168">O `IAuthenticationManager` interface é o ponto de entrada principal para o sistema de autenticação de 1. x.</span><span class="sxs-lookup"><span data-stu-id="80ef2-168">The `IAuthenticationManager` interface is the main entry point into the 1.x authentication system.</span></span> <span data-ttu-id="80ef2-169">Ele foi substituído por um novo conjunto de `HttpContext` métodos de extensão no `Microsoft.AspNetCore.Authentication` namespace.</span><span class="sxs-lookup"><span data-stu-id="80ef2-169">It has been replaced with a new set of `HttpContext` extension methods in the `Microsoft.AspNetCore.Authentication` namespace.</span></span>

<span data-ttu-id="80ef2-170">Por exemplo, projetos do 1.x referência um `Authentication` propriedade:</span><span class="sxs-lookup"><span data-stu-id="80ef2-170">For example, 1.x projects reference an `Authentication` property:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Controllers/AccountController.cs?name=snippet_AuthenticationProperty)]

<span data-ttu-id="80ef2-171">Em 2.0 projetos, importe as `Microsoft.AspNetCore.Authentication` namespace e exclua o `Authentication` referências de propriedade:</span><span class="sxs-lookup"><span data-stu-id="80ef2-171">In 2.0 projects, import the `Microsoft.AspNetCore.Authentication` namespace, and delete the `Authentication` property references:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Controllers/AccountController.cs?name=snippet_AuthenticationProperty)]

<a name="windows-auth-changes"></a>

## <a name="windows-authentication-httpsys--iisintegration"></a><span data-ttu-id="80ef2-172">Autenticação do Windows (http. sys / IISIntegration)</span><span class="sxs-lookup"><span data-stu-id="80ef2-172">Windows Authentication (HTTP.sys / IISIntegration)</span></span>
<span data-ttu-id="80ef2-173">Há duas variações de autenticação do Windows:</span><span class="sxs-lookup"><span data-stu-id="80ef2-173">There are two variations of Windows authentication:</span></span>
1. <span data-ttu-id="80ef2-174">O host permite que somente usuários autenticados</span><span class="sxs-lookup"><span data-stu-id="80ef2-174">The host only allows authenticated users</span></span>
2. <span data-ttu-id="80ef2-175">O host permite que ambos anônimos e usuários autenticados</span><span class="sxs-lookup"><span data-stu-id="80ef2-175">The host allows both anonymous and authenticated users</span></span>

<span data-ttu-id="80ef2-176">A primeira descrita acima não é afetada pelas alterações de 2.0.</span><span class="sxs-lookup"><span data-stu-id="80ef2-176">The first variation described above is unaffected by the 2.0 changes.</span></span>

<span data-ttu-id="80ef2-177">A segunda descrita acima é afetada pelas alterações de 2.0.</span><span class="sxs-lookup"><span data-stu-id="80ef2-177">The second variation described above is affected by the 2.0 changes.</span></span> <span data-ttu-id="80ef2-178">Por exemplo, você pode ser permitir que usuários anônimos em seu aplicativo no IIS ou [HTTP. sys](xref:fundamentals/servers/httpsys) mas autorizar usuários no nível do controlador de camada.</span><span class="sxs-lookup"><span data-stu-id="80ef2-178">As an example, you may be allowing anonymous users into your app at the IIS or [HTTP.sys](xref:fundamentals/servers/httpsys) layer but authorizing users at the Controller level.</span></span> <span data-ttu-id="80ef2-179">Nesse cenário, defina o esquema padrão `IISDefaults.AuthenticationScheme` no `Startup.ConfigureServices` método:</span><span class="sxs-lookup"><span data-stu-id="80ef2-179">In this scenario, set the default scheme to `IISDefaults.AuthenticationScheme` in the `Startup.ConfigureServices` method:</span></span>

```csharp
services.AddAuthentication(IISDefaults.AuthenticationScheme);
```

<span data-ttu-id="80ef2-180">Falha ao definir o esquema padrão adequadamente impede que a solicitação de autorização de desafio do trabalho.</span><span class="sxs-lookup"><span data-stu-id="80ef2-180">Failure to set the default scheme accordingly prevents the authorize request to challenge from working.</span></span>

<a name="identity-cookie-options"></a>

## <a name="identitycookieoptions-instances"></a><span data-ttu-id="80ef2-181">Instâncias de IdentityCookieOptions</span><span class="sxs-lookup"><span data-stu-id="80ef2-181">IdentityCookieOptions instances</span></span>
<span data-ttu-id="80ef2-182">Um efeito colateral das 2.0 alterações é o comutador que usa o chamado opções em vez de instâncias de opções de cookie.</span><span class="sxs-lookup"><span data-stu-id="80ef2-182">A side effect of the 2.0 changes is the switch to using named options instead of cookie options instances.</span></span> <span data-ttu-id="80ef2-183">A capacidade de personalizar os nomes de esquema do cookie de identidade é removida.</span><span class="sxs-lookup"><span data-stu-id="80ef2-183">The ability to customize the Identity cookie scheme names is removed.</span></span>

<span data-ttu-id="80ef2-184">Por exemplo, 1. x projetos usam [injeção de construtor](xref:mvc/controllers/dependency-injection#constructor-injection) para passar um `IdentityCookieOptions` parâmetro em *AccountController.cs*.</span><span class="sxs-lookup"><span data-stu-id="80ef2-184">For example, 1.x projects use [constructor injection](xref:mvc/controllers/dependency-injection#constructor-injection) to pass an `IdentityCookieOptions` parameter into *AccountController.cs*.</span></span> <span data-ttu-id="80ef2-185">O esquema de autenticação de cookie externa é acessado da instância fornecida:</span><span class="sxs-lookup"><span data-stu-id="80ef2-185">The external cookie authentication scheme is accessed from the provided instance:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Controllers/AccountController.cs?name=snippet_AccountControllerConstructor&highlight=4,11)]

<span data-ttu-id="80ef2-186">A injeção de construtor mencionados anteriormente se torna desnecessária em 2.0 projetos e o `_externalCookieScheme` campo pode ser excluído:</span><span class="sxs-lookup"><span data-stu-id="80ef2-186">The aforementioned constructor injection becomes unnecessary in 2.0 projects, and the `_externalCookieScheme` field can be deleted:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Controllers/AccountController.cs?name=snippet_AccountControllerConstructor)]

<span data-ttu-id="80ef2-187">O `IdentityConstants.ExternalScheme` constante pode ser usada diretamente:</span><span class="sxs-lookup"><span data-stu-id="80ef2-187">The `IdentityConstants.ExternalScheme` constant can be used directly:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Controllers/AccountController.cs?name=snippet_AuthenticationProperty)]

<a name="navigation-properties"></a>

## <a name="add-identityuser-poco-navigation-properties"></a><span data-ttu-id="80ef2-188">Adicionar propriedades de navegação IdentityUser POCO</span><span class="sxs-lookup"><span data-stu-id="80ef2-188">Add IdentityUser POCO navigation properties</span></span>
<span data-ttu-id="80ef2-189">As propriedades de navegação do Entity Framework (EF) Core da base de `IdentityUser` POCO (objeto Plain Old CLR) foram removidos.</span><span class="sxs-lookup"><span data-stu-id="80ef2-189">The Entity Framework (EF) Core navigation properties of the base `IdentityUser` POCO (Plain Old CLR Object) have been removed.</span></span> <span data-ttu-id="80ef2-190">Se seu projeto 1.x usou essas propriedades, manualmente adicione ao projeto 2.0:</span><span class="sxs-lookup"><span data-stu-id="80ef2-190">If your 1.x project used these properties, manually add them back to the 2.0 project:</span></span>

```csharp
/// <summary>
/// Navigation property for the roles this user belongs to.
/// </summary>
public virtual ICollection<IdentityUserRole<int>> Roles { get; } = new List<IdentityUserRole<int>>();

/// <summary>
/// Navigation property for the claims this user possesses.
/// </summary>
public virtual ICollection<IdentityUserClaim<int>> Claims { get; } = new List<IdentityUserClaim<int>>();

/// <summary>
/// Navigation property for this users login accounts.
/// </summary>
public virtual ICollection<IdentityUserLogin<int>> Logins { get; } = new List<IdentityUserLogin<int>>();
```

<span data-ttu-id="80ef2-191">Para impedir que as chaves estrangeiras duplicadas ao executar migrações do EF Core, adicione o seguinte ao seu `IdentityDbContext` classe `OnModelCreating` método (depois que o `base.OnModelCreating();` chamar):</span><span class="sxs-lookup"><span data-stu-id="80ef2-191">To prevent duplicate foreign keys when running EF Core Migrations, add the following to your `IdentityDbContext` class' `OnModelCreating` method (after the `base.OnModelCreating();` call):</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder builder)
{
    base.OnModelCreating(builder);
    // Customize the ASP.NET Core Identity model and override the defaults if needed.
    // For example, you can rename the ASP.NET Core Identity table names and more.
    // Add your customizations after calling base.OnModelCreating(builder);

    builder.Entity<ApplicationUser>()
        .HasMany(e => e.Claims)
        .WithOne()
        .HasForeignKey(e => e.UserId)
        .IsRequired()
        .OnDelete(DeleteBehavior.Cascade);

    builder.Entity<ApplicationUser>()
        .HasMany(e => e.Logins)
        .WithOne()
        .HasForeignKey(e => e.UserId)
        .IsRequired()
        .OnDelete(DeleteBehavior.Cascade);

    builder.Entity<ApplicationUser>()
        .HasMany(e => e.Roles)
        .WithOne()
        .HasForeignKey(e => e.UserId)
        .IsRequired()
        .OnDelete(DeleteBehavior.Cascade);
}
```

<a name="synchronous-method-removal"></a>

## <a name="replace-getexternalauthenticationschemes"></a><span data-ttu-id="80ef2-192">Substituir GetExternalAuthenticationSchemes</span><span class="sxs-lookup"><span data-stu-id="80ef2-192">Replace GetExternalAuthenticationSchemes</span></span>
<span data-ttu-id="80ef2-193">O método síncrono `GetExternalAuthenticationSchemes` foi removido para uma versão assíncrona.</span><span class="sxs-lookup"><span data-stu-id="80ef2-193">The synchronous method `GetExternalAuthenticationSchemes` was removed in favor of an asynchronous version.</span></span> <span data-ttu-id="80ef2-194">projetos do 1.x tem o seguinte código *ManageController.cs*:</span><span class="sxs-lookup"><span data-stu-id="80ef2-194">1.x projects have the following code in *ManageController.cs*:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Controllers/ManageController.cs?name=snippet_GetExternalAuthenticationSchemes)]

<span data-ttu-id="80ef2-195">Este método é exibido no *cshtml* muito:</span><span class="sxs-lookup"><span data-stu-id="80ef2-195">This method appears in *Login.cshtml* too:</span></span>

[!code-cshtml[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Views/Account/Login.cshtml?range=62,75-84)]

<span data-ttu-id="80ef2-196">Em projetos do 2.0, use o `GetExternalAuthenticationSchemesAsync` método:</span><span class="sxs-lookup"><span data-stu-id="80ef2-196">In 2.0 projects, use the `GetExternalAuthenticationSchemesAsync` method:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Controllers/ManageController.cs?name=snippet_GetExternalAuthenticationSchemesAsync)]

<span data-ttu-id="80ef2-197">Na *cshtml*, o `AuthenticationScheme` propriedade acessada no `foreach` loop é alterado para `Name`:</span><span class="sxs-lookup"><span data-stu-id="80ef2-197">In *Login.cshtml*, the `AuthenticationScheme` property accessed in the `foreach` loop changes to `Name`:</span></span>

[!code-cshtml[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Views/Account/Login.cshtml?range=62,75-84)]

<a name="property-change"></a>

## <a name="manageloginsviewmodel-property-change"></a><span data-ttu-id="80ef2-198">Alteração da propriedade ManageLoginsViewModel</span><span class="sxs-lookup"><span data-stu-id="80ef2-198">ManageLoginsViewModel property change</span></span>
<span data-ttu-id="80ef2-199">Um `ManageLoginsViewModel` objeto é usado em de `ManageLogins` ação de *ManageController.cs*.</span><span class="sxs-lookup"><span data-stu-id="80ef2-199">A `ManageLoginsViewModel` object is used in the `ManageLogins` action of *ManageController.cs*.</span></span> <span data-ttu-id="80ef2-200">Em projetos 1.x, o objeto `OtherLogins` propriedade de tipo de retorno é `IList<AuthenticationDescription>`.</span><span class="sxs-lookup"><span data-stu-id="80ef2-200">In 1.x projects, the object's `OtherLogins` property return type is `IList<AuthenticationDescription>`.</span></span> <span data-ttu-id="80ef2-201">Esse tipo de retorno requer uma importação de `Microsoft.AspNetCore.Http.Authentication`:</span><span class="sxs-lookup"><span data-stu-id="80ef2-201">This return type requires an import of `Microsoft.AspNetCore.Http.Authentication`:</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore1App/AspNetCoreDotNetCore1App/Models/ManageViewModels/ManageLoginsViewModel.cs?name=snippet_ManageLoginsViewModel&highlight=2,11)]

<span data-ttu-id="80ef2-202">Em projetos do 2.0, o tipo de retorno é alterado para `IList<AuthenticationScheme>`.</span><span class="sxs-lookup"><span data-stu-id="80ef2-202">In 2.0 projects, the return type changes to `IList<AuthenticationScheme>`.</span></span> <span data-ttu-id="80ef2-203">Esse novo tipo de retorno requer substituindo o `Microsoft.AspNetCore.Http.Authentication` importação de um `Microsoft.AspNetCore.Authentication` importar.</span><span class="sxs-lookup"><span data-stu-id="80ef2-203">This new return type requires replacing the `Microsoft.AspNetCore.Http.Authentication` import with a `Microsoft.AspNetCore.Authentication` import.</span></span>

[!code-csharp[](../1x-to-2x/samples/AspNetCoreDotNetCore2App/AspNetCoreDotNetCore2App/Models/ManageViewModels/ManageLoginsViewModel.cs?name=snippet_ManageLoginsViewModel&highlight=2,11)]

<a name="additional-resources"></a>

## <a name="additional-resources"></a><span data-ttu-id="80ef2-204">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="80ef2-204">Additional resources</span></span>
<span data-ttu-id="80ef2-205">Para obter mais detalhes e discussões, consulte o [discussão do Auth 2.0](https://github.com/aspnet/Security/issues/1338) problema no GitHub.</span><span class="sxs-lookup"><span data-stu-id="80ef2-205">For additional details and discussion, see the [Discussion for Auth 2.0](https://github.com/aspnet/Security/issues/1338) issue on GitHub.</span></span>
