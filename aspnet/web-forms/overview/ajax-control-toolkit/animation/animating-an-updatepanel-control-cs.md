---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: Animar um controle UpdatePanel (c#) | Microsoft Docs
author: wenz
description: O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle. Para o conteúdo de um...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 36d1166e1bd2b4c97b3cf3dd0bc3a7e8010a9443
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59393685"
---
# <a name="animating-an-updatepanel-control-c"></a><span data-ttu-id="f88d3-104">Animar um controle UpdatePanel (C#)</span><span class="sxs-lookup"><span data-stu-id="f88d3-104">Animating an UpdatePanel Control (C#)</span></span>

<span data-ttu-id="f88d3-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f88d3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f88d3-106">[Baixar o código](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f88d3-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span></span>

> <span data-ttu-id="f88d3-107">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="f88d3-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="f88d3-108">Para o conteúdo de um UpdatePanel, um extensor especial existe que depende muito do framework de animação: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="f88d3-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="f88d3-109">Este tutorial mostra como configurar uma animação desse tipo para um UpdatePanel.</span><span class="sxs-lookup"><span data-stu-id="f88d3-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>


## <a name="overview"></a><span data-ttu-id="f88d3-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f88d3-110">Overview</span></span>

<span data-ttu-id="f88d3-111">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="f88d3-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="f88d3-112">Para o conteúdo de um `UpdatePanel`, um extensor especial existe que depende muito do framework de animação: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="f88d3-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="f88d3-113">Este tutorial mostra como configurar uma animação desse tipo para um `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="f88d3-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="f88d3-114">Etapas</span><span class="sxs-lookup"><span data-stu-id="f88d3-114">Steps</span></span>

<span data-ttu-id="f88d3-115">Como de costume, a primeira etapa é incluir o `ScriptManager` na página de modo que a biblioteca do AJAX ASP.NET é carregada e o Kit de ferramentas de controle pode ser usado:</span><span class="sxs-lookup"><span data-stu-id="f88d3-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

<span data-ttu-id="f88d3-116">A animação neste cenário será aplicada a um ASP.NET `Wizard` controle de web que reside em um `UpdatePanel`.</span><span class="sxs-lookup"><span data-stu-id="f88d3-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="f88d3-117">Três etapas (arbitrárias) fornecem opções suficiente para disparar postbacks:</span><span class="sxs-lookup"><span data-stu-id="f88d3-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

<span data-ttu-id="f88d3-118">A marcação necessária para o `UpdatePanelAnimationExtender` controle é bastante semelhante à marcação usada para o `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="f88d3-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="f88d3-119">No `TargetControlID` atributo fornecemos a `ID` da `UpdatePanel` animar; dentro a `UpdatePanelAnimationExtender` controle, o `<Animations>` elemento contém a marcação XML para as animações.</span><span class="sxs-lookup"><span data-stu-id="f88d3-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="f88d3-120">No entanto, há uma diferença: A quantidade de eventos e manipuladores de eventos é limitada em comparação com `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="f88d3-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="f88d3-121">Para `UpdatePanels`, apenas duas delas existir:</span><span class="sxs-lookup"><span data-stu-id="f88d3-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="f88d3-122">`<OnUpdated>` Quando o UpdatePanel foi atualizado</span><span class="sxs-lookup"><span data-stu-id="f88d3-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="f88d3-123">`<OnUpdating>` Quando o UpdatePanel inicia a atualização</span><span class="sxs-lookup"><span data-stu-id="f88d3-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="f88d3-124">Nesse cenário, o novo conteúdo do `UpdatePanel` (após o postback) deverá aplicar fade-in.</span><span class="sxs-lookup"><span data-stu-id="f88d3-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="f88d3-125">Isso é a marcação necessária para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="f88d3-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

<span data-ttu-id="f88d3-126">Agora, sempre que um postback ocorre dentro do UpdatePanel, o novo conteúdo do painel aplicar fade-in sem problemas.</span><span class="sxs-lookup"><span data-stu-id="f88d3-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>


<span data-ttu-id="f88d3-127">[![A próxima etapa do assistente está desaparecendo](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f88d3-127">[![The next wizard step is fading in](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="f88d3-128">A próxima etapa do assistente está desaparecendo ([clique para exibir a imagem em tamanho normal](animating-an-updatepanel-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f88d3-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f88d3-129">[Anterior](changing-an-animation-using-client-side-code-cs.md)
> [Próximo](dynamically-controlling-updatepanel-animations-cs.md)</span><span class="sxs-lookup"><span data-stu-id="f88d3-129">[Previous](changing-an-animation-using-client-side-code-cs.md)
[Next](dynamically-controlling-updatepanel-animations-cs.md)</span></span>
