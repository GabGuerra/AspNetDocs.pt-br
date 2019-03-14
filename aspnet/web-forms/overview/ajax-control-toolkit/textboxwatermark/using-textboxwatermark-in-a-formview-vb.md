---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
title: Uso de TextBoxWatermark em um FormView (VB) | Microsoft Docs
author: wenz
description: O controle TextBoxWatermark do AJAX Control Toolkit estende uma caixa de texto para que um texto seja exibido dentro da caixa. Quando um usuário clica na caixa de-eu...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41497361-7fba-4825-b36c-f58d79522a88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
msc.type: authoredcontent
ms.openlocfilehash: b9a731be89d0582ebd411809a6bbcbee801fea2a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028243"
---
<a name="using-textboxwatermark-in-a-formview-vb"></a>Uso de TextBoxWatermark em um FormView (VB)
====================
por [Christian Wenz](https://github.com/wenz)

[Baixar o código](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip) ou [baixar PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)

> O controle TextBoxWatermark do AJAX Control Toolkit estende uma caixa de texto para que um texto seja exibido dentro da caixa. Quando um usuário clica na caixa, é esvaziado. Se o usuário deixa a caixa sem digitar texto, o texto previamente preenchido reaparece. Isso também é possível dentro de um controle FormView.


## <a name="overview"></a>Visão geral

O `TextBoxWatermark` o controle no AJAX Control Toolkit, uma caixa de texto para que um texto seja exibido dentro da caixa. Quando um usuário clica na caixa, é esvaziado. Se o usuário deixa a caixa sem digitar texto, o texto previamente preenchido reaparece. Isso também é possível dentro de um `FormView` controle.

## <a name="steps"></a>Etapas

Em primeiro lugar, uma fonte de dados é necessária. Este exemplo usa o banco de dados AdventureWorks e o Microsoft SQL Server 2005 Express Edition. O banco de dados é uma parte opcional da instalação do Visual Studio (inclusive a express edition) e também está disponível como um download separado em [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064). O banco de dados AdventureWorks é parte do SQL Server 2005 exemplos e bancos de dados de exemplo (download em [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). A maneira mais fácil de configurar o banco de dados é usar o Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) e anexe o `AdventureWorks.mdf` arquivo de banco de dados.

Para este exemplo, vamos supor que a instância do SQL Server 2005 Express Edition é chamada `SQLEXPRESS` e reside no mesmo computador que o servidor web; isso também é a configuração padrão. Se sua configuração for diferente, você precisa adaptar as informações de conexão para o banco de dados.

Para ativar a funcionalidade do AJAX ASP.NET e o Kit de ferramentas de controle, o `ScriptManager` controle deve ser colocada em qualquer lugar na página (mas dentro de `<form>` elemento):

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample1.aspx)]

Em seguida, adicione uma fonte de dados para a página que dá suporte a `DELETE`, `INSERT` e `UPDATE` instruções SQL. Se você estiver usando o Assistente do Visual Studio para criar a fonte de dados, lembre-se de que um bug na versão atual não prefixar o nome da tabela (`Vendor`) com `Purchasing`. A marcação a seguir mostra a sintaxe correta:

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample2.aspx)]

Lembre-se o nome (`ID`) da fonte de dados, pois ele será usado o `DataSourceID` propriedade do `FormView` controle. O `<InsertItemTemplate>` seção o `FormView` contém uma caixa de texto que será estendida a `TextBoxWatermarkExtender` controle. Certifique-se de que o extensor reside dentro do modelo e não fora dele.

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample3.aspx)]

Agora quando o usuário altera no modo de inserção do `FormView` controlar, o campo de texto para o novo fornecedor é previamente preenchido obrigado a `TextBoxWatermarkExtender` controle. Um clique na caixa de texto permite que o texto do enchimento desaparecer.


[![A marca d'água no campo vem do extensor](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)

A marca d'água no campo vem do extensor ([clique para exibir a imagem em tamanho normal](using-textboxwatermark-in-a-formview-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Anterior](using-textboxwatermark-with-validation-controls-cs.md)
> [Próximo](using-textboxwatermark-with-validation-controls-vb.md)
