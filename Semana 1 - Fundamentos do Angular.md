# Semana 1: Fundamentos do Angular

## O que é Angular?

- Angular é um framework de desenvolvimento front-end criado pelo Google, que utiliza TypeScript como sua linguagem principal. Ele é projetado para construir aplicações web dinâmicas e de página única (SPAs - Single Page Applications). O Angular é amplamente utilizado devido à sua capacidade de criar aplicações robustas e escaláveis.

## Principais Características do Angular:

### Arquitetura Baseada em Componentes:
- Angular utiliza o conceito de componentes, que são blocos de construção reutilizáveis para a interface do usuário. Cada componente possui um template (HTML), uma classe (TypeScript) e um arquivo de estilo (CSS).

### TypeScript:
- Angular é escrito em TypeScript, uma linguagem que é um superconjunto de JavaScript e oferece tipagem estática, interfaces, e outras funcionalidades avançadas que ajudam a construir aplicações mais robustas e menos propensas a erros.

### Roteamento:
- Angular possui um sistema de roteamento integrado que permite a navegação entre diferentes vistas ou componentes dentro de uma aplicação de página única.

### Injeção de Dependência:
- Angular oferece um sistema de injeção de dependência que facilita a gestão de dependências e promove a modularidade e reutilização de código.

### Formulários:
- Angular fornece suporte robusto para a criação e gerenciamento de formulários, incluindo validação e manipulação de dados de entrada do usuário.

### Comunicação HTTP:
- Angular possui um módulo HTTP que facilita a comunicação com servidores remotos via HTTP, permitindo a realização de operações como GET, POST, PUT, DELETE, etc.

### Diretivas:
- Diretivas são instruções no DOM que podem alterar o layout ou comportamento de elementos. Existem três tipos principais: componentes, diretivas estruturais (como *ngIf, *ngFor) e diretivas de atributo (como ngClass, ngStyle).

### Bindings de Dados:
- Angular oferece diferentes tipos de bindings para sincronizar dados entre o modelo e a interface do usuário, como interpolação, binding de propriedade, binding de evento, e binding de two-way.

### Ferramentas de Desenvolvimento:
- Angular CLI (Command Line Interface) é uma ferramenta poderosa que ajuda a iniciar, desenvolver e manter aplicações Angular de forma eficiente.

## Diferenças entre Angular e React:
 
### Angular

#### Framework Completo
- Angular é um framework completo que oferece soluções integradas para várias funcionalidades, como roteamento, formulários, injeção de dependência, e comunicação HTTP. Isso significa que, ao usar Angular, você tem uma solução pronta para a maioria das necessidades de desenvolvimento de uma aplicação web.

#### TypeScript
- Angular é baseado em TypeScript, uma linguagem que é um superconjunto de JavaScript. TypeScript oferece tipagem estática, interfaces, e outras funcionalidades avançadas que ajudam a construir aplicações mais robustas e menos propensas a erros.

#### Arquitetura Estruturada
- Angular segue uma arquitetura mais estruturada e opinativa, o que significa que ele impõe certas práticas e padrões de projeto. Isso pode ser benéfico para equipes grandes, pois promove consistência no código.

#### Curva de Aprendizado
- Devido à sua natureza completa e estruturada, Angular pode ter uma curva de aprendizado mais íngreme, especialmente para iniciantes.

### React

#### Biblioteca Focada em UI
- React é uma biblioteca focada na construção de interfaces de usuário. Ele não oferece soluções integradas para funcionalidades como roteamento ou gerenciamento de estado, o que significa que você pode precisar de bibliotecas adicionais (como React Router ou Redux) para essas funcionalidades.

#### JavaScript
- React é baseado em JavaScript, mas também suporta TypeScript. Isso oferece flexibilidade para desenvolvedores que preferem trabalhar com JavaScript puro.

#### Flexibilidade
- React oferece mais flexibilidade e liberdade na escolha de ferramentas e padrões de projeto. Isso pode ser vantajoso para desenvolvedores que preferem personalizar sua stack de tecnologia.

#### Curva de Aprendizado
- React é geralmente considerado mais fácil de aprender para iniciantes, especialmente para aqueles que já estão familiarizados com JavaScript.

## Configuração do Ambiente

- **Instalação do Node.js e Angular CLI:**

  - Node.js é necessário para executar o Angular CLI, que é uma ferramenta de linha de comando para iniciar, desenvolver e manter aplicações Angular.
  - Instale o Node.js a partir do site oficial (https://nodejs.org).
  - Instale o Angular CLI globalmente usando o comando:
    ```bash
    npm install -g @angular/cli
    ```

- **Criação de um novo projeto Angular:**
  - Use o Angular CLI para criar um novo projeto com o comando:
    ```bash
    ng new nome-do-projeto
    ```
  - Este comando configura a estrutura básica do projeto e instala as dependências necessárias.

## Estrutura de um Projeto Angular

- **Módulos, Componentes e Templates:**

  - **Módulos:** São contêineres que agrupam componentes, diretivas, pipes e serviços relacionados. O módulo principal é o `AppModule`. NgModule: Cada módulo é decorado com @NgModule, que define metadados como declarações, importações, provedores e bootstrap.
  - **Componentes:** São os blocos de construção da interface do usuário. Cada componente tem um template, uma classe e um arquivo de estilo. Um componente é definido por uma classe TypeScript decorada com @Component, que especifica o seletor, template e estilos.
  - **Templates:** Definem a interface do usuário e são escritos em HTML. Eles podem incluir bindings e diretivas para interagir com os dados do componente. Bindings: Usados para sincronizar dados entre o modelo e a interface do usuário.

- **Diretivas e Bindings:**
  - **Diretivas:** São instruções no DOM que podem alterar o layout ou comportamento de elementos. Existem três tipos principais: componentes, diretivas estruturais (como `*ngIf`, `*ngFor`) e diretivas de atributo (como `ngClass`, `ngStyle`).
  - **Bindings:** São usados para sincronizar dados entre o modelo e a interface do usuário. Existem diferentes tipos de bindings, como interpolação (`{{ }}`), binding de propriedade (`[property]`), binding de evento (`(event)`), e binding de two-way (`[(ngModel)]`).

- **Serviços e Injeção de Dependência:**
  - **Serviços:** São usados para lógica de negócios que não está diretamente relacionada à interface do usuário, como comunicação com APIs.
  - **Injeção de Dependência:** Angular oferece um sistema de injeção de dependência que facilita a gestão de dependências e promove a modularidade e reutilização de código.

- **Arquivos de Configuração:**
  - angular.json: Configurações do projeto Angular, como caminhos de build e configurações de ambiente.
  - package.json: Lista de dependências do projeto e scripts de build.

Esses fundamentos são essenciais para começar a trabalhar com Angular e entender como a estrutura do framework facilita o desenvolvimento de aplicações web complexas.
