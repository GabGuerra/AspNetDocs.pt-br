---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: Usando o controle deslizante com Postback automático (c#) | Microsoft Docs
author: wenz
description: O controle deslizante no AJAX Control Toolkit fornece um controle deslizante gráfico que pode ser controlado usando o mouse. É possível fazer a lançar automaticamente slider...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: a5b858a05470caa244902afbb404adbb2e4761b7
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59402720"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a><span data-ttu-id="5ec53-104">Usando o controle deslizante com Postback automático (c#)</span><span class="sxs-lookup"><span data-stu-id="5ec53-104">Using the Slider Control With Auto-Postback (C#)</span></span>

<span data-ttu-id="5ec53-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5ec53-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5ec53-106">[Baixar o código](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="5ec53-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span></span>

> <span data-ttu-id="5ec53-107">O controle deslizante no AJAX Control Toolkit fornece um controle deslizante gráfico que pode ser controlado usando o mouse.</span><span class="sxs-lookup"><span data-stu-id="5ec53-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="5ec53-108">É possível fazer o controle deslizante autopostback uma vez, seu valor for alterado.</span><span class="sxs-lookup"><span data-stu-id="5ec53-108">It is possible to make the slider autopostback once its value changes.</span></span>


## <a name="overview"></a><span data-ttu-id="5ec53-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5ec53-109">Overview</span></span>

<span data-ttu-id="5ec53-110">O controle deslizante no AJAX Control Toolkit fornece um controle deslizante gráfico que pode ser controlado usando o mouse.</span><span class="sxs-lookup"><span data-stu-id="5ec53-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="5ec53-111">É possível fazer o controle deslizante autopostback uma vez, seu valor for alterado.</span><span class="sxs-lookup"><span data-stu-id="5ec53-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="5ec53-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="5ec53-112">Steps</span></span>

<span data-ttu-id="5ec53-113">Para fazer o controle deslizante com postback automaticamente após uma alteração, ambas as caixas de texto precisam do atributo `AutoPostBack="true"`: Caixa de texto que se tornará o controle deslizante em si e a caixa de texto que contém a posição do controle deslizante.</span><span class="sxs-lookup"><span data-stu-id="5ec53-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="5ec53-114">Aqui está a marcação necessária para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="5ec53-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

<span data-ttu-id="5ec53-115">O `SliderExtender` controle do ASP.NET AJAX Control Toolkit atribui a funcionalidade de controle deslizante para duas caixas de texto:</span><span class="sxs-lookup"><span data-stu-id="5ec53-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

<span data-ttu-id="5ec53-116">Um elemento de rótulo adicional será usado mais tarde para informar o usuário de um postback:</span><span class="sxs-lookup"><span data-stu-id="5ec53-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

<span data-ttu-id="5ec53-117">Por fim, o `ScriptManager` controle do ASP.NET AJAX carrega o JavaScript necessário para o Kit de ferramentas trabalhar:</span><span class="sxs-lookup"><span data-stu-id="5ec53-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

<span data-ttu-id="5ec53-118">Agora o controle deslizante está postando novamente; no lado do servidor, esse evento pode ser detectado e tratado:</span><span class="sxs-lookup"><span data-stu-id="5ec53-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]


<span data-ttu-id="5ec53-119">[![Movendo o controle deslizante dispara um postback](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5ec53-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span></span>

<span data-ttu-id="5ec53-120">Movendo o controle deslizante dispara um postback ([clique para exibir a imagem em tamanho normal](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5ec53-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span></span>


<span data-ttu-id="5ec53-121">[![Depois disso, a data desta alteração é gravada no rótulo](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="5ec53-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span></span>

<span data-ttu-id="5ec53-122">Depois disso, a data desta alteração é gravada no rótulo ([clique para exibir a imagem em tamanho normal](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="5ec53-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5ec53-123">Avançar</span><span class="sxs-lookup"><span data-stu-id="5ec53-123">Next</span></span>](databinding-the-slider-control-cs.md)
