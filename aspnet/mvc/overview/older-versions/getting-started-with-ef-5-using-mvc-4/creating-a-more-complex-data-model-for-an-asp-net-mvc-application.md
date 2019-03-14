---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: Criando um modelo de dados mais complexo para um aplicativo ASP.NET MVC (4 de 10) | Microsoft Docs
author: tdykstra
description: Aplicativo web de exemplo Contoso University demonstra como criar aplicativos ASP.NET MVC 4 usando o Code First do Entity Framework 5 e o Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f81f3d80-3674-4d8e-a9b1-87feed1a93c9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: cfb01742c3921c24c71fd3fa4a14a9f71fac1ac1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063673"
---
<a name="creating-a-more-complex-data-model-for-an-aspnet-mvc-application-4-of-10"></a>Criando um modelo de dados mais complexo para um aplicativo ASP.NET MVC (4 de 10)
====================
por [Tom Dykstra](https://github.com/tdykstra)

[Baixe o projeto concluído](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Aplicativo web de exemplo Contoso University demonstra como criar aplicativos ASP.NET MVC 4 usando o Code First do Entity Framework 5 e o Visual Studio 2012. Para obter informações sobre a série de tutoriais, consulte [primeiro tutorial na série](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Você pode iniciar a série de tutoriais de início ou [baixar um projeto inicial para este capítulo](building-the-ef5-mvc4-chapter-downloads.md) e comece por aqui.
> 
> > [!NOTE] 
> > 
> > Se você enfrentar um problema que você não conseguir resolver, [baixar o capítulo concluído](building-the-ef5-mvc4-chapter-downloads.md) e tente reproduzir o problema. Em geral, você pode encontrar a solução ao problema comparando seu código com o código completo. Para alguns erros comuns e como resolvê-los, consulte [erros e soluções alternativas.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


Nos tutoriais anteriores trabalharam com um modelo de dados simples composto por três entidades. Neste tutorial você adicionará mais entidades e relações e personalizará o modelo de dados especificando formatação, validação e regras de mapeamento de banco de dados. Você verá duas maneiras de personalizar o modelo de dados: adicionando atributos a classes de entidade e adicionando código para a classe de contexto do banco de dados.

Quando terminar, as classes de entidade formarão o modelo de dados concluído mostrado na seguinte ilustração:

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

## <a name="customize-the-data-model-by-using-attributes"></a>Personalizar o modelo de dados usando atributos

Nesta seção, você verá como personalizar o modelo de dados usando atributos que especificam formatação, validação e regras de mapeamento de banco de dados. Em seguida, em várias das seções a seguir, você criará o completo `School` modelo de dados com a adição de atributos às classes você já criadas e criar novas classes para os demais tipos de entidade no modelo.

### <a name="the-datatype-attribute"></a>O atributo de tipo de dados

Para datas de registro de alunos, todas as páginas da Web atualmente exibem a hora junto com a data, embora tudo o que você deseje exibir nesse campo seja a data. Usando atributos de anotação de dados, você pode fazer uma alteração de código que corrigirá o formato de exibição em cada exibição que mostra os dados. Para ver um exemplo de como fazer isso, você adicionará um atributo à propriedade `EnrollmentDate` na classe `Student`.

Na *Models\Student.cs*, adicione uma `using` instrução para o `System.ComponentModel.DataAnnotations` namespace e adicione `DataType` e `DisplayFormat` atributos para o `EnrollmentDate` propriedade, conforme mostrado no exemplo a seguir:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,13-14)]

O [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) atributo é usado para especificar um tipo de dados que é mais específico do que o tipo intrínseco de banco de dados. Nesse caso, apenas desejamos acompanhar a data, não a data e a hora. O [enumeração DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) fornece muitos tipos de dados, tais como *data, hora, PhoneNumber, moeda, EmailAddress* e muito mais. O atributo `DataType` também pode permitir que o aplicativo forneça automaticamente recursos específicos a um tipo. Por exemplo, uma `mailto:` link pode ser criado para [DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx), e um seletor de data pode ser fornecido para [DataType.Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) em navegadores que oferecem suporte a [HTML5](http://html5.org/). O [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) atributos emite HTML 5 [dados -](http://ejohn.org/blog/html-5-data-attributes/) (pronuncia-se *dash dados*) atributos que navegadores HTML 5. O [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) atributos não fornecem nenhuma validação.

`DataType.Date` não especifica o formato da data exibida. Por padrão, o campo de dados é exibido de acordo com os formatos padrão com base no servidor do [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx).

O atributo `DisplayFormat` é usado para especificar explicitamente o formato de data:


[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]


O `ApplyFormatInEditMode` configuração especifica que a formatação especificado deve também ser aplicada quando o valor é exibido em uma caixa de texto para edição. (Talvez você não deseje isso em alguns campos – por exemplo, para valores de moeda, você talvez não deseja o símbolo de moeda na caixa de texto para edição.)

Você pode usar o [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) atributo por si só, mas geralmente é uma boa ideia usar o [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) atributo também. O `DataType` atributo transmite o *semântica* dos dados conforme em vez de como renderizá-lo em uma tela e oferece os seguintes benefícios que você não obtém com `DisplayFormat`:

- O navegador pode habilitar recursos do HTML5 (por exemplo mostrar um controle de calendário, o símbolo de moeda apropriado de localidade, links de email, etc.).
- Por padrão, o navegador renderizará os dados usando o formato correto com base em sua [localidade](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx).
- O [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) atributo pode permitir que o MVC escolha o modelo de campo correto para renderizar os dados (o [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) se usado por si só, usa o modelo de cadeia de caracteres). Para obter mais informações, consulte Brad Wilson [modelos do ASP.NET MVC 2](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html). (Embora escrito para MVC 2, neste artigo ainda se aplica à versão atual do ASP.NET MVC.)

Se você usar o `DataType` atributo com um campo de data, você deve especificar o `DisplayFormat` atributo também a fim de garantir que o campo seja renderizado corretamente em navegadores Chrome. Para obter mais informações, consulte [esse thread de StackOverflow](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie).

Execute novamente a página de índice de alunos e observe que vezes não são mais exibidas nas datas de registro. O mesmo será verdadeiro para qualquer exibição que usa o `Student` modelo.

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>O StringLengthAttribute

Você também pode especificar regras de validação de dados e mensagens usando atributos. Suponha que você deseje garantir que os usuários não insiram mais de 50 caracteres em um nome. Para adicionar essa limitação, adicione [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) atributos para o `LastName` e `FirstMidName` propriedades, conforme mostrado no exemplo a seguir:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

O [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) atributo não impedir que um usuário insira um nome em branco. Você pode usar o [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) atributo aplicar restrições à entrada. Por exemplo, o código a seguir exige o primeiro caractere a ser maiuscula e os caracteres restantes estejam em ordem alfabética:

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

O [MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) atributo fornece uma funcionalidade semelhante para o [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) de atributo, mas não fornece o lado do cliente validação.

Execute o aplicativo e clique no **alunos** guia. Você obterá o seguinte erro:

*O modelo fazendo o contexto de 'SchoolContext' foi alterado desde que o banco de dados foi criado. Considere o uso de migrações do Code First para atualizar o banco de dados ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*

O modelo de banco de dados foi alterado de forma que exige uma alteração no esquema de banco de dados, e o Entity Framework detectou que. Você usará as migrações para atualizar o esquema sem perder dados que você adicionou ao banco de dados usando a interface do usuário. Se você tiver alterado os dados que foi criados pelo `Seed` método, que será alterado para seu estado original devido a [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) método que você está usando no `Seed` método. ([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) é equivalente a uma operação "upsert" na terminologia de banco de dados.)

No PMC (Console do Gerenciador de Pacotes), Insira os seguintes comandos:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

O `add-migration MaxLengthOnNames` comando cria um arquivo chamado  *&lt;timeStamp&gt;\_MaxLengthOnNames.cs*. Esse arquivo contém o código que atualizará o banco de dados para corresponder ao modelo de dados atual. O carimbo de hora anexado ao nome do arquivo de migrações é usado pelo Entity Framework para ordenar as migrações. Depois que você criou várias migrações, se você remover o banco de dados, ou se você implantar o projeto usando as migrações, todas as migrações são aplicadas na ordem em que eles foram criados.

Execute o **criar** da página e insira um nome com mais de 50 caracteres. Assim que você exceder 50 caracteres, a validação do lado do cliente mostra uma mensagem de erro imediatamente.

![Erro de val do lado do cliente](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image3.png)

### <a name="the-column-attribute"></a>O atributo de coluna

Você também pode usar atributos para controlar como as classes e propriedades são mapeadas para o banco de dados. Suponha que você tenha usado o nome `FirstMidName` para o campo de nome porque o campo também pode conter um sobrenome. Mas você deseja que a coluna do banco de dados seja nomeada `FirstName`, pois os usuários que escreverão consultas ad hoc no banco de dados estão acostumados com esse nome. Para fazer esse mapeamento, use o atributo `Column`.

O atributo `Column` especifica que quando o banco de dados for criado, a coluna da tabela `Student` que é mapeada para a propriedade `FirstMidName` será nomeada `FirstName`. Em outras palavras, quando o código se referir a `Student.FirstMidName`, os dados serão obtidos ou atualizados na coluna `FirstName` da tabela `Student`. Se você não especificar nomes de coluna, eles recebem o mesmo nome que o nome da propriedade.

Adicionar uma instrução [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) e o atributo de nome de coluna para o `FirstMidName` propriedade, conforme mostrado no seguinte código realçado:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

A adição do [atributo de coluna](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) altera o modelo fazendo SchoolContext, portanto, ele não corresponde ao banco de dados. Digite os seguintes comandos no PMC para criar outra migração:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

Na **Gerenciador de servidores** (**Database Explorer** se você estiver usando o Express para Web), clique duas vezes o *aluno* tabela.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image4.png)

A imagem a seguir mostra o nome da coluna original como era antes de você aplicar as duas primeiras migrações. Além do nome da coluna, a alteração de `FirstMidName` à `FirstName`, as duas colunas de nome foram alterados de `MAX` comprimento a 50 caracteres.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

Você também pode fazer banco de dados de alterações de mapeamento usando o [API Fluent](https://msdn.microsoft.com/data/jj591617), como você verá posteriormente no tutorial.

> [!NOTE]
> Se você tentar compilar antes de concluir a criação de todas essas classes de entidade, você poderá receber erros de compilador.


## <a name="create-the-instructor-entity"></a>Criar a entidade Instructor

![Instructor_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image6.png)

Crie *Models\Instructor.cs*, substituindo o código de modelo pelo código a seguir:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

Observe que várias propriedades são iguais nas entidades `Student` e `Instructor`. No [Implementando a herança](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial mais adiante nesta série, você refatorará usando a herança para eliminar essa redundância.

### <a name="the-required-and-display-attributes"></a>O necessário e atributos de exibição

Os atributos no `LastName` propriedade especificar que ele é um campo obrigatório, que a legenda da caixa de texto deve ser "Sobrenome" (em vez do nome de propriedade, o que seria "LastName" sem espaço), e que o valor não pode ser mais de 50 caracteres.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

O [atributo StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) define o comprimento máximo do banco de dados e fornece do lado do cliente e do lado do servidor validação para o ASP.NET MVC. Você também pode especificar o tamanho mínimo da cadeia de caracteres nesse atributo, mas o valor mínimo não tem nenhum impacto sobre o esquema de banco de dados. O [atributo necessário](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) não é necessária para tipos de valor como DateTime, int, double e float. Tipos de valor não podem ser atribuídos um valor nulo, portanto, elas são inerentemente necessárias. Você pode remover o [atributo obrigatório](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) e substitua-o com um parâmetro de comprimento mínimo para o `StringLength` atributo:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs?highlight=2)]

Você pode colocar vários atributos em uma única linha, portanto, você também pode escrever a classe instructor da seguinte maneira:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-fullname-calculated-property"></a>O FullName calculada de propriedade

`FullName` é uma propriedade calculada que retorna um valor criado pela concatenação de duas outras propriedades. Portanto, ela tem apenas um `get` acessador e não `FullName` coluna será gerada no banco de dados.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>Os cursos e as propriedades de navegação OfficeAssignment

As propriedades `Courses` e `OfficeAssignment` são propriedades de navegação. Conforme explicado anteriormente, elas geralmente são definidas como [virtual](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) para que eles podem tirar proveito de um recurso do Entity Framework chamado [carregamento lento](https://msdn.microsoft.com/magazine/hh205756.aspx). Além disso, se uma propriedade de navegação pode armazenar várias entidades, seu tipo deve implementar o [ICollection&lt;T&gt; ](https://msdn.microsoft.com/library/92t2ye13.aspx) Interface. (Por exemplo [IList&lt;T&gt; ](https://msdn.microsoft.com/library/5y536ey6.aspx) qualifica, mas não [IEnumerable&lt;T&gt; ](https://msdn.microsoft.com/library/9eekhta0.aspx) porque `IEnumerable<T>` não implementa [adicionar ](https://msdn.microsoft.com/library/63ywd54z.aspx).

Um instrutor pode ministrar qualquer quantidade de cursos, portanto `Courses` é definido como uma coleção de `Course` entidades. Um instrutor só pode ter no máximo, um escritório; portanto, de estado de nossas regras comerciais `OfficeAssignment` é definido como uma única `OfficeAssignment` entity (que pode ser `null` se nenhum escritório for atribuído).

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-the-officeassignment-entity"></a>Criar a entidade OfficeAssignment

![OfficeAssignment_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image7.png)

Crie *Models\OfficeAssignment.cs* com o código a seguir:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

Compilar o projeto, que salva as alterações e verifica a que você ainda não fez qualquer cópia e cole erros que o compilador pode capturar.

### <a name="the-key-attribute"></a>O atributo de chave

Há uma relação um-para-zero-ou-um entre o `Instructor` e o `OfficeAssignment` entidades. Uma atribuição de escritório existe apenas em relação ao instrutor ao qual ele é atribuído a, e, portanto, sua chave primária também é a chave estrangeira a `Instructor` entidade. Mas o Entity Framework não pode reconhecer automaticamente `InstructorID` como o primário chave dessa entidade porque o nome não segue o `ID` ou *classname* `ID` convenção de nomenclatura. Portanto, o atributo `Key` é usado para identificá-la como a chave:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

Você também pode usar o `Key` se a entidade tem sua própria chave primária, mas você deseja algo diferente de um nome de propriedade de atributo `classnameID` ou `ID`. Por padrão o EF trata a chave como não gerada ao banco de dados porque a coluna é para uma relação de identificação.

### <a name="the-foreignkey-attribute"></a>O atributo ForeignKey

Quando há uma relação um-para-zero-ou-um ou um relacionamento individual entre duas entidades (tais como entre `OfficeAssignment` e `Instructor`), o EF não é possível descobrir qual ponta da relação é a entidade de segurança e quais final é dependente. Relações um para um tem uma propriedade de navegação de referência em cada classe para a outra classe. O [ForeignKey atributo](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) pode ser aplicado à classe dependente para estabelecer a relação. Se você omitir a [ForeignKey atributo](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx), você obterá o seguinte erro ao tentar criar a migração:

Não é possível determinar o final principal de uma associação entre os tipos 'ContosoUniversity.Models.OfficeAssignment' e 'ContosoUniversity.Models.Instructor'. O final principal dessa associação deve ser configurado explicitamente usando a API fluente de relacionamento ou anotações de dados.

Posteriormente no tutorial, mostraremos como configurar essa relação com a API fluente.

### <a name="the-instructor-navigation-property"></a>A propriedade de navegação Instructor

O `Instructor` entidade tem um valor anulável `OfficeAssignment` propriedade de navegação (porque um instrutor pode não ter uma atribuição de escritório) e o `OfficeAssignment` entidade tem um não-anulável `Instructor` propriedade de navegação (porque não é uma atribuição de escritório existir sem um instrutor – `InstructorID` é não anulável). Quando um `Instructor` entidade tem um relacionados `OfficeAssignment` entidade, cada entidade terá uma referência à outra em sua propriedade de navegação.

Você pode colocar um `[Required]` atributo na propriedade de navegação Instructor para especificar que deve haver um instrutor relacionado, mas você não precisa fazer isso porque a chave estrangeira de InstructorID (que também é a chave para esta tabela) é não anulável.

## <a name="modify-the-course-entity"></a>Modificar a entidade Course

![Course_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image8.png)

Na *Models\Course.cs*, substitua o código que você adicionou anteriormente pelo código a seguir:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

A entidade de curso tem uma propriedade de chave estrangeira `DepartmentID` que aponta para o relacionado `Department` entidade e ele tem um `Department` propriedade de navegação. O Entity Framework não exige que você adicione uma propriedade de chave estrangeira ao modelo de dados quando você tem uma propriedade de navegação para uma entidade relacionada. O EF cria automaticamente as chaves estrangeiras no banco de dados onde for necessário. No entanto, ter a chave estrangeira no modelo de dados pode tornar as atualizações mais simples e mais eficientes. Por exemplo, quando você busca uma entidade de curso para editar, o `Department` entidade é nula se você não carregá-lo, portanto, quando você atualiza a entidade de curso, você precisaria primeiro buscar a `Department` entidade. Quando a propriedade de chave estrangeira `DepartmentID` está incluído no modelo de dados, você não precisa buscar o `Department` entidade antes de atualizar.

### <a name="the-databasegenerated-attribute"></a>O atributo DatabaseGenerated

O [atributo DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) com o [None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) parâmetro no `CourseID` propriedade especifica que os valores de chave primários são fornecidos pelo usuário em vez de gerado pelo banco de dados.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

Por padrão, o Entity Framework pressupõe que os valores de chave primária são gerados pelo banco de dados. É isso que você quer na maioria dos cenários. No entanto, para `Course` entidades, você usa um número de curso especificado pelo usuário como uma série 1000 de um departamento, uma série 2000 para outro departamento e assim por diante.

### <a name="foreign-key-and-navigation-properties"></a>Chave estrangeira e propriedades de navegação

As propriedades de chave estrangeira e propriedades de navegação no `Course` entidade refletem as seguintes relações:

- Um curso é atribuído a um departamento e, portanto, há uma propriedade de chave estrangeira `DepartmentID` e de navegação `Department` pelas razões mencionadas acima. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- Um curso pode ter qualquer quantidade de estudantes inscritos; portanto, a propriedade de navegação `Enrollments` é uma coleção: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- Um curso pode ser ministrado por vários instrutores; portanto, a propriedade de navegação `Instructors` é uma coleção: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="creating-the-department-entity"></a>Criar a entidade de departamento

![Department_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image9.png)

Crie *Models\Department.cs* com o código a seguir:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>O atributo de coluna

Anteriormente, você usou o [atributo de coluna](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) para alterar o mapeamento de nome de coluna. No código para o `Department` entidade, o `Column` atributo está sendo usado para alterar a SQL tipo mapeamento de dados para que a coluna será definida usando o SQL Server [money](https://msdn.microsoft.com/library/ms179882.aspx) tipo no banco de dados:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

Mapeamento de coluna geralmente não é necessário, pois o Entity Framework geralmente escolhe o tipo de dados do SQL Server apropriado com base no tipo CLR que você define para a propriedade. O tipo `decimal` CLR é mapeado para um tipo `decimal` SQL Server. Mas nesse caso, você sabe que a coluna armazenará os valores de moeda e o [dinheiro](https://msdn.microsoft.com/library/ms179882.aspx) tipo de dados é mais apropriado para isso.

### <a name="foreign-key-and-navigation-properties"></a>Chave estrangeira e propriedades de navegação

As propriedades de navegação e de chave estrangeira refletem as seguintes relações:

- Um departamento pode ou não ter um administrador, e um administrador é sempre um instrutor. Portanto, o `InstructorID` propriedade é incluída como a chave estrangeira para a `Instructor` entidade e um ponto de interrogação é adicionado após o `int` designação para marcar a propriedade como nulo de tipo. A propriedade de navegação é chamada `Administrator` , mas contém uma `Instructor` entidade: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- Um departamento pode ter vários cursos e, portanto, não há um `Courses` propriedade de navegação: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > Por convenção, o Entity Framework habilita a exclusão em cascata para chaves estrangeiras que não permitem valor nulo e em relações muitos para muitos. Isso pode resultar em regras de exclusão em cascata circular, o que causarão uma exceção quando seu código inicializador é executado. Por exemplo, se você não definiu o `Department.InstructorID` propriedade como anuláveis, você teria a seguinte mensagem de exceção quando o inicializador é executado: "A relação referencial resultará em uma referência cíclica não permitida." Se as regras de negócio necessário `InstructorID` propriedade como não anuláveis, você precisaria usar a seguinte API fluente para desabilitar a exclusão em cascata na relação: 

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]


## <a name="modifying-the-student-entity"></a>Modificando a entidade Student

![Student_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image10.png)

Na *Models\Student.cs*, substitua o código que você adicionou anteriormente pelo código a seguir. As alterações são realçadas.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=12,15,24-27)]

## <a name="the-enrollment-entity"></a>A entidade Enrollment

 Na *Models\Enrollment.cs*, substitua o código que você adicionou anteriormente pelo código a seguir

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs?highlight=16)]

### <a name="foreign-key-and-navigation-properties"></a>Chave estrangeira e propriedades de navegação

As propriedades de navegação e de chave estrangeira refletem as seguintes relações:

- Um registro destina-se a um único curso e, portanto, há uma propriedade de chave estrangeira `CourseID` e uma propriedade de navegação `Course`: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]
- Um registro destina-se a um único aluno e, portanto, há uma propriedade de chave estrangeira `StudentID` e uma propriedade de navegação `Student`: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

### <a name="many-to-many-relationships"></a>Relações muitos para muitos

Há uma relação muitos-para-muitos entre a `Student` e `Course` entidades e o `Enrollment` entidade funciona como uma tabela de junção de muitos-para-muitos *com carga* no banco de dados. Isso significa que o `Enrollment` tabela contém dados adicionais além das chaves estrangeiras de tabelas unidas (nesse caso, uma chave primária e uma `Grade` propriedade).

A ilustração a seguir mostra a aparência dessas relações em um diagrama de entidades. (Esse diagrama foi gerado usando o [Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d); a criação do diagrama não faz parte do tutorial, está apenas sendo usada aqui como uma ilustração.)

![Course_many aluno de many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image11.png)

Cada linha da relação tem um 1 em uma extremidade e um asterisco (\*) na outra, indicando uma relação um-para-muitos.

Se o `Enrollment` tabela não inclui informações de nota, ela apenas precisará conter as duas chaves estrangeiras `CourseID` e `StudentID`. Nesse caso, ele corresponderia a uma tabela de junção de muitos-para-muitos *sem conteúdo* (ou um *tabela de junção pura*) no banco de dados, e você não precisará criar uma classe de modelo para ele. O `Instructor` e `Course` entidades têm esse tipo de relação muitos-para-muitos, e como você pode ver, não há nenhuma classe de entidade entre eles:

![Instrutor Course_many para many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

Uma tabela de junção é necessária no banco de dados, no entanto, conforme mostrado no diagrama de banco de dados a seguir:

![Instrutor Course_many para many_relationship_tables](https://asp.net/media/2577802/Windows-Live-Writer_Creating-a.NET-MVC-Application-4-of-10h1_B662_Instructor-Course_many-to-many_relationship_tables_03e042cf-db89-4b4c-985a-e458351ada76.png)

O Entity Framework cria automaticamente o `CourseInstructor` tabela e ler e atualizá-lo indiretamente por ler e atualizar o `Instructor.Courses` e `Course.Instructors` propriedades de navegação.

## <a name="entity-diagram-showing-relationships"></a>Diagrama de entidade mostrando relações

A ilustração a seguir mostra o diagrama criado pelo Entity Framework Power Tools para o modelo Escola concluído.

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

Além das linhas de relação muitos-para-muitos (\* à \*) e as linhas de relação um-para-muitos (1 para \*), você pode ver aqui a linha de relação um-para-zero-ou-um (1 para 0 a 1) entre a `Instructor` e `OfficeAssignment` entidades e a linha de relação zero-ou-um-para-muitos (entre 0 e 1 para \*) entre as entidades Instructor e Department.

## <a name="customize-the-data-model-by-adding-code-to-the-database-context"></a>Personalizar o modelo de dados, adicionando código para o contexto de banco de dados

Em seguida, você adicionará novas entidades para o `SchoolContext` de classe e personalizar algumas usando o mapeamento [API fluente](https://msdn.microsoft.com/data/jj591617) chamadas. (A API é "fluente" porque ela geralmente é usada pelo encadeamento de uma série de chamadas de método juntas em uma única instrução).

Neste tutorial, você usará a API fluente somente para o mapeamento de banco de dados que você não pode fazer com atributos. No entanto, você também pode usar a API fluente para especificar a maioria das regras de formatação, validação e mapeamento que pode ser feita por meio de atributos. Alguns atributos como `MinimumLength` não podem ser aplicados com a API fluente. Conforme mencionado anteriormente, `MinimumLength` não altera o esquema, ele só se aplica a uma regra de validação do lado cliente e servidor

Alguns desenvolvedores preferem usar a API fluente exclusivamente para que possam manter suas classes de entidade "limpas". Combine atributos e a API fluente se desejar. Além disso, há algumas personalizações que podem ser feitas apenas com a API fluente, mas em geral, a prática recomendada é escolher uma dessas duas abordagens e usar isso com o máximo de consistência possível.

Para adicionar novas entidades para os dados de modelo e realizar o mapeamento de banco de dados que você não precisava por meio de atributos, substitua o código em *DAL\SchoolContext.cs* com o código a seguir:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

A nova instrução na [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) método configura a tabela de junção de muitos-para-muitos:

- Para a relação muitos-para-muitos entre a `Instructor` e `Course` entidades, o código especifica os nomes de tabela e coluna para a tabela de junção. Código pela primeira vez pode configurar a relação muitos-para-muitos para você sem esse código, mas se você não chamá-lo, você obterá nomes padrão, como `InstructorInstructorID` para o `InstructorID` coluna.

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

O código a seguir fornece um exemplo de como você poderia ter usado a API fluente em vez de atributos para especificar a relação entre o `Instructor` e `OfficeAssignment` entidades:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

Para obter informações sobre o que as instruções de "API fluente" estão fazendo nos bastidores, consulte o [API Fluent](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) postagem de blog.

## <a name="seed-the-database-with-test-data"></a>Propagar o banco de dados com os dados de teste

Substitua o código na *Migrations\Configuration.cs* arquivo pelo código a seguir para fornecer dados de semente para as novas entidades que você criou.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

Como você viu no primeiro tutorial, a maioria desse código simplesmente atualiza ou cria novos objetos de entidade e carrega dados de exemplo em propriedades, conforme necessário, para teste. No entanto, observe como o `Course` entidade, que tem uma relação muitos-para-muitos com a `Instructor` entidade, é tratada:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

Quando você cria um `Course` do objeto, você inicializa o `Instructors` propriedade de navegação como uma coleção vazia usando o código `Instructors = new List<Instructor>()`. Isso torna possível adicionar `Instructor` entidades que estão relacionadas a este `Course` usando o `Instructors.Add` método. Se você não criou uma lista vazia, você não será capaz de adicionar essas relações, porque o `Instructors` propriedade seria nula e não teriam um `Add` método. Você também pode adicionar a inicialização de lista para o construtor.

## <a name="add-a-migration-and-update-the-database"></a>Adicionar uma migração e atualizar o banco de dados

No PMC, insira o `add-migration` comando:

`PM> add-Migration Chap4`

Se você tentar atualizar o banco de dados neste momento, você obterá o seguinte erro:

*A instrução ALTER TABLE entrou em conflito com a restrição FOREIGN KEY "FK\_dbo. Curso\_dbo. Departamento\_DepartmentID ". O conflito ocorreu no banco de dados "ContosoUniversity" tabela "dbo. Departamento", coluna 'DepartmentID'.*

Editar o &lt; *timestamp&gt;\_Chap4.cs* de arquivo e faça as alterações de código a seguir (você adicionará uma instrução SQL e modificar um `AddColumn` instrução):

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

(Certifique-se de que você comente ou exclua o existente `AddColumn` de linha quando você adiciona um novo, ou você obterá um erro quando você insere o `update-database` comando.)

Às vezes, quando você executa migrações com os dados existentes, você precisa inserir dados de stub no banco de dados para atender às restrições de chave estrangeira e que é o que você está fazendo agora. O código gerado adiciona um não-anulável `DepartmentID` chave estrangeira para a `Course` tabela. Se já houver linhas na `Course` tabela quando o código é executado, o `AddColumn` operação falharia, pois o SQL Server não saberá qual valor deve ser colocado na coluna que não pode ser nula. Portanto, você alterou o código para fornecer a nova coluna de um valor padrão e que você criou um departamento de stub chamado "Temp" para atuar como o departamento padrão. Como resultado, se houver existentes `Course` linhas quando esse código é executado, eles serão todas relacionados ao departamento "Temp".

Quando o `Seed` execução do método, ele irá inserir linhas na `Department` tabela e ela se relacionarão existente `Course` linhas para essas novas `Department` linhas. Se você ainda não adicionou nenhum curso na interface do usuário, você teria, em seguida, não precisa mais do departamento "Temp" ou o valor padrão no `Course.DepartmentID` coluna. Para permitir a possibilidade de que alguém pode ter adicionado cursos, usando o aplicativo, também convém atualizar o `Seed` código do método para garantir que todos os `Course` linhas (não apenas aqueles inseridos por execuções anteriores do `Seed` método) têm válido `DepartmentID` valores antes de remover o padrão de valor da coluna e exclua o departamento "Temp".

Depois de concluir a edição do &lt; *timestamp&gt;\_Chap4.cs* arquivo, insira o `update-database` comando no PMC para executar a migração.

> [!NOTE]
> É possível receber outros erros durante a migração de dados e fazer alterações de esquema. Se você receber erros de migração, você não conseguir resolver, você pode alterar a cadeia de conexão na *Web. config* de arquivo ou excluir o banco de dados. A abordagem mais simples é renomear o banco de dados *Web. config* arquivo. Por exemplo, altere o nome de banco de dados para o CU\_testar, conforme mostrado no exemplo a seguir:
> 
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.xml?highlight=1-2)]
> 
>  Com um novo banco de dados, não há nenhum dado para migrar e o `update-database` comando é muito mais provável de ser concluído sem erros. Para obter instruções sobre como excluir o banco de dados, consulte [como descartar um banco de dados do Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).


Abra o banco de dados **Gerenciador de servidores** como você fez anteriormente e expanda o **tabelas** nó para ver se todas as tabelas foram criadas. (Se você ainda tiver **Gerenciador de servidores** aberto do momento anterior, clique o **atualizar** botão.)

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

Você não criou uma classe de modelo para o `CourseInstructor` tabela. Conforme explicado anteriormente, essa é uma tabela de junção para a relação muitos-para-muitos entre a `Instructor` e `Course` entidades.

Clique com botão direito a `CourseInstructor` de tabela e selecione **Mostrar dados da tabela** para verificar se ele tem dados nele como resultado da `Instructor` entidades adicionadas para o `Course.Instructors` propriedade de navegação.

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="summary"></a>Resumo

Agora você tem um modelo de dados mais complexo e um banco de dados correspondente. O tutorial a seguir você aprenderá mais sobre as diferentes maneiras de acessar dados relacionados.

Links para outros recursos do Entity Framework podem ser encontradas na [mapa de conteúdo de acesso do ASP.NET dados](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Anterior](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [Próximo](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
