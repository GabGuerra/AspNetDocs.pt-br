---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: Criando testes de unidade para aplicativos ASP.NET MVC (c#) | Microsoft Docs
author: StephenWalther
description: Saiba como criar testes de unidade para ações do controlador. Neste tutorial, Stephen Walther demonstra como testar se uma ação do controlador retorna um parti...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 1193d7dc6fc29dfdac5637c9391a82f9f3566073
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59407725"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a><span data-ttu-id="52bbb-104">Criação de testes de unidade para aplicativos do ASP.NET MVC (C#)</span><span class="sxs-lookup"><span data-stu-id="52bbb-104">Creating Unit Tests for ASP.NET MVC Applications (C#)</span></span>

<span data-ttu-id="52bbb-105">por [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="52bbb-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="52bbb-106">Baixar PDF</span><span class="sxs-lookup"><span data-stu-id="52bbb-106">Download PDF</span></span>](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> <span data-ttu-id="52bbb-107">Saiba como criar testes de unidade para ações do controlador.</span><span class="sxs-lookup"><span data-stu-id="52bbb-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="52bbb-108">Neste tutorial, Stephen Walther demonstra como testar se uma ação do controlador retorna uma exibição específica, retorna um conjunto de dados específico ou retorna um tipo diferente de resultado da ação.</span><span class="sxs-lookup"><span data-stu-id="52bbb-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>


<span data-ttu-id="52bbb-109">O objetivo deste tutorial é demonstrar como você pode escrever o testes de unidade para os controladores no ASP.NET MVC aplicativos.</span><span class="sxs-lookup"><span data-stu-id="52bbb-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="52bbb-110">Vamos discutir como criar três tipos diferentes de testes de unidade.</span><span class="sxs-lookup"><span data-stu-id="52bbb-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="52bbb-111">Você aprenderá como testar a retornado por uma ação do controlador de exibição, como os dados de exibição retornados por uma ação do controlador de teste e como testar se uma ação de controlador redireciona você para uma segunda ação de controlador.</span><span class="sxs-lookup"><span data-stu-id="52bbb-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="52bbb-112">Criando o controlador de teste</span><span class="sxs-lookup"><span data-stu-id="52bbb-112">Creating the Controller under Test</span></span>

<span data-ttu-id="52bbb-113">Vamos começar criando o controlador que temos a intenção de teste.</span><span class="sxs-lookup"><span data-stu-id="52bbb-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="52bbb-114">O controlador, chamado de `ProductController`, está contida na listagem 1.</span><span class="sxs-lookup"><span data-stu-id="52bbb-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

**<span data-ttu-id="52bbb-115">Listagem 1 –</span><span class="sxs-lookup"><span data-stu-id="52bbb-115">Listing 1 –</span></span> `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

<span data-ttu-id="52bbb-116">O `ProductController` contém dois métodos de ação chamados `Index()` e `Details()`.</span><span class="sxs-lookup"><span data-stu-id="52bbb-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="52bbb-117">Ambos os métodos de ação retornam uma exibição.</span><span class="sxs-lookup"><span data-stu-id="52bbb-117">Both action methods return a view.</span></span> <span data-ttu-id="52bbb-118">Observe que o `Details()` ação aceita um parâmetro chamado ID.</span><span class="sxs-lookup"><span data-stu-id="52bbb-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="52bbb-119">Testando a exibição retornada por um controlador</span><span class="sxs-lookup"><span data-stu-id="52bbb-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="52bbb-120">Imagine que queremos testar ou não o `ProductController` retorna a exibição à direita.</span><span class="sxs-lookup"><span data-stu-id="52bbb-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="52bbb-121">Certifique-se de que, quando o `ProductController.Details()` ação é invocada, a exibição de detalhes é retornada.</span><span class="sxs-lookup"><span data-stu-id="52bbb-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="52bbb-122">A classe de teste na listagem 2 contém um teste de unidade para testar a exibição retornada pelo `ProductController.Details()` ação.</span><span class="sxs-lookup"><span data-stu-id="52bbb-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

**<span data-ttu-id="52bbb-123">Listagem 2 –</span><span class="sxs-lookup"><span data-stu-id="52bbb-123">Listing 2 –</span></span> `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

<span data-ttu-id="52bbb-124">A classe na listagem 2 inclui um método de teste chamado `TestDetailsView()`.</span><span class="sxs-lookup"><span data-stu-id="52bbb-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="52bbb-125">Este método contém três linhas de código.</span><span class="sxs-lookup"><span data-stu-id="52bbb-125">This method contains three lines of code.</span></span> <span data-ttu-id="52bbb-126">A primeira linha de código cria uma nova instância do `ProductController` classe.</span><span class="sxs-lookup"><span data-stu-id="52bbb-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="52bbb-127">A segunda linha de código invoca o controlador `Details()` método de ação.</span><span class="sxs-lookup"><span data-stu-id="52bbb-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="52bbb-128">Por fim, a última linha de verificações de código ou não o modo de exibição é retornado pelo `Details()` ação é a exibição de detalhes.</span><span class="sxs-lookup"><span data-stu-id="52bbb-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="52bbb-129">O `ViewResult.ViewName` propriedade representa o nome da exibição retornada por um controlador.</span><span class="sxs-lookup"><span data-stu-id="52bbb-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="52bbb-130">Uma importante advertência sobre como testar essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="52bbb-130">One big warning about testing this property.</span></span> <span data-ttu-id="52bbb-131">Há duas maneiras que um controlador pode retornar uma exibição.</span><span class="sxs-lookup"><span data-stu-id="52bbb-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="52bbb-132">Um controlador explicitamente pode retornar uma exibição como esta:</span><span class="sxs-lookup"><span data-stu-id="52bbb-132">A controller can explicitly return a view like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

<span data-ttu-id="52bbb-133">Como alternativa, o nome do modo de exibição pode ser inferido do nome da ação de controlador, como este:</span><span class="sxs-lookup"><span data-stu-id="52bbb-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

<span data-ttu-id="52bbb-134">Esta ação do controlador também retorna uma exibição nomeada `Details`.</span><span class="sxs-lookup"><span data-stu-id="52bbb-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="52bbb-135">No entanto, o nome da exibição é inferido do nome da ação.</span><span class="sxs-lookup"><span data-stu-id="52bbb-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="52bbb-136">Se você quiser testar o nome da exibição, explicitamente deve retornar o nome de exibição da ação de controlador.</span><span class="sxs-lookup"><span data-stu-id="52bbb-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="52bbb-137">Você pode executar o teste de unidade na listagem 2 digitando a combinação de teclado **Ctrl-R, A** ou clicando o **executar todos os testes na solução** botão (consulte a Figura 1).</span><span class="sxs-lookup"><span data-stu-id="52bbb-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="52bbb-138">Se o teste for bem-sucedido, você verá a janela Test Results na Figura 2.</span><span class="sxs-lookup"><span data-stu-id="52bbb-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>


[![R<span data-ttu-id="52bbb-139">Cancelar todos os testes na solução]</span><span class="sxs-lookup"><span data-stu-id="52bbb-139">un All Tests in Solution]</span></span>(creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)

<span data-ttu-id="52bbb-140">**Figura 01**: Executar todos os testes na solução ([clique para exibir a imagem em tamanho normal](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="52bbb-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span></span>


[![S<span data-ttu-id="52bbb-141">uccess!]</span><span class="sxs-lookup"><span data-stu-id="52bbb-141">uccess!]</span></span>(creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)

<span data-ttu-id="52bbb-142">**Figura 02**: Sucesso!</span><span class="sxs-lookup"><span data-stu-id="52bbb-142">**Figure 02**: Success!</span></span> <span data-ttu-id="52bbb-143">([Clique para exibir a imagem em tamanho normal](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="52bbb-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span></span>


## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="52bbb-144">Teste os dados de exibição retornada por um controlador</span><span class="sxs-lookup"><span data-stu-id="52bbb-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="52bbb-145">Um controlador MVC passa dados para um modo de exibição usando algo chamado *`View Data`*.</span><span class="sxs-lookup"><span data-stu-id="52bbb-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="52bbb-146">Por exemplo, imagine que você deseja exibir os detalhes de um produto específico, quando você invoca o `ProductController Details()` ação.</span><span class="sxs-lookup"><span data-stu-id="52bbb-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="52bbb-147">Nesse caso, você pode criar uma instância de um `Product` classe (definido no modelo) e passar a instância para o `Details` exibição aproveitando `View Data`.</span><span class="sxs-lookup"><span data-stu-id="52bbb-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="52bbb-148">Modificado `ProductController` na listagem 3 inclui atualizada `Details()` ação que retorna um produto.</span><span class="sxs-lookup"><span data-stu-id="52bbb-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

**<span data-ttu-id="52bbb-149">Listagem 3 –</span><span class="sxs-lookup"><span data-stu-id="52bbb-149">Listing 3 –</span></span> `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

<span data-ttu-id="52bbb-150">Primeiro, o `Details()` ação cria uma nova instância do `Product` classe que representa um computador laptop.</span><span class="sxs-lookup"><span data-stu-id="52bbb-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="52bbb-151">Em seguida, a instância das `Product` classe é passado como o segundo parâmetro para o `View()` método.</span><span class="sxs-lookup"><span data-stu-id="52bbb-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="52bbb-152">Você pode escrever testes de unidade testar se os dados esperados estão contidos na exibição dados.</span><span class="sxs-lookup"><span data-stu-id="52bbb-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="52bbb-153">O teste de unidade na listagem 4 testes se um produto que representa um computador laptop é retornado ao chamar o `ProductController Details()` método de ação.</span><span class="sxs-lookup"><span data-stu-id="52bbb-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

**<span data-ttu-id="52bbb-154">Listagem 4 –</span><span class="sxs-lookup"><span data-stu-id="52bbb-154">Listing 4 –</span></span> `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

<span data-ttu-id="52bbb-155">Na listagem 4, o `TestDetailsView()` método testa os dados de exibição retornado ao invocar o `Details()` método.</span><span class="sxs-lookup"><span data-stu-id="52bbb-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="52bbb-156">O `ViewData` é exposta como uma propriedade em de `ViewResult` retornado ao invocar o `Details()` método.</span><span class="sxs-lookup"><span data-stu-id="52bbb-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="52bbb-157">O `ViewData.Model` propriedade contém o produto passado para o modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="52bbb-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="52bbb-158">O teste simplesmente verifica que o produto contido nos dados do modo de exibição tem o nome do Laptop.</span><span class="sxs-lookup"><span data-stu-id="52bbb-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="52bbb-159">Testar o resultado de ação retornada por um controlador</span><span class="sxs-lookup"><span data-stu-id="52bbb-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="52bbb-160">Uma ação do controlador mais complexa pode retornar tipos diferentes de resultados de ação, dependendo dos valores dos parâmetros passados para a ação do controlador.</span><span class="sxs-lookup"><span data-stu-id="52bbb-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="52bbb-161">Uma ação do controlador pode retornar uma variedade de tipos de resultados de ação, incluindo uma `ViewResult`, `RedirectToRouteResult`, ou `JsonResult`.</span><span class="sxs-lookup"><span data-stu-id="52bbb-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="52bbb-162">Por exemplo, a modificação `Details()` ação na listagem 5 retorna o `Details` exibir ao passar um Id de produto válida para a ação.</span><span class="sxs-lookup"><span data-stu-id="52bbb-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="52bbb-163">Se você passar um produto inválida Id – uma Id com um valor menor que 1-- em seguida, você será redirecionado para o `Index()` ação.</span><span class="sxs-lookup"><span data-stu-id="52bbb-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

**<span data-ttu-id="52bbb-164">Listagem 5 –</span><span class="sxs-lookup"><span data-stu-id="52bbb-164">Listing 5 –</span></span> `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

<span data-ttu-id="52bbb-165">Você pode testar o comportamento do `Details()` ação com o teste de unidade na listagem 6.</span><span class="sxs-lookup"><span data-stu-id="52bbb-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="52bbb-166">O teste de unidade na listagem 6 verifica que você será redirecionado para o `Index` exibir quando uma Id com o valor -1 for passada para o `Details()` método.</span><span class="sxs-lookup"><span data-stu-id="52bbb-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

**<span data-ttu-id="52bbb-167">Listagem 6 –</span><span class="sxs-lookup"><span data-stu-id="52bbb-167">Listing 6 –</span></span> `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

<span data-ttu-id="52bbb-168">Quando você chama o `RedirectToAction()` método em uma ação de controlador, a ação do controlador retorna um `RedirectToRouteResult`.</span><span class="sxs-lookup"><span data-stu-id="52bbb-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="52bbb-169">O teste verifica se o `RedirectToRouteResult` redirecionará o usuário a uma ação de controlador chamada `Index`.</span><span class="sxs-lookup"><span data-stu-id="52bbb-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="52bbb-170">Resumo</span><span class="sxs-lookup"><span data-stu-id="52bbb-170">Summary</span></span>

<span data-ttu-id="52bbb-171">Neste tutorial, você aprendeu como criar testes de unidade para ações do controlador MVC.</span><span class="sxs-lookup"><span data-stu-id="52bbb-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="52bbb-172">Primeiro, você aprendeu como verificar se a exibição à direita é retornada por uma ação do controlador.</span><span class="sxs-lookup"><span data-stu-id="52bbb-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="52bbb-173">Você aprendeu a usar o `ViewResult.ViewName` propriedade para verificar o nome de uma exibição.</span><span class="sxs-lookup"><span data-stu-id="52bbb-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="52bbb-174">Em seguida, examinamos como você pode testar o conteúdo de `View Data`.</span><span class="sxs-lookup"><span data-stu-id="52bbb-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="52bbb-175">Você aprendeu como verificar se o produto certo foi retornado em `View Data` depois de chamar uma ação do controlador.</span><span class="sxs-lookup"><span data-stu-id="52bbb-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="52bbb-176">Por fim, discutimos como você pode testar se os tipos diferentes de resultados de ação são retornados de uma ação do controlador.</span><span class="sxs-lookup"><span data-stu-id="52bbb-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="52bbb-177">Você aprendeu como testar se um controlador retorna um `ViewResult` ou um `RedirectToRouteResult`.</span><span class="sxs-lookup"><span data-stu-id="52bbb-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="52bbb-178">Avançar</span><span class="sxs-lookup"><span data-stu-id="52bbb-178">Next</span></span>](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
