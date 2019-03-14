---
title: Artigos baseados em projetos do ASP.NET Core criados com contas de usuário individuais
author: rick-anderson
description: Descubra artigos baseados em projetos do ASP.NET Core criados com contas de usuário individuais.
ms.author: riande
ms.date: 11/30/2017
uid: security/authentication/individual
ms.openlocfilehash: c73365eafaf2c38ef02c3c83ccf5ced4264f7dc0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033833"
---
# <a name="articles-based-on-aspnet-core-projects-created-with-individual-user-accounts"></a><span data-ttu-id="69d1f-103">Artigos baseados em projetos do ASP.NET Core criados com contas de usuário individuais</span><span class="sxs-lookup"><span data-stu-id="69d1f-103">Articles based on ASP.NET Core projects created with individual user accounts</span></span>

<span data-ttu-id="69d1f-104">O ASP.NET Core Identity é incluído nos modelos de projeto no Visual Studio com a opção "Contas de usuário individuais".</span><span class="sxs-lookup"><span data-stu-id="69d1f-104">ASP.NET Core Identity is included in project templates in Visual Studio with the "Individual User Accounts" option.</span></span>

<span data-ttu-id="69d1f-105">Os modelos de autenticação estão disponíveis na CLI do .NET Core com `-au Individual`:</span><span class="sxs-lookup"><span data-stu-id="69d1f-105">The authentication templates are available in .NET Core CLI with `-au Individual`:</span></span>

::: moniker range=">= aspnetcore-2.1"

```console
dotnet new mvc -au Individual
dotnet new webapp -au Individual
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
dotnet new mvc -au Individual
dotnet new razor -au Individual
```

::: moniker-end

<span data-ttu-id="69d1f-106">Ver [esse problema de GitHub](https://github.com/aspnet/AspNetCore/issues/5833) para autenticação de API da web.</span><span class="sxs-lookup"><span data-stu-id="69d1f-106">See [this GitHub issue](https://github.com/aspnet/AspNetCore/issues/5833) for web API authentication.</span></span>

<a name="no"></a>
## <a name="no-authentication"></a><span data-ttu-id="69d1f-107">Sem autenticação</span><span class="sxs-lookup"><span data-stu-id="69d1f-107">No Authentication</span></span>

<span data-ttu-id="69d1f-108">Autenticação é especificada na CLI do .NET Core com o `-au` opção.</span><span class="sxs-lookup"><span data-stu-id="69d1f-108">Authentication is specified in the .NET Core CLI with the `-au` option.</span></span> <span data-ttu-id="69d1f-109">No Visual Studio, o **alterar autenticação** caixa de diálogo está disponível para novos aplicativos da web.</span><span class="sxs-lookup"><span data-stu-id="69d1f-109">In Visual Studio, the **Change Authentication** dialog is available for new web applications.</span></span> <span data-ttu-id="69d1f-110">É o padrão para novos aplicativos web no Visual Studio **sem autenticação**.</span><span class="sxs-lookup"><span data-stu-id="69d1f-110">The default for new web apps in Visual Studio is **No Authentication**.</span></span>

<span data-ttu-id="69d1f-111">Projetos criados com nenhuma autenticação:</span><span class="sxs-lookup"><span data-stu-id="69d1f-111">Projects created with no authentication:</span></span>

* <span data-ttu-id="69d1f-112">Não contêm páginas da web e a interface do usuário para entrar e sair.</span><span class="sxs-lookup"><span data-stu-id="69d1f-112">Don't contain web pages and UI to sign in and sign out.</span></span>
* <span data-ttu-id="69d1f-113">Não contêm o código de autenticação.</span><span class="sxs-lookup"><span data-stu-id="69d1f-113">Don't contain authentication code.</span></span>

<a name="win"></a>
## <a name="windows-authentication"></a><span data-ttu-id="69d1f-114">Autenticação do Windows</span><span class="sxs-lookup"><span data-stu-id="69d1f-114">Windows Authentication</span></span>

<span data-ttu-id="69d1f-115">Autenticação do Windows é especificada para novos aplicativos web na CLI do .NET Core com o `-au Windows` opção.</span><span class="sxs-lookup"><span data-stu-id="69d1f-115">Windows Authentication is specified for new web apps in the .NET Core CLI with the `-au Windows` option.</span></span> <span data-ttu-id="69d1f-116">No Visual Studio, o **alterar autenticação** caixa de diálogo fornece o **autenticação do Windows** opções.</span><span class="sxs-lookup"><span data-stu-id="69d1f-116">In Visual Studio, the **Change Authentication** dialog provides the **Windows Authentication** options.</span></span>

<span data-ttu-id="69d1f-117">Se a autenticação do Windows é selecionada, o aplicativo está configurado para usar o [módulo do IIS da autenticação Windows](xref:host-and-deploy/iis/modules).</span><span class="sxs-lookup"><span data-stu-id="69d1f-117">If Windows Authentication is selected, the app is configured to use the [Windows Authentication IIS module](xref:host-and-deploy/iis/modules).</span></span> <span data-ttu-id="69d1f-118">Autenticação do Windows destina-se a sites da Intranet.</span><span class="sxs-lookup"><span data-stu-id="69d1f-118">Windows Authentication is intended for Intranet web sites.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="69d1f-119">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="69d1f-119">Additional resources</span></span>

<span data-ttu-id="69d1f-120">Os artigos a seguir mostram como usar o código gerado em modelos do ASP.NET Core que usam contas de usuário individual:</span><span class="sxs-lookup"><span data-stu-id="69d1f-120">The following articles show how to use the code generated in ASP.NET Core templates that use individual user accounts:</span></span>

* [<span data-ttu-id="69d1f-121">Autenticação de dois fatores com SMS</span><span class="sxs-lookup"><span data-stu-id="69d1f-121">Two-factor authentication with SMS</span></span>](xref:security/authentication/2fa)
* [<span data-ttu-id="69d1f-122">Confirmação de conta e de recuperação de senha no ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="69d1f-122">Account confirmation and password recovery in ASP.NET Core</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="69d1f-123">Criar um aplicativo ASP.NET Core com os dados de usuário protegidos por autorização</span><span class="sxs-lookup"><span data-stu-id="69d1f-123">Create an ASP.NET Core app with user data protected by authorization</span></span>](xref:security/authorization/secure-data)
