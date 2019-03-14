---
title: Formato de armazenamento de chaves no ASP.NET Core
author: rick-anderson
description: Conheça os detalhes de implementação do formato de armazenamento de chaves de proteção de dados do ASP.NET Core.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-storage-format
ms.openlocfilehash: bca19ad001dd20b5d02ae5470f7d928082496037
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044813"
---
# <a name="key-storage-format-in-aspnet-core"></a><span data-ttu-id="6031f-103">Formato de armazenamento de chaves no ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="6031f-103">Key storage format in ASP.NET Core</span></span>

<a name="data-protection-implementation-key-storage-format"></a>

<span data-ttu-id="6031f-104">Objetos são armazenados em repouso na representação XML.</span><span class="sxs-lookup"><span data-stu-id="6031f-104">Objects are stored at rest in XML representation.</span></span> <span data-ttu-id="6031f-105">O diretório padrão para o armazenamento de chaves é % LOCALAPPDATA%\ASP.NET\DataProtection-Keys\.</span><span class="sxs-lookup"><span data-stu-id="6031f-105">The default directory for key storage is %LOCALAPPDATA%\ASP.NET\DataProtection-Keys\.</span></span>

## <a name="the-key-element"></a><span data-ttu-id="6031f-106">O \<key > elemento</span><span class="sxs-lookup"><span data-stu-id="6031f-106">The \<key> element</span></span>

<span data-ttu-id="6031f-107">Chaves existem como objetos de nível superior no repositório de chave.</span><span class="sxs-lookup"><span data-stu-id="6031f-107">Keys exist as top-level objects in the key repository.</span></span> <span data-ttu-id="6031f-108">Por convenção, as chaves têm o nome do arquivo **chave-{guid}. XML**, onde {guid} é a id da chave.</span><span class="sxs-lookup"><span data-stu-id="6031f-108">By convention keys have the filename **key-{guid}.xml**, where {guid} is the id of the key.</span></span> <span data-ttu-id="6031f-109">Cada arquivo contém uma única chave.</span><span class="sxs-lookup"><span data-stu-id="6031f-109">Each such file contains a single key.</span></span> <span data-ttu-id="6031f-110">O formato do arquivo é da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="6031f-110">The format of the file is as follows.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<key id="80732141-ec8f-4b80-af9c-c4d2d1ff8901" version="1">
  <creationDate>2015-03-19T23:32:02.3949887Z</creationDate>
  <activationDate>2015-03-19T23:32:02.3839429Z</activationDate>
  <expirationDate>2015-06-17T23:32:02.3839429Z</expirationDate>
  <descriptor deserializerType="{deserializerType}">
    <descriptor>
      <encryption algorithm="AES_256_CBC" />
      <validation algorithm="HMACSHA256" />
      <enc:encryptedSecret decryptorType="{decryptorType}" xmlns:enc="...">
        <encryptedKey>
          <!-- This key is encrypted with Windows DPAPI. -->
          <value>AQAAANCM...8/zeP8lcwAg==</value>
        </encryptedKey>
      </enc:encryptedSecret>
    </descriptor>
  </descriptor>
</key>
```

<span data-ttu-id="6031f-111">O \<key > elemento contém os seguintes atributos e elementos filho:</span><span class="sxs-lookup"><span data-stu-id="6031f-111">The \<key> element contains the following attributes and child elements:</span></span>

* <span data-ttu-id="6031f-112">A id da chave. Esse valor é tratado como autoritativo; o nome do arquivo é simplesmente uma sutileza por humanos.</span><span class="sxs-lookup"><span data-stu-id="6031f-112">The key id. This value is treated as authoritative; the filename is simply a nicety for human readability.</span></span>

* <span data-ttu-id="6031f-113">A versão do \<key > elemento, no momento é fixado em 1.</span><span class="sxs-lookup"><span data-stu-id="6031f-113">The version of the \<key> element, currently fixed at 1.</span></span>

* <span data-ttu-id="6031f-114">Datas de criação, ativação e expiração da chave.</span><span class="sxs-lookup"><span data-stu-id="6031f-114">The key's creation, activation, and expiration dates.</span></span>

* <span data-ttu-id="6031f-115">Um \<descritor > elemento, que contém informações sobre a implementação de criptografia autenticada contida dentro dessa chave.</span><span class="sxs-lookup"><span data-stu-id="6031f-115">A \<descriptor> element, which contains information on the authenticated encryption implementation contained within this key.</span></span>

<span data-ttu-id="6031f-116">No exemplo acima, id da chave é {80732141-ec8f-4b80-af9c-c4d2d1ff8901}, ele foi criado e ativado no dia 19 de março de 2015, e ele tem um tempo de vida de 90 dias.</span><span class="sxs-lookup"><span data-stu-id="6031f-116">In the above example, the key's id is {80732141-ec8f-4b80-af9c-c4d2d1ff8901}, it was created and activated on March 19, 2015, and it has a lifetime of 90 days.</span></span> <span data-ttu-id="6031f-117">(Ocasionalmente, a data de ativação pode ser um pouco antes da data de criação, como neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="6031f-117">(Occasionally the activation date might be slightly before the creation date as in this example.</span></span> <span data-ttu-id="6031f-118">Isso ocorre devido a um nit em como as APIs funcionam e é inofensivas na prática.)</span><span class="sxs-lookup"><span data-stu-id="6031f-118">This is due to a nit in how the APIs work and is harmless in practice.)</span></span>

## <a name="the-descriptor-element"></a><span data-ttu-id="6031f-119">O \<descritor > elemento</span><span class="sxs-lookup"><span data-stu-id="6031f-119">The \<descriptor> element</span></span>

<span data-ttu-id="6031f-120">Externo \<descritor > elemento contém um deserializerType de atributo, que é o nome qualificado pelo assembly de um tipo que implementa IAuthenticatedEncryptorDescriptorDeserializer.</span><span class="sxs-lookup"><span data-stu-id="6031f-120">The outer \<descriptor> element contains an attribute deserializerType, which is the assembly-qualified name of a type which implements IAuthenticatedEncryptorDescriptorDeserializer.</span></span> <span data-ttu-id="6031f-121">Esse tipo é responsável por ler interno \<descritor > elemento e para analisar as informações contidas neles.</span><span class="sxs-lookup"><span data-stu-id="6031f-121">This type is responsible for reading the inner \<descriptor> element and for parsing the information contained within.</span></span>

<span data-ttu-id="6031f-122">O formato específico do \<descritor > elemento depende da implementação do Criptografador autenticado encapsulada pela chave e cada tipo de desserializador espera um formato ligeiramente diferente para isso.</span><span class="sxs-lookup"><span data-stu-id="6031f-122">The particular format of the \<descriptor> element depends on the authenticated encryptor implementation encapsulated by the key, and each deserializer type expects a slightly different format for this.</span></span> <span data-ttu-id="6031f-123">Em geral, no entanto, esse elemento conterá informações algorítmicos (nomes, tipos, OIDs, ou semelhante) e o material de chave secreta.</span><span class="sxs-lookup"><span data-stu-id="6031f-123">In general, though, this element will contain algorithmic information (names, types, OIDs, or similar) and secret key material.</span></span> <span data-ttu-id="6031f-124">No exemplo acima, o descritor especifica que essa chave encapsula a criptografia AES-256-CBC + HMACSHA256 validação.</span><span class="sxs-lookup"><span data-stu-id="6031f-124">In the above example, the descriptor specifies that this key wraps AES-256-CBC encryption + HMACSHA256 validation.</span></span>

## <a name="the-encryptedsecret-element"></a><span data-ttu-id="6031f-125">O \<encryptedSecret > elemento</span><span class="sxs-lookup"><span data-stu-id="6031f-125">The \<encryptedSecret> element</span></span>

<span data-ttu-id="6031f-126">Uma **&lt;encryptedSecret&gt;** elemento que contém o formulário criptografado do material de chave secreto pode estar presente se [criptografia de segredos em repouso está ativada](xref:security/data-protection/implementation/key-encryption-at-rest).</span><span class="sxs-lookup"><span data-stu-id="6031f-126">An **&lt;encryptedSecret&gt;** element which contains the encrypted form of the secret key material may be present if [encryption of secrets at rest is enabled](xref:security/data-protection/implementation/key-encryption-at-rest).</span></span> <span data-ttu-id="6031f-127">O atributo `decryptorType` é o nome qualificado pelo assembly de um tipo que implementa [IXmlDecryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.xmlencryption.ixmldecryptor).</span><span class="sxs-lookup"><span data-stu-id="6031f-127">The attribute `decryptorType` is the assembly-qualified name of a type which implements [IXmlDecryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.xmlencryption.ixmldecryptor).</span></span> <span data-ttu-id="6031f-128">Esse tipo é responsável por ler interna **&lt;encryptedKey&gt;** elemento e descriptografá-los para recuperar o texto sem formatação original.</span><span class="sxs-lookup"><span data-stu-id="6031f-128">This type is responsible for reading the inner **&lt;encryptedKey&gt;** element and decrypting it to recover the original plaintext.</span></span>

<span data-ttu-id="6031f-129">Assim como acontece com \<descritor >, o formato específico do <encryptedSecret> elemento depende do mecanismo de criptografia em repouso em uso.</span><span class="sxs-lookup"><span data-stu-id="6031f-129">As with \<descriptor>, the particular format of the <encryptedSecret> element depends on the at-rest encryption mechanism in use.</span></span> <span data-ttu-id="6031f-130">No exemplo acima, a chave mestra é criptografada usando a DPAPI do Windows por comentário.</span><span class="sxs-lookup"><span data-stu-id="6031f-130">In the above example, the master key is encrypted using Windows DPAPI per the comment.</span></span>

## <a name="the-revocation-element"></a><span data-ttu-id="6031f-131">O \<revogação > elemento</span><span class="sxs-lookup"><span data-stu-id="6031f-131">The \<revocation> element</span></span>

<span data-ttu-id="6031f-132">Revogações existem como objetos de nível superior no repositório de chave.</span><span class="sxs-lookup"><span data-stu-id="6031f-132">Revocations exist as top-level objects in the key repository.</span></span> <span data-ttu-id="6031f-133">Por convenção revogações têm o nome do arquivo **revogação-{timestamp}. XML** (para revogar todas as chaves antes de uma data específica) ou **revogação-{guid}. XML** (para a revogação de uma chave específica).</span><span class="sxs-lookup"><span data-stu-id="6031f-133">By convention revocations have the filename **revocation-{timestamp}.xml** (for revoking all keys before a specific date) or **revocation-{guid}.xml** (for revoking a specific key).</span></span> <span data-ttu-id="6031f-134">Cada arquivo contém um único \<revogação > elemento.</span><span class="sxs-lookup"><span data-stu-id="6031f-134">Each file contains a single \<revocation> element.</span></span>

<span data-ttu-id="6031f-135">Para revogações de chaves individuais, o conteúdo do arquivo será conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="6031f-135">For revocations of individual keys, the file contents will be as below.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<revocation version="1">
  <revocationDate>2015-03-20T22:45:30.2616742Z</revocationDate>
  <key id="eb4fc299-8808-409d-8a34-23fc83d026c9" />
  <reason>human-readable reason</reason>
</revocation>
```

<span data-ttu-id="6031f-136">Nesse caso, apenas a chave especificada é revogada.</span><span class="sxs-lookup"><span data-stu-id="6031f-136">In this case, only the specified key is revoked.</span></span> <span data-ttu-id="6031f-137">Se a id da chave é "\*", no entanto, como mostra o exemplo abaixo, cuja data de criação está antes da data de revogação especificado de todas as chaves são revogadas.</span><span class="sxs-lookup"><span data-stu-id="6031f-137">If the key id is "\*", however, as in the below example, all keys whose creation date is prior to the specified revocation date are revoked.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<revocation version="1">
  <revocationDate>2015-03-20T15:45:45.7366491-07:00</revocationDate>
  <!-- All keys created before the revocation date are revoked. -->
  <key id="*" />
  <reason>human-readable reason</reason>
</revocation>
```

<span data-ttu-id="6031f-138">O \<motivo > elemento nunca é lido pelo sistema.</span><span class="sxs-lookup"><span data-stu-id="6031f-138">The \<reason> element is never read by the system.</span></span> <span data-ttu-id="6031f-139">Ele é simplesmente um local conveniente para armazenar um motivo legível por humanos para revogação.</span><span class="sxs-lookup"><span data-stu-id="6031f-139">It's simply a convenient place to store a human-readable reason for revocation.</span></span>
