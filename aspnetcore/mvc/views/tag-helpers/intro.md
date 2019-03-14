---
title: Auxiliares de Marca no ASP.NET Core
author: rick-anderson
description: Saiba o que são Auxiliares de Marca e como usá-los no ASP.NET Core.
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2018
uid: mvc/views/tag-helpers/intro
ms.openlocfilehash: 4b9bceb3ce0153af2d9a30c402febe09707145b7
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041233"
---
# <a name="tag-helpers-in-aspnet-core"></a><span data-ttu-id="bbb64-103">Auxiliares de Marca no ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="bbb64-103">Tag Helpers in ASP.NET Core</span></span>

<span data-ttu-id="bbb64-104">Por [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="bbb64-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="what-are-tag-helpers"></a><span data-ttu-id="bbb64-105">E que são Auxiliares de Marca?</span><span class="sxs-lookup"><span data-stu-id="bbb64-105">What are Tag Helpers?</span></span>

<span data-ttu-id="bbb64-106">Os Auxiliares de Marca permitem que o código do lado do servidor participe da criação e renderização de elementos HTML em arquivos do Razor.</span><span class="sxs-lookup"><span data-stu-id="bbb64-106">Tag Helpers enable server-side code to participate in creating and rendering HTML elements in Razor files.</span></span> <span data-ttu-id="bbb64-107">Por exemplo, o `ImageTagHelper` interno pode acrescentar um número de versão ao nome da imagem.</span><span class="sxs-lookup"><span data-stu-id="bbb64-107">For example, the built-in `ImageTagHelper` can append a version number to the image name.</span></span> <span data-ttu-id="bbb64-108">Sempre que a imagem é alterada, o servidor gera uma nova versão exclusiva para a imagem, de modo que os clientes tenham a garantia de obter a imagem atual (em vez de uma imagem obsoleta armazenada em cache).</span><span class="sxs-lookup"><span data-stu-id="bbb64-108">Whenever the image changes, the server generates a new unique version for the image, so clients are guaranteed to get the current image (instead of a stale cached image).</span></span> <span data-ttu-id="bbb64-109">Há muitos Auxiliares de Marca internos para tarefas comuns – como criação de formulários, links, carregamento de ativos e muito mais – e ainda outros disponíveis em repositórios GitHub públicos e como NuGet.</span><span class="sxs-lookup"><span data-stu-id="bbb64-109">There are many built-in Tag Helpers for common tasks - such as creating forms, links, loading assets and more - and even more available in public GitHub repositories and as NuGet packages.</span></span> <span data-ttu-id="bbb64-110">Os Auxiliares de Marca são criados no C# e são direcionados a elementos HTML de acordo com o nome do elemento, o nome do atributo ou a marca pai.</span><span class="sxs-lookup"><span data-stu-id="bbb64-110">Tag Helpers are authored in C#, and they target HTML elements based on element name, attribute name, or parent tag.</span></span> <span data-ttu-id="bbb64-111">Por exemplo, o `LabelTagHelper` interno pode ser direcionado ao elemento `<label>` HTML quando os atributos `LabelTagHelper` são aplicados.</span><span class="sxs-lookup"><span data-stu-id="bbb64-111">For example, the built-in `LabelTagHelper` can target the HTML `<label>` element when the `LabelTagHelper` attributes are applied.</span></span> <span data-ttu-id="bbb64-112">Se você está familiarizado com [Auxiliares HTML](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers), os Auxiliares de Marca reduzem as transições explícitas entre HTML e C# em exibições do Razor.</span><span class="sxs-lookup"><span data-stu-id="bbb64-112">If you're familiar with [HTML Helpers](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers), Tag Helpers reduce the explicit transitions between HTML and C# in Razor views.</span></span> <span data-ttu-id="bbb64-113">Em muitos casos, os Auxiliares HTML fornecem uma abordagem alternativa a um Auxiliar de Marca específico, mas é importante reconhecer que os Auxiliares de Marca não substituem os Auxiliares HTML e que não há um Auxiliar de Marca para cada Auxiliar HTML.</span><span class="sxs-lookup"><span data-stu-id="bbb64-113">In many cases, HTML Helpers provide an alternative approach to a specific Tag Helper, but it's important to recognize that Tag Helpers don't replace HTML Helpers and there's not a Tag Helper for each HTML Helper.</span></span> <span data-ttu-id="bbb64-114">[Comparação entre Auxiliares de Marca e Auxiliares HTML](#tag-helpers-compared-to-html-helpers) explica as diferenças mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="bbb64-114">[Tag Helpers compared to HTML Helpers](#tag-helpers-compared-to-html-helpers) explains the differences in more detail.</span></span>

## <a name="what-tag-helpers-provide"></a><span data-ttu-id="bbb64-115">O que os Auxiliares de Marca fornecem</span><span class="sxs-lookup"><span data-stu-id="bbb64-115">What Tag Helpers provide</span></span>

<span data-ttu-id="bbb64-116">**Uma experiência de desenvolvimento amigável a HTML** Na maioria dos casos, a marcação do Razor com Auxiliares de Marca parece um HTML padrão.</span><span class="sxs-lookup"><span data-stu-id="bbb64-116">**An HTML-friendly development experience** For the most part, Razor markup using Tag Helpers looks like standard HTML.</span></span> <span data-ttu-id="bbb64-117">Designers de front-end familiarizados com HTML/CSS/JavaScript podem editar o Razor sem aprender a sintaxe Razor do C#.</span><span class="sxs-lookup"><span data-stu-id="bbb64-117">Front-end designers conversant with HTML/CSS/JavaScript can edit Razor without learning C# Razor syntax.</span></span>

<span data-ttu-id="bbb64-118">**Um ambiente avançado do IntelliSense para criação do HTML e da marcação do Razor** Isso é um nítido contraste com Auxiliares HTML, a abordagem anterior para a criação do lado do servidor de marcação nas exibições do Razor.</span><span class="sxs-lookup"><span data-stu-id="bbb64-118">**A rich IntelliSense environment for creating HTML and Razor markup** This is in sharp contrast to HTML Helpers, the previous approach to server-side creation of markup in Razor views.</span></span> <span data-ttu-id="bbb64-119">[Comparação entre Auxiliares de Marca e Auxiliares HTML](#tag-helpers-compared-to-html-helpers) explica as diferenças mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="bbb64-119">[Tag Helpers compared to HTML Helpers](#tag-helpers-compared-to-html-helpers) explains the differences in more detail.</span></span> <span data-ttu-id="bbb64-120">[Suporte do IntelliSense para Auxiliares de Marca](#intellisense-support-for-tag-helpers) explica o ambiente do IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="bbb64-120">[IntelliSense support for Tag Helpers](#intellisense-support-for-tag-helpers) explains the IntelliSense environment.</span></span> <span data-ttu-id="bbb64-121">Até mesmo desenvolvedores experientes com a sintaxe Razor do C# são mais produtivos usando Auxiliares de Marca do que escrevendo a marcação do Razor do C#.</span><span class="sxs-lookup"><span data-stu-id="bbb64-121">Even developers experienced with Razor C# syntax are more productive using Tag Helpers than writing C# Razor markup.</span></span>

<span data-ttu-id="bbb64-122">**Uma maneira de fazer com que você fique mais produtivo e possa produzir um código mais robusto, confiável e possível de ser mantido usando as informações apenas disponíveis no servidor** Por exemplo, historicamente, o mantra da atualização de imagens era alterar o nome da imagem quando a imagem era alterada.</span><span class="sxs-lookup"><span data-stu-id="bbb64-122">**A way to make you more productive and able to produce more robust, reliable, and maintainable code using information only available on the server** For example, historically the mantra on updating images was to change the name of the image when you change the image.</span></span> <span data-ttu-id="bbb64-123">As imagens devem ser armazenadas em cache de forma agressiva por motivos de desempenho e, a menos que você altere o nome de uma imagem, você corre o risco de os clientes obterem uma cópia obsoleta.</span><span class="sxs-lookup"><span data-stu-id="bbb64-123">Images should be aggressively cached for performance reasons, and unless you change the name of an image, you risk clients getting a stale copy.</span></span> <span data-ttu-id="bbb64-124">Historicamente, depois que uma imagem era editada, o nome precisava ser alterado e cada referência à imagem no aplicativo Web precisava ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="bbb64-124">Historically, after an image was edited, the name had to be changed and each reference to the image in the web app needed to be updated.</span></span> <span data-ttu-id="bbb64-125">Não apenas isso exige muito trabalho, mas também é propenso a erros (você pode perder uma referência, inserir a cadeia de caracteres incorreta acidentalmente, etc.) O `ImageTagHelper` interno pode fazer isso para você automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bbb64-125">Not only is this very labor intensive, it's also error prone (you could miss a reference, accidentally enter the wrong string, etc.) The built-in `ImageTagHelper` can do this for you automatically.</span></span> <span data-ttu-id="bbb64-126">O `ImageTagHelper` pode acrescentar um número de versão ao nome da imagem, de modo que sempre que a imagem é alterada, o servidor gera automaticamente uma nova versão exclusiva para a imagem.</span><span class="sxs-lookup"><span data-stu-id="bbb64-126">The `ImageTagHelper` can append a version number to the image name, so whenever the image changes, the server automatically generates a new unique version for the image.</span></span> <span data-ttu-id="bbb64-127">Os clientes têm a garantia de obter a imagem atual.</span><span class="sxs-lookup"><span data-stu-id="bbb64-127">Clients are guaranteed to get the current image.</span></span> <span data-ttu-id="bbb64-128">Basicamente, essa economia na robustez e no trabalho é obtida gratuitamente com o `ImageTagHelper`.</span><span class="sxs-lookup"><span data-stu-id="bbb64-128">This robustness and labor savings comes essentially free by using the `ImageTagHelper`.</span></span>

<span data-ttu-id="bbb64-129">A maioria dos auxiliares de marca internos é direcionada a elementos HTML padrão e fornece atributos do lado do servidor para o elemento.</span><span class="sxs-lookup"><span data-stu-id="bbb64-129">Most built-in Tag Helpers target standard HTML elements and provide server-side attributes for the element.</span></span> <span data-ttu-id="bbb64-130">Por exemplo, o elemento `<input>` usado em várias exibições na pasta *Exibição/Conta* contém o atributo `asp-for`.</span><span class="sxs-lookup"><span data-stu-id="bbb64-130">For example, the `<input>` element used in many views in the *Views/Account* folder contains the `asp-for` attribute.</span></span> <span data-ttu-id="bbb64-131">Esse atributo extrai o nome da propriedade do modelo especificado no HTML renderizado.</span><span class="sxs-lookup"><span data-stu-id="bbb64-131">This attribute extracts the name of the specified model property into the rendered HTML.</span></span> <span data-ttu-id="bbb64-132">Considere uma exibição Razor com o seguinte modelo:</span><span class="sxs-lookup"><span data-stu-id="bbb64-132">Consider a Razor view with the following model:</span></span>

```csharp
public class Movie
{
    public int ID { get; set; }
    public string Title { get; set; }
    public DateTime ReleaseDate { get; set; }
    public string Genre { get; set; }
    public decimal Price { get; set; }
}
```

<span data-ttu-id="bbb64-133">A seguinte marcação do Razor:</span><span class="sxs-lookup"><span data-stu-id="bbb64-133">The following Razor markup:</span></span>

```cshtml
<label asp-for="Movie.Title"></label>
```

<span data-ttu-id="bbb64-134">Gera o seguinte HTML:</span><span class="sxs-lookup"><span data-stu-id="bbb64-134">Generates the following HTML:</span></span>

```html
<label for="Movie_Title">Title</label>
```

<span data-ttu-id="bbb64-135">O atributo `asp-for` é disponibilizado pela propriedade `For` no [LabelTagHelper](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.labeltaghelper?view=aspnetcore-2.0).</span><span class="sxs-lookup"><span data-stu-id="bbb64-135">The `asp-for` attribute is made available by the `For` property in the [LabelTagHelper](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.labeltaghelper?view=aspnetcore-2.0).</span></span> <span data-ttu-id="bbb64-136">Confira [Auxiliares de marca de autor](xref:mvc/views/tag-helpers/authoring) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="bbb64-136">See [Author Tag Helpers](xref:mvc/views/tag-helpers/authoring) for more information.</span></span>

## <a name="managing-tag-helper-scope"></a><span data-ttu-id="bbb64-137">Gerenciando o escopo do Auxiliar de Marca</span><span class="sxs-lookup"><span data-stu-id="bbb64-137">Managing Tag Helper scope</span></span>

<span data-ttu-id="bbb64-138">O escopo dos Auxiliares de Marca é controlado por uma combinação de `@addTagHelper`, `@removeTagHelper` e o caractere de recusa "!".</span><span class="sxs-lookup"><span data-stu-id="bbb64-138">Tag Helpers scope is controlled by a combination of `@addTagHelper`, `@removeTagHelper`, and the "!" opt-out character.</span></span>

<a name="add-helper-label"></a>

### <a name="addtaghelper-makes-tag-helpers-available"></a><span data-ttu-id="bbb64-139">`@addTagHelper` disponibiliza os Auxiliares de Marca</span><span class="sxs-lookup"><span data-stu-id="bbb64-139">`@addTagHelper` makes Tag Helpers available</span></span>

<span data-ttu-id="bbb64-140">Se você criar um novo aplicativo Web ASP.NET Core chamado *AuthoringTagHelpers*, o seguinte arquivo *Views/_ViewImports.cshtml* será adicionado ao projeto:</span><span class="sxs-lookup"><span data-stu-id="bbb64-140">If you create a new ASP.NET Core web app named *AuthoringTagHelpers*, the following *Views/_ViewImports.cshtml* file will be added to your project:</span></span>

[!code-cshtml[](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/_ViewImportsCopy.cshtml?highlight=2&range=2-3)]

<span data-ttu-id="bbb64-141">A diretiva `@addTagHelper` disponibiliza os Auxiliares de Marca para a exibição.</span><span class="sxs-lookup"><span data-stu-id="bbb64-141">The `@addTagHelper` directive makes Tag Helpers available to the view.</span></span> <span data-ttu-id="bbb64-142">Nesse caso, o arquivo de exibição é *Pages/_ViewImports.cshtml*, que é herdado por padrão por todos os arquivos na pasta *Páginas* e suas subpastas, disponibilizando os Auxiliares de Marca.</span><span class="sxs-lookup"><span data-stu-id="bbb64-142">In this case, the view file is *Pages/_ViewImports.cshtml*, which by default is inherited by all files in the *Pages* folder and subfolders; making Tag Helpers available.</span></span> <span data-ttu-id="bbb64-143">O código acima usa a sintaxe de curinga ("\*") para especificar que todos os Auxiliares de Marca no assembly especificado (*Microsoft.AspNetCore.Mvc.TagHelpers*) estarão disponíveis para todos os arquivos de exibição no diretório *Views* ou subdiretório.</span><span class="sxs-lookup"><span data-stu-id="bbb64-143">The code above uses the wildcard syntax ("\*") to specify that all Tag Helpers in the specified assembly (*Microsoft.AspNetCore.Mvc.TagHelpers*) will be available to every view file in the *Views* directory or subdirectory.</span></span> <span data-ttu-id="bbb64-144">O primeiro parâmetro após `@addTagHelper` especifica os Auxiliares de Marca a serem carregados (estamos usando "\*" para todos os Auxiliares de Marca) e o segundo parâmetro "Microsoft.AspNetCore.Mvc.TagHelpers" especifica o assembly que contém os Auxiliares de Marca.</span><span class="sxs-lookup"><span data-stu-id="bbb64-144">The first parameter after `@addTagHelper` specifies the Tag Helpers to load (we are using "\*" for all Tag Helpers), and the second parameter "Microsoft.AspNetCore.Mvc.TagHelpers" specifies the assembly containing the Tag Helpers.</span></span> <span data-ttu-id="bbb64-145">*Microsoft.AspNetCore.Mvc.TagHelpers* é o assembly para os Auxiliares de Marca internos do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="bbb64-145">*Microsoft.AspNetCore.Mvc.TagHelpers* is the assembly for the built-in ASP.NET Core Tag Helpers.</span></span>

<span data-ttu-id="bbb64-146">Para expor todos os Auxiliares de Marca neste projeto (que cria um assembly chamado *AuthoringTagHelpers*), você usará o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bbb64-146">To expose all of the Tag Helpers in this project (which creates an assembly named *AuthoringTagHelpers*), you would use the following:</span></span>

[!code-cshtml[](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/_ViewImportsCopy.cshtml?highlight=3)]

<span data-ttu-id="bbb64-147">Se o projeto contém um `EmailTagHelper` com o namespace padrão (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`), forneça o FQN ( nome totalmente qualificado) do Auxiliar de Marca:</span><span class="sxs-lookup"><span data-stu-id="bbb64-147">If your project contains an `EmailTagHelper` with the default namespace (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`), you can provide the fully qualified name (FQN) of the Tag Helper:</span></span>

```cshtml
@using AuthoringTagHelpers
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
@addTagHelper AuthoringTagHelpers.TagHelpers.EmailTagHelper, AuthoringTagHelpers
```

<span data-ttu-id="bbb64-148">Para adicionar um Auxiliar de Marca a uma exibição usando um FQN, primeiro adicione o FQN (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`) e, em seguida, o nome do assembly (*AuthoringTagHelpers*).</span><span class="sxs-lookup"><span data-stu-id="bbb64-148">To add a Tag Helper to a view using an FQN, you first add the FQN (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`), and then the assembly name (*AuthoringTagHelpers*).</span></span> <span data-ttu-id="bbb64-149">A maioria dos desenvolvedores prefere usar a sintaxe de curinga "\*".</span><span class="sxs-lookup"><span data-stu-id="bbb64-149">Most developers prefer to use the  "\*" wildcard syntax.</span></span> <span data-ttu-id="bbb64-150">A sintaxe de curinga permite que você insira o caractere curinga "\*" como o sufixo de um FQN.</span><span class="sxs-lookup"><span data-stu-id="bbb64-150">The wildcard syntax allows you to insert the wildcard character "\*" as the suffix in an FQN.</span></span> <span data-ttu-id="bbb64-151">Por exemplo, uma das seguintes diretivas exibirá o `EmailTagHelper`:</span><span class="sxs-lookup"><span data-stu-id="bbb64-151">For example, any of the following directives will bring in the `EmailTagHelper`:</span></span>

```cshtml
@addTagHelper AuthoringTagHelpers.TagHelpers.E*, AuthoringTagHelpers
@addTagHelper AuthoringTagHelpers.TagHelpers.Email*, AuthoringTagHelpers
```

<span data-ttu-id="bbb64-152">Conforme mencionado anteriormente, a adição da diretiva `@addTagHelper` ao arquivo *Views/_ViewImports.cshtml* disponibiliza o Auxiliar de Marca para todos os arquivos de exibição no diretório *Views* e subdiretórios.</span><span class="sxs-lookup"><span data-stu-id="bbb64-152">As mentioned previously, adding the `@addTagHelper` directive to the *Views/_ViewImports.cshtml* file makes the Tag Helper available to all view files in the *Views* directory and subdirectories.</span></span> <span data-ttu-id="bbb64-153">Use a diretiva `@addTagHelper` nos arquivos de exibição específicos se você deseja aceitar a exposição do Auxiliar de Marca a apenas essas exibições.</span><span class="sxs-lookup"><span data-stu-id="bbb64-153">You can use the `@addTagHelper` directive in specific view files if you want to opt-in to exposing the Tag Helper to only those views.</span></span>

<a name="remove-razor-directives-label"></a>

### <a name="removetaghelper-removes-tag-helpers"></a><span data-ttu-id="bbb64-154">`@removeTagHelper` remove os Auxiliares de Marca</span><span class="sxs-lookup"><span data-stu-id="bbb64-154">`@removeTagHelper` removes Tag Helpers</span></span>

<span data-ttu-id="bbb64-155">O `@removeTagHelper` tem os mesmos dois parâmetros `@addTagHelper` e remove um Auxiliar de Marca adicionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bbb64-155">The `@removeTagHelper` has the same two parameters as `@addTagHelper`, and it removes a Tag Helper that was previously added.</span></span> <span data-ttu-id="bbb64-156">Por exemplo, `@removeTagHelper` aplicado a uma exibição específica remove o Auxiliar de Marca especificado da exibição.</span><span class="sxs-lookup"><span data-stu-id="bbb64-156">For example, `@removeTagHelper` applied to a specific view removes the specified Tag Helper from the view.</span></span> <span data-ttu-id="bbb64-157">O uso de `@removeTagHelper` em um arquivo *Views/Folder/_ViewImports.cshtml* remove o Auxiliar de Marca especificado de todas as exibições em *Folder*.</span><span class="sxs-lookup"><span data-stu-id="bbb64-157">Using `@removeTagHelper` in a *Views/Folder/_ViewImports.cshtml* file removes the specified Tag Helper from all of the views in *Folder*.</span></span>

### <a name="controlling-tag-helper-scope-with-the-viewimportscshtml-file"></a><span data-ttu-id="bbb64-158">Controlando o escopo do Auxiliar de Marca com o arquivo *_ViewImports.cshtml*</span><span class="sxs-lookup"><span data-stu-id="bbb64-158">Controlling Tag Helper scope with the *_ViewImports.cshtml* file</span></span>

<span data-ttu-id="bbb64-159">Adicione um *_ViewImports.cshtml* a qualquer pasta de exibição e o mecanismo de exibição aplicará as diretivas desse arquivo e do arquivo *Views/_ViewImports.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="bbb64-159">You can add a *_ViewImports.cshtml* to any view folder, and the view engine applies the directives from both that file and the *Views/_ViewImports.cshtml* file.</span></span> <span data-ttu-id="bbb64-160">Se você adicionou um arquivo *Views/Home/_ViewImports.cshtml* vazio às exibições *Home*, não haverá nenhuma alteração porque o arquivo *_ViewImports.cshtml* é aditivo.</span><span class="sxs-lookup"><span data-stu-id="bbb64-160">If you added an empty *Views/Home/_ViewImports.cshtml* file for the *Home* views, there would be no change because the *_ViewImports.cshtml* file is additive.</span></span> <span data-ttu-id="bbb64-161">As diretivas `@addTagHelper` que você adicionar ao arquivo *Views/Home/_ViewImports.cshtml* (que não estão no arquivo *Views/_ViewImports.cshtml* padrão) exporão os Auxiliares de Marca às exibições somente na pasta *Home*.</span><span class="sxs-lookup"><span data-stu-id="bbb64-161">Any `@addTagHelper` directives you add to the *Views/Home/_ViewImports.cshtml* file (that are not in the default *Views/_ViewImports.cshtml* file) would expose those Tag Helpers to views only in the *Home* folder.</span></span>

<a name="opt-out"></a>

### <a name="opting-out-of-individual-elements"></a><span data-ttu-id="bbb64-162">Recusando elementos individuais</span><span class="sxs-lookup"><span data-stu-id="bbb64-162">Opting out of individual elements</span></span>

<span data-ttu-id="bbb64-163">Desabilite um Auxiliar de Marca no nível do elemento com o caractere de recusa do Auxiliar de Marca ("!").</span><span class="sxs-lookup"><span data-stu-id="bbb64-163">You can disable a Tag Helper at the element level with the Tag Helper opt-out character ("!").</span></span> <span data-ttu-id="bbb64-164">Por exemplo, a validação `Email` está desabilitada no `<span>` com o caractere de recusa do Auxiliar de Marca:</span><span class="sxs-lookup"><span data-stu-id="bbb64-164">For example, `Email` validation is disabled in the `<span>` with the Tag Helper opt-out character:</span></span>

```cshtml
<!span asp-validation-for="Email" class="text-danger"></!span>
```

<span data-ttu-id="bbb64-165">É necessário aplicar o caractere de recusa do Auxiliar de Marca à marca de abertura e fechamento.</span><span class="sxs-lookup"><span data-stu-id="bbb64-165">You must apply the Tag Helper opt-out character to the opening and closing tag.</span></span> <span data-ttu-id="bbb64-166">(O editor do Visual Studio adiciona automaticamente o caractere de recusa à marca de fechamento quando um é adicionado à marca de abertura).</span><span class="sxs-lookup"><span data-stu-id="bbb64-166">(The Visual Studio editor automatically adds the opt-out character to the closing tag when you add one to the opening tag).</span></span> <span data-ttu-id="bbb64-167">Depois de adicionar o caractere de recusa, o elemento e os atributos do Auxiliar de Marca deixam de ser exibidos em uma fonte diferenciada.</span><span class="sxs-lookup"><span data-stu-id="bbb64-167">After you add the opt-out character, the element and Tag Helper attributes are no longer displayed in a distinctive font.</span></span>

<a name="prefix-razor-directives-label"></a>

### <a name="using-taghelperprefix-to-make-tag-helper-usage-explicit"></a><span data-ttu-id="bbb64-168">Usando `@tagHelperPrefix` para tornar explícito o uso do Auxiliar de Marca</span><span class="sxs-lookup"><span data-stu-id="bbb64-168">Using `@tagHelperPrefix` to make Tag Helper usage explicit</span></span>

<span data-ttu-id="bbb64-169">A diretiva `@tagHelperPrefix` permite que você especifique uma cadeia de caracteres de prefixo de marca para habilitar o suporte do Auxiliar de Marca e tornar explícito o uso do Auxiliar de Marca.</span><span class="sxs-lookup"><span data-stu-id="bbb64-169">The `@tagHelperPrefix` directive allows you to specify a tag prefix string to enable Tag Helper support and to make Tag Helper usage explicit.</span></span> <span data-ttu-id="bbb64-170">Por exemplo, você pode adicionar a seguinte marcação ao arquivo *Views/_ViewImports.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="bbb64-170">For example, you could add the following markup to the *Views/_ViewImports.cshtml* file:</span></span>

```cshtml
@tagHelperPrefix th:
```
<span data-ttu-id="bbb64-171">Na imagem do código abaixo, o prefixo do Auxiliar de Marca é definido como `th:`; portanto, somente esses elementos que usam o prefixo `th:` dão suporte a Auxiliares de Marca (elementos habilitados para Auxiliar de Marca têm uma fonte diferenciada).</span><span class="sxs-lookup"><span data-stu-id="bbb64-171">In the code image below, the Tag Helper prefix is set to `th:`, so only those elements using the prefix `th:` support Tag Helpers (Tag Helper-enabled elements have a distinctive font).</span></span> <span data-ttu-id="bbb64-172">Os elementos `<label>` e `<input>` têm o prefixo do Auxiliar de Marca e são habilitados para Auxiliar de Marca, ao contrário do elemento `<span>`.</span><span class="sxs-lookup"><span data-stu-id="bbb64-172">The `<label>` and `<input>` elements have the Tag Helper prefix and are Tag Helper-enabled, while the `<span>` element doesn't.</span></span>

![imagem](intro/_static/thp.png)

<span data-ttu-id="bbb64-174">As mesmas regras de hierarquia que se aplicam a `@addTagHelper` também se aplicam a `@tagHelperPrefix`.</span><span class="sxs-lookup"><span data-stu-id="bbb64-174">The same hierarchy rules that apply to `@addTagHelper` also apply to `@tagHelperPrefix`.</span></span>

## <a name="self-closing-tag-helpers"></a><span data-ttu-id="bbb64-175">Auxiliares de Marca com autofechamento</span><span class="sxs-lookup"><span data-stu-id="bbb64-175">Self-closing Tag Helpers</span></span>

<span data-ttu-id="bbb64-176">Muitos Auxiliares de Marca não podem ser usados como marcações com autofechamento.</span><span class="sxs-lookup"><span data-stu-id="bbb64-176">Many Tag Helpers can't be used as self-closing tags.</span></span> <span data-ttu-id="bbb64-177">Alguns Auxiliares de Marca são projetados para serem marcações com autofechamento.</span><span class="sxs-lookup"><span data-stu-id="bbb64-177">Some Tag Helpers are designed to be self-closing tags.</span></span> <span data-ttu-id="bbb64-178">Usar um Auxiliar de Marca que não foi projetado para ser de autofechamento suprime a saída renderizada.</span><span class="sxs-lookup"><span data-stu-id="bbb64-178">Using a Tag Helper that was not designed to be self-closing suppresses the rendered output.</span></span> <span data-ttu-id="bbb64-179">Um Auxiliar de Marca com autofechamento resulta em uma marca com autofechamento na saída renderizada.</span><span class="sxs-lookup"><span data-stu-id="bbb64-179">Self-closing a Tag Helper results in a self-closing tag in the rendered output.</span></span> <span data-ttu-id="bbb64-180">Para obter mais informações, confira [esta observação](xref:mvc/views/tag-helpers/authoring#self-closing) em [Criando Auxiliares de Marca](xref:mvc/views/tag-helpers/authoring).</span><span class="sxs-lookup"><span data-stu-id="bbb64-180">For more information, see [this note](xref:mvc/views/tag-helpers/authoring#self-closing) in [Authoring Tag Helpers](xref:mvc/views/tag-helpers/authoring).</span></span>

## <a name="intellisense-support-for-tag-helpers"></a><span data-ttu-id="bbb64-181">Suporte do IntelliSense para Auxiliares de Marca</span><span class="sxs-lookup"><span data-stu-id="bbb64-181">IntelliSense support for Tag Helpers</span></span>

<span data-ttu-id="bbb64-182">Quando você cria um novo aplicativo Web ASP.NET Core no Visual Studio, ele adiciona o pacote NuGet "Microsoft.AspNetCore.Razor.Tools".</span><span class="sxs-lookup"><span data-stu-id="bbb64-182">When you create a new ASP.NET Core web app in Visual Studio, it adds the NuGet package "Microsoft.AspNetCore.Razor.Tools".</span></span> <span data-ttu-id="bbb64-183">Esse é o pacote que adiciona ferramentas do Auxiliar de Marca.</span><span class="sxs-lookup"><span data-stu-id="bbb64-183">This is the package that adds Tag Helper tooling.</span></span>

<span data-ttu-id="bbb64-184">Considere a escrita de um elemento `<label>` HTML.</span><span class="sxs-lookup"><span data-stu-id="bbb64-184">Consider writing an HTML `<label>` element.</span></span> <span data-ttu-id="bbb64-185">Assim que você insere `<l` no editor do Visual Studio, o IntelliSense exibe elementos correspondentes:</span><span class="sxs-lookup"><span data-stu-id="bbb64-185">As soon as you enter `<l` in the Visual Studio editor, IntelliSense displays matching elements:</span></span>

![imagem](intro/_static/label.png)

<span data-ttu-id="bbb64-187">Não só você obtém a ajuda do HTML, mas também o ícone (o "@" symbol with "<>" abaixo dele).</span><span class="sxs-lookup"><span data-stu-id="bbb64-187">Not only do you get HTML help, but the icon (the "@" symbol with "<>" under it).</span></span>

![imagem](intro/_static/tagSym.png)

<span data-ttu-id="bbb64-189">identifica o elemento como direcionado a Auxiliares de Marca.</span><span class="sxs-lookup"><span data-stu-id="bbb64-189">identifies the element as targeted by Tag Helpers.</span></span> <span data-ttu-id="bbb64-190">Elementos HTML puros (como o `fieldset`) exibem o ícone "<>".</span><span class="sxs-lookup"><span data-stu-id="bbb64-190">Pure HTML elements (such as the `fieldset`) display the "<>" icon.</span></span>

<span data-ttu-id="bbb64-191">Uma marca `<label>` HTML pura exibe a marca HTML (com o tema de cores padrão do Visual Studio) em uma fonte marrom, os atributos em vermelho e os valores de atributo em azul.</span><span class="sxs-lookup"><span data-stu-id="bbb64-191">A pure HTML `<label>` tag displays the HTML tag (with the default Visual Studio color theme) in a brown font, the attributes in red, and the attribute values in blue.</span></span>

![imagem](intro/_static/LableHtmlTag.png)

<span data-ttu-id="bbb64-193">Depois de inserir `<label`, o IntelliSense lista os atributos HTML/CSS disponíveis e os atributos direcionados ao Auxiliar de Marca:</span><span class="sxs-lookup"><span data-stu-id="bbb64-193">After you enter `<label`, IntelliSense lists the available HTML/CSS attributes and the Tag Helper-targeted attributes:</span></span>

![imagem](intro/_static/labelattr.png)

<span data-ttu-id="bbb64-195">O preenchimento de declaração do IntelliSense permite que você pressione a tecla TAB para preencher a declaração com o valor selecionado:</span><span class="sxs-lookup"><span data-stu-id="bbb64-195">IntelliSense statement completion allows you to enter the tab key to complete the statement with the selected value:</span></span>

![imagem](intro/_static/stmtcomplete.png)

<span data-ttu-id="bbb64-197">Assim que um atributo do Auxiliar de Marca é inserido, as fontes da marca e do atributo são alteradas.</span><span class="sxs-lookup"><span data-stu-id="bbb64-197">As soon as a Tag Helper attribute is entered, the tag and attribute fonts change.</span></span> <span data-ttu-id="bbb64-198">Usando o tema de cores padrão "Azul" ou "Claro" do Visual Studio, a fonte é roxo em negrito.</span><span class="sxs-lookup"><span data-stu-id="bbb64-198">Using the default Visual Studio "Blue" or "Light" color theme, the font is bold purple.</span></span> <span data-ttu-id="bbb64-199">Se estiver usando o tema "Escuro", a fonte será azul-petróleo em negrito.</span><span class="sxs-lookup"><span data-stu-id="bbb64-199">If you're using the "Dark" theme the font is bold teal.</span></span> <span data-ttu-id="bbb64-200">As imagens deste documento foram obtidas usando o tema padrão.</span><span class="sxs-lookup"><span data-stu-id="bbb64-200">The images in this document were taken using the default theme.</span></span>

![imagem](intro/_static/labelaspfor2.png)

<span data-ttu-id="bbb64-202">Insira o atalho *CompleteWord* do Visual Studio – Ctrl + barra de espaços é o [padrão](/visualstudio/ide/default-keyboard-shortcuts-in-visual-studio) dentro das aspas duplas ("") e você está agora no C#, exatamente como estaria em uma classe do C#.</span><span class="sxs-lookup"><span data-stu-id="bbb64-202">You can enter the Visual Studio *CompleteWord* shortcut (Ctrl +spacebar is the [default](/visualstudio/ide/default-keyboard-shortcuts-in-visual-studio) inside the double quotes (""), and you are now in C#, just like you would be in a C# class.</span></span> <span data-ttu-id="bbb64-203">O IntelliSense exibe todos os métodos e propriedades no modelo de página.</span><span class="sxs-lookup"><span data-stu-id="bbb64-203">IntelliSense displays all the methods and properties on the page model.</span></span> <span data-ttu-id="bbb64-204">Os métodos e as propriedades estão disponíveis porque o tipo de propriedade é `ModelExpression`.</span><span class="sxs-lookup"><span data-stu-id="bbb64-204">The methods and properties are available because the property type is `ModelExpression`.</span></span> <span data-ttu-id="bbb64-205">Na imagem abaixo, estou editando a exibição `Register` e, portanto, o `RegisterViewModel` está disponível.</span><span class="sxs-lookup"><span data-stu-id="bbb64-205">In the image below, I'm editing the `Register` view, so the `RegisterViewModel` is available.</span></span>

![imagem](intro/_static/intellemail.png)

<span data-ttu-id="bbb64-207">O IntelliSense lista as propriedades e os métodos disponíveis para o modelo na página.</span><span class="sxs-lookup"><span data-stu-id="bbb64-207">IntelliSense lists the properties and methods available to the model on the page.</span></span> <span data-ttu-id="bbb64-208">O ambiente avançado de IntelliSense ajuda você a selecionar a classe CSS:</span><span class="sxs-lookup"><span data-stu-id="bbb64-208">The rich IntelliSense environment helps you select the CSS class:</span></span>

![imagem](intro/_static/iclass.png)

![imagem](intro/_static/intel3.png)

## <a name="tag-helpers-compared-to-html-helpers"></a><span data-ttu-id="bbb64-211">Comparação entre Auxiliares de Marca e Auxiliares HTML</span><span class="sxs-lookup"><span data-stu-id="bbb64-211">Tag Helpers compared to HTML Helpers</span></span>

<span data-ttu-id="bbb64-212">Os Auxiliares de Marca são anexados a elementos HTML em exibições do Razor, enquanto os [Auxiliares HTML](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers) são invocados como métodos intercalados com HTML nas exibições do Razor.</span><span class="sxs-lookup"><span data-stu-id="bbb64-212">Tag Helpers attach to HTML elements in Razor views, while [HTML Helpers](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers) are invoked as methods interspersed with HTML in Razor views.</span></span> <span data-ttu-id="bbb64-213">Considere a seguinte marcação do Razor, que cria um rótulo HTML com a classe CSS "caption":</span><span class="sxs-lookup"><span data-stu-id="bbb64-213">Consider the following Razor markup, which creates an HTML label with the CSS class "caption":</span></span>

```cshtml
@Html.Label("FirstName", "First Name:", new {@class="caption"})
```

<span data-ttu-id="bbb64-214">O símbolo de arroba (`@`) informa o Razor de que este é o início do código.</span><span class="sxs-lookup"><span data-stu-id="bbb64-214">The at (`@`) symbol tells Razor this is the start of code.</span></span> <span data-ttu-id="bbb64-215">Os dois próximos parâmetros ("FirstName" e "First Name:") são cadeias de caracteres; portanto, o [IntelliSense](/visualstudio/ide/using-intellisense) não pode ajudar.</span><span class="sxs-lookup"><span data-stu-id="bbb64-215">The next two parameters ("FirstName" and "First Name:") are strings, so [IntelliSense](/visualstudio/ide/using-intellisense) can't help.</span></span> <span data-ttu-id="bbb64-216">O último argumento:</span><span class="sxs-lookup"><span data-stu-id="bbb64-216">The last argument:</span></span>

```cshtml
new {@class="caption"}
```

<span data-ttu-id="bbb64-217">É um objeto anônimo usado para representar atributos.</span><span class="sxs-lookup"><span data-stu-id="bbb64-217">Is an anonymous object used to represent attributes.</span></span> <span data-ttu-id="bbb64-218">Como a <strong>classe</strong> é uma palavra-chave reservada no C#, use o símbolo `@` para forçar o C# a interpretar "@class=" como um símbolo (nome da propriedade).</span><span class="sxs-lookup"><span data-stu-id="bbb64-218">Because <strong>class</strong> is a reserved keyword in C#, you use the `@` symbol to force C# to interpret "@class=" as a symbol (property name).</span></span> <span data-ttu-id="bbb64-219">Para um designer de front-end (alguém familiarizado com HTML/CSS/JavaScript e outras tecnologias de cliente, mas não familiarizado com o C# e Razor), a maior parte da linha é estranha.</span><span class="sxs-lookup"><span data-stu-id="bbb64-219">To a front-end designer (someone familiar with HTML/CSS/JavaScript and other client technologies but not familiar with C# and Razor), most of the line is foreign.</span></span> <span data-ttu-id="bbb64-220">Toda a linha precisa ser criada sem nenhuma ajuda do IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="bbb64-220">The entire line must be authored with no help from IntelliSense.</span></span>

<span data-ttu-id="bbb64-221">Usando o `LabelTagHelper`, a mesma marcação pode ser escrita como:</span><span class="sxs-lookup"><span data-stu-id="bbb64-221">Using the `LabelTagHelper`, the same markup can be written as:</span></span>

![imagem](intro/_static/label2.png)

<span data-ttu-id="bbb64-223">Com a versão do Auxiliar de Marca, assim que você insere `<l` no editor do Visual Studio, o IntelliSense exibe elementos correspondentes:</span><span class="sxs-lookup"><span data-stu-id="bbb64-223">With the Tag Helper version, as soon as you enter `<l` in the Visual Studio editor, IntelliSense displays matching elements:</span></span>

![imagem](intro/_static/label.png)

<span data-ttu-id="bbb64-225">O IntelliSense ajuda você a escrever a linha inteira.</span><span class="sxs-lookup"><span data-stu-id="bbb64-225">IntelliSense helps you write the entire line.</span></span> <span data-ttu-id="bbb64-226">O `LabelTagHelper` também usa como padrão a definição do conteúdo do valor de atributo `asp-for` ("FirstName") como "First Name"; ele converte propriedades concatenadas em uma frase composta do nome da propriedade com um espaço em que ocorre cada nova letra maiúscula.</span><span class="sxs-lookup"><span data-stu-id="bbb64-226">The `LabelTagHelper` also defaults to setting the content of the `asp-for` attribute value ("FirstName") to "First Name"; It converts camel-cased properties to a sentence composed of the property name with a space where each new upper-case letter occurs.</span></span> <span data-ttu-id="bbb64-227">Na seguinte marcação:</span><span class="sxs-lookup"><span data-stu-id="bbb64-227">In the following markup:</span></span>

![imagem](intro/_static/label2.png)

<span data-ttu-id="bbb64-229">gera:</span><span class="sxs-lookup"><span data-stu-id="bbb64-229">generates:</span></span>

```cshtml
<label class="caption" for="FirstName">First Name</label>
```

<span data-ttu-id="bbb64-230">O conteúdo concatenado para maiúsculas e minúsculas não é usado se você adiciona o conteúdo ao `<label>`.</span><span class="sxs-lookup"><span data-stu-id="bbb64-230">The camel-cased to sentence-cased content isn't used if you add content to the `<label>`.</span></span> <span data-ttu-id="bbb64-231">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bbb64-231">For example:</span></span>

![imagem](intro/_static/1stName.png)

<span data-ttu-id="bbb64-233">gera:</span><span class="sxs-lookup"><span data-stu-id="bbb64-233">generates:</span></span>

```cshtml
<label class="caption" for="FirstName">Name First</label>
```

<span data-ttu-id="bbb64-234">A imagem de código a seguir mostra a parte do Formulário da exibição do Razor *Views/Account/Register.cshtml* gerada com base no modelo herdado do ASP.NET 4.5 MVC incluído com o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="bbb64-234">The following code image shows the Form portion of the *Views/Account/Register.cshtml* Razor view generated from the legacy ASP.NET 4.5.x MVC template included with Visual Studio 2015.</span></span>

![imagem](intro/_static/regCS.png)

<span data-ttu-id="bbb64-236">O editor do Visual Studio exibe o código C# com uma tela de fundo cinza.</span><span class="sxs-lookup"><span data-stu-id="bbb64-236">The Visual Studio editor displays C# code with a grey background.</span></span> <span data-ttu-id="bbb64-237">Por exemplo, o Auxiliar HTML `AntiForgeryToken`:</span><span class="sxs-lookup"><span data-stu-id="bbb64-237">For example, the `AntiForgeryToken` HTML Helper:</span></span>

```cshtml
@Html.AntiForgeryToken()
```

<span data-ttu-id="bbb64-238">é exibido com uma tela de fundo cinza.</span><span class="sxs-lookup"><span data-stu-id="bbb64-238">is displayed with a grey background.</span></span> <span data-ttu-id="bbb64-239">A maior parte da marcação na exibição Register é C#.</span><span class="sxs-lookup"><span data-stu-id="bbb64-239">Most of the markup in the Register view is C#.</span></span> <span data-ttu-id="bbb64-240">Compare isso com a abordagem equivalente ao uso de Auxiliares de Marca:</span><span class="sxs-lookup"><span data-stu-id="bbb64-240">Compare that to the equivalent approach using Tag Helpers:</span></span>

![imagem](intro/_static/regTH.png)

<span data-ttu-id="bbb64-242">A marcação é muito mias limpa e fácil de ler, editar e manter que a abordagem dos Auxiliares HTML.</span><span class="sxs-lookup"><span data-stu-id="bbb64-242">The markup is much cleaner and easier to read, edit, and maintain than the HTML Helpers approach.</span></span> <span data-ttu-id="bbb64-243">O código C# é reduzido ao mínimo que o servidor precisa conhecer.</span><span class="sxs-lookup"><span data-stu-id="bbb64-243">The C# code is reduced to the minimum that the server needs to know about.</span></span> <span data-ttu-id="bbb64-244">O editor do Visual Studio exibe a marcação direcionada por um Auxiliar de Marca em uma fonte diferenciada.</span><span class="sxs-lookup"><span data-stu-id="bbb64-244">The Visual Studio editor displays markup targeted by a Tag Helper in a distinctive font.</span></span>

<span data-ttu-id="bbb64-245">Considere o grupo *Email*:</span><span class="sxs-lookup"><span data-stu-id="bbb64-245">Consider the *Email* group:</span></span>

[!code-csharp[](intro/sample/Register.cshtml?range=12-18)]

<span data-ttu-id="bbb64-246">Cada um dos atributos "asp-" tem um valor "Email", mas "Email" não é uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bbb64-246">Each of the "asp-" attributes has a value of "Email", but "Email" isn't a string.</span></span> <span data-ttu-id="bbb64-247">Nesse contexto, "Email" é a propriedade da expressão do modelo C# para o `RegisterViewModel`.</span><span class="sxs-lookup"><span data-stu-id="bbb64-247">In this context, "Email" is the C# model expression property for the `RegisterViewModel`.</span></span>

<span data-ttu-id="bbb64-248">O editor do Visual Studio ajuda você a escrever **toda** a marcação na abordagem do Auxiliar de Marca de formulário de registro, enquanto o Visual Studio não fornece nenhuma ajuda para a maioria do código na abordagem de Auxiliares HTML.</span><span class="sxs-lookup"><span data-stu-id="bbb64-248">The Visual Studio editor helps you write **all** of the markup in the Tag Helper approach of the register form, while Visual Studio provides no help for most of the code in the HTML Helpers approach.</span></span> <span data-ttu-id="bbb64-249">[Suporte do IntelliSense para Auxiliares de Marca](#intellisense-support-for-tag-helpers) apresenta detalhes sobre como trabalhar com Auxiliares de Marca no editor do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bbb64-249">[IntelliSense support for Tag Helpers](#intellisense-support-for-tag-helpers) goes into detail on working with Tag Helpers in the Visual Studio editor.</span></span>

## <a name="tag-helpers-compared-to-web-server-controls"></a><span data-ttu-id="bbb64-250">Comparação entre Auxiliares de Marca e Controles de Servidor Web</span><span class="sxs-lookup"><span data-stu-id="bbb64-250">Tag Helpers compared to Web Server Controls</span></span>

* <span data-ttu-id="bbb64-251">Os Auxiliares de Marca não têm o elemento ao qual estão associados; simplesmente participam da renderização do elemento e do conteúdo.</span><span class="sxs-lookup"><span data-stu-id="bbb64-251">Tag Helpers don't own the element they're associated with; they simply participate in the rendering of the element and content.</span></span> <span data-ttu-id="bbb64-252">Os [controles de Servidor Web](https://msdn.microsoft.com/library/7698y1f0.aspx) do ASP.NET são declarados e invocados em uma página.</span><span class="sxs-lookup"><span data-stu-id="bbb64-252">ASP.NET [Web Server controls](https://msdn.microsoft.com/library/7698y1f0.aspx) are declared and invoked on a page.</span></span>

* <span data-ttu-id="bbb64-253">Os [controles de Servidor Web](https://msdn.microsoft.com/library/zsyt68f1.aspx) têm um ciclo de vida não trivial que pode dificultar o desenvolvimento e a depuração.</span><span class="sxs-lookup"><span data-stu-id="bbb64-253">[Web Server controls](https://msdn.microsoft.com/library/zsyt68f1.aspx) have a non-trivial lifecycle that can make developing and debugging difficult.</span></span>

* <span data-ttu-id="bbb64-254">Os controles de Servidor Web permitem que você adicione a funcionalidade aos elementos DOM (Modelo de Objeto do Documento) do cliente usando um controle de cliente.</span><span class="sxs-lookup"><span data-stu-id="bbb64-254">Web Server controls allow you to add functionality to the client Document Object Model (DOM) elements by using a client control.</span></span> <span data-ttu-id="bbb64-255">Os Auxiliares de Marca não tem nenhum DOM.</span><span class="sxs-lookup"><span data-stu-id="bbb64-255">Tag Helpers have no DOM.</span></span>

* <span data-ttu-id="bbb64-256">Os controles de Servidor Web incluem a detecção automática do navegador.</span><span class="sxs-lookup"><span data-stu-id="bbb64-256">Web Server controls include automatic browser detection.</span></span> <span data-ttu-id="bbb64-257">Os Auxiliares de Marca não têm nenhum conhecimento sobre o navegador.</span><span class="sxs-lookup"><span data-stu-id="bbb64-257">Tag Helpers have no knowledge of the browser.</span></span>

* <span data-ttu-id="bbb64-258">Vários Auxiliares de Marca podem atuar no mesmo elemento (consulte [Evitando conflitos do Auxiliar de Marca](xref:mvc/views/tag-helpers/authoring#avoid-tag-helper-conflicts)), embora normalmente não seja possível compor controles de Servidor Web.</span><span class="sxs-lookup"><span data-stu-id="bbb64-258">Multiple Tag Helpers can act on the same element (see [Avoiding Tag Helper conflicts](xref:mvc/views/tag-helpers/authoring#avoid-tag-helper-conflicts) ) while you typically can't compose Web Server controls.</span></span>

* <span data-ttu-id="bbb64-259">Os Auxiliares de Marca podem modificar a marca e o conteúdo de elementos HTML no escopo com o qual foram definidos, mas não modificam diretamente todo o resto em uma página.</span><span class="sxs-lookup"><span data-stu-id="bbb64-259">Tag Helpers can modify the tag and content of HTML elements that they're scoped to, but don't directly modify anything else on a page.</span></span> <span data-ttu-id="bbb64-260">Os controles de Servidor Web têm um escopo menos específico e podem executar ações que afetam outras partes da página, permitindo efeitos colaterais não intencionais.</span><span class="sxs-lookup"><span data-stu-id="bbb64-260">Web Server controls have a less specific scope and can perform actions that affect other parts of your page; enabling unintended side effects.</span></span>

* <span data-ttu-id="bbb64-261">Os controles de Servidor Web usam conversores de tipo para converter cadeias de caracteres em objetos.</span><span class="sxs-lookup"><span data-stu-id="bbb64-261">Web Server controls use type converters to convert strings into objects.</span></span> <span data-ttu-id="bbb64-262">Com os Auxiliares de Marca, você trabalha nativamente no C# e, portanto, não precisa fazer a conversão de tipo.</span><span class="sxs-lookup"><span data-stu-id="bbb64-262">With Tag Helpers, you work natively in C#, so you don't need to do type conversion.</span></span>

* <span data-ttu-id="bbb64-263">Os controles de Servidor Web usam [System.ComponentModel](/dotnet/api/system.componentmodel) para implementar o comportamento de componentes e controles em tempo de execução e em tempo de design.</span><span class="sxs-lookup"><span data-stu-id="bbb64-263">Web Server controls use [System.ComponentModel](/dotnet/api/system.componentmodel) to implement the run-time and design-time behavior of components and controls.</span></span> <span data-ttu-id="bbb64-264">`System.ComponentModel` inclui as interfaces e as classes base para implementar atributos e conversores de tipo, associar a fontes de dados e licenciar componentes.</span><span class="sxs-lookup"><span data-stu-id="bbb64-264">`System.ComponentModel` includes the base classes and interfaces for implementing attributes and type converters, binding to data sources, and licensing components.</span></span> <span data-ttu-id="bbb64-265">Compare isso com os Auxiliares de Marca, que normalmente são derivados de `TagHelper`, e a classe base `TagHelper` expõe apenas dois métodos, `Process` e `ProcessAsync`.</span><span class="sxs-lookup"><span data-stu-id="bbb64-265">Contrast that to Tag Helpers, which typically derive from `TagHelper`, and the `TagHelper` base class exposes only two methods, `Process` and `ProcessAsync`.</span></span>

## <a name="customizing-the-tag-helper-element-font"></a><span data-ttu-id="bbb64-266">Personalizando a fonte de elemento do Auxiliar de Marca</span><span class="sxs-lookup"><span data-stu-id="bbb64-266">Customizing the Tag Helper element font</span></span>

<span data-ttu-id="bbb64-267">Personalize a fonte e a colorização em **Ferramentas** > **Opções** > **Ambiente** > **Fontes e Cores**:</span><span class="sxs-lookup"><span data-stu-id="bbb64-267">You can customize the font and colorization from **Tools** > **Options** > **Environment** > **Fonts and Colors**:</span></span>

![imagem](intro/_static/fontoptions2.png)

## <a name="additional-resources"></a><span data-ttu-id="bbb64-269">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="bbb64-269">Additional resources</span></span>

* [<span data-ttu-id="bbb64-270">Auxiliares de marca de autor</span><span class="sxs-lookup"><span data-stu-id="bbb64-270">Author Tag Helpers</span></span>](xref:mvc/views/tag-helpers/authoring)
* [<span data-ttu-id="bbb64-271">Trabalhando com formulários </span><span class="sxs-lookup"><span data-stu-id="bbb64-271">Working with Forms </span></span>](xref:mvc/views/working-with-forms)
* <span data-ttu-id="bbb64-272">[TagHelperSamples no GitHub](https://github.com/dpaquette/TagHelperSamples) contém amostras de Auxiliar de Marca para trabalhar com o [Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="bbb64-272">[TagHelperSamples on GitHub](https://github.com/dpaquette/TagHelperSamples) contains Tag Helper samples for working with [Bootstrap](http://getbootstrap.com/).</span></span>
