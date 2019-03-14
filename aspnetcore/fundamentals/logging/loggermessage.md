---
title: Registro em log de alto desempenho com o LoggerMessage no ASP.NET Core
author: guardrex
description: Saiba como usar o LoggerMessage para criar representantes que podem ser armazenados em cache e exigem menos alocações de objeto para cenários de registro em log de alto desempenho.
ms.author: riande
ms.date: 11/03/2017
uid: fundamentals/logging/loggermessage
ms.openlocfilehash: a0080a20fed2d8fc295e55822c11d5731c6910ca
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048613"
---
# <a name="high-performance-logging-with-loggermessage-in-aspnet-core"></a>Registro em log de alto desempenho com o LoggerMessage no ASP.NET Core

Por [Luke Latham](https://github.com/guardrex)

Os recursos do [LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage) criam delegados armazenáveis em cache que exigem menos alocações de objeto e sobrecarga de computação reduzida em comparação aos [métodos de extensão do agente](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions), como `LogInformation`, `LogDebug` e `LogError`. Para cenários de registro em log de alto desempenho, use o padrão `LoggerMessage`.

`LoggerMessage` fornece as seguintes vantagens de desempenho em relação aos métodos de extensão do Agente:

* Métodos de extensão do agente exigem tipos de valor de conversão boxing, como `int`, em `object`. O padrão `LoggerMessage` evita a conversão boxing usando campos `Action` estáticos e métodos de extensão com parâmetros fortemente tipados.
* Os métodos de extensão do agente precisam analisar o modelo de mensagem (cadeia de caracteres de formato nomeada) sempre que uma mensagem de log é gravada. `LoggerMessage` exige apenas a análise de um modelo uma vez quando a mensagem é definida.

[Exibir ou baixar código de exemplo](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/) ([como baixar](xref:index#how-to-download-a-sample))

O aplicativo de exemplo demonstra recursos do `LoggerMessage` com um sistema básico de acompanhamento de aspas. O aplicativo adiciona e exclui aspas usando um banco de dados em memória. Conforme ocorrem essas operações, são geradas mensagens de log usando o padrão `LoggerMessage`.

## <a name="loggermessagedefine"></a>LoggerMessage.Define

[Define(LogLevel, EventId, String)](/dotnet/api/microsoft.extensions.logging.loggermessage.define) cria um delegado `Action` para registrar uma mensagem em log. Sobrecargas de `Define` permitem passar até seis parâmetros de tipo para uma cadeia de caracteres de formato nomeada (modelo).

A cadeia de caracteres fornecida para o método `Define` é um modelo e não uma cadeia de caracteres interpolada. Os espaços reservados são preenchidos na ordem em que os tipos são especificados. Os nomes do espaço reservado no modelo devem ser descritivos e consistentes em todos os modelos. Eles servem como nomes de propriedade em dados de log estruturado. Recomendamos o uso da [formatação Pascal Case](/dotnet/standard/design-guidelines/capitalization-conventions) para nomes de espaço reservado. Por exemplo, `{Count}`, `{FirstName}`.

Cada mensagem de log é uma `Action` mantida em um campo estático criado por `LoggerMessage.Define`. Por exemplo, o aplicativo de exemplo cria um campo para descrever uma mensagem de log para uma solicitação GET para a página de Índice (*Internal/LoggerExtensions.cs*):

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet1)]

Para a `Action`, especifique:

* O nível de log.
* Um identificador de evento exclusivo ([EventId](/dotnet/api/microsoft.extensions.logging.eventid)) com o nome do método de extensão estático.
* O modelo de mensagem (cadeia de caracteres de formato nomeada). 

Uma solicitação para a página de Índice do aplicativo de exemplo define:

* O nível de log como `Information`.
* A ID do evento como `1` com o nome do método `IndexPageRequested`.
* Modelo de mensagem (cadeia de caracteres de formato nomeada) como uma cadeia de caracteres.

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet5)]

Repositórios de log estruturado podem usar o nome do evento quando recebem a ID do evento para enriquecer o log. Por exemplo, [Serilog](https://github.com/serilog/serilog-extensions-logging) usa o nome do evento.

A `Action` é invocada por meio de um método de extensão fortemente tipado. O método `IndexPageRequested` registra uma mensagem para uma solicitação GET da página de Índice no aplicativo de exemplo:

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet9)]

`IndexPageRequested` é chamado no agente no método `OnGetAsync` em *Pages/Index.cshtml.cs*:

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3)]

Inspecione a saída do console do aplicativo:

```console
info: LoggerMessageSample.Pages.IndexModel[1]
      => RequestId:0HL90M6E7PHK4:00000001 RequestPath:/ => /Index
      GET request for Index page
```

Para passar parâmetros para uma mensagem de log, defina até seis tipos ao criar o campo estático. O aplicativo de exemplo registra uma cadeia de caracteres em log ao adicionar aspas definindo um tipo `string` para o campo `Action`:

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet2)]

O modelo de mensagem de log do delegado recebe seus valores de espaço reservado dos tipos fornecidos. O aplicativo de exemplo define um delegado para adicionar aspas quando o parâmetro de aspas é uma `string`:

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet6)]

O método de extensão estático para adicionar aspas, `QuoteAdded`, recebe o valor do argumento de aspas e passa-o para o delegado `Action`:

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet10)]

No modelo da página de Índice (*Pages/Index.cshtml.cs*), `QuoteAdded` é chamado para registrar a mensagem em log:

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet3&highlight=6)]

Inspecione a saída do console do aplicativo:

```console
info: LoggerMessageSample.Pages.IndexModel[2]
      => RequestId:0HL90M6E7PHK5:0000000A RequestPath:/ => /Index
      Quote added (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand')
```

O aplicativo de exemplo implementa um padrão `try`&ndash;`catch` para a exclusão de aspas. Uma mensagem informativa é registrada em log para uma operação de exclusão bem-sucedida. Uma mensagem de erro é registrada em log para uma operação de exclusão quando uma exceção é gerada. A mensagem de log para a operação de exclusão sem êxito inclui o rastreamento de pilha da exceção (*Internal/LoggerExtensions.cs*):

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet3)]

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet7)]

Observe como a exceção é passada para o delegado em `QuoteDeleteFailed`:

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet11)]

No modelo da página de Índice, uma exclusão de aspas bem-sucedida chama o método `QuoteDeleted` no agente. Quando as aspas não são encontradas para exclusão, uma `ArgumentNullException` é gerada. A exceção é interceptada pela instrução `try`&ndash;`catch` e registrada em log com uma chamada ao método `QuoteDeleteFailed` no agente no bloco `catch` (*Pages/Index.cshtml.cs*):

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet5&highlight=14,18)]

Quando as aspas forem excluídas com êxito, inspecione a saída do console do aplicativo:

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:00000016 RequestPath:/ => /Index
      Quote deleted (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand' Id = 1)
```

Quando a exclusão de aspas falha, inspecione a saída do console do aplicativo. Observe que a exceção é incluída na mensagem de log:

```console
fail: LoggerMessageSample.Pages.IndexModel[5]
      => RequestId:0HL90M6E7PHK5:00000010 RequestPath:/ => /Index
      Quote delete failed (Id = 999)
System.ArgumentNullException: Value cannot be null.
Parameter name: entity
   at Microsoft.EntityFrameworkCore.Utilities.Check.NotNull[T](T value, String parameterName)
   at Microsoft.EntityFrameworkCore.DbContext.Remove[TEntity](TEntity entity)
   at Microsoft.EntityFrameworkCore.Internal.InternalDbSet`1.Remove(TEntity entity)
   at LoggerMessageSample.Pages.IndexModel.<OnPostDeleteQuoteAsync>d__14.MoveNext() in 
      <PATH>\sample\Pages\Index.cshtml.cs:line 87
```

## <a name="loggermessagedefinescope"></a>LoggerMessage.DefineScope

[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) cria um delegado `Func` para definir um [escopo de log](xref:fundamentals/logging/index#log-scopes). Sobrecargas de `DefineScope` permitem passar até três parâmetros de tipo para uma cadeia de caracteres de formato nomeada (modelo).

Como é o caso com o método `Define`, a cadeia de caracteres fornecida ao método `DefineScope` é um modelo e não uma cadeia de caracteres interpolada. Os espaços reservados são preenchidos na ordem em que os tipos são especificados. Os nomes do espaço reservado no modelo devem ser descritivos e consistentes em todos os modelos. Eles servem como nomes de propriedade em dados de log estruturado. Recomendamos o uso da [formatação Pascal Case](/dotnet/standard/design-guidelines/capitalization-conventions) para nomes de espaço reservado. Por exemplo, `{Count}`, `{FirstName}`.

Defina um [escopo de log](xref:fundamentals/logging/index#log-scopes) a ser aplicado a uma série de mensagens de log usando o método [DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope).

O aplicativo de exemplo tem um botão **Limpar Tudo** para excluir todas as aspas no banco de dados. As aspas são excluídas com a remoção das aspas individualmente, uma por vez. Sempre que aspas são excluídas, o método `QuoteDeleted` é chamado no agente. Um escopo de log é adicionado a essas mensagens de log.

Habilite `IncludeScopes` na seção de agente do console de *appSettings.json*:

[!code-csharp[](loggermessage/sample/appsettings.json?highlight=3-5)]

Para criar um escopo de log, adicione um campo para conter um delegado `Func` para o escopo. O aplicativo de exemplo cria um campo chamado `_allQuotesDeletedScope` (*Internal/LoggerExtensions.cs*):

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet4)]

Use `DefineScope` para criar o delegado. Até três tipos podem ser especificados para uso como argumentos de modelo quando o delegado é invocado. O aplicativo de exemplo usa um modelo de mensagem que inclui o número de aspas excluídas (um tipo `int`):

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet8)]

Forneça um método de extensão estático para a mensagem de log. Inclua os parâmetros de tipo para propriedades nomeadas exibidos no modelo de mensagem. O aplicativo de exemplo usa uma `count` de aspas a ser excluída e retorna `_allQuotesDeletedScope`:

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet12)]

O escopo encapsula as chamadas de extensão de log em um bloco `using`:

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet4&highlight=5-6,14)]

Inspecione as mensagens de log na saída do console do aplicativo. O seguinte resultado mostra três aspas excluídas com a mensagem de escopo de log incluída:

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 1' Id = 2)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 2' Id = 3)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 3' Id = 4)
```

## <a name="additional-resources"></a>Recursos adicionais

* [Registro em log](xref:fundamentals/logging/index)
