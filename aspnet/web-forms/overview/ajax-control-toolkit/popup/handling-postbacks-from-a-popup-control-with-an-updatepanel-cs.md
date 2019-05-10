---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
title: Tratamento de Postbacks de um controle pop-up com um UpdatePanel (c#) | Microsoft Docs
author: wenz
description: O extensor PopupControl no AJAX Control Toolkit oferece uma maneira fácil de disparar um pop-up quando qualquer outro controle é ativado. Tenha cuidado especial a ser executada...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1f68f59d-9c1e-4cf3-b304-c13ae6b7203e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 6b43822825de37903d6a15c3000ed896faae4d64
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132505"
---
# <a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-c"></a>Tratamento de postbacks de um controle pop-up com um UpdatePanel (C#)

por [Christian Wenz](https://github.com/wenz)

[Baixar o código](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)

> O extensor PopupControl no AJAX Control Toolkit oferece uma maneira fácil de disparar um pop-up quando qualquer outro controle é ativado. Tenha cuidado especial a ser executada quando ocorre um postback dentro de tal um pop-up.

## <a name="overview"></a>Visão geral

O extensor PopupControl no AJAX Control Toolkit oferece uma maneira fácil de disparar um pop-up quando qualquer outro controle é ativado. Tenha cuidado especial a ser executada quando ocorre um postback dentro de tal um pop-up.

## <a name="steps"></a>Etapas

Ao usar um `PopupControl` com um postback, um `UpdatePanel` pode evitar a atualização de página causada por postback. A marcação a seguir define dois elementos importantes:

- Um `ScriptManager` controlar de forma que o ASP.NET AJAX Control Toolkit funciona
- Dois `TextBox` controla quais ambas disparará um pop-up
- Um `Panel` controle que servirá como o pop-up
- Dentro do painel, um `Calendar` controle é inserido em um `UpdatePanel` controle
- Dois `PopupControlExtender` controles que atribui o painel para as caixas de texto

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample1.aspx)]

Observe que o `OnSelectionChanged` atributo do `Calendar` controle está definido. Portanto, quando o usuário seleciona uma data no calendário, ocorre um postback e o método do lado do servidor `c1_SelectionChanged()` é executado. Dentro desse método, a data atual deve ser recuperada e Write-back para a caixa de texto.

A sintaxe para fazer isso é da seguinte maneira: Em primeiro lugar, um proxy do objeto para o `PopupControlExtender` na página deve ser gerado. O ASP.NET AJAX Control Toolkit oferece o `GetProxyForCurrentPopup()` método. O objeto retorna este método dá suporte a `Commit()` método que envia um valor de volta para o controle que disparou o pop-up (não o controle que disparou a chamada de método!). O código a seguir fornece a data selecionada como o argumento para o `Commit()` método, fazendo com que o código gravar a data selecionada de volta à caixa de texto:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample2.aspx)]

Agora sempre que você clica em uma data de calendário, a data selecionada aparece na caixa de texto associada, criando um controle de seletor de data que é utilizada em vários sites.

[![O calendário é exibido quando o usuário clica na caixa de texto](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)

O calendário é exibido quando o usuário clica na caixa de texto ([clique para exibir a imagem em tamanho normal](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png))

[![Clicar em uma data coloca na caixa de texto](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)

Clicar em uma data coloca na caixa de texto ([clique para exibir a imagem em tamanho normal](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png))

> [!div class="step-by-step"]
> [Anterior](using-multiple-popup-controls-cs.md)
> [Próximo](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
