---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: Associação de dados o controle deslizante (VB) | Microsoft Docs
author: wenz
description: O controle deslizante no AJAX Control Toolkit fornece um controle deslizante gráfico que pode ser controlado usando o mouse. É possível associar o positio atual...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: a60e09b7cdda7f924a4287aab8cda32fef5a53ac
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59419763"
---
# <a name="databinding-the-slider-control-vb"></a>Associação de Dados do controle deslizante (VB)

por [Christian Wenz](https://github.com/wenz)

[Baixar o código](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) ou [baixar PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)

> O controle deslizante no AJAX Control Toolkit fornece um controle deslizante gráfico que pode ser controlado usando o mouse. É possível associar a posição atual do controle deslizante para outro controle ASP.NET.


## <a name="overview"></a>Visão geral

O controle deslizante no AJAX Control Toolkit fornece um controle deslizante gráfico que pode ser controlado usando o mouse. É possível associar a posição atual do controle deslizante para outro controle ASP.NET.

## <a name="steps"></a>Etapas

Para ativar a funcionalidade do AJAX ASP.NET e o Kit de ferramentas de controle, o `ScriptManager` controle deve ser colocada em qualquer lugar na página (mas dentro de `<form>` elemento):

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

Em seguida, adicione dois `TextBox` controles à página. Um será transformado em um controle deslizante gráfico e a outra conterá a posição do controle deslizante.

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

A próxima etapa já é a etapa final. O `SliderExtender` controle do ASP.NET AJAX Control Toolkit faz um controle deslizante de fora a primeira caixa de texto e a segunda caixa de texto é atualizada automaticamente quando as alterações de posicionar o controle deslizante. Em ordem para que isso funcione, o `SliderExtender`do `TargetControlID` atributo deve ser definido para a ID da primeira caixa de texto; o `BoundControlID` atributo deve ser definido para a ID da segunda caixa de texto.

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

Como você pode ver no navegador, a associação de dados funciona em ambas as direções: inserindo um novo valor na caixa de texto atualiza a posição do controle deslizante. Se você fizer a segunda caixa de texto somente leitura, você pode adicionar uma proteção fraca ao campo de texto para que ele seja mais difícil para o usuário atualizar manualmente o valor aqui.


[![Controle deslizante e caixa de texto estão em sincronia](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)

Controle deslizante e caixa de texto estão em sincronia ([clique para exibir a imagem em tamanho normal](databinding-the-slider-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Anterior](using-the-slider-control-with-auto-postback-vb.md)
