---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: Uso de vários controles pop-up (c#) | Microsoft Docs
author: wenz
description: O extensor PopupControl no AJAX Control Toolkit oferece uma maneira fácil de disparar um pop-up quando qualquer outro controle é ativado. Também é possível usar o m...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 498afada4e020d0edf8dabef5d4a00336e15c5f5
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65115138"
---
# <a name="using-multiple-popup-controls-c"></a><span data-ttu-id="ab157-104">Uso de vários controles pop-up (C#)</span><span class="sxs-lookup"><span data-stu-id="ab157-104">Using Multiple Popup Controls (C#)</span></span>

<span data-ttu-id="ab157-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ab157-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ab157-106">[Baixar o código](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ab157-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span></span>

> <span data-ttu-id="ab157-107">O extensor PopupControl no AJAX Control Toolkit oferece uma maneira fácil de disparar um pop-up quando qualquer outro controle é ativado.</span><span class="sxs-lookup"><span data-stu-id="ab157-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="ab157-108">Também é possível usar mais de um controle pop-up em uma única página.</span><span class="sxs-lookup"><span data-stu-id="ab157-108">It is also possible to use more than one popup control on one page.</span></span>

## <a name="overview"></a><span data-ttu-id="ab157-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ab157-109">Overview</span></span>

<span data-ttu-id="ab157-110">O extensor PopupControl no AJAX Control Toolkit oferece uma maneira fácil de disparar um pop-up quando qualquer outro controle é ativado.</span><span class="sxs-lookup"><span data-stu-id="ab157-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="ab157-111">Também é possível usar mais de um controle pop-up em uma única página.</span><span class="sxs-lookup"><span data-stu-id="ab157-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="ab157-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="ab157-112">Steps</span></span>

<span data-ttu-id="ab157-113">Para ativar a funcionalidade do AJAX ASP.NET e o Kit de ferramentas de controle, o `ScriptManager` controle deve ser colocada em qualquer lugar na página (mas dentro de `<form>` elemento):</span><span class="sxs-lookup"><span data-stu-id="ab157-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="ab157-114">Em seguida, adicione um painel que serve como o pop-up.</span><span class="sxs-lookup"><span data-stu-id="ab157-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="ab157-115">No cenário atual, o painel contém um `Calendar` controle.</span><span class="sxs-lookup"><span data-stu-id="ab157-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="ab157-116">Para evitar as atualizações de página causadas por postagens do calendário, o painel é colocado dentro um `UpdatePanel` controle:</span><span class="sxs-lookup"><span data-stu-id="ab157-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="ab157-117">A página também contém duas caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="ab157-117">The page also contains two text boxes.</span></span> <span data-ttu-id="ab157-118">Para cada caixa de texto, o calendário pop-up deverão aparecer depois que a caixa de texto for ativada.</span><span class="sxs-lookup"><span data-stu-id="ab157-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="ab157-119">Agora estender cada uma das duas caixas de texto com um `PopupControlExtender`.</span><span class="sxs-lookup"><span data-stu-id="ab157-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="ab157-120">O `TargetControlID` atributo fornece a ID do controle ligado ao extensor.</span><span class="sxs-lookup"><span data-stu-id="ab157-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="ab157-121">O `PopupControlID` atributo contém a ID do painel pop-up.</span><span class="sxs-lookup"><span data-stu-id="ab157-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="ab157-122">Nesse caso, ambos os extensores mostram o mesmo painel, mas diferentes painéis são possíveis, também.</span><span class="sxs-lookup"><span data-stu-id="ab157-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="ab157-123">Agora sempre que você clica em um campo de texto, um calendário aparece abaixo do campo, permitindo que você selecione uma data.</span><span class="sxs-lookup"><span data-stu-id="ab157-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="ab157-124">(Voltando a data selecionada nas caixas de texto será abordado em um tutorial diferente.)</span><span class="sxs-lookup"><span data-stu-id="ab157-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>

<span data-ttu-id="ab157-125">[![O calendário é exibido quando o usuário clica na caixa de texto](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ab157-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="ab157-126">O calendário é exibido quando o usuário clica na caixa de texto ([clique para exibir a imagem em tamanho normal](using-multiple-popup-controls-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ab157-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ab157-127">Avançar</span><span class="sxs-lookup"><span data-stu-id="ab157-127">Next</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
