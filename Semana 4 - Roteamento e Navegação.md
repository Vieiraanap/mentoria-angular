# Semana 4: Roteamento e Navegação

## Introdução ao Roteamento no Angular

- **O que é Roteamento:**
  - Roteamento é o mecanismo que permite a navegação entre diferentes vistas ou componentes em uma aplicação Angular.
  - Ele mapeia URLs para componentes, permitindo que os usuários naveguem pela aplicação.

## Configuração Básica de Rotas

- **Definindo Rotas:**

  - As rotas são definidas em um array de objetos de rota, onde cada objeto especifica um caminho e o componente associado.

  ```typescript
  import { NgModule } from "@angular/core";
  import { RouterModule, Routes } from "@angular/router";
  import { HomeComponent } from "./home/home.component";
  import { AboutComponent } from "./about/about.component";

  const routes: Routes = [
    { path: "", component: HomeComponent },
    { path: "about", component: AboutComponent },
  ];

  @NgModule({
    imports: [RouterModule.forRoot(routes)],
    exports: [RouterModule],
  })
  export class AppRoutingModule {}
  ```

## Parâmetros de Rota

- Parâmetros de rota são usados para passar informações entre componentes. Eles são definidos na configuração de rotas e podem ser acessados através do serviço ActivatedRoute.

- **Passando parâmetros:**

  - **Como passar parâmetros de rota:**

  ```typescript
  const routes: Routes = [{ path: "user/:id", component: UserComponent }];
  ```

  - **Como acessar parâmetros no componente:**

  ```typescript
  import { Component, OnInit } from "@angular/core";
  import { ActivatedRoute } from "@angular/router";

  @Component({
    selector: "app-user",
    template: `<p>User ID: {{ userId }}</p>`,
  })
  export class UserComponent implements OnInit {
    userId: string;

    constructor(private route: ActivatedRoute) {}

    ngOnInit() {
      this.userId = this.route.snapshot.paramMap.get("id");

      this.route.params.subscribe((params) => {
        console.log(params["id"]);
      });
    }
  }
  ```

## Proteção de Rotas com Guards

- Guards são usados para proteger rotas, garantindo que apenas usuários autenticados ou com permissões específicas possam acessá-las.
- CanActivate impede o acesso a uma rota se a condição não for atendida.
- CanDeactivate pode impedir que um usuário saia de uma rota sem salvar alterações.

```typescript
import { Injectable } from "@angular/core";
import {
  CanActivate,
  ActivatedRouteSnapshot,
  RouterStateSnapshot,
  Router,
} from "@angular/router";

@Injectable({
  providedIn: "root",
})
export class AuthGuard implements CanActivate {
  constructor(private router: Router) {}

  canActivate(
    next: ActivatedRouteSnapshot,
    state: RouterStateSnapshot
  ): boolean {
    const isAuthenticated = false; // lógica de autenticação
    if (!isAuthenticated) {
      this.router.navigate(["/login"]);
      return false;
    }
    return true;
  }
}

// Aplicando o guard a uma rota
const routes: Routes = [
  {
    path: "dashboard",
    component: DashboardComponent,
    canActivate: [AuthGuard],
  },
];
```

## Navegação entre rotas

### Navegação via router:

- utilizando router para navegar programaticamente entre rotas, é uma prática comum para controlar o fluxo da aplicação com base em ações do usuário.

```typescript
import { Component } from "@angular/core";
import { Router } from "@angular/router";

@Component({
  selector: "app-navigation",
  template: `<button (click)="goToAbout()">Go to About</button>`,
})
export class NavigationComponent {
  constructor(private router: Router) {}

  goToAbout() {
    this.router.navigate(["/about"]);
  }
}
```

### Métodos do serviço Router

1. **navigate(commands: any[], extras?: NavigationExtras): Promise<boolean>**

- Navega para uma rota específica usando um array de comandos. Você pode passar parâmetros de rota e opções de navegação adicionais.

  ```typescript
  this.router.navigate(["/dashboard", { id: 1 }]);
  ```

2. **navigateByUrl(url: string | UrlTree, extras?: NavigationExtras): Promise<boolean>**

- Navega para uma URL específica. Isso é útil quando você já tem a URL completa ou um UrlTree.

  ```typescript
  this.router.navigateByUrl("/dashboard");
  ```

3. **createUrlTree(commands: any[], extras?: NavigationExtras): UrlTree**

- Cria um UrlTree a partir de um array de comandos e opções de navegação. Isso é útil para manipular URLs sem realmente navegar.

  ```typescript
  const urlTree = this.router.createUrlTree(["/dashboard", { id: 1 }]);
  ```

4. **serializeUrl(url: UrlTree): string**

- Converte um UrlTree em uma string de URL.

  ```typescript
  const urlString = this.router.serializeUrl(urlTree);
  ```

5. **parseUrl(url: string): UrlTree**

- Converte uma string de URL em um UrlTree.

  ```typescript
  const urlTree = this.router.parseUrl("/dashboard?id=1");
  ```

6. **isActive(url: string | UrlTree, exact: boolean): boolean**

- Verifica se a URL atual é ativa. O parâmetro exact determina se a correspondência deve ser exata.

  ```typescript
  const isActive = this.router.isActive("/dashboard", true);
  ```

### Navegação via routerLink:

- Para realizar a navegação a partir do template HTML em uma aplicação Angular, você pode usar a diretiva routerLink. Essa diretiva é usada para vincular elementos HTML a rotas específicas, permitindo que os usuários naveguem clicando em links ou botões. Aqui está um exemplo de como usar o routerLink

```html
<nav>
  <ul>
    <li><a routerLink="/">Home</a></li>
    <li><a routerLink="/about">About</a></li>
    <li><a routerLink="/contact">Contact</a></li>
  </ul>
</nav>

<button [routerLink]="['/dashboard']">Go to Dashboard</button>

<a [routerLink]="['/user', userId]">User Profile</a>
```
