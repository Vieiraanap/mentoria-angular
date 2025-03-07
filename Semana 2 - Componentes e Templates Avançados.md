# Semana 2: Componentes e Templates Avançados

## Componentes Avançados

### Ciclo de Vida dos Componentes:

- Os componentes em Angular possuem um ciclo de vida que é gerenciado por uma série de hooks. Esses hooks permitem que você execute lógica em momentos específicos do ciclo de vida de um componente:

 - ngOnInit: Chamado uma vez após a primeira exibição do componente. Ideal para inicializar dados.
 - ngOnChanges: Chamado quando uma propriedade de entrada (decorada com @Input) é alterada.
 - ngOnDestroy: Chamado antes de o componente ser destruído. Útil para limpar recursos, como assinaturas de observáveis.
 - ngDoCheck: Chamado durante cada ciclo de verificação de mudanças. Útil para detectar e reagir a mudanças que o Angular não detecta automaticamente.
 - ngAfterViewInit: Chamado após a inicialização das visualizações do componente.
 - ngAfterViewChecked: Chamado após cada verificação das visualizações do componente.
 - ngAfterContentInit: Chamado uma vez após a projeção de conteúdo no componente.
 - ngAfterContentChecked: Chamado após cada verificação de conteúdo projetado no componente.

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-example',
  template: '<p>{{message}}</p>',
})
export class ExampleComponent implements OnInit, OnChanges, On {
  message: string;
  @Input() data: string;

  ngOnInit() {
    this.message = 'Componente inicializado!';
  }

  ngOnChanges(changes: SimpleChanges) {
    console.log('Mudanças detectadas:', changes);
    // Reaja às mudanças aqui
  }

  ngOnDestroy() {
    console.log('Componente será destruído');
    // Limpe recursos aqui
  }

  ngDoCheck() {
    console.log('Verificação de mudanças');
    // Verifique mudanças manuais aqui
  }

  ngAfterViewInit() {
    console.log('Visualizações inicializadas');
    // Acesse elementos do DOM aqui
  }
}
```

- Como e quando usar cada um desses hooks para gerenciar o comportamento dos componentes.

### Comunicação entre Componentes:

#### Input e Output Decorators:

- A comunicação entre componentes em Angular é feita principalmente através dos decoradores `@Input` e `@Output`.

- Uso de `@Input()` para passar dados de um componente pai para um componente filho.

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<p>{{childMessage}}</p>',
})
export class ChildComponent {
  @Input() childMessage: string;
}

import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <app-child [childMessage]="parentMessage"></app-child>
  `,
})
export class ParentComponent {
  parentMessage: string = 'Mensagem do componente pai!';
}
```

- Uso de `@Output()` e `EventEmitter` para enviar eventos do componente filho para o componente pai.

```typescript
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: '<button (click)="sendMessage()">Enviar Mensagem</button>',
})
export class ChildComponent {
  @Output() messageEvent = new EventEmitter<string>();

  sendMessage() {
    this.messageEvent.emit('Olá do componente filho!');
  }
}

import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <app-child (messageEvent)="receiveMessage($event)"></app-child>
    <p>{{ message }}</p>
  `,
})
export class ParentComponent {
  message: string;

  receiveMessage(event: string) {
    this.message = event;
  }
}
```

#### ViewChild e ContentChild:

- `@ViewChild()` usado para acessar um elemento filho ou uma diretiva dentro do mesmo componente. Ele permite que você interaja com elementos do DOM ou componentes filhos diretamente no TypeScript.

```typescript
import { Component, ViewChild, AfterViewInit } from '@angular/core';
import { ChildComponent } from './child.component';

@Component({
  selector: 'app-parent',
  template: '<app-child></app-child>',
})
export class ParentComponent implements AfterViewInit {
  @ViewChild(ChildComponent) child: ChildComponent;

  ngAfterViewInit() {
    console.log(this.child.childMessage);
  }
}

import { Component, ViewChild, AfterViewInit, ElementRef } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <h1 #headerElement>Olá, StackSpot!</h1>
    <button (click)="changeHeaderText()">Mudar Texto</button>
  `
})
export class AppComponent implements AfterViewInit {
  @ViewChild('headerElement') header: ElementRef;

  ngAfterViewInit() {
    console.log(this.header.nativeElement.textContent); // Saída: "Olá, StackSpot!"
  }

  changeHeaderText() {
    this.header.nativeElement.textContent = 'Texto Alterado!';
  }
}
```

- `@ContentChild()`  usado para acessar um elemento filho que é passado para um componente através de projeção de conteúdo.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <app-child>
      <p #projectedContent>Este é o conteúdo projetado!</p>
    </app-child>
  `
  // Componente Pai (ParentComponent): Define um elemento <p> com a referência #projectedContent que será projetado no componente filho.
})
export class ParentComponent {}

import { Component, ContentChild, AfterContentInit, ElementRef } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
    <div>
      <ng-content></ng-content>
    </div>
  `
})
export class ChildComponent implements AfterContentInit {
  // Componente Filho (ChildComponent): Usa @ContentChild('projectedContent') para acessar o elemento projetado. O ngAfterContentInit é um ciclo de vida que é chamado após o conteúdo ser projetado, permitindo que você interaja com o conteúdo projetado.
  @ContentChild('projectedContent') content: ElementRef;

  ngAfterContentInit() {
    console.log(this.content.nativeElement.textContent); // Saída: "Este é o conteúdo projetado!"
  }
}
```

## Templates Avançados

### Diretivas

As diretivas no Angular são classes que podem modificar o comportamento ou o layout de elementos no DOM. Existem três tipos principais de diretivas:

#### Diretivas de Componente

- São as mais comuns e incluem um template. Todo componente no Angular é uma diretiva de componente.

#### Diretivas de Atributo

- Alteram a aparência ou comportamento de um elemento, componente ou outra diretiva. Exemplos incluem `ngClass` e `ngStyle`.
- Você pode criar diretivas de atributo personalizadas para aplicar comportamentos específicos a elementos.

#### Exemplo de Diretiva de Atributo

```typescript
import { Directive, ElementRef, Renderer2, HostListener } from "@angular/core";

@Directive({
  selector: "[appHighlight]",
})
export class HighlightDirective {
  constructor(private el: ElementRef, private renderer: Renderer2) {}

  @HostListener("mouseenter") onMouseEnter() {
    this.renderer.setStyle(this.el.nativeElement, "backgroundColor", "yellow");
  }

  @HostListener("mouseleave") onMouseLeave() {
    this.renderer.setStyle(this.el.nativeElement, "backgroundColor", "white");
  }
}
```

#### Diretivas Estruturais

- Alteram a estrutura do DOM, adicionando ou removendo elementos. Exemplos incluem `*ngIf`, `*ngFor`, e `*ngSwitch`.
- Você também pode criar diretivas estruturais personalizadas.

```html
<div *ngIf="isVisible">
  Este conteúdo só será exibido se isVisible for true.
</div>

<ul>
  <li *ngFor="let item of items">
    {{ item }}
  </li>
</ul>

<div [ngSwitch]="color">
  <div *ngSwitchCase="'red'">Cor Vermelha</div>
  <div *ngSwitchCase="'blue'">Cor Azul</div>
  <div *ngSwitchDefault>Cor Desconhecida</div>
</div>
```

### Pipes

- Pipes são usados para transformar dados em templates. Angular fornece vários pipes embutidos, como `DatePipe`, `CurrencyPipe`, `DecimalPipe`, entre outros.

#### Exemplo DatePipe

- Por padrão, o DatePipe formata a data no formato mediumDate. Você pode especificar diferentes formatos de data, como shortDate, fullDate, ou até mesmo um formato personalizado.
  
```html
<p>Data atual: {{ today | date }}</p>

<!-- outros formatos de data -->
<p>Data curta: {{ today | date:'shortDate' }}</p>
<p>Data completa: {{ today | date:'fullDate' }}</p>
<p>Data e hora: {{ today | date:'medium' }}</p>
<p>Formato personalizado: {{ today | date:'dd/MM/yyyy' }}</p>
```

- Se você quiser usar um locale específico, como pt-BR, você pode configurá-lo no seu módulo:
  
```typescript
import { NgModule, LOCALE_ID } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { registerLocaleData } from '@angular/common';
import localePt from '@angular/common/locales/pt';

registerLocaleData(localePt);

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  providers: [{ provide: LOCALE_ID, useValue: 'pt-BR' }],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

- Você também pode criar pipes personalizados.

#### Pipe Personalizado

- Um pipe personalizado pode ser criado para transformar dados de acordo com suas necessidades específicas.

#### Exemplo de Pipe Personalizado

1. criar o pipe: `ng generate pipe uppercase`
- Isso criará dois arquivos: `uppercase.pipe.ts` e `uppercase.pipe.spec.ts`. Abra o arquivo `uppercase.pipe.ts` e implemente o método transform:

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'uppercase'
})
export class UppercasePipe implements PipeTransform {
  transform(value: string): string {
    return value.toUpperCase();
  }
}

import { Pipe, PipeTransform } from "@angular/core";

@Pipe({
  name: "exclamation",
})
export class ExclamationPipe implements PipeTransform {
  transform(value: string, ...args: unknown[]): string {
    return value + "!";
  }
}

```

2.  Registrar o Pipe no Módulo
- Certifique-se de que o pipe está registrado no módulo Angular. No arquivo app.module.ts, adicione o UppercasePipe ao array de declarações:

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { UppercasePipe } from './uppercase.pipe'; // Importe o pipe

@NgModule({
  declarations: [
    AppComponent,
    UppercasePipe // Declare o pipe aqui
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

3. Usar no componente:
- Agora, você pode usar o pipe no seu componente Angular. Vamos supor que você tem um componente chamado app.component.ts e deseja usar o pipe no template HTML.

```html
<p>{{ 'hello world' | uppercase }}</p> <!-- HELLO WORD -->
<p>{{ 'hello world' | uppercase | exclamation }}</p> <!-- HELLO WORD! -->
```

## Outras Estruturas no Angular

### Serviços

- Usados para lógica de negócios que pode ser compartilhada entre componentes. Serviços são criados e injetados em componentes através do sistema de injeção de dependência do Angular.

```typescript
import { Injectable } from "@angular/core";

@Injectable({
  providedIn: "root",
})
export class DataService {
  getData() {
    return ["data1", "data2", "data3"];
  }
}
```

### Módulos

- Agrupam componentes, diretivas, pipes e serviços relacionados. O módulo principal é o AppModule, mas você pode criar módulos adicionais para organizar melhor a aplicação.

```typescript
import { NgModule } from "@angular/core";
import { CommonModule } from "@angular/common";
import { MyComponent } from "./my-component/my-component.component";

@NgModule({
  declarations: [MyComponent],
  imports: [CommonModule],
  exports: [MyComponent],
})
export class MyModule {}
```

### Módulo de Roteamento

```typescript
import { NgModule } from "@angular/core";
import { RouterModule, Routes } from "@angular/router";
import { HomeComponent } from "./home/home.component";
import { AboutComponent } from "./about/about.component";

const routes: Routes = [
  { path: "produto/:id", component: HomeComponent, guards: [AuthGuard, guard], child: [
    { path: "about", component: AboutComponent, guar},
    { path: "about", component: AboutComponent },
    { path: "about", component: AboutComponent },

  ] }, //123
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

### Resolvers

- são usados no Angular para pré-carregar dados antes de ativar uma rota. Isso é útil quando você precisa garantir que certos dados estejam disponíveis antes de exibir um componente. (Pré-carrega dados antes de ativar uma rota.)

- Como criar um resolver:

```typescript
import { Injectable } from "@angular/core";
import {
  Resolve,
  ActivatedRouteSnapshot,
  RouterStateSnapshot,
} from "@angular/router";
import { Observable, of } from "rxjs";
import { DataService } from "./data.service";

@Injectable({
  providedIn: "root",
})
export class DataResolver implements Resolve<any> {
  constructor(private dataService: DataService) {}

  resolve(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot
  ): Observable<any> {
    return this.dataService.getData();
  }
}
```

- Como usar um Resolver em uma rota:

```typescript
import { NgModule } from "@angular/core";
import { RouterModule, Routes } from "@angular/router";
import { MyComponent } from "./my-component/my-component.component";
import { DataResolver } from "./data.resolver";

const routes: Routes = [
  {
    path: "my-path",
    component: MyComponent,
    resolve: {
      data: DataResolver,
    },
  },
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

### Interceptors

- são usados para interceptar e manipular requisições HTTP ou respostas no Angular. Eles são úteis para adicionar cabeçalhos, manipular erros, ou fazer logging de requisições.
- Essas estruturas são poderosas para gerenciar dados e requisições em aplicações Angular, permitindo um controle mais refinado sobre o fluxo de dados e a comunicação com APIs.

- Como criar um interceptor:

```typescript
import { Injectable } from "@angular/core";
import {
  HttpInterceptor,
  HttpRequest,
  HttpHandler,
  HttpEvent,
} from "@angular/common/http";
import { Observable } from "rxjs";

@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  intercept(
    req: HttpRequest<any>,
    next: HttpHandler
  ): Observable<HttpEvent<any>> {
    const clonedRequest = req.clone({
      headers: req.headers.set("Authorization", "Bearer YOUR_TOKEN_HERE"),
    });
    return next.handle(clonedRequest);
  }
}
```

- Como fornecer um interceptor:

```typescript
import { HTTP_INTERCEPTORS } from "@angular/common/http";
import { AuthInterceptor } from "./auth.interceptor";

@NgModule({
  providers: [
    { provide: HTTP_INTERCEPTORS, useClass: AuthInterceptor, multi: true },
  ],
})
export class AppModule {}
```

### Providers

- No Angular, "providers" são uma parte fundamental do sistema de injeção de dependência. Eles são responsáveis por informar ao Angular como criar e entregar uma dependência quando ela é solicitada.


1. O que é um Provider?

- Um provider é uma instrução para o Angular sobre como criar uma instância de uma dependência. Ele define como o serviço ou valor deve ser instanciado.


2. Tipos de Providers:

- **Class Provider:** Usa uma classe para criar a dependência.

```typescript
{ provide: MyService, useClass: MyService }
```

- **Value Provider:** Usa um valor estático como a dependência.

```typescript
{ provide: 'API_URL', useValue: 'https://api.example.com' }
```

- **Factory Provider:** Usa uma função de fábrica para criar a dependência.

```typescript
{ provide: MyService, useFactory: myFactoryFunction }
```

- **Existing Provider:** Usa um serviço existente como a dependência.

```typescript
{ provide: NewService, useExisting: OldService }
```

3. Onde Declarar Providers:

- **Módulo (app.module.ts):** Providers declarados aqui são singletons e estão disponíveis em toda a aplicação.
- **Componente:** Providers declarados em um componente são únicos para cada instância do componente.

4. Porquê utilizar:

- **Injeção de Dependência:** Providers permitem que você injete dependências em componentes, serviços e outras partes da aplicação de forma eficiente e controlada. Isso promove um design de código mais modular e testável. Quando um componente ou serviço precisa de uma dependência, ele declara isso em seu construtor, e o Angular injeta a dependência automaticamente.
- **Gerenciamento de Instâncias:** Com providers, você pode controlar como e quando as instâncias dos serviços são criadas. Por exemplo, você pode definir um serviço como singleton (uma única instância para toda a aplicação) ou criar uma nova instância para cada componente.
- **Flexibilidade:** Providers oferecem flexibilidade para substituir implementações de serviços sem alterar o código que depende desses serviços. Isso é útil para testes, onde você pode substituir um serviço real por um mock.
- **Configuração Centralizada:** Ao usar providers, você pode configurar e gerenciar dependências de forma centralizada, geralmente no módulo principal da aplicação, o que facilita a manutenção e a escalabilidade do código.
- **Hierarquia de Injeção:** O Angular usa uma hierarquia de injeção, o que significa que você pode ter diferentes instâncias de um serviço em diferentes partes da aplicação, dependendo de onde o provider é declarado.

### Guards

- são usados para controlar o acesso a rotas em uma aplicação. Eles permitem que você defina condições que devem ser atendidas antes de uma rota ser ativada ou desativada. Existem quatro tipos principais de guards no Angular.
- Os guards são uma parte essencial do roteamento no Angular, permitindo que você implemente lógica de navegação complexa e proteja suas rotas de acesso não autorizado.

1. CanActivate: Usado para impedir que uma rota seja ativada. Por exemplo, você pode usar CanActivate para proteger rotas que requerem autenticação. (Impede que uma rota seja ativada.)

```typescript
import { Injectable } from "@angular/core";
import {
  CanActivate,
  ActivatedRouteSnapshot,
  RouterStateSnapshot,
} from "@angular/router";
import { AuthService } from "./auth.service";

@Injectable({
  providedIn: "root",
})
export class AuthGuard implements CanActivate {
  constructor(private authService: AuthService) {}

  canActivate(
    next: ActivatedRouteSnapshot,
    state: RouterStateSnapshot
  ): boolean {
    return this.authService.isAuthenticated();
  }
}
```

2. CanActivateChild: Similar ao CanActivate, mas é usado para proteger rotas filhas. Se um CanActivateChild guard estiver em uma rota pai, ele será executado sempre que qualquer rota filha for ativada. (Protege rotas filhas.)

```typescript
import { Injectable } from "@angular/core";
import {
  CanActivateChild,
  ActivatedRouteSnapshot,
  RouterStateSnapshot,
  UrlTree,
} from "@angular/router";
import { Observable } from "rxjs";
import { AuthService } from "./auth.service";

@Injectable({
  providedIn: "root",
})
export class AuthChildGuard implements CanActivateChild {
  constructor(private authService: AuthService) {}

  canActivateChild(
    childRoute: ActivatedRouteSnapshot,
    state: RouterStateSnapshot
  ):
    | Observable<boolean | UrlTree>
    | Promise<boolean | UrlTree>
    | boolean
    | UrlTree {
    // Aqui você pode implementar a lógica para verificar se o usuário tem permissão
    // para acessar as rotas filhas. Por exemplo, verificar se o usuário está autenticado.
    return this.authService.isAuthenticated();
  }
}
```

3. CanDeactivate: Usado para impedir que o usuário saia de uma rota. Isso é útil para alertar o usuário sobre mudanças não salvas em um formulário, por exemplo. (Impede que o usuário saia de uma rota.)

```typescript
import { Injectable } from "@angular/core";
import { CanDeactivate } from "@angular/router";
import { Observable } from "rxjs";

export interface CanComponentDeactivate {
  canDeactivate: () => Observable<boolean> | Promise<boolean> | boolean;
}

@Injectable({
  providedIn: "root",
})
export class CanDeactivateGuard
  implements CanDeactivate<CanComponentDeactivate>
{
  canDeactivate(
    component: CanComponentDeactivate
  ): Observable<boolean> | Promise<boolean> | boolean {
    return component.canDeactivate ? component.canDeactivate() : true;
  }
}
```
