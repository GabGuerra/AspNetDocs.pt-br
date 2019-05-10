---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
title: Uso de um ConfirmButton em um repetidor (VB) | Microsoft Docs
author: wenz
description: O extensor ConfirmButton no AJAX Control Toolkit cria um Sim/não pop-up quando o usuário clica em um botão (incluindo um controle LinkButton). Somente se Sim for...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 18c31709-3f9d-4d93-8b01-f1356bf610b4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: 026426d4dec61433bfa9edc66f934fa3ef6146c3
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65108819"
---
# <a name="using-a-confirmbutton-in-a-repeater-vb"></a>Uso de um ConfirmButton em um repetidor (VB)

por [Christian Wenz](https://github.com/wenz)

[Baixar o código](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip) ou [baixar PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)

> O extensor ConfirmButton no AJAX Control Toolkit cria um Sim/não pop-up quando o usuário clica em um botão (incluindo um controle LinkButton). Somente se Sim for selecionada, a ação do botão é executada, caso contrário, foi cancelada. Isso também é possível em um repetidor.

## <a name="overview"></a>Visão geral

O extensor ConfirmButton no AJAX Control Toolkit cria um Sim/não pop-up quando o usuário clica em um botão (incluindo um controle LinkButton). Somente se Sim for selecionada, a ação do botão é executada, caso contrário, foi cancelada. Isso também é possível em um repetidor.

## <a name="steps"></a>Etapas

Em primeiro lugar, uma fonte de dados é necessária. Este exemplo usa o banco de dados AdventureWorks e o Microsoft SQL Server 2005 Express Edition. O banco de dados é uma parte opcional da instalação do Visual Studio (inclusive a express edition) e também está disponível como um download separado em [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064). O banco de dados AdventureWorks é parte do SQL Server 2005 exemplos e bancos de dados de exemplo (download em [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). A maneira mais fácil de configurar o banco de dados é usar o Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) e anexe o `AdventureWorks.mdf` arquivo de banco de dados.

Para este exemplo, vamos supor que a instância do SQL Server 2005 Express Edition é chamada `SQLEXPRESS` e reside no mesmo computador que o servidor web; isso também é a configuração padrão. Se sua configuração for diferente, você precisa adaptar as informações de conexão para o banco de dados.

Para ativar a funcionalidade do AJAX ASP.NET e o Kit de ferramentas de controle, o `ScriptManager` controle deve ser colocada em qualquer lugar na página (mas dentro de `<form>` elemento):

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample1.aspx)]

Em seguida, uma fonte de dados é necessária. Para simplificar, somente as primeiras cinco entradas na tabela de fornecedores de AdventureWorks são recuperadas. Observe que, ao usar o Assistente do Visual Studio para criar a fonte de dados, o nome da tabela (`Vendors`) no momento não está corretamente prefixado com `Purchasing`. A marcação a seguir é a correta:

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample2.aspx)]

Esta fonte de dados, em seguida, pode ser usada em um repetidor. Como de costume, o `DataBinder.Eval()` método recupera dados da fonte de dados. O `ConfirmButtonExtender` , em seguida, deve ser colocado dentro do controle a `<ItemTemplate>` seção do repetidor de modo que ele apareça para cada entrada na fonte de dados.

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample3.aspx)]

[![O botão Confirmar aparece ao lado de cada entrada da fonte de dados](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)

O botão Confirmar aparece ao lado de cada entrada da fonte de dados ([clique para exibir a imagem em tamanho normal](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Anterior](using-a-confirmbutton-in-a-repeater-cs.md)
