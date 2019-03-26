---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: Páginas mestras | Microsoft Docs
author: microsoft
description: Um dos principais componentes para o êxito de um site da Web é uma aparência consistente. No ASP.NET 1. x, os desenvolvedores usavam os controles de usuário para replicar Elem de página comuns....
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: 644beb37bf893a590be03dd0929c5870af6fbe87
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58425763"
---
<a name="master-pages"></a>Páginas mestras
====================
por [Microsoft](https://github.com/microsoft)

> Um dos principais componentes para o êxito de um site da Web é uma aparência consistente. No ASP.NET 1. x, os desenvolvedores usavam os controles de usuário para replicar os elementos de página comuns entre um aplicativo da Web. Embora seja certamente uma solução viável, usando controles de usuário tem algumas desvantagens. Por exemplo, uma alteração na posição de um controle de usuário requer uma alteração em várias páginas em um site. Controles de usuário também não são renderizados no modo de exibição de Design depois que está sendo inserido em uma página.


Um dos principais componentes para o êxito de um site da Web é uma aparência consistente. No ASP.NET 1. x, os desenvolvedores usavam os controles de usuário para replicar os elementos de página comuns entre um aplicativo da Web. Embora seja certamente uma solução viável, usando controles de usuário tem algumas desvantagens. Por exemplo, uma alteração na posição de um controle de usuário requer uma alteração em várias páginas em um site. Controles de usuário também não são renderizados no modo de exibição de Design depois que está sendo inserido em uma página.

O ASP.NET 2.0 apresenta mestre páginas como uma maneira de manter uma aparência consistente e como você verá em breve, mestre páginas representam uma melhoria significativa em relação ao método de controle de usuário.

## <a name="why-master-pages"></a>Por que páginas-mestre?

Você pode estar se perguntando por que as páginas mestras eram necessários no ASP.NET 2.0. Afinal de contas, os desenvolvedores de sites já estiver usando controles de usuário no ASP.NET 1.x para compartilhar as áreas de conteúdo entre as páginas. Há, na verdade, vários motivos por que os controles de usuário são uma solução menos ideal para criar um layout comum.

Controles de usuário, na verdade, não definem o layout da página. Em vez disso, elas definem o layout e a funcionalidade de uma parte de uma página. A distinção entre essas duas é importante, pois ele torna a capacidade de gerenciamento de uma solução de controle de usuário muito mais difícil. Por exemplo, quando você deseja alterar a posição de um controle de usuário em sua página, você deve editar a página real na qual o controle de usuário é exibida. Que bem se você tiver apenas algumas páginas, mas em sites grandes, ele rapidamente vira um pesadelo de gerenciamento do site!

Outra desvantagem do uso de controles de usuário para definir um layout comum está enraizada na arquitetura do ASP.NET em si. Se nenhum membro público de um controle de usuário for alterado, ele exige que você recompile todas as páginas que usam o controle de usuário. Por sua vez, o ASP.NET irá então recompilado por JIT suas páginas quando são acessadas. Isso, mais uma vez, produz uma arquitetura não escalonável e um problema de gerenciamento de site para sites maiores.

Muito bem, ambos esses problemas (e muito mais) são endereçados por páginas mestras no ASP.NET 2.0.

## <a name="how-master-pages-work"></a>Como páginas mestras funcionam

Uma página mestra é análoga a um modelo para outras páginas. Elementos de página que devem ser compartilhados com outras páginas (ou seja, menus, bordas, etc.) são adicionados à página mestra. Quando novas páginas são adicionadas ao site, você pode associá-los com uma página mestra. Uma página que está associada uma página mestra é chamada de um **página de conteúdo**. Por padrão, uma página de conteúdo assume a aparência da página mestra. No entanto, quando você cria uma página mestra, você pode definir as partes da página que a página de conteúdo pode substituir por seu próprio conteúdo. Essas partes são definidas usando um novo controle introduzido no ASP.NET 2.0; o **ContentPlaceHolder** controle.

Uma página mestra pode conter qualquer número de controles ContentPlaceHolder (ou nenhum). Na página de conteúdo, o conteúdo dos controles ContentPlaceHolder aparece dentro de **conteúdo** controles, outro controle novo no ASP.NET 2.0. Por padrão, os controles de conteúdo de páginas de conteúdo estão vazias, para que você possa fornecer seu próprio conteúdo. Se você quiser usar o conteúdo da página mestra dentro de controles de conteúdo, você pode fazer então como você verá neste módulo. O controle de conteúdo é mapeado para o controle ContentPlaceHolder por meio do atributo ContentPlaceHolderID do controle de conteúdo. O código a seguir mapeia um conteúdo de controle para um controle de ContentPlaceHolder chamado mainBody em uma página mestra.

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> Normalmente as pessoas descrevem as páginas mestras como sendo uma classe base para outras páginas. Que, na verdade, não é verdade. A relação entre as páginas mestras e páginas de conteúdo não é um de herança.


**Figura 1** mostra uma página mestra e uma página de conteúdo associada que aparecem no Visual Studio 2005. Você pode ver o controle ContentPlaceHolder na página mestra e o correspondente controle na página de conteúdo de conteúdo. Observe que o conteúdo de páginas mestras que está fora de ContentPlaceHolder é visível, mas esmaecidos na página de conteúdo. Somente o conteúdo dentro de ContentPlaceHolder pode ser suplantado pela página de conteúdo. Todos os outros conteúdos que vem da página mestra é imutável.


![Uma página mestra e sua página de conteúdo associada](master-pages/_static/image1.jpg)

**Figura 1**: Uma página mestra e sua página de conteúdo associada


## <a name="creating-a-master-page"></a>Criando uma página mestra

Para criar uma nova página mestra:

1. Abra o Visual Studio 2005 e crie um novo site.
2. Clique em arquivo, novo, de arquivos.
3. Escolha o arquivo mestre na caixa de diálogo Add New Item, como mostrado na **Figura 2**.
4. Clique em Adicionar.


![Criando uma nova página mestra](master-pages/_static/image2.jpg)

**Figura 2**: Criando uma nova página mestra


Observe que é a extensão de arquivo para uma página mestra <em>. master</em>. Essa é uma das maneiras que uma página mestra difere de uma página comum. A principal diferença é que no lugar de um @Page diretiva, a página mestra contém um @Master diretiva. Alternar a exibição da fonte para o mestre de página que você acabou de criar e revisar o código.

Uma nova página mestra terá um controle de ContentPlaceHolder por padrão. Na maioria dos casos, ele faz mais sentido para criar os elementos de página comuns primeiro e, em seguida, inserir controles ContentPlaceHolder onde o conteúdo personalizado é desejado. Nesses casos, os desenvolvedores desejará excluir o controle padrão ContentPlaceHolder e inserir novos registros, como a página é desenvolvida. ContentPlaceHolder controles não são redimensionáveis apesar do fato de que elas exibem as alças de dimensionamento. Os tamanhos de controle de ContentPlaceHolder automaticamente com base no conteúdo que ele contém com uma exceção; Se você colocar um controle ContentPlaceHolder dentro de um elemento de bloco, como uma célula de tabela, ele será redimensionado acordo com o tamanho do elemento.

## <a name="lab-1-working-with-master-pages"></a>Laboratório 1 trabalhando com páginas mestras

Neste laboratório, você criará uma nova página mestra e definir três controles ContentPlaceHolder. Você, em seguida, crie uma nova página de conteúdo e substitua o conteúdo de pelo menos um dos controles ContentPlaceHolder.

1. Criar uma página mestra e inserir controles ContentPlaceHolder. 

    1. Crie uma nova página mestra, conforme descrito acima.
    2. Exclua o controle de ContentPlaceHolder padrão.
    3. Selecione o controle ContentPlaceHolder clicando na borda sombreada superior do controle e, em seguida, excluí-lo pressionando a tecla DEL no seu teclado.
    4. Inserir uma nova tabela usando o *cabeçalho e o lado* modelo conforme mostrado na Figura 3. Altere a largura e altura para 90% cada para que a tabela inteira está visível no designer.


![](master-pages/_static/image3.jpg)

**Figura 3**


1. Coloque o cursor em cada célula da tabela e defina as *valign* propriedade *superior*.
2. Na caixa de ferramentas, inserir um controle ContentPlaceHolder na célula superior da tabela (a célula de cabeçalho).
3. Quando você insere esse controle ContentPlaceHolder, você observará que a altura da linha será levar até quase toda a página, conforme mostrado na Figura 4. Não estar preocupado que neste momento.


![O espaço vazio está na mesma célula como o ContentPlaceHolder](master-pages/_static/image1.gif)

**Figura 4**: O espaço vazio está na mesma célula como o ContentPlaceHolder


1. Coloque um controle de ContentPlaceHolder nas outras duas células. Depois que os outros controles ContentPlaceHolder foram inseridos, o tamanho das células da tabela deve ser como você esperaria. A página agora deve ser semelhante a página mostrada na **Figura 5**.


![O mestre com todos os controles de ContentPlaceHolder. Observe que a altura da célula para a célula de cabeçalho é agora o que deve ser](master-pages/_static/image2.gif)

**Figura 5**: O mestre com todos os controles de ContentPlaceHolder. Observe que a altura da célula para a célula de cabeçalho é agora o que deve ser


1. Digite algum texto de sua escolha em cada um dos três controles ContentPlaceHolder.
2. Salve a página mestra como exercise1.master.
3. Criar um novo formulário da Web e associá-la com a página mestra do exercise1.master.
4. Selecione o arquivo, novo, de arquivos no Visual Studio 2005.
5. Selecione **Web Form** na caixa de diálogo Adicionar Novo Item.
6. Certifique-se de que a caixa de seleção Selecionar página mestre é verificada, conforme mostrado na Figura 6.


![Adicionando uma nova página de conteúdo](master-pages/_static/image3.gif)

**Figura 6**: Adicionando uma nova página de conteúdo


1. Clique em Adicionar.
2. Selecione exercise1.master no, selecione uma caixa de diálogo de página mestra conforme mostrado na Figura 7.
3. Clique em Okey para adicionar a nova página de conteúdo.

Nova página de conteúdo é exibido no Visual Studio com um controle de conteúdo para cada controle ContentPlaceHolder na página mestra. Por padrão, os controles de conteúdo estão vazios, para que você possa adicionar seu próprio conteúdo. Se você gostaria de usar o conteúdo do controle ContentPlaceHolder na página mestra, basta clicar no símbolo de marca inteligente (a pequena seta preta no canto superior direito do controle) e escolha *padrão para o conteúdo de mestres* da marca inteligente conforme mostrado na **Figura 8**. Quando você fizer isso, o item de menu muda para *criar conteúdo personalizado*. Ao clicar nesse ponto remove o conteúdo da página mestra, permitindo que você defina o conteúdo personalizado para esse determinado controle de conteúdo.


![Definir um controle de conteúdo padrão para o conteúdo de páginas mestras](master-pages/_static/image4.gif)

**Figura 7**: Definir um controle de conteúdo padrão para o conteúdo de páginas mestras


## <a name="connecting-master-page-and-content-pages"></a>Conectar-se a página mestra e páginas de conteúdo

A associação entre uma página mestra e uma página de conteúdo pode ser configurada em uma das quatro maneiras diferentes:

- O <strong>MasterPageFile</strong> atributo do @Page diretiva
- Definindo o **Page.MasterPageFile** propriedade no código.
- O **&lt;páginas&gt;** elemento no arquivo de configuração do aplicativo (Web. config na pasta raiz do aplicativo)
- O **&lt;páginas&gt;** elemento em um arquivo de configuração de subpastas (Web. config em uma subpasta)

## <a name="masterpagefile-attribute"></a>Atributo MasterPageFile

O atributo MasterPageFile torna mais fácil de aplicar uma página mestra para uma determinada página do ASP.NET. Também é o método usado para aplicar a página mestra ao verificar a **selecionar a página mestra** caixa de seleção que você fez no Exercício 1.

## <a name="setting-pagemasterpagefile-in-code"></a>Configurando Page.MasterPageFile no código

Definindo a propriedade MasterPageFile no código, você pode aplicar uma página mestra específica ao seu conteúdo em tempo de execução. Isso é útil em casos em que você talvez seja necessário aplicar uma página mestra específica com base em uma função de usuários ou algum outro critério. A propriedade MasterPageFile deve ser definida no método PreInit. Se ele é definido após o método PreInit, será gerada uma InvalidOperationException. A página em que essa propriedade está sendo definida também deve ter um conteúdo de controle como o controle de nível superior da página. Caso contrário, um HttpException será gerada quando a propriedade MasterPageFile está definida.

## <a name="using-the-ltpagesgt-element"></a>Usando o &lt;páginas&gt; elemento

Você pode configurar uma página mestra para suas páginas, definindo o atributo masterPageFile na &lt;páginas&gt; elemento do arquivo Web. config. Ao usar esse método, lembre-se de que arquivos Web. config inferiores na estrutura de aplicativo podem substituir essa configuração. Qualquer atributo MasterPageFile definido um @Page diretiva também irá substituir essa configuração. Usando o &lt;páginas&gt; elemento torna simples para criar um <em>mestre</em> página mestra que pode ser substituída se for necessário em determinadas pastas ou arquivos.

## <a name="properties-in-master-pages"></a>Propriedades em páginas mestras

Uma página mestra pode expor propriedades, basta fazer essas propriedades públicas dentro da página mestra. Por exemplo, o código a seguir define uma propriedade chamada SomeProperty:

[!code-csharp[Main](master-pages/samples/sample2.cs)]

Para acessar a propriedade SomeProperty da página de conteúdo, você precisará usar o mestre de propriedade da seguinte forma:

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>Páginas mestras de aninhamento

Páginas mestras são a solução perfeita para garantir uma aparência comum em um aplicativo Web grande. No entanto, não é incomum ter algumas partes de um compartilhamento de sites grande uma interface comum, enquanto outras partes compartilham uma interface diferente. Para atender a essa necessidade, várias páginas mestras são a solução perfeita. No entanto, isso ainda não aborda o fato de que um aplicativo grande pode ter alguns componentes (como um menu, por exemplo) que são compartilhados entre todas as páginas e outros componentes que são compartilhados somente entre determinadas seções do site. Para esse tipo de situação, páginas mestras aninhadas atender a essa necessidade muito bem. Como você viu, uma página mestra normal consiste em uma página mestra e uma página de conteúdo. Em uma situação de página mestra aninhada, há duas páginas mestras. um mestre de pai e um mestre de filho. A página mestra filha também é uma página de conteúdo e seu mestre é a página mestra pai.

Aqui está o código para uma página mestra típico:

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

Em um cenário de mestre aninhado, isso seria o mestre do pai. Outra página mestra usaria esta página como sua página mestra e que o código ficaria assim:

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

Observe que, nesse cenário, o mestre de filho também é uma página de conteúdo para o mestre do pai. Todo o conteúdo do mestre filho é exibido dentro de um controle de conteúdo que obtém seu conteúdo do controle de ContentPlaceHolder do pai.

> [!NOTE]
> Suporte do Designer não está disponível para páginas mestras aninhadas. Quando você estiver desenvolvendo usando mestres aninhadas, você precisará usar exibição da fonte.


Este vídeo mostra um passo a passo de como usar páginas mestras aninhadas.


![](master-pages/_static/image1.png)


[Abra vídeo de tela inteira](master-pages/_static/nested1.wmv)


![Selecionar uma página mestra](master-pages/_static/image4.jpg)

**Figura 8**: Selecionar uma página mestra
