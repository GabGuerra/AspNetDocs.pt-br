---
title: Acessar o HttpContext no ASP.NET Core
author: coderandhiker
description: Saiba como acessar o HttpContext no ASP.NET Core.
ms.author: riande
ms.custom: mvc
ms.date: 07/27/2018
uid: fundamentals/httpcontext
ms.openlocfilehash: 446882297524af3cbaed3ba7f941935debf5e7f4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026423"
---
# <a name="access-httpcontext-in-aspnet-core"></a>Acessar o HttpContext no ASP.NET Core

Os aplicativos ASP.NET Core acessam o `HttpContext` por meio da interface [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) e da implementação padrão do [HttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.httpcontextaccessor). Só é necessário usar o `IHttpContextAccessor` quando você precisar acessar o `HttpContext` em um serviço.

::: moniker range=">= aspnetcore-2.0"

## <a name="use-httpcontext-from-razor-pages"></a>Usar o HttpContext de Razor Pages

O [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) das Razor Pages expõe a propriedade [HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.httpcontext):

```csharp
public class AboutModel : PageModel
{
    public string Message { get; set; }

    public void OnGet()
    {
        Message = HttpContext.Request.PathBase;
    }
}
```

::: moniker-end

## <a name="use-httpcontext-from-a-razor-view"></a>Usar o HttpContext de uma exibição do Razor

As exibições do Razor expõem o `HttpContext` diretamente por meio de uma propriedade [RazorPage.Context](/dotnet/api/microsoft.aspnetcore.mvc.razor.razorpage.context#Microsoft_AspNetCore_Mvc_Razor_RazorPage_Context) na exibição. O exemplo a seguir recupera o nome de usuário atual em um aplicativo de Intranet usando a Autenticação do Windows:

```cshtml
@{
    var username = Context.User.Identity.Name;
}
```

## <a name="use-httpcontext-from-a-controller"></a>Usar o HttpContext de um controlador

Os controladores expõem a propriedade [ControllerBase.HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.httpcontext):

```csharp
public class HomeController : Controller
{
    public IActionResult About()
    {
        var pathBase = HttpContext.Request.PathBase;
        // Do something with the PathBase.

        return View();
    }
}
```

## <a name="use-httpcontext-from-middleware"></a>Usar o HttpContext de middleware

Ao trabalhar com componentes personalizados de middleware, o `HttpContext` é passado para o método `Invoke` ou `InvokeAsync` e pode ser acessado quando o middleware for configurado:

```csharp
public class MyCustomMiddleware
{
    public Task InvokeAsync(HttpContext context)
    {
        // Middleware initialization optionally using HttpContext
    }
}
```

## <a name="use-httpcontext-from-custom-components"></a>Usar o HttpContext de componentes personalizados

Para outras estruturas e componentes personalizados que exigem acesso ao `HttpContext`, a abordagem recomendada é registrar uma dependência usando o contêiner integrado de [injeção de dependência](xref:fundamentals/dependency-injection). O contêiner de injeção de dependência fornece o `IHttpContextAccessor` para todas as classes que o declaram como uma dependência em seus construtores.

::: moniker range=">= aspnetcore-2.1"

```csharp
public void ConfigureServices(IServiceCollection services)
{
     services.AddMvc()
         .SetCompatibilityVersion(CompatibilityVersion.Version_2_1);
     services.AddHttpContextAccessor();
     services.AddTransient<IUserRepository, UserRepository>();
}
```

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

```csharp
public void ConfigureServices(IServiceCollection services)
{
     services.AddMvc();
     services.AddSingleton<IHttpContextAccessor, HttpContextAccessor>();
     services.AddTransient<IUserRepository, UserRepository>();
}
```

::: moniker-end

No exemplo a seguir:

* o `UserRepository` declara sua dependência no `IHttpContextAccessor`.
* A dependência é fornecida quando a injeção de dependência resolve a cadeia de dependências e cria uma instância do `UserRepository`.

```csharp
public class UserRepository : IUserRepository
{
    private readonly IHttpContextAccessor _httpContextAccessor;

    public UserRepository(IHttpContextAccessor httpContextAccessor)
    {
        _httpContextAccessor = httpContextAccessor;
    }

    public void LogCurrentUser()
    {
        var username = _httpContextAccessor.HttpContext.User.Identity.Name;
        service.LogAccessRequest(username);
    }
}
```

## <a name="httpcontext-access-from-a-background-thread"></a>Acesso a HttpContext de um thread em segundo plano

`HttpContext` não é thread-safe. Ler ou gravar propriedades de `HttpContext` fora do processamento de uma solicitação pode resultar em um `NullReferenceException`.

> [!NOTE]
> Usar `HttpContext` fora do processamento de uma solicitação geralmente resulta em um `NullReferenceException`. Se seu aplicativo gera `NullReferenceException`s esporádicos, revise as partes do código que iniciam o processamento em segundo plano ou que continuam o processamento depois que uma solicitação é concluída. Procure por erros como a definição um método controlador como `async void`.

Para executar com segurança o trabalho em segundo plano com os dados de `HttpContext`:

* Copie os dados necessários durante o processamento da solicitação.
* Passe os dados copiados para uma tarefa em segundo plano.

Para evitar o código não seguro, nunca passe o `HttpContext` em um método que realiza o trabalho em segundo plano. Em vez disso, passe os dados necessários.

```csharp
public class EmailController
{
    public ActionResult SendEmail(string email)
    {
        var correlationId = HttpContext.Request.Headers["x-correlation-id"].ToString();

        // Starts sending an email, but doesn't wait for it to complete
        _ = SendEmailCore(correlationId);
        return View();
    }

    private async Task SendEmailCore(string correlationId)
    {
        // send the email
    }
}

