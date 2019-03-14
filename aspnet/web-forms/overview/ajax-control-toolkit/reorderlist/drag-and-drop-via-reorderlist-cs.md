---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
title: Arrastar e soltar por meio de ReorderList (c#) | Microsoft Docs
author: wenz
description: O controle ReorderList no AJAX Control Toolkit fornece uma lista que pode ser reordenada por usuário por meio de arrastar e soltar. O pedido atual da lista deverá...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6350ee8e-11d6-4aff-b51c-942878014835
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 15ae6ae60381f3f656f667a97dac72dbb283c80e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035023"
---
<a name="drag-and-drop-via-reorderlist-c"></a><span data-ttu-id="e83d3-104">Arrastar e soltar por meio de ReorderList (C#)</span><span class="sxs-lookup"><span data-stu-id="e83d3-104">Drag and Drop via ReorderList (C#)</span></span>
====================
<span data-ttu-id="e83d3-105">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="e83d3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e83d3-106">[Baixar o código](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="e83d3-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)</span></span>

> <span data-ttu-id="e83d3-107">O controle ReorderList no AJAX Control Toolkit fornece uma lista que pode ser reordenada por usuário por meio de arrastar e soltar.</span><span class="sxs-lookup"><span data-stu-id="e83d3-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="e83d3-108">O pedido atual da lista deverá ser persistente no servidor.</span><span class="sxs-lookup"><span data-stu-id="e83d3-108">The current order of the list shall be persisted on the server.</span></span>


## <a name="overview"></a><span data-ttu-id="e83d3-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e83d3-109">Overview</span></span>

<span data-ttu-id="e83d3-110">O `ReorderList` controle no AJAX Control Toolkit fornece uma lista que pode ser reordenada por usuário por meio de arrastar e soltar.</span><span class="sxs-lookup"><span data-stu-id="e83d3-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="e83d3-111">O pedido atual da lista deverá ser persistente no servidor.</span><span class="sxs-lookup"><span data-stu-id="e83d3-111">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="e83d3-112">Etapas</span><span class="sxs-lookup"><span data-stu-id="e83d3-112">Steps</span></span>

<span data-ttu-id="e83d3-113">O `ReorderList` controle dá suporte à associação de dados de um banco de dados à lista.</span><span class="sxs-lookup"><span data-stu-id="e83d3-113">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="e83d3-114">O melhor de tudo, ele também suporta gravando alterações consecutivos o elemento da lista para o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="e83d3-114">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="e83d3-115">Este exemplo usa o Microsoft SQL Server 2005 Express Edition como armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="e83d3-115">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="e83d3-116">O banco de dados é uma parte opcional (e gratuita) de uma instalação do Visual Studio, incluindo a express edition.</span><span class="sxs-lookup"><span data-stu-id="e83d3-116">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="e83d3-117">Ele também está disponível como um download separado em [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="e83d3-117">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="e83d3-118">Para este exemplo, vamos supor que a instância do SQL Server 2005 Express Edition é chamada `SQLEXPRESS` e reside no mesmo computador que o servidor web; isso também é a configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="e83d3-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="e83d3-119">Se sua configuração for diferente, você precisa adaptar as informações de conexão para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e83d3-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="e83d3-120">A maneira mais fácil de configurar o banco de dados é usar o Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span><span class="sxs-lookup"><span data-stu-id="e83d3-120">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="e83d3-121">Conecte-se ao servidor, clique duas vezes em `Databases` e crie um novo banco de dados (com o botão direito e escolha `New Database`) chamado `Tutorials`.</span><span class="sxs-lookup"><span data-stu-id="e83d3-121">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="e83d3-122">Neste banco de dados, criar uma nova tabela chamada `AJAX` com as seguintes quatro colunas:</span><span class="sxs-lookup"><span data-stu-id="e83d3-122">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="e83d3-123">`id` (inteiro de chave, primário, identidade, not NULL)</span><span class="sxs-lookup"><span data-stu-id="e83d3-123">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="e83d3-124">`char` (char(1), NULL)</span><span class="sxs-lookup"><span data-stu-id="e83d3-124">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="e83d3-125">`description` (varchar(50), NULL)</span><span class="sxs-lookup"><span data-stu-id="e83d3-125">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="e83d3-126">`position` NULL (int)</span><span class="sxs-lookup"><span data-stu-id="e83d3-126">`position` (int, NULL)</span></span>


<span data-ttu-id="e83d3-127">[![O layout da tabela AJAX](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e83d3-127">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="e83d3-128">O layout da tabela AJAX ([clique para exibir a imagem em tamanho normal](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e83d3-128">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image3.png))</span></span>


<span data-ttu-id="e83d3-129">Em seguida, preencha a tabela com um par de valores.</span><span class="sxs-lookup"><span data-stu-id="e83d3-129">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="e83d3-130">Observe que o `position` coluna mantém a ordem de classificação dos elementos.</span><span class="sxs-lookup"><span data-stu-id="e83d3-130">Note that the `position` column holds the sort order of the elements.</span></span>


<span data-ttu-id="e83d3-131">[![Os dados iniciais na tabela de AJAX](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="e83d3-131">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)</span></span>

<span data-ttu-id="e83d3-132">Os dados iniciais na tabela de AJAX ([clique para exibir a imagem em tamanho normal](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="e83d3-132">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image6.png))</span></span>


<span data-ttu-id="e83d3-133">A próxima etapa requer para gerar um `SqlDataSource` controle para se comunicar com o novo banco de dados e sua tabela.</span><span class="sxs-lookup"><span data-stu-id="e83d3-133">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="e83d3-134">A fonte de dados deve dar suporte a `SELECT` e `UPDATE` comandos SQL.</span><span class="sxs-lookup"><span data-stu-id="e83d3-134">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="e83d3-135">Quando a ordem dos elementos de lista for alterada posteriormente, o `ReorderList` controle envia automaticamente os dois valores para a fonte de dados `Update` comando: a nova posição e a ID do elemento.</span><span class="sxs-lookup"><span data-stu-id="e83d3-135">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="e83d3-136">Portanto, a fonte de dados necessidades um `<UpdateParameters>` seção para esses dois valores:</span><span class="sxs-lookup"><span data-stu-id="e83d3-136">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="e83d3-137">O `ReorderList` controle precisa definir os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="e83d3-137">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="e83d3-138">`AllowReorder`: Se os itens da lista podem ser reorganizados</span><span class="sxs-lookup"><span data-stu-id="e83d3-138">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="e83d3-139">`DataSourceID`: A ID da fonte de dados</span><span class="sxs-lookup"><span data-stu-id="e83d3-139">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="e83d3-140">`DataKeyField`: O nome da coluna de chave primária na fonte de dados</span><span class="sxs-lookup"><span data-stu-id="e83d3-140">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="e83d3-141">`SortOrderField`: A coluna de fonte de dados que fornece a ordem de classificação para os itens de lista</span><span class="sxs-lookup"><span data-stu-id="e83d3-141">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="e83d3-142">No `<DragHandleTemplate>` e `<ItemTemplate>` seções, o layout da lista pode ser ajustado.</span><span class="sxs-lookup"><span data-stu-id="e83d3-142">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="e83d3-143">Além disso, a associação de dados é possível usar o `Eval()` método, como visto aqui:</span><span class="sxs-lookup"><span data-stu-id="e83d3-143">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="e83d3-144">Informações de estilo CSS a seguir (referenciado na `<DragHandleTemplate>` seção o `ReorderList` controle) torna-se de que o ponteiro do mouse muda adequadamente quando ele passa o mouse sobre a alça de arraste:</span><span class="sxs-lookup"><span data-stu-id="e83d3-144">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

<span data-ttu-id="e83d3-145">Por fim, um `ScriptManager` controle inicializa o ASP.NET AJAX para a página:</span><span class="sxs-lookup"><span data-stu-id="e83d3-145">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="e83d3-146">Executar este exemplo no navegador e reorganizar os itens da lista um pouco.</span><span class="sxs-lookup"><span data-stu-id="e83d3-146">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="e83d3-147">Em seguida, recarregue a página e/ou dar uma olhada no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e83d3-147">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="e83d3-148">As posições alteradas ter sido mantidas e também são refletidas pelos valores no `position` coluna no banco de dados e que tudo isso sem qualquer código, apenas usando marcação.</span><span class="sxs-lookup"><span data-stu-id="e83d3-148">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>


<span data-ttu-id="e83d3-149">[![Os dados em que as alterações de banco de dados de acordo com a nova ordem de item de lista](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="e83d3-149">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)</span></span>

<span data-ttu-id="e83d3-150">Os dados em que as alterações de banco de dados de acordo com a nova lista de ordem de item ([clique para exibir a imagem em tamanho normal](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="e83d3-150">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-cs/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e83d3-151">[Anterior](using-postbacks-with-reorderlist-cs.md)
> [Próximo](using-postbacks-with-reorderlist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e83d3-151">[Previous](using-postbacks-with-reorderlist-cs.md)
[Next](using-postbacks-with-reorderlist-vb.md)</span></span>
