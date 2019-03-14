---
ms.openlocfilehash: 68902f2839e3f8687509dd625535f210ab725f04
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038303"
---
# <a name="add-search-to-an-aspnet-core-razor-pages-app"></a><span data-ttu-id="49925-101">Adicionar a pesquisa ao aplicativo Razor Pages do ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="49925-101">Add search to an ASP.NET Core Razor Pages app</span></span>

<span data-ttu-id="49925-102">Por [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="49925-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="49925-103">Neste documento, a funcionalidade de pesquisa é adicionada à página de Índice que permite pesquisar filmes por *gênero* ou *nome*.</span><span class="sxs-lookup"><span data-stu-id="49925-103">In this document, search capability is added to the Index page that enables searching movies by *genre* or *name*.</span></span>

<span data-ttu-id="49925-104">Atualize o método `OnGetAsync` da página de Índice pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="49925-104">Update the Index page's `OnGetAsync` method with the following code:</span></span>

[!code-cshtml[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/_ViewStart.cshtml)]

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_1stSearch)]

<span data-ttu-id="49925-105">A primeira linha do método `OnGetAsync` cria uma consulta [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) para selecionar os filmes:</span><span class="sxs-lookup"><span data-stu-id="49925-105">The first line of the `OnGetAsync` method creates a [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) query to select the movies:</span></span>

```csharp
var movies = from m in _context.Movie
             select m;
```

<span data-ttu-id="49925-106">A consulta é *somente* definida neste ponto; ela **não** foi executada no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="49925-106">The query is *only* defined at this point, it has **not** been run against the database.</span></span>

<span data-ttu-id="49925-107">Se o parâmetro `searchString` contiver uma cadeia de caracteres, a consulta de filmes será modificada para filtrar a cadeia de caracteres de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="49925-107">If the `searchString` parameter contains a string, the movies query is modified to filter on the search string:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SearchNull)]

<span data-ttu-id="49925-108">O código `s => s.Title.Contains()` é uma [Expressão Lambda](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span><span class="sxs-lookup"><span data-stu-id="49925-108">The `s => s.Title.Contains()` code is a [Lambda Expression](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span></span> <span data-ttu-id="49925-109">Lambdas são usados em consultas [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) baseadas em método como argumentos para métodos de operadores de consulta padrão, como o método [Where](/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) ou `Contains` (usado no código anterior).</span><span class="sxs-lookup"><span data-stu-id="49925-109">Lambdas are used in method-based [LINQ](/dotnet/csharp/programming-guide/concepts/linq/) queries as arguments to standard query operator methods such as the [Where](/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) method or `Contains` (used in the preceding code).</span></span> <span data-ttu-id="49925-110">As consultas LINQ não são executadas quando são definidas ou quando são modificadas com uma chamada a um método (como `Where`, `Contains` ou `OrderBy`).</span><span class="sxs-lookup"><span data-stu-id="49925-110">LINQ queries are not executed when they're defined or when they're modified by calling a method (such as `Where`, `Contains`  or `OrderBy`).</span></span> <span data-ttu-id="49925-111">Em vez disso, a execução da consulta é adiada.</span><span class="sxs-lookup"><span data-stu-id="49925-111">Rather, query execution is deferred.</span></span> <span data-ttu-id="49925-112">Isso significa que a avaliação de uma expressão é atrasada até que seu valor realizado seja iterado ou o método `ToListAsync` seja chamado.</span><span class="sxs-lookup"><span data-stu-id="49925-112">That means the evaluation of an expression is delayed until its realized value is iterated over or the `ToListAsync` method is called.</span></span> <span data-ttu-id="49925-113">Consulte [Execução de consulta](/dotnet/framework/data/adonet/ef/language-reference/query-execution) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="49925-113">See [Query Execution](/dotnet/framework/data/adonet/ef/language-reference/query-execution) for more information.</span></span>

<span data-ttu-id="49925-114">**Observação:** o método [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) é executado no banco de dados, não no código C#.</span><span class="sxs-lookup"><span data-stu-id="49925-114">**Note:** The [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) method is run on the database, not in the C# code.</span></span> <span data-ttu-id="49925-115">A diferenciação de maiúsculas e minúsculas na consulta depende do banco de dados e da ordenação.</span><span class="sxs-lookup"><span data-stu-id="49925-115">The case sensitivity on the query depends on the database and the collation.</span></span> <span data-ttu-id="49925-116">No SQL Server, `Contains` é mapeado para [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), que não diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="49925-116">On SQL Server, `Contains` maps to [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), which is case insensitive.</span></span> <span data-ttu-id="49925-117">No SQLite, com a ordenação padrão, ele diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="49925-117">In SQLite, with the default collation, it's case sensitive.</span></span>

<span data-ttu-id="49925-118">Navegue para a página Movies e acrescente uma cadeia de consulta, como `?searchString=Ghost`, à URL (por exemplo, `http://localhost:5000/Movies?searchString=Ghost`).</span><span class="sxs-lookup"><span data-stu-id="49925-118">Navigate to the Movies page and append a query string such as `?searchString=Ghost` to the URL (for example, `http://localhost:5000/Movies?searchString=Ghost`).</span></span> <span data-ttu-id="49925-119">Os filmes filtrados são exibidos.</span><span class="sxs-lookup"><span data-stu-id="49925-119">The filtered movies are displayed.</span></span>

![Exibição de índice](../../tutorials/razor-pages/search/_static/ghost.png)

<span data-ttu-id="49925-121">Se o modelo de rota a seguir for adicionado à página de Índice, a cadeia de caracteres de pesquisa poderá ser passada como um segmento de URL (por exemplo, `http://localhost:5000/Movies/ghost`).</span><span class="sxs-lookup"><span data-stu-id="49925-121">If the following route template is added to the Index page, the search string can be passed as a URL segment (for example, `http://localhost:5000/Movies/ghost`).</span></span>

```cshtml
@page "{searchString?}"
```

<span data-ttu-id="49925-122">A restrição da rota anterior permite a pesquisa do título como dados de rota (um segmento de URL), em vez de como um valor de cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="49925-122">The preceding route constraint allows searching the title as route data (a URL segment) instead of as a query string value.</span></span>  <span data-ttu-id="49925-123">O `?` em `"{searchString?}"` significa que esse é um parâmetro de rota opcional.</span><span class="sxs-lookup"><span data-stu-id="49925-123">The `?` in `"{searchString?}"` means this is an optional route parameter.</span></span>

![Exibição de índice com a palavra “ghost” adicionada à URL e uma lista de filmes retornados com dois filmes, Ghostbusters e Ghostbusters 2](../../tutorials/razor-pages/search/_static/g2.png)

<span data-ttu-id="49925-125">No entanto, você não pode esperar que os usuários modifiquem a URL para pesquisar um filme.</span><span class="sxs-lookup"><span data-stu-id="49925-125">However, you can't expect users to modify the URL to search for a movie.</span></span> <span data-ttu-id="49925-126">Nesta etapa, a interface do usuário é adicionada para filtrar filmes.</span><span class="sxs-lookup"><span data-stu-id="49925-126">In this step, UI is added to filter movies.</span></span> <span data-ttu-id="49925-127">Se você adicionou a restrição de rota `"{searchString?}"`, remova-a.</span><span class="sxs-lookup"><span data-stu-id="49925-127">If you added the route constraint `"{searchString?}"`, remove it.</span></span>

<span data-ttu-id="49925-128">Abra o arquivo *Pages/Movies/Index.cshtml* e, em seguida, adicione a marcação `<form>` realçada no seguinte código:</span><span class="sxs-lookup"><span data-stu-id="49925-128">Open the *Pages/Movies/Index.cshtml* file, and add the `<form>` markup highlighted in the following code:</span></span>

[!code-cshtml[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index2.cshtml?highlight=14-19&range=1-22)]

<span data-ttu-id="49925-129">A marcação `<form>` HTML usa o [Auxiliar de Marcação de Formulário](xref:mvc/views/working-with-forms#the-form-tag-helper).</span><span class="sxs-lookup"><span data-stu-id="49925-129">The HTML `<form>` tag uses the [Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper).</span></span> <span data-ttu-id="49925-130">Quando o formulário é enviado, a cadeia de caracteres de filtro é enviada para a página *Pages/Movies/Index*.</span><span class="sxs-lookup"><span data-stu-id="49925-130">When the form is submitted, the filter string is sent to the *Pages/Movies/Index* page.</span></span> <span data-ttu-id="49925-131">Salve as alterações e teste o filtro.</span><span class="sxs-lookup"><span data-stu-id="49925-131">Save the changes and test the filter.</span></span>

![Exibição de índice com a palavra “ghost” digitada na caixa de texto Filtro de título](../../tutorials/razor-pages/search/_static/filter.png)

## <a name="search-by-genre"></a><span data-ttu-id="49925-133">Pesquisar por gênero</span><span class="sxs-lookup"><span data-stu-id="49925-133">Search by genre</span></span>

<span data-ttu-id="49925-134">Adicione as seguintes propriedades realçadas em *Pages/Movies/Index.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="49925-134">Add the following highlighted properties to *Pages/Movies/Index.cshtml.cs*:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_newProps&highlight=11-999)]

<span data-ttu-id="49925-135">O `SelectList Genres` contém a lista de gêneros.</span><span class="sxs-lookup"><span data-stu-id="49925-135">The `SelectList Genres` contains the list of genres.</span></span> <span data-ttu-id="49925-136">Isso permite que o usuário selecione um gênero na lista.</span><span class="sxs-lookup"><span data-stu-id="49925-136">This allows the user to select a genre from the list.</span></span>

<span data-ttu-id="49925-137">A propriedade `MovieGenre` contém o gênero específico selecionado pelo usuário (por exemplo, “Faroeste”).</span><span class="sxs-lookup"><span data-stu-id="49925-137">The `MovieGenre` property contains the specific genre the user selects (for example, "Western").</span></span>

<span data-ttu-id="49925-138">Atualize o método `OnGetAsync` pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="49925-138">Update the `OnGetAsync` method with the following code:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SearchGenre)]

<span data-ttu-id="49925-139">O código a seguir é uma consulta LINQ que recupera todos os gêneros do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="49925-139">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_LINQ)]

<span data-ttu-id="49925-140">O `SelectList` de gêneros é criado com a projeção dos gêneros distintos.</span><span class="sxs-lookup"><span data-stu-id="49925-140">The `SelectList` of genres is created by projecting the distinct genres.</span></span>

<!-- BUG in OPS
Tag snippet_selectlist's start line '75' should be less than end line '29' when resolving "[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]"

There's no start line.

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs?name=snippet_SelectList)]
-->

```csharp
Genres = new SelectList(await genreQuery.Distinct().ToListAsync());
```

### <a name="adding-search-by-genre"></a><span data-ttu-id="49925-141">Adicionando uma pesquisa por gênero</span><span class="sxs-lookup"><span data-stu-id="49925-141">Adding search by genre</span></span>

<span data-ttu-id="49925-142">Atualize *Index.cshtml* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="49925-142">Update *Index.cshtml* as follows:</span></span>

[!code-cshtml[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Pages/Movies/IndexFormGenreNoRating.cshtml?highlight=16-18&range=1-26)]

<span data-ttu-id="49925-143">Teste o aplicativo pesquisando por gênero, título do filme e por ambos.</span><span class="sxs-lookup"><span data-stu-id="49925-143">Test the app by searching by genre, by movie title, and by both.</span></span>
