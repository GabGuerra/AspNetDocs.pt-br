---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: Instalando manualmente os pacotes da Web | Microsoft Docs
author: jrjlee
description: Este tópico descreve como importar manualmente um pacote de implantação da web em serviços de informações da Internet (IIS). A construção de tópico e o aplicativo da Web de empacotamento...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: 9d0e57eb85242a0d6fa8ca9eef7f6c741862069d
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59408791"
---
# <a name="manually-installing-web-packages"></a>Instalação manual de pacotes da Web

by [Jason Lee](https://github.com/jrjlee)

[Baixar PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Este tópico descreve como importar manualmente um pacote de implantação da web em serviços de informações da Internet (IIS).
> 
> O tópico [compilação e empacotamento Web Application Projects](building-and-packaging-web-application-projects.md) descrito como o IIS ferramenta de implantação Web (implantação da Web), em conjunto com o Microsoft Build Engine (MSBuild) e o Web Publishing Pipeline (WPP), permite que você empacotar seu projetos de aplicativos Web em um único arquivo zip. Esse arquivo, conhecido como um pacote de implantação da web (ou simplesmente um pacote de implantação), contém todas as informações de configuração e conteúdo que o IIS precisa para recriar seu aplicativo web em um servidor web.
> 
> Depois de criar um pacote de implantação da web, você pode publicá-lo em um servidor IIS de várias maneiras. Em muitos cenários, você vai querer tirar proveito dos pontos de integração entre o MSBuild, o WPP e implantação da Web para criar e instalar pacotes da web remotamente, como parte de um processo de compilação e implantação automatizado ou passo a passo. Esse processo é descrito em [Implantando pacotes da Web](deploying-web-packages.md). No entanto, isso nem sempre é possível. Suponha que você deseja implantar um aplicativo web em um ambiente de produção para a Internet. Por motivos de segurança, um ambiente de produção desse tipo é em muito menos provável estar por trás de um firewall em uma sub-rede que é separado do servidor de compilação, em uma rede de perímetro (também conhecida como DMZ, zona desmilitarizada e sub-rede filtrada). Em muitos casos, o ambiente de produção será em um domínio separado ou em uma rede fisicamente isolada.
> 
> Nesses cenários, sua única opção pode ser portar o pacote da web no servidor de destino e importá-lo manualmente no IIS. Embora essa abordagem impede a implantação automatizada, ainda é uma técnica altamente eficaz para publicar um aplicativo web&#x2014;simplesmente copiar um único arquivo zip em seu servidor web e usar um Assistente para orientá-lo o processo de importação.


Este tópico faz parte de uma série de tutoriais com base em torno de requisitos corporativos de implantação de uma empresa fictícia chamada Fabrikam, Inc. Esta série de tutoriais usa uma solução de exemplo&#x2014;o [entre em contato com o Gerenciador soluções](the-contact-manager-solution.md)&#x2014;para representar um aplicativo web com um nível realista de complexidade, incluindo um aplicativo ASP.NET MVC 3, uma comunicação do Windows Serviço Foundation (WCF) e um projeto de banco de dados.

## <a name="task-overview"></a>Visão geral da tarefa

Você precisará concluir essas tarefas de alto nível para importar um pacote de implantação da web no IIS:

- Crie um pacote de implantação da web usando o MSBuild linha de comando, Team Build ou o Visual Studio 2010.
- Copie o pacote da web para o servidor web de destino.
- Use o Assistente de importação de pacote de aplicativo no Gerenciador do IIS para instalar o pacote da web e fornecer valores para variáveis, como cadeias de caracteres de conexão e pontos de extremidade de serviço.

Este tópico mostra como executar esses procedimentos. As tarefas e instruções passo a passo neste tópico pressupõem que você já esteja familiarizado com os conceitos por trás de pacotes da web, implantação da Web e o WPP. Para obter mais informações, consulte [compilação e empacotamento Web Application Projects](building-and-packaging-web-application-projects.md).

> [!NOTE]
> Este tópico é melhor usado em conjunto com [configurar um servidor Web para publicação de implantação do Web (off-line de implantação)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md), que explica como instalar os componentes necessários e preparar um site do IIS para a importação de pacote.


## <a name="create-a-web-deployment-package"></a>Criar um pacote de implantação da Web

A primeira tarefa é criar um pacote de implantação da web para o projeto de aplicativo web que você deseja implantar. Você pode criar pacotes da web de várias maneiras.

**Abordagem 1: Criar um pacote como parte do processo de compilação com o Visual Studio**

Você pode configurar seu projeto de aplicativo web para criar um pacote de implantação da web depois de cada compilação por meio de **empacotar/Publicar Web** guia nas páginas de propriedades do projeto. Esse processo é descrito em [compilação e empacotamento Web Application Projects](building-and-packaging-web-application-projects.md).

**Abordagem 2: Criar um pacote como parte do processo de compilação com o MSBuild**

Se você compilar seu projeto de aplicativo web usando o MSBuild diretamente, por meio de um arquivo de projeto personalizado do MSBuild ou da linha de comando, você pode criar um pacote de implantação da web como parte do processo de compilação, incluindo o **DeployOnBuild = true** e **DeployTarget 2=pacote** propriedades em seu comando. Esse processo é descrito em [Noções básicas sobre o processo de compilação](understanding-the-build-process.md).

**Abordagem 3: Criar um pacote sob demanda no Visual Studio**

Você pode criar um pacote de implantação da web para um projeto de aplicativo web a qualquer momento no Visual Studio 2010. Para fazer isso, na **Gerenciador de soluções** , clique em seu projeto de aplicativo web e, em seguida, clique em **criar o pacote de implantação**.

![](manually-installing-web-packages/_static/image1.png)

**Abordagem 4: Criar um pacote sob demanda a partir da linha de comando**

Você pode criar um pacote de implantação da web da linha de comando, invocando o **pacote** destino em seu projeto de aplicativo web usando o MSBuild. O comando deve ter esta aparência:


[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]


O que a abordagem usar, o resultado final é o mesmo. O WPP cria um pacote de implantação da web como um arquivo zip, junto com vários recursos de suporte, na pasta de saída do projeto de aplicativo da web.

![](manually-installing-web-packages/_static/image2.png)

Quando você estiver planejando importar manualmente o pacote da web, você pode exigir apenas o arquivo zip. Copie esse arquivo para seu servidor web de destino, e você pode começar o processo de importação.

## <a name="import-a-web-package-into-iis"></a>Importar um pacote da Web para o IIS

Você pode usar o procedimento a seguir para importar um pacote de implantação da web do sistema de arquivos local para um site do IIS. Antes de executar este procedimento, certifique-se de que você tenha:

- Copiou o pacote de implantação da web para o servidor web.
- Configurado um servidor de web do IIS para hospedar seu aplicativo.

Para obter mais informações sobre como configurar um servidor de web do IIS para dar suporte a pacotes de implantação da web, consulte [configurar um servidor Web para publicação de implantação do Web (off-line de implantação)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).

**Para importar um pacote de implantação da web usando o Gerenciador do IIS**

1. No Gerenciador do IIS, nos **conexões** painel, clique com botão direito seu site do IIS, aponte para **Deploy**e, em seguida, clique em **importar aplicativo**.

    ![](manually-installing-web-packages/_static/image3.png)
2. No Assistente do pacote de aplicativo de importação, sobre o **, selecione o pacote** página, navegue até o local do seu pacote de implantação da web e, em seguida, clique em **próximo**.
3. Sobre o **selecionar o conteúdo do pacote** página, desmarque qualquer conteúdo que você não precisa e, em seguida, clique em **próxima**.

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > Em muitos casos, talvez não queira importar tudo o que vem com um pacote de implantação da web. Por exemplo, não convém permitir a implantação da Web substituir o banco de dados associado.  
    > O **conceder permissões** entradas definir permissões no sistema de arquivos de destino para garantir que a identidade do pool de aplicativos pode acessar a pasta física que armazena o conteúdo do site. Além disso, o usuário de autenticação anônima é concedida permissão de leitura para a pasta para permitir que o aplicativo fornecer arquivos de tipo de email extensões MIME (Multipurpose Internet). Se você preferir, você pode remover essas entradas e configurar as permissões manualmente.
4. Sobre o **inserir informações do pacote de aplicativo** , forneça as informações solicitadas.

    ![](manually-installing-web-packages/_static/image5.png)
5. Quando você cria um pacote da web, o WPP analisa o arquivo de configuração para seu aplicativo e detecta todas as variáveis, como cadeias de caracteres de conexão e pontos de extremidade de serviço. Nesse caso:

    1. **Caminho do aplicativo** é o caminho do IIS onde você deseja instalar seu aplicativo. Essa configuração é comum a todos os pacotes de implantação que cria o WPP.
    2. **Endereço do ponto de extremidade de serviço ContactService** é o endereço que o aplicativo deve usar para se comunicar com o serviço WCF implantado. Essa configuração corresponde a uma entrada na *Web. config* arquivo.
    3. A primeira **cadeia de caracteres de Conexão** configuração é a cadeia de caracteres de conexão que a implantação da Web deve usar para implantar o banco de dados associado com o aplicativo (neste caso, um associação ao banco de dados ASP.NET). Essa configuração corresponde à configuração sobre o **empacotar/publicar SQL** guia no Visual Studio.
    4. A segunda **cadeia de caracteres de Conexão** configuração é a cadeia de caracteres de conexão que seu aplicativo, na verdade, usará para se comunicar com o banco de dados quando ele está em execução. Isso corresponde a uma entrada de cadeia de caracteres de conexão na *Web. config* arquivo.

        > [!NOTE]
        > Para obter mais informações sobre de onde vêm esses parâmetros, consulte [Configurando parâmetros para a implantação de pacote da Web](configuring-parameters-for-web-package-deployment.md).
6. Clique em **Avançar**.
7. Se isso não for a primeira vez em que você implantou o aplicativo neste site, você será solicitado a especificar se deseja excluir todo o conteúdo existente antes da instalação. Escolha a opção apropriada para suas necessidades e, em seguida, clique em **próxima**.

    ![](manually-installing-web-packages/_static/image6.png)
8. Quando o IIS terminou de instalar o pacote, clique em **concluir**.

    ![](manually-installing-web-packages/_static/image7.png)

Neste ponto, você publicou com êxito seu aplicativo web no IIS.

## <a name="conclusion"></a>Conclusão

Este tópico descreveu como importar um pacote de implantação da web para um site do IIS usando o Gerenciador do IIS. Essa abordagem para publicação de aplicativos web é apropriada quando as restrições de segurança ou a infraestrutura faz a implantação remota impossível ou indesejável.

## <a name="further-reading"></a>Leitura adicional

Para obter orientação sobre como configurar um servidor de web do IIS para dar suporte à importação manual de um pacote da web, consulte [configurar um servidor Web para publicação de implantação do Web (off-line de implantação)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md). Para obter orientação geral sobre a implantação de pacotes da web, consulte [passo a passo: Implantando um projeto de aplicativo Web usando um pacote de implantação da Web (parte 1 de 4)](https://msdn.microsoft.com/library/dd483479.aspx).

> [!div class="step-by-step"]
> [Voltar](creating-and-running-a-deployment-command-file.md)
