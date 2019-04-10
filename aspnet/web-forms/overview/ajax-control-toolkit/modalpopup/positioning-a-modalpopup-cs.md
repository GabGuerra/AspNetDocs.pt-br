---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: Posicionamento de um ModalPopup (c#) | Microsoft Docs
author: wenz
description: O controle ModalPopup no AJAX Control Toolkit oferece uma maneira simples de criar um pop-up modal usando meios do lado do cliente. No entanto o controle não tem um...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: db69c0cf4fc3e5d39d88d8a6478a529309020d3d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59398027"
---
# <a name="positioning-a-modalpopup-c"></a>Posicionamento de um ModalPopup (C#)

por [Christian Wenz](https://github.com/wenz)

[Baixar o código](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)

> O controle ModalPopup no AJAX Control Toolkit oferece uma maneira simples de criar um pop-up modal usando meios do lado do cliente. No entanto o controle não oferece uma funcionalidade interna para posicionar o pop-up.


## <a name="overview"></a>Visão geral

O controle ModalPopup no AJAX Control Toolkit oferece uma maneira simples de criar um pop-up modal usando meios do lado do cliente. No entanto o controle não oferece uma funcionalidade interna para posicionar o pop-up.

## <a name="steps"></a>Etapas

Para ativar a funcionalidade do AJAX ASP.NET e o Kit de ferramentas de controle, o `ScriptManager`. controle deve ser colocada em qualquer lugar na página (mas dentro do `<form>` elemento):

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

Em seguida, adicione um painel que serve como o popup modal. Um botão é usado para fechar o janela pop-up:

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

Sempre que o pop-up for exibido, ele deverá ser posicionado em certo lugar na página. Para essa tarefa, uma função de JavaScript do lado do cliente é criada. Primeiro, ele tenta acessar o painel. Se tiver êxito, a posição do painel é definida usando CSS e JavaScript (alterar a posição do popup no será). No entanto, o `ModalPopupExtender` controle também tenta posicionar o pop-up. Portanto, o código JavaScript repetidamente posiciona o pop-up, cada décimo de segundo.

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

Como você pode ver, o valor de retorno de `setTimeout()` método JavaScript é salvo em uma variável global. Isso permite parar o posicionamento repetidas de pop-up sob demanda, usando o `clearTimeout()` método:

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

Agora tudo o que resta para fazer é tornar o navegador chamar essas funções sempre que apropriado. O `movePanel()` função JavaScript deve ser chamada quando o botão é clicado que dispara o painel:

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

E o `stopMoving()` função entra em jogo quando o pop-up é fechado isso pode ser disparada no `ModalPopupExtender` controle:

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]


[![Tpop-up modal de he aparece na posição designada](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)

O popup modal é exibido na posição designada ([clique para exibir a imagem em tamanho normal](positioning-a-modalpopup-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Anterior](handling-postbacks-from-a-modalpopup-cs.md)
> [Próximo](launching-a-modal-popup-window-from-server-code-vb.md)
