# Semana 3: Serviços e Injeção de Dependência

## Introdução aos Serviços

- **O que são Serviços no Angular:**

  - Serviços são classes que encapsulam lógica de negócios, dados ou funcionalidades que podem ser compartilhadas entre diferentes componentes de uma aplicação Angular.
  - Eles ajudam a manter o código modular e reutilizável, separando a lógica de negócios da lógica de apresentação.

- **Criação de um Serviço:**
  - Você pode criar um serviço usando o Angular CLI com o comando:
    ```bash
    ng generate service nome-do-servico
    ```
  - Isso gera um arquivo de serviço básico que pode ser modificado para incluir a lógica necessária.

## Injeção de Dependência

- **O que é Injeção de Dependência:**

  - É um padrão de design que permite que uma classe receba suas dependências de fontes externas em vez de criá-las internamente.
  - No Angular, o sistema de injeção de dependência é usado para fornecer instâncias de serviços para componentes e outros serviços.

- **Como funciona a Injeção de Dependência no Angular:**

  - O Angular usa um injetor para manter um contêiner de dependências que podem ser injetadas em componentes e serviços.
  - As dependências são especificadas no construtor da classe, e o Angular cuida de instanciá-las e fornecê-las.

- **Fornecendo Serviços:**

  - Serviços podem ser fornecidos em diferentes níveis:
    - **Raiz (Root):** O serviço é singleton e está disponível em toda a aplicação.
    - **Módulo:** O serviço é singleton dentro do módulo onde é fornecido.
    - **Componente:** O serviço é instanciado para cada instância do componente.

- **Exemplo de Injeção de Dependência:**

  - Aqui está um exemplo de como injetar um serviço em um componente:

    ```typescript
    import { Component, OnInit } from "@angular/core";
    import { MeuServico } from "./meu-servico.service";

    @Component({
      selector: "app-meu-componente",
      templateUrl: "./meu-componente.component.html",
      styleUrls: ["./meu-componente.component.css"],
    })
    export class MeuComponente implements OnInit {
      constructor(private meuServico: MeuServico) {}

      ngOnInit(): void {
        this.meuServico.fazerAlgo();
      }
    }
    ```

## HttpClient

- **
  O que é HttpClient:
  **

  - HttpClient é um serviço Angular que facilita a comunicação com servidores HTTP para realizar operações como GET, POST, PUT, DELETE, etc.
  - Ele é parte do módulo `HttpClientModule`, que deve ser importado no módulo principal da aplicação.

- **
  Como usar HttpClient:
  **

  - Primeiro, importe o `HttpClientModule` no seu módulo:

    ```typescript
    import { HttpClientModule } from "@angular/common/http";

    @NgModule({
      declarations: [
        /* seus componentes */
      ],
      imports: [
        HttpClientModule,
        /* outros módulos */
      ],
      providers: [],
      bootstrap: [
        /* componente principal */
      ],
    })
    export class AppModule {}
    ```

  - Em seguida, injete o `HttpClient` no seu serviço:

    ```typescript
    import { Injectable } from "@angular/core";
    import { HttpClient } from "@angular/common/http";
    import { Observable } from "rxjs";

    @Injectable({
      providedIn: "root",
    })
    export class ApiService {
      private apiUrl = "https://api.exemplo.com/dados";

      constructor(private http: HttpClient) {}

      getDados(): Observable<any> {
        return this.http.get<any>(this.apiUrl);
      }
    }
    ```

- **
  Exemplo de uso do HttpClient em um componente:
  **

  - Aqui está um exemplo de como usar o serviço `ApiService` em um componente:

    ```typescript
    import { Component, OnInit } from "@angular/core";
    import { ApiService } from "./api.service";

    @Component({
      selector: "app-dados",
      templateUrl: "./dados.component.html",
      styleUrls: ["./dados.component.css"],
    })
    export class DadosComponent implements OnInit {
      dados: any;

      constructor(private apiService: ApiService) {}

      ngOnInit(): void {
        this.apiService.getDados().subscribe((data) => {
          this.dados = data;
        });
      }
    }
    ```

## RxJS

### O que é RxJS?

RxJS (Reactive Extensions for JavaScript) é uma biblioteca para programação reativa usando Observables, que facilita a composição de código assíncrono ou baseado em eventos. É uma parte essencial do ecossistema Angular, mas também pode ser usada em outros frameworks ou bibliotecas JavaScript.

### Principais Conceitos do RxJS:

- **Observable:** Representa uma coleção de valores ou eventos futuros. É a base para a programação reativa no Angular.
- **Observer:** É um conjunto de callbacks que sabe ouvir valores entregues por um Observable.
- **Operators:** São funções que permitem manipular coleções de valores emitidos por Observables. Exemplos incluem `map`, `filter`, `mergeMap`, etc.
- **Subscription:** Representa a execução de um Observable. É usado para cancelar a execução de um Observable.
- **Subject:** É um tipo especial de Observable que permite multicasting para múltiplos Observers.

```typescript
import { Observable, Observer, Subject } from "rxjs";
import { map, filter } from "rxjs/operators";

// **Observable**: Cria um Observable que emite uma sequência de números
const numberObservable = new Observable<number>((subscriber) => {
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
  subscriber.complete();
});

// **Observer**: Define um conjunto de callbacks para lidar com os valores emitidos pelo Observable
const numberObserver: Observer<number> = {
  next: (value) => console.log(`Observer recebeu: ${value}`),
  error: (err) => console.error(`Erro: ${err}`),
  complete: () => console.log("Observable completo"),
};

// **Operators**: Usa operadores para transformar os valores emitidos pelo Observable
const processedNumbers$ = numberObservable.pipe(
  filter((n) => n % 2 !== 0), // Filtra apenas números ímpares
  map((n) => n * 10) // Multiplica cada número por 10
);

// **Subscription**: Assina o Observable e começa a receber valores
const subscription = processedNumbers$.subscribe(numberObserver);

// **Subject**: Cria um Subject que pode emitir valores para múltiplos Observers
const numberSubject = new Subject<number>();

// Assina o Subject com dois Observers diferentes
numberSubject.subscribe((value) => console.log(`Observer 1: ${value}`));
numberSubject.subscribe((value) => console.log(`Observer 2: ${value}`));

// Emite valores através do Subject
numberSubject.next(10);
numberSubject.next(20);

// Cancela a assinatura do Observable
subscription.unsubscribe();
```

- **Explicação:**

  - Observable: Criamos um Observable que emite uma sequência de números (1, 2, 3).
  - Observer: Definimos um Observer que sabe como lidar com os valores emitidos pelo Observable.
  - Operators: Usamos filter para permitir apenas números ímpares e map para multiplicar cada número por 10.
  - Subscription: Assinamos o Observable para começar a receber valores e, em seguida, cancelamos a assinatura.
  - Subject: Criamos um Subject que permite emitir valores para múltiplos Observers, demonstrando o conceito de multicasting.

#### Observable x Subject

- **Observable**
  - Definição: Um Observable é uma fonte de dados que pode emitir uma sequência de valores ao longo do tempo. Ele é "frio" por padrão, o que significa que ele não começa a emitir valores até que alguém se inscreva nele.
  - Uso: É usado para representar fluxos de dados que são produzidos de forma assíncrona, como eventos de usuário, requisições HTTP, etc.
  - Assinatura: Cada vez que um Observable é assinado, ele cria uma nova execução do fluxo de dados. Isso significa que cada assinante recebe sua própria sequência de valores.
- **Subject**

  - Definição: Um Subject é um tipo especial de Observable que permite multicasting, ou seja, ele pode emitir valores para múltiplos Observers ao mesmo tempo. Ele é "quente", pois começa a emitir valores assim que eles são produzidos, independentemente de haver assinantes.
  - Uso: É usado quando você precisa de um ponto central para emitir valores para múltiplos assinantes, como em eventos de interface do usuário ou quando você precisa compartilhar um fluxo de dados entre diferentes partes de um aplicativo.
  - Assinatura: Todos os assinantes de um Subject compartilham a mesma execução do fluxo de dados, recebendo os mesmos valores emitidos.

- **Exemplo:**

```typescript
import { Observable, Subject } from "rxjs";

// Observable: Cada assinante recebe sua própria sequência de valores
const observable = new Observable<number>((subscriber) => {
  subscriber.next(Math.random()); // Emite um número aleatório
  subscriber.complete();
});

observable.subscribe((value) => console.log(`Observable 1: ${value}`));
observable.subscribe((value) => console.log(`Observable 2: ${value}`));

// Subject: Todos os assinantes recebem a mesma sequência de valores
const subject = new Subject<number>();

subject.subscribe((value) => console.log(`Subject 1: ${value}`));
subject.subscribe((value) => console.log(`Subject 2: ${value}`));

subject.next(Math.random()); // Emite um número aleatório
```

- **Explicação**
  - No exemplo do Observable, cada assinatura recebe um número aleatório diferente, pois cada assinatura cria uma nova execução.
  - No exemplo do Subject, ambos os assinantes recebem o mesmo número aleatório, pois o Subject emite o valor para todos os seus assinantes ao mesmo tempo.

### Por que usar RxJS?

RxJS é usado para lidar com operações assíncronas de forma mais eficiente e elegante. Ele permite que você trabalhe com fluxos de dados assíncronos, como eventos de usuário, requisições HTTP, ou qualquer outra operação que não seja síncrona, de uma maneira mais declarativa.

### Benefícios do uso de RxJS

1. **Composição de Fluxos de Dados:**

   - RxJS permite compor fluxos de dados complexos de maneira simples e declarativa. Você pode combinar, filtrar, transformar e manipular fluxos de dados com facilidade.

2. **Tratamento de Erros:**

   - Com operadores como `catchError`, você pode interceptar e tratar erros de forma centralizada, melhorando a robustez do seu código.

3. **Concorrência e Assincronismo:**

   - RxJS facilita o trabalho com operações assíncronas e concorrentes, permitindo que você lide com múltiplas operações ao mesmo tempo sem complicações.

4. **Operadores Poderosos:**

   - RxJS oferece uma vasta gama de operadores que permitem manipular fluxos de dados de várias maneiras, como `map`, `filter`, `merge`, `switchMap`, entre outros.

5. **Facilidade de Testes:**

   - A programação reativa com RxJS pode tornar o código mais fácil de testar, pois você pode simular fluxos de dados e verificar como seu código reage a diferentes cenários.

6. **Integração com Angular:**
   - No Angular, RxJS é amplamente utilizado para lidar com requisições HTTP, eventos de formulário, e outras operações assíncronas, tornando-se uma ferramenta essencial para desenvolvedores Angular.

### Exemplo de Uso

Aqui está um exemplo simples de como RxJS pode ser usado para tratar erros em uma requisição HTTP no Angular:

```typescript
import { HttpClient, HttpErrorResponse } from '@angular/common/http';
import { catchError } from 'rxjs/operators';
import { throwError } from 'rxjs';

constructor(private http: HttpClient) { }

getData() {
  return this.http.get('https://api.exemplo.com/dados')
    .pipe(
      catchError(this.handleError)
    );
}

private handleError(error: HttpErrorResponse) {
  let errorMessage = '';
  if (error.error instanceof ErrorEvent) {
    // Erro no lado do cliente
    errorMessage = `Erro: ${error.error.message}`;
  } else {
    // Erro no lado do servidor
    errorMessage = `Código do erro: ${error.status}\nMensagem: ${error.message}`;
  }
  console.error(errorMessage);
  return throwError('Algo deu errado; por favor, tente novamente mais tarde.');
}
```

- Neste exemplo, o operador catchError é usado para capturar e tratar erros que ocorrem durante a requisição HTTP, demonstrando como RxJS pode simplificar o tratamento de erros em operações assíncronas.

- O operador pipe no RxJS é usado para encadear múltiplos operadores de forma legível e organizada. Ele permite que você aplique uma sequência de operações a um Observable, transformando ou filtrando os dados que ele emite. O pipe é essencial para a composição de operadores, tornando o código mais modular e fácil de entender.

```typescript
import { of } from "rxjs";
import { map, filter } from "rxjs/operators";

// Cria um Observable que emite uma sequência de números
const numbers$ = of(1, 2, 3, 4, 5);

// Usa o pipe para encadear operadores
const processedNumbers$ = numbers$.pipe(
  filter((n) => n % 2 === 0), // Filtra apenas números pares
  map((n) => n * 10) // Multiplica cada número por 10
);

// Assina o Observable e imprime os valores processados
processedNumbers$.subscribe((value) => console.log(value));
```

## Considerações Finais

- **Benefícios dos Serviços e Injeção de Dependência:**

  - Promovem a reutilização de código e a separação de preocupações.
  - Facilitam o teste de unidades, pois as dependências podem ser facilmente mockadas.
  - Melhoram a manutenção e escalabilidade da aplicação.

- **Práticas Recomendadas:**

  - Sempre que possível, use serviços para lógica de negócios e acesso a dados.
  - Evite criar instâncias de serviços diretamente; use a injeção de dependência para gerenciar dependências.
  - Considere o escopo adequado para seus serviços (raiz, módulo ou componente) para otimizar o uso de recursos.

Compreender e aplicar corretamente os conceitos de serviços e injeção de dependência é crucial para o desenvolvimento eficiente de aplicações Angular.

- **Benefícios do RxJS:**

  - Facilita o tratamento de operações assíncronas e baseadas em eventos.
  - Permite a composição de operações complexas de forma declarativa.
  - Integra-se perfeitamente com o Angular, especialmente em serviços e componentes.

- **Práticas Recomendadas:**

  - Use operadores do RxJS para manipular dados de forma eficiente.
  - Sempre trate erros em streams de Observables para evitar falhas silenciosas.
  - Utilize Subjects e BehaviorSubjects para comunicação entre componentes quando necessário.

Compreender e aplicar corretamente os conceitos de RxJS é crucial para o desenvolvimento eficiente de aplicações Angular, especialmente ao lidar com operações assíncronas e comunicação entre componentes.

```

```
