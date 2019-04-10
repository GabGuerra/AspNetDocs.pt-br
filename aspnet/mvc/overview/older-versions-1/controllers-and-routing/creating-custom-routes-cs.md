---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: Criação de rotas personalizadas (c#) | Microsoft Docs
author: microsoft
description: Saiba como adicionar rotas personalizadas para um aplicativo ASP.NET MVC. Neste tutorial, você aprenderá como modificar a tabela de rotas padrão no arquivo global. asax.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: 7b7324c9e0518697c0978b96b0123cb44133722b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418931"
---
# <a name="creating-custom-routes-c"></a><span data-ttu-id="c0054-104">Criação de rotas personalizadas (C#)</span><span class="sxs-lookup"><span data-stu-id="c0054-104">Creating Custom Routes (C#)</span></span>

<span data-ttu-id="c0054-105">por [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c0054-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c0054-106">Saiba como adicionar rotas personalizadas para um aplicativo ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c0054-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="c0054-107">Neste tutorial, você aprenderá como modificar a tabela de rotas padrão no arquivo global. asax.</span><span class="sxs-lookup"><span data-stu-id="c0054-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>


<span data-ttu-id="c0054-108">Neste tutorial, você aprenderá como adicionar uma rota personalizada a um aplicativo ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c0054-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="c0054-109">Você aprenderá a modificar a tabela de rotas padrão no arquivo global. asax com uma rota personalizada.</span><span class="sxs-lookup"><span data-stu-id="c0054-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="c0054-110">Para muitos aplicativos ASP.NET MVC simples, a tabela de rotas padrão funcionará bem.</span><span class="sxs-lookup"><span data-stu-id="c0054-110">For many simple ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="c0054-111">No entanto, talvez você descubra que você tiver um roteamentos necessidades especializado.</span><span class="sxs-lookup"><span data-stu-id="c0054-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="c0054-112">Nesse caso, você pode criar uma rota personalizada.</span><span class="sxs-lookup"><span data-stu-id="c0054-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="c0054-113">Por exemplo, imagine que você esteja criando um aplicativo de blog.</span><span class="sxs-lookup"><span data-stu-id="c0054-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="c0054-114">Você talvez queira manipular solicitações de entrada que ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="c0054-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="c0054-115">/ Arquivamento/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="c0054-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="c0054-116">Quando um usuário insere essa solicitação, você deseja retornar a entrada de blog que corresponde à data 12/25/2009.</span><span class="sxs-lookup"><span data-stu-id="c0054-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="c0054-117">Para lidar com esse tipo de solicitação, você precisa criar uma rota personalizada.</span><span class="sxs-lookup"><span data-stu-id="c0054-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="c0054-118">O arquivo global asax na listagem 1 contém uma nova rota personalizada, chamada de Blog, que trata as solicitações que se parecem com /Archive/*data de entrada*.</span><span class="sxs-lookup"><span data-stu-id="c0054-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

**<span data-ttu-id="c0054-119">Listagem 1 - global. asax (com rota personalizada)</span><span class="sxs-lookup"><span data-stu-id="c0054-119">Listing 1 - Global.asax (with custom route)</span></span>**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

<span data-ttu-id="c0054-120">A ordem das rotas que você adicionar à tabela de rotas é importante.</span><span class="sxs-lookup"><span data-stu-id="c0054-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="c0054-121">Nossa nova rota Blog personalizada é adicionada antes da rota padrão existente.</span><span class="sxs-lookup"><span data-stu-id="c0054-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="c0054-122">Se você invertemos a ordem, em seguida, a rota padrão sempre será chamada em vez de na rota personalizada.</span><span class="sxs-lookup"><span data-stu-id="c0054-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="c0054-123">A rota de Blog personalizada corresponde a qualquer solicitação que começa com/arquivamento /.</span><span class="sxs-lookup"><span data-stu-id="c0054-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="c0054-124">Assim, ele corresponde a todas as URLs a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0054-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="c0054-125">/ Arquivamento/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="c0054-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="c0054-126">/ Arquivamento/10 6 de 2004</span><span class="sxs-lookup"><span data-stu-id="c0054-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="c0054-127">/ Arquivamento/apple</span><span class="sxs-lookup"><span data-stu-id="c0054-127">/Archive/apple</span></span>

<span data-ttu-id="c0054-128">A rota personalizada mapeia a solicitação de entrada para um controlador chamado arquivo morto e invoca a ação Entry().</span><span class="sxs-lookup"><span data-stu-id="c0054-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="c0054-129">Quando o método Entry() é chamado, a data de entrada é passada como um parâmetro chamado entryDate.</span><span class="sxs-lookup"><span data-stu-id="c0054-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="c0054-130">Você pode usar a rota personalizada do Blog com o controlador na listagem 2.</span><span class="sxs-lookup"><span data-stu-id="c0054-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

**<span data-ttu-id="c0054-131">Listagem 2 - ArchiveController.cs</span><span class="sxs-lookup"><span data-stu-id="c0054-131">Listing 2 - ArchiveController.cs</span></span>**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

<span data-ttu-id="c0054-132">Observe que o método Entry() na listagem 2 aceita um parâmetro do tipo DateTime.</span><span class="sxs-lookup"><span data-stu-id="c0054-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="c0054-133">A estrutura do MVC é inteligente o suficiente para converter a data de entrada da URL em um valor DateTime automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c0054-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="c0054-134">Se o parâmetro de data de entrada da URL não pode ser convertido em uma data e hora, ocorrerá um erro (consulte a Figura 1).</span><span class="sxs-lookup"><span data-stu-id="c0054-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

**<span data-ttu-id="c0054-135">Figura 1 – erro de conversão de parâmetro</span><span class="sxs-lookup"><span data-stu-id="c0054-135">Figure 1 - Error from converting parameter</span></span>**


[![T<span data-ttu-id="c0054-136">caixa de diálogo Novo projeto he]</span><span class="sxs-lookup"><span data-stu-id="c0054-136">he New Project dialog box]</span></span>(creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

<span data-ttu-id="c0054-137">**Figura 01**: Erro de conversão de parâmetro ([clique para exibir a imagem em tamanho normal](creating-custom-routes-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="c0054-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-cs/_static/image2.png))</span></span>


## <a name="summary"></a><span data-ttu-id="c0054-138">Resumo</span><span class="sxs-lookup"><span data-stu-id="c0054-138">Summary</span></span>

<span data-ttu-id="c0054-139">O objetivo deste tutorial era demonstrar como você pode criar uma rota personalizada.</span><span class="sxs-lookup"><span data-stu-id="c0054-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="c0054-140">Você aprendeu como adicionar uma rota personalizada à tabela de rotas no arquivo global. asax que representa as entradas de blog.</span><span class="sxs-lookup"><span data-stu-id="c0054-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="c0054-141">Discutimos como mapear solicitações para entradas de blog para um controlador chamado ArchiveController e uma ação de controlador chamada Entry().</span><span class="sxs-lookup"><span data-stu-id="c0054-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c0054-142">[Anterior](aspnet-mvc-controllers-overview-cs.md)
> [Próximo](creating-a-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="c0054-142">[Previous](aspnet-mvc-controllers-overview-cs.md)
[Next](creating-a-route-constraint-cs.md)</span></span>
