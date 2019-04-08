---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
title: Predefinição de entradas de lista com CascadingDropDown (C#) | Microsoft Docs
author: wenz
description: O controle CascadingDropDown do AJAX Control Toolkit estende um controle DropDownList, de modo que as alterações em uma carga de DropDownList associado valores em anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 04c79748-0f21-4a3b-aba5-e1ce3161c32e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 2599b5015f288b2e8d02577a0865252a862574a4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049993"
---
<a name="presetting-list-entries-with-cascadingdropdown-c"></a><span data-ttu-id="99c4f-103">Predefinição de entradas de lista com CascadingDropDown (C#)</span><span class="sxs-lookup"><span data-stu-id="99c4f-103">Presetting List Entries with CascadingDropDown (C#)</span></span>
====================
<span data-ttu-id="99c4f-104">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="99c4f-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="99c4f-105">[Baixar o código](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="99c4f-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)</span></span>

> <span data-ttu-id="99c4f-106">O controle CascadingDropDown do AJAX Control Toolkit estende um controle DropDownList, de modo que as alterações em uma carga de DropDownList associadas a valores em outra DropDownList.</span><span class="sxs-lookup"><span data-stu-id="99c4f-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="99c4f-107">Com um pouco de código, é possível que um elemento de lista é pré-selecionado após os dados serem carregados dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="99c4f-107">With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>


## <a name="overview"></a><span data-ttu-id="99c4f-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="99c4f-108">Overview</span></span>

<span data-ttu-id="99c4f-109">O controle CascadingDropDown do AJAX Control Toolkit estende um controle DropDownList, de modo que as alterações em uma carga de DropDownList associadas a valores em outra DropDownList.</span><span class="sxs-lookup"><span data-stu-id="99c4f-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="99c4f-110">(Por exemplo, uma lista fornece uma lista de estados dos EUA e a lista seguinte, em seguida, é preenchida com principais cidades nesse estado.) Com um pouco de código, é possível que um elemento de lista é pré-selecionado após os dados serem carregados dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="99c4f-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="steps"></a><span data-ttu-id="99c4f-111">Etapas</span><span class="sxs-lookup"><span data-stu-id="99c4f-111">Steps</span></span>

<span data-ttu-id="99c4f-112">Para ativar a funcionalidade do AJAX ASP.NET e o Kit de ferramentas de controle, o `ScriptManager` controle deve ser colocada em qualquer lugar na página (mas dentro de `<form>` elemento):</span><span class="sxs-lookup"><span data-stu-id="99c4f-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample1.aspx)]

<span data-ttu-id="99c4f-113">Em seguida, um controle DropDownList é necessário:</span><span class="sxs-lookup"><span data-stu-id="99c4f-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample2.aspx)]

<span data-ttu-id="99c4f-114">Para obter essa lista, um extensor de CascadingDropDown é adicionado, fornecendo as informações de URL e o método de serviço web:</span><span class="sxs-lookup"><span data-stu-id="99c4f-114">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample3.aspx)]

<span data-ttu-id="99c4f-115">O extensor CascadingDropDown chama assincronamente um serviço web com a assinatura de método a seguir:</span><span class="sxs-lookup"><span data-stu-id="99c4f-115">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-csharp[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample4.cs)]

<span data-ttu-id="99c4f-116">O método retorna uma matriz do tipo valor CascadingDropDown.</span><span class="sxs-lookup"><span data-stu-id="99c4f-116">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="99c4f-117">O construtor do tipo primeiro espera legenda da entrada de lista e, em seguida, o valor (HTML `value` atributo).</span><span class="sxs-lookup"><span data-stu-id="99c4f-117">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span> <span data-ttu-id="99c4f-118">Se o terceiro argumento é definido como true, a lista de elemento é selecionado automaticamente no navegador.</span><span class="sxs-lookup"><span data-stu-id="99c4f-118">If the third argument is set to true, the list element is automatically selected in the browser.</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample5.aspx)]

<span data-ttu-id="99c4f-119">Carregamento da página no navegador preencherá a lista suspensa com três fornecedores, o segundo é que está sendo pré-selecionado.</span><span class="sxs-lookup"><span data-stu-id="99c4f-119">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span>


<span data-ttu-id="99c4f-120">[![A lista é preenchida e pré-selecionado automaticamente](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="99c4f-120">[![The list is filled and preselected automatically](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)</span></span>

<span data-ttu-id="99c4f-121">A lista é preenchida e pré-selecionado automaticamente ([clique para exibir a imagem em tamanho normal](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="99c4f-121">The list is filled and preselected automatically ([Click to view full-size image](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="99c4f-122">[Anterior](using-cascadingdropdown-with-a-database-cs.md)
> [Próximo](using-auto-postback-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="99c4f-122">[Previous](using-cascadingdropdown-with-a-database-cs.md)
[Next](using-auto-postback-with-cascadingdropdown-cs.md)</span></span>
