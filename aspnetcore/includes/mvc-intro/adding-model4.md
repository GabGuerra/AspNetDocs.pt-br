---
ms.openlocfilehash: cf30f952c08d9801eead9574d4fc5073e80ceb71
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57027883"
---
<span data-ttu-id="e2bb6-101">O código realçado acima mostra o contexto de banco de dados do filme que está sendo adicionado ao contêiner [Injeção de Dependência](xref:fundamentals/dependency-injection) (No arquivo *Startup.cs*).</span><span class="sxs-lookup"><span data-stu-id="e2bb6-101">The highlighted code above shows the movie database context being added to the [Dependency Injection](xref:fundamentals/dependency-injection) container (In the *Startup.cs* file).</span></span> <span data-ttu-id="e2bb6-102">`services.AddDbContext<MvcMovieContext>(options =>` especifica o banco de dados a ser usado e a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-102">`services.AddDbContext<MvcMovieContext>(options =>` specifies the database to use and the connection string.</span></span> <span data-ttu-id="e2bb6-103">`=>` é um [operador lambda](/dotnet/articles/csharp/language-reference/operators/lambda-operator).</span><span class="sxs-lookup"><span data-stu-id="e2bb6-103">`=>` is a [lambda operator](/dotnet/articles/csharp/language-reference/operators/lambda-operator).</span></span>

<span data-ttu-id="e2bb6-104">Abra o arquivo *Controllers/MoviesController.cs* e examine o construtor:</span><span class="sxs-lookup"><span data-stu-id="e2bb6-104">Open the *Controllers/MoviesController.cs* file and examine the constructor:</span></span>

<!-- l.. Make copy of Movies controller because we comment out the initial index method and update it later  -->

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Controllers/MC1.cs?name=snippet_1)] 

<span data-ttu-id="e2bb6-105">O construtor usa a [Injeção de Dependência](xref:fundamentals/dependency-injection) para injetar o contexto de banco de dados (`MvcMovieContext `) no controlador.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-105">The constructor uses [Dependency Injection](xref:fundamentals/dependency-injection) to inject the database context (`MvcMovieContext `) into the controller.</span></span> <span data-ttu-id="e2bb6-106">O contexto de banco de dados é usado em cada um dos métodos [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) no controlador.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-106">The database context is used in each of the [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) methods in the controller.</span></span>

<a name="strongly-typed-models-keyword-label"></a>
<a name="strongly-typed-models-and-the--keyword"></a>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="e2bb6-107">Modelos fortemente tipados e a palavra-chave @model</span><span class="sxs-lookup"><span data-stu-id="e2bb6-107">Strongly typed models and the @model keyword</span></span>

<span data-ttu-id="e2bb6-108">Anteriormente neste tutorial, você viu como um controlador pode passar dados ou objetos para uma exibição usando o dicionário `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-108">Earlier in this tutorial, you saw how a controller can pass data or objects to a view using the `ViewData` dictionary.</span></span> <span data-ttu-id="e2bb6-109">O dicionário `ViewData` é um objeto dinâmico que fornece uma maneira conveniente de associação tardia para passar informações para uma exibição.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-109">The `ViewData` dictionary is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="e2bb6-110">O MVC também fornece a capacidade de passar objetos de modelo fortemente tipados para uma exibição.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-110">MVC also provides the ability to pass strongly typed model objects to a view.</span></span> <span data-ttu-id="e2bb6-111">Essa abordagem fortemente tipada permite uma melhor verificação em tempo de compilação do código.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-111">This strongly typed approach enables better compile-time checking of your code.</span></span> <span data-ttu-id="e2bb6-112">O mecanismo de scaffolding usou essa abordagem (ou seja, passando um modelo fortemente tipado) com a classe `MoviesController` e as exibições quando ele criou os métodos e as exibições.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-112">The scaffolding mechanism used this approach (that is, passing a strongly typed model) with the `MoviesController` class and views when it created the methods and views.</span></span>

<span data-ttu-id="e2bb6-113">Examine o método `Details` gerado no arquivo *Controllers/MoviesController.cs*:</span><span class="sxs-lookup"><span data-stu-id="e2bb6-113">Examine the generated `Details` method in the *Controllers/MoviesController.cs* file:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Controllers/MoviesController.cs?name=snippet_details)]

<span data-ttu-id="e2bb6-114">O parâmetro `id` geralmente é passado como dados de rota.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-114">The `id` parameter is generally passed as route data.</span></span> <span data-ttu-id="e2bb6-115">Por exemplo, `http://localhost:5000/movies/details/1` define:</span><span class="sxs-lookup"><span data-stu-id="e2bb6-115">For example `http://localhost:5000/movies/details/1` sets:</span></span>

* <span data-ttu-id="e2bb6-116">O controlador para o controlador `movies` (o primeiro segmento de URL).</span><span class="sxs-lookup"><span data-stu-id="e2bb6-116">The controller to the `movies` controller (the first URL segment).</span></span>
* <span data-ttu-id="e2bb6-117">A ação para `details` (o segundo segmento de URL).</span><span class="sxs-lookup"><span data-stu-id="e2bb6-117">The action to `details` (the second URL segment).</span></span>
* <span data-ttu-id="e2bb6-118">A ID como 1 (o último segmento de URL).</span><span class="sxs-lookup"><span data-stu-id="e2bb6-118">The id to 1 (the last URL segment).</span></span>

<span data-ttu-id="e2bb6-119">Você também pode passar a `id` com uma cadeia de consulta da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e2bb6-119">You can also pass in the `id` with a query string as follows:</span></span>

`http://localhost:1234/movies/details?id=1`

<span data-ttu-id="e2bb6-120">O parâmetro `id` é definido como um [tipo que permite valor nulo](/dotnet/csharp/programming-guide/nullable-types/index) (`int?`), caso um valor de ID não seja fornecido.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-120">The `id` parameter is defined as a [nullable type](/dotnet/csharp/programming-guide/nullable-types/index) (`int?`) in case an ID value isn't provided.</span></span>

<span data-ttu-id="e2bb6-121">Um [expressão lambda](/dotnet/articles/csharp/programming-guide/statements-expressions-operators/lambda-expressions) é passada para `FirstOrDefaultAsync` para selecionar as entidades de filmes que correspondem ao valor da cadeia de consulta ou de dados da rota.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-121">A [lambda expression](/dotnet/articles/csharp/programming-guide/statements-expressions-operators/lambda-expressions) is passed in to `FirstOrDefaultAsync` to select movie entities that match the route data or query string value.</span></span>

```csharp
var movie = await _context.Movie
    .FirstOrDefaultAsync(m => m.Id == id);
```

<span data-ttu-id="e2bb6-122">Se for encontrado um filme, uma instância do modelo `Movie` será passada para a exibição `Details`:</span><span class="sxs-lookup"><span data-stu-id="e2bb6-122">If a movie is found, an instance of the `Movie` model is passed to the `Details` view:</span></span>

```csharp
return View(movie);
   ```

<span data-ttu-id="e2bb6-123">Examine o conteúdo do arquivo *Views/Movies/Details.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e2bb6-123">Examine the contents of the *Views/Movies/Details.cshtml* file:</span></span>

[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/DetailsOriginal.cshtml)]

<span data-ttu-id="e2bb6-124">Incluindo uma instrução `@model` na parte superior do arquivo de exibição, você pode especificar o tipo de objeto esperado pela exibição.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-124">By including a `@model` statement at the top of the view file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="e2bb6-125">Quando você criou o controlador de filmes, a seguinte instrução `@model` foi automaticamente incluída na parte superior do arquivo *Details.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e2bb6-125">When you created the movie controller, the following `@model` statement was automatically included at the top of the *Details.cshtml* file:</span></span>

```HTML
@model MvcMovie.Models.Movie
   ```

<span data-ttu-id="e2bb6-126">Esta diretiva `@model` permite acessar o filme que o controlador passou para a exibição usando um objeto `Model` fortemente tipado.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-126">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="e2bb6-127">Por exemplo, na exibição *Details.cshtml*, o código passa cada campo de filme para os Auxiliares de HTML `DisplayNameFor` e `DisplayFor` com o objeto `Model` fortemente tipado.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-127">For example, in the *Details.cshtml* view, the code passes each movie field to the `DisplayNameFor` and `DisplayFor` HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="e2bb6-128">Os métodos `Create` e `Edit` e as exibições também passam um objeto de modelo `Movie`.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-128">The `Create` and `Edit` methods and views also pass a `Movie` model object.</span></span>

<span data-ttu-id="e2bb6-129">Examine a exibição *Index.cshtml* e o método `Index` no controlador Movies.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-129">Examine the *Index.cshtml* view and the `Index` method in the Movies controller.</span></span> <span data-ttu-id="e2bb6-130">Observe como o código cria um objeto `List` quando ele chama o método `View`.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-130">Notice how the code creates a `List` object when it calls the `View` method.</span></span> <span data-ttu-id="e2bb6-131">O código passa esta lista `Movies` do método de ação `Index` para a exibição:</span><span class="sxs-lookup"><span data-stu-id="e2bb6-131">The code passes this `Movies` list from the `Index` action method to the view:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Controllers/MC1.cs?name=snippet_index)]

<span data-ttu-id="e2bb6-132">Quando você criou o controlador de filmes, o scaffolding incluiu automaticamente a seguinte instrução `@model` na parte superior do arquivo *Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e2bb6-132">When you created the movies controller, scaffolding automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

<!-- Copy Index.cshtml to IndexOriginal.cshtml -->

[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/IndexOriginal.cshtml?range=1)]

<span data-ttu-id="e2bb6-133">A diretiva `@model` permite acessar a lista de filmes que o controlador passou para a exibição usando um objeto `Model` fortemente tipado.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-133">The `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="e2bb6-134">Por exemplo, na exibição *Index.cshtml*, o código executa um loop pelos filmes com uma instrução `foreach` no objeto `Model` fortemente tipado:</span><span class="sxs-lookup"><span data-stu-id="e2bb6-134">For example, in the *Index.cshtml* view, the code loops through the movies with a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/IndexOriginal.cshtml?highlight=1,31,34,37,40,43,46-48)]

<span data-ttu-id="e2bb6-135">Como o objeto `Model` é fortemente tipado (como um objeto `IEnumerable<Movie>`), cada item no loop é tipado como `Movie`.</span><span class="sxs-lookup"><span data-stu-id="e2bb6-135">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each item in the loop is typed as `Movie`.</span></span> <span data-ttu-id="e2bb6-136">Entre outros benefícios, isso significa que você obtém a verificação em tempo de compilação do código:</span><span class="sxs-lookup"><span data-stu-id="e2bb6-136">Among other benefits, this means that you get compile-time checking of the code:</span></span>
