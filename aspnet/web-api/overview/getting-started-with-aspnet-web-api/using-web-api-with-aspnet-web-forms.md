---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: Usando a API da Web com Web Forms do ASP.NET | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 04/03/2012
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: a14bf0abd8c5d603cf3859891f855415cf3df9f3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57055683"
---
<a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="43eb9-102">Uso da API Web com Web Forms do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="43eb9-102">Using Web API with ASP.NET Web Forms</span></span>
====================
<span data-ttu-id="43eb9-103">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="43eb9-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="43eb9-104">Embora a API Web ASP.NET é empacotada com o ASP.NET MVC, é fácil adicionar a API da Web a um aplicativo Web Forms do ASP.NET tradicional.</span><span class="sxs-lookup"><span data-stu-id="43eb9-104">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span> <span data-ttu-id="43eb9-105">Este tutorial orienta você pelas etapas.</span><span class="sxs-lookup"><span data-stu-id="43eb9-105">This tutorial walks you through the steps.</span></span>

## <a name="overview"></a><span data-ttu-id="43eb9-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="43eb9-106">Overview</span></span>

<span data-ttu-id="43eb9-107">Para usar a API da Web em um aplicativo Web Forms, há duas etapas principais:</span><span class="sxs-lookup"><span data-stu-id="43eb9-107">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="43eb9-108">Adicionar um controlador de API da Web que deriva de **ApiController** classe.</span><span class="sxs-lookup"><span data-stu-id="43eb9-108">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="43eb9-109">Adicionar uma tabela de rotas para o **Application\_iniciar** método.</span><span class="sxs-lookup"><span data-stu-id="43eb9-109">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="43eb9-110">Criar um projeto de formulários da Web</span><span class="sxs-lookup"><span data-stu-id="43eb9-110">Create a Web Forms Project</span></span>

<span data-ttu-id="43eb9-111">Inicie o Visual Studio e selecione **Novo projeto** na página **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="43eb9-111">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="43eb9-112">Ou, no menu **Arquivo**, selecione **Novo** e, em seguida, **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="43eb9-112">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="43eb9-113">No painel **Modelos**, selecione **Modelos Instalados** e expanda o nó **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="43eb9-113">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="43eb9-114">Em **Visual C#**, selecione **Web**.</span><span class="sxs-lookup"><span data-stu-id="43eb9-114">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="43eb9-115">Na lista de modelos de projeto, selecione **aplicativo do ASP.NET Web Forms**.</span><span class="sxs-lookup"><span data-stu-id="43eb9-115">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="43eb9-116">Insira um nome para o projeto e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="43eb9-116">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="43eb9-117">Criar o modelo e o controlador</span><span class="sxs-lookup"><span data-stu-id="43eb9-117">Create the Model and Controller</span></span>

<span data-ttu-id="43eb9-118">Este tutorial usa as mesmas classes de modelo e controlador como o [guia de Introdução](tutorial-your-first-web-api.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="43eb9-118">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="43eb9-119">Primeiro, adicione uma classe de modelo.</span><span class="sxs-lookup"><span data-stu-id="43eb9-119">First, add a model class.</span></span> <span data-ttu-id="43eb9-120">Na **Gerenciador de soluções**, clique com botão direito no projeto e selecione **Adicionar classe**.</span><span class="sxs-lookup"><span data-stu-id="43eb9-120">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="43eb9-121">Nomeie a classe Product e, em seguida, adicione a seguinte implementação:</span><span class="sxs-lookup"><span data-stu-id="43eb9-121">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="43eb9-122">Em seguida, adicione um controlador de API da Web ao projeto., uma *controlador* é o objeto que manipula as solicitações HTTP para a API da Web.</span><span class="sxs-lookup"><span data-stu-id="43eb9-122">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="43eb9-123">No **Gerenciador de Soluções**, clique com o botão direito do mouse no nome do projeto.</span><span class="sxs-lookup"><span data-stu-id="43eb9-123">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="43eb9-124">Selecione **Adicionar Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="43eb9-124">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="43eb9-125">Sob **modelos instalados**, expanda **Visual c#** e selecione **Web**.</span><span class="sxs-lookup"><span data-stu-id="43eb9-125">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="43eb9-126">Em seguida, na lista de modelos, selecione **Web API Controller Class**.</span><span class="sxs-lookup"><span data-stu-id="43eb9-126">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="43eb9-127">Nomeie o controlador "ProductsController" e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="43eb9-127">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="43eb9-128">O **Adicionar Novo Item** assistente criará um arquivo chamado ProductsController.cs.</span><span class="sxs-lookup"><span data-stu-id="43eb9-128">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="43eb9-129">Exclua os métodos que o assistente incluído e adicione os seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="43eb9-129">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="43eb9-130">Para obter mais informações sobre o código neste controlador, consulte o [guia de Introdução](tutorial-your-first-web-api.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="43eb9-130">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="43eb9-131">Adicionar informações de roteamento</span><span class="sxs-lookup"><span data-stu-id="43eb9-131">Add Routing Information</span></span>

<span data-ttu-id="43eb9-132">Em seguida, vamos adicionar uma rota URI assim que URIs do formulário &quot;/API/produtos/&quot; são roteadas para o controlador.</span><span class="sxs-lookup"><span data-stu-id="43eb9-132">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="43eb9-133">Na **Gerenciador de soluções**, clique duas vezes em global. asax para abrir o arquivo code-behind Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="43eb9-133">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="43eb9-134">Adicione o seguinte **usando** instrução.</span><span class="sxs-lookup"><span data-stu-id="43eb9-134">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="43eb9-135">Em seguida, adicione o seguinte código para o **Application\_iniciar** método:</span><span class="sxs-lookup"><span data-stu-id="43eb9-135">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="43eb9-136">Para obter mais informações sobre tabelas de roteamento, consulte [roteamento na API Web ASP.NET](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="43eb9-136">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="43eb9-137">Adicionar o AJAX do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="43eb9-137">Add Client-Side AJAX</span></span>

<span data-ttu-id="43eb9-138">Isso é tudo o que você precisa criar uma API web que os clientes podem acessar.</span><span class="sxs-lookup"><span data-stu-id="43eb9-138">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="43eb9-139">Agora vamos adicionar uma página HTML que usa o jQuery para chamar a API.</span><span class="sxs-lookup"><span data-stu-id="43eb9-139">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="43eb9-140">Verifique se a página mestra (por exemplo, *Master*) inclui um `ContentPlaceHolder` com `ID="HeadContent"`:</span><span class="sxs-lookup"><span data-stu-id="43eb9-140">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="43eb9-141">Abra o arquivo default. aspx.</span><span class="sxs-lookup"><span data-stu-id="43eb9-141">Open the file Default.aspx.</span></span> <span data-ttu-id="43eb9-142">Substitua o texto clichê que está na seção de conteúdo principal, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="43eb9-142">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="43eb9-143">Em seguida, adicione uma referência para o arquivo de origem do jQuery no `HeaderContent` seção:</span><span class="sxs-lookup"><span data-stu-id="43eb9-143">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="43eb9-144">Observação: Você pode adicionar facilmente a referência de script arrastando e soltando o arquivo a partir **Gerenciador de soluções** na janela do editor de código.</span><span class="sxs-lookup"><span data-stu-id="43eb9-144">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="43eb9-145">Abaixo da marca de script do jQuery, adicione o seguinte bloco de script:</span><span class="sxs-lookup"><span data-stu-id="43eb9-145">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="43eb9-146">Quando o documento for carregado, esse script faz uma solicitação AJAX ao &quot;api/produtos&quot;.</span><span class="sxs-lookup"><span data-stu-id="43eb9-146">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="43eb9-147">A solicitação retorna uma lista de produtos no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="43eb9-147">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="43eb9-148">O script adiciona as informações do produto na tabela de HTML.</span><span class="sxs-lookup"><span data-stu-id="43eb9-148">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="43eb9-149">Quando você executa o aplicativo, ele deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="43eb9-149">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
