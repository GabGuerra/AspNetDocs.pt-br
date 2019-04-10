---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: Criação de Classes de modelo com o LINQ to SQL (c#) | Microsoft Docs
author: microsoft
description: O objetivo deste tutorial é explicar um método de criação de classes de modelo para um aplicativo ASP.NET MVC. Neste tutorial, você aprenderá a compilar modelo c...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: d1895b03a2aa877bfd279995dc5647c5efefade6
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59414199"
---
# <a name="creating-model-classes-with-linq-to-sql-c"></a>Criação de classes de modelo com o LINQ to SQL (C#)

por [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> O objetivo deste tutorial é explicar um método de criação de classes de modelo para um aplicativo ASP.NET MVC. Neste tutorial, você aprenderá como criar classes de modelo e executar o acesso de banco de dados, tirando proveito do Microsoft LINQ to SQL.


O objetivo deste tutorial é explicar um método de criação de classes de modelo para um aplicativo ASP.NET MVC. Neste tutorial, você aprenderá a criar classes de modelo e executar o acesso de banco de dados, tirando proveito do Microsoft LINQ to SQL

Neste tutorial, vamos criar um aplicativo básico do banco de dados do filme. Vamos começar criando o aplicativo de banco de dados do filme da maneira mais rápida e fácil possível. Podemos executar todos de nosso acesso a dados diretamente do nosso ações do controlador.

Em seguida, você aprenderá como usar o padrão de repositório. Usando o padrão de repositório requer um pouco mais trabalho. No entanto, a vantagem de adotar esse padrão é que ele permite que você crie aplicativos que são adaptáveis para alterar e pode ser facilmente testados.

## <a name="what-is-a-model-class"></a>O que é uma classe de modelo?

Um modelo MVC contém toda a lógica de aplicativo que não está contida em uma exibição do MVC ou controlador MVC. Em particular, um modelo MVC contém todos os seus negócios de aplicativos e a lógica de acesso a dados.

Você pode usar uma variedade de tecnologias diferentes para implementar a lógica de acesso de dados. Por exemplo, você pode criar suas classes de acesso de dados usando as classes do Microsoft Entity Framework, NHibernate, o Subsonic ou ADO.NET.

Neste tutorial, uso o LINQ to SQL para consultar e atualizar o banco de dados. LINQ to SQL oferece um método muito fácil de interagir com um banco de dados do Microsoft SQL Server. No entanto, é importante entender que o ASP.NET MVC framework não está vinculado ao LINQ to SQL de qualquer forma. ASP.NET MVC é compatível com qualquer tecnologia de acesso a dados.

## <a name="create-a-movie-database"></a>Criar um banco de dados do filme

Neste tutorial, para ilustrar como você pode criar classes de modelo – vamos criar um aplicativo de banco de dados de filme simples. A primeira etapa é criar um novo banco de dados. O aplicativo com o botão direito\_pasta de dados na janela do Gerenciador de soluções e selecione a opção de menu **adicionar, Item novo**. Selecione o **banco de dados do SQL Server** modelo, atribua o nome MoviesDB.mdf e clique no **Add** botão (consulte a Figura 1).


[![Aadição de um novo banco de dados do SQL Server](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)

**Figura 01**: Adicionando um novo banco de dados do SQL Server ([clique para exibir a imagem em tamanho normal](creating-model-classes-with-linq-to-sql-cs/_static/image3.png))


Depois de criar o novo banco de dados, é possível abrir o banco de dados, duas vezes no arquivo MoviesDB.mdf no aplicativo\_pasta de dados. Duas vezes no arquivo MoviesDB.mdf abre a janela do Gerenciador de servidores (consulte a Figura 2).

A janela do Gerenciador de servidores é chamada a janela Gerenciador de banco de dados ao usar o Visual Web Developer.


[![Ucantar a janela do Gerenciador de servidores](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)

**Figura 02**: Usando a janela do Gerenciador de servidores ([clique para exibir a imagem em tamanho normal](creating-model-classes-with-linq-to-sql-cs/_static/image6.png))


Precisamos adicionar uma tabela ao nosso banco de dados que representa nosso filmes. Clique com botão direito na pasta tabelas e selecione a opção de menu **adicionar nova tabela**. Selecionar essa opção de menu abre o Designer de tabela (veja a Figura 3).


[![Ucantar a janela do Gerenciador de servidores](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)

**Figura 03**: O Designer de tabela ([clique para exibir a imagem em tamanho normal](creating-model-classes-with-linq-to-sql-cs/_static/image9.png))


É preciso adicionar as colunas a seguir para nossa tabela de banco de dados:

| **Nome da coluna** | **Tipo de dados** | **Permitir nulos** |
| --- | --- | --- |
| Id | int | False |
| Título | Nvarchar(200) | False |
| Diretor | Nvarchar(50) | False |

Você precisa fazer duas coisas especiais para a coluna de Id. Primeiro, você precisa marcar a coluna de Id como uma coluna de chave primária, selecionando a coluna no Designer de tabela e clicando no ícone de uma chave. LINQ to SQL requer que você especifique suas colunas de chave primária quando executar inserções ou atualizações no banco de dados.

Em seguida, você precisará marcar a coluna Id como uma coluna de identidade, atribuindo o valor Sim para o **é identidade** propriedade (veja a Figura 3). Uma coluna de identidade é uma coluna que é atribuída um novo número automaticamente sempre que você adicionar uma nova linha de dados a uma tabela.

## <a name="create-linq-to-sql-classes"></a>Criar Classes LINQ to SQL

Nosso modelo MVC conterá o LINQ para SQL classes que representam a tabela de banco de dados tblMovie. A maneira mais fácil de criar essas classes LINQ to SQL é com o botão direito na pasta modelos, selecione **Add, o novo Item**, selecione o LINQ para o modelo de Classes do SQL, nomeie as classes de Movie.dbml e clique no **Add**botão (consulte a Figura 4).


[![Criando LINQ para classes SQL](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)

**Figura 04**: Criando o LINQ para SQL classes ([clique para exibir a imagem em tamanho normal](creating-model-classes-with-linq-to-sql-cs/_static/image12.png))


Imediatamente depois de criar o filme Classes LINQ to SQL, o Object Relational Designer é exibido. Você pode arrastar tabelas de banco de dados da janela Gerenciador de servidores para o Object Relational Designer para criar Classes LINQ to SQL que representam as tabelas de banco de dados específico. Precisamos adicionar a tabela de banco de dados de tblMovie em Object Relational Designer (consulte a Figura 5).


[![Ucantar o Object Relational Designer](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)

**Figura 05**: Usando o Object Relational Designer ([clique para exibir a imagem em tamanho normal](creating-model-classes-with-linq-to-sql-cs/_static/image15.png))


Por padrão, o Object Relational Designer cria uma classe com o mesmo nome como a tabela de banco de dados que você arrasta para o Designer. No entanto, não queremos chamar nossa classe `tblMovie`. Portanto, clique no nome da classe no Designer e altere o nome da classe para filme.

Por fim, lembre-se de clicar o **salvar** botão (a imagem de disquete) para salvar o LINQ to SQL Classes. Caso contrário, a Classes LINQ to SQL não gerado pelo Designer relacional de objeto.

## <a name="using-linq-to-sql-in-a-controller-action"></a>Usando LINQ to SQL em uma ação do controlador

Agora que temos nosso classes LINQ to SQL, podemos usar essas classes para recuperar dados do banco de dados. Nesta seção, você aprenderá a usar LINQ to SQL classes diretamente dentro de uma ação do controlador. Podemos vai exibir a lista de filmes da tabela de banco de dados tblMovies em uma exibição do MVC.

Primeiro, precisamos modificar a classe HomeController. Essa classe pode ser encontrada na pasta controladores do seu aplicativo. Modifique a classe para que ele se parece com a classe na listagem 1.

**Listagem 1 – `Controllers\HomeController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

O `Index()` ação na listagem 1 usa uma classe LINQ to SQL DataContext (o `MovieDataContext`) para representar o `MoviesDB` banco de dados. O `MoveDataContext` classe foi gerada pelo Visual Studio o Object Relational Designer.

Uma consulta LINQ é executada em relação a DataContext para recuperar todos os filmes do `tblMovies` tabela de banco de dados. A lista de filmes é atribuída a uma variável local chamada `movies`. Por fim, a lista de filmes é passada para o modo de exibição por meio de exibir dados.

Para mostrar os filmes, em seguida, precisamos modificar a exibição de índice. Você pode encontrar a exibição de índice no `Views\Home\` pasta. Atualize a exibição de índice para que ele se parece com o modo de exibição na listagem 2.

**Listagem 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

Observe que o modo de exibição do índice modificado inclui um `<%@ import namespace %>` diretiva na parte superior do modo de exibição. Essa diretiva importa o `MvcApplication1.Models namespace`. Precisamos esse namespace para trabalhar com o `model` classes – em particular, o `Movie` classe – no modo de exibição.

A exibição na listagem 2 contém uma `foreach` loop que itera em todos os itens representados pelo `ViewData.Model` propriedade. O valor de `Title` propriedade é exibida para cada `movie`.

Observe que o valor de `ViewData.Model` propriedade é convertida para um `IEnumerable`. Isso é necessário para executar um loop pelo conteúdo da `ViewData.Model`. Outra opção aqui é criar um tipo mais acentuado `view`. Quando você cria um tipo mais acentuado `view`, você converter o `ViewData.Model` propriedade para um tipo específico na classe code-behind de uma exibição.

Se você executar o aplicativo depois de modificar o `HomeController` classe e o índice de exibição, você obterá uma página em branco. Você obterá uma página em branco porque não há registros no filme a `tblMovies` tabela de banco de dados.

Para adicionar registros a `tblMovies` tabela de banco de dados, clique com botão direito a `tblMovies` tabela na janela do Gerenciador de servidores (janela do Gerenciador de banco de dados no Visual Web Developer) do banco de dados e selecione a opção de menu Mostrar dados da tabela. Você pode inserir `movie` registros usando a grade que aparece (veja a Figura 6).


[![Ifilmes nserting](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)

**Figura 06**: Inserção de filmes ([clique para exibir a imagem em tamanho normal](creating-model-classes-with-linq-to-sql-cs/_static/image18.png))


Depois de adicionar alguns registros de banco de dados para o `tblMovies` tabela e você executar o aplicativo, você verá a página na Figura 7. Todos os registros de banco de dados do filme são exibidos em uma lista com marcadores.


[![Displaying filmes com o modo de exibição do índice](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)

**Figura 07**: Exibição de filmes com o modo de exibição de índice ([clique para exibir a imagem em tamanho normal](creating-model-classes-with-linq-to-sql-cs/_static/image21.png))


## <a name="using-the-repository-pattern"></a>Usando o padrão de repositório

Na seção anterior, usamos o LINQ para SQL classes diretamente dentro de uma ação do controlador. Usamos o `MovieDataContext` diretamente a partir de classe a `Index()` ação do controlador. Não há nada de errado com isso no caso de um aplicativo simples. No entanto, trabalhar diretamente com o LINQ to SQL em uma classe de controlador cria problemas quando você precisa para criar um aplicativo mais complexo.

Usando LINQ to SQL dentro de uma classe de controlador torna difícil alternar as tecnologias de acesso no futuro. Por exemplo, você pode decidir alternar entre usar o Microsoft LINQ to SQL usando o Entity Framework da Microsoft como sua tecnologia de acesso a dados. Nesse caso, você precisaria reescrever cada controlador que acessa o banco de dados dentro de seu aplicativo.

Usando LINQ to SQL dentro de uma classe de controlador também torna difíceis de criar testes de unidade para seu aplicativo. Normalmente, você não deseja interagir com um banco de dados ao executar testes de unidade. Você deseja usar os testes de unidade para testar a lógica do aplicativo e não o servidor de banco de dados.

A fim de criar um aplicativo MVC, que é mais adaptável para futuras alterações e que podem ser testados com mais facilidade, você deve considerar usar o padrão de repositório. Quando você usa o padrão de repositório, você pode criar uma classe de repositório separado que contém todos os de sua lógica de acesso do banco de dados.

Quando você cria a classe de repositório, você pode criar uma interface que representa todos os métodos usados pela classe de repositório. Dentro dos controladores, você escreve seu código com base na interface em vez de no repositório. Dessa forma, você pode implementar o repositório usando tecnologias de acesso a dados diferentes no futuro.

A interface na listagem 3 é denominada `IMovieRepository` e representa um único método chamado `ListAll()`.

**Listagem 3 – `Models\IMovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

A classe de repositório na listagem 4 implementa o `IMovieRepository` interface. Observe que ela contém um método chamado `ListAll()` que corresponde ao método exigido pelo `IMovieRepository` interface.

**Listagem 4 – `Models\MovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

Por fim, o `MoviesController` classe na listagem 5 usa o padrão de repositório. Ele não usa mais LINQ para classes SQL diretamente.

**Listagem 5 – `Controllers\MoviesController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

Observe que o `MoviesController` classe na listagem 5 tem dois construtores. O primeiro construtor, o construtor sem parâmetros, é chamado quando o aplicativo é executado. Este construtor cria uma instância da `MovieRepository` de classe e o passa para o segundo construtor.

O segundo construtor tem um único parâmetro: um `IMovieRepository` parâmetro. Esse construtor simplesmente atribui o valor do parâmetro a um campo de nível de classe chamado `_repository`.

O `MoviesController` classe está aproveitando um padrão de design de software chamado o padrão de injeção de dependência. Em particular, ele está usando algo chamado injeção de dependência de construtor. Você pode ler mais sobre esse padrão, lendo o artigo a seguir por Martin Fowler:

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

Observe que todo o código na `MoviesController` classe (exceto o primeiro construtor) interage com o `IMovieRepository` interface em vez de real `MovieRepository` classe. O código interage com uma interface abstrata, em vez de uma implementação concreta da interface.

Se você deseja modificar a tecnologia de acesso de dados usada pelo aplicativo, você pode simplesmente implementar o `IMovieRepository` interface com uma classe que usa a tecnologia de acesso alternativo do banco de dados. Por exemplo, você pode criar uma `EntityFrameworkMovieRepository` classe ou um `SubSonicMovieRepository` classe. Porque a classe de controlador é programada com base na interface, você pode passar uma nova implementação de `IMovieRepository` para o controlador de classe e a classe continuará a funcionar.

Além disso, se você quiser testar o `MoviesController` classe, em seguida, você pode passar uma classe de repositório de filme falso para o `HomeController`. Você pode implementar o `IMovieRepository` classe com uma classe que não tem acesso, na verdade, o banco de dados, mas contém todos os métodos necessários do `IMovieRepository` interface. Dessa forma, você pode testar a unidade a `MoviesController` classe sem, na verdade, acessar um banco de dados real.

## <a name="summary"></a>Resumo

O objetivo deste tutorial era demonstrar como você pode criar classes de modelo do MVC, tirando proveito do Microsoft LINQ to SQL. Examinamos duas estratégias para exibir dados do banco de dados em um aplicativo ASP.NET MVC. Primeiro, criamos LINQ para classes SQL e usamos as classes diretamente dentro de uma ação do controlador. Usando o LINQ para classes SQL dentro de um controlador permite que você rapidamente e facilmente exibir dados de banco de dados em um aplicativo MVC.

Em seguida, exploramos um caminho um pouco mais difícil, mas definitivamente mais virtuoso, para exibir os dados do banco de dados. Podemos aproveitou o padrão de repositório e colocado todos nossa lógica de acesso do banco de dados em uma classe de repositório separado. Em nosso controller, escrevemos todo o nosso código em relação a uma interface em vez de uma classe concreta. A vantagem do padrão de repositório é que ele nos permite alterar facilmente as tecnologias de acesso de banco de dados no futuro, e ele nos permite testar facilmente a nossas classes de controlador.

> [!div class="step-by-step"]
> [Anterior](creating-model-classes-with-the-entity-framework-cs.md)
> [Próximo](displaying-a-table-of-database-data-cs.md)
