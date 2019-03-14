---
ms.openlocfilehash: 873e399dc7bf6bf97c0925c1bdcf21f699f0be2e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057583"
---
# <a name="add-validation-to-an-aspnet-core-mvc-app"></a>Adicionar a validação a um aplicativo ASP.NET Core MVC

Por [Rick Anderson](https://twitter.com/RickAndMSFT)

Nesta seção, você adicionará a lógica de validação ao modelo `Movie` e garantirá que as regras de validação são impostas sempre que um usuário criar ou editar um filme.

## <a name="keeping-things-dry"></a>Mantendo o processo DRY

Um dos princípios de design do MVC é o [DRY](https://wikipedia.org/wiki/Don%27t_repeat_yourself) (“Don't Repeat Yourself”). O ASP.NET Core MVC incentiva você a especificar a funcionalidade ou o comportamento somente uma vez e, em seguida, refleti-lo em qualquer lugar de um aplicativo. Isso reduz a quantidade de código que você precisa escrever e faz com que o código escrito seja menos propenso a erros e mais fácil de testar e manter.

O suporte de validação fornecido pelo MVC e pelo Entity Framework Core Code First é um bom exemplo do princípio DRY em ação. Especifique as regras de validação de forma declarativa em um único lugar (na classe de modelo) e as regras são impostas em qualquer lugar no aplicativo.

## <a name="adding-validation-rules-to-the-movie-model"></a>Adicionando regras de validação ao modelo de filme

Abra o arquivo *Movie.cs*. DataAnnotations fornece um conjunto interno de atributos de validação que são aplicados de forma declarativa a qualquer classe ou propriedade. (Também contém atributos de formatação como `DataType`, que ajudam com a formatação e não fornecem nenhuma validação.)

Atualize a classe `Movie` para aproveitar os atributos de validação `Required`, `StringLength`, `RegularExpression` e `Range` internos.

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie21/Models/MovieDateRatingDA.cs?name=snippet1)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Models/MovieDateRatingDA.cs?name=snippet1)]

::: moniker-end

Os atributos de validação especificam o comportamento que você deseja impor nas propriedades de modelo às quais eles são aplicados. Os atributos `Required` e `MinimumLength` indicam que uma propriedade deve ter um valor; porém, nada impede que um usuário insira um espaço em branco para atender a essa validação. O atributo `RegularExpression` é usado para limitar quais caracteres podem ser inseridos. No código acima, `Genre` e `Rating` devem usar apenas letras (primeira letra maiúscula, espaço em branco, números e caracteres especiais não são permitidos). O atributo `Range` restringe um valor a um intervalo especificado. O atributo `StringLength` permite definir o tamanho máximo de uma propriedade de cadeia de caracteres e, opcionalmente, seu tamanho mínimo. Os tipos de valor (como `decimal`, `int`, `float`, `DateTime`) são inerentemente necessários e não precisam do atributo `[Required]`.

Ter as regras de validação automaticamente impostas pelo ASP.NET Core ajuda a tornar seu aplicativo mais robusto. Também garante que você não se esqueça de validar algo e inadvertidamente permita dados incorretos no banco de dados.

## <a name="validation-error-ui-in-mvc"></a>Interface do usuário do erro de validação no MVC

Execute o aplicativo e navegue para o controlador Movies.

Toque no link **Criar Novo** para adicionar um novo filme. Preencha o formulário com alguns valores inválidos. Assim que a validação do lado do cliente do jQuery detecta o erro, ela exibe uma mensagem de erro.

![Formulário da exibição de filmes com vários erros de validação do lado do cliente do jQuery](~/tutorials/first-mvc-app/validation/_static/val.png)

[!INCLUDE[](~/includes/currency.md)]

Observe como o formulário renderizou automaticamente uma mensagem de erro de validação apropriada em cada campo que contém um valor inválido. Os erros são impostos no lado do cliente (usando o JavaScript e o jQuery) e no lado do servidor (caso um usuário tenha o JavaScript desabilitado).

Uma vantagem significativa é que você não precisa alterar uma única linha de código na classe `MoviesController` ou na exibição *Create.cshtml* para habilitar essa interface do usuário de validação. O controlador e as exibições criados anteriormente neste tutorial selecionaram automaticamente as regras de validação especificadas com atributos de validação nas propriedades da classe de modelo `Movie`. Teste a validação usando o método de ação `Edit` e a mesma validação é aplicada.

Os dados de formulário não serão enviados para o servidor enquanto houver erros de validação do lado do cliente. Verifique isso colocando um ponto de interrupção no método `HTTP Post` usando a [ferramenta Fiddler](http://www.telerik.com/fiddler) ou as [ferramentas do Desenvolvedor F12](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).

## <a name="how-validation-works"></a>Como funciona a validação

Talvez você esteja se perguntando como a interface do usuário de validação foi gerada sem atualizações do código no controlador ou nas exibições. O código a seguir mostra os dois métodos `Create`.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Controllers/MoviesController.cs?name=snippetCreate)]

O primeiro método de ação (HTTP GET) `Create` exibe o formulário Criar inicial. A segunda versão (`[HttpPost]`) manipula a postagem de formulário. O segundo método `Create` (a versão `[HttpPost]`) chama `ModelState.IsValid` para verificar se o filme tem erros de validação. A chamada a esse método avalia os atributos de validação que foram aplicados ao objeto. Se o objeto tiver erros de validação, o método `Create` exibirá o formulário novamente. Se não houver erros, o método salvará o novo filme no banco de dados. Em nosso exemplo de filme, o formulário não é postado no servidor quando há erros de validação detectados no lado do cliente; o segundo método `Create` nunca é chamado quando há erros de validação do lado do cliente. Se você desabilitar o JavaScript no navegador, a validação do cliente será desabilitada e você poderá testar o método `Create` HTTP POST `ModelState.IsValid` detectando erros de validação.

Defina um ponto de interrupção no método `[HttpPost] Create` e verifique se o método nunca é chamado; a validação do lado do cliente não enviará os dados de formulário quando forem detectados erros de validação. Se você desabilitar o JavaScript no navegador e, em seguida, enviar o formulário com erros, o ponto de interrupção será atingido. Você ainda pode obter uma validação completa sem o JavaScript. 

A imagem a seguir mostra como desabilitar o JavaScript no navegador FireFox.

![Firefox: na guia Conteúdo de Opções, desmarque a caixa de seleção Habilitar JavaScript.](~/tutorials/first-mvc-app/validation/_static/ff.png)

A imagem a seguir mostra como desabilitar o JavaScript no navegador Chrome.

![Google Chrome: Na seção JavaScript das configurações de Conteúdo, selecione Não permitir que nenhum site execute JavaScript.](~/tutorials/first-mvc-app/validation/_static/chrome.png)

Depois de desabilitar o JavaScript, poste os dados inválidos e execute o depurador em etapas.

![Durante a depuração em uma postagem de dados inválidos, o IntelliSense em ModelState.IsValid mostra que o valor é falso.](~/tutorials/first-mvc-app/validation/_static/ms.png)

Veja abaixo uma parte do modelo de exibição *Create.cshtml* gerada por scaffolding anteriormente no tutorial. Ela é usada pelos métodos de ação mostrados acima para exibir o formulário inicial e exibi-lo novamente em caso de erro.

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Views/Movies/CreateRatingBrevity.cshtml)]

O [Auxiliar de Marcação de Entrada](xref:mvc/views/working-with-forms) usa os atributos de [DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) e produz os atributos HTML necessários para a Validação do jQuery no lado do cliente. O [Auxiliar de Marcação de Validação](xref:mvc/views/working-with-forms#the-validation-tag-helpers) exibe erros de validação. Consulte [Validação](xref:mvc/models/validation) para obter mais informações.

O que é realmente interessante nessa abordagem é que o controlador nem o modelo de exibição `Create` sabem nada sobre as regras de validação reais que estão sendo impostas ou as mensagens de erro específicas exibidas. As regras de validação e as cadeias de caracteres de erro são especificadas somente na classe `Movie`. Essas mesmas regras de validação são aplicadas automaticamente à exibição `Edit` e a outros modelos de exibição que podem ser criados e que editam o modelo.

Quando você precisar alterar a lógica de validação, faça isso exatamente em um lugar, adicionando atributos de validação ao modelo (neste exemplo, a classe `Movie`). Você não precisa se preocupar se diferentes partes do aplicativo estão inconsistentes com a forma como as regras são impostas – toda a lógica de validação será definida em um lugar e usada em todos os lugares. Isso mantém o código muito limpo e torna-o mais fácil de manter e desenvolver. Além disso, isso significa que você respeitará totalmente o princípio DRY.

## <a name="using-datatype-attributes"></a>Usando atributos DataType

Abra o arquivo *Movie.cs* e examine a classe `Movie`. O namespace `System.ComponentModel.DataAnnotations` fornece atributos de formatação, além do conjunto interno de atributos de validação. Já aplicamos um valor de enumeração `DataType` à data de lançamento e aos campos de preço. O código a seguir mostra as propriedades `ReleaseDate` e `Price` com o atributo `DataType` apropriado.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Models/MovieDateRatingDA.cs?highlight=2,6&name=snippet2)]

Os atributos `DataType` fornecem dicas apenas para que o mecanismo de exibição formate os dados (e fornece atributos como `<a>` para as URLs e `<a href="mailto:EmailAddress.com">` para o email). Use o atributo `RegularExpression` para validar o formato dos dados. O atributo `DataType` é usado para especificar um tipo de dados mais específico do que o tipo intrínseco de banco de dados; eles não são atributos de validação. Nesse caso, apenas desejamos acompanhar a data, não a hora. A Enumeração `DataType` fornece muitos tipos de dados, como Date, Time, PhoneNumber, Currency, EmailAddress e muito mais. O atributo `DataType` também pode permitir que o aplicativo forneça automaticamente recursos específicos a um tipo. Por exemplo, um link `mailto:` pode ser criado para `DataType.EmailAddress` e um seletor de data pode ser fornecido para `DataType.Date` em navegadores que dão suporte a HTML5. Os atributos `DataType` emitem atributos `data-` HTML 5 (ou "data dash") que são reconhecidos pelos navegadores HTML 5. Os atributos `DataType` **não** fornecem nenhuma validação.

`DataType.Date` não especifica o formato da data exibida. Por padrão, o campo de dados é exibido de acordo com os formatos padrão com base nas `CultureInfo` do servidor.

O atributo `DisplayFormat` é usado para especificar explicitamente o formato de data:

```csharp
[DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
public DateTime ReleaseDate { get; set; }
```

A configuração `ApplyFormatInEditMode` especifica que a formatação também deve ser aplicada quando o valor é exibido em uma caixa de texto para edição. (Talvez você não deseje isso em alguns campos – por exemplo, para valores de moeda, provavelmente, você não deseja exibir o símbolo de moeda na caixa de texto para edição.)

Você pode usar o atributo `DisplayFormat` por si só, mas geralmente é uma boa ideia usar o atributo `DataType`. O atributo `DataType` transmite a semântica dos dados, ao invés de apresentar como renderizá-lo em uma tela e oferece os seguintes benefícios que você não obtém com DisplayFormat:

* O navegador pode habilitar os recursos do HTML5 (por exemplo, mostrar um controle de calendário, o símbolo de moeda apropriado à localidade, links de email, etc.)

* Por padrão, o navegador renderizará os dados usando o formato correto de acordo com a localidade.

* O atributo `DataType` pode permitir que o MVC escolha o modelo de campo correto para renderizar os dados (o `DisplayFormat`, se usado por si só, usa o modelo de cadeia de caracteres).

> [!NOTE]
> A validação do jQuery não funciona com os atributos `Range` e `DateTime`. Por exemplo, o seguinte código sempre exibirá um erro de validação do lado do cliente, mesmo quando a data estiver no intervalo especificado:

```csharp
[Range(typeof(DateTime), "1/1/1966", "1/1/2020")]
   ```

Você precisará desabilitar a validação de data do jQuery para usar o atributo `Range` com `DateTime`. Geralmente, não é uma boa prática compilar datas rígidas nos modelos e, portanto, o uso do atributo `Range` e de `DateTime` não é recomendado.

O seguinte código mostra como combinar atributos em uma linha:

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie21/Models/MovieDateRatingDAmult.cs?name=snippet1)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Models/MovieDateRatingDAmult.cs?name=snippet1)]

::: moniker-end

Na próxima parte da série, examinaremos o aplicativo e faremos algumas melhorias nos métodos `Details` e `Delete` gerados automaticamente.

## <a name="additional-resources"></a>Recursos adicionais

* [Trabalhando com formulários](xref:mvc/views/working-with-forms)
* [Globalização e localização](xref:fundamentals/localization)
* [Introdução aos auxiliares de marcação](xref:mvc/views/tag-helpers/intro)
* [Auxiliares de marca de autor](xref:mvc/views/tag-helpers/authoring)
