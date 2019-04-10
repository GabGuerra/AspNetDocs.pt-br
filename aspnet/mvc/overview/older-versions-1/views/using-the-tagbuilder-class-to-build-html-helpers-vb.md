---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: Usando a classe TagBuilder para criar auxiliares de HTML (VB) | Microsoft Docs
author: StephenWalther
description: Stephen Walther apresenta uma classe de utilitário útil na estrutura do ASP.NET MVC, a classe TagBuilder nomeada. Você pode usar facilmente a classe TagBuilder para...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 4fe34858aadb705ffb59e06ba805493d89aa4028
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59403201"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a>Usando a classe TagBuilder para criar auxiliares de HTML (VB)

por [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther apresenta uma classe de utilitário útil na estrutura do ASP.NET MVC, a classe TagBuilder nomeada. Você pode usar a classe TagBuilder para criar facilmente as marcas HTML.


A estrutura ASP.NET MVC inclui uma classe de utilitário útil nomeada a classe TagBuilder que você pode usar ao criar auxiliares HTML. A classe TagBuilder, como sugere o nome da classe, permite criar facilmente as marcas HTML. Neste breve tutorial, você é provido com uma visão geral da classe TagBuilder e você aprenderá a usar essa classe quando a criação de um auxiliar HTML simple que renderiza o HTML &lt;img&gt; marcas.

## <a name="overview-of-the-tagbuilder-class"></a>Visão geral da classe TagBuilder

A classe TagBuilder está contida no namespace System.Web.Mvc. Ele tem cinco métodos:

- AddCssClass() – permite que você adicione um novo *classe = ""* do atributo a uma marca.
- GenerateId() – permite que você adicione um atributo de id para uma marca. Esse método substitui automaticamente os períodos em que a id (por padrão, períodos são substituídos por sublinhados)
- MergeAttribute() – permite que você adicione atributos a uma marca. Há várias sobrecargas desse método.
- SetInnerText() – permite que você defina o texto interno da marca. O texto interno é a codificação HTML automaticamente.
- ToString () – permite que você renderize a marca. Você pode especificar se deseja criar uma marca normal, uma marca de início, uma marca de fim ou uma marca de fechamento automático.
  

A classe TagBuilder tem quatro propriedades importantes:

- Atributos – representa todos os atributos da marca.
- IdAttributeDotReplacement – representa o caractere usado pelo método GenerateId() substituir períodos (o padrão é um caractere de sublinhado).
- InnerHTML – representa o conteúdo interno da marca. Atribuir uma cadeia de caracteres para esta propriedade *não* HTML codificar a cadeia de caracteres.
- TagName – representa o nome da marca.

Esses métodos e propriedades oferecem todos os métodos básicos e as propriedades que você precisa para criar uma marca HTML. Você não precisa usar a classe TagBuilder realmente. Você pode usar uma classe StringBuilder. No entanto, a classe TagBuilder facilita sua vida um pouco.

## <a name="creating-an-image-html-helper"></a>Criar um auxiliar de HTML de imagem

Quando você cria uma instância da classe TagBuilder, você pode passar o nome da marca que você deseja compilar para o construtor TagBuilder. Em seguida, você pode chamar métodos, como os métodos AddCssClass e MergeAttribute() para modificar os atributos da marca. Por fim, você pode chamar o método ToString () para processar a tag.

Por exemplo, a listagem 1 contém um auxiliar de imagem HTML. O auxiliar de imagem é implementado internamente com um que representa um HTML TagBuilder &lt;img&gt; marca.

**Listagem 1 – Helpers\ImageHelper.vb**

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

O módulo na listagem 1 contém dois métodos sobrecarregados chamados Image(). Quando você chama o método Image(), você pode passar um objeto que representa um conjunto de atributos HTML ou não.

Observe como o método TagBuilder.MergeAttribute() é usado para adicionar atributos individuais, como o atributo src para o TagBuilder. Observe, além disso, como o método de TagBuilder.MergeAttributes() é usado para adicionar uma coleção de atributos para o TagBuilder. O método MergeAttributes() aceita um dicionário&lt;cadeia de caracteres, objeto&gt; parâmetro. A classe RouteValueDictionary é usada para converter o objeto que representa a coleção de atributos em um dicionário&lt;cadeia de caracteres, objeto&gt;.

Depois de criar o auxiliar de imagem, você pode usar o auxiliar em suas exibições ASP.NET MVC, assim como qualquer um dos outros auxiliares HTML padrão. O modo de exibição na listagem 2 usa o auxiliar de imagem para exibir a mesma imagem de um Xbox duas vezes (veja a Figura 1). O auxiliar Image() é chamado com e sem uma coleção de atributos HTML.

**Listagem 2 – Home\Index.aspx**

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]


[![Tcaixa de diálogo Novo projeto he](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)

**Figura 01**: Usando o auxiliar de imagem ([clique para exibir a imagem em tamanho normal](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))


Observe que você deve importar o namespace associado com o auxiliar de imagem na parte superior do modo de exibição aspx. O auxiliar é importado com a seguinte diretiva:

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

Em um aplicativo Visual Basic, o namespace padrão é o mesmo que o nome do aplicativo.

> [!div class="step-by-step"]
> [Anterior](creating-custom-html-helpers-vb.md)
> [Próximo](creating-page-layouts-with-view-master-pages-vb.md)
