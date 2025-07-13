# Guia de Configuração de Ambiente para o Projeto

Este guia descreve os passos necessários para configurar o ambiente de desenvolvimento para este projeto, que já está disponível no GitHub. Seguir estes passos garantirá que você possa importar, compilar e executar a aplicação Eclipse RCP corretamente.

## Índice

  - [Pré-requisitos](https://www.google.com/search?q=%23pr%C3%A9-requisitos)
  - [Parte 1: Configuração do Ambiente no Windows](https://www.google.com/search?q=%23parte-1-configura%C3%A7%C3%A3o-do-ambiente-no-windows)
      - [1.1: Instalação do Java 21 (Windows)](https://www.google.com/search?q=%2311-instala%C3%A7%C3%A3o-do-java-21-windows)
      - [1.2: Instalação do Eclipse IDE (Windows)](https://www.google.com/search?q=%2312-instala%C3%A7%C3%A3o-do-eclipse-ide-windows)
  - [Parte 2: Configuração do Ambiente no Linux (Debian/Ubuntu)](https://www.google.com/search?q=%23parte-2-configura%C3%A7%C3%A3o-do-ambiente-no-linux-debianubuntu)
      - [2.1: Instalação do Java 21 (Linux)](https://www.google.com/search?q=%2321-instala%C3%A7%C3%A3o-do-java-21-linux)
      - [2.2: Instalação do Eclipse IDE (Linux)](https://www.google.com/search?q=%2322-instala%C3%A7%C3%A3o-do-eclipse-ide-linux)
  - [Parte 3: Configuração Comum do Eclipse (Multiplataforma)](https://www.google.com/search?q=%23parte-3-configura%C3%A7%C3%A3o-comum-do-eclipse-multiplataforma)
      - [3.1: Configuração do JDK no Eclipse](https://www.google.com/search?q=%2331-configura%C3%A7%C3%A3o-do-jdk-no-eclipse)
      - [3.2: Configuração da Target Platform](https://www.google.com/search?q=%2332-configura%C3%A7%C3%A3o-da-target-platform)
  - [Parte 4: Importando e Executando o Projeto](https://www.google.com/search?q=%23parte-4-importando-e-executando-o-projeto)
  - [Solução de Problemas Comuns (Troubleshooting)](https://www.google.com/search?q=%23solu%C3%A7%C3%A3o-de-problemas-comuns-troubleshooting)

## Pré-requisitos

Antes de começar, certifique-se de que você tem os seguintes softwares instalados:

1.  **Java Development Kit (JDK)**

      - **Versão:** Java 21.
      - **Observação:** Um JRE (Java Runtime Environment) não é suficiente. É necessário o JDK completo.

2.  **Git**

      - Necessário para clonar o repositório do projeto a partir do GitHub.

-----

## Parte 1: Configuração do Ambiente no Windows

### 1.1: Instalação do Java 21 (Windows)

1.  **Baixe o JDK:** Faça o download do instalador do OpenJDK 21 (ou Oracle JDK 21) para Windows.
2.  **Execute o Instalador:** Siga os passos do instalador. Ele geralmente configura o registro do Windows, mas é uma boa prática configurar as variáveis de ambiente manualmente.
3.  **Configure as Variáveis de Ambiente:**
      - Pesquise por "Editar as variáveis de ambiente do sistema" no menu Iniciar.
      - Na janela de "Propriedades do Sistema", clique em "Variáveis de Ambiente...".
      - Em "Variáveis do sistema", clique em "Novo..." e crie a variável `JAVA_HOME` apontando para o diretório de instalação do JDK (ex: `C:\Program Files\Java\jdk-21`).
      - Encontre a variável `Path`, clique em "Editar...", depois em "Novo" e adicione a entrada `%JAVA_HOME%\bin`.
4.  **Verifique a Instalação:** Abra um novo Prompt de Comando e digite `java -version`. A saída deve mostrar a versão 21.

### 1.2: Instalação do Eclipse IDE (Windows)

Para este projeto, precisamos de ferramentas tanto para desenvolvimento RCP quanto para visualização de DSLs. A abordagem recomendada é instalar a IDE para RCP e depois adicionar as ferramentas de DSL.

1.  **Baixe o Eclipse Installer:** Acesse a [página de downloads do Eclipse](https://www.eclipse.org/downloads/) e baixe o "Eclipse Installer".
2.  **Execute o Instalador:**
      - Abra o instalador.
      - Na lista de pacotes, selecione **"Eclipse IDE for RCP and RAP Developers"**. Este será nosso ambiente base de desenvolvimento do plug-in.
      - Escolha o diretório de instalação e conclua a instalação.
      - Repita o mesmo processo com o **"Eclipse IDE for Java and DSL Developers"**. Este será o ambiente que você poderá visualizar os scripts DSL.

-----

## Parte 2: Configuração do Ambiente no Linux (Debian/Ubuntu)

### 2.1: Instalação do Java 21 (Linux)

1.  **Abra o Terminal.**
2.  **Atualize os Pacotes:**
    ```bash
    sudo apt update
    ```
3.  **Instale o OpenJDK 21:**
    ```bash
    sudo apt install openjdk-21-jdk
    ```
4.  **Verifique a Instalação:**
    ```bash
    java -version
    ```
    A saída deve mostrar a versão 21.

### 2.2: Instalação do Eclipse IDE (Linux)

Não é recomendado instalar o Eclipse via `apt`, pois a versão nos repositórios costuma ser antiga. O método correto é baixar o arquivo `.tar.gz`.

1.  **Baixe o Eclipse IDE:**
      - Acesse a [página de downloads de pacotes do Eclipse](https://www.eclipse.org/downloads/packages/).
      - Baixe o arquivo `.tar.gz` do pacote **"Eclipse IDE for RCP and RAP Developers"** para Linux.
2.  **Extraia e Mova o Eclipse:**
      - Abra o terminal e navegue até a pasta onde o arquivo foi baixado (geralmente `~/Downloads`).
      - Extraia o arquivo:
        ```bash
        tar -xzf eclipse-rcp-*.tar.gz
        ```
      - Mova a pasta extraída para um local padrão, como `/opt`:
        ```bash
        sudo mv eclipse /opt/
        ```
3.  **Crie um Lançador (Opcional, mas Recomendado):**
      - Crie um arquivo `.desktop` para iniciar o Eclipse facilmente:
        ```bash
        sudo nano /usr/share/applications/eclipse.desktop
        ```
      - Cole o seguinte conteúdo no editor, salve (`Ctrl+O`) e feche (`Ctrl+X`):
        ```ini
        [Desktop Entry]
        Name=Eclipse IDE
        Comment=Eclipse IDE for RCP and RAP Developers
        Type=Application
        Exec=/opt/eclipse/eclipse
        Icon=/opt/eclipse/icon.xpm
        Terminal=false
        Categories=Development;IDE;Java;
        ```
4.  **Adicione as Ferramentas de DSL:**
      - Repita o mesmo processo com o **"Eclipse IDE for Java and DSL Developers"**. Este será o ambiente que você poderá visualizar os scripts DSL.

-----

## Parte 3: Importando e Executando o Projeto

1.  **Clone e Importe:**
      - Vá em `File` \> `Import...` \> `Git` \> `Projects from Git`.
      - Selecione `Clone URI`, cole o URL do repositório do GitHub e siga os passos do assistente.
      - Na tela "Import Projects", certifique-se de que todos os projetos do repositório sejam importados para o workspace.
2.  **Execute a Aplicação:**
      - Clique com o botão direito no projeto do plugin principal.
      - Vá em `Run As` \> `Eclipse Application`.
      - Uma nova instância do Eclipse será lançada com a sua aplicação em execução.

## Solução de Problemas Comuns (Troubleshooting)

  - **Erro: `NoClassDefFoundError` ou `ClassNotFoundException`:** A dependência não foi declarada no `MANIFEST.MF` do seu plugin. Vá na aba `Dependencies` e adicione o plugin faltante.
  - **Erro: "Unresolved requirement" ou "Missing Constraint":** O plugin necessário não existe na sua Target Platform. Edite sua Target Platform e adicione o software que está faltando.
  - **Erro: Adicionei um JAR ao `Java Build Path`, mas não funciona:** Esta é a forma **incorreta** de adicionar dependências em RCP. Remova o JAR do build path e adicione a dependência via Target Platform e `MANIFEST.MF`.
