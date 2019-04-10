---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: Controles de fonte de dados | Microsoft Docs
author: microsoft
description: O controle DataGrid no ASP.NET 1. x marcado como um grande aprimoramento em acesso a dados em aplicativos da Web. No entanto, não era amigável poderia ter sido...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: 3ba9fdaaf655f6510d3ebf6ce0930fbf4000add3
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59388862"
---
# <a name="data-source-controls"></a>Controles de fonte de dados

por [Microsoft](https://github.com/microsoft)

> O controle DataGrid no ASP.NET 1. x marcado como um grande aprimoramento em acesso a dados em aplicativos da Web. No entanto, não era amigável poderia ter sido. Ela ainda exigia uma quantidade considerável de código para obter uma funcionalidade muito útil dele. Esse é o modelo em todos os esforços de acesso de dados em 1. x.


O controle DataGrid no ASP.NET 1. x marcado como um grande aprimoramento em acesso a dados em aplicativos da Web. No entanto, não era amigável poderia ter sido. Ela ainda exigia uma quantidade considerável de código para obter uma funcionalidade muito útil dele. Esse é o modelo em todos os esforços de acesso de dados em 1. x.

O ASP.NET 2.0 trata disso com parcialmente com controles de fonte de dados. Os controles de fonte de dados no ASP.NET 2.0 oferecem aos desenvolvedores um modelo declarativo para recuperação de dados, exibição de dados e editar dados. A finalidade dos controles de fonte de dados é fornecer uma representação consistente dos dados para controles ligados a dados, independentemente da fonte desses dados. O cerne dos controles da fonte de dados no ASP.NET 2.0 é a classe abstrata DataSourceControl. A classe DataSourceControl fornece uma implementação básica da interface IDataSource e a interface IListSource, o último permite que você atribua o controle de fonte de dados como a fonte de dados de um controle associado a dados (por meio da nova propriedade DataSourceId discutido posteriormente) e expor os dados nele como uma lista. Cada lista de dados de um controle de fonte de dados é exposta como um objeto DataSourceView. Acesso às instâncias do DataSourceView é fornecido pela interface IDataSource. Por exemplo, o método GetViewNames retorna ICollection que permite que você enumere o DataSourceViews associado com um controle de fonte de dados específico, e o método GetView permite que você acesse uma instância de DataSourceView específica por nome.

Controles de fonte de dados não tem nenhuma interface de usuário. Eles são implementados como controles de servidor para que eles podem dar suporte a sintaxe declarativa e para que eles tenham acesso ao estado da página, se desejado. Controles de fonte de dados não processam qualquer marcação HTML para o cliente.

> [!NOTE]
> Como você verá mais tarde, são também cache benefícios obtidos usando controles de fonte de dados.


## <a name="storing-connection-strings"></a>O armazenamento de cadeias de Conexão

Antes de entrarmos em observando como configurar controles de fonte de dados, que devemos abordar uma nova funcionalidade no ASP.NET 2.0 relacionadas a cadeias de caracteres de conexão. O ASP.NET 2.0 apresenta uma nova seção no arquivo de configuração que permite que você possa facilmente armazenar cadeias de caracteres de conexão que podem ser lidos dinamicamente em tempo de execução. O &lt;connectionStrings&gt; seção torna mais fácil armazenar cadeias de caracteres de conexão.

O trecho a seguir adiciona uma nova cadeia de caracteres de conexão.

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> Assim como ocorre com o &lt;appSettings&gt; seção, o &lt;connectionStrings&gt; seção aparece fora do &lt;System. Web&gt; seção no arquivo de configuração.


Para usar essa cadeia de caracteres de conexão, você pode usar a sintaxe a seguir ao definir o atributo ConnectionString de um controle de servidor.

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

O &lt;connectionStrings&gt; seção também pode ser criptografada para que informações confidenciais não são expostas. Essa capacidade será abordada em um módulo posterior.

## <a name="caching-data-sources"></a>Armazenamento em cache fontes de dados

Cada DataSourceControl fornece quatro propriedades para configurar o armazenamento em cache. EnableCaching, CacheDuration, CacheExpirationPolicy e CacheKeyDependency.

## <a name="enablecaching"></a>EnableCaching

EnableCaching é uma propriedade booliana que determina se o armazenamento em cache ou não está habilitada para o controle de fonte de dados.

## <a name="cacheduration-property"></a>Propriedade CacheDuration

A propriedade CacheDuration define o número de segundos que o cache permanece válido. Definir essa propriedade como **0** faz com que o cache permaneça válido até explicitamente invalidados.

## <a name="cacheexpirationpolicy-property"></a>CacheExpirationPolicy Property

A propriedade CacheExpirationPolicy pode ser definida como **absoluto** ou **deslizante**. Defini-lo como absoluta significa que a quantidade máxima de tempo que os dados serão armazenados em cache é o número de segundos especificado pela propriedade CacheDuration. Definindo-a para deslizante, o tempo de expiração é redefinido quando cada operação é executada.

## <a name="cachekeydependency-property"></a>Propriedade CacheKeyDependency

Se um valor de cadeia de caracteres for especificado para a propriedade CacheKeyDependency, o ASP.NET irá configurar uma nova dependência de cache com base em cadeia de caracteres. Isso permite que você explicitamente invalida o cache, simplesmente alterando ou removendo o CacheKeyDependency.

**Importante**: Se representação está habilitada e acesso para a fonte de dados e/ou o conteúdo de dados baseiam-se na identidade do cliente, é recomendável que o cache ser desabilitado definindo EnableCaching como False. Se o cache está habilitado neste cenário, e um usuário diferente do usuário que solicitou os dados emite uma solicitação, a autorização para a fonte de dados não é imposta. Os dados serão simplesmente ser servidos do cache.

## <a name="the-sqldatasource-control"></a>O controle SqlDataSource

O controle SqlDataSource permite que um desenvolvedor para acessar dados armazenados em qualquer banco de dados relacional que dá suporte ao ADO.NET. Ele pode usar o provedor de.NET para acessar um banco de dados do SQL Server, o provedor OLEDB, o provedor System.Data.Odbc ou provedor do OracleClient para acessar o Oracle. Portanto, o SqlDataSource é certamente não somente usado para acessar dados em um banco de dados do SQL Server.

Para usar o SqlDataSource, você simplesmente fornece um valor para a propriedade ConnectionString e especificar um comando SQL ou procedimento armazenado. O controle SqlDataSource se encarrega de trabalhar com a arquitetura subjacente do ADO.NET. Ele abre a conexão, consulta a fonte de dados ou executa o procedimento armazenado, retorna os dados e, em seguida, fecha a conexão para você.

> [!NOTE]
> Porque a classe DataSourceControl fecha automaticamente a conexão para você, ele deve reduzir o número de chamadas de cliente gerado pelo vazamento de conexões de banco de dados.


O trecho de código a seguir associa um controle DropDownList a um controle SqlDataSource usando a cadeia de conexão que é armazenada no arquivo de configuração, conforme mostrado acima.

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

Conforme ilustrado acima, a propriedade DataSourceMode do SqlDataSource Especifica o modo da fonte de dados. No exemplo acima, o DataSourceMode está definido como DataReader. Nesse caso, o SqlDataSource retornará um objeto IDataReader usando um cursor de somente avanço e somente leitura. O tipo especificado do objeto que é retornado é controlado pelo provedor que é usado. Nesse caso, estou usando o provedor de.NET conforme especificado na &lt;connectionStrings&gt; seção do arquivo Web. config. Portanto, o objeto retornado será do tipo SqlDataReader. Especificando um valor de DataSourceMode do conjunto de dados, os dados podem ser armazenados em um conjunto de dados no servidor. Esse modo permite que você adicione recursos, como classificação, paginação, etc. Se eu tivesse sido vinculação de dados SqlDataSource para um controle GridView, eu seria tiver escolhido o modo de conjunto de dados. No entanto, no caso de uma DropDownList, o modo de DataReader é a opção correta.

> [!NOTE]
> Ao armazenar em cache um SqlDataSource ou um AccessDataSource, a propriedade de DataSourceMode deve ser definida para o conjunto de dados. Se você habilitar o cache com um DataSourceMode do DataReader, ocorrerá uma exceção.


## <a name="sqldatasource-properties"></a>Propriedades do SqlDataSource

A seguir estão algumas das propriedades do controle SqlDataSource.

### <a name="cancelselectonnullparameter"></a>CancelSelectOnNullParameter

Um valor booliano que especifica se um comando select é cancelado se um dos parâmetros for nulo. True por padrão.

### <a name="conflictdetection"></a>ConflictDetection

Em uma situação em que vários usuários podem estar atualizando uma fonte de dados ao mesmo tempo, a propriedade ConflictDetection determina o comportamento do controle SqlDataSource. Essa propriedade é avaliada como um dos valores da enumeração ConflictOptions. Esses valores são **CompareAllValues** e **OverwriteChanges**. Se definido como OverwriteChanges, a última pessoa a gravar dados na fonte de dados substituirá qualquer alteração anterior. No entanto, se a propriedade ConflictDetection é definida como CompareAllValues, parâmetros são criados para as colunas retornadas pela SelectCommand e parâmetros também são criados para manter os valores originais em cada uma dessas colunas, permitindo que o SqlDataSource para Determine se os valores foram alterados desde que o SelectCommand foi executado.

### <a name="deletecommand"></a>DeleteCommand

Define ou obtém a cadeia de caracteres SQL usada ao excluir linhas do banco de dados. Isso pode ser uma consulta SQL ou um nome de procedimento armazenado.

### <a name="deletecommandtype"></a>DeleteCommandType

Define ou obtém o tipo de comando de exclusão, ou uma consulta SQL (texto) ou um procedimento armazenado (StoredProcedure).

### <a name="deleteparameters"></a>DeleteParameters

Retorna os parâmetros que são usados por DeleteCommand do objeto SqlDataSourceView associado ao controle SqlDataSource.

### <a name="oldvaluesparameterformatstring"></a>OldValuesParameterFormatString

Essa propriedade é usada para especificar o formato dos parâmetros de valor original em casos em que a propriedade ConflictDetection é definida como CompareAllValues. O padrão é {0} que significa que os parâmetros de valor original levará o mesmo nome que o parâmetro original. Em outras palavras, se o nome do campo for EmployeeID, o parâmetro do valor original seria @EmployeeID.

### <a name="selectcommand"></a>SelectCommand

Define ou obtém a cadeia de caracteres SQL que é usada para recuperar dados do banco de dados. Isso pode ser uma consulta SQL ou um nome de procedimento armazenado.

### <a name="selectcommandtype"></a>SelectCommandType

Define ou obtém o tipo do comando select, ou uma consulta SQL (texto) ou um procedimento armazenado (StoredProcedure).

### <a name="selectparameters"></a>SelectParameters

Retorna os parâmetros que são usados por SelectCommand do objeto SqlDataSourceView associado ao controle SqlDataSource.

### <a name="sortparametername"></a>SortParameterName

Obtém ou define o nome de um parâmetro de procedimento armazenado que é usado quando a classificação de dados recuperados pelo controle de fonte de dados. Válido somente quando SelectCommandType é definido como o procedimento armazenado.

### <a name="sqlcachedependency"></a>SqlCacheDependency

Uma cadeia de caracteres de ponto e vírgula delimitado por especificando os bancos de dados e tabelas usadas em uma dependência de cache do SQL Server. (Dependências de cache SQL serão abordadas em um módulo posterior.)

### <a name="updatecommand"></a>UpdateCommand

Define ou obtém a cadeia de caracteres SQL que é usada ao atualizar dados no banco de dados. Isso pode ser uma consulta SQL ou um nome de procedimento armazenado.

### <a name="updatecommandtype"></a>UpdateCommandType

Define ou obtém o tipo de comando de atualização, ou uma consulta SQL (texto) ou um procedimento armazenado (StoredProcedure).

### <a name="updateparameters"></a>UpdateParameters

Retorna os parâmetros que são usados pelo UpdateCommand do objeto SqlDataSourceView associado ao controle SqlDataSource.

## <a name="the-accessdatasource-control"></a>O controle AccessDataSource

O controle AccessDataSource deriva da classe SqlDataSource e é usado para associar dados a um banco de dados do Microsoft Access. A propriedade ConnectionString para o controle AccessDataSource é uma propriedade somente leitura. Em vez de usar a propriedade ConnectionString, a propriedade do arquivo de dados é usada para apontar para o banco de dados, conforme mostrado abaixo.

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

O AccessDataSource sempre definiremos o ProviderName de base SqlDataSource para OLEDB e conecta-se ao banco de dados usando o provedor Microsoft.Jet.OLEDB.4.0 OLE DB. Você não pode usar o controle AccessDataSource para se conectar a um banco de dados do Access protegido por senha. Se você precisa se conectar a um banco de dados protegido por senha, você deve usar o controle SqlDataSource.

> [!NOTE]
> Bancos de dados do Access armazenados dentro do site devem ser colocados no aplicativo\_diretório de dados. O ASP.NET não permite arquivos nesse diretório a serem procurados. Você precisará conceder permissões de leitura e gravação para o aplicativo da conta de processo\_diretório de dados ao usar bancos de dados do Access.


## <a name="the-xmldatasource-control"></a>O controle XmlDataSource

XmlDataSource é usado para vincular dados em dados XML para controles ligados a dados. Você pode associar a um arquivo XML usando a propriedade do arquivo de dados ou você pode associar a uma cadeia de caracteres XML usando a propriedade de dados. XmlDataSource expõe atributos XML como campos associáveis. Em casos em que você precisa para associar aos valores que não são representadas como atributos, você precisará usar uma transformação XSL. Você também pode usar as expressões XPath para filtrar os dados XML.

Considere o seguinte arquivo XML:

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

Observe que o XmlDataSource usa uma propriedade XPath de */gente* para filtrar apenas as &lt;pessoa&gt; nós. A DropDownList e em seguida, associa dados para o atributo de sobrenome usando a propriedade DataTextField.

Enquanto o controle XmlDataSource é usado principalmente para associar dados aos dados XML de somente leitura, é possível editar o arquivo de dados XML. Observe que nesses casos, a inserção automática, atualização e exclusão de informações no arquivo XML não acontece automaticamente como ocorre com outros controles de fonte de dados. Em vez disso, você terá de escrever código para editar manualmente os dados usando os seguintes métodos do controle XmlDataSource.

### <a name="getxmldocument"></a>GetXmlDocument

Recupera um objeto XmlDocument que contém o código XML recuperado pelo XmlDataSource.

### <a name="save"></a>Salvar

Salva o XmlDocument na memória para a fonte de dados.

É importante perceber que o método Save só funcionarão quando as duas seguintes condições forem atendidas:

1. XmlDataSource está usando a propriedade do arquivo de dados para associar a um arquivo XML em vez da propriedade de dados para associar aos dados XML na memória.
2. Nenhuma transformação é especificada por meio da propriedade de transformação ou TransformFile.

Observe também que o método Save pode produzir resultados inesperados quando chamado por vários usuários simultaneamente.

## <a name="the-objectdatasource-control"></a>O controle ObjectDataSource

Os controles de fonte de dados que abordamos até esse ponto são excelentes opções para aplicativos de duas camadas, onde o controle de fonte de dados se comunica diretamente com o armazenamento de dados. No entanto, muitos aplicativos do mundo real são aplicativos de várias camadas em que um controle de fonte de dados talvez precise se comunicar com um objeto comercial que, por sua vez, se comunica com a camada de dados. Nessas situações, o ObjectDataSource preenche a fatura muito bem. O ObjectDataSource funciona em conjunto com um objeto de origem. O controle ObjectDataSource criará uma instância do objeto de origem, chame o método especificado e descarte a instância de objeto todos dentro do escopo de uma única solicitação, se o objeto tiver métodos de instância, em vez de métodos estáticos (Shared no Visual Basic). Portanto, seu objeto deve ser sem monitoração de estado. Ou seja, seu objeto deve adquirir e liberar todos os recursos necessários dentro do período de uma única solicitação. Você pode controlar como o objeto de origem é criado ao manipular o evento ObjectCreating do controle ObjectDataSource. Você pode criar uma instância do objeto de origem e, em seguida, definir a propriedade ObjectInstance da classe ObjectDataSourceEventArgs a essa instância. O controle ObjectDataSource usará a instância que é criada no evento ObjectCreating em vez de criar uma instância por conta própria.

Se o objeto de origem para um controle ObjectDataSource expõe métodos estáticos públicos (Shared no Visual Basic) que podem ser chamados para recuperar e modificar dados, um controle ObjectDataSource chamará esses métodos diretamente. Se um controle ObjectDataSource deve criar uma instância do objeto de origem para fazer chamadas de método, o objeto deve incluir um construtor público sem parâmetros. O controle ObjectDataSource chamará este construtor quando ele cria uma nova instância do objeto de fonte.

Se o objeto de origem não contiver um construtor público sem parâmetros, você pode criar uma instância do objeto de origem que será usado pelo controle ObjectDataSource no evento ObjectCreating.

## <a name="specifying-object-methods"></a>Especificação dos métodos de objeto

O objeto de origem para um controle ObjectDataSource pode conter qualquer número de métodos que são usados para selecionar, inserir, atualizar ou excluir dados. Esses métodos são chamados pelo controle ObjectDataSource com base no nome do método, conforme identificado usando a propriedade SelectMethod, InsertMethod, UpdateMethod ou DeleteMethod do controle ObjectDataSource. O objeto de origem também pode incluir um método SelectCount opcional, que é identificado pelo controle ObjectDataSource usando a propriedade SelectCountMethod, que retorna a contagem do número total de objetos na fonte de dados. O controle ObjectDataSource chamará o método de SelectCount depois que um método de seleção foi chamado para recuperar o número total de registros na fonte de dados para uso quando a paginação.

## <a name="lab-using-data-source-controls"></a>Laboratório usando controles de fonte de dados

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>Exercício 1: exibindo dados com o controle SqlDataSource

O exercício a seguir usa o controle SqlDataSource para se conectar ao banco de dados Northwind. Ele pressupõe que você tenha acesso ao banco de dados Northwind em uma instância do SQL Server 2000.

1. Crie um novo site da Web do ASP.NET.
2. Adicione um novo arquivo Web. config.

    1. Clique com botão direito no projeto no Gerenciador de soluções e clique em Adicionar Novo Item.
    2. Escolha o arquivo de configuração Web da lista de modelos e clique em Adicionar.
3. Editar o &lt;connectionStrings&gt; seção da seguinte maneira: 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. Alternar para a exibição de código e adicione um atributo de ConnectionString e um atributo SelectCommand para o &lt;asp: SqlDataSource&gt; controlar da seguinte maneira: 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. Na exibição de Design, adicione um novo controle GridView.
6. No menu suspenso Escolher fonte de dados, no menu Tarefas GridView, escolha SqlDataSource1.
7. Clique duas vezes em Default. aspx e escolha exibir no navegador, no menu. Clique em Sim, quando solicitado a salvar.
8. O GridView exibe os dados da tabela produtos.

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>Exercício 2 - edição de dados com o controle SqlDataSource

O exercício a seguir demonstra como associar dados DropDownList usando a sintaxe declarativa de controle e permite que você edite os dados apresentados no controle DropDownList.

1. No modo de Design, exclua o controle GridView de Default. aspx. 

    **Importante**: Mantenha o controle SqlDataSource na página.
2. Adicione um controle DropDownList para default. aspx.
3. Alternar a exibição da fonte.
4. Adicione um atributo DataSourceId DataTextField e DataValueField para o &lt;asp: DropDownList&gt; controlar da seguinte maneira: 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. Salve o default. aspx e exibi-lo no navegador. Observe que a DropDownList contém todos os produtos do banco de dados Northwind.
6. Feche o navegador.
7. Na exibição da fonte de Default. aspx, adicione um novo controle de caixa de texto abaixo do controle DropDownList. Altere a propriedade de ID da caixa de texto para txtProductName.
8. Sob o controle de caixa de texto, adicione um novo controle de botão. Altere a propriedade de ID do botão para btnUpdate e a propriedade de texto como **nome do produto de atualização**.
9. Na exibição da fonte de Default. aspx, adicione uma propriedade UpdateCommand e dois UpdateParameters novo à marca SqlDataSource da seguinte maneira: 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > Observe que há que dois parâmetros (ProductName e ProductID) adicionados neste código de atualização. Esses parâmetros são mapeados para a propriedade Text da caixa de texto txtProductName e a propriedade SelectedValue do ddlProducts DropDownList.
10. Alterne para modo de Design e clique duas vezes no controle de botão para adicionar um manipulador de eventos.
11. Adicione o seguinte código para o btnUpdate\_clique em código: 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. Clique duas vezes em Default. aspx e escolha para exibi-lo no navegador. Clique em Sim, quando for solicitado a salvar todas as alterações.
13. O ASP.NET 2.0 classes parciais permitem que a compilação em tempo de execução. Não é necessário criar um aplicativo para ver as alterações de código entrarem em vigor.
14. Selecione um produto na lista suspensa.
15. Insira um novo nome para o produto selecionado na caixa de texto e, em seguida, clique no botão de atualização.
16. O nome do produto é atualizado no banco de dados.

## <a name="exercise-3-using-the-objectdatasource-control"></a>Exercício 3 usando o controle ObjectDataSource

Este exercício demonstrará como usar o controle ObjectDataSource e um objeto de fonte para interagir com o banco de dados Northwind.

1. Clique com botão direito no projeto no Gerenciador de soluções e clique em Adicionar Novo Item.
2. Selecione o formulário da Web na lista de modelos. Altere o nome para object.aspx e clique em Adicionar.
3. Clique com botão direito no projeto no Gerenciador de soluções e clique em Adicionar Novo Item.
4. Selecione a classe na lista de modelos. Altere o nome da classe para NorthwindData.cs e clique em Adicionar.
5. Clique em Sim, quando solicitado a adicionar a classe para o aplicativo\_pasta de código.
6. Adicione o seguinte código ao arquivo NorthwindData.cs: 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. Adicione o seguinte código para a exibição da fonte de object.aspx: 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. Salve todos os arquivos e procurar object.aspx.
9. Interagir com a interface exibindo detalhes, edição de funcionários, adicionando os funcionários, e exclusão de funcionários.
