---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
title: Escolhendo uma animação em uma lista (VB) | Microsoft Docs
author: wenz
description: O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle. A estrutura também mitir...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 81ba9116-d485-40c0-8ff6-7e9ae23e0a0c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
msc.type: authoredcontent
ms.openlocfilehash: 7d8807962e5cf668358e03821d5fd3bf755a0e7d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418879"
---
# <a name="picking-one-animation-out-of-a-list-vb"></a><span data-ttu-id="90a61-104">Escolher uma animação em uma lista (VB)</span><span class="sxs-lookup"><span data-stu-id="90a61-104">Picking One Animation Out Of a List (VB)</span></span>

<span data-ttu-id="90a61-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="90a61-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="90a61-106">[Baixar o código](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) ou [baixar PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="90a61-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span></span>

> <span data-ttu-id="90a61-107">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="90a61-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="90a61-108">O framework também permite que o programador escolher uma animação em uma lista de animações, dependendo da avaliação de algum código JavaScript.</span><span class="sxs-lookup"><span data-stu-id="90a61-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="90a61-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="90a61-109">Overview</span></span>

<span data-ttu-id="90a61-110">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="90a61-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="90a61-111">O framework também permite que o programador escolher uma animação em uma lista de animações, dependendo da avaliação de algum código JavaScript.</span><span class="sxs-lookup"><span data-stu-id="90a61-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="90a61-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="90a61-112">Steps</span></span>

<span data-ttu-id="90a61-113">Em primeiro lugar, inclua o `ScriptManager` na página; em seguida, a biblioteca do AJAX ASP.NET é carregada, tornando possível usar o Kit de ferramentas de controle:</span><span class="sxs-lookup"><span data-stu-id="90a61-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample1.aspx)]

<span data-ttu-id="90a61-114">A animação será aplicada a um painel de texto que tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="90a61-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample2.aspx)]

<span data-ttu-id="90a61-115">Na classe CSS associado para o painel, definir uma cor de fundo interessante e também definir uma largura fixa para o painel:</span><span class="sxs-lookup"><span data-stu-id="90a61-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-vb/samples/sample3.css)]

<span data-ttu-id="90a61-116">Em seguida, adicione a `AnimationExtender` para a página, fornecendo uma `ID`, o `TargetControlID` atributo e o obrigatório</span><span class="sxs-lookup"><span data-stu-id="90a61-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory</span></span> `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample4.aspx)]

<span data-ttu-id="90a61-117">Dentro de `<Animations>` nó, use `<OnLoad>` para as animações são executadas uma vez que a página foi totalmente carregada.</span><span class="sxs-lookup"><span data-stu-id="90a61-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="90a61-118">Em vez de uma das animações regulares, o `<Case>` elemento entra em cena.</span><span class="sxs-lookup"><span data-stu-id="90a61-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="90a61-119">O valor do seu atributo SelectScript é avaliado; o valor de retorno deve ser numérico.</span><span class="sxs-lookup"><span data-stu-id="90a61-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="90a61-120">Dependendo desse número, uma das subanimations dentro &lt;caso&gt; é executado.</span><span class="sxs-lookup"><span data-stu-id="90a61-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="90a61-121">Por exemplo, se SelectScript for avaliada como 2, o Kit de ferramentas de controle é executado a terceira animação dentro &lt;caso&gt; (contando começa em 0).</span><span class="sxs-lookup"><span data-stu-id="90a61-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="90a61-122">A marcação a seguir define três subanimations: Redimensionando a largura, redimensionar a altura e desaparecimento. O código JavaScript (`Math.floor(3 * Math.random())`), em seguida, escolhe um número entre 0 e 2, para que um dos três animações é executado:</span><span class="sxs-lookup"><span data-stu-id="90a61-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample5.aspx)]


[![O<span data-ttu-id="90a61-123">m das animações de três possíveis: O painel obtém mais largo]</span><span class="sxs-lookup"><span data-stu-id="90a61-123">ne of the possible three animations: The panel gets wider]</span></span>(picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)

<span data-ttu-id="90a61-124">Uma das três animações possíveis: O painel obtém mais amplo ([clique para exibir a imagem em tamanho normal](picking-one-animation-out-of-a-list-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="90a61-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="90a61-125">[Anterior](animation-depending-on-a-condition-vb.md)
> [Próximo](animating-in-response-to-user-interaction-vb.md)</span><span class="sxs-lookup"><span data-stu-id="90a61-125">[Previous](animation-depending-on-a-condition-vb.md)
[Next](animating-in-response-to-user-interaction-vb.md)</span></span>
