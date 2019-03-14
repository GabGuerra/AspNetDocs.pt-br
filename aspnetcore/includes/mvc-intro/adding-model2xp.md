---
ms.openlocfilehash: 0084d8c6bc5d16eaa1c3fa36d8aabb2aa31e1283
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029463"
---
<a name="cli"></a>
## <a name="perform-initial-migration"></a>Executar a migração inicial

Na linha de comando, execute os seguintes comandos de CLI do .NET Core:

```console
dotnet ef migrations add InitialCreate
dotnet ef database update
```

O comando `dotnet ef migrations add InitialCreate` gera código para criar o esquema de banco de dados inicial. O esquema é baseado no modelo especificado no `DbContext` (no arquivo *Models/MvcMovieContext.cs*). O argumento `Initial` é usado para nomear as migrações. Você pode usar qualquer nome, mas, por convenção, escolha um nome que descreve a migração. Consulte [Introdução às migrações](xref:data/ef-mvc/migrations#introduction-to-migrations) para obter mais informações.

O comando `dotnet ef database update` executa o método `Up` no arquivo *Migrations/\<time-stamp>_InitialCreate.cs*, que cria o banco de dados.
