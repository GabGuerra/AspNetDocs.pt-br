---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: Suporte a BSON na API Web ASP.NET 2.1 - ASP.NET 4.x
author: MikeWasson
description: mostra como usar o BSON em um controlador de API da Web (lado do servidor) em um aplicativo cliente .NET para o ASP.NET 4. x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: 911e2abcfd277075b3cba71e624ec6390b99a15e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59382219"
---
# <a name="bson-support-in-aspnet-web-api-21"></a>Suporte a BSON na API Web ASP.NET 2.1

por [Mike Wasson](https://github.com/MikeWasson)

Este tópico mostra como usar o BSON em seu controlador de API da Web (lado do servidor) em um aplicativo cliente .NET. API Web 2.1 apresenta suporte para BSON. 

## <a name="what-is-bson"></a>O que é o BSON?

[BSON](http://bsonspec.org/) é um formato de serialização binária. "BSON" significa "Binary JSON", mas BSON e JSON são serializados de forma muito diferente. BSON é "Como JSON", porque os objetos são representados como pares nome-valor, semelhantes ao JSON. Ao contrário de JSON, os tipos de dados numéricos são armazenados como bytes, não cadeias de caracteres

BSON foi projetado para ser leve, fácil de examinar e rápido para codificação/decodificação.

- BSON é comparável em tamanho ao JSON. Dependendo dos dados, uma carga BSON pode ser menor ou maior que uma carga JSON. Para serializar os dados binários, como um arquivo de imagem BSON é menor do que o JSON, porque os dados binários não são codificada em base64.
- Documentos BSON são fáceis de examinar como os elementos são prefixados com um campo de comprimento, portanto, um analisador pode ignorar elementos sem decodificação-los.
- Codificação e decodificação são eficientes, como tipos de dados numéricos são armazenados como números, não cadeias de caracteres.

Clientes nativos, como aplicativos de cliente .NET, podem se beneficiar do uso BSON no lugar de formatos baseados em texto, como JSON ou XML. Para clientes de navegador, você provavelmente desejará fique com JSON, porque o JavaScript pode converter diretamente o conteúdo JSON.

Felizmente, a API Web usa [negociação de conteúdo](content-negotiation.md), portanto, sua API pode oferecer suporte a ambos os formatos e permitir que o cliente escolher.

## <a name="enabling-bson-on-the-server"></a>Habilitando o BSON no servidor

Em sua configuração de API da Web, adicione a **BsonMediaTypeFormatter** à coleção de formatadores.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

Agora, se o cliente solicita "application/bson", API da Web usará o formatador BSON.

Para associar o BSON com outros tipos de mídia, adicioná-los à coleção SupportedMediaTypes. O código a seguir adiciona "application/vnd.contoso" para os tipos de mídia com suporte:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a>Sessão HTTP de exemplo

Neste exemplo, vamos usar a seguinte classe de modelo mais de um controlador de API Web simples:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

Um cliente pode enviar a solicitação HTTP a seguir:

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

Aqui está a resposta:

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

Aqui posso substituir os dados binários com &quot;.&quot; caracteres. A seguinte captura de tela do mostra Fiddler os valores de hexadecimais brutos.

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a>Usando o BSON com HttpClient

Aplicativos de clientes .NET podem usar com o formatador de BSON **HttpClient**. Para obter mais informações sobre **HttpClient**, consulte [chamar um Web API de um cliente .NET](../advanced/calling-a-web-api-from-a-net-client.md).

O código a seguir envia uma solicitação GET que aceita BSON e, em seguida, desserializa o conteúdo BSON na resposta.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

Para solicitar o BSON do servidor, defina o cabeçalho Accept para "application/bson":

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

Para desserializar o corpo da resposta, use o **BsonMediaTypeFormatter**. Esse formatador não está na coleção de formatadores do padrão, portanto, você precisa especificá-lo quando você ler o corpo da resposta:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

O exemplo a seguir mostra como enviar uma solicitação POST que contém o BSON.

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

Grande parte desse código é o mesmo do exemplo anterior. Mas no **PostAsync** método, especifique **BsonMediaTypeFormatter** como o formatador:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a>Serialização de tipos primitivos de nível superior

Todos os documentos BSON é uma lista de pares chave/valor. A especificação de BSON não define uma sintaxe para serializar um único valor bruto, como um inteiro ou cadeia de caracteres.

Para contornar essa limitação, o **BsonMediaTypeFormatter** trata tipos primitivos como um caso especial. Antes de serializar, ele converte o valor em um par chave/valor com a chave "Value". Por exemplo, suponha que seu controlador de API retorna um inteiro:

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

Antes de serialização, o formatador BSON converte esse valor para o par chave/valor a seguir:

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

Quando você desserializa, o formatador converte os dados para o valor original. No entanto, os clientes que usam um analisador BSON diferente precisará lidar com isso, se sua API web retornar valores brutos. Em geral, você deve considerar retornando dados estruturados, em vez de valores brutos.

## <a name="additional-resources"></a>Recursos adicionais

[Exemplo de API BSON Web](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/)

[Formatadores de mídia](media-formatters.md)
