---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: Diretrizes de segurança para a API Web ASP.NET 2 OData | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 02/06/2013
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 0e43ec6b1cbe922b00f0f71d08aed4d0f4c08af8
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58425854"
---
<a name="security-guidance-for-aspnet-web-api-2-odata"></a><span data-ttu-id="19c0c-102">Diretrizes de segurança para a API Web ASP.NET 2 OData</span><span class="sxs-lookup"><span data-stu-id="19c0c-102">Security Guidance for ASP.NET Web API 2 OData</span></span>
====================
<span data-ttu-id="19c0c-103">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="19c0c-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="19c0c-104">Este tópico descreve alguns dos problemas de segurança que você deve considerar ao expor um conjunto de dados por meio do OData.</span><span class="sxs-lookup"><span data-stu-id="19c0c-104">This topic describes some of the security issues that you should consider when exposing a dataset through OData.</span></span>

## <a name="edm-security"></a><span data-ttu-id="19c0c-105">Segurança EDM</span><span class="sxs-lookup"><span data-stu-id="19c0c-105">EDM Security</span></span>

<span data-ttu-id="19c0c-106">A semântica de consulta se baseia no modelo de dados de entidade (EDM), não os tipos de modelo subjacente.</span><span class="sxs-lookup"><span data-stu-id="19c0c-106">The query semantics are based on the entity data model (EDM), not the underlying model types.</span></span> <span data-ttu-id="19c0c-107">Você pode excluir uma propriedade do EDM, e não será visível para a consulta.</span><span class="sxs-lookup"><span data-stu-id="19c0c-107">You can exclude a property from the EDM and it will not be visible to the query.</span></span> <span data-ttu-id="19c0c-108">Por exemplo, suponha que seu modelo incluir um tipo de funcionário com uma propriedade de salário.</span><span class="sxs-lookup"><span data-stu-id="19c0c-108">For example, suppose your model includes an Employee type with a Salary property.</span></span> <span data-ttu-id="19c0c-109">Você talvez queira excluir essa propriedade do EDM para ocultá-la a partir de clientes.</span><span class="sxs-lookup"><span data-stu-id="19c0c-109">You might want to exclude this property from the EDM to hide it from clients.</span></span>

<span data-ttu-id="19c0c-110">Há duas maneiras de excluir uma propriedade do EDM.</span><span class="sxs-lookup"><span data-stu-id="19c0c-110">There are two ways to exclude a property from the EDM.</span></span> <span data-ttu-id="19c0c-111">Você pode definir as **[IgnoreDataMember]** atributo na propriedade na classe de modelo:</span><span class="sxs-lookup"><span data-stu-id="19c0c-111">You can set the **[IgnoreDataMember]** attribute on the property in the model class:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

<span data-ttu-id="19c0c-112">Você também pode remover programaticamente a propriedade do EDM:</span><span class="sxs-lookup"><span data-stu-id="19c0c-112">You can also remove the property from the EDM programmatically:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a><span data-ttu-id="19c0c-113">Segurança de consulta</span><span class="sxs-lookup"><span data-stu-id="19c0c-113">Query Security</span></span>

<span data-ttu-id="19c0c-114">Um cliente mal-intencionado ou ingênua pode ser capaz de construir uma consulta que demora muito tempo para executar.</span><span class="sxs-lookup"><span data-stu-id="19c0c-114">A malicious or naive client may be able to construct a query that takes a very long time to execute.</span></span> <span data-ttu-id="19c0c-115">Na pior das hipóteses, isso pode interromper o acesso ao seu serviço.</span><span class="sxs-lookup"><span data-stu-id="19c0c-115">In the worst case this can disrupt access to your service.</span></span>

<span data-ttu-id="19c0c-116">O **[Queryable]** atributo é um filtro de ação que analisa, valida e aplica a consulta.</span><span class="sxs-lookup"><span data-stu-id="19c0c-116">The **[Queryable]** attribute is an action filter that parses, validates, and applies the query.</span></span> <span data-ttu-id="19c0c-117">O filtro converte as opções de consulta em uma expressão LINQ.</span><span class="sxs-lookup"><span data-stu-id="19c0c-117">The filter converts the query options into a LINQ expression.</span></span> <span data-ttu-id="19c0c-118">Quando o controlador de OData retorna um **IQueryable** tipo, o **IQueryable** provedor LINQ converte a expressão LINQ em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="19c0c-118">When the OData controller returns an **IQueryable** type, the **IQueryable** LINQ provider converts the LINQ expression into a query.</span></span> <span data-ttu-id="19c0c-119">Portanto, o desempenho depende no provedor LINQ que é usado e também as características específicas de seu esquema de banco de dados ou conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="19c0c-119">Therefore, performance depends on the LINQ provider that is used, and also on the particular characteristics of your dataset or database schema.</span></span>

<span data-ttu-id="19c0c-120">Para obter mais informações sobre como usar as opções de consulta OData na API Web ASP.NET, consulte [que dão suporte a opções de consulta OData](supporting-odata-query-options.md).</span><span class="sxs-lookup"><span data-stu-id="19c0c-120">For more information about using OData query options in ASP.NET Web API, see [Supporting OData Query Options](supporting-odata-query-options.md).</span></span>

<span data-ttu-id="19c0c-121">Se você souber que todos os clientes são confiáveis (por exemplo, em um ambiente corporativo), ou se seu conjunto de dados for pequeno, o desempenho da consulta não pode ser um problema.</span><span class="sxs-lookup"><span data-stu-id="19c0c-121">If you know that all clients are trusted (for example, in an enterprise environment), or if your dataset is small, query performance might not be an issue.</span></span> <span data-ttu-id="19c0c-122">Caso contrário, você deve considerar as recomendações a seguir.</span><span class="sxs-lookup"><span data-stu-id="19c0c-122">Otherwise, you should consider the following recommendations.</span></span>

- <span data-ttu-id="19c0c-123">Testar o serviço com várias consultas e o banco de dados de perfil.</span><span class="sxs-lookup"><span data-stu-id="19c0c-123">Test your service with various queries and profile the DB.</span></span>
- <span data-ttu-id="19c0c-124">Habilite a paginação orientado para servidor evitar o retorno de um grande conjunto de dados em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="19c0c-124">Enable server-driven paging, to avoid returning a large data set in one query.</span></span> <span data-ttu-id="19c0c-125">Para obter mais informações, consulte [Server-Driven paginação](supporting-odata-query-options.md#server-paging).</span><span class="sxs-lookup"><span data-stu-id="19c0c-125">For more information, see [Server-Driven Paging](supporting-odata-query-options.md#server-paging).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- <span data-ttu-id="19c0c-126">Você precisa $filter e $orderby?</span><span class="sxs-lookup"><span data-stu-id="19c0c-126">Do you need $filter and $orderby?</span></span> <span data-ttu-id="19c0c-127">Alguns aplicativos podem permitir que o cliente de paginação, usando $top e $skip, mas desabilitar as outras opções de consulta.</span><span class="sxs-lookup"><span data-stu-id="19c0c-127">Some applications might allow client paging, using $top and $skip, but disable the other query options.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- <span data-ttu-id="19c0c-128">Considere restringir $orderby a propriedades em um índice clusterizado.</span><span class="sxs-lookup"><span data-stu-id="19c0c-128">Consider restricting $orderby to properties in a clustered index.</span></span> <span data-ttu-id="19c0c-129">Classificação de dados grandes sem um índice clusterizado é lento.</span><span class="sxs-lookup"><span data-stu-id="19c0c-129">Sorting large data without a clustered index is slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- <span data-ttu-id="19c0c-130">Contagem máxima de nós: O **MaxNodeCount** propriedade **[Queryable]** define o número máximo de nós permitido na árvore de sintaxe $filter.</span><span class="sxs-lookup"><span data-stu-id="19c0c-130">Maximum node count: The **MaxNodeCount** property on **[Queryable]** sets the maximum number nodes allowed in the $filter syntax tree.</span></span> <span data-ttu-id="19c0c-131">O valor padrão é 100, mas você talvez queira definir um valor mais baixo, pois um grande número de nós pode ser lento para compilar.</span><span class="sxs-lookup"><span data-stu-id="19c0c-131">The default value is 100, but you may want to set a lower value, because a large number of nodes can be slow to compile.</span></span> <span data-ttu-id="19c0c-132">Isso é especialmente verdadeiro se você estiver usando o LINQ to Objects (ou seja, consultas LINQ em uma coleção na memória, sem o uso de um provedor LINQ intermediário).</span><span class="sxs-lookup"><span data-stu-id="19c0c-132">This is particularly true if you are using LINQ to Objects (i.e., LINQ queries on a collection in memory, without the use of an intermediate LINQ provider).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- <span data-ttu-id="19c0c-133">Considere desabilitar as funções any () e All (), pois elas podem ser lentas.</span><span class="sxs-lookup"><span data-stu-id="19c0c-133">Consider disabling the any() and all() functions, as these can be slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- <span data-ttu-id="19c0c-134">Se quaisquer propriedades de cadeia de caracteres contém grandes cadeias de caracteres&#8212;por exemplo, uma descrição de produto ou uma entrada de blog&#8212;considere desabilitar as funções de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="19c0c-134">If any string properties contain large strings&#8212;for example, a product description or a blog entry&#8212;consider disabling the string functions.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- <span data-ttu-id="19c0c-135">Considere a possibilidade de desabilitação de filtragem nas propriedades de navegação.</span><span class="sxs-lookup"><span data-stu-id="19c0c-135">Consider disallowing filtering on navigation properties.</span></span> <span data-ttu-id="19c0c-136">Filtrando em Propriedades de navegação pode resultar em uma junção, que pode ser lenta, dependendo de seu esquema de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="19c0c-136">Filtering on navigation properties can result in a join, which might be slow, depending on your database schema.</span></span> <span data-ttu-id="19c0c-137">O código a seguir mostra um validador de consultas que impede a filtragem nas propriedades de navegação.</span><span class="sxs-lookup"><span data-stu-id="19c0c-137">The following code shows a query validator that prevents filtering on navigation properties.</span></span> <span data-ttu-id="19c0c-138">Para obter mais informações sobre os validadores de consulta, consulte [validação de consulta](supporting-odata-query-options.md#query-validation).</span><span class="sxs-lookup"><span data-stu-id="19c0c-138">For more information about query validators, see [Query Validation](supporting-odata-query-options.md#query-validation).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- <span data-ttu-id="19c0c-139">A possibilidade de restringir $filter consultas escrevendo um validador personalizado para seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="19c0c-139">Consider restricting $filter queries by writing a validator that is customized for your database.</span></span> <span data-ttu-id="19c0c-140">Por exemplo, considere essas duas consultas:</span><span class="sxs-lookup"><span data-stu-id="19c0c-140">For example, consider these two queries:</span></span> 

  - <span data-ttu-id="19c0c-141">Todos os filmes com atores cujo sobrenome começa com 'A'.</span><span class="sxs-lookup"><span data-stu-id="19c0c-141">All movies with actors whose last name starts with ‘A'.</span></span>
  - <span data-ttu-id="19c0c-142">Todos os filmes lançados em 1994.</span><span class="sxs-lookup"><span data-stu-id="19c0c-142">All movies released in 1994.</span></span>

    <span data-ttu-id="19c0c-143">A menos que os filmes são indexados por atores, a primeira consulta pode exigir que o mecanismo de banco de dados para digitalizar toda a lista de filmes.</span><span class="sxs-lookup"><span data-stu-id="19c0c-143">Unless movies are indexed by actors, the first query might require the DB engine to scan the entire list of movies.</span></span> <span data-ttu-id="19c0c-144">Enquanto a segunda consulta pode ser aceitável, assumindo a filmes são indexados por ano de lançamento.</span><span class="sxs-lookup"><span data-stu-id="19c0c-144">Whereas the second query might be acceptable, assuming movies are indexed by release year.</span></span>

    <span data-ttu-id="19c0c-145">O código a seguir mostra um validador que permite a filtragem de propriedades "ReleaseYear" e "Title", mas nenhuma outra propriedade.</span><span class="sxs-lookup"><span data-stu-id="19c0c-145">The following code shows a validator that allows filtering on the "ReleaseYear" and "Title" properties but no other properties.</span></span>

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- <span data-ttu-id="19c0c-146">Em geral, considere quais funções $filter que você precisa.</span><span class="sxs-lookup"><span data-stu-id="19c0c-146">In general, consider which $filter functions you need.</span></span> <span data-ttu-id="19c0c-147">Se os clientes não é necessário a expressividade completa de $filter, você pode limitar as funções permitidas.</span><span class="sxs-lookup"><span data-stu-id="19c0c-147">If your clients do not need the full expressiveness of $filter, you can limit the allowed functions.</span></span>
