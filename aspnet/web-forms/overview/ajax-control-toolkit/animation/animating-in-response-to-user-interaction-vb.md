---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: Animação em resposta à interação do usuário (VB) | Microsoft Docs
author: wenz
description: O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle. As animações podem estrelas...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: fa774eecd872e79e3b05f6a6ebe177be895b8191
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65112920"
---
# <a name="animating-in-response-to-user-interaction-vb"></a><span data-ttu-id="5ed12-104">Animação em resposta à interação do usuário (VB)</span><span class="sxs-lookup"><span data-stu-id="5ed12-104">Animating in Response To User Interaction (VB)</span></span>

<span data-ttu-id="5ed12-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5ed12-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5ed12-106">[Baixar o código](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) ou [baixar PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="5ed12-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span></span>

> <span data-ttu-id="5ed12-107">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="5ed12-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5ed12-108">As animações podem iniciar automaticamente ou podem ser disparadas pela interação do usuário, por exemplo, clicando com o mouse.</span><span class="sxs-lookup"><span data-stu-id="5ed12-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="overview"></a><span data-ttu-id="5ed12-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5ed12-109">Overview</span></span>

<span data-ttu-id="5ed12-110">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="5ed12-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5ed12-111">As animações podem iniciar automaticamente ou podem ser disparadas pela interação do usuário, por exemplo, clicando com o mouse.</span><span class="sxs-lookup"><span data-stu-id="5ed12-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="5ed12-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="5ed12-112">Steps</span></span>

<span data-ttu-id="5ed12-113">Em primeiro lugar, inclua o `ScriptManager` na página; em seguida, a biblioteca do AJAX ASP.NET é carregada, tornando possível usar o Kit de ferramentas de controle:</span><span class="sxs-lookup"><span data-stu-id="5ed12-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

<span data-ttu-id="5ed12-114">A animação será aplicada a um painel de texto que tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="5ed12-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

<span data-ttu-id="5ed12-115">Na classe CSS associado para o painel, definir uma cor de fundo interessante e também definir uma largura fixa para o painel:</span><span class="sxs-lookup"><span data-stu-id="5ed12-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

<span data-ttu-id="5ed12-116">Em seguida, adicione a `AnimationExtender` para a página, fornecendo uma `ID`, o `TargetControlID` atributo e o obrigatoriamente `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="5ed12-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

<span data-ttu-id="5ed12-117">Dentro de `<Animations>` nó, há cinco maneiras de iniciar a animação por meio de interação do usuário (o elemento ausente é `<OnLoad>` que é executado depois que a página inteira tenha sido totalmente carregada):</span><span class="sxs-lookup"><span data-stu-id="5ed12-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="5ed12-118">`<OnClick>` (clique do mouse no controle)</span><span class="sxs-lookup"><span data-stu-id="5ed12-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="5ed12-119">`<OnHoverOut>` (o mouse deixa o controle)</span><span class="sxs-lookup"><span data-stu-id="5ed12-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="5ed12-120">`<OnHoverOver>` (mouse passa sobre um controle, interrompendo o `<OnHoverOut>` animação)</span><span class="sxs-lookup"><span data-stu-id="5ed12-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="5ed12-121">`<OnMouseOut>` (o mouse sai de um controle)</span><span class="sxs-lookup"><span data-stu-id="5ed12-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="5ed12-122">`<OnMouseOver>` (mouse passa sobre um controle, não parar a `<OnMouseOut>` animação)</span><span class="sxs-lookup"><span data-stu-id="5ed12-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="5ed12-123">Nesse cenário, `<OnClick>` é usado.</span><span class="sxs-lookup"><span data-stu-id="5ed12-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="5ed12-124">Quando o usuário clica no painel, ele é redimensionado e fade out ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="5ed12-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]

<span data-ttu-id="5ed12-125">[![Um clique do mouse inicia a animação](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5ed12-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span></span>

<span data-ttu-id="5ed12-126">Um clique do mouse inicia a animação ([clique para exibir a imagem em tamanho normal](animating-in-response-to-user-interaction-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5ed12-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5ed12-127">[Anterior](picking-one-animation-out-of-a-list-vb.md)
> [Próximo](disabling-actions-during-animation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5ed12-127">[Previous](picking-one-animation-out-of-a-list-vb.md)
[Next](disabling-actions-during-animation-vb.md)</span></span>
