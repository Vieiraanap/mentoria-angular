# Semana 5: Formulários

## Objetivo

O objetivo desta semana é introduzir os conceitos de formulários no Angular e capacitar os participantes a criar e validar formulários reativos e baseados em template.

## Conteúdos

### 1. Introdução aos Formulários no Angular

- Angular oferece duas abordagens principais para a criação de formulários: Reativos e Baseados em Template.
- Formulários Reativos são mais adequados para formulários complexos e dinâmicos, oferecendo um controle mais programático sobre o estado do formulário.
- Formulários Baseados em Template são mais declarativos e integram-se diretamente com o template HTML, sendo ideais para formulários mais simples.

### 2. Formulários Reativos

#### Criação de Formulários Reativos:

- Os formulários reativos no Angular são baseados em uma abordagem programática, onde o estado do formulário é gerenciado no componente TypeScript. Isso oferece um controle mais preciso sobre a validação e o estado do formulário.
- Utiliza `FormGroup`, `FormControl`, e `FormArray` para gerenciar o estado do formulário.

```typescript
// import do ReactiveFormsModule no módulo da aplicação ou módulo do formulário
import { NgModule } from "@angular/core";
import { BrowserModule } from "@angular/platform-browser";
import { ReactiveFormsModule } from "@angular/forms";

@NgModule({
  declarations: [
    /* seus componentes */
  ],
  imports: [
    BrowserModule,
    ReactiveFormsModule, // Importação do ReactiveFormsModule
  ],
  providers: [],
  bootstrap: [
    /* componente principal */
  ],
})
export class AppModule {}
```

1. No componente, você cria uma instância de FormGroup ou FormArray e define os controles do formulário.

```typescript
import { Component } from "@angular/core";
import { FormGroup, FormControl, FormArray, Validators } from "@angular/forms";

@Component({
  selector: "app-user-form",
  template: `
    <form [formGroup]="userForm" (ngSubmit)="onSubmit()">
      <label for="name">Name:</label>
      <input id="name" formControlName="name" />
      <div *ngIf="userForm.get('name').invalid && userForm.get('name').touched">
        Name is required and must be at least 3 characters long.
      </div>

      <label for="email">Email:</label>
      <input id="email" formControlName="email" />
      <div
        *ngIf="userForm.get('email').invalid && userForm.get('email').touched"
      >
        Enter a valid email.
      </div>

      <label for="password">Password:</label>
      <input id="password" type="password" formControlName="password" />
      <div
        *ngIf="
          userForm.get('password').invalid && userForm.get('password').touched
        "
      >
        Password is required and must be at least 6 characters long.
      </div>

      <button type="submit" [disabled]="userForm.invalid">Submit</button>
    </form>
  `,
})
export class UserFormComponent {
  userForm = new FormGroup({
    name: new FormControl("", [Validators.required, Validators.minLength(3)]),
    email: new FormControl("", [Validators.required, Validators.email]),
    password: new FormControl("", [
      Validators.required,
      Validators.minLength(6),
    ]),
  });

  phoneNumbers = new FormArray([new FormControl(""), new FormControl("")]);

  userForm = new FormGroup({
    name: new FormControl(""),
    email: new FormControl(""),
    phoneNumbers: new FormArray([new FormControl(""), new FormControl("")]),
  });

  onSubmit() {
    if (this.userForm.valid) {
      console.log(this.userForm.value);
    }
  }
}
```

2. Utilizando o FormBuild

- O FormBuilder é uma classe auxiliar no Angular que facilita a criação de formulários reativos, tornando o código mais conciso e legível.

```typescript
import { Component } from "@angular/core";
import { FormBuilder, FormGroup, FormArray, Validators } from "@angular/forms";

@Component({
  selector: "app-user-form",
  template: `
    <form [formGroup]="userForm" (ngSubmit)="onSubmit()">
      <label>
        Name:
        <input formControlName="name" />
      </label>
      <label>
        Email:
        <input formControlName="email" />
      </label>
      <div formArrayName="phoneNumbers">
        <div *ngFor="let phone of phoneNumbers().controls; let i = index">
          <label>
            Phone {{ i + 1 }}:
            <input [formControlName]="i" />
          </label>
        </div>
      </div>
      <button type="button" (click)="addPhoneNumber()">Add Phone Number</button>
      <button type="submit">Submit</button>
    </form>
  `,
})
export class UserFormComponent {
  userForm: FormGroup;

  constructor(private fb: FormBuilder) {
    this.userForm = this.fb.group({
      name: ["", Validators.required],
      email: ["", [Validators.required, Validators.email]],
      phoneNumbers: this.fb.array([this.fb.control("")]),
    });
  }

  get phoneNumbers() {
    return this.userForm.get("phoneNumbers") as FormArray;
  }

  addPhoneNumber() {
    this.phoneNumbers.push(this.fb.control(""));
  }

  onSubmit() {
    console.log(this.userForm.value);
  }
}
```

- **Explicação:**
  - FormGroup: Representa o formulário e é um agrupador de FormControl ou outros FormGroup.
  - FormControl: Representa um único campo de entrada no formulário.
  - FormArray: Gerencia um array de FormControl, permitindo um número variável de entradas.
  - Validators: São usados para aplicar validações aos campos do formulário, como required, minLength, e email.

#### Validação de Formulários Reativos:

- A validação de formulários reativos no Angular é feita de forma programática, permitindo um controle mais preciso e flexível sobre as regras de validação.
- Você pode aplicar validações síncronas e assíncronas aos controles do formulário.

## Validações Síncronas

As validações síncronas são aplicadas diretamente aos controles do formulário usando validadores fornecidos pelo Angular ou personalizados.

1. **Validadores Padrão:**

- O Angular fornece vários validadores prontos, como `Validators.required`, `Validators.minLength`, `Validators.maxLength`, `Validators.email`, entre outros.

  ```typescript
  import { FormGroup, FormControl, Validators } from "@angular/forms";

  this.userForm = new FormGroup({
    name: new FormControl("", [Validators.required, Validators.minLength(3)]),
    email: new FormControl("", [Validators.required, Validators.email]),
    password: new FormControl("", [
      Validators.required,
      Validators.minLength(6),
    ]),
  });
  ```

2. **Validadores Personalizados:**

- Você pode criar validadores personalizados para atender a requisitos específicos.

  ```typescript
  import { AbstractControl, ValidationErrors } from '@angular/forms';

  function customValidator(control: AbstractControl): ValidationErrors | null {
    const isValid = /* lógica de validação */;
    return isValid ? null : { customError: true };
  }

  // utilizando no componente
  this.userForm = new FormGroup({
    customField: new FormControl('', [customValidator])
  });
  ```

## Validações Assíncronas

- As validações assíncronas são úteis quando você precisa validar um campo com base em uma operação assíncrona, como uma chamada HTTP.

  ```typescript
  import { AbstractControl, ValidationErrors } from '@angular/forms';
  import { Observable, of } from 'rxjs';
  import { delay, map } from 'rxjs/operators';

  function asyncValidator(control: AbstractControl): Observable<ValidationErrors | null> {
    return of(null).pipe(
      delay(1000), // Simula uma operação assíncrona
      map(() => {
        const isValid = /* lógica de validação */;
        return isValid ? null : { asyncError: true };
      })
    );
  }

  this.userForm = new FormGroup({
    asyncField: new FormControl('', [], [asyncValidator])
  });
  ```

## Exibindo mensagens de erro

- No template, você pode exibir mensagens de erro com base no estado de validação dos controles.

  ```html
  <div *ngIf="userForm.get('name').invalid && userForm.get('name').touched">
    <div *ngIf="userForm.get('name').errors?.required">Name is required.</div>
    <div *ngIf="userForm.get('name').errors?.minlength">
      Name must be at least 3 characters long.
    </div>
  </div>
  ```

### 3. Formulários Baseados em Template

- Os Formulários Baseados em Template no Angular utilizam diretivas para vinculação de dados e validação diretamente no template HTML. Essa abordagem é mais declarativa e pode ser mais intuitiva para desenvolvedores que preferem trabalhar diretamente com o HTML.

- **Criação de Formulários Baseados em Template:**

  - importar o módulo `FormsModule` no seu módulo Angular para habilitar o uso de formulários baseados em template.

  ```typescript
  import { NgModule } from "@angular/core";
  import { BrowserModule } from "@angular/platform-browser";
  import { FormsModule } from "@angular/forms";
  import { AppComponent } from "./app.component";

  @NgModule({
    declarations: [AppComponent],
    imports: [BrowserModule, FormsModule],
    bootstrap: [AppComponent],
  })
  export class AppModule {}
  ```

  - Utilize a diretiva ngModel para vincular dados entre o template e o componente.

  1. **Unidirecional (Somente Leitura):** Quando você usa ngModel sem colchetes, está apenas vinculando o valor do modelo ao elemento de entrada. Isso significa que o valor do modelo é exibido no campo de entrada, mas as alterações feitas no campo de entrada não são refletidas de volta no modelo.

  - Uso Comum: É usado principalmente quando você deseja apenas exibir o valor do modelo no campo de entrada sem a necessidade de atualizar o modelo com as alterações feitas pelo usuário.

  ```html
  <input [ngModel]="userName" />
  ```

  2. **Bidirecional:** O uso de [(ngModel)] cria uma vinculação de dados bidirecional. Isso significa que o valor do modelo é exibido no campo de entrada e qualquer alteração feita no campo de entrada é automaticamente refletida de volta no modelo.

  - Uso Comum: É usado quando você precisa que o modelo seja atualizado com as alterações feitas pelo usuário no campo de entrada. É a forma mais comum de usar ngModel em formulários, pois permite que o modelo e a visão estejam sempre sincronizados.

  ```html
  <input [(ngModel)]="userName" />
  ```

- **Validação de Formulários Baseados em Template:**

  - Aplique validações usando atributos HTML padrão como required, minlength, maxlength, etc.

  ```html
  <form #myForm="ngForm">
    <label for="name">Nome:</label>
    <input id="name" name="name" ngModel required />
    <div
      *ngIf="myForm.controls['name']?.invalid && myForm.controls['name']?.touched"
    >
      O nome é obrigatório.
    </div>

    <button [disabled]="myForm.invalid">Enviar</button>
  </form>
  ```
