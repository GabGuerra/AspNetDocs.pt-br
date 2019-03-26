---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Criar um banco de dados | Microsoft Docs
author: microsoft
description: Etapa 2 mostra as etapas para criar o banco de dados que contém todos os o jantar e CONFIRME os dados de nosso aplicativo NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: 48ca2984ca8e4ec5b2bc49952a8718aa26138aea
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2019
ms.locfileid: "58423696"
---
<a name="create-a-database"></a>Criar um banco de dados
====================
por [Microsoft](https://github.com/microsoft)

[Baixar PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Esta é a etapa 2 do grátis [aplicativo "NerdDinner"](introducing-the-nerddinner-tutorial.md) que orienta-through como criar um pequeno, mas concluir, o aplicativo web usando ASP.NET MVC 1.
> 
> Etapa 2 mostra as etapas para criar o banco de dados que contém todos os o jantar e CONFIRME os dados de nosso aplicativo NerdDinner.
> 
> Se você estiver usando o ASP.NET MVC 3, recomendamos que você siga a [obtendo iniciado com o MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) ou [Store de música do MVC](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutoriais.


## <a name="nerddinner-step-2-creating-the-database"></a>Etapa 2 do NerdDinner: Criando o banco de dados

Usaremos um banco de dados para armazenar todos os dados de jantar e RSVP para nosso aplicativo NerdDinner.

As etapas a seguir mostram a criação de banco de dados usando a edição gratuita do SQL Server Express (que você pode instalar facilmente usando V2 do [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)). Todo o código que escreveremos funciona com o SQL Server Express e o SQL Server completo.

### <a name="creating-a-new-sql-server-express-database"></a>Criando um novo banco de dados do SQL Server Express

Vamos começar clicando-se em nosso projeto web e, em seguida, selecione a **Add -&gt;Novo Item** comando de menu:

![](create-a-database/_static/image1.png)

Isso exibirá a caixa de diálogo de "Adicionar Novo Item" do Visual Studio. Vamos filtrar por categoria "Dados" e selecione o modelo de item de "Banco de dados do SQL Server":

![](create-a-database/_static/image2.png)

Nomear o banco de dados do SQL Server Express que desejamos criar "NerdDinner.mdf" e pressionar okey. Visual Studio, então, solicitará-nos se quisermos adicionar esse arquivo para nosso \App\_diretório de dados (que é um diretório já de instalação com a leitura e gravação de ACLs de segurança):

![](create-a-database/_static/image3.png)

Vamos clicar em "Sim" e nosso novo banco de dados será criado e adicionado ao nosso Gerenciador de soluções:

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>Criando tabelas dentro de nosso banco de dados

Agora temos um novo banco de dados vazio. Vamos adicionar algumas tabelas a ele.

Para fazer isso vamos navegar até a janela de guia "Gerenciador de servidores" dentro do Visual Studio, que permite gerenciar servidores e bancos de dados. Bancos de dados SQL Server Express armazenados em do \App\_pasta de dados do nosso aplicativo aparecerá automaticamente no Gerenciador de servidores. Pode, opcionalmente, usamos o ícone de "Conectar-se ao banco de dados" na parte superior da janela "Server Explorer" para adicionar bancos de dados do SQL Server adicionais (locais e remotos) para a lista também:

![](create-a-database/_static/image5.png)

Vamos adicionar duas tabelas para nosso banco de dados do NerdDinner – um para armazenar nosso jantares e outro para acompanhar o RSVP aceitações a eles. Podemos criar novas tabelas clicando duas vezes na pasta "Tabelas" dentro do nosso banco de dados e escolher o comando de menu "Adicionar nova tabela":

![](create-a-database/_static/image6.png)

Isso abrirá um designer de tabela que permite que configuremos o esquema de nossa tabela. Para nossa tabela "Jantares", adicionaremos 10 colunas de dados:

![](create-a-database/_static/image7.png)

Queremos que a coluna "DinnerID" para ser uma chave primária exclusiva para a tabela. Podemos configurar isso clicando duas vezes na coluna "DinnerID" e escolhendo o item de menu "Definir chave primária":

![](create-a-database/_static/image8.png)

Além de tornar DinnerID uma chave primária, também queremos que configurá-lo como uma coluna de "identidade" cujo valor é incrementado automaticamente conforme novas linhas de dados são adicionadas à tabela (ou seja, a primeira linha inserida do jantar terá um DinnerID de 1, o segundo inserido linha terá um DinnerID de 2, etc).

Podemos fazer isso, selecione a coluna "DinnerID" e, em seguida, use o editor de "Propriedades da coluna" para definir a propriedade "(é identidade)" na coluna como "Sim". Usaremos os padrões de identidade padrão (iniciam em 1 e incrementar 1 em cada nova linha de jantar):

![](create-a-database/_static/image9.png)

Em seguida, salvaremos nossa tabela digitando Ctrl-S ou usando o **arquivo -&gt;salvar** comando de menu. Essa ação solicitará que nos dê um nome de tabela. Vamos chamá-la de "Jantares":

![](create-a-database/_static/image10.png)

Nossa nova tabela de jantares, em seguida, serão exibidos em nosso banco de dados no Gerenciador de servidores.

Vamos, em seguida, repita as etapas acima e criar uma tabela de "Confirmação". Essa tabela com tem 3 colunas. Vamos configurar a coluna RsvpID como a chave primária e também o tornam uma coluna de identidade:

![](create-a-database/_static/image11.png)

Vamos salvá-lo e dê a ele o nome "RSVP".

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>Como configurar uma relação de chave estrangeira entre tabelas

Agora temos duas tabelas dentro de nosso banco de dados. Nossa última etapa de design de esquema será configurar um relacionamento entre essas duas tabelas – de "um-para-muitos", de modo que podemos pode associar cada linha de jantar com zero ou mais linhas RSVP que se aplicam a ele. Faremos isso configurando a RSVP coluna da tabela "DinnerID" para ter uma relação de chave estrangeira para a coluna "DinnerID" na tabela "Jantares".

Para fazer isso, que vamos abri a tabela de RSVP dentro do designer de tabela clicando duas vezes no Gerenciador de servidores. Em seguida, vamos selecionar a coluna "DinnerID" dentro dele, direito do mouse e escolha o "relações..." comando de menu de contexto:

![](create-a-database/_static/image12.png)

Isso abrirá uma caixa de diálogo que podemos usar relações de instalação entre tabelas:

![](create-a-database/_static/image13.png)

Clicaremos no botão "Adicionar" para adicionar uma nova relação na caixa de diálogo. Após a adição de uma relação, podemos vai expandir o nó do modo de exibição de árvore de "Especificação de tabelas e coluna" dentro da grade de propriedade à direita da caixa de diálogo e, em seguida, clique no botão "..." à direita dele:

![](create-a-database/_static/image14.png)

Clicar no botão "..." abrirá outra caixa de diálogo que nos permite especificar quais tabelas e colunas estão envolvidas na relação, como também nos permitem nomear a relação.

Iremos alterar a tabela de chave primária para ser "Jantares" e selecione a coluna "DinnerID" dentro da tabela de jantares como a chave primária. Nossa tabela RSVP será o RSVP e a tabela de chave estrangeira. Coluna DinnerID será associada como a chave estrangeira:

![](create-a-database/_static/image15.png)

Agora, cada linha na tabela RSVP será associada uma linha na tabela de jantar. SQL Server irá manter a integridade referencial para que possamos – e nos impedem de adicionar uma nova linha RSVP se ele não aponta para uma linha válida do jantar. Ele também impedirá nos de exclusão de uma linha de jantar se não houver ainda RSVP linhas se referindo a ele.

### <a name="adding-data-to-our-tables"></a>Adicionando dados a nossas tabelas

Vamos terminar com a adição de alguns dados de exemplo para nossa tabela jantares. Podemos adicionar dados a uma tabela clicando duas vezes no Gerenciador de servidores e escolhendo o comando "Mostrar dados da tabela":

![](create-a-database/_static/image16.png)

Vamos adicionar algumas linhas de dados de Dinner que usaremos mais tarde, como podemos começar a implementar o aplicativo:

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>Próxima etapa

Podemos concluir a criação de nosso banco de dados. Agora, vamos criar classes de modelo que podemos usar para consultar e atualizá-lo.

> [!div class="step-by-step"]
> [Anterior](create-a-new-aspnet-mvc-project.md)
> [Próximo](build-a-model-with-business-rule-validations.md)
