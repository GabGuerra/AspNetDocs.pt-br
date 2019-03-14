---
ms.openlocfilehash: 0084d8c6bc5d16eaa1c3fa36d8aabb2aa31e1283
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029463"
---
<a name="cli"></a>
## <a name="perform-initial-migration"></a><span data-ttu-id="f9ee6-101">Executar a migração inicial</span><span class="sxs-lookup"><span data-stu-id="f9ee6-101">Perform initial migration</span></span>

<span data-ttu-id="f9ee6-102">Na linha de comando, execute os seguintes comandos de CLI do .NET Core:</span><span class="sxs-lookup"><span data-stu-id="f9ee6-102">From the command line, run the following .NET Core CLI commands:</span></span>

```console
dotnet ef migrations add InitialCreate
dotnet ef database update
```

<span data-ttu-id="f9ee6-103">O comando `dotnet ef migrations add InitialCreate` gera código para criar o esquema de banco de dados inicial.</span><span class="sxs-lookup"><span data-stu-id="f9ee6-103">The `dotnet ef migrations add InitialCreate` command generates code to create the initial database schema.</span></span> <span data-ttu-id="f9ee6-104">O esquema é baseado no modelo especificado no `DbContext` (no arquivo *Models/MvcMovieContext.cs*).</span><span class="sxs-lookup"><span data-stu-id="f9ee6-104">The schema is based on the model specified in the `DbContext` (In the *Models/MvcMovieContext.cs* file).</span></span> <span data-ttu-id="f9ee6-105">O argumento `Initial` é usado para nomear as migrações.</span><span class="sxs-lookup"><span data-stu-id="f9ee6-105">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="f9ee6-106">Você pode usar qualquer nome, mas, por convenção, escolha um nome que descreve a migração.</span><span class="sxs-lookup"><span data-stu-id="f9ee6-106">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="f9ee6-107">Consulte [Introdução às migrações](xref:data/ef-mvc/migrations#introduction-to-migrations) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="f9ee6-107">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="f9ee6-108">O comando `dotnet ef database update` executa o método `Up` no arquivo *Migrations/\<time-stamp>_InitialCreate.cs*, que cria o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f9ee6-108">The `dotnet ef database update` command runs the `Up` method in the *Migrations/\<time-stamp>_InitialCreate.cs* file, which creates the database.</span></span>
