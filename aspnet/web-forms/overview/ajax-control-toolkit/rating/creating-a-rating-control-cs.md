---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: Criação de um controle classificação (C#) | Microsoft Docs
author: wenz
description: Muitos sites, de comércio eletrônico para sites de comunidades, oferecem seus usuários para artigos de taxa ou itens. Isso geralmente exige algum esforço de codificação, mas temos o...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 5776101d9e40f999806aefa5a9529dbef21af161
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048383"
---
<a name="creating-a-rating-control-c"></a><span data-ttu-id="8a5a1-104">Criação de um controle Classificação (C#)</span><span class="sxs-lookup"><span data-stu-id="8a5a1-104">Creating a Rating Control (C#)</span></span>
====================
<span data-ttu-id="8a5a1-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8a5a1-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8a5a1-106">[Baixar o código](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="8a5a1-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span></span>

> <span data-ttu-id="8a5a1-107">Muitos sites, de comércio eletrônico para sites de comunidades, oferecem seus usuários para artigos de taxa ou itens.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="8a5a1-108">Isso geralmente exige algum esforço de codificação, mas temos o Kit de ferramentas de controle à nossa disposição.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>


## <a name="overview"></a><span data-ttu-id="8a5a1-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8a5a1-109">Overview</span></span>

<span data-ttu-id="8a5a1-110">Muitos sites, de comércio eletrônico para sites de comunidades, oferecem seus usuários para artigos de taxa ou itens.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="8a5a1-111">Isso geralmente exige algum esforço de codificação, mas temos o Kit de ferramentas de controle à nossa disposição.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="8a5a1-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="8a5a1-112">Steps</span></span>

<span data-ttu-id="8a5a1-113">Em primeiro lugar, você precisa (pelo menos) dois tipos de imagens: uma para um preenchido-out do item de classificação e um para um item de classificação vazia.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="8a5a1-114">Um item de classificação é normalmente uma estrela ou um sorriso.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="8a5a1-115">Para este cenário, você encontra três arquivos, smiley.png e empty.png e sorriso done.png como parte dos downloads de código de origem para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="8a5a1-116">Em seguida, crie um novo arquivo do ASP.NET e comece a adicionar um `ScriptManager` controle a ele:</span><span class="sxs-lookup"><span data-stu-id="8a5a1-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

<span data-ttu-id="8a5a1-117">Em seguida, adicione o `Rating` controle do ASP.NET AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="8a5a1-118">Os atributos a seguir precisam ser definidas para este exemplo:</span><span class="sxs-lookup"><span data-stu-id="8a5a1-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="8a5a1-119">`CurrentRating` a classificação inicial a ser usado</span><span class="sxs-lookup"><span data-stu-id="8a5a1-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="8a5a1-120">`MaxRating` a classificação máxima</span><span class="sxs-lookup"><span data-stu-id="8a5a1-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="8a5a1-121">`EmptyStarCssClass` a classe CSS a ser usado quando um item de classificação (star) está vazio</span><span class="sxs-lookup"><span data-stu-id="8a5a1-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="8a5a1-122">`FilledStarCssClass` a classe CSS a ser usado quando um item de classificação (star) é preenchido</span><span class="sxs-lookup"><span data-stu-id="8a5a1-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="8a5a1-123">`StarCssClass` a classe CSS a ser usado para um estado visível</span><span class="sxs-lookup"><span data-stu-id="8a5a1-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="8a5a1-124">`WaitingStarCssClass` a classe CSS a usar enquanto uma classificação por estrelas é enviada de volta ao servidor</span><span class="sxs-lookup"><span data-stu-id="8a5a1-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="8a5a1-125">E aqui está a marcação que cria um controle de classificação com cinco itens (smileys) de que nenhum é preenchido inicialmente:</span><span class="sxs-lookup"><span data-stu-id="8a5a1-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

<span data-ttu-id="8a5a1-126">As três classes CSS referenciadas agora precisam mostrar os arquivos de imagem apropriada, que é uma tarefa fácil usando CSS:</span><span class="sxs-lookup"><span data-stu-id="8a5a1-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

<span data-ttu-id="8a5a1-127">Certifique-se de que você forneça a largura e altura de três imagens, caso contrário, a exibição pode parecer um pouco bagunçada backup.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="8a5a1-128">Por fim, o resultado da avaliação deve ser exibido para o usuário (ou, pelo menos é salvo em um banco de dados).</span><span class="sxs-lookup"><span data-stu-id="8a5a1-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="8a5a1-129">Portanto, adicione um rótulo para a saída de uma mensagem de texto e um botão de envio de enviar novamente o formulário de classificação para o servidor:</span><span class="sxs-lookup"><span data-stu-id="8a5a1-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

<span data-ttu-id="8a5a1-130">No código do lado do servidor, acessar o controle de classificação por meio de seu `ID` e, em seguida, acessar seu `CurrentRating` propriedade que é o número de itens de classificação selecionada, em nosso exemplo, um valor entre 0 e 5.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

<span data-ttu-id="8a5a1-131">Salve a página e carregá-lo em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="8a5a1-132">Quando você focaliza os itens de classificação (inicialmente vazio), ocorre um efeito de JavaScript: As alterações de classificação.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="8a5a1-133">Quando você clica no conjunto de estrelas, a classificação atual é mantida.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="8a5a1-134">Por fim, quando você envia o formulário, o código do lado do servidor gera a classificação selecionada.</span><span class="sxs-lookup"><span data-stu-id="8a5a1-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>


<span data-ttu-id="8a5a1-135">[![Criando um sistema de classificação com o mínimo de código](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8a5a1-135">[![Creating a rating system with minimal code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="8a5a1-136">Criando um sistema de classificação com o mínimo de código ([clique para exibir a imagem em tamanho normal](creating-a-rating-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8a5a1-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8a5a1-137">Avançar</span><span class="sxs-lookup"><span data-stu-id="8a5a1-137">Next</span></span>](creating-a-rating-control-vb.md)
