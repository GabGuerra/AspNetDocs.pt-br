---
uid: webhooks/receiving/dependencies
title: Dependências de receptor de WebHooks do ASP.NET | Microsoft Docs
author: rick-anderson
description: Dependências de receptor e injeção de dependência no ASP.NET WebHooks.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: c44cfe3ed310aa728a989b108c410e8786e4f514
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048723"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="ab35a-103">Dependências de receptor de WebHooks do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ab35a-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="ab35a-104">WebHooks do Microsoft ASP.NET foi projetado com injeção de dependência em mente.</span><span class="sxs-lookup"><span data-stu-id="ab35a-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="ab35a-105">A maioria das dependências do sistema podem ser substituídas por implementações alternativas usando um mecanismo de injeção de dependência.</span><span class="sxs-lookup"><span data-stu-id="ab35a-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="ab35a-106">Consulte [DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) para obter uma lista de dependências de receptor.</span><span class="sxs-lookup"><span data-stu-id="ab35a-106">Please see [DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="ab35a-107">Se nenhuma dependência tiver sido registrada, uma implementação padrão será usada.</span><span class="sxs-lookup"><span data-stu-id="ab35a-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="ab35a-108">Consulte [ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) para obter uma lista das implementações padrão.</span><span class="sxs-lookup"><span data-stu-id="ab35a-108">Please see [ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
