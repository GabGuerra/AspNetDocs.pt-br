---
title: Páginas Razor com o EF Core no ASP.NET Core – CRUD – 2 de 8
author: rick-anderson
description: Mostra como criar, ler, atualizar e excluir com o EF Core
ms.author: riande
ms.date: 6/31/2017
uid: data/ef-rp/crud
ms.openlocfilehash: 4af16bdf3928609214c1255cdd411312c8b7d3f3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040103"
---
# <a name="razor-pages-with-ef-core-in-aspnet-core---crud---2-of-8"></a>Páginas Razor com o EF Core no ASP.NET Core – CRUD – 2 de 8

[!INCLUDE[2.0 version](~/includes/RP-EF/20-pdf.md)]

::: moniker range=">= aspnetcore-2.1"

Por [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog) e [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [about the series](~/includes/RP-EF/intro.md)]

Neste tutorial, o código CRUD (criar, ler, atualizar e excluir) gerado por scaffolding é examinado e personalizado.

Para minimizar a complexidade e manter o foco destes tutoriais no EF Core, o código do EF Core é usado nos modelos de página. Alguns desenvolvedores usam um padrão de repositório ou de camada de serviço para criar uma camada de abstração entre a interface do usuário (Páginas do Razor) e a camada de acesso a dados.

Neste tutorial, as Razor Pages Criar, Editar, Excluir e Detalhes na pasta *Student* são examinadas.

O código gerado por scaffolding usa o seguinte padrão para as páginas Criar, Editar e Excluir:

* Obtenha e exiba os dados solicitados com o método HTTP GET `OnGetAsync`.
* Salve as alterações nos dados com o método HTTP POST `OnPostAsync`.

As páginas Índice e Detalhes obtêm e exibem os dados solicitados com o método HTTP GET `OnGetAsync`

## <a name="singleordefaultasync-vs-firstordefaultasync"></a>SingleOrDefaultAsync vs. FirstOrDefaultAsync

O código gerado usa [FirstOrDefaultAsync](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.firstordefaultasync#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_FirstOrDefaultAsync__1_System_Linq_IQueryable___0__System_Threading_CancellationToken_), que geralmente é uma preferência em relação a [SingleOrDefaultAsync](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.singleordefaultasync#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_SingleOrDefaultAsync__1_System_Linq_IQueryable___0__System_Linq_Expressions_Expression_System_Func___0_System_Boolean___System_Threading_CancellationToken_).

 `FirstOrDefaultAsync` é mais eficiente que `SingleOrDefaultAsync` na busca de uma entidade:

* A menos que o código precise verificar se não há mais de uma entidade retornada da consulta.
* `SingleOrDefaultAsync` busca mais dados e faz o trabalho desnecessário.
* `SingleOrDefaultAsync` gera uma exceção se há mais de uma entidade que se ajusta à parte do filtro.
* `FirstOrDefaultAsync` não gera uma exceção se há mais de uma entidade que se ajusta à parte do filtro.

<a name="FindAsync"></a>

### <a name="findasync"></a>FindAsync

Em grande parte do código gerado por scaffolding, [FindAsync](/dotnet/api/microsoft.entityframeworkcore.dbcontext.findasync#Microsoft_EntityFrameworkCore_DbContext_FindAsync_System_Type_System_Object___) pode ser usado no lugar de `FirstOrDefaultAsync`.

`FindAsync`:

* Encontra uma entidade com o PK (chave primária). Se uma entidade com o PK está sendo controlada pelo contexto, ela é retornada sem uma solicitação para o BD.
* É simples e conciso.
* É otimizado para pesquisar uma única entidade.
* Pode ter benefícios de desempenho em algumas situações, mas isso é raro em aplicativos Web.
* Usa [FirstAsync](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.firstasync#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_FirstAsync__1_System_Linq_IQueryable___0__System_Linq_Expressions_Expression_System_Func___0_System_Boolean___System_Threading_CancellationToken_) em vez de [SingleAsync](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.singleasync#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_SingleAsync__1_System_Linq_IQueryable___0__System_Linq_Expressions_Expression_System_Func___0_System_Boolean___System_Threading_CancellationToken_) de forma implícita.

Mas se você deseja `Include` outras entidades, `FindAsync` não é mais apropriado. Isso significa que talvez seja necessário abandonar `FindAsync` e passar para uma consulta à medida que o aplicativo avança.

## <a name="customize-the-details-page"></a>Personalizar a página Detalhes

Navegue para a página `Pages/Students`. Os links **Editar**, **Detalhes** e **Excluir** são gerados pelo [Auxiliar de Marcação de Âncora](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) no arquivo *Pages/Students/Index.cshtml*.

[!code-cshtml[](intro/samples/cu21/Pages/Students/Index1.cshtml?name=snippet)]

Execute o aplicativo e selecione o link **Detalhes**. A URL tem o formato `http://localhost:5000/Students/Details?id=2`. A ID do Aluno é passada com uma cadeia de caracteres de consulta (`?id=2`).

Atualize as Páginas Editar, Detalhes e Excluir do Razor para que elas usem o modelo de rota `"{id:int}"`. Altere a diretiva de página de cada uma dessas páginas de `@page` para `@page "{id:int}"`.

Uma solicitação para a página com o modelo de rota "{id:int}" que **não** inclui um valor inteiro de rota retorna um erro HTTP 404 (não encontrado). Por exemplo, `http://localhost:5000/Students/Details` retorna um erro 404. Para tornar a ID opcional, acrescente `?` à restrição de rota:

 ```cshtml
@page "{id:int?}"
```

Execute o aplicativo, clique em um link Detalhes e verifique se a URL está passando a ID como dados de rota (`http://localhost:5000/Students/Details/2`).

Não altere `@page` globalmente para `@page "{id:int}"`, pois isso desfaz os links para as páginas Início e Criar.

<!-- See https://github.com/aspnet/Scaffolding/issues/590 -->

### <a name="add-related-data"></a>Adicionar dados relacionados

O código gerado por scaffolding para a página Índice de Alunos não inclui a propriedade `Enrollments`. Nesta seção, o conteúdo da coleção `Enrollments` é exibido na página Detalhes.

O método `OnGetAsync` de *Pages/Students/Details.cshtml.cs* usa o método `FirstOrDefaultAsync` para recuperar uma única entidade `Student`. Adicione o seguinte código realçado:

[!code-csharp[](intro/samples/cu21/Pages/Students/Details.cshtml.cs?name=snippet_Details&highlight=8-12)]

Os métodos [Include](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.include) e [ThenInclude](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.theninclude#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_ThenInclude__3_Microsoft_EntityFrameworkCore_Query_IIncludableQueryable___0_System_Collections_Generic_IEnumerable___1___System_Linq_Expressions_Expression_System_Func___1___2___) fazem com que o contexto carregue a propriedade de navegação `Student.Enrollments` e, dentro de cada registro, a propriedade de navegação `Enrollment.Course`. Esses métodos são examinados em detalhes no tutorial de dados relacionado à leitura.

O método [AsNoTracking](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.asnotracking#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_AsNoTracking__1_System_Linq_IQueryable___0__) melhora o desempenho em cenários em que as entidades retornadas não são atualizadas no contexto atual. `AsNoTracking` é abordado mais adiante neste tutorial.

### <a name="display-related-enrollments-on-the-details-page"></a>Exibir registros relacionados na página Detalhes

Abra *Pages/Students/Details.cshtml*. Adicione o seguinte código realçado para exibir uma lista de registros:

[!code-cshtml[](intro/samples/cu21/Pages/Students/Details.cshtml?highlight=32-53)]

Se o recuo do código estiver incorreto depois que o código for colado, pressione CTRL-K-D para corrigi-lo.

O código anterior percorre as entidades na propriedade de navegação `Enrollments`. Para cada registro, ele exibe o nome do curso e a nota. O título do curso é recuperado da entidade Course, que é armazenada na propriedade de navegação `Course` da entidade Enrollments.

Execute o aplicativo, selecione a guia **Alunos** e clique no link **Detalhes** de um aluno. A lista de cursos e notas do aluno selecionado é exibida.

## <a name="update-the-create-page"></a>Atualizar a página Criar

Atualize o método `OnPostAsync` em *Pages/Students/Create.cshtml.cs* com o seguinte código:

[!code-csharp[](intro/samples/cu21/Pages/Students/Create.cshtml.cs?name=snippet_OnPostAsync)]

<a name="TryUpdateModelAsync"></a>

### <a name="tryupdatemodelasync"></a>TryUpdateModelAsync

Examine o código [TryUpdateModelAsync](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.tryupdatemodelasync#Microsoft_AspNetCore_Mvc_ControllerBase_TryUpdateModelAsync_System_Object_System_Type_System_String_):

[!code-csharp[](intro/samples/cu21/Pages/Students/Create.cshtml.cs?name=snippet_TryUpdateModelAsync)]

No código anterior, `TryUpdateModelAsync<Student>` tenta atualizar o objeto `emptyStudent` usando os valores de formulário postados da propriedade [PageContext](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.pagecontext#Microsoft_AspNetCore_Mvc_RazorPages_PageModel_PageContext) no [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel). `TryUpdateModelAsync` atualiza apenas as propriedades listadas (`s => s.FirstMidName, s => s.LastName, s => s.EnrollmentDate`).

Na amostra anterior:

* O segundo argumento (`"student", // Prefix`) é o prefixo usado para pesquisar valores. Não diferencia maiúsculas de minúsculas.
* Os valores de formulário postados são convertidos nos tipos no modelo `Student` usando o [model binding](xref:mvc/models/model-binding#how-model-binding-works).

<a id="overpost"></a>

### <a name="overposting"></a>Excesso de postagem

O uso de `TryUpdateModel` para atualizar campos com valores postados é uma melhor prática de segurança porque ele impede o excesso de postagem. Por exemplo, suponha que a entidade Student inclua uma propriedade `Secret` que esta página da Web não deve atualizar nem adicionar:

[!code-csharp[](intro/samples/cu21/Models/StudentZsecret.cs?name=snippet_Intro&highlight=7)]

Mesmo que o aplicativo não tenha um campo `Secret` na Página criar/atualizar do Razor, um invasor pode definir o valor `Secret` por excesso de postagem. Um invasor pode usar uma ferramenta como o Fiddler ou escrever um JavaScript para postar um valor de formulário `Secret`. O código original não limita os campos que o associador de modelos usa quando ele cria uma instância Student.

Seja qual for o valor que o invasor especificou para o campo de formulário `Secret`, ele será atualizado no BD. A imagem a seguir mostra a ferramenta Fiddler adicionando o campo `Secret` (com o valor "OverPost") aos valores de formulário postados.

![Fiddler adicionando o campo Secreto](../ef-mvc/crud/_static/fiddler.png)

O valor "OverPost" foi adicionado com êxito à propriedade `Secret` da linha inserida. O designer do aplicativo nunca desejou que a propriedade `Secret` fosse definida com a página Criar.

<a name="vm"></a>

### <a name="view-model"></a>Modelo de exibição

Um modelo de exibição normalmente contém um subconjunto das propriedades incluídas no modelo usado pelo aplicativo. O modelo de aplicativo costuma ser chamado de modelo de domínio. O modelo de domínio normalmente contém todas as propriedades necessárias para a entidade correspondente no BD. O modelo de exibição contém apenas as propriedades necessárias para a camada de interface do usuário (por exemplo, a página Criar). Além do modelo de exibição, alguns aplicativos usam um modelo de associação ou modelo de entrada para passar dados entre a classe de modelo de página das Páginas do Razor e o navegador. Considere o seguinte modelo de exibição `Student`:

[!code-csharp[](intro/samples/cu21/Models/StudentVM.cs)]

Os modelos de exibição fornecem uma maneira alternativa para impedir o excesso de postagem. O modelo de exibição contém apenas as propriedades a serem exibidas ou atualizadas.

O seguinte código usa o modelo de exibição `StudentVM` para criar um novo aluno:

[!code-csharp[](intro/samples/cu21/Pages/Students/CreateVM.cshtml.cs?name=snippet_OnPostAsync)]

O método [SetValues](/dotnet/api/microsoft.entityframeworkcore.changetracking.propertyvalues.setvalues#Microsoft_EntityFrameworkCore_ChangeTracking_PropertyValues_SetValues_System_Object_) define os valores desse objeto lendo os valores de outro objeto [PropertyValues](/dotnet/api/microsoft.entityframeworkcore.changetracking.propertyvalues). `SetValues` usa a correspondência de nomes de propriedade. O tipo de modelo de exibição não precisa estar relacionado ao tipo de modelo, apenas precisa ter as propriedades correspondentes.

O uso de `StudentVM` exige a atualização de [CreateVM.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu21/Pages/Students/CreateVM.cshtml) para usar `StudentVM` em vez de `Student`.

Nas Páginas do Razor, a classe derivada `PageModel` é o modelo de exibição.

## <a name="update-the-edit-page"></a>Atualizar a página Editar

Atualize o modelo de página para a página de edição. As alterações principais são realçadas:

[!code-csharp[](intro/samples/cu21/Pages/Students/Edit.cshtml.cs?name=snippet_OnPostAsync&highlight=20,36)]

As alterações de código são semelhantes à página Criar, com algumas exceções:

* `OnPostAsync` tem um parâmetro `id` opcional.
* O aluno atual é buscado do BD, em vez de criar um aluno vazio.
* `FirstOrDefaultAsync` foi substituído por [FindAsync](/dotnet/api/microsoft.entityframeworkcore.dbset-1.findasync). `FindAsync` é uma boa opção ao selecionar uma entidade da chave primária. Consulte [FindAsync](#FindAsync) para obter mais informações.

### <a name="test-the-edit-and-create-pages"></a>Testar as páginas Editar e Criar

Crie e edite algumas entidades de aluno.

## <a name="entity-states"></a>Estados da entidade

O contexto de BD controla se as entidades em memória estão em sincronia com suas linhas correspondentes no BD. As informações de sincronização de contexto do BD determinam o que acontece quando [SaveChangesAsync](/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechangesasync#Microsoft_EntityFrameworkCore_DbContext_SaveChangesAsync_System_Threading_CancellationToken_) é chamado. Por exemplo, quando uma nova entidade é passada para o método [AddAsync](/dotnet/api/microsoft.entityframeworkcore.dbcontext.addasync), o estado da entidade é definido como [Added](/dotnet/api/microsoft.entityframeworkcore.entitystate#Microsoft_EntityFrameworkCore_EntityState_Added). Quando `SaveChangesAsync` é chamado, o contexto de BD emite um comando SQL INSERT.

Uma entidade pode estar em um dos [seguintes estados](/dotnet/api/microsoft.entityframeworkcore.entitystate):

* `Added`: a entidade ainda não existe no BD. O método `SaveChanges` emite uma instrução INSERT.

* `Unchanged`: nenhuma alteração precisa ser salva com essa entidade. Uma entidade tem esse status quando é lida do BD.

* `Modified`: Alguns ou todos os valores de propriedade da entidade foram modificados. O método `SaveChanges` emite uma instrução UPDATE.

* `Deleted`: A entidade foi marcada para exclusão. O método `SaveChanges` emite uma instrução DELETE.

* `Detached`: a entidade não está sendo controlada pelo contexto de BD.

Em um aplicativo da área de trabalho, em geral, as alterações de estado são definidas automaticamente. Uma entidade é lida, as alterações são feitas e o estado da entidade é alterado automaticamente para `Modified`. A chamada a `SaveChanges` gera uma instrução SQL UPDATE que atualiza apenas as propriedades alteradas.

Em um aplicativo Web, o `DbContext` que lê uma entidade e exibe os dados é descartado depois que uma página é renderizada. Quando o método `OnPostAsync` de uma página é chamado, é feita uma nova solicitação da Web e com uma nova instância do `DbContext`. A nova leitura da entidade nesse novo contexto simula o processamento da área de trabalho.

## <a name="update-the-delete-page"></a>Atualizar a página Excluir

Nesta seção, o código é adicionado para implementar uma mensagem de erro personalizada quando há falha na chamada a `SaveChanges`. Adicione uma cadeia de caracteres para que ela contenha as possíveis mensagens de erro:

[!code-csharp[](intro/samples/cu21/Pages/Students/Delete.cshtml.cs?name=snippet1&highlight=12)]

Substitua o método `OnGetAsync` pelo seguinte código:

[!code-csharp[](intro/samples/cu21/Pages/Students/Delete.cshtml.cs?name=snippet_OnGetAsync&highlight=1,9,17-20)]

O código anterior contém o parâmetro opcional `saveChangesError`. `saveChangesError` indica se o método foi chamado após uma falha ao excluir o objeto de aluno. A operação de exclusão pode falhar devido a problemas de rede temporários. Erros de rede transitórios serão mais prováveis de ocorrerem na nuvem. `saveChangesError` é falso quando a página Excluir `OnGetAsync` é chamada na interface do usuário. Quando `OnGetAsync` é chamado por `OnPostAsync` (devido à falha da operação de exclusão), o parâmetro `saveChangesError` é verdadeiro.

### <a name="the-delete-pages-onpostasync-method"></a>O método OnPostAsync nas páginas Excluir

Substitua `OnPostAsync` pelo seguinte código:

[!code-csharp[](intro/samples/cu21/Pages/Students/Delete.cshtml.cs?name=snippet_OnPostAsync)]

O código anterior recupera a entidade selecionada e, em seguida, chama o método [Remove](/dotnet/api/microsoft.entityframeworkcore.dbcontext.remove#Microsoft_EntityFrameworkCore_DbContext_Remove_System_Object_) para definir o status da entidade como `Deleted`. Quando `SaveChanges` é chamado, um comando SQL DELETE é gerado. Se `Remove` falhar:

* A exceção de BD é capturada.
* O método `OnGetAsync` das páginas Excluir é chamado com `saveChangesError=true`.

### <a name="update-the-delete-razor-page"></a>Atualizar a Página Excluir do Razor

Adicione a mensagem de erro realçada a seguir à Página Excluir do Razor.
<!--
[!code-cshtml[](intro/samples/cu21/Pages/Students/Delete.cshtml?name=snippet&highlight=11)]
-->
[!code-cshtml[](intro/samples/cu21/Pages/Students/Delete.cshtml?range=1-13&highlight=10)]

Exclusão de teste.

## <a name="common-errors"></a>Erros comuns

Alunos/Índice ou outros links não funcionam:

Verifique se a Página do Razor contém a diretiva `@page` correta. Por exemplo, a Razor Page Alunos/Índice **não** deve conter um modelo de rota:

```cshtml
@page "{id:int}"
```

Cada Página do Razor deve incluir a diretiva `@page`.

::: moniker-end

> [!div class="step-by-step"]
> [Anterior](xref:data/ef-rp/intro)
> [Próximo](xref:data/ef-rp/sort-filter-page)
