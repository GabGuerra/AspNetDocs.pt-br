---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
title: Usar o extensor de controle ColorPicker (c#) | Microsoft Docs
author: microsoft
description: ColorPicker é um extensor ASP.NET AJAX que fornece funcionalidade de separação de cor do lado do cliente com interface do usuário em um controle pop-up. Ele pode ser anexado a qualquer ASP.NET...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0d86a1e7-a910-4ab2-b85c-7a9ea6906c39
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 58b8d581ed426227ed77435e22c84e9ea5d62ebe
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040043"
---
<a name="using-the-colorpicker-control-extender-c"></a><span data-ttu-id="6db70-104">Usar o extensor de controle ColorPicker (c#)</span><span class="sxs-lookup"><span data-stu-id="6db70-104">Using the ColorPicker Control Extender (C#)</span></span>
====================
<span data-ttu-id="6db70-105">por [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6db70-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6db70-106">ColorPicker é um extensor ASP.NET AJAX que fornece funcionalidade de separação de cor do lado do cliente com interface do usuário em um controle pop-up.</span><span class="sxs-lookup"><span data-stu-id="6db70-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="6db70-107">Ele pode ser anexado a qualquer controle TextBox do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6db70-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="6db70-108">-Lo.</span><span class="sxs-lookup"><span data-stu-id="6db70-108">It.</span></span>


<span data-ttu-id="6db70-109">O objetivo deste tutorial é explicar como você pode usar o extensor do controle ColorPicker de kit de ferramentas de controle do AJAX.</span><span class="sxs-lookup"><span data-stu-id="6db70-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="6db70-110">O extensor de controle ColorPicker exibe uma caixa de diálogo pop-up que permite que você selecione uma cor.</span><span class="sxs-lookup"><span data-stu-id="6db70-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="6db70-111">ColorPicker é útil sempre que você deseja fornecer uma interface de usuário intuitiva para um usuário selecionar uma cor.</span><span class="sxs-lookup"><span data-stu-id="6db70-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="6db70-112">Estendendo um controle de caixa de texto com o extensor de controle ColorPicker</span><span class="sxs-lookup"><span data-stu-id="6db70-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="6db70-113">Por exemplo, imagine que você deseja criar um site que permite aos visitantes criar cartões de visita personalizados.</span><span class="sxs-lookup"><span data-stu-id="6db70-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="6db70-114">Os visitantes podem digitar o texto para um cartão de visita e escolher a cor.</span><span class="sxs-lookup"><span data-stu-id="6db70-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="6db70-115">A página ASP.NET na listagem 1 contém dois controles de caixa de texto chamado txtCardText e txtCardColor.</span><span class="sxs-lookup"><span data-stu-id="6db70-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="6db70-116">Quando você envia o formulário, os valores selecionados são exibidos (consulte a Figura 1).</span><span class="sxs-lookup"><span data-stu-id="6db70-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>


<span data-ttu-id="6db70-117">[![Formulário simples para a criação de um cartão de visita](using-the-colorpicker-control-extender-cs/_static/image1.jpg)](using-the-colorpicker-control-extender-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6db70-117">[![Simple form for creating a business card](using-the-colorpicker-control-extender-cs/_static/image1.jpg)](using-the-colorpicker-control-extender-cs/_static/image1.png)</span></span>

<span data-ttu-id="6db70-118">**Figura 01**: Formulário simples para a criação de um cartão de visita ([clique para exibir a imagem em tamanho normal](using-the-colorpicker-control-extender-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="6db70-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image2.png))</span></span>


<span data-ttu-id="6db70-119">**Listagem 1 - CreateCard.aspx**</span><span class="sxs-lookup"><span data-stu-id="6db70-119">**Listing 1 - CreateCard.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample1.aspx)]

<span data-ttu-id="6db70-120">O formulário na listagem 1 funciona, mas não fornece uma excelente experiência de usuário.</span><span class="sxs-lookup"><span data-stu-id="6db70-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="6db70-121">O usuário deve digitar uma cor na caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6db70-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="6db70-122">Se o usuário deseja uma cor especializada - por exemplo, apenas a direito tonalidade de verde pea – e em seguida, o usuário deve descobrir o código de cor HTML sem qualquer ajuda.</span><span class="sxs-lookup"><span data-stu-id="6db70-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="6db70-123">Você pode usar o extensor do controle ColorPicker para criar uma melhor experiência do usuário.</span><span class="sxs-lookup"><span data-stu-id="6db70-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="6db70-124">ColorPicker exibe uma caixa de diálogo de cor quando você move o foco para um controle TextBox (veja a Figura 2).</span><span class="sxs-lookup"><span data-stu-id="6db70-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>


<span data-ttu-id="6db70-125">[![O extensor de controle ColorPicker](using-the-colorpicker-control-extender-cs/_static/image2.jpg)](using-the-colorpicker-control-extender-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="6db70-125">[![The ColorPicker Control Extender](using-the-colorpicker-control-extender-cs/_static/image2.jpg)](using-the-colorpicker-control-extender-cs/_static/image3.png)</span></span>

<span data-ttu-id="6db70-126">**Figura 02**: O extensor de controle ColorPicker ([clique para exibir a imagem em tamanho normal](using-the-colorpicker-control-extender-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="6db70-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image4.png))</span></span>


<span data-ttu-id="6db70-127">Você precisa concluir duas etapas para usar o extensor do controle ColorPicker com o formulário na listagem 1:</span><span class="sxs-lookup"><span data-stu-id="6db70-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="6db70-128">Adicione um controle ScriptManager à página</span><span class="sxs-lookup"><span data-stu-id="6db70-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="6db70-129">Adicione o extensor do controle ColorPicker à página</span><span class="sxs-lookup"><span data-stu-id="6db70-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="6db70-130">Antes de usar o ColorPicker, você deve adicionar um ScriptManager à página.</span><span class="sxs-lookup"><span data-stu-id="6db70-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="6db70-131">Um bom lugar para adicionar o ScriptManager é logo abaixo do lado do servidor abrindo &lt;formulário&gt; marca.</span><span class="sxs-lookup"><span data-stu-id="6db70-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="6db70-132">Você pode arrastar o ScriptManager para a página da caixa de ferramentas (o ScriptManager está localizado na guia Extensões AJAX).</span><span class="sxs-lookup"><span data-stu-id="6db70-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="6db70-133">Como alternativa, você pode digitar a seguinte marca na exibição da fonte abaixo da marca de formulário do lado do servidor de abertura:</span><span class="sxs-lookup"><span data-stu-id="6db70-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="6db70-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span><span class="sxs-lookup"><span data-stu-id="6db70-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="6db70-135">A maneira mais fácil para adicionar o extensor do controle ColorPicker para a página está no modo de exibição de Design.</span><span class="sxs-lookup"><span data-stu-id="6db70-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="6db70-136">Se você passar o mouse sobre a caixa de texto txtCardColor, uma opção de tarefa inteligente aparece o permite que você adicione um extensor (veja a Figura 3).</span><span class="sxs-lookup"><span data-stu-id="6db70-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="6db70-137">Se você escolher essa opção, o Assistente de extensor aparece (veja a Figura 4).</span><span class="sxs-lookup"><span data-stu-id="6db70-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>


<span data-ttu-id="6db70-138">[![Adicionando um extensor](using-the-colorpicker-control-extender-cs/_static/image3.jpg)](using-the-colorpicker-control-extender-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="6db70-138">[![Adding an extender](using-the-colorpicker-control-extender-cs/_static/image3.jpg)](using-the-colorpicker-control-extender-cs/_static/image5.png)</span></span>

<span data-ttu-id="6db70-139">**Figura 03**: Adicionando um extensor ([clique para exibir a imagem em tamanho normal](using-the-colorpicker-control-extender-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="6db70-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image6.png))</span></span>


<span data-ttu-id="6db70-140">[![Selecionando um extensor de controle com o Assistente de extensor](using-the-colorpicker-control-extender-cs/_static/image4.jpg)](using-the-colorpicker-control-extender-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="6db70-140">[![Selecting a control extender with the Extender Wizard](using-the-colorpicker-control-extender-cs/_static/image4.jpg)](using-the-colorpicker-control-extender-cs/_static/image7.png)</span></span>

<span data-ttu-id="6db70-141">**Figura 04**: Selecionando um extensor de controle com o Assistente de extensor ([clique para exibir a imagem em tamanho normal](using-the-colorpicker-control-extender-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="6db70-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image8.png))</span></span>


<span data-ttu-id="6db70-142">Você pode escolher o extensor ColorPicker para estender o txtCardColor caixa de texto com o extensor ColorPicker.</span><span class="sxs-lookup"><span data-stu-id="6db70-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="6db70-143">Clique em Okey para fechar a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6db70-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="6db70-144">Depois de fazer essas alterações, o código-fonte para a página semelhante à listagem 2.</span><span class="sxs-lookup"><span data-stu-id="6db70-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

<span data-ttu-id="6db70-145">Listagem 2 - CreateCard.aspx (com ColorPicker)</span><span class="sxs-lookup"><span data-stu-id="6db70-145">Listing 2 - CreateCard.aspx (with ColorPicker)</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample2.aspx)]

<span data-ttu-id="6db70-146">Observe que agora a página contém um controle ColorPickerExtender que aparece diretamente abaixo do controle TextBox txtCardColor.</span><span class="sxs-lookup"><span data-stu-id="6db70-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="6db70-147">O controle ColorPickerExtender estende o controle txtCardColor para que ele exiba uma caixa de diálogo do seletor de cor.</span><span class="sxs-lookup"><span data-stu-id="6db70-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="6db70-148">Usando um botão para iniciar a caixa de diálogo do seletor de cor</span><span class="sxs-lookup"><span data-stu-id="6db70-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="6db70-149">O extensor ColorPicker suporta as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="6db70-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="6db70-150">PopupButtonId - a ID de um botão na página que faz com que a caixa de diálogo do seletor de cor aparecer.</span><span class="sxs-lookup"><span data-stu-id="6db70-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="6db70-151">PopupPosition - a posição, em relação ao controle de destino da caixa de diálogo de seletor de cor.</span><span class="sxs-lookup"><span data-stu-id="6db70-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="6db70-152">Valores possíveis são absoluto, Center, BottomLeft, BottomRight, TopLeft, superior direito, à direita e esquerda (o padrão é BottomLeft).</span><span class="sxs-lookup"><span data-stu-id="6db70-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="6db70-153">SampleControlId - a ID de um controle que exibe a cor selecionada.</span><span class="sxs-lookup"><span data-stu-id="6db70-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="6db70-154">SelectedColor – a cor inicial selecionada pelo ColorPicker.</span><span class="sxs-lookup"><span data-stu-id="6db70-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="6db70-155">Você pode usar essas propriedades para personalizar como a caixa de diálogo do seletor de cor é exibida e como a cor selecionada é exibida.</span><span class="sxs-lookup"><span data-stu-id="6db70-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="6db70-156">A página na listagem 3 ilustra como você pode usar várias dessas propriedades.</span><span class="sxs-lookup"><span data-stu-id="6db70-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

<span data-ttu-id="6db70-157">**Listagem 3 - CreateCardButton.aspx**</span><span class="sxs-lookup"><span data-stu-id="6db70-157">**Listing 3 - CreateCardButton.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample3.aspx)]

<span data-ttu-id="6db70-158">A página na listagem 3 inclui selecionar cor botão (consulte a Figura 5).</span><span class="sxs-lookup"><span data-stu-id="6db70-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="6db70-159">Quando você clica nesse botão, a caixa de diálogo do seletor de cor é exibido acima da caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6db70-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="6db70-160">Se você selecionar uma cor na caixa de diálogo cor selecionada é exibida como a cor do plano de fundo do lblSample controle de rótulo.</span><span class="sxs-lookup"><span data-stu-id="6db70-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="6db70-161">A propriedade ColorPicker PopupButtonID é usada para associar o botão Selecionar cor o extensor ColorPicker.</span><span class="sxs-lookup"><span data-stu-id="6db70-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="6db70-162">Ao fornecer um valor da propriedade PopupButtonID, a caixa de diálogo do seletor de cor será mais exibida quando o controle de destino tem o foco.</span><span class="sxs-lookup"><span data-stu-id="6db70-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="6db70-163">Você deve clicar no botão para exibir a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6db70-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="6db70-164">A propriedade SampleControlID é usada para associar um controle que exibe a cor selecionada com o ColorPicker.</span><span class="sxs-lookup"><span data-stu-id="6db70-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="6db70-165">ColorPicker altera a cor de plano de fundo desse controle para a cor atualmente selecionada.</span><span class="sxs-lookup"><span data-stu-id="6db70-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>


<span data-ttu-id="6db70-166">[![Exibir a caixa de diálogo do seletor de cor com um botão](using-the-colorpicker-control-extender-cs/_static/image5.jpg)](using-the-colorpicker-control-extender-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="6db70-166">[![Displaying the color picker dialog with a button](using-the-colorpicker-control-extender-cs/_static/image5.jpg)](using-the-colorpicker-control-extender-cs/_static/image9.png)</span></span>

<span data-ttu-id="6db70-167">**Figura 05**: Exibir a caixa de diálogo do seletor de cor com um botão ([clique para exibir a imagem em tamanho normal](using-the-colorpicker-control-extender-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="6db70-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-cs/_static/image10.png))</span></span>


## <a name="summary"></a><span data-ttu-id="6db70-168">Resumo</span><span class="sxs-lookup"><span data-stu-id="6db70-168">Summary</span></span>

<span data-ttu-id="6db70-169">Neste tutorial, você aprendeu como usar o extensor do controle ColorPicker para exibir uma caixa de diálogo do seletor de cor do pop-up.</span><span class="sxs-lookup"><span data-stu-id="6db70-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="6db70-170">Primeiro, examinamos como você pode exibir a caixa de diálogo quando o foco é movido para um controle de caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6db70-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="6db70-171">Em seguida, você aprendeu a criar um botão que exibe a caixa de diálogo do seletor de cor quando o botão é clicado.</span><span class="sxs-lookup"><span data-stu-id="6db70-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6db70-172">Avançar</span><span class="sxs-lookup"><span data-stu-id="6db70-172">Next</span></span>](using-the-colorpicker-control-extender-vb.md)
