---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
title: Associação de dados com um Accordion (VB) | Microsoft Docs
author: wenz
description: O controle Accordion no AJAX Control Toolkit fornece vários painéis e permite que o usuário exibir um por vez. Painéis são normalmente declaradas w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b19f0875-7d3e-4ecf-baa1-a0c693c765b3
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
msc.type: authoredcontent
ms.openlocfilehash: 948741e3b8618a642c440a527fddef825faf595e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050803"
---
<a name="databinding-to-an-accordion-vb"></a><span data-ttu-id="e35ee-104">Associação de Dados com um Accordion (VB)</span><span class="sxs-lookup"><span data-stu-id="e35ee-104">Databinding to an Accordion (VB)</span></span>
====================
<span data-ttu-id="e35ee-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="e35ee-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e35ee-106">[Baixar o código](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) ou [baixar PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="e35ee-106">[Download Code](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)</span></span>

> <span data-ttu-id="e35ee-107">O controle Accordion no AJAX Control Toolkit fornece vários painéis e permite que o usuário exibir um por vez.</span><span class="sxs-lookup"><span data-stu-id="e35ee-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="e35ee-108">Painéis geralmente são declarados dentro da página em si, mas a associação a uma fonte de dados oferece mais flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="e35ee-108">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>


## <a name="overview"></a><span data-ttu-id="e35ee-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e35ee-109">Overview</span></span>

<span data-ttu-id="e35ee-110">O controle Accordion no AJAX Control Toolkit fornece vários painéis e permite que o usuário exibir um por vez.</span><span class="sxs-lookup"><span data-stu-id="e35ee-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="e35ee-111">Painéis geralmente são declarados dentro da página em si, mas a associação a uma fonte de dados oferece mais flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="e35ee-111">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="e35ee-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="e35ee-112">Steps</span></span>

<span data-ttu-id="e35ee-113">Em primeiro lugar, uma fonte de dados é necessária.</span><span class="sxs-lookup"><span data-stu-id="e35ee-113">First of all, a data source is required.</span></span> <span data-ttu-id="e35ee-114">Este exemplo usa o banco de dados AdventureWorks e o Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="e35ee-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="e35ee-115">O banco de dados é uma parte opcional da instalação do Visual Studio (inclusive a express edition) e também está disponível como um download separado em [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="e35ee-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="e35ee-116">O banco de dados AdventureWorks é parte do SQL Server 2005 exemplos e bancos de dados de exemplo (download em [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="e35ee-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="e35ee-117">A maneira mais fácil de configurar o banco de dados é usar o Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) e anexe o `AdventureWorks.mdf` arquivo de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e35ee-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="e35ee-118">Para este exemplo, vamos supor que a instância do SQL Server 2005 Express Edition é chamada `SQLEXPRESS` e reside no mesmo computador que o servidor web; isso também é a configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="e35ee-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="e35ee-119">Se sua configuração for diferente, você precisa adaptar as informações de conexão para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e35ee-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="e35ee-120">Para ativar a funcionalidade do AJAX ASP.NET e o Kit de ferramentas de controle, o `ScriptManager` controle deve ser colocada em qualquer lugar na página (mas dentro de `<form>` elemento):</span><span class="sxs-lookup"><span data-stu-id="e35ee-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample1.aspx)]

<span data-ttu-id="e35ee-121">Em seguida, adicione uma fonte de dados para a página.</span><span class="sxs-lookup"><span data-stu-id="e35ee-121">Then, add a data source to the page.</span></span> <span data-ttu-id="e35ee-122">Para usar uma quantidade limitada de dados, vamos selecionar apenas as primeiras cinco entradas na tabela de fornecedores de banco de dados AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="e35ee-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="e35ee-123">Se você estiver usando o Assistente do Visual Studio para criar a fonte de dados, lembre-se de que um bug na versão atual não prefixar o nome da tabela (`Vendor`) com `Purchasing`.</span><span class="sxs-lookup"><span data-stu-id="e35ee-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="e35ee-124">A marcação a seguir mostra a sintaxe correta:</span><span class="sxs-lookup"><span data-stu-id="e35ee-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample2.aspx)]

<span data-ttu-id="e35ee-125">Lembre-se o nome (ID) da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="e35ee-125">Remember the name (ID) of the data source.</span></span> <span data-ttu-id="e35ee-126">Essa identificação muita deve ser usada no `DataSourceID` propriedade do controle Accordion:</span><span class="sxs-lookup"><span data-stu-id="e35ee-126">This very identification must then be used in the `DataSourceID` property of the Accordion control:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample3.aspx)]

<span data-ttu-id="e35ee-127">Dentro do controle Accordion, você pode fornecer modelos para várias partes do controle, incluindo o cabeçalho (`<HeaderTemplate>`) e o conteúdo (`<ContentTemplate>`).</span><span class="sxs-lookup"><span data-stu-id="e35ee-127">Within the Accordion control, you can provide templates for various parts of the control, including the header (`<HeaderTemplate>`) and the content (`<ContentTemplate>`).</span></span> <span data-ttu-id="e35ee-128">Dentro desses elementos, apenas dados de saída os partir dos dados de origem, usando o `DataBinder.Eval()` método:</span><span class="sxs-lookup"><span data-stu-id="e35ee-128">Within these elements, just output the data from the data source, using the `DataBinder.Eval()` method:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample4.aspx)]

<span data-ttu-id="e35ee-129">Quando a página é carregada, a fonte de dados deve ser vinculada a Acordeão com esse código do lado do servidor:</span><span class="sxs-lookup"><span data-stu-id="e35ee-129">When the page is loaded, the data source must be bound to the accordion with this server-side code:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample5.aspx)]

<span data-ttu-id="e35ee-130">Para concluir este exemplo, você precisa definir as duas classes CSS que são referenciadas no controle Accordion (em suas propriedades `HeaderCssClass` e `ContentCssClass`).</span><span class="sxs-lookup"><span data-stu-id="e35ee-130">To conclude this sample, you need to define the two CSS classes that are referenced in the Accordion control (in its properties `HeaderCssClass` and `ContentCssClass`).</span></span> <span data-ttu-id="e35ee-131">Coloque a seguinte marcação no `<head>` seção da página:</span><span class="sxs-lookup"><span data-stu-id="e35ee-131">Put the following markup in the `<head>` section of the page:</span></span>

[!code-css[Main](databinding-to-an-accordion-vb/samples/sample6.css)]


<span data-ttu-id="e35ee-132">[![Os dados no acordeão vêm diretamente da fonte de dados](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e35ee-132">[![The data in the accordion comes directly from the data source](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)</span></span>

<span data-ttu-id="e35ee-133">Os dados no acordeão vêm diretamente da fonte de dados ([clique para exibir a imagem em tamanho normal](databinding-to-an-accordion-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e35ee-133">The data in the accordion comes directly from the data source ([Click to view full-size image](databinding-to-an-accordion-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e35ee-134">[Anterior](dynamically-adding-an-accordion-pane-cs.md)
> [Próximo](dynamically-adding-an-accordion-pane-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e35ee-134">[Previous](dynamically-adding-an-accordion-pane-cs.md)
[Next](dynamically-adding-an-accordion-pane-vb.md)</span></span>
