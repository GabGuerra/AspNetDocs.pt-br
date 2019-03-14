---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: Alterar uma animação usando o código do lado do cliente (c#) | Microsoft Docs
author: wenz
description: O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle. A animação também pode...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 253377ef6019a672680c6e819349357627ef111b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024523"
---
<a name="changing-an-animation-using-client-side-code-c"></a><span data-ttu-id="54b6a-104">Alterar uma animação usando o código do lado do cliente (C#)</span><span class="sxs-lookup"><span data-stu-id="54b6a-104">Changing an Animation Using Client-Side Code (C#)</span></span>
====================
<span data-ttu-id="54b6a-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="54b6a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="54b6a-106">[Baixar o código](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="54b6a-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span></span>

> <span data-ttu-id="54b6a-107">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="54b6a-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="54b6a-108">A animação pode ser alterada usando código personalizado de JavaScript do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="54b6a-108">The animation can also be changed using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="54b6a-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="54b6a-109">Overview</span></span>

<span data-ttu-id="54b6a-110">O controle de animação no ASP.NET AJAX Control Toolkit não é apenas um controle, mas uma estrutura inteira para adicionar animações a um controle.</span><span class="sxs-lookup"><span data-stu-id="54b6a-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="54b6a-111">A animação pode ser alterada usando código personalizado de JavaScript do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="54b6a-111">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="54b6a-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="54b6a-112">Steps</span></span>

<span data-ttu-id="54b6a-113">Em primeiro lugar, inclua o `ScriptManager` na página; em seguida, a biblioteca do AJAX ASP.NET é carregada, tornando possível usar o Kit de ferramentas de controle:</span><span class="sxs-lookup"><span data-stu-id="54b6a-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="54b6a-114">A animação será aplicada a um painel de texto que tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="54b6a-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="54b6a-115">Na classe CSS associado para o painel, definir uma cor de fundo interessante e também definir uma largura fixa para o painel:</span><span class="sxs-lookup"><span data-stu-id="54b6a-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="54b6a-116">A animação real é iniciada por um botão HTML:</span><span class="sxs-lookup"><span data-stu-id="54b6a-116">The actual animation is launched by an HTML button:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="54b6a-117">Em seguida, adicione a `AnimationExtender` para a página, fornecendo uma `ID`, o `TargetControlID` atributo e o obrigatoriamente `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="54b6a-117">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

<span data-ttu-id="54b6a-118">Observe que não há nenhuma `<Animations>` nó dentro de `AnimationExtender` controle.</span><span class="sxs-lookup"><span data-stu-id="54b6a-118">Note that there is no `<Animations>` node within the `AnimationExtender` control.</span></span> <span data-ttu-id="54b6a-119">Código JavaScript personalizado é usado para fornecer as animações a serem usados com o controle.</span><span class="sxs-lookup"><span data-stu-id="54b6a-119">Custom JavaScript code is used to provide the animations to be used with the control.</span></span>

<span data-ttu-id="54b6a-120">Assim como acontece com a API do servidor de `AnimationExtender`, não há nenhuma maneira fácil para atribuir uma animação para o extensor ainda.</span><span class="sxs-lookup"><span data-stu-id="54b6a-120">As with the server API of `AnimationExtender`, there is no easy way to assign an animation to the extender yet.</span></span> <span data-ttu-id="54b6a-121">No entanto o extensor expõe vários métodos para ler e gravar animações registrado com os vários eventos (`OnClick`, `OnLoad`e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="54b6a-121">However the extender does expose several methods to read and write animations registered with the various events (`OnClick`, `OnLoad`, and so on).</span></span> <span data-ttu-id="54b6a-122">Estes são alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="54b6a-122">Here are some examples:</span></span>

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

<span data-ttu-id="54b6a-123">O formato do valor de retorno do `get_*()` funções e o formato do argumento para o `set_*()` functions é uma cadeia de caracteres JSON, fornecendo uma representação de objeto do qual seria a marcação XML.</span><span class="sxs-lookup"><span data-stu-id="54b6a-123">The format of the return value of the `get_*()` functions and the format of the argument for the `set_*()` functions is a JSON string, providing an object representation of what the XML markup would be.</span></span> <span data-ttu-id="54b6a-124">Atualmente, não há nenhuma maneira de passar um objeto no, mas é possível ler um objeto de uma determinada animação (`get_OnXXXBehavior()` métodos).</span><span class="sxs-lookup"><span data-stu-id="54b6a-124">Currently, there is no way to pass an object in, but it is possible to read an object from a given animation (`get_OnXXXBehavior()` methods).</span></span>

<span data-ttu-id="54b6a-125">Aqui está uma cadeia de caracteres JSON (sem as aspas de delimitação e formatado legalmente) que representa uma animação disparada pelo botão, mas Animando o painel, redimensioná-la e desaparecimento ao mesmo tempo:</span><span class="sxs-lookup"><span data-stu-id="54b6a-125">Here is a JSON string (without the delimiting quotes and formatted nicely) representing an animation triggered by the button, but animating the panel by resizing it and fading it out at the same time:</span></span>

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

<span data-ttu-id="54b6a-126">O código JavaScript a seguir atribui esse descripting JSON para o `OnClick` animação do extensor atual e a executa:</span><span class="sxs-lookup"><span data-stu-id="54b6a-126">The following JavaScript code assigns this JSON descripting to the `OnClick` animation of the current extender and runs it:</span></span>

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]


<span data-ttu-id="54b6a-127">[![A animação é executada imediatamente, sem um clique do mouse (e com muito pouco de marcação)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="54b6a-127">[![The animation runs immediately, without a mouse click (and with very little markup)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="54b6a-128">A animação é executada imediatamente, sem um clique do mouse (e com muito pouco de marcação) ([clique para exibir a imagem em tamanho normal](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="54b6a-128">The animation runs immediately, without a mouse click (and with very little markup) ([Click to view full-size image](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="54b6a-129">[Anterior](executing-animations-using-client-side-code-cs.md)
> [Próximo](animating-an-updatepanel-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="54b6a-129">[Previous](executing-animations-using-client-side-code-cs.md)
[Next](animating-an-updatepanel-control-cs.md)</span></span>
