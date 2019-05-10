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
ms.openlocfilehash: 8adeceba0d43d6baf1af944a910750ca0682b097
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65124926"
---
# <a name="drag-and-drop-via-reorderlist-c"></a>Arrastar e soltar por meio de ReorderList (C#)

por [Christian Wenz](https://github.com/wenz)

[Baixar o código](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)

> O controle ReorderList no AJAX Control Toolkit fornece uma lista que pode ser reordenada por usuário por meio de arrastar e soltar. O pedido atual da lista deverá ser persistente no servidor.

## <a name="overview"></a>Visão geral

O `ReorderList` controle no AJAX Control Toolkit fornece uma lista que pode ser reordenada por usuário por meio de arrastar e soltar. O pedido atual da lista deverá ser persistente no servidor.

## <a name="steps"></a>Etapas

O `ReorderList` controle dá suporte à associação de dados de um banco de dados à lista. O melhor de tudo, ele também suporta gravando alterações consecutivos o elemento da lista para o armazenamento de dados.

Este exemplo usa o Microsoft SQL Server 2005 Express Edition como armazenamento de dados. O banco de dados é uma parte opcional (e gratuita) de uma instalação do Visual Studio, incluindo a express edition. Ele também está disponível como um download separado em [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064). Para este exemplo, vamos supor que a instância do SQL Server 2005 Express Edition é chamada `SQLEXPRESS` e reside no mesmo computador que o servidor web; isso também é a configuração padrão. Se sua configuração for diferente, você precisa adaptar as informações de conexão para o banco de dados.

A maneira mais fácil de configurar o banco de dados é usar o Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ). Conecte-se ao servidor, clique duas vezes em `Databases` e crie um novo banco de dados (com o botão direito e escolha `New Database`) chamado `Tutorials`.

Neste banco de dados, criar uma nova tabela chamada `AJAX` com as seguintes quatro colunas:

- `id` (inteiro de chave, primário, identidade, not NULL)
- `char` (char(1), NULL)
- `description` (varchar(50), NULL)
- `position` NULL (int)

[![O layout da tabela AJAX](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)

O layout da tabela AJAX ([clique para exibir a imagem em tamanho normal](drag-and-drop-via-reorderlist-cs/_static/image3.png))

Em seguida, preencha a tabela com um par de valores. Observe que o `position` coluna mantém a ordem de classificação dos elementos.

[![Os dados iniciais na tabela de AJAX](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)

Os dados iniciais na tabela de AJAX ([clique para exibir a imagem em tamanho normal](drag-and-drop-via-reorderlist-cs/_static/image6.png))

A próxima etapa requer para gerar um `SqlDataSource` controle para se comunicar com o novo banco de dados e sua tabela. A fonte de dados deve dar suporte a `SELECT` e `UPDATE` comandos SQL. Quando a ordem dos elementos de lista for alterada posteriormente, o `ReorderList` controle envia automaticamente os dois valores para a fonte de dados `Update` comando: a nova posição e a ID do elemento. Portanto, a fonte de dados necessidades um `<UpdateParameters>` seção para esses dois valores:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

O `ReorderList` controle precisa definir os seguintes atributos:

- `AllowReorder`: Se os itens da lista podem ser reorganizados
- `DataSourceID`: A ID da fonte de dados
- `DataKeyField`: O nome da coluna de chave primária na fonte de dados
- `SortOrderField`: A coluna de fonte de dados que fornece a ordem de classificação para os itens de lista

No `<DragHandleTemplate>` e `<ItemTemplate>` seções, o layout da lista pode ser ajustado. Além disso, a associação de dados é possível usar o `Eval()` método, como visto aqui:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

Informações de estilo CSS a seguir (referenciado na `<DragHandleTemplate>` seção o `ReorderList` controle) torna-se de que o ponteiro do mouse muda adequadamente quando ele passa o mouse sobre a alça de arraste:

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

Por fim, um `ScriptManager` controle inicializa o ASP.NET AJAX para a página:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

Executar este exemplo no navegador e reorganizar os itens da lista um pouco. Em seguida, recarregue a página e/ou dar uma olhada no banco de dados. As posições alteradas ter sido mantidas e também são refletidas pelos valores no `position` coluna no banco de dados e que tudo isso sem qualquer código, apenas usando marcação.

[![Os dados em que as alterações de banco de dados de acordo com a nova ordem de item de lista](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)

Os dados em que as alterações de banco de dados de acordo com a nova lista de ordem de item ([clique para exibir a imagem em tamanho normal](drag-and-drop-via-reorderlist-cs/_static/image9.png))

> [!div class="step-by-step"]
> [Anterior](using-postbacks-with-reorderlist-cs.md)
> [Próximo](using-postbacks-with-reorderlist-vb.md)
