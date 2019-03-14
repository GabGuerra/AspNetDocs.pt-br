---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: Manipulando propriedades de DropShadow através de código do cliente (VB) | Microsoft Docs
author: wenz
description: O controle de DropShadow no AJAX Control Toolkit, um painel com uma sombra. Propriedades desse extensor também podem ser alteradas usando o cliente JavaScript&lt;2}&lt;1}...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: d8b8330174f6f49e96c42a0e15eeaf934bf24f87
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048363"
---
<a name="manipulating-dropshadow-properties-from-client-code-vb"></a><span data-ttu-id="f0912-104">Manipular propriedades de DropShadow através de código de cliente (VB)</span><span class="sxs-lookup"><span data-stu-id="f0912-104">Manipulating DropShadow Properties from Client Code (VB)</span></span>
====================
<span data-ttu-id="f0912-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f0912-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f0912-106">[Baixar o código](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) ou [baixar PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f0912-106">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span></span>

> <span data-ttu-id="f0912-107">O controle de DropShadow no AJAX Control Toolkit, um painel com uma sombra.</span><span class="sxs-lookup"><span data-stu-id="f0912-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="f0912-108">Propriedades desse extensor também podem ser alteradas usando o código de JavaScript do cliente.</span><span class="sxs-lookup"><span data-stu-id="f0912-108">Properties of this extender can also be changed using client JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="f0912-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f0912-109">Overview</span></span>

<span data-ttu-id="f0912-110">O controle de DropShadow no AJAX Control Toolkit, um painel com uma sombra.</span><span class="sxs-lookup"><span data-stu-id="f0912-110">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="f0912-111">Propriedades desse extensor também podem ser alteradas usando o código de JavaScript do cliente.</span><span class="sxs-lookup"><span data-stu-id="f0912-111">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="f0912-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="f0912-112">Steps</span></span>

<span data-ttu-id="f0912-113">O código começa com um painel que contém algumas linhas de texto:</span><span class="sxs-lookup"><span data-stu-id="f0912-113">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

<span data-ttu-id="f0912-114">A classe CSS associada fornece o painel de uma cor de fundo interessante:</span><span class="sxs-lookup"><span data-stu-id="f0912-114">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

<span data-ttu-id="f0912-115">O `DropShadowExtender` é adicionado ao estender o painel com um efeito de sombra, definido como 50% de opacidade:</span><span class="sxs-lookup"><span data-stu-id="f0912-115">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

<span data-ttu-id="f0912-116">Em seguida, o ASP.NET AJAX `ScriptManager` controle permite que o Kit de ferramentas trabalhar:</span><span class="sxs-lookup"><span data-stu-id="f0912-116">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

<span data-ttu-id="f0912-117">Outro painel contém dois links de JavaScript para definir a opacidade da sombra: o link do sinal de subtração diminui a opacidade da sombra, o link de adição aumenta a ele.</span><span class="sxs-lookup"><span data-stu-id="f0912-117">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

<span data-ttu-id="f0912-118">A função JavaScript `changeOpacity()` , em seguida, deve primeiro localizar o `DropShadowExtender` controle na página.</span><span class="sxs-lookup"><span data-stu-id="f0912-118">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="f0912-119">ASP.NET AJAX define o `$find()` método para exatamente essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="f0912-119">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="f0912-120">Em seguida, o `get_Opacity()` método recupera a opacidade atual, o `set_Opacity()` método define a ele.</span><span class="sxs-lookup"><span data-stu-id="f0912-120">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="f0912-121">O código JavaScript, em seguida, coloca o valor de opacidade atual no `<label>` elemento:</span><span class="sxs-lookup"><span data-stu-id="f0912-121">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]


<span data-ttu-id="f0912-122">[![A opacidade é alterada no lado do cliente](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f0912-122">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="f0912-123">A opacidade é alterada no lado do cliente ([clique para exibir a imagem em tamanho normal](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f0912-123">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f0912-124">Anterior</span><span class="sxs-lookup"><span data-stu-id="f0912-124">Previous</span></span>](adjusting-the-z-index-of-a-dropshadow-vb.md)
