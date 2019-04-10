---
uid: signalr/overview/security/hub-authorization
title: Autenticação e autorização para Hubs do SignalR | Microsoft Docs
author: bradygaster
description: Este tópico descreve como restringir quais usuários ou funções podem acessar os métodos de hub. Versões de software usados neste tópico ve .NET 4.5 SignalR do Visual Studio 2013...
ms.author: bradyg
ms.date: 01/05/2015
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 91703a9ea088ab8b2898945dbd80b671ee25be07
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59392489"
---
# <a name="authentication-and-authorization-for-signalr-hubs"></a>Autenticação e autorização para hubs do SignalR

by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Este tópico descreve como restringir quais usuários ou funções podem acessar os métodos de hub.
>
> ## <a name="software-versions-used-in-this-topic"></a>Versões de software usadas neste tópico
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - Versão 2 do SignalR
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Versões anteriores deste tópico
>
> Para obter informações sobre versões anteriores do SignalR, consulte [versões mais antigas do SignalR](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Perguntas e comentários
>
> Deixe comentários sobre como você gostou neste tutorial e o que poderíamos melhorar nos comentários na parte inferior da página. Se você tiver perguntas que não estão diretamente relacionadas para o tutorial, você pode postá-los para o [Fórum do ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](http://stackoverflow.com/).


## <a name="overview"></a>Visão geral

Esse tópico contém as seguintes seções:

- [Autorizar atributo](#authorizeattribute)
- [Exigir autenticação para todos os hubs](#requireauth)
- [Autorização personalizada](#custom)
- [Passar informações de autenticação para clientes](#passauth)
- [Opções de autenticação para clientes .NET](#authoptions)

    - [Cookie de autenticação de formulários](#cookie)
    - [Autenticação do Windows](#windows)
    - [Cabeçalho de Conexão](#header)
    - [Certificado](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a>Autorizar atributo

O SignalR fornece o [autorizar](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) atributo para especificar quais usuários ou funções têm acesso a um hub ou método. Esse atributo está localizado no `Microsoft.AspNet.SignalR` namespace. Aplicar o `Authorize` de atributo para um hub ou determinados métodos em um hub. Quando você aplica o `Authorize` atributo a uma classe hub, o requisito de autorização especificado é aplicado a todos os métodos no hub. Este tópico fornece exemplos de diferentes tipos de requisitos de autorização que você pode aplicar. Sem o `Authorize` de atributo, um conectado cliente pode acessar qualquer método público no hub.

Se você tiver definido uma função chamada "Admin" em seu aplicativo web, você pode especificar que somente os usuários nessa função podem acessar um hub com o código a seguir.

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

Ou, você pode especificar que um hub contém um método que está disponível para todos os usuários e um segundo método que está disponível somente para usuários autenticados, conforme mostrado abaixo.

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

Os exemplos a seguir abordam os cenários de autorização diferentes:

- `[Authorize]` – somente usuários autenticados
- `[Authorize(Roles = "Admin,Manager")]` – somente os usuários em funções especificadas autenticados
- `[Authorize(Users = "user1,user2")]` – somente usuários com os nomes de usuário especificado autenticados
- `[Authorize(RequireOutgoing=false)]` – somente usuários autenticados podem invocar o hub, mas o marshaling de chamadas do servidor para os clientes não são limitadas por autorização, como, quando apenas alguns usuários podem enviar uma mensagem, mas todos os outros podem receber a mensagem. A propriedade RequireOutgoing só pode ser aplicada para o hub inteiro, não em métodos de indivíduos dentro do hub de. Quando RequireOutgoing não for definido como false, somente os usuários que atendem ao requisito de autorização são chamados do servidor.

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a>Exigir autenticação para todos os hubs

Você pode exigir autenticação para todos os hubs e métodos de hub em seu aplicativo chamando o [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) método quando o aplicativo é iniciado. Você pode usar esse método quando você tem vários hubs e deseja impor um requisito de autenticação para todos eles. Com esse método, você não pode especificar os requisitos para a saída de autorização, usuário ou função. Você só pode especificar que o acesso aos métodos de hub é restrito a usuários autenticados. No entanto, você ainda poderá aplicar o atributo Authorize a hubs ou métodos para especificar os requisitos adicionais. Necessidade de que especificar um atributo é adicionada ao requisito de autenticação básico.

O exemplo a seguir mostra um arquivo de inicialização que restringe todos os métodos de hub para usuários autenticados.

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

Se você chamar o `RequireAuthentication()` método após o processamento de uma solicitação de SignalR, SignalR lançará um `InvalidOperationException` exceção. O SignalR gera esta exceção, porque você não pode adicionar um módulo ao HubPipeline depois que o pipeline foi invocado. O exemplo anterior mostra uma chamada a `RequireAuthentication` método no `Configuration` método que é executado uma vez antes de lidar com a primeira solicitação.

<a id="custom"></a>

## <a name="customized-authorization"></a>Autorização personalizada

Se você precisar personalizar como a autorização é determinada, você pode criar uma classe que deriva de `AuthorizeAttribute` e substitua o [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) método. Para cada solicitação, o SignalR invoca esse método para determinar se o usuário está autorizado a concluir a solicitação. No método substituído, você pode fornecer a lógica necessária para seu cenário de autorização. O exemplo a seguir mostra como implantar a autorização por meio de identidade baseada em declarações.

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a>Passar informações de autenticação para clientes

Talvez você precise usar informações de autenticação no código que é executado no cliente. Você passa as informações necessárias ao chamar os métodos no cliente. Por exemplo, um método de aplicativo de bate-papo poderia passar como um parâmetro de nome de usuário da pessoa que está postando uma mensagem, conforme mostrado abaixo.

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

Ou, você pode criar um objeto para representar as informações de autenticação e passa o objeto como um parâmetro, conforme mostrado abaixo.

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

Você nunca deve passar a id de conexão de um cliente a outros clientes, como um usuário mal-intencionado poderia usá-lo para simular uma solicitação do cliente.

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a>Opções de autenticação para clientes .NET

Quando você tem um cliente do .NET, como um aplicativo de console, que interage com um hub é limitado a usuários autenticados, você pode passar as credenciais de autenticação em um cookie, o cabeçalho de conexão ou um certificado. Os exemplos nesta seção mostram como usar os métodos diferentes para autenticar um usuário. Eles não são totalmente funcional aplicativos do SignalR. Para obter mais informações sobre os clientes do .NET com o SignalR, consulte [guia da API Hubs – cliente .NET](../guide-to-the-api/hubs-api-guide-net-client.md).

<a id="cookie"></a>

### <a name="cookie"></a>Cookie

Quando o cliente .NET interage com um hub que usa a autenticação de formulários do ASP.NET, você precisará definir manualmente o cookie de autenticação sobre a conexão. Você adiciona o cookie para o `CookieContainer` propriedade sobre a [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) objeto. O exemplo a seguir mostra um aplicativo de console que recupera um cookie de autenticação de uma página da web e adiciona esse cookie para a conexão.

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

O aplicativo de console envia as credenciais a serem <strong>www.contoso.com/RemoteLogin</strong> que pode se referir a uma página vazia que contém o seguinte arquivo de code-behind.

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a>Autenticação do Windows

Ao usar a autenticação do Windows, você pode passar credenciais do usuário atual usando o [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) propriedade. Você pode definir as credenciais para a conexão com o valor da DefaultCredentials.

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a>Cabeçalho de Conexão

Se seu aplicativo não estiver usando cookies, você pode passar informações de usuário no cabeçalho da conexão. Por exemplo, você pode passar um token no cabeçalho da conexão.

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

Em seguida, no hub, você poderia verificar o token do usuário.

<a id="certificate"></a>

### <a name="certificate"></a>Certificado

Você pode passar um certificado de cliente para verificar se o usuário. Você adiciona o certificado ao criar a conexão. O exemplo a seguir mostra apenas como adicionar um certificado de cliente para a conexão; ele não mostra o aplicativo de console completo. Ele usa o [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) classe que fornece várias maneiras diferentes para criar o certificado.

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]
