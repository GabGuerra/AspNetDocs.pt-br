---
ms.openlocfilehash: 984edac5f093d59bd5e1d826df8f32fda89f9e46
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024573"
---
# <a name="work-with-sqlite-in-an-aspnet-core-mvc-app"></a><span data-ttu-id="f4cef-101">Trabalhar com o SQLite em um aplicativo ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="f4cef-101">Work with SQLite in an ASP.NET Core MVC app</span></span>

<span data-ttu-id="f4cef-102">Por [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="f4cef-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="f4cef-103">O objeto `MvcMovieContext` cuida da tarefa de se conectar ao banco de dados e mapear objetos `Movie` para registros do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f4cef-103">The `MvcMovieContext` object handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="f4cef-104">O contexto de banco de dados é registrado com o contêiner [Injeção de Dependência](xref:fundamentals/dependency-injection) no método `ConfigureServices` no arquivo *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="f4cef-104">The database context is registered with the [Dependency Injection](xref:fundamentals/dependency-injection) container in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app-xplat/start-mvc/sample/MvcMovie/Startup.cs?name=snippet2&highlight=6-8)]

## <a name="sqlite"></a><span data-ttu-id="f4cef-105">SQLite</span><span class="sxs-lookup"><span data-stu-id="f4cef-105">SQLite</span></span>

<span data-ttu-id="f4cef-106">O site do [SQLite](https://www.sqlite.org/) afirma:</span><span class="sxs-lookup"><span data-stu-id="f4cef-106">The [SQLite](https://www.sqlite.org/) website states:</span></span>

> <span data-ttu-id="f4cef-107">O SQLite é um mecanismo de banco de dados SQL independente, de alta confiabilidade, inserido, completo e de domínio público.</span><span class="sxs-lookup"><span data-stu-id="f4cef-107">SQLite is a self-contained, high-reliability, embedded, full-featured, public-domain, SQL database engine.</span></span> <span data-ttu-id="f4cef-108">O SQLite é o mecanismo de banco de dados mais usado no mundo.</span><span class="sxs-lookup"><span data-stu-id="f4cef-108">SQLite is the most used database engine in the world.</span></span>

<span data-ttu-id="f4cef-109">Há muitas ferramentas de terceiros que podem ser baixadas para gerenciar e exibir um banco de dados SQLite.</span><span class="sxs-lookup"><span data-stu-id="f4cef-109">There are many third party tools you can download to manage and view a SQLite database.</span></span> <span data-ttu-id="f4cef-110">A imagem abaixo é do [Navegador do DB para SQLite](http://sqlitebrowser.org/).</span><span class="sxs-lookup"><span data-stu-id="f4cef-110">The image below is from [DB Browser for SQLite](http://sqlitebrowser.org/).</span></span> <span data-ttu-id="f4cef-111">Se você tiver uma ferramenta favorita do SQLite, deixe um comentário sobre o que mais gosta dela.</span><span class="sxs-lookup"><span data-stu-id="f4cef-111">If you have a favorite SQLite tool, leave a comment on what you like about it.</span></span>

![Navegador do BD do SQLite mostrando o BD de filmes](~/tutorials/first-mvc-app-xplat/working-with-sql/_static/dbb.png)

## <a name="seed-the-database"></a><span data-ttu-id="f4cef-113">Propagar o banco de dados</span><span class="sxs-lookup"><span data-stu-id="f4cef-113">Seed the database</span></span>

<span data-ttu-id="f4cef-114">Crie uma nova classe chamada `SeedData` na pasta *Models*.</span><span class="sxs-lookup"><span data-stu-id="f4cef-114">Create a new class named `SeedData` in the *Models* folder.</span></span> <span data-ttu-id="f4cef-115">Substitua o código gerado pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="f4cef-115">Replace the generated code with the following:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/SeedData.cs?name=snippet_1)]

<span data-ttu-id="f4cef-116">Se houver um filme no BD, o inicializador de semeadura será retornado.</span><span class="sxs-lookup"><span data-stu-id="f4cef-116">If there are any movies in the DB, the seed initializer returns.</span></span>

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a><span data-ttu-id="f4cef-117">Adicionar o inicializador de semeadura</span><span class="sxs-lookup"><span data-stu-id="f4cef-117">Add the seed initializer</span></span>

<span data-ttu-id="f4cef-118">Adicione o inicializador de semeadura ao método `Main` no arquivo *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="f4cef-118">Add the seed initializer to the `Main` method in the *Program.cs* file:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Program.cs)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Program.cs?highlight=6,16-32)]

::: moniker-end

### <a name="test-the-app"></a><span data-ttu-id="f4cef-119">Testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="f4cef-119">Test the app</span></span>

<span data-ttu-id="f4cef-120">Exclua todos os registros no BD (para que o método de semeadura seja executado).</span><span class="sxs-lookup"><span data-stu-id="f4cef-120">Delete all the records in the DB (So the seed method will run).</span></span> <span data-ttu-id="f4cef-121">Interrompa e inicie o aplicativo para propagar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f4cef-121">Stop and start the app to seed the database.</span></span>
   
<span data-ttu-id="f4cef-122">O aplicativo mostra os dados propagados.</span><span class="sxs-lookup"><span data-stu-id="f4cef-122">The app shows the seeded data.</span></span>

![Navegador aberto no aplicativo MVC de Filmes mostrando os dados de filmes](~/tutorials/first-mvc-app/working-with-sql/_static/m55.png)
