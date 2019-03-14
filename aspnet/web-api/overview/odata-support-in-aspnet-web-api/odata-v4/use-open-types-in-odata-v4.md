---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Tipos abertos no OData v4 com a API Web ASP.NET | Microsoft Docs
author: microsoft
description: No OData v4, um tipo aberto é um tipo de stuctured que contém as propriedades dinâmicas, além de quaisquer propriedades que são declaradas na definição de tipo. Abra...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 77771d85532b8b622c2ad4ca219a38990e474c9c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042583"
---
<a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="ee2b4-104">Tipos abertos no OData v4 com a API da Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ee2b4-104">Open Types in OData v4 with ASP.NET Web API</span></span>
====================
<span data-ttu-id="ee2b4-105">por [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ee2b4-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ee2b4-106">No OData v4, uma *abrir tipo* é um tipo de stuctured que contém as propriedades dinâmicas, além de quaisquer propriedades que são declaradas na definição de tipo.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-106">In OData v4, an *open type* is a stuctured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="ee2b4-107">Tipos abertos permitem adicionar flexibilidade aos modelos de dados.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="ee2b4-108">Este tutorial mostra como usar tipos abertos no OData da API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="ee2b4-109">Este tutorial presume que você já sabe como criar um ponto de extremidade OData na API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="ee2b4-110">Se não, comece lendo [criar um ponto de extremidade OData v4](create-an-odata-v4-endpoint.md) primeiro.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ee2b4-111">Versões de software usadas no tutorial</span><span class="sxs-lookup"><span data-stu-id="ee2b4-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="ee2b4-112">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="ee2b4-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="ee2b4-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="ee2b4-113">OData v4</span></span>


<span data-ttu-id="ee2b4-114">Primeiro, algumas terminologias OData:</span><span class="sxs-lookup"><span data-stu-id="ee2b4-114">First, some OData terminology:</span></span>

- <span data-ttu-id="ee2b4-115">Tipo de entidade: Um tipo estruturado com uma chave.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="ee2b4-116">Tipo complexo: Um tipo estruturado sem uma chave.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="ee2b4-117">Abrir tipo: Um tipo com propriedades dinâmicas.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="ee2b4-118">Tipos de entidade e tipos complexos podem ser abertos.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="ee2b4-119">O valor de uma propriedade dinâmica pode ser um tipo primitivo, um tipo complexo ou um tipo de enumeração; ou uma coleção de qualquer um desses tipos.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="ee2b4-120">Para obter mais informações sobre tipos abertos, consulte o [especificação do OData v4](http://www.odata.org/documentation/odata-version-4-0/).</span><span class="sxs-lookup"><span data-stu-id="ee2b4-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="ee2b4-121">Instalar as bibliotecas de OData na Web</span><span class="sxs-lookup"><span data-stu-id="ee2b4-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="ee2b4-122">Use o Gerenciador de pacotes de NuGet para instalar as bibliotecas mais recentes do Web API OData.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="ee2b4-123">Da janela do Console do Gerenciador de pacotes:</span><span class="sxs-lookup"><span data-stu-id="ee2b4-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="ee2b4-124">Definir os tipos CLR</span><span class="sxs-lookup"><span data-stu-id="ee2b4-124">Define the CLR Types</span></span>

<span data-ttu-id="ee2b4-125">Comece definindo os modelos EDM como tipos CLR.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="ee2b4-126">Quando o modelo de dados de entidade (EDM) é criado,</span><span class="sxs-lookup"><span data-stu-id="ee2b4-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="ee2b4-127">`Category` é um tipo de enumeração.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="ee2b4-128">`Address` é um tipo complexo.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-128">`Address` is a complex type.</span></span> <span data-ttu-id="ee2b4-129">(Ele não tem uma chave, portanto, não é um tipo de entidade.)</span><span class="sxs-lookup"><span data-stu-id="ee2b4-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="ee2b4-130">`Customer` é um tipo de entidade.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-130">`Customer` is an entity type.</span></span> <span data-ttu-id="ee2b4-131">(Ele tem uma chave).</span><span class="sxs-lookup"><span data-stu-id="ee2b4-131">(It has a key.)</span></span>
- <span data-ttu-id="ee2b4-132">`Press` é um tipo complexo aberto.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="ee2b4-133">`Book` é um tipo de entidade aberto.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="ee2b4-134">Para criar um tipo aberto, o tipo CLR deve ter uma propriedade de tipo `IDictionary<string, object>`, que contém as propriedades dinâmicas.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="ee2b4-135">Criar o modelo EDM</span><span class="sxs-lookup"><span data-stu-id="ee2b4-135">Build the EDM Model</span></span>

<span data-ttu-id="ee2b4-136">Se você usar **ODataConventionModelBuilder** para criar o EDM `Press` e `Book` são automaticamente adicionados como tipos abertos, com base na presença de um `IDictionary<string, object>` propriedade.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="ee2b4-137">Você também pode compilar o EDM explicitamente, usando **ODataModelBuilder**.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="ee2b4-138">Adicionar um controlador de OData</span><span class="sxs-lookup"><span data-stu-id="ee2b4-138">Add an OData Controller</span></span>

<span data-ttu-id="ee2b4-139">Em seguida, adicione um controlador de OData.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-139">Next, add an OData controller.</span></span> <span data-ttu-id="ee2b4-140">Para este tutorial, vamos usar um controlador simplificado que dá suporte a apenas GET e POST solicita e usa uma lista na memória para armazenar entidades.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="ee2b4-141">Observe que a primeira `Book` instância não tem nenhuma propriedade dinâmica.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="ee2b4-142">O segundo `Book` instância tem as seguintes propriedades dinâmicas:</span><span class="sxs-lookup"><span data-stu-id="ee2b4-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="ee2b4-143">"Published": Tipo primitivo</span><span class="sxs-lookup"><span data-stu-id="ee2b4-143">"Published": Primitive type</span></span>
- <span data-ttu-id="ee2b4-144">"Authors": Coleção de tipos primitivos</span><span class="sxs-lookup"><span data-stu-id="ee2b4-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="ee2b4-145">"OtherCategories": Coleção de tipos de enumeração.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="ee2b4-146">Além disso, o `Press` propriedade isso `Book` instância tem as seguintes propriedades dinâmicas:</span><span class="sxs-lookup"><span data-stu-id="ee2b4-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="ee2b4-147">"Blog": Tipo primitivo</span><span class="sxs-lookup"><span data-stu-id="ee2b4-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="ee2b4-148">"Address": Tipo complexo</span><span class="sxs-lookup"><span data-stu-id="ee2b4-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="ee2b4-149">Consultar os metadados</span><span class="sxs-lookup"><span data-stu-id="ee2b4-149">Query the Metadata</span></span>

<span data-ttu-id="ee2b4-150">Para obter o documento de metadados do OData, envie uma solicitação GET para `~/$metadata`.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="ee2b4-151">O corpo da resposta deve ser semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="ee2b4-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="ee2b4-152">Do documento de metadados, você pode ver que:</span><span class="sxs-lookup"><span data-stu-id="ee2b4-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="ee2b4-153">Para o `Book` e `Press` tipos, o valor da `OpenType` atributo é true.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="ee2b4-154">O `Customer` e `Address` tipos não têm esse atributo.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="ee2b4-155">O `Book` tipo de entidade tem três propriedades declaradas: Pressione, título e ISBN.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="ee2b4-156">Os metadados do OData não incluem o `Book.Properties` propriedade da classe CLR.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="ee2b4-157">Da mesma forma, o `Press` tipo complexo tem apenas duas propriedades declaradas: Nome e categoria.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="ee2b4-158">Os metadados não incluem o `Press.DynamicProperties` propriedade da classe CLR.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="ee2b4-159">Consultar uma entidade</span><span class="sxs-lookup"><span data-stu-id="ee2b4-159">Query an Entity</span></span>

<span data-ttu-id="ee2b4-160">Para obter o livro com ISBN igual a "978-0-7356-7942-9", envie uma solicitação GET para `~/Books('978-0-7356-7942-9')`.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="ee2b4-161">O corpo da resposta deve ser semelhante ao seguinte.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-161">The response body should look similar to the following.</span></span> <span data-ttu-id="ee2b4-162">(Recuado para torná-lo mais legível).</span><span class="sxs-lookup"><span data-stu-id="ee2b4-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="ee2b4-163">Observe que as propriedades dinâmicas são incluídas embutidas com as propriedades declaradas.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="ee2b4-164">Uma entidade de POSTAGEM</span><span class="sxs-lookup"><span data-stu-id="ee2b4-164">POST an Entity</span></span>

<span data-ttu-id="ee2b4-165">Para adicionar uma entidade de livro, envie uma solicitação POST para `~/Books`.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="ee2b4-166">O cliente pode definir as propriedades dinâmicas no conteúdo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="ee2b4-167">Aqui está um exemplo de solicitação.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-167">Here is an example request.</span></span> <span data-ttu-id="ee2b4-168">Observe as propriedades "Price" e "Publicado".</span><span class="sxs-lookup"><span data-stu-id="ee2b4-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="ee2b4-169">Se você definir um ponto de interrupção no método do controlador, você pode ver que a API da Web adicionado essas propriedades para o `Properties` dicionário.</span><span class="sxs-lookup"><span data-stu-id="ee2b4-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="ee2b4-170">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ee2b4-170">Additional Resources</span></span>

[<span data-ttu-id="ee2b4-171">Exemplo de tipo aberto de OData</span><span class="sxs-lookup"><span data-stu-id="ee2b4-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
