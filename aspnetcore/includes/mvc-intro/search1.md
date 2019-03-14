---
ms.openlocfilehash: 24726fba7f431f701b264a988a8de1b67d41d8a2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048713"
---
# <a name="add-search-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="0c163-101">Adicionar a pesquisa a um aplicativo ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="0c163-101">Add search to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="0c163-102">Por [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="0c163-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="0c163-103">Nesta seção, você adiciona a funcionalidade de pesquisa ao método de ação `Index` que permite pesquisar filmes por *gênero* ou *nome*.</span><span class="sxs-lookup"><span data-stu-id="0c163-103">In this section you add search capability to the `Index` action method that lets you search movies by *genre* or *name*.</span></span>

<span data-ttu-id="0c163-104">Atualize o método `Index` pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="0c163-104">Update the `Index` method with the following code:</span></span>
<!--
[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Shared/_Layout.cshtml?highlight=7,31)]
-->

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_1stSearch)]

<span data-ttu-id="0c163-105">A primeira linha do método de ação `Index` cria uma consulta [LINQ](/dotnet/standard/using-linq) para selecionar os filmes:</span><span class="sxs-lookup"><span data-stu-id="0c163-105">The first line of the `Index` action method creates a [LINQ](/dotnet/standard/using-linq) query to select the movies:</span></span>

```csharp
var movies = from m in _context.Movie
             select m;
```

<span data-ttu-id="0c163-106">A consulta é *somente* definida neste ponto; ela **não** foi executada no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0c163-106">The query is *only* defined at this point, it has **not** been run against the database.</span></span>

<span data-ttu-id="0c163-107">Se o parâmetro `searchString` contiver uma cadeia de caracteres, a consulta de filmes será modificada para filtrar o valor da cadeia de caracteres de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="0c163-107">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_SearchNull2)]

<span data-ttu-id="0c163-108">O código `s => s.Title.Contains()` acima é uma [Expressão Lambda](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span><span class="sxs-lookup"><span data-stu-id="0c163-108">The `s => s.Title.Contains()` code above is a [Lambda Expression](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span></span> <span data-ttu-id="0c163-109">Lambdas são usados em consultas [LINQ](/dotnet/standard/using-linq) baseadas em método como argumentos para métodos de operadores de consulta padrão, como o método [Where](/dotnet/api/system.linq.enumerable.where) ou `Contains` (usado no código acima).</span><span class="sxs-lookup"><span data-stu-id="0c163-109">Lambdas are used in method-based [LINQ](/dotnet/standard/using-linq) queries as arguments to standard query operator methods such as the [Where](/dotnet/api/system.linq.enumerable.where) method or `Contains` (used in the code above).</span></span> <span data-ttu-id="0c163-110">As consultas LINQ não são executadas quando são definidas ou no momento em que são modificadas com uma chamada a um método, como `Where`, `Contains` ou `OrderBy`.</span><span class="sxs-lookup"><span data-stu-id="0c163-110">LINQ queries are not executed when they're defined or when they're modified by calling a method such as `Where`, `Contains`  or `OrderBy`.</span></span> <span data-ttu-id="0c163-111">Em vez disso, a execução da consulta é adiada.</span><span class="sxs-lookup"><span data-stu-id="0c163-111">Rather, query execution is deferred.</span></span>  <span data-ttu-id="0c163-112">Isso significa que a avaliação de uma expressão é atrasada até que seu valor realizado seja, de fato, iterado ou o método `ToListAsync` seja chamado.</span><span class="sxs-lookup"><span data-stu-id="0c163-112">That means that the evaluation of an expression is delayed until its realized value is actually iterated over or the `ToListAsync` method is called.</span></span> <span data-ttu-id="0c163-113">Para obter mais informações sobre a execução de consulta adiada, consulte [Execução da consulta](/dotnet/framework/data/adonet/ef/language-reference/query-execution).</span><span class="sxs-lookup"><span data-stu-id="0c163-113">For more information about deferred query execution, see [Query Execution](/dotnet/framework/data/adonet/ef/language-reference/query-execution).</span></span>

<span data-ttu-id="0c163-114">Observação: o método [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) é executado no banco de dados, não no código C# mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="0c163-114">Note: The [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) method is run on the database, not in the c# code shown above.</span></span> <span data-ttu-id="0c163-115">A diferenciação de maiúsculas e minúsculas na consulta depende do banco de dados e da ordenação.</span><span class="sxs-lookup"><span data-stu-id="0c163-115">The case sensitivity on the query depends on the database and the collation.</span></span> <span data-ttu-id="0c163-116">No SQL Server, [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) é mapeado para [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), que não diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="0c163-116">On SQL Server, [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) maps to [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), which is case insensitive.</span></span> <span data-ttu-id="0c163-117">No SQLite, com a ordenação padrão, ele diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="0c163-117">In SQLlite, with the default collation, it's case sensitive.</span></span>

<span data-ttu-id="0c163-118">Navegue para `/Movies/Index`.</span><span class="sxs-lookup"><span data-stu-id="0c163-118">Navigate to `/Movies/Index`.</span></span> <span data-ttu-id="0c163-119">Acrescente uma cadeia de consulta, como `?searchString=Ghost`, à URL.</span><span class="sxs-lookup"><span data-stu-id="0c163-119">Append a query string such as `?searchString=Ghost` to the URL.</span></span> <span data-ttu-id="0c163-120">Os filmes filtrados são exibidos.</span><span class="sxs-lookup"><span data-stu-id="0c163-120">The filtered movies are displayed.</span></span>

![Exibição de índice](~/tutorials/first-mvc-app/search/_static/ghost.png)

<span data-ttu-id="0c163-122">Se você alterar a assinatura do método `Index` para que ele tenha um parâmetro chamado `id`, o parâmetro `id` corresponderá o espaço reservado `{id}` opcional com as rotas padrão definidas em *Startup.cs*.</span><span class="sxs-lookup"><span data-stu-id="0c163-122">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the optional `{id}` placeholder for the default routes set in *Startup.cs*.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]
