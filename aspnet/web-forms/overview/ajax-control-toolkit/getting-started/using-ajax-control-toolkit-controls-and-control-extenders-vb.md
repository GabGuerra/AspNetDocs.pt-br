---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: Usando controles do Kit de ferramentas de controle AJAX e extensores de controle (VB) | Microsoft Docs
author: microsoft
description: Saiba como adicionar controles do AJAX Control Toolkit e extensores para suas páginas ASP.NET.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: f1cf40ec3ba299ee2702258a93aa1192a2112e7f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047453"
---
<a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a><span data-ttu-id="d6402-103">Uso de controles e extensores de controle do AJAX Control Toolkit (VB)</span><span class="sxs-lookup"><span data-stu-id="d6402-103">Using AJAX Control Toolkit Controls and Control Extenders (VB)</span></span>
====================
<span data-ttu-id="d6402-104">por [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d6402-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d6402-105">Saiba como adicionar controles do AJAX Control Toolkit e extensores para suas páginas ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d6402-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>


<span data-ttu-id="d6402-106">O AJAX Control Toolkit contém um conjunto de controles e extensores de controle.</span><span class="sxs-lookup"><span data-stu-id="d6402-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="d6402-107">Este breve tutorial, você aprenderá como adicionar controles e extensores de controle a uma página ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d6402-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="d6402-108">Para obter instruções sobre como instalar o AJAX Control Toolkit e adicionando o AJAX Control Toolkit para a caixa de ferramentas do Visual Studio/Visual Web Developer, consulte o tutorial [Introdução ao AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb.md).</span><span class="sxs-lookup"><span data-stu-id="d6402-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb.md).</span></span>


## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="d6402-109">Usando controles do Kit de ferramentas de controle AJAX</span><span class="sxs-lookup"><span data-stu-id="d6402-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="d6402-110">Um controle do AJAX Control Toolkit funciona como um controle ASP.NET normal.</span><span class="sxs-lookup"><span data-stu-id="d6402-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="d6402-111">Você pode arrastar o controle da caixa de ferramentas em uma página ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d6402-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="d6402-112">Você pode adicionar o controle para a página no modo de exibição de Design ou exibição da fonte.</span><span class="sxs-lookup"><span data-stu-id="d6402-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="d6402-113">Há um requisito especial ao usar os controles do AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="d6402-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="d6402-114">A página deve conter um controle ScriptManager.</span><span class="sxs-lookup"><span data-stu-id="d6402-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="d6402-115">O controle ScriptManager é responsável por incluir todos o JavaScript necessário necessário pelos controles AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="d6402-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="d6402-116">Por exemplo, na guia do AJAX Control Toolkit inclui um controle chamado o controle do Editor.</span><span class="sxs-lookup"><span data-stu-id="d6402-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="d6402-117">Esse controle exibe um rico editor de HTML.</span><span class="sxs-lookup"><span data-stu-id="d6402-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="d6402-118">Siga estas etapas para adicionar o controle de Editor para uma página:</span><span class="sxs-lookup"><span data-stu-id="d6402-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="d6402-119">Criar uma nova página do ASP.NET chamada ShowEditor.aspx</span><span class="sxs-lookup"><span data-stu-id="d6402-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="d6402-120">Selecione o controle ScriptManager do guia Extensões AJAX na caixa de ferramentas e arraste o controle para a página.</span><span class="sxs-lookup"><span data-stu-id="d6402-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="d6402-121">Selecione o controle de Editor do AJAX Control Toolkit guia na caixa de ferramentas e arraste o controle para a página (consulte a Figura 1).</span><span class="sxs-lookup"><span data-stu-id="d6402-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="d6402-122">O Designer deve ser semelhante a Figura 2.</span><span class="sxs-lookup"><span data-stu-id="d6402-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="d6402-123">Executar o site selecionando a opção de menu **depurar, iniciar depuração** ou pressionando a tecla F5.</span><span class="sxs-lookup"><span data-stu-id="d6402-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="d6402-124">Você verá a página na Figura 3.</span><span class="sxs-lookup"><span data-stu-id="d6402-124">You should see the page in Figure 3.</span></span>


<span data-ttu-id="d6402-125">[![Selecionando o controle de Editor de HTML](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d6402-125">[![Selecting the HTML Editor control](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)</span></span>

<span data-ttu-id="d6402-126">**Figura 01**: Selecionando o controle de Editor de HTML ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="d6402-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))</span></span>


<span data-ttu-id="d6402-127">[![Designer do Visual Studio com o controle ScriptManager e editar](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d6402-127">[![Visual Studio Designer with ScriptManager and Edit control](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)</span></span>

<span data-ttu-id="d6402-128">**Figura 02**: Designer do Visual Studio com o controle ScriptManager e edição ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="d6402-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))</span></span>


<span data-ttu-id="d6402-129">[![A página DisplayEditor.aspx](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="d6402-129">[![The DisplayEditor.aspx page](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)</span></span>

<span data-ttu-id="d6402-130">**Figura 03**: A página DisplayEditor.aspx ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="d6402-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))</span></span>


## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="d6402-131">Usando extensores de controle do Kit de ferramentas de controle do AJAX</span><span class="sxs-lookup"><span data-stu-id="d6402-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="d6402-132">O AJAX Control Toolkit também contém os extensores de controle.</span><span class="sxs-lookup"><span data-stu-id="d6402-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="d6402-133">Como o nome sugere, um extensor de controle estende a funcionalidade de um controle existente.</span><span class="sxs-lookup"><span data-stu-id="d6402-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="d6402-134">Por exemplo, o extensor ConfirmButton do controle estende o controle de botão do ASP.NET padrão.</span><span class="sxs-lookup"><span data-stu-id="d6402-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="d6402-135">O extensor altera o comportamento de s de controle de botão para que o botão exibe uma caixa de diálogo de confirmação quando você clica nele.</span><span class="sxs-lookup"><span data-stu-id="d6402-135">The extender changes the Button control�s behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="d6402-136">Um extensor de controle, assim como um controle do AJAX Control Toolkit, requer um controle ScriptManager.</span><span class="sxs-lookup"><span data-stu-id="d6402-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="d6402-137">Você deve adicionar um controle ScriptManager para uma página para começar a usar extensores de controle na página.</span><span class="sxs-lookup"><span data-stu-id="d6402-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="d6402-138">Siga estas etapas para usar o extensor do controle ConfirmButton:</span><span class="sxs-lookup"><span data-stu-id="d6402-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="d6402-139">Criar uma nova página do ASP.NET chamada ShowConfirmButton.aspx</span><span class="sxs-lookup"><span data-stu-id="d6402-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="d6402-140">Adicione um controle ScriptManager à página, arrastando o controle para a página de guia Extensões AJAX.</span><span class="sxs-lookup"><span data-stu-id="d6402-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="d6402-141">Adicione um controle de botão padrão para a página, arrastando o botão de guia padrão na caixa de ferramentas para a superfície de Designer.</span><span class="sxs-lookup"><span data-stu-id="d6402-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="d6402-142">Clique o **adicionar extensor** opção de tarefa (consulte a Figura 4).</span><span class="sxs-lookup"><span data-stu-id="d6402-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="d6402-143">Na caixa de diálogo Choose Extender, selecione ConfirmButtonExtender (consulte a Figura 5) e clique no botão Okey.</span><span class="sxs-lookup"><span data-stu-id="d6402-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="d6402-144">Selecione o controle de botão no Designer e expanda os extensores, Button1\_ConfirmButtonExtender nó na janela Propriedades (veja a Figura 6).</span><span class="sxs-lookup"><span data-stu-id="d6402-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="d6402-145">Atribua o valor *realmente?* para a propriedade ConfirmText.</span><span class="sxs-lookup"><span data-stu-id="d6402-145">Assign the value *�Really?�* to the ConfirmText property.</span></span>
7. <span data-ttu-id="d6402-146">Execute a página, selecionando a opção de menu **depurar, iniciar depuração** ou pressionar a tecla F5.</span><span class="sxs-lookup"><span data-stu-id="d6402-146">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>


<span data-ttu-id="d6402-147">[![A opção de adicionar extensor de tarefas](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="d6402-147">[![The Add Extender task option](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)</span></span>

<span data-ttu-id="d6402-148">**Figura 04**: A opção de tarefa de adicionar extensor ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="d6402-148">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))</span></span>


<span data-ttu-id="d6402-149">[![Selecionando o extensor ConfirmButton do controle](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="d6402-149">[![Selecting the ConfirmButton control extender](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)</span></span>

<span data-ttu-id="d6402-150">**Figura 05**: Selecionando o extensor ConfirmButton do controle ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="d6402-150">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))</span></span>


<span data-ttu-id="d6402-151">[![Definir uma propriedade ConfirmButton](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="d6402-151">[![Setting a ConfirmButton property](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)</span></span>

<span data-ttu-id="d6402-152">**Figura 06**: Definir uma propriedade ConfirmButton ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="d6402-152">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))</span></span>


<span data-ttu-id="d6402-153">Quando a página é aberta, você verá um botão.</span><span class="sxs-lookup"><span data-stu-id="d6402-153">When the page opens, you should see a button.</span></span> <span data-ttu-id="d6402-154">Quando você clica no botão, você obtém a caixa de diálogo de confirmação na Figura 7.</span><span class="sxs-lookup"><span data-stu-id="d6402-154">When you click the button, you get the confirmation dialog in Figure 7.</span></span>


<span data-ttu-id="d6402-155">[![Exibir a caixa de diálogo de confirmação](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="d6402-155">[![Displaying the confirmation dialog](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)</span></span>

<span data-ttu-id="d6402-156">**Figura 07**: Exibir a caixa de diálogo de confirmação ([clique para exibir a imagem em tamanho normal](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="d6402-156">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))</span></span>


<span data-ttu-id="d6402-157">Observe que você normalmente não arrastar um extensor de controle para uma página.</span><span class="sxs-lookup"><span data-stu-id="d6402-157">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="d6402-158">Em vez disso, você usa o **adicionar extensor** opção para adicionar um extensor a um controle que você já tiver adicionado a uma página de tarefas.</span><span class="sxs-lookup"><span data-stu-id="d6402-158">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="d6402-159">Além disso, observe que você defina controle extensor propriedades abrindo a folha de propriedades para o controle que está sendo estendido.</span><span class="sxs-lookup"><span data-stu-id="d6402-159">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="d6402-160">Um único controle ASP.NET pode ser estendido por vários extensores de controle.</span><span class="sxs-lookup"><span data-stu-id="d6402-160">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="d6402-161">A folha de propriedades para o controle que está sendo estendido lista todos os extensores de controle associados ao controle.</span><span class="sxs-lookup"><span data-stu-id="d6402-161">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d6402-162">[Anterior](get-started-with-the-ajax-control-toolkit-vb.md)
> [Próximo](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d6402-162">[Previous](get-started-with-the-ajax-control-toolkit-vb.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)</span></span>
