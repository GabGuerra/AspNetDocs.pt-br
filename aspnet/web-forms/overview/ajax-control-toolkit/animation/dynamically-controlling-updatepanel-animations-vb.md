---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
title: Controlando dinamicamente animações UpdatePanel (VB) | Microsoft Docs
author: wenz
description: O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle. Para o conteúdo de um...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: bea66072-59b6-42b4-98fa-211812f5925f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
msc.type: authoredcontent
ms.openlocfilehash: 2a4c01ffdee20f2c7970d999b34bf1374088d4c5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57053663"
---
<a name="dynamically-controlling-updatepanel-animations-vb"></a><span data-ttu-id="195f3-104">Controlar dinamicamente animações UpdatePanel (VB)</span><span class="sxs-lookup"><span data-stu-id="195f3-104">Dynamically Controlling UpdatePanel Animations (VB)</span></span>
====================
<span data-ttu-id="195f3-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="195f3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="195f3-106">[Baixar o código](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) ou [baixar PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="195f3-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)</span></span>

> <span data-ttu-id="195f3-107">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="195f3-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="195f3-108">Para o conteúdo de um UpdatePanel, um extensor especial existe que depende muito do framework de animação: UpdatePanelAnimation.</span><span class="sxs-lookup"><span data-stu-id="195f3-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="195f3-109">Ele também pode trabalhar junto com os gatilhos UpdatePanel.</span><span class="sxs-lookup"><span data-stu-id="195f3-109">It can also work together with UpdatePanel triggers.</span></span>


## <a name="overview"></a><span data-ttu-id="195f3-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="195f3-110">Overview</span></span>

<span data-ttu-id="195f3-111">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="195f3-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="195f3-112">Para o conteúdo de um `UpdatePanel`, um extensor especial existe que depende muito do framework de animação: `UpdatePanelAnimation`.</span><span class="sxs-lookup"><span data-stu-id="195f3-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="195f3-113">Ele também pode trabalhar em conjunto com `UpdatePanel` gatilhos.</span><span class="sxs-lookup"><span data-stu-id="195f3-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="195f3-114">Etapas</span><span class="sxs-lookup"><span data-stu-id="195f3-114">Steps</span></span>

<span data-ttu-id="195f3-115">Como de costume, a primeira etapa é incluir o `ScriptManager` na página de modo que a biblioteca do AJAX ASP.NET é carregada e o Kit de ferramentas de controle pode ser usado:</span><span class="sxs-lookup"><span data-stu-id="195f3-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample1.aspx)]

<span data-ttu-id="195f3-116">A animação neste cenário será aplicada a uma exibição de tempo atual.</span><span class="sxs-lookup"><span data-stu-id="195f3-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="195f3-117">Essas informações podem ser gravadas em um rótulo usando o `Page_Load()` método, ou (para fins de simplicidade) o seguinte código embutido é usado:</span><span class="sxs-lookup"><span data-stu-id="195f3-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample2.aspx)]

<span data-ttu-id="195f3-118">Além disso, é criado um botão para disparar a atualização de tempo:</span><span class="sxs-lookup"><span data-stu-id="195f3-118">Also, a button to trigger updating the time is created:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample3.aspx)]

<span data-ttu-id="195f3-119">Esse código é colocado na `<ContentTemplate>` seção de um `UpdatePanel` elemento.</span><span class="sxs-lookup"><span data-stu-id="195f3-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="195f3-120">O painel `UpdateMode` atributo deve ser definido como `"Conditional"`, já que apenas os gatilhos podem atualizar o conteúdo do painel.</span><span class="sxs-lookup"><span data-stu-id="195f3-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="195f3-121">No `<Triggers>` seção o `UpdatePanel`, um gatilho de postback assíncrono é criado e vinculado ao `Click` evento do botão.</span><span class="sxs-lookup"><span data-stu-id="195f3-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="195f3-122">Portanto, se o usuário clica no botão, o `UpdatePanel` é atualizado.</span><span class="sxs-lookup"><span data-stu-id="195f3-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="195f3-123">Aqui está a marcação para o `UpdatePanel` controle:</span><span class="sxs-lookup"><span data-stu-id="195f3-123">Here is the markup for the `UpdatePanel` control:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample4.aspx)]

<span data-ttu-id="195f3-124">Por fim, o `UpdatePanelAnimationExtender` devem ser configurados: Defina o `TargetControlID` para a ID do painel de atributo e definir uma animação dentro do extensor.</span><span class="sxs-lookup"><span data-stu-id="195f3-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="195f3-125">Fade in faz sentido, o que cria uma ótima visual enfatiza a hora da atualização.</span><span class="sxs-lookup"><span data-stu-id="195f3-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="195f3-126">Sua marcação de extensor pode, em seguida, esta aparência:</span><span class="sxs-lookup"><span data-stu-id="195f3-126">Your extender markup may then look like this:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample5.aspx)]

<span data-ttu-id="195f3-127">Execute o arquivo no navegador.</span><span class="sxs-lookup"><span data-stu-id="195f3-127">Run the file in the browser.</span></span> <span data-ttu-id="195f3-128">Sempre que você clica no botão, a hora atual é mostrada no painel, sempre fade in para a duração de um segundo.</span><span class="sxs-lookup"><span data-stu-id="195f3-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>


<span data-ttu-id="195f3-129">[![A hora atual está desaparecendo](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="195f3-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)</span></span>

<span data-ttu-id="195f3-130">A hora atual está desaparecendo ([clique para exibir a imagem em tamanho normal](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="195f3-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="195f3-131">Anterior</span><span class="sxs-lookup"><span data-stu-id="195f3-131">Previous</span></span>](animating-an-updatepanel-control-vb.md)
