---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: Animação em resposta à interação do usuário (c#) | Microsoft Docs
author: wenz
description: O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle. As animações podem estrelas...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: 6bf69927c5a73f89d94282937d1d4e21ec75ea53
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65108134"
---
# <a name="animating-in-response-to-user-interaction-c"></a><span data-ttu-id="1b606-104">Animação em resposta à interação do usuário (C#)</span><span class="sxs-lookup"><span data-stu-id="1b606-104">Animating in Response To User Interaction (C#)</span></span>

<span data-ttu-id="1b606-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1b606-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1b606-106">[Baixar o código](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1b606-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)</span></span>

> <span data-ttu-id="1b606-107">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="1b606-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1b606-108">As animações podem iniciar automaticamente ou podem ser disparadas pela interação do usuário, por exemplo, clicando com o mouse.</span><span class="sxs-lookup"><span data-stu-id="1b606-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="overview"></a><span data-ttu-id="1b606-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1b606-109">Overview</span></span>

<span data-ttu-id="1b606-110">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="1b606-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1b606-111">As animações podem iniciar automaticamente ou podem ser disparadas pela interação do usuário, por exemplo, clicando com o mouse.</span><span class="sxs-lookup"><span data-stu-id="1b606-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="1b606-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="1b606-112">Steps</span></span>

<span data-ttu-id="1b606-113">Em primeiro lugar, inclua o `ScriptManager` na página; em seguida, a biblioteca do AJAX ASP.NET é carregada, tornando possível usar o Kit de ferramentas de controle:</span><span class="sxs-lookup"><span data-stu-id="1b606-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

<span data-ttu-id="1b606-114">A animação será aplicada a um painel de texto que tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="1b606-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

<span data-ttu-id="1b606-115">Na classe CSS associado para o painel, definir uma cor de fundo interessante e também definir uma largura fixa para o painel:</span><span class="sxs-lookup"><span data-stu-id="1b606-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

<span data-ttu-id="1b606-116">Em seguida, adicione a `AnimationExtender` para a página, fornecendo uma `ID`, o `TargetControlID` atributo e o obrigatoriamente `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="1b606-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

<span data-ttu-id="1b606-117">Dentro de `<Animations>` nó, há cinco maneiras de iniciar a animação por meio de interação do usuário (o elemento ausente é `<OnLoad>` que é executado depois que a página inteira tenha sido totalmente carregada):</span><span class="sxs-lookup"><span data-stu-id="1b606-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="1b606-118">`<OnClick>` (clique do mouse no controle)</span><span class="sxs-lookup"><span data-stu-id="1b606-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="1b606-119">`<OnHoverOut>` (o mouse deixa o controle)</span><span class="sxs-lookup"><span data-stu-id="1b606-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="1b606-120">`<OnHoverOver>` (mouse passa sobre um controle, interrompendo o `<OnHoverOut>` animação)</span><span class="sxs-lookup"><span data-stu-id="1b606-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="1b606-121">`<OnMouseOut>` (o mouse sai de um controle)</span><span class="sxs-lookup"><span data-stu-id="1b606-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="1b606-122">`<OnMouseOver>` (mouse passa sobre um controle, não parar a `<OnMouseOut>` animação)</span><span class="sxs-lookup"><span data-stu-id="1b606-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="1b606-123">Nesse cenário, `<OnClick>` é usado.</span><span class="sxs-lookup"><span data-stu-id="1b606-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="1b606-124">Quando o usuário clica no painel, ele é redimensionado e fade out ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="1b606-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]

<span data-ttu-id="1b606-125">[![Um clique do mouse inicia a animação](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1b606-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)</span></span>

<span data-ttu-id="1b606-126">Um clique do mouse inicia a animação ([clique para exibir a imagem em tamanho normal](animating-in-response-to-user-interaction-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1b606-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1b606-127">[Anterior](picking-one-animation-out-of-a-list-cs.md)
> [Próximo](disabling-actions-during-animation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1b606-127">[Previous](picking-one-animation-out-of-a-list-cs.md)
[Next](disabling-actions-during-animation-cs.md)</span></span>
