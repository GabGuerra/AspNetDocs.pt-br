---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
title: Criar procedimentos armazenados e funções definidas pelo usuário com código (c#) gerenciado | Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server 2005 integra-se com o .NET Common Language Runtime para permitir que os desenvolvedores a criar objetos de banco de dados por meio de código gerenciado. Este tutorial...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 213eea41-1ab4-4371-8b24-1a1a66c515de
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-stored-procedures-and-user-defined-functions-with-managed-code-cs
msc.type: authoredcontent
ms.openlocfilehash: a6d6dc7b45d2891d3124794bf7b10f3a7d065130
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59392437"
---
# <a name="creating-stored-procedures-and-user-defined-functions-with-managed-code-c"></a>Criar procedimentos armazenados e funções definidas pelo usuário com código gerenciado (C#)

por [Scott Mitchell](https://twitter.com/ScottOnWriting)

[Baixar o código](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_75_CS.zip) ou [baixar PDF](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/datatutorial75cs1.pdf)

> Microsoft SQL Server 2005 integra-se com o .NET Common Language Runtime para permitir que os desenvolvedores a criar objetos de banco de dados por meio de código gerenciado. Este tutorial mostra como criar procedimentos armazenados gerenciados e gerenciados de funções definidas pelo usuário com seu código Visual Basic ou c#. Também vemos como essas edições do Visual Studio permitem que você depurar esses objetos de banco de dados gerenciado.


## <a name="introduction"></a>Introdução

Bancos de dados, como s do Microsoft SQL Server 2005 usam o [linguagem de consulta Transact-Structured (T-SQL)](http://en.wikipedia.org/wiki/Transact-SQL) para inserir, modificar e recuperação de dados. A maioria dos sistemas de banco de dados incluem construções para agrupar uma série de instruções SQL que, em seguida, pode ser executado como uma unidade única e reutilizável. Procedimentos armazenados são um exemplo. A outra é *funções definidas pelo usuário*(UDFs), uma construção que vamos examinar mais detalhadamente na etapa 9.

Em seu núcleo, o SQL foi projetado para trabalhar com conjuntos de dados. O `SELECT`, `UPDATE`, e `DELETE` instruções se aplicam a todos os registros na tabela correspondente por natureza e são limitadas apenas pelos seus `WHERE` cláusulas. Ainda há muitos recursos de linguagem projetados para trabalhar com um registro por vez e manipulação de dados escalares. [`CURSOR` s](http://www.sqlteam.com/item.asp?ItemID=553) permitem um conjunto de registros para estar em um loop por meio de um de cada vez. Funções de manipulação, como cadeia de caracteres `LEFT`, `CHARINDEX`, e `PATINDEX` funcionam com dados escalares. SQL também inclui instruções de fluxo de controle, como `IF` e `WHILE`.

Antes do Microsoft SQL Server 2005, procedimentos armazenados e UDFs só pode ser definidos como uma coleção de instruções T-SQL. SQL Server 2005, no entanto, foi projetado para fornecer integração com o [Common Language Runtime (CLR)](https://msdn.microsoft.com/netframework/aa497266.aspx), que é o tempo de execução usado por todos os assemblies do .NET. Consequentemente, os procedimentos armazenados e UDFs em um banco de dados do SQL Server 2005 podem ser criados usando código gerenciado. Ou seja, você pode criar um procedimento armazenado ou UDF como um método em uma classe c#. Isso permite que esses procedimentos armazenados e UDFs para utilizar a funcionalidade no .NET Framework e de suas próprias classes personalizadas.

Neste tutorial, que vamos examinar como criar gerenciado procedimentos armazenados e funções definidas pelo usuário e como integrá-los ao nosso banco de dados Northwind. Permitir que o s começar!

> [!NOTE]
> Objetos de banco de dados gerenciados oferecem algumas vantagens sobre suas contrapartes SQL. Riqueza de linguagem e familiaridade e a capacidade de reutilizar a lógica e o código existente são as principais vantagens. Mas os objetos de banco de dados gerenciado são provavelmente será menos eficiente ao trabalhar com conjuntos de dados que não envolvem muita lógica de procedimento. Para uma discussão mais completa sobre as vantagens de usar código gerenciado em comparação com o T-SQL, confira a [vantagens de usar código gerenciado para criar objetos de banco de dados](https://msdn.microsoft.com/library/k2e1fb36(VS.80).aspx).


## <a name="step-1-moving-the-northwind-database-out-ofappdata"></a>Etapa 1: Movendo o banco de dados Northwind de`App_Data`

Até agora todos os nossos tutoriais de tem usado um arquivo de banco de dados do Microsoft SQL Server 2005 Express Edition em s aplicativo web `App_Data` pasta. Colocar o banco de dados `App_Data` simplificado distribuindo e executando esses tutoriais como todos os arquivos foram localizados dentro de um diretório e não necessária nenhuma etapa de configuração adicionais para testar o tutorial.

Para este tutorial, no entanto, let s mover o banco de dados Northwind de `App_Data` e registre-o explicitamente com a instância de banco de dados do SQL Server 2005 Express Edition. Enquanto estamos pode executar as etapas neste tutorial com o banco de dados a `App_Data` pasta, um número das etapas é feito muito mais simples, registrando explicitamente o banco de dados com a instância de banco de dados do SQL Server 2005 Express Edition.

O download para este tutorial tem os arquivos de dois bancos de dados - `NORTHWND.MDF` e `NORTHWND_log.LDF` - colocado em uma pasta chamada `DataFiles`. Se você estiver acompanhando com sua própria implementação dos tutoriais, feche o Visual Studio e mova os `NORTHWND.MDF` e `NORTHWND_log.LDF` arquivos do site do s `App_Data` para uma pasta fora do site. Depois que os arquivos de banco de dados foram movidos para outra pasta, é preciso registrar o banco de dados Northwind com a instância de banco de dados do SQL Server 2005 Express Edition. Isso pode ser feito no SQL Server Management Studio. Se você tiver um não - Express Edition do SQL Server 2005 instalado em seu computador, em seguida, você provavelmente já terá Management Studio instalado. Se você tiver o SQL Server 2005 Express Edition em seu computador, reserve um tempo para baixar e instalar somente [Microsoft SQL Server Management Studio Express](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796).

Inicie o SQL Server Management Studio. Como mostra a Figura 1, o Management Studio é iniciado perguntando qual servidor para se conectar ao. Insira localhost\SQLExpress para o nome do servidor, escolha autenticação do Windows na lista suspensa de autenticação e clique em conectar.


![Conectar-se à instância do banco de dados apropriado](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image1.png)

**Figura 1**: Conectar-se à instância do banco de dados apropriado


Quando você tiver conectado, a janela Pesquisador de objetos listará informações sobre a instância de banco de dados do SQL Server 2005 Express Edition, incluindo seus bancos de dados, informações de segurança, as opções de gerenciamento e assim por diante.

É necessário anexar o banco de dados Northwind o `DataFiles` pasta (ou onde quer que você talvez tenha movido) para a instância de banco de dados do SQL Server 2005 Express Edition. Clique com botão direito na pasta de bancos de dados e escolha a opção de anexar o menu de contexto. Isso abrirá a caixa de diálogo anexar bancos de dados. Clique no botão Adicionar, fazer drill down até apropriado `NORTHWND.MDF` de arquivo e, em seguida, clique em Okey. Neste ponto, sua tela deve ser semelhante da Figura 2.


[![Conectar-se à instância do banco de dados apropriado](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image3.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image2.png)

**Figura 2**: Conectar-se à instância apropriada do banco de dados ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image4.png))


> [!NOTE]
> Ao conectar-se à instância do SQL Server 2005 Express Edition com o Management Studio a caixa de diálogo anexar bancos de dados não permite fazer uma busca detalhada em diretórios de perfil do usuário, como Meus documentos. Portanto, certifique-se de colocar o `NORTHWND.MDF` e `NORTHWND_log.LDF` arquivos em um diretório de perfil de não usuário.


Clique no botão Okey para anexar o banco de dados. A caixa de diálogo anexar bancos de dados será fechado e o Pesquisador de objetos agora deve listar o banco de dados just-anexado. As chances são de banco de dados tem um nome como Northwind `9FE54661B32FDD967F51D71D0D5145CC_LINE ARTICLES\DATATUTORIALS\VOLUME 3\CSHARP\73\ASPNET_DATA_TUTORIAL_75_CS\APP_DATA\NORTHWND.MDF`. Renomear o banco de dados Northwind clicando duas vezes no banco de dados e escolher a renomeação.


![Renomear o banco de dados Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image5.png)

**Figura 3**: Renomear o banco de dados Northwind


## <a name="step-2-creating-a-new-solution-and-sql-server-project-in-visual-studio"></a>Etapa 2: Criando uma nova solução e projeto do SQL Server no Visual Studio

Para criar procedimentos armazenados gerenciados ou UDFs no SQL Server 2005 escreveremos o procedimento armazenado e a lógica UDF como o código c# em uma classe. Depois que o código foi escrito, será necessário compilar essa classe em um assembly (um `.dll` arquivo), registrar o assembly com o banco de dados do SQL Server e, em seguida, criar um procedimento armazenado ou UDF no banco de dados que aponta para o método correspondente em o assembly. Essas etapas podem ser executadas manualmente. Podemos criar o código em qualquer texto editor, compilá-lo na linha de comando usando o compilador do c# ([`csc.exe`](https://msdn.microsoft.com/library/ms379563(vs.80).aspx)), registrá-lo com o banco de dados usando o [ `CREATE ASSEMBLY` ](https://msdn.microsoft.com/library/ms189524.aspx) comando ou do gerenciamento Studio e adicione o procedimento armazenado ou o objeto UDF através de meios semelhantes. Felizmente, as versões Professional e sistemas de equipe do Visual Studio incluem um tipo de projeto do SQL Server que automatiza a essas tarefas. Neste tutorial, orientaremos pelas usando o tipo de projeto do SQL Server para criar um procedimento armazenado gerenciado e UDF.

> [!NOTE]
> Se você estiver usando o Visual Web Developer ou Standard edition do Visual Studio, você precisará usar a abordagem manual em vez disso. Etapa 13 fornece instruções detalhadas para executar essas etapas manualmente. Eu recomendo que você leia as etapas 2 a 12 antes de ler a etapa 13, pois essas etapas incluem instruções de configuração do SQL Server importantes que devem ser aplicadas, independentemente de qual versão do Visual Studio que você está usando.


Comece abrindo o Visual Studio. No menu Arquivo, escolha o novo projeto para exibir a caixa de diálogo Novo projeto caixa (veja a Figura 4). Fazer drill down até o tipo de projeto de banco de dados e, em seguida, nos modelos listados à direita, optar por criar um novo projeto do SQL Server. Optei por Nomeie esse projeto `ManagedDatabaseConstructs` e colocou-o dentro de uma solução chamada `Tutorial75`.


[![Criar um novo projeto do SQL Server](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image7.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image6.png)

**Figura 4**: Criar um novo projeto do SQL Server ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image8.png))


Clique no botão Okey na caixa de diálogo Novo projeto para criar a solução e projeto do SQL Server.

Um projeto do SQL Server está ligado a um determinado banco de dados. Consequentemente, depois de criar o novo projeto do SQL Server são imediatamente perguntamos para especificar essas informações. Figura 5 mostra a caixa de diálogo Nova referência de banco de dados que foram preenchida para apontar para o banco de dados Northwind que são registrados na instância de banco de dados do SQL Server 2005 Express Edition novamente na etapa 1.


![Associar o projeto do SQL Server com o banco de dados Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image9.png)

**Figura 5**: Associar o projeto do SQL Server com o banco de dados Northwind


Para depurar os procedimentos armazenados gerenciados e UDFs criaremos dentro desse projeto, precisamos habilitar o suporte para a conexão de depuração SQL/CLR. Sempre que um projeto do SQL Server associando um novo banco de dados (como fizemos na Figura 5), Visual Studio pergunta se você deseja habilitar a depuração SQL/CLR a conexão (consulte a Figura 6). Clique em Sim.


![Habilitar a depuração SQL/CLR](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image10.png)

**Figura 6**: Habilitar a depuração SQL/CLR


Neste ponto o novo projeto do SQL Server tiver sido adicionado à solução. Ele contém uma pasta chamada `Test Scripts` com um arquivo chamado `Test.sql`, que é usado para depurar os objetos de banco de dados gerenciados criados no projeto. Vamos examinar depuração na etapa 12.

Agora adicionamos novos procedimentos armazenados gerenciados e UDFs para este projeto, mas antes que deixamos s primeiro incluir nosso aplicativo web existente na solução. No menu Arquivo, selecione a opção de adicionar e escolha o Site da Web existente. Navegue até a pasta do site apropriado e clique em Okey. Como mostra a Figura 7, isso atualizará a solução para incluir dois projetos: o site e o `ManagedDatabaseConstructs` projeto do SQL Server.


![O Gerenciador de soluções agora inclui dois projetos](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image11.png)

**Figura 7**: O Gerenciador de soluções agora inclui dois projetos


O `NORTHWNDConnectionString` valor em `Web.config` atualmente faz referência a `NORTHWND.MDF` do arquivo no `App_Data` pasta. Já que removemos esse banco de dados `App_Data` e o registro explicitamente na instância de banco de dados do SQL Server 2005 Express Edition, precisamos atualizar proporcionalmente o `NORTHWNDConnectionString` valor. Abra o `Web.config` arquivo no site e altere o `NORTHWNDConnectionString` valor para que lê a cadeia de caracteres de conexão: `Data Source=localhost\SQLExpress;Initial Catalog=Northwind;Integrated Security=True`. Após essa alteração, seu `<connectionStrings>` seção `Web.config` deve ser semelhante ao seguinte:


[!code-xml[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample1.xml)]

> [!NOTE]
> Conforme discutido na [tutorial anterior](debugging-stored-procedures-cs.md), durante a depuração de um objeto do SQL Server de um aplicativo cliente, como um site ASP.NET, é preciso desabilitar o pooling de conexão. A cadeia de caracteres de conexão mostrada acima desabilita o pooling de conexão ( `Pooling=false` ). Se você não pretende depurar o UDFs e procedimentos armazenados gerenciados pelo site do ASP.NET, habilite o pooling de conexão.


## <a name="step-3-creating-a-managed-stored-procedure"></a>Etapa 3: Criando um procedimento armazenado gerenciado

Para adicionar um procedimento armazenado gerenciado para o banco de dados Northwind, primeiro precisamos criar o procedimento armazenado como um método no projeto do servidor SQL. Gerenciador de soluções, clique com botão direito no `ManagedDatabaseConstructs` nome do projeto e escolha Adicionar um novo item. Isso exibirá a caixa de diálogo Add New Item, que lista os tipos de objetos de banco de dados gerenciado que podem ser adicionados ao projeto. Como mostra a Figura 8, isso inclui procedimentos armazenados e funções definidas pelo usuário, entre outros.

Deixe o s começar pela adição de um procedimento armazenado que simplesmente retorna todos os produtos que foram descontinuados. Nomeie o novo arquivo de procedimento armazenado `GetDiscontinuedProducts.cs`.


[![Adicionar um novo procedimento armazenado chamado GetDiscontinuedProducts.cs](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image13.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image12.png)

**Figura 8**: Adicione um novo chamado procedimento de armazenado `GetDiscontinuedProducts.cs` ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image14.png))


Isso criará um novo arquivo de classe em c# com o seguinte conteúdo:


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample2.cs)]

Observe que o procedimento armazenado é implementado como um `static` método dentro de uma `partial` arquivo de classe chamado `StoredProcedures`. Além disso, o `GetDiscontinuedProducts` método é decorado com o `SqlProcedure attribute`, que marca o método como um procedimento armazenado.

O código a seguir cria uma `SqlCommand` objeto e define seu `CommandText` para um `SELECT` consulta que retorna todas as colunas da `Products` tabela de produtos cujos `Discontinued` campo é igual a 1. Em seguida, ele executa o comando e envia os resultados para o aplicativo cliente. Adicione este código para o `GetDiscontinuedProducts` método.


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample3.cs)]

Todos os objetos de banco de dados gerenciado têm acesso a um [ `SqlContext` objeto](https://msdn.microsoft.com/library/ms131108.aspx) que representa o contexto do chamador. O `SqlContext` fornece acesso a um [ `SqlPipe` objeto](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx) por meio de seu [ `Pipe` propriedade](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.pipe.aspx). Isso `SqlPipe` objeto é usado para ferry informações entre o banco de dados do SQL Server e o aplicativo de chamada. Como o nome sugere, o [ `ExecuteAndSend` método](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.executeandsend.aspx) executa um passado-in `SqlCommand` objeto e envia os resultados de volta para o aplicativo cliente.

> [!NOTE]
> Objetos de banco de dados gerenciado são mais adequados para procedimentos armazenados e UDFs que usam a lógica de procedimento em vez de lógica baseada em conjunto. Trabalhando com conjuntos de dados em uma base linha por linha ou trabalhando com dados escalares envolve a lógica de procedimento. O `GetDiscontinuedProducts` não envolve o método que acabamos de criar, no entanto, nenhuma lógica de procedimento. Portanto, seria o ideal é implementado como um procedimento armazenado T-SQL. Ele é implementado como um procedimento armazenado gerenciado para demonstrar as etapas necessárias para criar e implantar gerenciado procedimentos armazenados.


## <a name="step-4-deploying-the-managed-stored-procedure"></a>Etapa 4: Implantando o procedimento armazenado gerenciado

Com esse código é concluído, você está pronto para implantá-lo no banco de dados Northwind. Implantar um projeto do SQL Server compila o código em um assembly, registra o assembly com o banco de dados e cria objetos correspondentes no banco de dados, vinculando-as para os métodos apropriados no assembly. O conjunto exato das tarefas executadas pela opção de implantar com mais precisão está escrito na etapa 13. Clique com botão direito no `ManagedDatabaseConstructs` nome no Gerenciador de soluções do projeto e escolha a opção de implantar. No entanto, a implantação falhará com o seguinte erro: Sintaxe incorreta próxima a 'Externo'. Você talvez precise definir o nível de compatibilidade do banco de dados atual para um valor mais alto para habilitar esse recurso. Consulte a Ajuda para o procedimento armazenado `sp_dbcmptlevel`.

Essa mensagem de erro ocorre ao tentar registrar o assembly no banco de dados Northwind. Para registrar um assembly com um banco de dados do SQL Server 2005, o nível de compatibilidade do banco de dados s deve ser definido como 90. Por padrão, os novos bancos de dados do SQL Server 2005 têm um nível de compatibilidade 90. No entanto, os bancos de dados criados usando o Microsoft SQL Server 2000 tem um nível de compatibilidade padrão de 80. Como o banco de dados Northwind inicialmente era um banco de dados do Microsoft SQL Server 2000, o seu nível de compatibilidade está definido como 80 e, portanto, precisa ser aumentado para 90 para registrar objetos de banco de dados gerenciado.

Para atualizar o nível de compatibilidade do banco de dados s, abra uma janela nova consulta no Management Studio e digite:


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample4.sql)]

Clique no ícone executar na barra de ferramentas para executar a consulta acima.


[![Atualizar o nível de compatibilidade do banco de dados Northwind s](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image16.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image15.png)

**Figura 9**: Atualizar o banco de dados Northwind s de nível de compatibilidade ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image17.png))


Depois de atualizar o nível de compatibilidade, reimplante o projeto do SQL Server. Neste momento a implantação deverá ser concluída sem erros.

Retornar para o SQL Server Management Studio, clique com botão direito no banco de dados Northwind no Pesquisador de objetos e escolha atualizar. Em seguida, fazer uma busca detalhada para a pasta de programabilidade e, em seguida, expanda a pasta de módulos (assemblies). Como mostra a Figura 10, o banco de dados Northwind agora inclui o assembly gerado pelo `ManagedDatabaseConstructs` projeto.


![O Assembly de ManagedDatabaseConstructs está agora registrado com o banco de dados Northwind](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image18.png)

**Figura 10**: O `ManagedDatabaseConstructs` Assembly é registrado com o banco de dados Northwind


Também, expanda a pasta de procedimentos armazenados. Lá você verá um procedimento armazenado denominado `GetDiscontinuedProducts`. Esse procedimento armazenado foi criado pelo processo de implantação e aponta para o `GetDiscontinuedProducts` método no `ManagedDatabaseConstructs` assembly. Quando o `GetDiscontinuedProducts` procedimento armazenado é executado, ele, por sua vez, executa o `GetDiscontinuedProducts` método. Como esse é um procedimento armazenado gerenciado não pode ser editado por meio do Management Studio (portanto, o ícone de cadeado ao lado do nome do procedimento armazenado).


![O procedimento armazenado de GetDiscontinuedProducts está listado na pasta de procedimentos armazenados](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image19.png)

**Figura 11**: O `GetDiscontinuedProducts` procedimento armazenado está listado na pasta de procedimentos armazenados


Ainda há mais um obstáculo temos superar antes que podemos chamar o procedimento armazenado gerenciado: o banco de dados está configurado para impedir a execução de código gerenciado. Verificar isso abrindo uma nova janela de consulta e executar o `GetDiscontinuedProducts` procedimento armazenado. Você receberá a seguinte mensagem de erro: A execução do código do usuário no .NET Framework está desabilitada. Habilite a opção de configuração clr habilitado.

Para examinar as informações de configuração do banco de dados s Northwind, digite e execute o comando `exec sp_configure` na janela de consulta. Isso mostra que o clr habilitado definindo no momento é definido como 0.


[![O clr habilitado configuração é atualmente definido como 0](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image21.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image20.png)

**Figura 12**: O clr habilitado configuração está atualmente definida como 0 ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image22.png))


Observe que cada configuração na Figura 12 tem quatro valores listado com ele: o mínimo e valores máximos e a configuração e valores de execução. Para atualizar o valor de configuração para a configuração de clr habilitado, execute o seguinte comando:


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample5.sql)]

Se você executar novamente o `exec sp_configure` você verá que a instrução acima atualizado o valor de config da configuração de clr habilitado s para 1, mas o valor de execução ainda está definido como 0. Para que essa alteração de configuração entrem em vigor, é preciso executar o [ `RECONFIGURE` comando](https://msdn.microsoft.com/library/ms176069.aspx), que definirá o valor de execução para o valor da configuração atual. Basta digitar `RECONFIGURE` na janela de consulta e clique no ícone executar na barra de ferramentas. Se você executar `exec sp_configure` agora você deve ver um valor de 1 para a configuração de configuração do clr habilitado s e executar valores.

Com a configuração de clr habilitado completa, estamos prontos para executar o gerenciado `GetDiscontinuedProducts` procedimento armazenado. Na janela de consulta, digite e execute o comando `exec` `GetDiscontinuedProducts`. Chamar o procedimento armazenado faz com que o código gerenciado correspondente no `GetDiscontinuedProducts` método a ser executado. Esse código emite um `SELECT` consulta para retornar todos os produtos são descontinuados e retorna esses dados para o aplicativo de chamada, que é o SQL Server Management Studio nesta instância. Management Studio recebe esses resultados e os exibe na janela de resultados.


[![O GetDiscontinuedProducts procedimento armazenado retorna todos os produtos de descontinuados](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image24.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image23.png)

**Figura 13**: O `GetDiscontinuedProducts` armazenados procedimento retorna todos os produtos descontinuados ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image25.png))


## <a name="step-5-creating-managed-stored-procedures-that-accept-input-parameters"></a>Etapa 5: Criando gerenciado procedimentos armazenados que aceitam parâmetros de entrada

Muitas das consultas e procedimentos armazenados que criamos durante esses tutoriais usou *parâmetros*. Por exemplo, nos [criando novos procedimentos armazenados para o s TableAdapters do conjunto de dados tipado](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) tutorial, criamos um procedimento armazenado denominado `GetProductsByCategoryID` que aceita um parâmetro de entrada chamado `@CategoryID`. O procedimento armazenado, em seguida, retornados todos os produtos cujos `CategoryID` campo correspondeu ao valor de fornecido `@CategoryID` parâmetro.

Para criar um procedimento armazenado gerenciado que aceita parâmetros de entrada, basta especifica esses parâmetros na definição do método s. Para ilustrar isso, let s adicionar outro procedimento armazenado gerenciado para o `ManagedDatabaseConstructs` projeto chamado `GetProductsWithPriceLessThan`. Esse procedimento armazenado gerenciado aceita um parâmetro de entrada especificando um preço e retornará todos os produtos cujo `UnitPrice` campo for menor que o valor do parâmetro s.

Para adicionar um novo procedimento armazenado ao projeto, clique com botão direito no `ManagedDatabaseConstructs` nome do projeto e escolha Adicionar um novo procedimento armazenado. Dê o nome `GetProductsWithPriceLessThan.cs` para o arquivo. Como vimos na etapa 3, isso criará um novo arquivo de classe em c# com um método chamado `GetProductsWithPriceLessThan` colocados dentro de `partial` classe `StoredProcedures`.

Atualizar o `GetProductsWithPriceLessThan` definição de método s forma que ele aceite uma [ `SqlMoney` ](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.aspx) parâmetro de entrada chamado `price` e escrever o código para executar e retornar os resultados da consulta:


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample6.cs)]

O `GetProductsWithPriceLessThan` definição de método s e o código é parecido com a definição e o código do `GetDiscontinuedProducts` método criado na etapa 3. As únicas diferenças são que o `GetProductsWithPriceLessThan` método aceita como parâmetro de entrada (`price`), o `SqlCommand` s consulta inclui um parâmetro (`@MaxPrice`), e um parâmetro é adicionado para o `SqlCommand` s `Parameters` coleção é e recebe o valor da `price` variável.

Depois de adicionar esse código, reimplante o projeto do SQL Server. Em seguida, volte para o SQL Server Management Studio e atualize a pasta de procedimentos armazenados. Você deve ver uma nova entrada, `GetProductsWithPriceLessThan`. Em uma janela de consulta, digite e execute o comando `exec GetProductsWithPriceLessThan 25`, que será a lista de todos os produtos de menor que US $25, como mostra a Figura 14.


[![Produtos em US $25 são exibidos](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image27.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image26.png)

**Figura 14**: Produtos em US $25 são exibidas ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image28.png))


## <a name="step-6-calling-the-managed-stored-procedure-from-the-data-access-layer"></a>Etapa 6: Chamar o procedimento armazenado gerenciado de camada de acesso a dados

Neste ponto, adicionamos a `GetDiscontinuedProducts` e `GetProductsWithPriceLessThan` gerenciados procedimentos armazenados para o `ManagedDatabaseConstructs` do projeto e registrou com o banco de dados Northwind do SQL Server. Podemos também invocado esses procedimentos armazenados gerenciados no SQL Server Management Studio (veja a Figura 13 e 14 s). Para que nossa ASP.NET aplicativo para usar esses gerenciados procedimentos armazenados, no entanto, é necessário adicioná-los para o acesso a dados e camadas de lógica de negócios na arquitetura. Nesta etapa, adicionaremos dois novos métodos para o `ProductsTableAdapter` no `NorthwindWithSprocs` tipada DataSet, que foi inicialmente criado na [criando novos procedimentos armazenados para o s TableAdapters do conjunto de dados tipado](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) tutorial. Etapa 7, adicionaremos métodos correspondentes para a BLL.

Abra o `NorthwindWithSprocs` conjunto de dados tipado no Visual Studio e comece adicionando um novo método para o `ProductsTableAdapter` denominado `GetDiscontinuedProducts`. Para adicionar um novo método a um TableAdapter, clique com botão direito no nome do s TableAdapter no Designer e escolha a opção Add Query no menu de contexto.

> [!NOTE]
> Desde que mudamos o banco de dados Northwind a `App_Data` pasta para a instância de banco de dados do SQL Server 2005 Express Edition, é imperativo que a cadeia de caracteres de conexão correspondentes no Web. config atualizado para refletir essa alteração. Na etapa 2 discutimos atualizando os `NORTHWNDConnectionString` valor em `Web.config`. Se você se esqueceu de fazer essa atualização, você verá a mensagem de erro Falha ao adicionar consulta. Não é possível localizar a conexão `NORTHWNDConnectionString` para o objeto `Web.config` em uma caixa de diálogo ao tentar adicionar um novo método ao TableAdapter. Para resolver esse erro, clique em Okey e, em seguida, vá para `Web.config` e atualize o `NORTHWNDConnectionString` valor conforme discutido na etapa 2. Em seguida, tente adicionar novamente o método ao TableAdapter. Desta vez, ele deve funcionar sem erros.


Adicionando um novo método inicia o Assistente de configuração de consulta do TableAdapter, o que poderíamos ter usado muitas vezes nos últimos tutoriais. A primeira etapa nos pede para especificar como o TableAdapter deve acessar o banco de dados: por meio de uma instrução de SQL ad hoc ou por meio de um procedimento armazenado de novo ou existente. Uma vez que estamos já ter criado e registrado o `GetDiscontinuedProducts` procedimento armazenado gerenciado com o banco de dados, escolha usar existente armazenado opção procedimento e clique em Avançar.


[![Escolha o uso de opção de procedimento armazenado de existente](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image30.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image29.png)

**Figura 15**: Escolha usar existente armazenado procedimento opção ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image31.png))


A próxima tela nos solicita o procedimento armazenado que invoca o método. Escolha o `GetDiscontinuedProducts` procedimento armazenado gerenciado na lista suspensa e clique em Avançar.


[![Selecione o GetDiscontinuedProducts gerenciada de procedimento armazenado](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image33.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image32.png)

**Figura 16**: Selecione o `GetDiscontinuedProducts` gerenciados Stored Procedure ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image34.png))


Somos solicitados, em seguida, para especificar se o procedimento armazenado retorna linhas, um único valor ou nada. Uma vez que `GetDiscontinuedProducts` retorna o conjunto de linhas de produto descontinuado, escolha a primeira opção (dados de tabela) e clique em Avançar.


[![Selecione a opção de dados de tabela](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image36.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image35.png)

**Figura 17**: Selecione a opção de dados tabulares ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image37.png))


A tela final do assistente permite especificar os padrões de acesso de dados usados e os nomes dos métodos resultantes. Deixe as caixas de seleção marcadas e o nome os métodos `FillByDiscontinued` e `GetDiscontinuedProducts`. Clique em Concluir para concluir o assistente.


[![Nome FillByDiscontinued os métodos e GetDiscontinuedProducts](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image39.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image38.png)

**Figura 18**: Nomeie os métodos `FillByDiscontinued` e `GetDiscontinuedProducts` ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image40.png))


Repita essas etapas para criar métodos chamados `FillByPriceLessThan` e `GetProductsWithPriceLessThan` na `ProductsTableAdapter` para o `GetProductsWithPriceLessThan` procedimento armazenado gerenciado.

Figura 19 mostra uma captura de tela do Designer de conjunto de dados depois de adicionar os métodos para o `ProductsTableAdapter` para o `GetDiscontinuedProducts` e `GetProductsWithPriceLessThan` gerenciados procedimentos armazenados.


[![O ProductsTableAdapter inclui os novos métodos adicionados nessa etapa](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image42.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image41.png)

**Figura 19**: O `ProductsTableAdapter` inclui novos métodos adicionados nesta etapa ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image43.png))


## <a name="step-7-adding-corresponding-methods-to-the-business-logic-layer"></a>Etapa 7: Adicionando métodos correspondentes para a camada de lógica de negócios

Agora que atualizamos a camada de acesso a dados para incluir métodos para chamar os procedimentos armazenados gerenciados adicionados nas etapas 4 e 5, precisamos adicionar métodos correspondentes para a camada de lógica de negócios. Adicione os dois métodos a seguir para o `ProductsBLLWithSprocs` classe:


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample7.cs)]

Ambos os métodos simplesmente chamar o método correspondente da DAL e retornar o `ProductsDataTable` instância. O `DataObjectMethodAttribute` marcação acima de cada método faz com que esses métodos a serem incluídos na lista suspensa na guia SELECT do assistente ObjectDataSource s configurar fonte de dados.

## <a name="step-8-invoking-the-managed-stored-procedures-from-the-presentation-layer"></a>Etapa 8: Chamar os procedimentos armazenados gerenciados da camada de apresentação

Com a lógica de negócios e as camadas de acesso de dados aumentada para incluir suporte para chamar o `GetDiscontinuedProducts` e `GetProductsWithPriceLessThan` gerenciados procedimentos armazenados, podemos agora exibir esses armazenados resultados de procedimentos por meio de uma página ASP.NET.

Abra o `ManagedFunctionsAndSprocs.aspx` página o `AdvancedDAL` pasta e, na caixa de ferramentas, arraste um controle GridView para o Designer. Definir o s GridView `ID` propriedade para `DiscontinuedProducts` e, na marca inteligente, de associá-lo a um novo ObjectDataSource chamado `DiscontinuedProductsDataSource`. Configurar o ObjectDataSource para efetuar pull de seus dados a partir de `ProductsBLLWithSprocs` classe s `GetDiscontinuedProducts` método.


[![Configurar o ObjectDataSource para usar a classe ProductsBLLWithSprocs](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image45.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image44.png)

**Figura 20**: Configurar o ObjectDataSource para usar o `ProductsBLLWithSprocs` classe ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image46.png))


[![Escolha o método GetDiscontinuedProducts na lista suspensa na guia SELECT](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image48.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image47.png)

**Figura 21**: Escolha o `GetDiscontinuedProducts` método na lista suspensa na guia Selecionar ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image49.png))


Porque essa grade será usado para exibir informações de produto apenas, defina as listas suspensas na atualização, inserção e excluir guias como (nenhum) e, em seguida, clique em Concluir.

Após a conclusão do assistente, o Visual Studio adicionará automaticamente um BoundField ou CheckBoxField para cada campo de dados no `ProductsDataTable`. Reserve um tempo para remover todos esses campos, exceto `ProductName` e `Discontinued`, em que ponto o GridView e marcação declarativa do ObjectDataSource s deve ser semelhante ao seguinte:


[!code-aspx[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample8.aspx)]

Reserve um tempo para exibir esta página por meio de um navegador. Quando a página é visitada, as chamadas do ObjectDataSource a `ProductsBLLWithSprocs` classe s `GetDiscontinuedProducts` método. Como vimos na etapa 7, esse método chama para baixo para o s DAL `ProductsDataTable` classe s `GetDiscontinuedProducts` método, que invoca o `GetDiscontinuedProducts` procedimento armazenado. Esse procedimento armazenado é um procedimento armazenado e executa o código que criamos na etapa 3, retornando os produtos descontinuados.

Os resultados retornados pelo procedimento armazenado gerenciado são empacotados em um `ProductsDataTable` pela DAL e, em seguida, é retornado para a BLL, que, em seguida, retorna-os para a camada de apresentação onde eles estão associados a GridView e exibidos. Conforme o esperado, a grade lista os produtos que foram descontinuados.


[![Os produtos descontinuados estão listados](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image51.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image50.png)

**Figura 22**: Os produtos descontinuados são listados ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image52.png))


Ainda mais prática, adicione uma caixa de texto e outro GridView à página. Ter esse GridView exibe os produtos de menor que o valor inserido na caixa de texto chamando o `ProductsBLLWithSprocs` classe s `GetProductsWithPriceLessThan` método.

## <a name="step-9-creating-and-calling-t-sql-udfs"></a>Etapa 9: Criando e chamando UDFs de T-SQL

Funções definidas pelo usuário ou UDFs, são o banco de dados objetos intimamente imitar a semântica das funções em linguagens de programação. Como uma função em c#, as UDFs podem incluir um número variável de parâmetros de entrada e retornam um valor de um tipo específico. Uma UDF pode retornar qualquer um dos dados escalares - uma cadeia de caracteres, um número inteiro e assim por diante – ou dados tabulares. Deixe o s dar uma olhada rápida em ambos os tipos de UDFs, começando com um UDF que retorna um tipo de dados escalares.

O UDF a seguir calcula o valor estimado do estoque de um produto específico. Ele faz isso levando-se em três parâmetros de entrada - a `UnitPrice`, `UnitsInStock`, e `Discontinued` os valores para um determinado produto - e retorna um valor do tipo `money`. Ele calcula o valor estimado do inventário multiplicando-se a `UnitPrice` pelo `UnitsInStock`. Para itens descontinuados, esse valor é reduzido à metade.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample9.sql)]

Depois que essa UDF foi adicionado ao banco de dados, ele pode ser encontrado por meio do Management Studio, expandindo a pasta de programação, em seguida, funções e, em seguida, funções com valor escalar. Ele pode ser usado em um `SELECT` consulta desta forma:


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample10.sql)]

Eu ter adicionado o `udf_ComputeInventoryValue` UDF no banco de dados Northwind; Figura 23 mostra a saída das opções acima `SELECT` consultar quando visualizado no Management Studio. Observe também que o UDF é listado sob a pasta de funções com valor escalar no Pesquisador de objetos.


[![Cada produto s valores de estoque está listado](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image54.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image53.png)

**Figura 23**: Cada produto s valores de estoque é listado ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image55.png))


UDFs também podem retornar dados tabulares. Por exemplo, podemos criar um UDF que retorna os produtos que pertencem a uma determinada categoria:


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample11.sql)]

O `udf_GetProductsByCategoryID` UDF aceita um `@CategoryID` parâmetro de entrada e retorna os resultados de especificado `SELECT` consulta. Depois de criado, essa UDF pode ser referenciada na `FROM` (ou `JOIN`) a cláusula de um `SELECT` consulta. O exemplo a seguir retornaria os `ProductID`, `ProductName`, e `CategoryID` valores para cada uma de bebidas.


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample12.sql)]

Eu ter adicionado o `udf_GetProductsByCategoryID` UDF no banco de dados Northwind; Figura 24 mostra a saída das opções acima `SELECT` consultar quando visualizado no Management Studio. UDFs que retornam dados tabulares podem ser encontrados na pasta de funções com valor de tabela s do Pesquisador de objetos.


[![O ProductID, ProductName e CategoryID são listadas para cada bebidas](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image57.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image56.png)

**Figura 24**: O `ProductID`, `ProductName`, e `CategoryID` são listadas para cada Bebidas ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image58.png))


> [!NOTE]
> Para obter mais informações sobre como criar e usar UDFs, fazer check-out [Introdução a funções definidas pelo usuário](http://www.sqlteam.com/item.asp?ItemID=1955). Também fazer check-out [vantagens e as funções de Drawbacks of User-Defined](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1).


## <a name="step-10-creating-a-managed-udf"></a>Etapa 10: Criação de uma UDF gerenciada

O `udf_ComputeInventoryValue` e `udf_GetProductsByCategoryID` UDFs criados nos exemplos acima são objetos de banco de dados do T-SQL. SQL Server 2005 também oferece suporte a UDFs gerenciados, que podem ser adicionados para o `ManagedDatabaseConstructs` projeto assim como o gerenciado procedimentos armazenados das etapas 3 e 5. Para esta etapa, deixe s implementar o `udf_ComputeInventoryValue` UDF em código gerenciado.

Para adicionar uma UDF gerenciada para o `ManagedDatabaseConstructs` do projeto, clique com botão direito no nome do projeto no Gerenciador de soluções e escolha Adicionar um novo Item. Selecione o modelo de definidas pelo usuário na caixa de diálogo Add New Item e nomeie o novo arquivo UDF `udf_ComputeInventoryValue_Managed.cs`.


[![Adicionar uma nova UDF gerenciada para o projeto ManagedDatabaseConstructs](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image60.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image59.png)

**Figura 25**: Adicionar uma nova UDF gerenciada para o `ManagedDatabaseConstructs` projeto ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image61.png))


O modelo de função definida pelo usuário cria uma `partial` classe denominada `UserDefinedFunctions` com um método cujo nome é igual ao nome de arquivo s de classe (`udf_ComputeInventoryValue_Managed`, nesta instância). Esse método é decorado usando o [ `SqlFunction` atributo](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlfunctionattribute.aspx), que sinaliza o método como uma UDF gerenciada.


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample13.cs)]

O `udf_ComputeInventoryValue` atualmente, o método retorna um [ `SqlString` objeto](https://msdn.microsoft.com/library/system.data.sqltypes.sqlstring.aspx) e não aceita parâmetros de entrada. É necessário atualizar a definição do método para que ela aceita três parâmetros – de entrada `UnitPrice`, `UnitsInStock`, e `Discontinued` - e retorna um `SqlMoney` objeto. A lógica para calcular o valor do estoque é idêntica no T-SQL `udf_ComputeInventoryValue` UDF.


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample14.cs)]

Observe que os parâmetros de entrada do método s UDF são de seus tipos SQL correspondentes: `SqlMoney` para o `UnitPrice` campo [ `SqlInt16` ](https://msdn.microsoft.com/library/system.data.sqltypes.sqlint16.aspx) para `UnitsInStock`, e [ `SqlBoolean` ](https://msdn.microsoft.com/library/system.data.sqltypes.sqlboolean.aspx) para `Discontinued`. Esses tipos de dados refletem os tipos definidos na `Products` tabela: a `UnitPrice` coluna é do tipo `money`, o `UnitsInStock` coluna do tipo `smallint`e o `Discontinued` coluna do tipo `bit`.

O código começa criando uma `SqlMoney` instância nomeada `inventoryValue` que é atribuído um valor de 0. O `Products` permite a tabela de banco de dados `NULL` os valores na `UnitsInPrice` e `UnitsInStock` colunas. Portanto, precisamos primeiro verificar para ver se esses valores contêm `NULL` s, o que podemos fazer por meio de `SqlMoney` objeto s [ `IsNull` propriedade](https://msdn.microsoft.com/library/system.data.sqltypes.sqlmoney.isnull.aspx). Se os dois `UnitPrice` e `UnitsInStock` contêm não -`NULL` valores, em seguida, calculamos o `inventoryValue` para ser o produto dos dois. Então, se `Discontinued` for true, em seguida, podemos dividir o valor.

> [!NOTE]
> O `SqlMoney` objeto só permite que dois `SqlMoney` instâncias ser multiplicados juntos. Ela não permite um `SqlMoney` instância seja multiplicado por um número de ponto flutuante literal. Portanto, para dividir `inventoryValue` , multiplique-o por um novo `SqlMoney` instância que tem o valor 0,5.


## <a name="step-11-deploying-the-managed-udf"></a>Etapa 11: Implantando o UDF gerenciada

Agora que o UDF gerenciada tiver sido criado, estamos prontos para implantá-lo no banco de dados Northwind. Como vimos na etapa 4, os objetos gerenciados em um projeto do SQL Server são implantados clicando duas vezes no nome do projeto no Gerenciador de soluções e escolhendo a opção implantar no menu de contexto.

Depois de implantar o projeto, retorne ao SQL Server Management Studio e atualize a pasta de funções com valor escalar. Agora você deve ver duas entradas:

- `dbo.udf_ComputeInventoryValue` -T-SQL UDF criado na etapa 9, e
- `dbo.udf ComputeInventoryValue_Managed` -o UDF gerenciada criada na etapa 10 que acabou de ser implantado.

Para testar essa UDF gerenciado, execute a seguinte consulta no Management Studio:


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample15.sql)]

Esse comando usa o gerenciado `udf ComputeInventoryValue_Managed` UDF em vez do T-SQL `udf_ComputeInventoryValue` UDF, mas a saída é o mesmo. Consulte a Figura 23 para ver uma captura de tela da saída s UDF.

## <a name="step-12-debugging-the-managed-database-objects"></a>Etapa 12: Os objetos de banco de dados gerenciado de depuração

No [depuração de procedimentos armazenados](debugging-stored-procedures-cs.md) tutorial discutimos as três opções para a depuração do SQL Server por meio do Visual Studio: Banco de dados direto de depuração, depuração do aplicativo e de depuração de um projeto do SQL Server. Banco de dados objetos não podem ser depurados por meio de depuração direta de banco de dados, mas podem ser depurados gerenciado de um aplicativo cliente e diretamente do projeto do SQL Server. Em ordem para a depuração funcionar, no entanto, o banco de dados do SQL Server 2005 deve permitir depuração SQL/CLR. Lembre-se de que quando criamos primeiro o `ManagedDatabaseConstructs` projeto Visual Studio nos perguntou se quiséssemos habilitar a depuração (veja a Figura 6 na etapa 2) do SQL/CLR. Essa configuração pode ser modificada clicando com o banco de dados da janela Gerenciador de servidores.


![Verifique se o banco de dados permite a depuração SQL/CLR](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image62.png)

**Figura 26**: Verifique se o banco de dados permite a depuração SQL/CLR


Imagine que gostaríamos de depurar o `GetProductsWithPriceLessThan` procedimento armazenado gerenciado. Começamos definindo um ponto de interrupção no código do `GetProductsWithPriceLessThan` método.


[![Defina um ponto de interrupção no método GetProductsWithPriceLessThan](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image64.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image63.png)

**Figura 27**: Defina um ponto de interrupção na `GetProductsWithPriceLessThan` método ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image65.png))


Deixe o s primeiro examinar os objetos de banco de dados gerenciado do SQL Server projeto de depuração. Uma vez que a nossa solução inclui dois projetos - a `ManagedDatabaseConstructs` projeto do SQL Server, juntamente com o nosso site - para depurar a partir do projeto do SQL Server, precisamos instruir o Visual Studio para iniciar o `ManagedDatabaseConstructs` quando iniciar a depuração de projeto do SQL Server. Clique com botão direito do `ManagedDatabaseConstructs` do projeto no Gerenciador de soluções e escolha o conjunto como opção de projeto de inicialização no menu de contexto.

Quando o `ManagedDatabaseConstructs` projeto é inicializado do depurador, ele executa as instruções SQL no `Test.sql` arquivo, que está localizado no `Test Scripts` pasta. Por exemplo, para testar o `GetProductsWithPriceLessThan` gerenciados de procedimento armazenado, substitua a `Test.sql` arquivo de conteúdo com a instrução a seguir, que invoca a `GetProductsWithPriceLessThan` passando de procedimento armazenado gerenciado a `@CategoryID` valor 14,95:


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample16.sql)]

Depois que você tiver inserido o script acima em `Test.sql`, iniciar a depuração no menu de depuração e selecionando Iniciar depuração ou pressionando F5 ou ícone de reproduzir o verde na barra de ferramentas. Isso irá compilar os projetos na solução, implantar os objetos de banco de dados gerenciados no banco de dados Northwind e, em seguida, execute o `Test.sql` script. Neste ponto, o ponto de interrupção será atingido e podemos usar step through a `GetProductsWithPriceLessThan` método, examine os valores dos parâmetros de entrada e assim por diante.


[![O ponto de interrupção no método GetProductsWithPriceLessThan foi atingido](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image67.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image66.png)

**Figura 28**: O ponto de interrupção a `GetProductsWithPriceLessThan` método foi atingida ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image68.png))


Para um objeto de banco de dados SQL a ser depurado por meio de um aplicativo cliente que, é imperativo que o banco de dados seja configurada para dar suporte à depuração do aplicativo. Clique com botão direito no banco de dados no Gerenciador de servidores e certifique-se de que a opção de depuração do aplicativo é verificada. Além disso, é necessário configurar o aplicativo ASP.NET para integrar com o depurador do SQL e para desabilitar o pooling de conexão. Essas etapas foram discutidas em detalhes na etapa 2 do [depuração de procedimentos armazenados](debugging-stored-procedures-cs.md) tutorial.

Quando você tiver configurado o aplicativo ASP.NET e o banco de dados, definir o site do ASP.NET como o projeto de inicialização e iniciar a depuração. Se você visitar uma página que chama um dos objetos gerenciados que tem um ponto de interrupção, o aplicativo será interrompida e o controle será ativado ao longo do depurador, onde você pode percorrer o código conforme mostrado na Figura 28.

## <a name="step-13-manually-compiling-and-deploying-managed-database-objects"></a>Etapa 13: Compilando e implantando gerenciados manualmente os objetos de banco de dados

Projetos do SQL Server tornam fácil criar, compilar e implantar objetos de banco de dados gerenciado. Infelizmente, os projetos do SQL Server só estão disponíveis nas edições Professional e sistemas de equipe do Visual Studio. Se você estiver usando o Visual Web Developer ou Standard Edition do Visual Studio e para usar objetos de banco de dados gerenciado, você precisará criar manualmente e implantá-los. Isso envolve quatro etapas:

1. Criar um arquivo que contém o código-fonte para o objeto de banco de dados gerenciado
2. Compilar o objeto em um assembly,
3. Registrar o assembly com o banco de dados do SQL Server 2005, e
4. Crie um objeto de banco de dados no SQL Server que aponta para o método apropriado no assembly.

Para ilustrar essas tarefas, permitir que o s crie um novo managed procedimento armazenado que retorna os produtos cujo `UnitPrice` é maior que um valor especificado. Crie um novo arquivo em seu computador chamado `GetProductsWithPriceGreaterThan.cs` e insira o código a seguir no arquivo (você pode usar o Visual Studio, o bloco de notas ou qualquer editor de texto para fazer isso):


[!code-csharp[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample17.cs)]

Esse código é quase idêntico do `GetProductsWithPriceLessThan` método criado na etapa 5. As únicas diferenças são os nomes de método, o `WHERE` cláusula e o nome do parâmetro usado na consulta. Volta a `GetProductsWithPriceLessThan` método, o `WHERE` cláusula ler: `WHERE UnitPrice < @MaxPrice`. Aqui, na `GetProductsWithPriceGreaterThan`, usamos: `WHERE UnitPrice > @MinPrice` .

Agora, precisamos compilar essa classe em um assembly. Na linha de comando, navegue até o diretório onde você salvou o `GetProductsWithPriceGreaterThan.cs` arquivo e usar o compilador c# (`csc.exe`) para compilar o arquivo de classe em um assembly:


[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample18.cmd)]

Se a pasta que contém `csc.exe` em não no sistema s `PATH`, você terá que referenciar totalmente seu caminho, `%WINDOWS%\Microsoft.NET\Framework\version\`, da seguinte forma:


[!code-console[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample19.cmd)]


[![Compilar GetProductsWithPriceGreaterThan.cs em um Assembly](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image70.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image69.png)

**Figura 29**: Compile `GetProductsWithPriceGreaterThan.cs` em um Assembly ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image71.png))


O `/t` sinalizador Especifica que o arquivo de classe do c# deve ser compilado em uma DLL (em vez de um executável). O `/out` sinalizador Especifica o nome do assembly resultante.

> [!NOTE]
> Em vez de compilar os `GetProductsWithPriceGreaterThan.cs` arquivo de classe da linha de comando, você também pode usar [Visual c# Express Edition](https://msdn.microsoft.com/vstudio/express/visualcsharp/) ou criar um projeto de biblioteca de classes separado no Visual Studio Standard Edition. S ren Jacob Lauritsen tiver fornecido gentilmente um projeto de Visual c# Express Edition com o código para o `GetProductsWithPriceGreaterThan` procedimento armazenado e os dois procedimentos armazenados de gerenciados e UDF criado nas etapas 3, 5 e 10. Projeto de s ren S também inclui os comandos T-SQL necessários para adicionar os objetos de banco de dados correspondente.


Com o código compilado em um assembly, estamos prontos para registrar o assembly no banco de dados do SQL Server 2005. Isso pode ser feito por meio do T-SQL, usando o comando `CREATE ASSEMBLY`, ou por meio do SQL Server Management Studio. Deixe o foco usando o Management Studio.

No Management Studio, expanda a pasta de programabilidade do banco de dados Northwind. Uma das subpastas é Assemblies. Para adicionar manualmente um novo Assembly no banco de dados, clique com botão direito na pasta Asssemblies e escolha o novo Assembly no menu de contexto. Este exibe a caixa de diálogo Novo Assembly caixa (veja a Figura 30). Clique no botão Procurar, selecione o `ManuallyCreatedDBObjects.dll` assembly estamos apenas é compilado e, em seguida, clique em Okey para adicionar o Assembly no banco de dados. Você não verá o `ManuallyCreatedDBObjects.dll` assembly no Pesquisador de objetos.


[![Adicione o Assembly de ManuallyCreatedDBObjects.dll no banco de dados](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image73.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image72.png)

**Figura 30**: Adicione a `ManuallyCreatedDBObjects.dll` Assembly no banco de dados ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image74.png))


![O ManuallyCreatedDBObjects.dll está listado no Pesquisador de objetos](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image75.png)

**Figura 31**: O `ManuallyCreatedDBObjects.dll` está listado no Pesquisador de objetos


Embora tenhamos adicionado o assembly no banco de dados Northwind, ainda temos que associar um procedimento armazenado com o `GetProductsWithPriceGreaterThan` método no assembly. Para fazer isso, abra uma nova janela de consulta e execute o script a seguir:


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample20.sql)]

Isso cria um novo procedimento armazenado no banco de dados Northwind denominado `GetProductsWithPriceGreaterThan` e a associa o método gerenciado `GetProductsWithPriceGreaterThan` (que é na classe `StoredProcedures`, que está no assembly `ManuallyCreatedDBObjects`).

Depois de executar o script acima, atualize a pasta de procedimentos armazenados no Pesquisador de objetos. Você deve ver uma nova entrada de procedimento armazenado - `GetProductsWithPriceGreaterThan` -que tem um ícone de cadeado ao lado dele. Para testar esse procedimento armazenado, digite e execute o seguinte script na janela de consulta:


[!code-sql[Main](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/samples/sample21.sql)]

Como mostra a Figura 32, o comando acima exibe informações de produtos com um `UnitPrice` maior que US $24.95.


[![O ManuallyCreatedDBObjects.dll está listado no Pesquisador de objetos](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image77.png)](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image76.png)

**Figura 32**: O `ManuallyCreatedDBObjects.dll` está listado no Pesquisador de objetos ([clique para exibir a imagem em tamanho normal](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs/_static/image78.png))


## <a name="summary"></a>Resumo

Microsoft SQL Server 2005 fornece integração com o tempo de execução do CLR (Common Language), que permite que os objetos de banco de dados a ser criado usando código gerenciado. Anteriormente, esses objetos de banco de dados só podiam ser criados usando o T-SQL, mas agora podemos criar esses objetos usando linguagens como c# de programação .NET. Neste tutorial, criamos dois gerenciado procedimentos armazenados e uma função definida pelo usuário gerenciada.

Visual Studio s tipo de projeto do SQL Server facilita a criação, compilação e implantação de objetos de banco de dados gerenciado. Além disso, ele oferece suporte avançado a depuração. No entanto, os tipos de projeto do SQL Server só estão disponíveis nas edições Professional e sistemas de equipe do Visual Studio. Para aqueles usar o Visual Web Developer ou Standard Edition do Visual Studio, a criação, compilação e as etapas de implantação deve ser executada manualmente, como vimos na etapa 13.

Boa programação!

## <a name="further-reading"></a>Leitura adicional

Para obter mais informações sobre os tópicos abordados neste tutorial, consulte os seguintes recursos:

- [Vantagens e desvantagens de funções definidas pelo usuário](http://www.samspublishing.com/articles/article.asp?p=31724&amp;rl=1)
- [Criando objetos do SQL Server 2005 em código gerenciado](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Criando gatilhos usando código gerenciado no SQL Server 2005](http://www.15seconds.com/issue/041006.htm)
- [Como: Criar e executar um SQL CLR procedimento armazenado de servidor](https://msdn.microsoft.com/library/5czye81z(VS.80).aspx)
- [Como: Criar e executar uma função definida pelo usuário do CLR SQL Server](https://msdn.microsoft.com/library/w2kae45k(VS.80).aspx)
- [Como: Editar o `Test.sql` Script para executar objetos SQL](https://msdn.microsoft.com/library/ms233682(VS.80).aspx)
- [Introdução ao usuário de funções definidas pelo](http://www.sqlteam.com/item.asp?ItemID=1955)
- [Código gerenciado e o SQL Server 2005 (vídeo)](https://channel9.msdn.com/Showpost.aspx?postid=142413)
- [Referência do Transact-SQL](https://msdn.microsoft.com/library/aa299742(SQL.80).aspx)
- [Passo a passo: Criar um procedimento armazenado no código gerenciado](https://msdn.microsoft.com/library/zxsa8hkf(VS.80).aspx)

## <a name="about-the-author"></a>Sobre o autor

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor de sete livros sobre ASP/ASP.NET e fundador da [4GuysFromRolla.com](http://www.4guysfromrolla.com), tem trabalhado com tecnologias Microsoft Web desde 1998. Scott funciona como um consultor independente, instrutor e escritor. Seu livro mais recente é [ *Sams Teach por conta própria ASP.NET 2.0 em 24 horas*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Ele pode ser contatado pelo [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) ou por meio de seu blog, que pode ser encontrado em [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Agradecimentos especiais a

Esta série de tutoriais foi revisada por muitos revisores úteis. Revisor de avanço para este tutorial foi S ren Jacob Lauritsen. Além de examinar este artigo, ren S também criou o projeto de Visual c# Express Edition incluído no download neste artigo s para compilar manualmente os objetos de banco de dados gerenciado. Você está interessado na revisão Meus próximos artigos do MSDN? Nesse caso, me descartar uma linha na [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Anterior](debugging-stored-procedures-cs.md)
> [Próximo](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
