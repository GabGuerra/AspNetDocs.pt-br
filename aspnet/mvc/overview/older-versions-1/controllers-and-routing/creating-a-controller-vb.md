---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
title: Criando um controlador (VB) | Microsoft Docs
author: StephenWalther
description: Neste tutorial, Stephen Walther demonstra como você pode adicionar um controlador a um aplicativo ASP.NET MVC.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 204b7e86-f560-4611-8adb-785b33e777b9
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c14ceff17d15b1a8460bad41429b82cb9504a24
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035153"
---
<a name="creating-a-controller-vb"></a><span data-ttu-id="39d00-103">Criar um controlador (VB)</span><span class="sxs-lookup"><span data-stu-id="39d00-103">Creating a Controller (VB)</span></span>
====================
<span data-ttu-id="39d00-104">por [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="39d00-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="39d00-105">Neste tutorial, Stephen Walther demonstra como você pode adicionar um controlador a um aplicativo ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="39d00-105">In this tutorial, Stephen Walther demonstrates how you can add a controller to an ASP.NET MVC application.</span></span>


<span data-ttu-id="39d00-106">O objetivo deste tutorial é explicar como você pode criar novas ASP.NET MVC controladores.</span><span class="sxs-lookup"><span data-stu-id="39d00-106">The goal of this tutorial is to explain how you can create new ASP.NET MVC controllers.</span></span> <span data-ttu-id="39d00-107">Você aprenderá a criar controladores usando a opção de menu do Visual Studio Adicionar controlador e criando um arquivo de classe manualmente.</span><span class="sxs-lookup"><span data-stu-id="39d00-107">You learn how to create controllers both by using the Visual Studio Add Controller menu option and by creating a class file by hand.</span></span>

### <a name="using-the-add-controller-menu-option"></a><span data-ttu-id="39d00-108">Usando o adicionar a opção de Menu do controlador</span><span class="sxs-lookup"><span data-stu-id="39d00-108">Using the Add Controller Menu Option</span></span>

<span data-ttu-id="39d00-109">A maneira mais fácil de criar um novo controlador é com o botão direito na pasta controladores na janela do Gerenciador de soluções do Visual Studio e selecione o **Add, controlador** opção de menu (veja a Figura 1).</span><span class="sxs-lookup"><span data-stu-id="39d00-109">The easiest way to create a new controller is to right-click the Controllers folder in the Visual Studio Solution Explorer window and select the **Add, Controller** menu option (see Figure 1).</span></span> <span data-ttu-id="39d00-110">Selecionar essa opção de menu abre a **Adicionar controlador** caixa de diálogo (consulte a Figura 2).</span><span class="sxs-lookup"><span data-stu-id="39d00-110">Selecting this menu option opens the **Add Controller** dialog (see Figure 2).</span></span>


<span data-ttu-id="39d00-111">[![A caixa de diálogo Novo projeto](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="39d00-111">[![The New Project dialog box](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)</span></span>

<span data-ttu-id="39d00-112">**Figura 01**: Adicionando um novo controlador ([clique para exibir a imagem em tamanho normal](creating-a-controller-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="39d00-112">**Figure 01**: Adding a new controller([Click to view full-size image](creating-a-controller-vb/_static/image2.png))</span></span>


<span data-ttu-id="39d00-113">[![A caixa de diálogo Novo projeto](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="39d00-113">[![The New Project dialog box](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)</span></span>

<span data-ttu-id="39d00-114">**Figura 02**: A caixa de diálogo Adicionar controlador ([clique para exibir a imagem em tamanho normal](creating-a-controller-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="39d00-114">**Figure 02**: The Add Controller dialog ([Click to view full-size image](creating-a-controller-vb/_static/image4.png))</span></span>


<span data-ttu-id="39d00-115">Observe que a primeira parte do nome do controlador está realçada na **Adicionar controlador** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="39d00-115">Notice that the first part of the controller name is highlighted in the **Add Controller** dialog.</span></span> <span data-ttu-id="39d00-116">Cada nome de controlador deve terminar com o sufixo *controlador*.</span><span class="sxs-lookup"><span data-stu-id="39d00-116">Every controller name must end with the suffix *Controller*.</span></span> <span data-ttu-id="39d00-117">Por exemplo, você pode criar um controlador chamado *ProductController* , mas não um controlador chamado *produto*.</span><span class="sxs-lookup"><span data-stu-id="39d00-117">For example, you can create a controller named *ProductController* but not a controller named *Product*.</span></span>


<span data-ttu-id="39d00-118">Se você criar um controlador que está faltando a *controlador* sufixo e em seguida, você não poderá invocar o controlador.</span><span class="sxs-lookup"><span data-stu-id="39d00-118">If you create a controller that is missing the *Controller* suffix then you won't be able to invoke the controller.</span></span> <span data-ttu-id="39d00-119">Não fizer isso, eu já desperdiçado incontáveis horas da minha vida depois de cometer esse erro.</span><span class="sxs-lookup"><span data-stu-id="39d00-119">Don't do this -- I've wasted countless hours of my life after making this mistake.</span></span>


<span data-ttu-id="39d00-120">**Listagem 1 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="39d00-120">**Listing 1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample1.vb)]

<span data-ttu-id="39d00-121">Você deve sempre criar controladores na pasta controladores.</span><span class="sxs-lookup"><span data-stu-id="39d00-121">You should always create controllers in the Controllers folder.</span></span> <span data-ttu-id="39d00-122">Caso contrário, você vai ser violar as convenções do ASP.NET MVC e outros desenvolvedores terá mais dificuldade Noções básicas sobre seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="39d00-122">Otherwise, you'll be violating the conventions of ASP.NET MVC and other developers will have a more difficult time understanding your application.</span></span>

### <a name="scaffolding-action-methods"></a><span data-ttu-id="39d00-123">Métodos de ação de scaffolding</span><span class="sxs-lookup"><span data-stu-id="39d00-123">Scaffolding Action Methods</span></span>

<span data-ttu-id="39d00-124">Quando você cria um controlador, você tem a opção para gerar os métodos de ação de criar, atualizar e detalhes automaticamente (veja a Figura 3).</span><span class="sxs-lookup"><span data-stu-id="39d00-124">When you create a controller, you have the option to generate Create, Update, and Details action methods automatically (see Figure 3).</span></span> <span data-ttu-id="39d00-125">Se você selecionar essa opção, em seguida, a classe do controlador na listagem 2 é gerada.</span><span class="sxs-lookup"><span data-stu-id="39d00-125">If you select this option then the controller class in Listing 2 is generated.</span></span>


<span data-ttu-id="39d00-126">[![Criação automática de métodos de ação](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="39d00-126">[![Creating action methods automatically](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)</span></span>

<span data-ttu-id="39d00-127">**Figura 03**: Criação automática de métodos de ação ([clique para exibir a imagem em tamanho normal](creating-a-controller-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="39d00-127">**Figure 03**: Creating action methods automatically ([Click to view full-size image](creating-a-controller-vb/_static/image6.png))</span></span>


<span data-ttu-id="39d00-128">**Listagem 2 - Controllers\CustomerController.vb**</span><span class="sxs-lookup"><span data-stu-id="39d00-128">**Listing 2 - Controllers\CustomerController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample2.vb)]

<span data-ttu-id="39d00-129">Esses métodos gerados são métodos stub.</span><span class="sxs-lookup"><span data-stu-id="39d00-129">These generated methods are stub methods.</span></span> <span data-ttu-id="39d00-130">Você deve adicionar a lógica real para criar, atualizar e mostrando detalhes de um cliente.</span><span class="sxs-lookup"><span data-stu-id="39d00-130">You must add the actual logic for creating, updating, and showing details for a customer yourself.</span></span> <span data-ttu-id="39d00-131">Porém, os métodos stub fornecem um bom ponto de partida.</span><span class="sxs-lookup"><span data-stu-id="39d00-131">But, the stub methods provide you with a nice starting point.</span></span>

### <a name="creating-a-controller-class"></a><span data-ttu-id="39d00-132">Criando uma classe de controlador</span><span class="sxs-lookup"><span data-stu-id="39d00-132">Creating a Controller Class</span></span>

<span data-ttu-id="39d00-133">O controlador MVC do ASP.NET é apenas uma classe.</span><span class="sxs-lookup"><span data-stu-id="39d00-133">The ASP.NET MVC controller is just a class.</span></span> <span data-ttu-id="39d00-134">Se você preferir, você pode ignorar o scaffolding de controlador conveniente do Visual Studio e criar uma classe de controlador manualmente.</span><span class="sxs-lookup"><span data-stu-id="39d00-134">If you prefer, you can ignore the convenient Visual Studio controller scaffolding and create a controller class by hand.</span></span> <span data-ttu-id="39d00-135">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="39d00-135">Follow these steps:</span></span>

1. <span data-ttu-id="39d00-136">Clique com botão direito na pasta controladores e selecione a opção de menu **Add, o novo Item** e selecione o **classe** modelo (consulte a Figura 4).</span><span class="sxs-lookup"><span data-stu-id="39d00-136">Right-click the Controllers folder and select the menu option **Add, New Item** and select the **Class** template (see Figure 4).</span></span>
2. <span data-ttu-id="39d00-137">Nomeie a nova classe PersonController.vb e clique no **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="39d00-137">Name the new class PersonController.vb and click the **Add** button.</span></span>
3. <span data-ttu-id="39d00-138">Modifique o arquivo de classe resultante para que a classe herda da classe Controller base (consulte a listagem 3).</span><span class="sxs-lookup"><span data-stu-id="39d00-138">Modify the resulting class file so that the class inherits from the base System.Web.Mvc.Controller class (see Listing 3).</span></span>


<span data-ttu-id="39d00-139">[![Criando uma nova classe](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="39d00-139">[![Creating a new class](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)</span></span>

<span data-ttu-id="39d00-140">**Figura 04**: Criando uma nova classe ([clique para exibir a imagem em tamanho normal](creating-a-controller-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="39d00-140">**Figure 04**: Creating a new class([Click to view full-size image](creating-a-controller-vb/_static/image8.png))</span></span>


<span data-ttu-id="39d00-141">**Listagem 3 - Controllers\PersonController.vb**</span><span class="sxs-lookup"><span data-stu-id="39d00-141">**Listing 3 - Controllers\PersonController.vb**</span></span>

[!code-vb[Main](creating-a-controller-vb/samples/sample3.vb)]

<span data-ttu-id="39d00-142">O controlador na listagem 3 expõe uma ação chamada index () que retorna a cadeia de caracteres "Hello World!".</span><span class="sxs-lookup"><span data-stu-id="39d00-142">The controller in Listing 3 exposes one action named Index() that returns the string "Hello World!".</span></span> <span data-ttu-id="39d00-143">Você pode chamar essa ação de controlador, executando o aplicativo e solicitar uma URL semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="39d00-143">You can invoke this controller action by running your application and requesting a URL like the following:</span></span>

`http://localhost:40071/Person`

> [!NOTE]
> 
> <span data-ttu-id="39d00-144">O ASP.NET Development Server usa um número de porta aleatória (por exemplo, 40071).</span><span class="sxs-lookup"><span data-stu-id="39d00-144">The ASP.NET Development Server uses a random port number (for example, 40071).</span></span> <span data-ttu-id="39d00-145">Ao inserir uma URL para invocar um controlador, você precisará fornecer o número da porta à direita.</span><span class="sxs-lookup"><span data-stu-id="39d00-145">When entering a URL to invoke a controller, you'll need to supply the right port number.</span></span> <span data-ttu-id="39d00-146">Você pode passar o mouse sobre o ícone para o ASP.NET Development Server na área de notificação do Windows (canto inferior direito da tela) para determinar o número da porta.</span><span class="sxs-lookup"><span data-stu-id="39d00-146">You can determine the port number by hovering your mouse over the icon for the ASP.NET Development Server in the Windows Notification Area (bottom-right of your screen).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="39d00-147">[Anterior](adding-dynamic-content-to-a-cached-page-vb.md)
> [Próximo](creating-an-action-vb.md)</span><span class="sxs-lookup"><span data-stu-id="39d00-147">[Previous](adding-dynamic-content-to-a-cached-page-vb.md)
[Next](creating-an-action-vb.md)</span></span>
