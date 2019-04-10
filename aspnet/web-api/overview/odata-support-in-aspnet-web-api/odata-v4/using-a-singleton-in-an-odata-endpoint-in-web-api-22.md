---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: Criar um Singleton no OData v4 usando a API Web 2.2 | Microsoft Docs
author: rick-anderson
description: Este tópico mostra como definir um singleton em um ponto de extremidade OData na Web API 2.2.
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 935448a1f9770e1f11460c95997aa778c4208c9f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59403331"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a><span data-ttu-id="49f5a-103">Criar um Singleton no OData v4 usando a API Web 2.2</span><span class="sxs-lookup"><span data-stu-id="49f5a-103">Create a Singleton in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="49f5a-104">by Zoe Luo</span><span class="sxs-lookup"><span data-stu-id="49f5a-104">by Zoe Luo</span></span>

> <span data-ttu-id="49f5a-105">Tradicionalmente, uma entidade pode ser acessada somente se ele foi encapsulado dentro de um conjunto de entidades.</span><span class="sxs-lookup"><span data-stu-id="49f5a-105">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="49f5a-106">Mas o OData v4 fornece duas opções adicionais, Singleton e contenção, que oferece suporte da API Web 2.2.</span><span class="sxs-lookup"><span data-stu-id="49f5a-106">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>


<span data-ttu-id="49f5a-107">Este artigo mostra como definir um singleton em um ponto de extremidade OData na Web API 2.2.</span><span class="sxs-lookup"><span data-stu-id="49f5a-107">This article shows how to define a singleton in an OData endpoint in Web API 2.2.</span></span> <span data-ttu-id="49f5a-108">Para obter informações sobre quais um singleton é e como você pode se beneficiar de usá-lo, consulte [usando um singleton para definir sua entidade especial](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span><span class="sxs-lookup"><span data-stu-id="49f5a-108">For information on what a singleton is and how you can benefit from using it, see [Using a singleton to define your special entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span></span> <span data-ttu-id="49f5a-109">Para criar um ponto de extremidade OData V4 no API da Web, consulte [criar um OData v4 ponto de extremidade usando API Web ASP.NET 2.2](create-an-odata-v4-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="49f5a-109">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span> 

<span data-ttu-id="49f5a-110">Vamos criar um singleton em seu projeto de API da Web usando o modelo de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="49f5a-110">We'll create a singleton in your Web API project using the following data model:</span></span>

![Modelo de dados](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

<span data-ttu-id="49f5a-112">Um singleton chamado `Umbrella` serão definidos com base no tipo `Company`e um conjunto nomeado de entidades `Employees` será definida com base no tipo `Employee`.</span><span class="sxs-lookup"><span data-stu-id="49f5a-112">A singleton named `Umbrella` will be defined based on type `Company`, and an entity set named `Employees` will be defined based on type `Employee`.</span></span>

<span data-ttu-id="49f5a-113">A solução usada neste tutorial pode ser baixada em [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span><span class="sxs-lookup"><span data-stu-id="49f5a-113">The solution used in this tutorial can be downloaded from [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span></span>

## <a name="define-the-data-model"></a><span data-ttu-id="49f5a-114">Definir o modelo de dados</span><span class="sxs-lookup"><span data-stu-id="49f5a-114">Define the data model</span></span>

1. <span data-ttu-id="49f5a-115">Defina os tipos CLR.</span><span class="sxs-lookup"><span data-stu-id="49f5a-115">Define the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. <span data-ttu-id="49f5a-116">Gere o modelo EDM com base nos tipos de CLR.</span><span class="sxs-lookup"><span data-stu-id="49f5a-116">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="49f5a-117">Aqui, `builder.Singleton<Company>("Umbrella")` informa o construtor de modelo para criar um singleton chamado `Umbrella` no modelo de EDM.</span><span class="sxs-lookup"><span data-stu-id="49f5a-117">Here, `builder.Singleton<Company>("Umbrella")` tells the model builder to create a singleton named `Umbrella` in the EDM model.</span></span>

    <span data-ttu-id="49f5a-118">Os metadados gerados terão a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="49f5a-118">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    <span data-ttu-id="49f5a-119">Metadados do podemos ver que a propriedade de navegação `Company` no `Employees` conjunto de entidades está associado ao singleton `Umbrella`.</span><span class="sxs-lookup"><span data-stu-id="49f5a-119">From the metadata we can see that the navigation property `Company` in the `Employees` entity set is bound to the singleton `Umbrella`.</span></span> <span data-ttu-id="49f5a-120">A associação é feita automaticamente pelo `ODataConventionModelBuilder`, já que só `Umbrella` tem o `Company` tipo.</span><span class="sxs-lookup"><span data-stu-id="49f5a-120">The binding is done automatically by `ODataConventionModelBuilder`, since only `Umbrella` has the `Company` type.</span></span> <span data-ttu-id="49f5a-121">Se houver qualquer ambiguidade no modelo, você pode usar `HasSingletonBinding` para associar explicitamente uma propriedade de navegação em um singleton; `HasSingletonBinding` tem o mesmo efeito que usar o `Singleton` atributo na definição de tipo CLR:</span><span class="sxs-lookup"><span data-stu-id="49f5a-121">If there is any ambiguity in the model, you can use `HasSingletonBinding` to explicitly bind a navigation property to a singleton; `HasSingletonBinding` has the same effect as using the `Singleton` attribute in the CLR type definition:</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a><span data-ttu-id="49f5a-122">Definir o controlador de singleton</span><span class="sxs-lookup"><span data-stu-id="49f5a-122">Define the singleton controller</span></span>

<span data-ttu-id="49f5a-123">Como o controlador de EntitySet, o controlador de singleton herda `ODataController`, e o nome do controlador de singleton deve ser `[singletonName]Controller`.</span><span class="sxs-lookup"><span data-stu-id="49f5a-123">Like the EntitySet controller, the singleton controller inherits from `ODataController`, and the singleton controller name should be `[singletonName]Controller`.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

<span data-ttu-id="49f5a-124">Para lidar com diferentes tipos de solicitações, ações devem ser predefinidos no controlador.</span><span class="sxs-lookup"><span data-stu-id="49f5a-124">In order to handle different kinds of requests, actions are required to be pre-defined in the controller.</span></span> <span data-ttu-id="49f5a-125">**Roteamento de atributo** é habilitado por padrão na API Web 2.2.</span><span class="sxs-lookup"><span data-stu-id="49f5a-125">**Attribute routing** is enabled by default in WebApi 2.2.</span></span> <span data-ttu-id="49f5a-126">Por exemplo, para definir uma ação para tratar a consultar `Revenue` de `Company` usando o roteamento de atributo, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="49f5a-126">For example, to define an action to handle querying `Revenue` from `Company` using attribute routing, use the following:</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

<span data-ttu-id="49f5a-127">Se você não estiver disposto a definir os atributos de cada ação, basta definir as ações a seguir [convenções de roteamento OData](../odata-routing-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="49f5a-127">If you are not willing to define attributes for each action, just define your actions following [OData Routing Conventions](../odata-routing-conventions.md).</span></span> <span data-ttu-id="49f5a-128">Como uma chave não é necessária para consultar um singleton, as ações definidas no controlador singleton são ligeiramente diferentes das ações definidas no controlador entityset.</span><span class="sxs-lookup"><span data-stu-id="49f5a-128">Since a key is not required for querying a singleton, the actions defined in the singleton controller are slightly different from actions defined in the entityset controller.</span></span>

<span data-ttu-id="49f5a-129">Para referência, as assinaturas de método para cada definição de ação no controlador singleton estão listadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="49f5a-129">For reference, method signatures for every action definition in the singleton controller are listed below.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

<span data-ttu-id="49f5a-130">Basicamente, isso é tudo o que você precisa fazer no lado do serviço.</span><span class="sxs-lookup"><span data-stu-id="49f5a-130">Basically, this is all you need to do on the service side.</span></span> <span data-ttu-id="49f5a-131">O [projeto de exemplo](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contém todo o código para a solução e o cliente do OData que mostra como usar o singleton.</span><span class="sxs-lookup"><span data-stu-id="49f5a-131">The [sample project](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contains all of the code for the solution and the OData client that shows how to use the singleton.</span></span> <span data-ttu-id="49f5a-132">O cliente é criado seguindo as etapas em [criar um aplicativo de cliente do OData v4](create-an-odata-v4-client-app.md).</span><span class="sxs-lookup"><span data-stu-id="49f5a-132">The client is built by following the steps in [Create an OData v4 Client App](create-an-odata-v4-client-app.md).</span></span>

<span data-ttu-id="49f5a-133">.</span><span class="sxs-lookup"><span data-stu-id="49f5a-133">.</span></span> 

*<span data-ttu-id="49f5a-134">Graças ao Leo Hu para o conteúdo original deste artigo.</span><span class="sxs-lookup"><span data-stu-id="49f5a-134">Thanks to Leo Hu for the original content of this article.</span></span>*
