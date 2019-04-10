---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: Modificando animações pelo lado do servidor (VB) | Microsoft Docs
author: wenz
description: O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle. As animações podem também...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: fb7e992246b9c630d99a1493f344c4089540d67e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59398079"
---
# <a name="modifying-animations-from-the-server-side-vb"></a><span data-ttu-id="95ac7-104">Modificando animações pelo lado do servidor (VB)</span><span class="sxs-lookup"><span data-stu-id="95ac7-104">Modifying Animations From The Server Side (VB)</span></span>

<span data-ttu-id="95ac7-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="95ac7-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="95ac7-106">[Baixar o código](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) ou [baixar PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="95ac7-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span></span>

> <span data-ttu-id="95ac7-107">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="95ac7-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="95ac7-108">As animações também podem ser alteradas no lado do servidor</span><span class="sxs-lookup"><span data-stu-id="95ac7-108">The animations may also be changed on the server-side</span></span>


## <a name="overview"></a><span data-ttu-id="95ac7-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="95ac7-109">Overview</span></span>

<span data-ttu-id="95ac7-110">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="95ac7-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="95ac7-111">As animações também podem ser alteradas no lado do servidor</span><span class="sxs-lookup"><span data-stu-id="95ac7-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="95ac7-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="95ac7-112">Steps</span></span>

<span data-ttu-id="95ac7-113">Em primeiro lugar, inclua o `ScriptManager` na página; em seguida, a biblioteca do AJAX ASP.NET é carregada, tornando possível usar o Kit de ferramentas de controle:</span><span class="sxs-lookup"><span data-stu-id="95ac7-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

<span data-ttu-id="95ac7-114">A animação será aplicada a um painel de texto que tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="95ac7-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

<span data-ttu-id="95ac7-115">Na classe CSS associado para o painel, definir uma cor de fundo interessante e também definir uma largura fixa para o painel:</span><span class="sxs-lookup"><span data-stu-id="95ac7-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

<span data-ttu-id="95ac7-116">O restante do código é executado no lado do servidor e não usa marcação; em vez disso, ele usa o código para criar o `AnimationExtender` controle:</span><span class="sxs-lookup"><span data-stu-id="95ac7-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

<span data-ttu-id="95ac7-117">No entanto, o Kit de ferramentas de controle atualmente não fornece um acesso de API para criar as animações individuais.</span><span class="sxs-lookup"><span data-stu-id="95ac7-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="95ac7-118">No entanto, é possível definir o `AnimationExtender`propriedade Animations para uma cadeia de caracteres que contém a marcação XML usada ao atribuir as animações de forma declarativa.</span><span class="sxs-lookup"><span data-stu-id="95ac7-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="95ac7-119">Para criar o XML que não deve conter o `<Animations>` elemento, você pode usar o XML do .NET Framework dão suporte ou, como no código a seguir, basta fornecer a cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="95ac7-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

<span data-ttu-id="95ac7-120">Por fim, adicione a `AnimationExtender` dentro de controle para a página atual, o `<form runat="server">` elemento, certificando-se de que a animação está incluída e é executado:</span><span class="sxs-lookup"><span data-stu-id="95ac7-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]


[![T<span data-ttu-id="95ac7-121">animação he é criada usando o servidor C#código /VB]</span><span class="sxs-lookup"><span data-stu-id="95ac7-121">he animation is created using server-side C#/VB code]</span></span>(modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)

<span data-ttu-id="95ac7-122">A animação é criada usando o código do lado do servidor C# /VB ([clique para exibir a imagem em tamanho normal](modifying-animations-from-the-server-side-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="95ac7-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="95ac7-123">[Anterior](triggering-an-animation-in-another-control-vb.md)
> [Próximo](executing-animations-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="95ac7-123">[Previous](triggering-an-animation-in-another-control-vb.md)
[Next](executing-animations-using-client-side-code-vb.md)</span></span>
