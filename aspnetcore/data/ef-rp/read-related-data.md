---
title: Páginas Razor com o EF Core no ASP.NET Core – Ler dados relacionados – 6 de 8
author: rick-anderson
description: Neste tutorial, você lê e exibe dados relacionados – ou seja, os dados que o Entity Framework carrega nas propriedades de navegação.
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: data/ef-rp/read-related-data
ms.openlocfilehash: cf8733e1e806c4be0c4b217fc45c7a338a03a3ce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061853"
---
# <a name="razor-pages-with-ef-core-in-aspnet-core---read-related-data---6-of-8"></a>Páginas Razor com o EF Core no ASP.NET Core – Ler dados relacionados – 6 de 8

Por [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog) e [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [about the series](../../includes/RP-EF/intro.md)]

Neste tutorial, os dados relacionados são lidos e exibidos. Dados relacionados são dados que o EF Core carrega nas propriedades de navegação.

Caso tenha problemas que não consiga resolver, [baixe ou exiba o aplicativo concluído.](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples) [Instruções de download](xref:index#how-to-download-a-sample).

As seguintes ilustrações mostram as páginas concluídas para este tutorial:

![Página Índice de Cursos](read-related-data/_static/courses-index.png)

![Página Índice de Instrutores](read-related-data/_static/instructors-index.png)

## <a name="eager-explicit-and-lazy-loading-of-related-data"></a>Carregamento adiantado, explícito e lento de dados relacionados

Há várias maneiras pelas quais o EF Core pode carregar dados relacionados nas propriedades de navegação de uma entidade:

* [Carregamento adiantado](/ef/core/querying/related-data#eager-loading). O carregamento adiantado é quando uma consulta para um tipo de entidade também carrega entidades relacionadas. Quando a entidade é lida, seus dados relacionados são recuperados. Normalmente, isso resulta em uma única consulta de junção que recupera todos os dados necessários. O EF Core emitirá várias consultas para alguns tipos de carregamento adiantado. A emissão de várias consultas pode ser mais eficiente do que era o caso para algumas consultas no EF6 quando havia uma única consulta. O carregamento adiantado é especificado com os métodos `Include` e `ThenInclude`.

  ![Exemplo de carregamento adiantado](read-related-data/_static/eager-loading.png)
 
  O carregamento adiantado envia várias consultas quando a navegação de coleção é incluída:

  * Uma consulta para a consulta principal 
  * Uma consulta para cada "borda" de coleção na árvore de carregamento.

* Separe consultas com `Load`: os dados podem ser recuperados em consultas separadas e o EF Core "corrige" as propriedades de navegação. "Correção" significa que o EF Core popula automaticamente as propriedades de navegação. A separação de consultas com `Load` é mais parecida com o carregamento explícito do que com o carregamento adiantado.

  ![Exemplo de consultas separadas](read-related-data/_static/separate-queries.png)

  Observação: o EF Core corrige automaticamente as propriedades de navegação para outras entidades que foram carregadas anteriormente na instância do contexto. Mesmo se os dados de uma propriedade de navegação *não* foram incluídos de forma explícita, a propriedade ainda pode ser populada se algumas ou todas as entidades relacionadas foram carregadas anteriormente.

* [Carregamento explícito](/ef/core/querying/related-data#explicit-loading). Quando a entidade é lida pela primeira vez, os dados relacionados não são recuperados. Um código precisa ser escrito para recuperar os dados relacionados quando eles forem necessários. O carregamento explícito com consultas separadas resulta no envio de várias consultas ao BD. Com o carregamento explícito, o código especifica as propriedades de navegação a serem carregadas. Use o método `Load` para fazer o carregamento explícito. Por exemplo:

  ![Exemplo de carregamento explícito](read-related-data/_static/explicit-loading.png)

* [Carregamento lento](/ef/core/querying/related-data#lazy-loading). [O carregamento lento foi adicionado ao EF Core na versão 2.1](/ef/core/querying/related-data#lazy-loading). Quando a entidade é lida pela primeira vez, os dados relacionados não são recuperados. Na primeira vez que uma propriedade de navegação é acessada, os dados necessários para essa propriedade de navegação são recuperados automaticamente. Uma consulta é enviada para o BD sempre que uma propriedade de navegação é acessada pela primeira vez.

* O operador `Select` carrega somente os dados relacionados necessários.

## <a name="create-a-course-page-that-displays-department-name"></a>Criar uma página Course que exibe o nome do departamento

A entidade Course inclui uma propriedade de navegação que contém a entidade `Department`. A entidade `Department` contém o departamento ao qual o curso é atribuído.

Para exibir o nome do departamento atribuído em uma lista de cursos:

* Obtenha a propriedade `Name` da entidade `Department`.
* A entidade `Department` é obtida da propriedade de navegação `Course.Department`.

![Course.Department](read-related-data/_static/dep-crs.png)

<a name="scaffold"></a>
### <a name="scaffold-the-course-model"></a>Gerar o modelo Curso por scaffolding

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

Siga as instruções em [Gere um modelo de aluno por scaffold](xref:data/ef-rp/intro#scaffold-the-student-model) e use `Course` para a classe de modelo.

# <a name="net-core-clitabnetcore-cli"></a>[CLI do .NET Core](#tab/netcore-cli)

 Execute o seguinte comando:

  ```console
  dotnet aspnet-codegenerator razorpage -m Course -dc SchoolContext -udl -outDir Pages\Courses --referenceScriptLibraries
  ```

------

O comando anterior gera o modelo `Course` por scaffolding. Abra o projeto no Visual Studio.

Abra *Pages/Courses/Index.cshtml.cs* e examine o método `OnGetAsync`. O mecanismo de scaffolding especificou o carregamento adiantado para a propriedade de navegação `Department`. O método `Include` especifica o carregamento adiantado.

Execute o aplicativo e selecione o link **Cursos**. A coluna de departamento exibe a `DepartmentID`, que não é útil.

Atualize o método `OnGetAsync` pelo seguinte código:

[!code-csharp[](intro/samples/cu/Pages/Courses/Index.cshtml.cs?name=snippet_RevisedIndexMethod)]

O código anterior adiciona `AsNoTracking`. `AsNoTracking` melhora o desempenho porque as entidades retornadas não são controladas. As entidades não são controladas porque elas não são atualizadas no contexto atual.

Atualize *Pages/Courses/Index.cshtml* com a seguinte marcação realçada:

[!code-html[](intro/samples/cu/Pages/Courses/Index.cshtml?highlight=4,7,15-17,34-36,44)]

As seguintes alterações foram feitas na biblioteca gerada por código em scaffolding:

* Alterou o cabeçalho de Índice para Cursos.
* Adicionou uma coluna **Número** que mostra o valor da propriedade `CourseID`. Por padrão, as chaves primárias não são geradas por scaffolding porque normalmente não têm sentido para os usuários finais. No entanto, nesse caso, a chave primária é significativa.
* Alterou a coluna **Departamento** para que ela exiba o nome de departamento. O código exibe a propriedade `Name` da entidade `Department` que é carregada na propriedade de navegação `Department`:

  ```html
  @Html.DisplayFor(modelItem => item.Department.Name)
  ```

Execute o aplicativo e selecione a guia **Cursos** para ver a lista com nomes de departamentos.

![Página Índice de Cursos](read-related-data/_static/courses-index.png)

<a name="select"></a>
### <a name="loading-related-data-with-select"></a>Carregando dados relacionados com Select

O método `OnGetAsync` carrega dados relacionados com o método `Include`:

[!code-csharp[](intro/samples/cu/Pages/Courses/Index.cshtml.cs?name=snippet_RevisedIndexMethod&highlight=4)]

O operador `Select` carrega somente os dados relacionados necessários. Para itens únicos, como o `Department.Name`, ele usa um SQL INNER JOIN. Para coleções, ele usa outro acesso ao banco de dados, assim como o operador `Include` em coleções.

O seguinte código carrega dados relacionados com o método `Select`:

[!code-csharp[](intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs?name=snippet_RevisedIndexMethod&highlight=4)]

O `CourseViewModel`:

[!code-csharp[](intro/samples/cu/Models/SchoolViewModels/CourseViewModel.cs?name=snippet)]

Consulte [IndexSelect.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml) e [IndexSelect.cshtml.cs](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs) para obter um exemplo completo.

## <a name="create-an-instructors-page-that-shows-courses-and-enrollments"></a>Criar uma página Instrutores que mostra Cursos e Registros

Nesta seção, a página Instrutores é criada.

<a name="IP"></a>
![Página Índice de Instrutores](read-related-data/_static/instructors-index.png)

Essa página lê e exibe dados relacionados das seguintes maneiras:

* A lista de instrutores exibe dados relacionados da entidade `OfficeAssignment` (Office na imagem anterior). As entidades `Instructor` e `OfficeAssignment` estão em uma relação um para zero ou um. O carregamento adiantado é usado para as entidades `OfficeAssignment`. O carregamento adiantado costuma ser mais eficiente quando os dados relacionados precisam ser exibidos. Nesse caso, as atribuições de escritório para os instrutores são exibidas.
* Quando o usuário seleciona um instrutor (Pedro na imagem anterior), as entidades `Course` relacionadas são exibidas. As entidades `Instructor` e `Course` estão em uma relação muitos para muitos. O carregamento adiantado é usado para entidades `Course` e suas entidades `Department` relacionadas. Nesse caso, consultas separadas podem ser mais eficientes porque somente os cursos para o instrutor selecionado são necessários. Este exemplo mostra como usar o carregamento adiantado para propriedades de navegação em entidades que estão nas propriedades de navegação.
* Quando o usuário seleciona um curso (Química na imagem anterior), os dados relacionados da entidade `Enrollments` são exibidos. Na imagem anterior, o nome do aluno e a nota são exibidos. As entidades `Course` e `Enrollment` estão em uma relação um-para-muitos.

### <a name="create-a-view-model-for-the-instructor-index-view"></a>Criar um modelo de exibição para a exibição Índice de Instrutor

A página Instrutores mostra dados de três tabelas diferentes. É criado um modelo de exibição que inclui as três entidades que representam as três tabelas.

Na pasta *SchoolViewModels*, crie *InstructorIndexData.cs* com o seguinte código:

[!code-csharp[](intro/samples/cu/Models/SchoolViewModels/InstructorIndexData.cs)]

### <a name="scaffold-the-instructor-model"></a>Gerar o modelo Instrutor por scaffolding

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

Siga as instruções em [Gere um modelo de aluno por scaffold](xref:data/ef-rp/intro#scaffold-the-student-model) e use `Instructor` para a classe de modelo.

# <a name="net-core-clitabnetcore-cli"></a>[CLI do .NET Core](#tab/netcore-cli)

 Execute o seguinte comando:

  ```console
  dotnet aspnet-codegenerator razorpage -m Instructor -dc SchoolContext -udl -outDir Pages\Instructors --referenceScriptLibraries
  ```

------

O comando anterior gera o modelo `Instructor` por scaffolding. Execute o aplicativo e navegue para a página Instrutores.

Substitua *Pages/Instructors/Index.cshtml.cs* pelo seguinte código:

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index1.cshtml.cs?name=snippet_all&highlight=2,18-99)]

O método `OnGetAsync` aceita dados de rota opcionais para a ID do instrutor selecionado.

Examine a consulta no arquivo *Pages/Instructors/Index.cshtml*:

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index1.cshtml.cs?name=snippet_ThenInclude)]

A consulta tem duas inclusões:

* `OfficeAssignment`: mostrado na [exibição de instrutores](#IP).
* `CourseAssignments`: que mostra os cursos ministrados.


### <a name="update-the-instructors-index-page"></a>Atualizar a página Índice de instrutores

Atualize *Pages/Instructors/Index.cshtml* com a seguinte marcação:

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=1-65&highlight=1,5,8,16-21,25-32,43-57)]

A marcação anterior faz as seguintes alterações:

* Atualiza a diretiva `page` de `@page` para `@page "{id:int?}"`. `"{id:int?}"` é um modelo de rota. O modelo de rota altera cadeias de consulta de inteiro na URL para dados de rota. Por exemplo, clicar no link **Selecionar** de um o instrutor apenas com a diretiva `@page` produz uma URL semelhante à seguinte:

    `http://localhost:1234/Instructors?id=2`

    Quando a diretiva de página é `@page "{id:int?}"`, a URL anterior é:

    `http://localhost:1234/Instructors/2`

* O título de página é **Instrutores**.
* Adicionou uma coluna **Office** que exibe `item.OfficeAssignment.Location` somente se `item.OfficeAssignment` não é nulo. Como essa é uma relação um para zero ou um, pode não haver uma entidade OfficeAssignment relacionada.

  ```html
  @if (item.OfficeAssignment != null)
  {
      @item.OfficeAssignment.Location
  }
  ```

* Adicionou uma coluna **Courses** que exibe os cursos ministrados por cada instrutor. Consulte [Transição de linha explícita com `@:`](xref:mvc/views/razor#explicit-line-transition-with-) para obter mais informações sobre essa sintaxe Razor.

* Adicionou um código que adiciona `class="success"` dinamicamente ao elemento `tr` do instrutor selecionado. Isso define uma cor da tela de fundo para a linha selecionada usando uma classe Bootstrap.

  ```html
  string selectedRow = "";
  if (item.CourseID == Model.CourseID)
  {
      selectedRow = "success";
  }
  <tr class="@selectedRow">
  ```

* Adicionou um novo hiperlink rotulado **Selecionar**. Este link envia a ID do instrutor selecionado para o método `Index` e define uma cor da tela de fundo.

  ```html
  <a asp-action="Index" asp-route-id="@item.ID">Select</a> |
  ```

Execute o aplicativo e selecione a guia **Instrutores**. A página exibe o `Location` (escritório) da entidade `OfficeAssignment` relacionada. Se OfficeAssignment é nulo, uma célula de tabela vazia é exibida.

![Página Índice de Instrutores – nenhuma opção selecionada](read-related-data/_static/instructors-index-no-selection.png)

Clique no link **Selecionar**. O estilo de linha é alterado.

### <a name="add-courses-taught-by-selected-instructor"></a>Adicionar cursos ministrados pelo instrutor selecionado

Atualize o método `OnGetAsync` em *Pages/Instructors/Index.cshtml.cs* com o seguinte código:

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_OnGetAsync&highlight=1,8,16-999)]

Adicione `public int CourseID { get; set; }`

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_1&highlight=12)]

Examine a consulta atualizada:

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_ThenInclude)]

A consulta anterior adiciona as entidades `Department`.

O código a seguir é executado quando o instrutor é selecionado (`id != null`). O instrutor selecionado é recuperado da lista de instrutores no modelo de exibição. Em seguida, a propriedade `Courses` do modelo de exibição é carregada com as entidades `Course` da propriedade de navegação `CourseAssignments` desse instrutor.

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_ID)]

O método `Where` retorna uma coleção. No método `Where` anterior, uma única entidade `Instructor` é retornada. O método `Single` converte a coleção em uma única entidade `Instructor`. A entidade `Instructor` fornece acesso à propriedade `CourseAssignments`. `CourseAssignments` fornece acesso às entidades `Course` relacionadas.

![Instrutor para Cursos m:M](complex-data-model/_static/courseassignment.png)

O método `Single` é usado em uma coleção quando a coleção tem apenas um item. O método `Single` gera uma exceção se a coleção está vazia ou se há mais de um item. Uma alternativa é `SingleOrDefault`, que retorna um valor padrão (nulo, nesse caso) se a coleção está vazia. O uso de `SingleOrDefault` é uma coleção vazia:

* Resulta em uma exceção (da tentativa de encontrar uma propriedade `Courses` em uma referência nula).
* A mensagem de exceção indica menos claramente a causa do problema.

O seguinte código popula a propriedade `Enrollments` do modelo de exibição quando um curso é selecionado:

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_courseID)]

Adicione a seguinte marcação ao final do Razor Page *Pages/Courses/Index.cshtml*:

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=60-102&highlight=7-999)]

A marcação anterior exibe uma lista de cursos relacionados a um instrutor quando um instrutor é selecionado.

Teste o aplicativo. Clique em um link **Selecionar** na página Instrutores.

![Página Índice de Instrutores – instrutor selecionado](read-related-data/_static/instructors-index-instructor-selected.png)

### <a name="show-student-data"></a>Mostrar dados de alunos

Nesta seção, o aplicativo é atualizado para mostrar os dados de alunos de um curso selecionado.

Atualize a consulta no método `OnGetAsync` em *Pages/Instructors/Index.cshtml.cs* com o seguinte código:

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index.cshtml.cs?name=snippet_ThenInclude&highlight=6-9)]

Atualize *Pages/Instructors/Index.cshtml*. Adicione a seguinte marcação ao final do arquivo:

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=103-)]

A marcação anterior exibe uma lista dos alunos registrados no curso selecionado.

Atualize a página e selecione um instrutor. Selecione um curso para ver a lista de alunos registrados e suas notas.

![Página Índice de Instrutores – instrutor e curso selecionados](read-related-data/_static/instructors-index.png)

## <a name="using-single"></a>Usando Single

O método `Single` pode passar a condição `Where` em vez de chamar o método `Where` separadamente:

[!code-csharp[](intro/samples/cu/Pages/Instructors/IndexSingle.cshtml.cs?name=snippet_single&highlight=21-22,30-31)]

A abordagem `Single` anterior não oferece nenhum benefício em relação ao uso de `Where`. Alguns desenvolvedores preferem o estilo de abordagem `Single`.

## <a name="explicit-loading"></a>Carregamento explícito

O código atual especifica o carregamento adiantado para `Enrollments` e `Students`:

[!code-csharp[](intro/samples/cu/Pages/Instructors/Index.cshtml.cs?name=snippet_ThenInclude&highlight=6-9)]

Suponha que os usuários raramente desejem ver registros em um curso. Nesse caso, uma otimização será carregar apenas os dados de registro se eles forem solicitados. Nesta seção, o `OnGetAsync` é atualizado para usar o carregamento explícito de `Enrollments` e `Students`.

Atualize o `OnGetAsync` com o seguinte código:

[!code-csharp[](intro/samples/cu/Pages/Instructors/IndexXp.cshtml.cs?name=snippet_OnGetAsync&highlight=9-13,29-35)]

O código anterior remove as chamadas do método *ThenInclude* para dados de registro e de alunos. Se um curso é selecionado, o código realçado recupera:

* As entidades `Enrollment` para o curso selecionado.
* As entidades `Student` para cada `Enrollment`.

Observe que o código anterior comenta `.AsNoTracking()`. As propriedades de navegação apenas podem ser carregadas de forma explícita para entidades controladas.

Teste o aplicativo. De uma perspectiva dos usuários, o aplicativo se comporta de forma idêntica à versão anterior.

O próximo tutorial mostra como atualizar os dados relacionados.

>[!div class="step-by-step"]
>[Anterior](xref:data/ef-rp/complex-data-model)
>[Próximo](xref:data/ef-rp/update-related-data)
