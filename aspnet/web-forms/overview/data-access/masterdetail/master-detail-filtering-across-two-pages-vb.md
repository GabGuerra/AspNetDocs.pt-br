---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
title: Mestre/detalhes filtragem em duas páginas (VB) | Microsoft Docs
author: rick-anderson
description: Neste tutorial, implementaremos esse padrão usando um GridView para listar os fornecedores no banco de dados. Cada linha de fornecedor no GridView conterá um e de exibição...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 361d6a44-3f1f-4daf-85df-d4c2b8bf065d
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 5569af095909b4aacaaf559dfae025d13805a510
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65129552"
---
# <a name="masterdetail-filtering-across-two-pages-vb"></a>Filtragem mestre/detalhes em duas páginas (VB)

por [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Baixe o aplicativo de exemplo](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_9_VB.exe) ou [baixar PDF](master-detail-filtering-across-two-pages-vb/_static/datatutorial09vb1.pdf)

> Neste tutorial, implementaremos esse padrão usando um GridView para listar os fornecedores no banco de dados. Cada linha de fornecedor no GridView conterá um link Exibir produtos que, quando clicado, levará o usuário para uma página separada que lista os produtos para o fornecedor selecionado.

## <a name="introduction"></a>Introdução

Nos dois tutoriais anteriores, vimos como exibir relatórios mestre/detalhes em uma única página da web usando DropDownLists para exibir os registros de "mestres" e um [GridView](master-detail-filtering-with-a-dropdownlist-vb.md) ou [DetailsView](master-detail-filtering-with-two-dropdownlists-vb.md) controle para exibir o " detalhes." Outro padrão comum usado para relatórios mestre/detalhes é ter os registros mestres em uma página da web e os detalhes mostrados no outro. Um site do fórum, como [fóruns do ASP.NET](https://forums.asp.net/), é um ótimo exemplo desse padrão na prática. Fóruns do ASP.NET são compostos de uma variedade de fóruns do guia de Introdução, Web Forms, controles de apresentação de dados e assim por diante. Cada grupo de discussão é composto de vários threads e cada thread é composto de um número de postagens. Na home page fóruns do ASP.NET, os fóruns são listados. Clicar em um fórum levado a uma `ShowForum.aspx` página, que lista os threads de Fórum. Da mesma forma, clicar em um thread leva você para `ShowPost.aspx`, que exibe as postagens para o thread que foi clicado.

Neste tutorial, implementaremos esse padrão usando um GridView para listar os fornecedores no banco de dados. Cada linha de fornecedor no GridView conterá um link Exibir produtos que, quando clicado, levará o usuário para uma página separada que lista os produtos para o fornecedor selecionado.

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>Etapa 1: Adicionando`SupplierListMaster.aspx`e`ProductsForSupplierDetails.aspx`páginas para o`Filtering`pasta

Ao definir o layout de página no terceiro tutorial adicionamos um número de páginas "starter" a `BasicReporting`, `Filtering`, e `CustomFormatting` pastas. No entanto, não adicionamos uma página inicial para este tutorial no momento, portanto, reserve um tempo para adicionar duas novas páginas para o `Filtering` pasta: `SupplierListMaster.aspx` e `ProductsForSupplierDetails.aspx`. `SupplierListMaster.aspx` listará os registros "mestres" (os fornecedores) enquanto `ProductsForSupplierDetails.aspx` exibirá os produtos para o fornecedor selecionado.

Ao criar essas duas novas páginas ser determinadas para associá-los com o `Site.master` página mestra.

![Adicione as páginas de ProductsForSupplierDetails.aspx e SupplierListMaster.aspx para a pasta de filtragem](master-detail-filtering-across-two-pages-vb/_static/image1.png)

**Figura 1**: Adicione a `SupplierListMaster.aspx` e `ProductsForSupplierDetails.aspx` páginas para o `Filtering` pasta

Além disso, ao adicionar novas páginas ao projeto, certifique-se atualizar o arquivo de mapa de site, `Web.sitemap`, adequadamente. Para este tutorial simplesmente adicionar o `SupplierListMaster.aspx` página para o mapa do site usando o seguinte conteúdo XML como um filho dos relatórios de filtragem `<siteMapNode>` elemento:

[!code-xml[Main](master-detail-filtering-across-two-pages-vb/samples/sample1.xml)]

> [!NOTE]
> Você pode ajudar a automatizar o processo de atualizar o arquivo de mapa de site quando adicionar novos ASP.NET páginas usando [K. Scott Allen](http://odetocode.com/Blogs/scott/)do Visual Studio gratuito [macros de mapa de Site](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx).

## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>Etapa 2: Exibindo a lista de fornecedores em`SupplierListMaster.aspx`

Com o `SupplierListMaster.aspx` e `ProductsForSupplierDetails.aspx` páginas criadas, nossa próxima etapa é criar o GridView de fornecedores em `SupplierListMaster.aspx`. Adicione um controle GridView à página e associá-lo a um novo ObjectDataSource. Este ObjectDataSource deve usar o `SuppliersBLL` da classe `GetSuppliers()` método para retornar todos os fornecedores.

[![Selecione a classe SuppliersBLL](master-detail-filtering-across-two-pages-vb/_static/image3.png)](master-detail-filtering-across-two-pages-vb/_static/image2.png)

**Figura 2**: Selecione o `SuppliersBLL` classe ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image4.png))

[![Configurar o ObjectDataSource para usar o método GetSuppliers()](master-detail-filtering-across-two-pages-vb/_static/image6.png)](master-detail-filtering-across-two-pages-vb/_static/image5.png)

**Figura 3**: Configurar o ObjectDataSource para usar o `GetSuppliers()` método ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image7.png))

Precisamos incluir um link intitulado exibir produtos em cada linha GridView que, quando clicado, leva o usuário à `ProductsForSupplierDetails.aspx` passando a linha selecionada `SupplierID` valor por meio da cadeia de consulta. Por exemplo, se o usuário clica no link Exibir produtos para o fornecedor Tokyo Traders (que tem um `SupplierID` valor de 4), eles devem ser enviados ao `ProductsForSupplierDetails.aspx?SupplierID=4`.

Para fazer isso, adicione uma [HyperLinkField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx) para o controle GridView, que adiciona um hiperlink para cada linha de GridView. Inicie clicando no link Edit Columns na marca inteligente do GridView. Em seguida, selecione o HyperLinkField na lista na parte superior esquerda e clique em Adicionar para incluir o HyperLinkField na lista de campos do GridView.

[![Adicionar um HyperLinkField a GridView](master-detail-filtering-across-two-pages-vb/_static/image9.png)](master-detail-filtering-across-two-pages-vb/_static/image8.png)

**Figura 4**: Adicionar um HyperLinkField a GridView ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image10.png))

O HyperLinkField pode ser configurado para usar o mesmo texto ou URL valores o link em cada linha de GridView, ou pode basear esses valores em valores de dados associados a cada linha específica. Para especificar um estático valor em todas as linhas usam o HyperLinkField `Text` ou `NavigateUrl` propriedades. Como queremos que o texto do link ser o mesmo para todas as linhas, defina o HyperLinkField `Text` propriedade para exibir produtos.

[![Defina a propriedade de texto do HyperLinkField para exibir os produtos](master-detail-filtering-across-two-pages-vb/_static/image12.png)](master-detail-filtering-across-two-pages-vb/_static/image11.png)

**Figura 5**: Defina o HyperLinkField `Text` propriedade para exibir os produtos ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image13.png))

Para definir o texto ou valores de URL deve ser baseado nos dados subjacentes associados à linha de GridView, especifique o texto de campos de dados ou valores de URL devem ser extraídas do `DataTextField` ou `DataNavigateUrlFields` propriedades. `DataTextField` só pode ser definida como um único campo de dados; `DataNavigateUrlFields`, no entanto, pode ser definido como uma lista delimitada por vírgulas de campos de dados. Com frequência, é necessário basear o texto ou a URL em uma combinação de valor do campo de dados da linha atual e algumas marcações estática. Neste tutorial, por exemplo, queremos ser a URL de links do HyperLinkField `ProductsForSupplierDetails.aspx?SupplierID=supplierID`, onde *`supplierID`* é uma linha do GridView cada `SupplierID` valor. Observe que precisamos estáticos e controlados por dados os valores aqui: a `ProductsForSupplierDetails.aspx?SupplierID=` parte da URL do link é estático, enquanto a *`supplierID`* parte é controlada por dados como seu valor é a cada linha própria `SupplierID` valor.

Para indicar uma combinação de valores estáticos e controlados por dados, use o `DataTextFormatString` e `DataNavigateUrlFormatString` propriedades. Nessas propriedades, insira a marcação estática conforme necessário e, em seguida, use o marcador `{0}` onde você deseja que o valor do campo especificado em de `DataTextField` ou `DataNavigateUrlFields` propriedades apareçam. Se o `DataNavigateUrlFields` propriedade tem vários uso especificado de campos `{0}` onde você deseja que o primeiro valor do campo inserido, `{1}` para o segundo valor do campo e assim por diante.

Aplicar isso em nosso tutorial, precisamos definir a `DataNavigateUrlFields` propriedade para `SupplierID`, já que é o campo de dados cujo valor é preciso personalizar em uma base por linha, e o `DataNavigateUrlFormatString` propriedade `ProductsForSupplierDetails.aspx?SupplierID={0}`.

[![Configurar o HyperLinkField para incluir a URL do Link apropriado com base em SupplierID](master-detail-filtering-across-two-pages-vb/_static/image15.png)](master-detail-filtering-across-two-pages-vb/_static/image14.png)

**Figura 6**: Configurar o HyperLinkField para incluir o adequada Link de URL com base após o `SupplierID` ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image16.png))

Depois de adicionar o HyperLinkField, fique à vontade personalizar e reordenar os campos do GridView. A marcação a seguir mostra o GridView depois que eu fiz algumas personalizações secundárias do nível de campo.

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample2.aspx)]

Reserve um tempo para exibir o `SupplierListMaster.aspx` página por meio de um navegador. Como mostra a Figura 7, a página atualmente lista todos os fornecedores, incluindo um link Exibir produtos. Clicar em Exibir produtos link levará você para `ProductsForSupplierDetails.aspx`, passando ao longo do fornecedor `SupplierID` na querystring.

[![Cada linha de fornecedor contém um Link de produtos do modo de exibição](master-detail-filtering-across-two-pages-vb/_static/image18.png)](master-detail-filtering-across-two-pages-vb/_static/image17.png)

**Figura 7**: Cada linha de fornecedor contém um Link de produtos do modo de exibição ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image19.png))

## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>Etapa 3: Lista os produtos do fornecedor em`ProductsForSupplierDetails.aspx`

Neste momento a `SupplierListMaster.aspx` página está enviando os usuários `ProductsForSupplierDetails.aspx`, passando o fornecedor selecionado `SupplierID` na querystring. Etapa de final deste tutorial é exibir os produtos em um GridView no `ProductsForSupplierDetails.aspx` cujos `SupplierID` é igual ao `SupplierID` transmitidos por meio da cadeia de consulta. Para realizar este guia de início, adicionando um GridView para o `ProductsForSupplierDetails.aspx` página, usando um novo controle ObjectDataSource chamado `ProductsBySupplierDataSource` que invoca o `GetProductsBySupplierID(supplierID)` método a partir de `ProductsBLL` classe.

[![Adicionar um novo ObjectDataSource chamado ProductsBySupplierDataSource](master-detail-filtering-across-two-pages-vb/_static/image21.png)](master-detail-filtering-across-two-pages-vb/_static/image20.png)

**Figura 8**: Adicionar um novo ObjectDataSource nomeado `ProductsBySupplierDataSource` ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image22.png))

[![Selecione a classe ProductsBLL](master-detail-filtering-across-two-pages-vb/_static/image24.png)](master-detail-filtering-across-two-pages-vb/_static/image23.png)

**Figura 9**: Selecione o `ProductsBLL` classe ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image25.png))

[![Ter o ObjectDataSource invoca o método GetProductsBySupplierID(supplierID)](master-detail-filtering-across-two-pages-vb/_static/image27.png)](master-detail-filtering-across-two-pages-vb/_static/image26.png)

**Figura 10**: Ter o ObjectDataSource invocar o `GetProductsBySupplierID(supplierID)` método ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image28.png))

A etapa final do Assistente Configurar fonte de dados nos pede para fornecer a origem do `GetProductsBySupplierID(supplierID)` do método *`supplierID`* parâmetro. Para usar o valor de querystring, defina a origem do parâmetro QueryString e insira o nome do valor de cadeia de consulta para usar na caixa de texto QueryStringField (`SupplierID`).

[![Preencher o valor do parâmetro do valor de Querystring SupplierID supplierID](master-detail-filtering-across-two-pages-vb/_static/image30.png)](master-detail-filtering-across-two-pages-vb/_static/image29.png)

**Figura 11**: Popular o *`supplierID`* valor de parâmetro a `SupplierID` valor de Querystring ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image31.png))

E isso é tudo! A Figura 12 mostra os `ProductsForSupplierDetails.aspx` página quando acessadas clicando no link Tokyo Traders de `SupplierListMaster.aspx`.

[![Os produtos fornecidos pela Tokyo Traders são mostrados](master-detail-filtering-across-two-pages-vb/_static/image33.png)](master-detail-filtering-across-two-pages-vb/_static/image32.png)

**Figura 12**: Os produtos fornecidos pela Tokyo Traders são mostrados ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image34.png))

## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>Exibindo informações de fornecedor no`ProductsForSupplierDetails.aspx`

Como mostra a Figura 12, o `ProductsForSupplierDetails.aspx` página simplesmente lista os produtos que são fornecidos pelo `SupplierID` especificado na cadeia de consulta. Alguém enviadas diretamente para essa página, no entanto, não saberia que a Figura 12 mostra produtos Tokyo Traders. Para corrigir isso, podemos exibir informações de fornecedor também nesta página.

Comece adicionando um FormView acima os produtos GridView. Criar um novo controle ObjectDataSource chamado `SuppliersDataSource` que invoca a `SuppliersBLL` da classe `GetSupplierBySupplierID(supplierID)` método.

[![Selecione a classe SuppliersBLL](master-detail-filtering-across-two-pages-vb/_static/image36.png)](master-detail-filtering-across-two-pages-vb/_static/image35.png)

**Figura 13**: Selecione o `SuppliersBLL` classe ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image37.png))

[![Ter o ObjectDataSource invoca o método GetSupplierBySupplierID(supplierID)](master-detail-filtering-across-two-pages-vb/_static/image39.png)](master-detail-filtering-across-two-pages-vb/_static/image38.png)

**Figura 14**: Ter o ObjectDataSource invocar o `GetSupplierBySupplierID(supplierID)` método ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image40.png))

Assim como acontece com o `ProductsBySupplierDataSource`, tem o *`supplierID`* parâmetro recebe o valor da `SupplierID` valor de cadeia de consulta.

[![Preencher o valor do parâmetro do valor de Querystring SupplierID supplierID](master-detail-filtering-across-two-pages-vb/_static/image42.png)](master-detail-filtering-across-two-pages-vb/_static/image41.png)

**Figura 15**: Popular o *`supplierID`* valor de parâmetro a `SupplierID` valor de Querystring ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image43.png))

Quando a associação de FormView o ObjectDataSource no modo Design, o Visual Studio criará automaticamente de FormView `ItemTemplate`, `InsertItemTemplate`, e `EditItemTemplate` com controles de rótulo e da TextBox Web para cada um dos campos de dados retornados pelo ObjectDataSource. Uma vez que queremos exibir supplier informações à vontade remover apenas o `InsertItemTemplate` e `EditItemTemplate`. Em seguida, edite o ItemTemplate para que ele exibe o nome da empresa do fornecedor em um `<h3>` elemento e o endereço, cidade, país e número de telefone abaixo do nome da empresa. Como alternativa, você pode definir manualmente o FormView `DataSourceID` e crie a `ItemTemplate` marcação, como fizemos na "[exibindo dados com o ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)" tutorial.

Após essas edições marcação declarativa de FormView deve ser semelhante ao seguinte:

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample3.aspx)]

A Figura 16 mostra uma captura de tela de `ProductsForSupplierDetails.aspx` página depois que as informações de fornecedor detalhadas acima tem sido incluídas.

[![A lista de produtos inclui um resumo sobre o fornecedor](master-detail-filtering-across-two-pages-vb/_static/image45.png)](master-detail-filtering-across-two-pages-vb/_static/image44.png)

**Figura 16**: A lista de produtos inclui um resumo sobre o fornecedor ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image46.png))

## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>Aplicar Final toca para o`ProductsForSupplierDetails.aspx`interface do usuário

Para melhorar o usuário a experiência para este relatório lá são algumas das adições que devemos fazer o `ProductsForSupplierDetails.aspx` página. Atualmente, a única maneira de um usuário pode ir do `ProductsForSupplierDetails.aspx` página de volta para a lista de fornecedores é clicar em botão Voltar do seu navegador. Vamos adicionar um controle de hiperlink para o `ProductsForSupplierDetails.aspx` página vincula de volta para `SupplierListMaster.aspx`, fornecendo ainda outra maneira para o usuário retornar à lista mestra.

[![Adicionar um controle de hiperlink para levar o usuário ao SupplierListMaster.aspx](master-detail-filtering-across-two-pages-vb/_static/image48.png)](master-detail-filtering-across-two-pages-vb/_static/image47.png)

**Figura 17**: Adicionar um controle de hiperlink para levar o usuário voltar para `SupplierListMaster.aspx` ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image49.png))

Se o usuário clicar no link Exibir produtos para um fornecedor que não tem quaisquer produtos, o `ProductsBySupplierDataSource` ObjectDataSource em `ProductsForSupplierDetails.aspx` não retornará nenhum resultado. O GridView vinculado a ObjectDataSource não renderiza nenhuma marcação resultando em uma região em branco na página no navegador do usuário. Para mais claramente se comunicar com o usuário que não há nenhum produto associado com o fornecedor selecionado, podemos definir o GridView `EmptyDataText` propriedade à mensagem de que deseja que seja exibidos quando surge uma situação como essa. Defini a essa propriedade como "Não há nenhum produtos fornecidos por esse fornecedor"

Por padrão, todos os fornecedores no banco de dados Northwind fornecem pelo menos um produto. No entanto, para este tutorial manualmente modifiquei o `Products` para que o fornecedor Escargots Nouveaux não está mais associado a todos os produtos da tabela. Figura 18 mostra a página de detalhes para Escargots Nouveaux após essa alteração foi feita.

[![Os usuários serão informados de que o fornecedor não fornece todos os produtos](master-detail-filtering-across-two-pages-vb/_static/image51.png)](master-detail-filtering-across-two-pages-vb/_static/image50.png)

**Figura 18**: Os usuários serão informados de que o fornecedor não fornece todos os produtos ([clique para exibir a imagem em tamanho normal](master-detail-filtering-across-two-pages-vb/_static/image52.png))

## <a name="summary"></a>Resumo

Enquanto os relatórios mestre/detalhes podem exibir registros mestre e de detalhes em uma única página, em muitos sites eles são separados em duas páginas da web. Neste tutorial vimos como implementar tal relatório mestre/detalhes fazendo com que os fornecedores listados em um GridView na página da web "mestre" e os produtos associados listados na página "Detalhes". Cada linha de fornecedor na página da web mestre continha um link para a página de detalhes do passado ao longo da linha `SupplierID` valor. Esses links específicas de linha podem ser adicionados facilmente usando HyperLinkField do GridView.

Na página de detalhes ao recuperar esses produtos para o fornecedor especificado foi feito invocando o `ProductsBLL` da classe `GetProductsBySupplierID(supplierID)` método. O *`supplierID`* valor do parâmetro foi especificado declarativamente usando a cadeia de consulta como a origem do parâmetro. Também examinamos como exibir os detalhes de fornecedor na página de detalhes usando um FormView.

Nossos [próximo tutorial](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md) é o final sobre relatórios mestre/detalhes. Vamos examinar como exibir uma lista de produtos em um GridView onde cada linha tem um botão de seleção. Clicar no botão de seleção exibirá os detalhes do produto em um controle DetailsView na mesma página.

Boa programação!

## <a name="about-the-author"></a>Sobre o autor

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor de sete livros sobre ASP/ASP.NET e fundador da [4GuysFromRolla.com](http://www.4guysfromrolla.com), tem trabalhado com tecnologias Microsoft Web desde 1998. Scott funciona como um consultor independente, instrutor e escritor. Seu livro mais recente é [ *Sams Teach por conta própria ASP.NET 2.0 em 24 horas*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Ele pode ser contatado pelo [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) ou por meio de seu blog, que pode ser encontrado em [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Agradecimentos especiais a

Esta série de tutoriais foi revisada por muitos revisores úteis. Revisor de avanço para este tutorial foi Hilton Giesenow. Você está interessado na revisão Meus próximos artigos do MSDN? Nesse caso, me descartar uma linha na [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Anterior](master-detail-filtering-with-two-dropdownlists-vb.md)
> [Próximo](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)
