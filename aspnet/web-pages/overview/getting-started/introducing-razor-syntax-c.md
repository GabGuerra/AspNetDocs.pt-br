---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: Introdução à programação Web do ASP.NET usando a sintaxe do Razor (c#) | Microsoft Docs
author: Rick-Anderson
description: Este capítulo fornece uma visão geral da programação com páginas da Web do ASP.NET usando a sintaxe do Razor. O ASP.NET é uma tecnologia da Microsoft para executar o pa web dinâmico...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: d9edcd61e52941c0fd69e645da7e2cf467a632ac
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65131778"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a><span data-ttu-id="80255-104">Introdução à programação Web do ASP.NET usando a sintaxe do Razor (c#)</span><span class="sxs-lookup"><span data-stu-id="80255-104">Introduction to ASP.NET Web Programming Using the Razor Syntax (C#)</span></span>

<span data-ttu-id="80255-105">por [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="80255-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="80255-106">Este artigo fornece uma visão geral da programação com páginas da Web do ASP.NET usando a sintaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="80255-106">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax.</span></span> <span data-ttu-id="80255-107">O ASP.NET é uma tecnologia da Microsoft para a execução de páginas da web dinâmicas em servidores web.</span><span class="sxs-lookup"><span data-stu-id="80255-107">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span> <span data-ttu-id="80255-108">Este artigo concentra-se em usando a linguagem de programação c#.</span><span class="sxs-lookup"><span data-stu-id="80255-108">This articles focuses on using the C# programming language.</span></span>
> 
> <span data-ttu-id="80255-109">**O que você vai aprender**:</span><span class="sxs-lookup"><span data-stu-id="80255-109">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="80255-110">Os 8 principais dicas para começar a programação de páginas Web ASP.NET usando a sintaxe do Razor de programação.</span><span class="sxs-lookup"><span data-stu-id="80255-110">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="80255-111">Conceitos básicos de programação, será necessário.</span><span class="sxs-lookup"><span data-stu-id="80255-111">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="80255-112">Qual código de servidor ASP.NET e a sintaxe do Razor é tudo sobre.</span><span class="sxs-lookup"><span data-stu-id="80255-112">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="80255-113">Versões de software</span><span class="sxs-lookup"><span data-stu-id="80255-113">Software versions</span></span>
> 
> 
> - <span data-ttu-id="80255-114">Páginas da Web do ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="80255-114">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="80255-115">Este tutorial também funciona com ASP.NET Web Pages 2.</span><span class="sxs-lookup"><span data-stu-id="80255-115">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="80255-116">Principais dicas de programação 8</span><span class="sxs-lookup"><span data-stu-id="80255-116">The Top 8 Programming Tips</span></span>

<span data-ttu-id="80255-117">Esta seção lista algumas dicas que com certeza, você precisa saber como começar a escrever código de servidor ASP.NET usando a sintaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="80255-117">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="80255-118">A sintaxe Razor é baseada na linguagem de programação c#, e que é o idioma que é usado com mais frequência com páginas da Web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="80255-118">The Razor syntax is based on the C# programming language, and that's the language that's used most often with ASP.NET Web Pages.</span></span> <span data-ttu-id="80255-119">No entanto, a sintaxe do Razor também oferece suporte a linguagem Visual Basic e tudo o que você vê que você também pode fazer no Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="80255-119">However, the Razor syntax also supports the Visual Basic language, and everything you see you can also do in Visual Basic.</span></span> <span data-ttu-id="80255-120">Para obter detalhes, consulte o Apêndice [linguagem Visual Basic e a sintaxe](https://go.microsoft.com/fwlink/?LinkId=202908).</span><span class="sxs-lookup"><span data-stu-id="80255-120">For details, see the appendix [Visual Basic Language and Syntax](https://go.microsoft.com/fwlink/?LinkId=202908).</span></span>

<span data-ttu-id="80255-121">Você pode encontrar mais detalhes sobre a maioria dessas técnicas de programação posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="80255-121">You can find more details about most of these programming techniques later in the article.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="80255-122">1. Adicione o código para uma página usando o caractere @</span><span class="sxs-lookup"><span data-stu-id="80255-122">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="80255-123">O `@` caractere inicia expressões embutidas, os blocos de instrução única e blocos de várias instruções:</span><span class="sxs-lookup"><span data-stu-id="80255-123">The `@` character starts inline expressions, single statement blocks, and multi-statement blocks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

<span data-ttu-id="80255-124">Isso é que essas instruções aparência quando a página é executada em um navegador:</span><span class="sxs-lookup"><span data-stu-id="80255-124">This is what these statements look like when the page runs in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="80255-126">**A codificação HTML**</span><span class="sxs-lookup"><span data-stu-id="80255-126">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="80255-127">Quando você exibe o conteúdo em uma página usando o `@` de caracteres, como nos exemplos anteriores, ASP.NET codifica em HTML a saída.</span><span class="sxs-lookup"><span data-stu-id="80255-127">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="80255-128">Isso substitui os caracteres reservados de HTML (tal como `<` e `>` e `&`) com os códigos que permitem que os caracteres a serem exibidos como caracteres em uma página da web, em vez de sejam interpretados como marcações HTML ou entidades.</span><span class="sxs-lookup"><span data-stu-id="80255-128">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="80255-129">Sem codificação HTML, a saída do seu código de servidor não seja exibido corretamente e pode expor uma página a riscos de segurança.</span><span class="sxs-lookup"><span data-stu-id="80255-129">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="80255-130">Se sua meta é uma marcação HTML que processa marcas como marcação de saída (por exemplo `<p></p>` para um parágrafo ou `<em></em>` para enfatizar o texto), consulte a seção [combinação de texto, marcação e código em blocos de código](#BM_CombiningTextMarkupAndCode) mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="80255-130">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="80255-131">Você pode ler mais sobre a codificação HTML no [trabalhando com formulários](https://go.microsoft.com/fwlink/?LinkId=202892).</span><span class="sxs-lookup"><span data-stu-id="80255-131">You can read more about HTML encoding in [Working with Forms](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-in-braces"></a><span data-ttu-id="80255-132">2. Coloque blocos de código entre chaves</span><span class="sxs-lookup"><span data-stu-id="80255-132">2. You enclose code blocks in braces</span></span>

<span data-ttu-id="80255-133">Um *bloco de código* inclui uma ou mais instruções de código e é colocado entre chaves.</span><span class="sxs-lookup"><span data-stu-id="80255-133">A *code block* includes one or more code statements and is enclosed in braces.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

<span data-ttu-id="80255-134">O resultado exibido em um navegador:</span><span class="sxs-lookup"><span data-stu-id="80255-134">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a><span data-ttu-id="80255-136">3. Dentro de um bloco, você encerrar cada instrução de código com um ponto e vírgula</span><span class="sxs-lookup"><span data-stu-id="80255-136">3. Inside a block, you end each code statement with a semicolon</span></span>

<span data-ttu-id="80255-137">Dentro de um bloco de código, cada instrução de código completo deve terminar com um ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="80255-137">Inside a code block, each complete code statement must end with a semicolon.</span></span> <span data-ttu-id="80255-138">Expressões embutidas não terminam com ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="80255-138">Inline expressions don't end with a semicolon.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="80255-139">4. Usar variáveis para armazenar valores</span><span class="sxs-lookup"><span data-stu-id="80255-139">4. You use variables to store values</span></span>

<span data-ttu-id="80255-140">Você pode armazenar valores em uma *variável*, incluindo cadeias de caracteres, números e datas, etc. Você cria uma nova variável usando o `var` palavra-chave.</span><span class="sxs-lookup"><span data-stu-id="80255-140">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `var` keyword.</span></span> <span data-ttu-id="80255-141">Você pode inserir valores de variáveis diretamente em uma página usando `@`.</span><span class="sxs-lookup"><span data-stu-id="80255-141">You can insert variable values directly in a page using `@`.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

<span data-ttu-id="80255-142">O resultado exibido em um navegador:</span><span class="sxs-lookup"><span data-stu-id="80255-142">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="80255-144">5. Coloque os valores de cadeia de caracteres literal entre aspas duplas</span><span class="sxs-lookup"><span data-stu-id="80255-144">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="80255-145">Um *cadeia de caracteres* é uma sequência de caracteres que são tratados como texto.</span><span class="sxs-lookup"><span data-stu-id="80255-145">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="80255-146">Para especificar uma cadeia de caracteres, coloque-o entre aspas duplas:</span><span class="sxs-lookup"><span data-stu-id="80255-146">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

<span data-ttu-id="80255-147">Se a cadeia de caracteres que você deseja exibir contém um caractere de barra invertida ( `\` ) ou aspas duplas ( `"` ), use uma *literal de cadeia de caracteres textual* que é prefixado com o `@` operador.</span><span class="sxs-lookup"><span data-stu-id="80255-147">If the string that you want to display contains a backslash character ( `\` ) or double quotation marks ( `"` ), use a *verbatim string literal* that's prefixed with the `@` operator.</span></span> <span data-ttu-id="80255-148">(No c#, a \ caractere tem um significado especial, a menos que você use uma cadeia de caracteres textual literal.)</span><span class="sxs-lookup"><span data-stu-id="80255-148">(In C#, the \ character has special meaning unless you use a verbatim string literal.)</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

<span data-ttu-id="80255-149">Para inserir marcas de aspas duplas, use uma cadeia de caracteres textual literal e repita as aspas:</span><span class="sxs-lookup"><span data-stu-id="80255-149">To embed double quotation marks, use a verbatim string literal and repeat the quotation marks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

<span data-ttu-id="80255-150">Aqui está o resultado do uso de ambos os exemplos em uma página:</span><span class="sxs-lookup"><span data-stu-id="80255-150">Here's the result of using both of these examples in a page:</span></span>

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> <span data-ttu-id="80255-152">Observe que o `@` caractere é usado para marcar os literais de cadeia de caracteres textual em c# e para marcar o código em páginas ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="80255-152">Notice that the `@` character is used both to mark verbatim string literals in C# and to mark code in ASP.NET pages.</span></span>

### <a name="6-code-is-case-sensitive"></a><span data-ttu-id="80255-153">6. Código diferencia maiusculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="80255-153">6. Code is case sensitive</span></span>

<span data-ttu-id="80255-154">No c#, palavras-chave (como `var`, `true`, e `if`) e nomes de variáveis diferenciam maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="80255-154">In C#, keywords (like `var`, `true`, and `if`) and variable names are case sensitive.</span></span> <span data-ttu-id="80255-155">As seguintes linhas de código criam duas variáveis diferentes, `lastName` e `LastName.`</span><span class="sxs-lookup"><span data-stu-id="80255-155">The following lines of code create two different variables, `lastName` and `LastName.`</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

<span data-ttu-id="80255-156">Se você declarar uma variável como `var lastName = "Smith";` e se você tentar referenciar essa variável em sua página como `@LastName`, ocorrerá um erro porque `LastName` não será reconhecida.</span><span class="sxs-lookup"><span data-stu-id="80255-156">If you declare a variable as `var lastName = "Smith";` and if you try to reference that variable in your page as `@LastName`, an error results because `LastName` won't be recognized.</span></span>

> [!NOTE]
> <span data-ttu-id="80255-157">No Visual Basic, variáveis e palavras-chave são *não* diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="80255-157">In Visual Basic, keywords and variables are *not* case sensitive.</span></span>

### <a name="7-much-of-your-coding-involves-objects"></a><span data-ttu-id="80255-158">7. Grande parte da sua codificação envolve objetos</span><span class="sxs-lookup"><span data-stu-id="80255-158">7. Much of your coding involves objects</span></span>

<span data-ttu-id="80255-159">Uma *objeto* representa uma coisa que você pode programar com &#8212; uma página, uma caixa de texto, um arquivo, uma imagem, uma solicitação da web, uma mensagem de email, um registro de cliente (linha de banco de dados), etc. Objetos têm propriedades que descrevem suas características e que você pode ler ou modificar &#8212; um objeto de caixa de texto tem uma `Text` propriedade (entre outros), um objeto de solicitação tem um `Url` propriedade, uma mensagem de email tem um `From` propriedade, e um objeto do cliente tem um `FirstName` propriedade.</span><span class="sxs-lookup"><span data-stu-id="80255-159">An *object* represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics and that you can read or change &#8212; a text box object has a `Text` property (among others), a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="80255-160">Objetos também têm métodos que são as &quot;verbos&quot; eles podem executar.</span><span class="sxs-lookup"><span data-stu-id="80255-160">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="80255-161">Exemplos incluem um objeto de arquivo `Save` método, um objeto de imagem `Rotate` método e um objeto de email `Send` método.</span><span class="sxs-lookup"><span data-stu-id="80255-161">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="80255-162">Geralmente, você trabalhará com o `Request` do objeto, que oferece informações como os valores das caixas de texto (campos de formulário) na página, o tipo de navegador fez a solicitação, a URL da página, a identidade do usuário, etc. O exemplo a seguir mostra como acessar propriedades do `Request` objeto e como chamar o `MapPath` método o `Request` objeto, que fornece o caminho absoluto da página no servidor:</span><span class="sxs-lookup"><span data-stu-id="80255-162">You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page, what type of browser made the request, the URL of the page, the user identity, etc. The following example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

<span data-ttu-id="80255-163">O resultado exibido em um navegador:</span><span class="sxs-lookup"><span data-stu-id="80255-163">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="80255-165">8. Você pode escrever código que toma decisões</span><span class="sxs-lookup"><span data-stu-id="80255-165">8. You can write code that makes decisions</span></span>

<span data-ttu-id="80255-166">Um recurso importante de páginas da web dinâmicas é que você pode determinar o que fazer com base em condições.</span><span class="sxs-lookup"><span data-stu-id="80255-166">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="80255-167">A maneira mais comum para isso é com o `if` instrução (e opcional `else` instrução).</span><span class="sxs-lookup"><span data-stu-id="80255-167">The most common way to do this is with the `if` statement (and optional `else` statement).</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

<span data-ttu-id="80255-168">A instrução `if(IsPost)` é uma forma abreviada da gravação `if(IsPost == true)`.</span><span class="sxs-lookup"><span data-stu-id="80255-168">The statement `if(IsPost)` is a shorthand way of writing `if(IsPost == true)`.</span></span> <span data-ttu-id="80255-169">Juntamente com `if` instruções, há uma variedade de maneiras de testar condições, repetidas blocos de código, e assim por diante, que são descritos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="80255-169">Along with `if` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="80255-170">O resultado exibido em um navegador (depois de clicar em **enviar**):</span><span class="sxs-lookup"><span data-stu-id="80255-170">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a><span data-ttu-id="80255-172">HTTP GET e POST métodos e a propriedade IsPost</span><span class="sxs-lookup"><span data-stu-id="80255-172">HTTP GET and POST Methods and the IsPost Property</span></span>
> 
> <span data-ttu-id="80255-173">O protocolo usado para páginas da web (HTTP) dá suporte a um número muito limitado de métodos (verbos) que são usados para fazer solicitações ao servidor.</span><span class="sxs-lookup"><span data-stu-id="80255-173">The protocol used for web pages (HTTP) supports a very limited number of methods (verbs) that are used to make requests to the server.</span></span> <span data-ttu-id="80255-174">Dois os mais comuns são GET, que é usado para ler uma página, e o POST, o que é usado para enviar uma página.</span><span class="sxs-lookup"><span data-stu-id="80255-174">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="80255-175">Em geral, na primeira vez que um usuário solicita uma página, a página é solicitada usando GET.</span><span class="sxs-lookup"><span data-stu-id="80255-175">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="80255-176">Se o usuário preenche um formulário e, em seguida, clica no botão Enviar, o navegador faz uma solicitação POST para o servidor.</span><span class="sxs-lookup"><span data-stu-id="80255-176">If the user fills in a form and then clicks a submit button, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="80255-177">Na programação da web, muitas vezes é útil saber se uma página está sendo solicitada como um GET ou como uma POSTAGEM para que você saiba como processar a página.</span><span class="sxs-lookup"><span data-stu-id="80255-177">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="80255-178">Em páginas de Web do ASP.NET, você pode usar o `IsPost` propriedade para ver se uma solicitação é um GET ou uma POSTAGEM.</span><span class="sxs-lookup"><span data-stu-id="80255-178">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="80255-179">Se a solicitação for uma POSTAGEM, o `IsPost` propriedade retornará true, e você pode fazer coisas como ler os valores das caixas de texto em um formulário.</span><span class="sxs-lookup"><span data-stu-id="80255-179">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="80255-180">Muitos exemplos, você verá mostram como processar a página de forma diferente dependendo do valor de `IsPost`.</span><span class="sxs-lookup"><span data-stu-id="80255-180">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="80255-181">Um exemplo de código simples</span><span class="sxs-lookup"><span data-stu-id="80255-181">A Simple Code Example</span></span>

<span data-ttu-id="80255-182">Este procedimento mostra como criar uma página que ilustra as técnicas de programação básicas.</span><span class="sxs-lookup"><span data-stu-id="80255-182">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="80255-183">No exemplo, você cria uma página que permite aos usuários inserir dois números, em seguida, adiciona-os e exibe o resultado.</span><span class="sxs-lookup"><span data-stu-id="80255-183">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="80255-184">Em seu editor, crie um novo arquivo e nomeie- *AddNumbers.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="80255-184">In your editor, create a new file and name it *AddNumbers.cshtml*.</span></span>
2. <span data-ttu-id="80255-185">Copie o seguinte código e marcação para a página, substituindo qualquer coisa já na página.</span><span class="sxs-lookup"><span data-stu-id="80255-185">Copy the following code and markup into the page, replacing anything already in the page.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    <span data-ttu-id="80255-186">Aqui estão algumas coisas a observar:</span><span class="sxs-lookup"><span data-stu-id="80255-186">Here are some things for you to note:</span></span>

    - <span data-ttu-id="80255-187">O `@` caractere inicia o primeiro bloco de código na página, e precede o `totalMessage` variável que é inserido na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="80255-187">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable that's embedded near the bottom of the page.</span></span>
    - <span data-ttu-id="80255-188">O bloco na parte superior da página é colocado entre chaves.</span><span class="sxs-lookup"><span data-stu-id="80255-188">The block at the top of the page is enclosed in braces.</span></span>
    - <span data-ttu-id="80255-189">No bloco na parte superior, todas as linhas terminam com um ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="80255-189">In the block at the top, all lines end with a semicolon.</span></span>
    - <span data-ttu-id="80255-190">As variáveis `total`, `num1`, `num2`, e `totalMessage` armazenar vários números e uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="80255-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="80255-191">O valor de cadeia de caracteres literal atribuído para o `totalMessage` variável está entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="80255-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="80255-192">Porque o código é diferencia maiusculas de minúsculas, quando o `totalMessage` variável é usada na parte inferior da página, seu nome deve corresponder exatamente a variável na parte superior.</span><span class="sxs-lookup"><span data-stu-id="80255-192">Because the code is case-sensitive, when the `totalMessage` variable is used near the bottom of the page, its name must match the variable at the top exactly.</span></span>
    - <span data-ttu-id="80255-193">A expressão `num1.AsInt() + num2.AsInt()` mostra como trabalhar com objetos e métodos.</span><span class="sxs-lookup"><span data-stu-id="80255-193">The expression `num1.AsInt() + num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="80255-194">O `AsInt` método em cada variável converte a cadeia de caracteres inserida por um usuário em um número (um inteiro) para que você possa realizar aritmética nele.</span><span class="sxs-lookup"><span data-stu-id="80255-194">The `AsInt` method on each variable converts the string entered by a user to a number (an integer) so that you can perform arithmetic on it.</span></span>
    - <span data-ttu-id="80255-195">O `<form>` marca inclui um `method="post"` atributo.</span><span class="sxs-lookup"><span data-stu-id="80255-195">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="80255-196">Isso especifica que quando o usuário clica **adicionar**, a página será enviada ao servidor usando o método HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="80255-196">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="80255-197">Quando a página é enviada, o `if(IsPost)` teste for avaliado como true e a condicional código é executado, exibindo o resultado da adição de números.</span><span class="sxs-lookup"><span data-stu-id="80255-197">When the page is submitted, the `if(IsPost)` test evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="80255-198">Salve a página e executá-lo em um navegador.</span><span class="sxs-lookup"><span data-stu-id="80255-198">Save the page and run it in a browser.</span></span> <span data-ttu-id="80255-199">(Certifique-se de que a página está selecionada na **arquivos** espaço de trabalho antes de executá-lo.) Insira dois números inteiros e, em seguida, clique no **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="80255-199">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span> 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a><span data-ttu-id="80255-201">Conceitos básicos de programação</span><span class="sxs-lookup"><span data-stu-id="80255-201">Basic Programming Concepts</span></span>

<span data-ttu-id="80255-202">Este artigo fornece uma visão geral da programação de web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="80255-202">This article provides you with an overview of ASP.NET web programming.</span></span> <span data-ttu-id="80255-203">Não é um exame exaustivo, apenas um tour rápido por meio dos conceitos de programação que você usará com mais frequência.</span><span class="sxs-lookup"><span data-stu-id="80255-203">It isn't an exhaustive examination, just a quick tour through the programming concepts you'll use most often.</span></span> <span data-ttu-id="80255-204">Mesmo assim, ele aborda a quase tudo o que você precisará começar com páginas da Web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="80255-204">Even so, it covers almost everything you'll need to get started with ASP.NET Web Pages.</span></span>

<span data-ttu-id="80255-205">Mas primeiro, uma pouco técnicas básicas.</span><span class="sxs-lookup"><span data-stu-id="80255-205">But first, a little technical background.</span></span>

### <a name="the-razor-syntax-server-code-and-aspnet"></a><span data-ttu-id="80255-206">A sintaxe do Razor, o código do servidor e o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="80255-206">The Razor Syntax, Server Code, and ASP.NET</span></span>

<span data-ttu-id="80255-207">Sintaxe do Razor é uma sintaxe de programação simple para inserir código baseado em servidor em uma página da web.</span><span class="sxs-lookup"><span data-stu-id="80255-207">Razor syntax is a simple programming syntax for embedding server-based code in a web page.</span></span> <span data-ttu-id="80255-208">Em uma página da web que usa a sintaxe do Razor, há dois tipos de conteúdo: código de conteúdo e o servidor do cliente.</span><span class="sxs-lookup"><span data-stu-id="80255-208">In a web page that uses the Razor syntax, there are two kinds of content: client content and server code.</span></span> <span data-ttu-id="80255-209">Conteúdo do cliente é a coisa que você está acostumado em páginas da web: Marcação HTML (elementos), informações de estilo, como CSS, talvez alguns scripts de cliente, como JavaScript e texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="80255-209">Client content is the stuff you're used to in web pages: HTML markup (elements), style information such as CSS, maybe some client script such as JavaScript, and plain text.</span></span>

<span data-ttu-id="80255-210">Sintaxe do Razor permite adicionar código de servidor para esse conteúdo de cliente.</span><span class="sxs-lookup"><span data-stu-id="80255-210">Razor syntax lets you add server code to this client content.</span></span> <span data-ttu-id="80255-211">Se não houver código de servidor na página, o servidor executa o código em primeiro lugar, antes de enviar a página no navegador.</span><span class="sxs-lookup"><span data-stu-id="80255-211">If there's server code in the page, the server runs that code first, before it sends the page to the browser.</span></span> <span data-ttu-id="80255-212">Executando no servidor, o código pode executar tarefas que podem ser muito mais complexas de fazer usando o conteúdo do cliente usado sozinho, como acessar os bancos de dados baseados em servidor.</span><span class="sxs-lookup"><span data-stu-id="80255-212">By running on the server, the code can perform tasks that can be a lot more complex to do using client content alone, like accessing server-based databases.</span></span> <span data-ttu-id="80255-213">Mais importante, código de servidor pode criar dinamicamente o conteúdo de cliente &#8212; ele pode gerar uma marcação HTML ou outro conteúdo em tempo real e, em seguida, enviá-lo no navegador junto com qualquer HTML estático que a página pode conter.</span><span class="sxs-lookup"><span data-stu-id="80255-213">Most importantly, server code can dynamically create client content &#8212; it can generate HTML markup or other content on the fly and then send it to the browser along with any static HTML that the page might contain.</span></span> <span data-ttu-id="80255-214">Da perspectiva do navegador, cliente o conteúdo que é gerado pelo seu código de servidor não é diferente de qualquer outro conteúdo do cliente.</span><span class="sxs-lookup"><span data-stu-id="80255-214">From the browser's perspective, client content that's generated by your server code is no different than any other client content.</span></span> <span data-ttu-id="80255-215">Como você já viu, o código de servidor que é necessário é bastante simples.</span><span class="sxs-lookup"><span data-stu-id="80255-215">As you've already seen, the server code that's required is quite simple.</span></span>

<span data-ttu-id="80255-216">Páginas da web ASP.NET que incluem a sintaxe do Razor têm uma extensão de arquivo especial (*. cshtml* ou *. vbhtml*).</span><span class="sxs-lookup"><span data-stu-id="80255-216">ASP.NET web pages that include the Razor syntax have a special file extension (*.cshtml* or *.vbhtml*).</span></span> <span data-ttu-id="80255-217">O servidor reconhece essas extensões, executa o código que é marcado com a sintaxe do Razor e, em seguida, envia a página no navegador.</span><span class="sxs-lookup"><span data-stu-id="80255-217">The server recognizes these extensions, runs the code that's marked with Razor syntax, and then sends the page to the browser.</span></span>

### <a name="where-does-aspnet-fit-in"></a><span data-ttu-id="80255-218">Em que o ASP.NET se encaixa?</span><span class="sxs-lookup"><span data-stu-id="80255-218">Where does ASP.NET fit in?</span></span>

<span data-ttu-id="80255-219">Sintaxe do Razor baseia-se em uma tecnologia da Microsoft chamada ASP.NET, que por sua vez, baseia-se no Microsoft .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="80255-219">Razor syntax is based on a technology from Microsoft called ASP.NET, which in turn is based on the Microsoft .NET Framework.</span></span> <span data-ttu-id="80255-220">O.NET Framework é uma estrutura de programação intensa e abrangente da Microsoft para o desenvolvimento de praticamente qualquer tipo de aplicativo do computador.</span><span class="sxs-lookup"><span data-stu-id="80255-220">The.NET Framework is a big, comprehensive programming framework from Microsoft for developing virtually any type of computer application.</span></span> <span data-ttu-id="80255-221">O ASP.NET é a parte do .NET Framework que é projetado especificamente para criação de aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="80255-221">ASP.NET is the part of the .NET Framework that's specifically designed for creating web applications.</span></span> <span data-ttu-id="80255-222">Os desenvolvedores usaram o ASP.NET para criar muitos dos maiores e mais alto tráfego sites do mundo.</span><span class="sxs-lookup"><span data-stu-id="80255-222">Developers have used ASP.NET to create many of the largest and highest-traffic websites in the world.</span></span> <span data-ttu-id="80255-223">(Qualquer momento você ver a extensão de nome de arquivo *. aspx* como parte da URL em um site, você saberá que o site foi escrito usando o ASP.NET.)</span><span class="sxs-lookup"><span data-stu-id="80255-223">(Any time you see the file-name extension *.aspx* as part of the URL in a site, you'll know that the site was written using ASP.NET.)</span></span>

<span data-ttu-id="80255-224">A sintaxe do Razor oferece toda a potência do ASP.NET, mas usando uma sintaxe simplificada que é mais fácil de saber se você for um iniciante e o que torna você mais produtivo se você for um especialista.</span><span class="sxs-lookup"><span data-stu-id="80255-224">The Razor syntax gives you all the power of ASP.NET, but using a simplified syntax that's easier to learn if you're a beginner and that makes you more productive if you're an expert.</span></span> <span data-ttu-id="80255-225">Mesmo que essa sintaxe é simple de usar, significa que sua família relação com o ASP.NET e o .NET Framework como seus sites se tornarem mais sofisticados, você tem o poder das estruturas maiores disponíveis para você.</span><span class="sxs-lookup"><span data-stu-id="80255-225">Even though this syntax is simple to use, its family relationship to ASP.NET and the .NET Framework means that as your websites become more sophisticated, you have the power of the larger frameworks available to you.</span></span>

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> <span data-ttu-id="80255-227">**Classes e instâncias**</span><span class="sxs-lookup"><span data-stu-id="80255-227">**Classes and Instances**</span></span>
> 
> <span data-ttu-id="80255-228">Código de servidor ASP.NET usa objetos, que por sua vez, são criados na ideia de classes.</span><span class="sxs-lookup"><span data-stu-id="80255-228">ASP.NET server code uses objects, which are in turn built on the idea of classes.</span></span> <span data-ttu-id="80255-229">A classe é a definição ou modelo para um objeto.</span><span class="sxs-lookup"><span data-stu-id="80255-229">The class is the definition or template for an object.</span></span> <span data-ttu-id="80255-230">Por exemplo, um aplicativo pode conter um `Customer` classe que define as propriedades e métodos que precisa de qualquer objeto de cliente.</span><span class="sxs-lookup"><span data-stu-id="80255-230">For example, an application might contain a `Customer` class that defines the properties and methods that any customer object needs.</span></span>
> 
> <span data-ttu-id="80255-231">Quando o aplicativo precisa trabalhar com informações de cliente real, ele cria uma instância do (ou *instancia*) um objeto do cliente.</span><span class="sxs-lookup"><span data-stu-id="80255-231">When the application needs to work with actual customer information, it creates an instance of (or *instantiates*) a customer object.</span></span> <span data-ttu-id="80255-232">Cada cliente individual é uma instância separada do `Customer` classe.</span><span class="sxs-lookup"><span data-stu-id="80255-232">Each individual customer is a separate instance of the `Customer` class.</span></span> <span data-ttu-id="80255-233">Cada instância suporta as mesmas propriedades e métodos, mas os valores de propriedade para cada instância são normalmente é diferentes, pois cada objeto customer é exclusivo.</span><span class="sxs-lookup"><span data-stu-id="80255-233">Every instance supports the same properties and methods, but the property values for each instance are typically different, because each customer object is unique.</span></span> <span data-ttu-id="80255-234">No objeto de um cliente, o `LastName` propriedade poderia ser "Smith"; em outro objeto de cliente, o `LastName` propriedade poderia ser "Dias".</span><span class="sxs-lookup"><span data-stu-id="80255-234">In one customer object, the `LastName` property might be "Smith"; in another customer object, the `LastName` property might be "Jones."</span></span>
> 
> <span data-ttu-id="80255-235">Da mesma forma, qualquer página da web individuais em seu site é um `Page` que é uma instância do objeto a `Page` classe.</span><span class="sxs-lookup"><span data-stu-id="80255-235">Similarly, any individual web page in your site is a `Page` object that's an instance of the `Page` class.</span></span> <span data-ttu-id="80255-236">Um botão na página é uma `Button` objeto que é uma instância do `Button` classe e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="80255-236">A button on the page is a `Button` object that is an instance of the `Button` class, and so on.</span></span> <span data-ttu-id="80255-237">Cada instância tem suas próprias características, mas todos eles baseiam-se no que é especificado na definição de classe do objeto.</span><span class="sxs-lookup"><span data-stu-id="80255-237">Each instance has its own characteristics, but they all are based on what's specified in the object's class definition.</span></span>

## <a name="basic-syntax"></a><span data-ttu-id="80255-238">Sintaxe básica</span><span class="sxs-lookup"><span data-stu-id="80255-238">Basic Syntax</span></span>

<span data-ttu-id="80255-239">Anteriormente, você viu um exemplo básico de como criar uma página da Web do ASP.NET e como você pode adicionar código de servidor a marcação HTML.</span><span class="sxs-lookup"><span data-stu-id="80255-239">Earlier you saw a basic example of how to create an ASP.NET Web Pages page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="80255-240">Aqui você aprenderá os conceitos básicos de escrever código de servidor ASP.NET usando a sintaxe do Razor &#8212; ou seja, as regras linguagem de programação.</span><span class="sxs-lookup"><span data-stu-id="80255-240">Here you'll learn the basics of writing ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="80255-241">Se você tiver experiência com programação (especialmente se você já usou o C, C++, c#, Visual Basic ou JavaScript), grande parte o que você leia aqui será familiar.</span><span class="sxs-lookup"><span data-stu-id="80255-241">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="80255-242">Você provavelmente precisará familiarizar-se apenas com como o código do servidor é adicionado à marcação na *. cshtml* arquivos.</span><span class="sxs-lookup"><span data-stu-id="80255-242">You'll probably need to familiarize yourself only with how server code is added to markup in *.cshtml* files.</span></span>

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a><span data-ttu-id="80255-243">A combinação de texto, marcação e código em blocos de código</span><span class="sxs-lookup"><span data-stu-id="80255-243">Combining Text, Markup, and Code in Code Blocks</span></span>

<span data-ttu-id="80255-244">Em blocos de código do servidor, você geralmente deseja saída texto ou marcação (ou ambos) para a página.</span><span class="sxs-lookup"><span data-stu-id="80255-244">In server code blocks, you often want to output text or markup (or both) to the page.</span></span> <span data-ttu-id="80255-245">Se um bloco de código de servidor contiver o texto que não é código e que em vez disso, deve ser renderizado como está, o ASP.NET precisa ser capaz de distinguir que o texto do código.</span><span class="sxs-lookup"><span data-stu-id="80255-245">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="80255-246">Há várias maneiras de fazer isso.</span><span class="sxs-lookup"><span data-stu-id="80255-246">There are several ways to do this.</span></span>

- <span data-ttu-id="80255-247">Colocar o texto em um elemento HTML, como `<p></p>` ou `<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="80255-247">Enclose the text in an HTML element like `<p></p>` or `<em></em>`:</span></span>   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    <span data-ttu-id="80255-248">O elemento HTML pode incluir texto, elementos HTML adicionais e expressões de código do servidor.</span><span class="sxs-lookup"><span data-stu-id="80255-248">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="80255-249">Quando o ASP.NET vê a marca HTML de abertura (por exemplo, `<p>`), ele processa tudo, incluindo o elemento e seu conteúdo como é para o navegador, resolução de expressões de código do servidor quando ele passa.</span><span class="sxs-lookup"><span data-stu-id="80255-249">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything including the element and its content as is to the browser, resolving server-code expressions as it goes.</span></span>
- <span data-ttu-id="80255-250">Use o `@:` operador ou o `<text>` elemento.</span><span class="sxs-lookup"><span data-stu-id="80255-250">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="80255-251">O `@:` gera uma única linha de conteúdo que contém o texto sem formatação ou marcas HTML sem correspondência; o `<text>` elemento abrange várias linhas de saída.</span><span class="sxs-lookup"><span data-stu-id="80255-251">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="80255-252">Essas opções são úteis quando você não deseja renderizar um elemento HTML como parte da saída.</span><span class="sxs-lookup"><span data-stu-id="80255-252">These options are useful when you don't want to render an HTML element as part of the output.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    <span data-ttu-id="80255-253">Se você quiser várias linhas de texto ou marcas HTML não correspondentes de saída, você pode preceder cada linha com `@:`, ou você pode colocar a linha em um `<text>` elemento.</span><span class="sxs-lookup"><span data-stu-id="80255-253">If you want to output multiple lines of text or unmatched HTML tags, you can precede each line with `@:`, or you can enclose the line in a `<text>` element.</span></span> <span data-ttu-id="80255-254">Como o `@:` operador,`<text>` marcas são usadas pelo ASP.NET para identificar o conteúdo de texto e nunca são renderizadas na saída de página.</span><span class="sxs-lookup"><span data-stu-id="80255-254">Like the `@:` operator,`<text>` tags are used by ASP.NET to identify text content and are never rendered in the page output.</span></span>

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    <span data-ttu-id="80255-255">O primeiro exemplo repete o exemplo anterior, mas usa um único par de `<text>` marcas para delimitar o texto a ser renderizado.</span><span class="sxs-lookup"><span data-stu-id="80255-255">The first example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span> <span data-ttu-id="80255-256">No segundo exemplo, o `<text>` e `</text>` marcas Coloque três linhas, todas com parte do texto dependente e marcas HTML não correspondentes (`<br />`), junto com código de servidor e as marcas HTML correspondentes.</span><span class="sxs-lookup"><span data-stu-id="80255-256">In the second example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="80255-257">Novamente, você também pode preceder cada linha individualmente com a `@:` operador; ambas funcionam de forma.</span><span class="sxs-lookup"><span data-stu-id="80255-257">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    > [!NOTE]
    > <span data-ttu-id="80255-258">Quando você gerar o texto conforme mostrado nesta seção &#8212; usando um elemento HTML, o `@:` operador, ou o `<text>` elemento &#8212; ASP.NET não codificar com HTML a saída.</span><span class="sxs-lookup"><span data-stu-id="80255-258">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="80255-259">(Conforme observado anteriormente, o ASP.NET codificar a saída de expressões de código do servidor e os blocos de código do servidor que são precedidos por `@`, exceto nos casos especiais observados nesta seção.)</span><span class="sxs-lookup"><span data-stu-id="80255-259">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="80255-260">Whitespace</span><span class="sxs-lookup"><span data-stu-id="80255-260">Whitespace</span></span>

<span data-ttu-id="80255-261">Os espaços extras em uma instrução (e fora de uma cadeia de caracteres literal) não afetam a instrução:</span><span class="sxs-lookup"><span data-stu-id="80255-261">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

<span data-ttu-id="80255-262">Uma quebra de linha em uma instrução não tem nenhum efeito sobre a instrução, e você pode encapsular instruções para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="80255-262">A line break in a statement has no effect on the statement, and you can wrap statements for readability.</span></span> <span data-ttu-id="80255-263">As instruções a seguir são os mesmos:</span><span class="sxs-lookup"><span data-stu-id="80255-263">The following statements are the same:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

<span data-ttu-id="80255-264">No entanto, você não pode inserir uma linha no meio de um literal de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="80255-264">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="80255-265">O exemplo a seguir não funciona:</span><span class="sxs-lookup"><span data-stu-id="80255-265">The following example doesn't work:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

<span data-ttu-id="80255-266">Para combinar uma cadeia de caracteres longa é quebrada para várias linhas, como o código acima, há duas opções.</span><span class="sxs-lookup"><span data-stu-id="80255-266">To combine a long string that wraps to multiple lines like the above code, there are two options.</span></span> <span data-ttu-id="80255-267">Você pode usar o operador de concatenação (`+`), que você verá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="80255-267">You can use the concatenation operator (`+`), which you'll see later in this article.</span></span> <span data-ttu-id="80255-268">Você também pode usar o `@` caracteres para criar uma cadeia de caracteres textual literal, como você viu neste artigo.</span><span class="sxs-lookup"><span data-stu-id="80255-268">You can also use the `@` character to create a verbatim string literal, as you saw earlier in this article.</span></span> <span data-ttu-id="80255-269">Você pode dividir literais de cadeia de caracteres textual em linhas:</span><span class="sxs-lookup"><span data-stu-id="80255-269">You can break verbatim string literals across lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a><span data-ttu-id="80255-270">Código (e a marcação) comentários</span><span class="sxs-lookup"><span data-stu-id="80255-270">Code (and Markup) Comments</span></span>

<span data-ttu-id="80255-271">Comentários permitem que você deixar observações para você ou terceiros.</span><span class="sxs-lookup"><span data-stu-id="80255-271">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="80255-272">Eles também permitem que você desabilite (*comente*) uma seção de código ou marcação que você não deseja executar, mas deseja manter em sua página por enquanto.</span><span class="sxs-lookup"><span data-stu-id="80255-272">They also allow you to disable (*comment out*) a section of code or markup that you don't want to run but want to keep in your page for the time being.</span></span>

<span data-ttu-id="80255-273">Há diferentes de sintaxe para código do Razor em marcação HTML de comentário.</span><span class="sxs-lookup"><span data-stu-id="80255-273">There's different commenting syntax for Razor code and for HTML markup.</span></span> <span data-ttu-id="80255-274">Assim como acontece com todos os códigos do Razor, Razor comentários são processados (e, em seguida, removidos) no servidor antes que a página é enviada ao navegador.</span><span class="sxs-lookup"><span data-stu-id="80255-274">As with all Razor code, Razor comments are processed (and then removed) on the server before the page is sent to the browser.</span></span> <span data-ttu-id="80255-275">Portanto, a sintaxe de comentário do Razor permite colocar comentários no código (ou até mesmo na marcação) que você pode ver quando você editar o arquivo, mas que os usuários não veem, até mesmo na fonte de página.</span><span class="sxs-lookup"><span data-stu-id="80255-275">Therefore, the Razor commenting syntax lets you put comments into the code (or even into the markup) that you can see when you edit the file, but that users don't see, even in the page source.</span></span>

<span data-ttu-id="80255-276">Para comentários do Razor do ASP.NET, você iniciar o comentário com `@*` e encerrá-lo com `*@`.</span><span class="sxs-lookup"><span data-stu-id="80255-276">For ASP.NET Razor comments, you start the comment with `@*` and end it with `*@`.</span></span> <span data-ttu-id="80255-277">O comentário pode estar em uma linha ou várias linhas:</span><span class="sxs-lookup"><span data-stu-id="80255-277">The comment can be on one line or multiple lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

<span data-ttu-id="80255-278">Aqui está um comentário dentro de um bloco de código:</span><span class="sxs-lookup"><span data-stu-id="80255-278">Here is a comment within a code block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

<span data-ttu-id="80255-279">Aqui é o mesmo bloco de código, com a linha de código comentada para que ele não será executado:</span><span class="sxs-lookup"><span data-stu-id="80255-279">Here is the same block of code, with the line of code commented out so that it won't run:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

<span data-ttu-id="80255-280">Dentro de um bloco de código, como uma alternativa ao uso da sintaxe de comentário do Razor, você pode usar a sintaxe de comentário da linguagem de programação que você está usando, como c#:</span><span class="sxs-lookup"><span data-stu-id="80255-280">Inside a code block, as an alternative to using Razor comment syntax, you can use the commenting syntax of the programming language you're using, such as C#:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

<span data-ttu-id="80255-281">No c#, os comentários de linha única são precedidos pela `//` caracteres e comentários de várias linhas começam com `/*` e terminar com `*/`.</span><span class="sxs-lookup"><span data-stu-id="80255-281">In C#, single-line comments are preceded by the `//` characters, and multi-line comments begin with `/*` and end with `*/`.</span></span> <span data-ttu-id="80255-282">(Assim como acontece com comentários em Razor, c# comentários não são renderizados no navegador.)</span><span class="sxs-lookup"><span data-stu-id="80255-282">(As with Razor comments, C# comments are not rendered to the browser.)</span></span>

<span data-ttu-id="80255-283">Para marcação, como você provavelmente sabe, você pode criar um comentário HTML:</span><span class="sxs-lookup"><span data-stu-id="80255-283">For markup, as you probably know, you can create an HTML comment:</span></span>

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

<span data-ttu-id="80255-284">Os comentários do HTML começam com `<!--` caracteres e terminam com `-->`.</span><span class="sxs-lookup"><span data-stu-id="80255-284">HTML comments start with `<!--` characters and end with `-->`.</span></span> <span data-ttu-id="80255-285">Você pode usar comentários HTML ao redor não apenas texto, mas também qualquer marcação HTML que você talvez queira manter na página, mas não deseja renderizar.</span><span class="sxs-lookup"><span data-stu-id="80255-285">You can use HTML comments to surround not only text, but also any HTML markup that you may want to keep in the page but don't want to render.</span></span> <span data-ttu-id="80255-286">Este comentário HTML ocultará a todo o conteúdo de marcas e o texto que contêm:</span><span class="sxs-lookup"><span data-stu-id="80255-286">This HTML comment will hide the entire content of the tags and the text they contain:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

<span data-ttu-id="80255-287">Ao contrário de comentários, comentários HTML do Razor *são* renderizado para a página e o usuário poderá vê-los ao exibir a origem da página.</span><span class="sxs-lookup"><span data-stu-id="80255-287">Unlike Razor comments, HTML comments *are* rendered to the page and the user can see them by viewing the page source.</span></span>

<span data-ttu-id="80255-288">O Razor tem limitações em blocos aninhados da linguagem c#.</span><span class="sxs-lookup"><span data-stu-id="80255-288">Razor has limitations on nested blocks of C#.</span></span> <span data-ttu-id="80255-289">Para obter mais informações, consulte [variáveis c# chamado e aninhados blocos gerar quebrado código](http://aspnetwebstack.codeplex.com/workitem/1914)</span><span class="sxs-lookup"><span data-stu-id="80255-289">For more information see [Named C# Variables and Nested Blocks Generate Broken Code](http://aspnetwebstack.codeplex.com/workitem/1914)</span></span>

## <a name="variables"></a><span data-ttu-id="80255-290">Variáveis</span><span class="sxs-lookup"><span data-stu-id="80255-290">Variables</span></span>

<span data-ttu-id="80255-291">Uma variável é um objeto nomeado que você pode usar para armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="80255-291">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="80255-292">Você pode nomear variáveis, mas o nome deve começar com um caractere alfabético e não pode conter espaço em branco ou caracteres reservados.</span><span class="sxs-lookup"><span data-stu-id="80255-292">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="80255-293">Variáveis e tipos de dados</span><span class="sxs-lookup"><span data-stu-id="80255-293">Variables and Data Types</span></span>

<span data-ttu-id="80255-294">Uma variável pode ter um tipo de dados específico, que indica o tipo de dados é armazenado na variável.</span><span class="sxs-lookup"><span data-stu-id="80255-294">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="80255-295">Você pode ter variáveis de cadeia de caracteres que armazenam valores de cadeia de caracteres (como &quot;Olá, mundo&quot;), variáveis de inteiro que armazenam valores de número inteiro (como 3 ou 79) e variáveis de data que armazenam valores de data em uma variedade de formatos (como 12/4/2012 ou de março de 2009 ).</span><span class="sxs-lookup"><span data-stu-id="80255-295">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="80255-296">E há muitos outros tipos de dados que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="80255-296">And there are many other data types you can use.</span></span>

<span data-ttu-id="80255-297">No entanto, você geralmente não precisa especificar um tipo para uma variável.</span><span class="sxs-lookup"><span data-stu-id="80255-297">However, you generally don't have to specify a type for a variable.</span></span> <span data-ttu-id="80255-298">Na maioria das vezes, ASP.NET pode descobrir o tipo com base em como os dados na variável está sendo usados.</span><span class="sxs-lookup"><span data-stu-id="80255-298">Most of the time, ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="80255-299">(Ocasionalmente, você deve especificar um tipo; você verá exemplos em que isso é verdadeiro).</span><span class="sxs-lookup"><span data-stu-id="80255-299">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="80255-300">Você declara uma variável usando o `var` palavra-chave (se você não quiser especificar um tipo) ou usando o nome do tipo:</span><span class="sxs-lookup"><span data-stu-id="80255-300">You declare a variable using the `var` keyword (if you don't want to specify a type) or by using the name of the type:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

<span data-ttu-id="80255-301">O exemplo a seguir mostra alguns usos típicos de variáveis em uma página da web:</span><span class="sxs-lookup"><span data-stu-id="80255-301">The following example shows some typical uses of variables in a web page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

<span data-ttu-id="80255-302">Se você combinar os exemplos anteriores em uma página, você verá que eles são exibidos em um navegador:</span><span class="sxs-lookup"><span data-stu-id="80255-302">If you combine the previous examples in a page, you see this displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="80255-304">Convertendo e tipos de dados de teste</span><span class="sxs-lookup"><span data-stu-id="80255-304">Converting and Testing Data Types</span></span>

<span data-ttu-id="80255-305">Embora o ASP.NET geralmente pode determinar automaticamente um tipo de dados, às vezes, ele não é possível.</span><span class="sxs-lookup"><span data-stu-id="80255-305">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="80255-306">Portanto, você pode precisar ajudar ASP.NET executando uma conversão explícita.</span><span class="sxs-lookup"><span data-stu-id="80255-306">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="80255-307">Mesmo se você não precisa converter os tipos, às vezes é útil testar para ver qual tipo de dados você pode estar trabalhando com.</span><span class="sxs-lookup"><span data-stu-id="80255-307">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="80255-308">O caso mais comum é que você precisa converter uma cadeia de caracteres para outro tipo, como em um inteiro ou uma data.</span><span class="sxs-lookup"><span data-stu-id="80255-308">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="80255-309">O exemplo a seguir mostra um caso típico onde você deve converter uma cadeia de caracteres em um número.</span><span class="sxs-lookup"><span data-stu-id="80255-309">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

<span data-ttu-id="80255-310">Como uma regra de entrada do usuário são enviados a você como cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="80255-310">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="80255-311">Mesmo se você tiver solicitado que os usuários insiram um número, e mesmo se eles inseriu um dígito, quando a entrada do usuário é enviada e lê-lo no código, os dados estão no formato de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="80255-311">Even if you've prompted users to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="80255-312">Portanto, você deve converter a cadeia de caracteres em um número.</span><span class="sxs-lookup"><span data-stu-id="80255-312">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="80255-313">No exemplo, se você tentar executar cálculos nos valores sem convertê-los, o erro a seguir resulta, porque o ASP.NET não é possível adicionar duas cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="80255-313">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

<span data-ttu-id="80255-314">*Não é possível converter implicitamente o tipo 'string' para 'int'.*</span><span class="sxs-lookup"><span data-stu-id="80255-314">*Cannot implicitly convert type 'string' to 'int'.*</span></span>

<span data-ttu-id="80255-315">Para converter os valores inteiros, você deve chamar o `AsInt` método.</span><span class="sxs-lookup"><span data-stu-id="80255-315">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="80255-316">Se a conversão for bem-sucedida, você pode adicionar os números.</span><span class="sxs-lookup"><span data-stu-id="80255-316">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="80255-317">A tabela a seguir lista alguns métodos comuns de conversão e teste para variáveis.</span><span class="sxs-lookup"><span data-stu-id="80255-317">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="80255-318"><strong>Método</strong></span><span class="sxs-lookup"><span data-stu-id="80255-318"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-319"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="80255-319"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-320"><strong>Exemplo</strong></span><span class="sxs-lookup"><span data-stu-id="80255-320"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-321">Converte uma cadeia de caracteres que representa um número inteiro (como "593") em um inteiro.</span><span class="sxs-lookup"><span data-stu-id="80255-321">Converts a string that represents a whole number (like "593") to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-322">Converte uma cadeia de caracteres like &quot;verdadeira&quot; ou &quot;falso&quot; para um tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="80255-322">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-323">Converte uma cadeia de caracteres que tem um valor decimal como &quot;1.3&quot; ou &quot;7.439&quot; um número de ponto flutuante.</span><span class="sxs-lookup"><span data-stu-id="80255-323">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-324">Converte uma cadeia de caracteres que tem um valor decimal como &quot;1.3&quot; ou &quot;7.439&quot; em um número decimal.</span><span class="sxs-lookup"><span data-stu-id="80255-324">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="80255-325">(No ASP.NET, um número decimal é mais preciso do que um número de ponto flutuante.)</span><span class="sxs-lookup"><span data-stu-id="80255-325">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-326">Converte uma cadeia de caracteres que representa um valor de data e hora para o ASP.NET `DateTime` tipo.</span><span class="sxs-lookup"><span data-stu-id="80255-326">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-327">Converte qualquer tipo de dados em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="80255-327">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="80255-328">Operadores</span><span class="sxs-lookup"><span data-stu-id="80255-328">Operators</span></span>

<span data-ttu-id="80255-329">Um operador é uma palavra-chave ou um caractere que informa ao ASP.NET que tipo de comando para executar em uma expressão.</span><span class="sxs-lookup"><span data-stu-id="80255-329">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="80255-330">A linguagem c# (e a sintaxe do Razor que se baseia) dá suporte a muitos operadores, mas você só precisa reconhecer algumas para começar a usar.</span><span class="sxs-lookup"><span data-stu-id="80255-330">The C# language (and the Razor syntax that's based on it) supports many operators, but you only need to recognize a few to get started.</span></span> <span data-ttu-id="80255-331">A tabela a seguir resume os operadores mais comuns.</span><span class="sxs-lookup"><span data-stu-id="80255-331">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="80255-332"><strong>Operador</strong></span><span class="sxs-lookup"><span data-stu-id="80255-332"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-333"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="80255-333"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-334"><strong>Exemplos</strong></span><span class="sxs-lookup"><span data-stu-id="80255-334"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+` `-` `*` `/`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-335">Operadores de cálculo usados em expressões numéricas.</span><span class="sxs-lookup"><span data-stu-id="80255-335">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-336">Atribuição.</span><span class="sxs-lookup"><span data-stu-id="80255-336">Assignment.</span></span> <span data-ttu-id="80255-337">Atribui o valor no lado direito de uma instrução para o objeto no lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="80255-337">Assigns the value on the right side of a statement to the object on the left side.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-338">Igualdade.</span><span class="sxs-lookup"><span data-stu-id="80255-338">Equality.</span></span> <span data-ttu-id="80255-339">Retorna `true` se os valores forem iguais.</span><span class="sxs-lookup"><span data-stu-id="80255-339">Returns `true` if the values are equal.</span></span> <span data-ttu-id="80255-340">(Observe a diferença entre o `=` operador e o `==` operador.)</span><span class="sxs-lookup"><span data-stu-id="80255-340">(Notice the distinction between the `=` operator and the `==` operator.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-341">Desigualdade.</span><span class="sxs-lookup"><span data-stu-id="80255-341">Inequality.</span></span> <span data-ttu-id="80255-342">Retorna `true` se os valores não forem iguais.</span><span class="sxs-lookup"><span data-stu-id="80255-342">Returns `true` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-343">Menor-que, maior-que less-than-or-equal e maior-than-or-equal.</span><span class="sxs-lookup"><span data-stu-id="80255-343">Less-than, greater-than, less-than-or-equal, and greater-than-or-equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-344">Concatenação, que é usada para unir cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="80255-344">Concatenation, which is used to join strings.</span></span> <span data-ttu-id="80255-345">ASP.NET sabe a diferença entre esse operador e o operador de adição com base no tipo de dados da expressão.</span><span class="sxs-lookup"><span data-stu-id="80255-345">ASP.NET knows the difference between this operator and the addition operator based on the data type of the expression.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+=` `-=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-346">Os operadores de incremento e decremento, que adicionar e subtrair 1 (respectivamente) a partir de uma variável.</span><span class="sxs-lookup"><span data-stu-id="80255-346">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-347">Ponto.</span><span class="sxs-lookup"><span data-stu-id="80255-347">Dot.</span></span> <span data-ttu-id="80255-348">Usado para distinguir os objetos e suas propriedades e métodos.</span><span class="sxs-lookup"><span data-stu-id="80255-348">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-349">Parênteses.</span><span class="sxs-lookup"><span data-stu-id="80255-349">Parentheses.</span></span> <span data-ttu-id="80255-350">Usado para agrupar expressões e passar parâmetros para métodos.</span><span class="sxs-lookup"><span data-stu-id="80255-350">Used to group expressions and to pass parameters to methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-351">Colchetes.</span><span class="sxs-lookup"><span data-stu-id="80255-351">Brackets.</span></span> <span data-ttu-id="80255-352">Usado para acessar valores em matrizes ou coleções.</span><span class="sxs-lookup"><span data-stu-id="80255-352">Used for accessing values in arrays or collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-353">Não.</span><span class="sxs-lookup"><span data-stu-id="80255-353">Not.</span></span> <span data-ttu-id="80255-354">Inverte uma `true` valor `false` e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="80255-354">Reverses a `true` value to `false` and vice versa.</span></span> <span data-ttu-id="80255-355">Normalmente usado como uma forma abreviada para testar `false` (ou seja, para não `true`).</span><span class="sxs-lookup"><span data-stu-id="80255-355">Typically used as a shorthand way to test for `false` (that is, for not `true`).</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&&` `||`
    :::column-end:::
    :::column:::
    <span data-ttu-id="80255-356">AND lógico e, que são usados para vincular condições ou juntos.</span><span class="sxs-lookup"><span data-stu-id="80255-356">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="80255-357">Trabalhando com arquivos e caminhos de pasta no código</span><span class="sxs-lookup"><span data-stu-id="80255-357">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="80255-358">Geralmente, você trabalhará com caminhos de arquivo e pasta em seu código.</span><span class="sxs-lookup"><span data-stu-id="80255-358">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="80255-359">Aqui está um exemplo da estrutura de pasta física para um site, como pode aparecer em seu computador de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="80255-359">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="80255-360">Aqui estão alguns detalhes essenciais sobre URLs e caminhos:</span><span class="sxs-lookup"><span data-stu-id="80255-360">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="80255-361">Uma URL começa com qualquer um de um nome de domínio (`http://www.example.com`) ou um nome de servidor (`http://localhost`, `http://mycomputer`).</span><span class="sxs-lookup"><span data-stu-id="80255-361">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="80255-362">Uma URL corresponde a um caminho físico em um computador host.</span><span class="sxs-lookup"><span data-stu-id="80255-362">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="80255-363">Por exemplo, `http://myserver` podem corresponder à pasta *C:\websites\mywebsite* no servidor.</span><span class="sxs-lookup"><span data-stu-id="80255-363">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="80255-364">Um caminho virtual é uma abreviação para representar caminhos no código sem ter que especificar o caminho completo.</span><span class="sxs-lookup"><span data-stu-id="80255-364">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="80255-365">Ele inclui a parte de uma URL que segue o nome de domínio ou servidor.</span><span class="sxs-lookup"><span data-stu-id="80255-365">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="80255-366">Quando você usa caminhos virtuais, você pode mover seu código para um domínio diferente ou um servidor sem ter que atualizar os caminhos.</span><span class="sxs-lookup"><span data-stu-id="80255-366">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="80255-367">Aqui está um exemplo para ajudá-lo a entender as diferenças:</span><span class="sxs-lookup"><span data-stu-id="80255-367">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="80255-368">URL completa</span><span class="sxs-lookup"><span data-stu-id="80255-368">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="80255-369">Nome do servidor</span><span class="sxs-lookup"><span data-stu-id="80255-369">Server name</span></span> | <span data-ttu-id="80255-370">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="80255-370">*mycompanyserver*</span></span> |
| <span data-ttu-id="80255-371">Caminho virtual</span><span class="sxs-lookup"><span data-stu-id="80255-371">Virtual path</span></span> | <span data-ttu-id="80255-372">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="80255-372">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="80255-373">Caminho físico</span><span class="sxs-lookup"><span data-stu-id="80255-373">Physical path</span></span> | <span data-ttu-id="80255-374">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="80255-374">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="80255-375">É a raiz virtual /, assim como a raiz da unidade c: unidade é \.</span><span class="sxs-lookup"><span data-stu-id="80255-375">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="80255-376">(Os caminhos de pasta virtual sempre usam barras "/"). O caminho virtual de uma pasta não precisa ter o mesmo nome que a pasta física; ele pode ser um alias.</span><span class="sxs-lookup"><span data-stu-id="80255-376">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="80255-377">(Em servidores de produção, o caminho virtual raramente corresponde a um caminho físico exato.)</span><span class="sxs-lookup"><span data-stu-id="80255-377">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="80255-378">Quando você trabalha com arquivos e pastas no código, às vezes, você precisará referenciar o caminho físico e, às vezes, um caminho virtual, dependendo de quais objetos você está trabalhando com.</span><span class="sxs-lookup"><span data-stu-id="80255-378">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="80255-379">ASP.NET fornece essas ferramentas para trabalhar com caminhos de arquivo e pasta no código: o `Server.MapPath` método e o `~` operador e `Href` método.</span><span class="sxs-lookup"><span data-stu-id="80255-379">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="80255-380">Conversão de caminhos virtuais físicos: o método Server. MapPath</span><span class="sxs-lookup"><span data-stu-id="80255-380">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="80255-381">O `Server.MapPath` método converte um caminho virtual (como */default.cshtml*) em um caminho físico absoluto (como *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="80255-381">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="80255-382">Você usar esse método sempre que precisar de um caminho físico completo.</span><span class="sxs-lookup"><span data-stu-id="80255-382">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="80255-383">Um exemplo típico é quando você estiver lendo ou gravando um arquivo de texto ou arquivo de imagem no servidor web.</span><span class="sxs-lookup"><span data-stu-id="80255-383">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="80255-384">Normalmente você não souber o caminho físico absoluto do seu site no servidor de hospedagem do site, para que esse método possa converter o caminho que você sabe, o caminho virtual — para o caminho correspondente no servidor para você.</span><span class="sxs-lookup"><span data-stu-id="80255-384">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="80255-385">Passe o caminho virtual para um arquivo ou pasta para o método e retorna o caminho físico:</span><span class="sxs-lookup"><span data-stu-id="80255-385">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="80255-386">Fazendo referência a raiz virtual: o ~ operador e o método de Href</span><span class="sxs-lookup"><span data-stu-id="80255-386">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="80255-387">Em um *. cshtml* ou *. vbhtml* arquivo, você pode referenciar o caminho virtual raiz usando o `~` operador.</span><span class="sxs-lookup"><span data-stu-id="80255-387">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="80255-388">Isso é muito útil porque você pode mover páginas em um site, e todos os links para outras páginas contêm não será interrompidos.</span><span class="sxs-lookup"><span data-stu-id="80255-388">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="80255-389">Também é útil caso você nunca move seu site para um local diferente.</span><span class="sxs-lookup"><span data-stu-id="80255-389">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="80255-390">Estes são alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="80255-390">Here are some examples:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

<span data-ttu-id="80255-391">Se o site `http://myserver/myapp`, aqui está como ASP.NET irá tratar esses caminhos quando a página é executada:</span><span class="sxs-lookup"><span data-stu-id="80255-391">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="80255-392">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="80255-392">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="80255-393">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="80255-393">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="80255-394">(Na verdade, você não verá esses caminhos como os valores da variável, mas ASP.NET tratará os caminhos como se isso é o que eles foram).</span><span class="sxs-lookup"><span data-stu-id="80255-394">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="80255-395">Você pode usar o `~` operador no código do servidor (como acima) e na marcação, como este:</span><span class="sxs-lookup"><span data-stu-id="80255-395">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

<span data-ttu-id="80255-396">Na marcação, você deve usar o `~` operador para criar caminhos a recursos como arquivos de imagem, outras páginas da web e arquivos CSS.</span><span class="sxs-lookup"><span data-stu-id="80255-396">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="80255-397">Quando a página é executada, o ASP.NET procura por meio da página (código e marcação) e resolve todos os `~` referências para o caminho apropriado.</span><span class="sxs-lookup"><span data-stu-id="80255-397">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="80255-398">Loops e lógica condicional</span><span class="sxs-lookup"><span data-stu-id="80255-398">Conditional Logic and Loops</span></span>

<span data-ttu-id="80255-399">Código de servidor do ASP.NET permite que você execute tarefas com base nas condições e escrever código que repete instruções um número específico de vezes (ou seja, código que executa um loop).</span><span class="sxs-lookup"><span data-stu-id="80255-399">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times (that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="80255-400">Condições de testes</span><span class="sxs-lookup"><span data-stu-id="80255-400">Testing Conditions</span></span>

<span data-ttu-id="80255-401">Para testar uma condição simple é usar o `if` instrução, que retorna true ou false com base em um teste que você especificar:</span><span class="sxs-lookup"><span data-stu-id="80255-401">To test a simple condition you use the `if` statement, which returns true or false based on a test you specify:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

<span data-ttu-id="80255-402">O `if` palavra-chave inicia um bloco.</span><span class="sxs-lookup"><span data-stu-id="80255-402">The `if` keyword starts a block.</span></span> <span data-ttu-id="80255-403">O teste real (condição) está entre parênteses e retorna true ou false.</span><span class="sxs-lookup"><span data-stu-id="80255-403">The actual test (condition) is in parentheses and returns true or false.</span></span> <span data-ttu-id="80255-404">As instruções que são executados se o teste seja verdadeiro são colocadas entre chaves.</span><span class="sxs-lookup"><span data-stu-id="80255-404">The statements that run if the test is true are enclosed in braces.</span></span> <span data-ttu-id="80255-405">Uma `if` instrução pode incluir um `else` bloco que especifica as instruções a serem executadas se a condição for falsa:</span><span class="sxs-lookup"><span data-stu-id="80255-405">An `if` statement can include an `else` block that specifies statements to run if the condition is false:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

<span data-ttu-id="80255-406">Você pode adicionar várias condições usando um `else if` bloco:</span><span class="sxs-lookup"><span data-stu-id="80255-406">You can add multiple conditions using an `else if` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

<span data-ttu-id="80255-407">Neste exemplo, se a primeira condição na se bloco não for true, o `else if` condição está marcada.</span><span class="sxs-lookup"><span data-stu-id="80255-407">In this example, if the first condition in the if block is not true, the `else if` condition is checked.</span></span> <span data-ttu-id="80255-408">Se essa condição for atendida, as instruções no `else if` bloco são executados.</span><span class="sxs-lookup"><span data-stu-id="80255-408">If that condition is met, the statements in the `else if` block are executed.</span></span> <span data-ttu-id="80255-409">Se nenhuma das condições forem atendidas, as instruções no `else` bloco são executados.</span><span class="sxs-lookup"><span data-stu-id="80255-409">If none of the conditions are met, the statements in the `else` block are executed.</span></span> <span data-ttu-id="80255-410">Você pode adicionar qualquer número de else if bloqueia e, em seguida, fechar com uma `else` bloquear como o &quot;todo o resto&quot; condição.</span><span class="sxs-lookup"><span data-stu-id="80255-410">You can add any number of else if blocks, and then close with an `else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="80255-411">Para testar um grande número de condições, use um `switch` bloco:</span><span class="sxs-lookup"><span data-stu-id="80255-411">To test a large number of conditions, use a `switch` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

<span data-ttu-id="80255-412">O valor a ser testado está entre parênteses (no exemplo, o `weekday` variável).</span><span class="sxs-lookup"><span data-stu-id="80255-412">The value to test is in parentheses (in the example, the `weekday` variable).</span></span> <span data-ttu-id="80255-413">Cada teste individual usa um `case` instrução que termina com dois-pontos (:).</span><span class="sxs-lookup"><span data-stu-id="80255-413">Each individual test uses a `case` statement that ends with a colon (:).</span></span> <span data-ttu-id="80255-414">Se o valor de um `case` instrução corresponde ao valor de teste, o código daquele bloco case é executado.</span><span class="sxs-lookup"><span data-stu-id="80255-414">If the value of a `case` statement matches the test value, the code in that case block is executed.</span></span> <span data-ttu-id="80255-415">Fechar cada instrução case com uma `break` instrução.</span><span class="sxs-lookup"><span data-stu-id="80255-415">You close each case statement with a `break` statement.</span></span> <span data-ttu-id="80255-416">(Se você se esquecer de incluir quebra em cada `case` bloquear, o código do próximo `case` instrução serão executados também.) Um `switch` bloco geralmente tem uma `default` instrução como o último caso de uma &quot;todo o resto&quot; opção que é executado se nenhum dos outros casos forem verdadeiras.</span><span class="sxs-lookup"><span data-stu-id="80255-416">(If you forget to include break in each `case` block, the code from the next `case` statement will run also.) A `switch` block often has a `default` statement as the last case for an &quot;everything else&quot; option that runs if none of the other cases are true.</span></span>

<span data-ttu-id="80255-417">O resultado dos dois últimos blocos condicionais exibido em um navegador:</span><span class="sxs-lookup"><span data-stu-id="80255-417">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="80255-419">Código de loop</span><span class="sxs-lookup"><span data-stu-id="80255-419">Looping Code</span></span>

<span data-ttu-id="80255-420">Geralmente, você precisará executar as mesmas instruções repetidas vezes.</span><span class="sxs-lookup"><span data-stu-id="80255-420">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="80255-421">Você pode fazer isso por meio de loops.</span><span class="sxs-lookup"><span data-stu-id="80255-421">You do this by looping.</span></span> <span data-ttu-id="80255-422">Por exemplo, você sempre execute as mesmas instruções para cada item em uma coleção de dados.</span><span class="sxs-lookup"><span data-stu-id="80255-422">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="80255-423">Se você souber exatamente quantas vezes você deseja executar um loop, você pode usar um `for` loop.</span><span class="sxs-lookup"><span data-stu-id="80255-423">If you know exactly how many times you want to loop, you can use a `for` loop.</span></span> <span data-ttu-id="80255-424">Esse tipo de loop é especialmente útil para de contagem ou contagem regressiva:</span><span class="sxs-lookup"><span data-stu-id="80255-424">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

<span data-ttu-id="80255-425">O loop começa com o `for` palavra-chave, seguido de três instruções entre parênteses, cada encerrada com ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="80255-425">The loop begins with the `for` keyword, followed by three statements in parentheses, each terminated with a semicolon.</span></span>

- <span data-ttu-id="80255-426">Dentro dos parênteses, a primeira instrução (`var i=10;`) cria um contador e o inicializa para 10.</span><span class="sxs-lookup"><span data-stu-id="80255-426">Inside the parentheses, the first statement (`var i=10;`) creates a counter and initializes it to 10.</span></span> <span data-ttu-id="80255-427">Não é necessário nomear o contador `i` &#8212; você pode usar qualquer variável.</span><span class="sxs-lookup"><span data-stu-id="80255-427">You don't have to name the counter `i` &#8212; you can use any variable.</span></span> <span data-ttu-id="80255-428">Quando o `for` loop é executado, o contador é incrementado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="80255-428">When the `for` loop runs, the counter is automatically incremented.</span></span>
- <span data-ttu-id="80255-429">A segunda instrução (`i < 21;`) define a condição para até onde você deseja contar.</span><span class="sxs-lookup"><span data-stu-id="80255-429">The second statement (`i < 21;`) sets the condition for how far you want to count.</span></span> <span data-ttu-id="80255-430">Nesse caso, você deseja que ele vá até um máximo de 20 (ou seja, continue enquanto o contador for menor que 21).</span><span class="sxs-lookup"><span data-stu-id="80255-430">In this case, you want it to go to a maximum of 20 (that is, keep going while the counter is less than 21).</span></span>
- <span data-ttu-id="80255-431">A terceira instrução (`i++` ) usa um operador de incremento, que só especifica que o contador deve ter 1 adicionado a cada vez que o loop é executado.</span><span class="sxs-lookup"><span data-stu-id="80255-431">The third statement (`i++` ) uses an increment operator, which simply specifies that the counter should have 1 added to it each time the loop runs.</span></span>

<span data-ttu-id="80255-432">Dentro das chaves é o código que será executado em cada iteração do loop.</span><span class="sxs-lookup"><span data-stu-id="80255-432">Inside the braces is the code that will run for each iteration of the loop.</span></span> <span data-ttu-id="80255-433">A marcação cria um novo parágrafo (`<p>` elemento) cada vez e adiciona uma linha na saída, exibindo o valor de `i` (o contador).</span><span class="sxs-lookup"><span data-stu-id="80255-433">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of `i` (the counter).</span></span> <span data-ttu-id="80255-434">Quando você executa essa página, o exemplo cria 11 linhas exibindo a saída, com o texto em cada linha que indica o número de item.</span><span class="sxs-lookup"><span data-stu-id="80255-434">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

<span data-ttu-id="80255-436">Se você estiver trabalhando com uma coleção ou matriz, você geralmente usa um `foreach` loop.</span><span class="sxs-lookup"><span data-stu-id="80255-436">If you're working with a collection or array, you often use a `foreach` loop.</span></span> <span data-ttu-id="80255-437">Uma coleção é um grupo de objetos semelhantes e o `foreach` loop permite que você executar uma tarefa em cada item na coleção.</span><span class="sxs-lookup"><span data-stu-id="80255-437">A collection is a group of similar objects, and the `foreach` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="80255-438">Esse tipo de loop é conveniente para coleções, pois ao contrário de um `for` loop, você não precisa incrementar o contador ou definir um limite.</span><span class="sxs-lookup"><span data-stu-id="80255-438">This type of loop is convenient for collections, because unlike a `for` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="80255-439">Em vez disso, o `foreach` loop código simplesmente ocorrerá por meio da coleção, até que ela seja concluída.</span><span class="sxs-lookup"><span data-stu-id="80255-439">Instead, the `foreach` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="80255-440">Por exemplo, o código a seguir retorna os itens a `Request.ServerVariables` coleção, que é um objeto que contém informações sobre seu servidor web.</span><span class="sxs-lookup"><span data-stu-id="80255-440">For example, the following code returns the items in the `Request.ServerVariables` collection, which is an object that contains information about your web server.</span></span> <span data-ttu-id="80255-441">Ele usa um `foreac` loop h para exibir o nome de cada item, criando um novo `<li>` elemento em uma lista com marcadores de HTML.</span><span class="sxs-lookup"><span data-stu-id="80255-441">It uses a `foreac` h loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

<span data-ttu-id="80255-442">O `foreach` palavra-chave é seguido por parênteses, em que você declare uma variável que representa um único item na coleção (no exemplo, `var item`), seguido pelo `in` palavra-chave, seguido pela coleção que você deseja fazer o loop.</span><span class="sxs-lookup"><span data-stu-id="80255-442">The `foreach` keyword is followed by parentheses where you declare a variable that represents a single item in the collection (in the example, `var item`), followed by the `in` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="80255-443">No corpo do `foreach` loop, você pode acessar o item atual usando a variável declarada anteriormente por você.</span><span class="sxs-lookup"><span data-stu-id="80255-443">In the body of the `foreach` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

<span data-ttu-id="80255-445">Para criar um loop de propósito mais geral, use o `while` instrução:</span><span class="sxs-lookup"><span data-stu-id="80255-445">To create a more general-purpose loop, use the `while` statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

<span data-ttu-id="80255-446">Um `while` loop começa com o `while` palavra-chave, seguido por parênteses, onde você especifica por quanto tempo o loop continua (aqui, para desde que `countNum` é menor que 50), em seguida, o bloco de repetir.</span><span class="sxs-lookup"><span data-stu-id="80255-446">A `while` loop begins with the `while` keyword, followed by parentheses where you specify how long the loop continues (here, for as long as `countNum` is less than 50), then the block to repeat.</span></span> <span data-ttu-id="80255-447">Loops normalmente incrementam (Adicionar ao) ou decrementar (subtrair de) uma variável ou um objeto usado para contagem.</span><span class="sxs-lookup"><span data-stu-id="80255-447">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="80255-448">No exemplo, o `+=` operador adiciona 1 ao `countNum` cada vez que o loop é executado.</span><span class="sxs-lookup"><span data-stu-id="80255-448">In the example, the `+=` operator adds 1 to `countNum` each time the loop runs.</span></span> <span data-ttu-id="80255-449">(Para diminuir a uma variável em um loop de contagem regressiva, você usaria o operador de decremento `-=`).</span><span class="sxs-lookup"><span data-stu-id="80255-449">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`).</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="80255-450">Objetos e coleções</span><span class="sxs-lookup"><span data-stu-id="80255-450">Objects and Collections</span></span>

<span data-ttu-id="80255-451">Quase tudo em um site ASP.NET é um objeto, incluindo a própria página da web.</span><span class="sxs-lookup"><span data-stu-id="80255-451">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="80255-452">Esta seção discute alguns objetos importantes que você trabalhará com frequência em seu código.</span><span class="sxs-lookup"><span data-stu-id="80255-452">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="80255-453">Objetos de página</span><span class="sxs-lookup"><span data-stu-id="80255-453">Page Objects</span></span>

<span data-ttu-id="80255-454">O objeto mais básico no ASP.NET é a página.</span><span class="sxs-lookup"><span data-stu-id="80255-454">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="80255-455">Você pode acessar as propriedades do objeto page diretamente sem qualquer objeto qualificado.</span><span class="sxs-lookup"><span data-stu-id="80255-455">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="80255-456">O código a seguir obtém o caminho do arquivo da página, usando o `Request` objeto da página:</span><span class="sxs-lookup"><span data-stu-id="80255-456">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

<span data-ttu-id="80255-457">Para torná-lo claro que você está fazendo referência a propriedades e métodos no objeto da página atual, você pode usar a palavra-chave `this` para representar o objeto de página em seu código.</span><span class="sxs-lookup"><span data-stu-id="80255-457">To make it clear that you're referencing properties and methods on the current page object, you can optionally use the keyword `this` to represent the page object in your code.</span></span> <span data-ttu-id="80255-458">Aqui está o exemplo de código anterior, com `this` adicionado para representar a página:</span><span class="sxs-lookup"><span data-stu-id="80255-458">Here is the previous code example, with `this` added to represent the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

<span data-ttu-id="80255-459">Você pode usar propriedades do `Page` objeto do qual obter muitas informações, tais como:</span><span class="sxs-lookup"><span data-stu-id="80255-459">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="80255-460">`Request`.</span><span class="sxs-lookup"><span data-stu-id="80255-460">`Request`.</span></span> <span data-ttu-id="80255-461">Como você já viu, esta é uma coleção de informações sobre a solicitação atual, incluindo o tipo de navegador fez a solicitação, a URL da página, a identidade do usuário, etc.</span><span class="sxs-lookup"><span data-stu-id="80255-461">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="80255-462">`Response`.</span><span class="sxs-lookup"><span data-stu-id="80255-462">`Response`.</span></span> <span data-ttu-id="80255-463">Esta é uma coleção de informações sobre a resposta (página) que será enviada ao navegador quando o código de servidor concluiu a execução.</span><span class="sxs-lookup"><span data-stu-id="80255-463">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="80255-464">Por exemplo, você pode usar essa propriedade para gravar informações na resposta.</span><span class="sxs-lookup"><span data-stu-id="80255-464">For example, you can use this property to write information into the response.</span></span> 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="80255-465">Objetos de coleção (matrizes e dicionários)</span><span class="sxs-lookup"><span data-stu-id="80255-465">Collection Objects (Arrays and Dictionaries)</span></span>

<span data-ttu-id="80255-466">Um *coleta* é um grupo de objetos do mesmo tipo, como uma coleção de `Customer` objetos de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="80255-466">A *collection* is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="80255-467">ASP.NET contém várias coleções internas, como o `Request.Files` coleção.</span><span class="sxs-lookup"><span data-stu-id="80255-467">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="80255-468">Geralmente, você trabalhará com dados em coleções.</span><span class="sxs-lookup"><span data-stu-id="80255-468">You'll often work with data in collections.</span></span> <span data-ttu-id="80255-469">Dois tipos de coleção comuns são as *array* e o *dicionário*.</span><span class="sxs-lookup"><span data-stu-id="80255-469">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="80255-470">Uma matriz é útil quando você deseja armazenar uma coleção de itens semelhantes, mas não quiser criar uma variável separada para manter cada item:</span><span class="sxs-lookup"><span data-stu-id="80255-470">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

<span data-ttu-id="80255-471">Com matrizes, você declara um tipo de dados específico, como `string`, `int`, ou `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="80255-471">With arrays, you declare a specific data type, such as `string`, `int`, or `DateTime`.</span></span> <span data-ttu-id="80255-472">Para indicar que a variável pode conter uma matriz, adicione parênteses para a declaração (como `string[]` ou `int[]`).</span><span class="sxs-lookup"><span data-stu-id="80255-472">To indicate that the variable can contain an array, you add brackets to the declaration (such as `string[]` or `int[]`).</span></span> <span data-ttu-id="80255-473">Você pode acessar itens em uma matriz usando sua posição (índice) ou usando o `foreach` instrução.</span><span class="sxs-lookup"><span data-stu-id="80255-473">You can access items in an array using their position (index) or by using the `foreach` statement.</span></span> <span data-ttu-id="80255-474">Índices de matriz são baseados em zero &#8212; ou seja, o primeiro item está na posição 0, o segundo item estiver na posição 1 e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="80255-474">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

<span data-ttu-id="80255-475">Você pode determinar o número de itens em uma matriz obtendo sua `Length` propriedade.</span><span class="sxs-lookup"><span data-stu-id="80255-475">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="80255-476">Para obter a posição de um item específico na matriz (para pesquisar a matriz), use o `Array.IndexOf` método.</span><span class="sxs-lookup"><span data-stu-id="80255-476">To get the position of a specific item in the array (to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="80255-477">Você também pode fazer coisas como reverter o conteúdo de uma matriz (o `Array.Reverse` método) ou classificar o conteúdo (o `Array.Sort` método).</span><span class="sxs-lookup"><span data-stu-id="80255-477">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="80255-478">A saída do código de matriz de cadeia de caracteres exibido em um navegador:</span><span class="sxs-lookup"><span data-stu-id="80255-478">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

<span data-ttu-id="80255-480">Um dicionário é uma coleção de pares chave/valor, em que você fornece a chave (ou nome) para definir ou recuperar o valor correspondente:</span><span class="sxs-lookup"><span data-stu-id="80255-480">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

<span data-ttu-id="80255-481">Para criar um dicionário, você deve usar o `new` palavra-chave para indicar que você está criando um novo objeto de dicionário.</span><span class="sxs-lookup"><span data-stu-id="80255-481">To create a dictionary, you use the `new` keyword to indicate that you're creating a new dictionary object.</span></span> <span data-ttu-id="80255-482">Você pode atribuir um dicionário para uma variável usando o `var` palavra-chave.</span><span class="sxs-lookup"><span data-stu-id="80255-482">You can assign a dictionary to a variable using the `var` keyword.</span></span> <span data-ttu-id="80255-483">Você indica os tipos de dados dos itens no dicionário usando colchetes angulares ( `< >` ).</span><span class="sxs-lookup"><span data-stu-id="80255-483">You indicate the data types of the items in the dictionary using angle brackets ( `< >` ).</span></span> <span data-ttu-id="80255-484">No final da declaração, você deve adicionar um par de parênteses, porque isso é, na verdade, um método que cria um novo dicionário.</span><span class="sxs-lookup"><span data-stu-id="80255-484">At the end of the declaration, you must add a pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="80255-485">Para adicionar itens ao dicionário, você pode chamar o `Add` método da variável de dicionário (`myScores` nesse caso) e, em seguida, especifique uma chave e um valor.</span><span class="sxs-lookup"><span data-stu-id="80255-485">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="80255-486">Como alternativa, você pode usar colchetes para indicar a chave e fazer uma simples atribuição, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="80255-486">Alternatively, you can use square brackets to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

<span data-ttu-id="80255-487">Para obter um valor do dicionário, você pode especificar a chave entre colchetes:</span><span class="sxs-lookup"><span data-stu-id="80255-487">To get a value from the dictionary, you specify the key in brackets:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="80255-488">Chamar métodos com parâmetros</span><span class="sxs-lookup"><span data-stu-id="80255-488">Calling Methods with Parameters</span></span>

<span data-ttu-id="80255-489">Ao ler no início deste artigo, os objetos que você programa com podem ter métodos.</span><span class="sxs-lookup"><span data-stu-id="80255-489">As you read earlier in this article, the objects that you program with can have methods.</span></span> <span data-ttu-id="80255-490">Por exemplo, uma `Database` objeto pode ter um `Database.Connect` método.</span><span class="sxs-lookup"><span data-stu-id="80255-490">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="80255-491">Muitos métodos também tem um ou mais parâmetros.</span><span class="sxs-lookup"><span data-stu-id="80255-491">Many methods also have one or more parameters.</span></span> <span data-ttu-id="80255-492">Um *parâmetro* é um valor que você passa para um método para habilitar o método concluir a tarefa.</span><span class="sxs-lookup"><span data-stu-id="80255-492">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="80255-493">Por exemplo, examinar uma declaração para o `Request.MapPath` método, que usa três parâmetros:</span><span class="sxs-lookup"><span data-stu-id="80255-493">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

<span data-ttu-id="80255-494">(A linha foi encapsulada para torná-lo mais legível.</span><span class="sxs-lookup"><span data-stu-id="80255-494">(The line has been wrapped to make it more readable.</span></span> <span data-ttu-id="80255-495">Lembre-se de que você pode colocar quebras de linha quase qualquer lugar exceto inside cadeias de caracteres que são colocados entre aspas.)</span><span class="sxs-lookup"><span data-stu-id="80255-495">Remember that you can put line breaks almost any place except inside strings that are enclosed in quotation marks.)</span></span>

<span data-ttu-id="80255-496">Esse método retorna o caminho físico no servidor que corresponde a um caminho virtual especificado.</span><span class="sxs-lookup"><span data-stu-id="80255-496">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="80255-497">Os três parâmetros para o método são `virtualPath`, `baseVirtualDir`, e `allowCrossAppMapping`.</span><span class="sxs-lookup"><span data-stu-id="80255-497">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="80255-498">(Observe que na declaração, os parâmetros são listados com os tipos de dados dos dados que ele aceitará.) Quando você chama esse método, você deve fornecer valores para todos os três parâmetros.</span><span class="sxs-lookup"><span data-stu-id="80255-498">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="80255-499">A sintaxe do Razor oferece duas opções para passar parâmetros para um método: *parâmetros posicionais* e *parâmetros nomeados*.</span><span class="sxs-lookup"><span data-stu-id="80255-499">The Razor syntax gives you two options for passing parameters to a method: *positional parameters* and *named parameters*.</span></span> <span data-ttu-id="80255-500">Para chamar um método usando parâmetros posicionais, você pode passar os parâmetros em uma ordem estrita que é especificada na declaração de método.</span><span class="sxs-lookup"><span data-stu-id="80255-500">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="80255-501">(Você normalmente saberia nesta ordem, lendo a documentação do método.) Você deve seguir a ordem, e você não pode ignorar qualquer um dos parâmetros &#8212; se necessário, você passa uma cadeia de caracteres vazia (`""`) ou `null` para um parâmetro posicional que você não tiver um valor para.</span><span class="sxs-lookup"><span data-stu-id="80255-501">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or `null` for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="80255-502">O exemplo a seguir pressupõe que você tem uma pasta chamada *scripts* em seu site.</span><span class="sxs-lookup"><span data-stu-id="80255-502">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="80255-503">O código chama o `Request.MapPath` e passa valores para os três parâmetros na ordem correta.</span><span class="sxs-lookup"><span data-stu-id="80255-503">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="80255-504">Ele, em seguida, exibe o caminho de mapeada resultante.</span><span class="sxs-lookup"><span data-stu-id="80255-504">It then displays the resulting mapped path.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

<span data-ttu-id="80255-505">Quando um método tem muitos parâmetros, você pode manter seu código mais legível usando parâmetros nomeados.</span><span class="sxs-lookup"><span data-stu-id="80255-505">When a method has many parameters, you can keep your code more readable by using named parameters.</span></span> <span data-ttu-id="80255-506">Para chamar um método usando parâmetros nomeados, você especifica o nome do parâmetro seguido por dois-pontos (:) e, em seguida, o valor.</span><span class="sxs-lookup"><span data-stu-id="80255-506">To call a method using named parameters, you specify the parameter name followed by a colon (:), and then the value.</span></span> <span data-ttu-id="80255-507">A vantagem dos parâmetros nomeados é que você pode passá-los em qualquer ordem desejada.</span><span class="sxs-lookup"><span data-stu-id="80255-507">The advantage of named parameters is that you can pass them in any order you want.</span></span> <span data-ttu-id="80255-508">(Uma desvantagem é que a chamada de método não é mais compacta.)</span><span class="sxs-lookup"><span data-stu-id="80255-508">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="80255-509">O exemplo a seguir chama o método acima, mas usa parâmetros para fornecer os valores nomeados:</span><span class="sxs-lookup"><span data-stu-id="80255-509">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

<span data-ttu-id="80255-510">Como você pode ver, os parâmetros são passados em uma ordem diferente.</span><span class="sxs-lookup"><span data-stu-id="80255-510">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="80255-511">No entanto, se você executar o exemplo anterior e este exemplo, eles retornar o mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="80255-511">However, if you run the previous example and this example, they'll return the same value.</span></span>

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a><span data-ttu-id="80255-512">Manipulando erros</span><span class="sxs-lookup"><span data-stu-id="80255-512">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="80255-513">Instruções Try-Catch</span><span class="sxs-lookup"><span data-stu-id="80255-513">Try-Catch Statements</span></span>

<span data-ttu-id="80255-514">Geralmente, você terá as instruções em seu código que pode falhar por razões de fora do seu controle.</span><span class="sxs-lookup"><span data-stu-id="80255-514">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="80255-515">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="80255-515">For example:</span></span>

- <span data-ttu-id="80255-516">Se seu código tentar criar ou acessar um arquivo, todos os tipos de erros podem ocorrer.</span><span class="sxs-lookup"><span data-stu-id="80255-516">If your code tries to create or access a file, all sorts of errors might occur.</span></span> <span data-ttu-id="80255-517">O arquivo que você deseja que pode não existir, ele pode ter sido bloqueado, o código pode não ter permissões e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="80255-517">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="80255-518">Da mesma forma, se seu código tenta atualizar registros em um banco de dados, pode haver problemas de permissões, a conexão ao banco de dados pode ser descartado, os dados para salvar podem estar inválido e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="80255-518">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="80255-519">Em termos de programação, essas situações são chamadas *exceções*.</span><span class="sxs-lookup"><span data-stu-id="80255-519">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="80255-520">Se seu código encontrar uma exceção, ele gera (gera) uma mensagem de erro que está, na melhor das hipóteses, irritantes aos usuários:</span><span class="sxs-lookup"><span data-stu-id="80255-520">If your code encounters an exception, it generates (throws) an error message that's, at best, annoying to users:</span></span>

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

<span data-ttu-id="80255-522">Em situações em que seu código poderá encontrar exceções e para evitar mensagens de erro desse tipo, você pode usar `try/catch` instruções.</span><span class="sxs-lookup"><span data-stu-id="80255-522">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `try/catch` statements.</span></span> <span data-ttu-id="80255-523">No `try` instrução, que você executa o código que você está verificando.</span><span class="sxs-lookup"><span data-stu-id="80255-523">In the `try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="80255-524">Em uma ou mais `catch` instruções, você pode procurar específicos de erros (tipos específicos de exceções) que possam ter ocorrido.</span><span class="sxs-lookup"><span data-stu-id="80255-524">In one or more `catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="80255-525">Você pode incluir tantos `catch` instruções que você precisam procurar por erros que você está prevendo.</span><span class="sxs-lookup"><span data-stu-id="80255-525">You can include as many `catch` statements as you need to look for errors that you are anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="80255-526">É recomendável que você evite usar o `Response.Redirect` método no `try/catch` instruções, porque isso pode causar uma exceção em sua página.</span><span class="sxs-lookup"><span data-stu-id="80255-526">We recommend that you avoid using the `Response.Redirect` method in `try/catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="80255-527">O exemplo a seguir mostra uma página que cria um arquivo de texto na primeira solicitação e, em seguida, exibe um botão que permite que o usuário abrir o arquivo.</span><span class="sxs-lookup"><span data-stu-id="80255-527">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="80255-528">O exemplo deliberadamente usa um nome de arquivo incorreto para que ela fará com que uma exceção.</span><span class="sxs-lookup"><span data-stu-id="80255-528">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="80255-529">O código inclui `catch` instruções para duas exceções possíveis: `FileNotFoundException`, que ocorre se o nome do arquivo é ruim, e `DirectoryNotFoundException`, que ocorre se o ASP.NET ainda não é possível localizar a pasta.</span><span class="sxs-lookup"><span data-stu-id="80255-529">The code includes `catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="80255-530">(Você pode remover o comentário uma instrução no exemplo a fim de ver como ele é executado quando tudo está funcionando corretamente.)</span><span class="sxs-lookup"><span data-stu-id="80255-530">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="80255-531">Se seu código não trata a exceção, você verá uma página de erro, como a captura de tela anterior.</span><span class="sxs-lookup"><span data-stu-id="80255-531">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="80255-532">No entanto, o `try/catch` seção ajuda a impedir que o usuário ver esses tipos de erros.</span><span class="sxs-lookup"><span data-stu-id="80255-532">However, the `try/catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="80255-533">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="80255-533">Additional Resources</span></span>

<span data-ttu-id="80255-534">**Programação com o Visual Basic**</span><span class="sxs-lookup"><span data-stu-id="80255-534">**Programming with Visual Basic**</span></span>

[<span data-ttu-id="80255-535">Apêndice: Sintaxe e a linguagem Visual Basic</span><span class="sxs-lookup"><span data-stu-id="80255-535">Appendix: Visual Basic Language and Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkId=202908)

<span data-ttu-id="80255-536">**Documentação de referência**</span><span class="sxs-lookup"><span data-stu-id="80255-536">**Reference Documentation**</span></span>

[<span data-ttu-id="80255-537">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="80255-537">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)

[<span data-ttu-id="80255-538">Linguagem c#</span><span class="sxs-lookup"><span data-stu-id="80255-538">C# Language</span></span>](https://msdn.microsoft.com/library/kx37x362.aspx)
