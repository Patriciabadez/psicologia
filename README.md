# PsicologiaSite

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 18.2.7.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.dev/tools/cli) page.
Abaixo está um **guia completo do ZERO**, com **pastas, comandos, telas e CSS**, usando **APENAS AppModule** (sem CoreModule, PagesModule etc.).

---

## 1️⃣ Criar o projeto (do zero)

```bash
ng new psicologia-site \
  --standalone=false \
  --routing=true \
  --style=css
```

Responda:

* SSR/SSG → **NO**

Entre no projeto:

```bash
cd psicologia-site
```

---

## 2️⃣ Criar os componentes (todos no AppModule)

```bash
ng g c header
ng g c footer
ng g c home
ng g c servicos
ng g c sobre
ng g c contato
```

Estrutura final:

```text
src/app/
├── app.module.ts
├── app-routing.module.ts
├── app.component.ts
├── app.component.html
├── app.component.css
│
├── header/
├── footer/
├── home/
├── servicos/
├── sobre/
└── contato/
```

---

## 3️⃣ app.module.ts (TUDO CENTRALIZADO)

```ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppComponent } from './app.component';
import { AppRoutingModule } from './app-routing.module';

import { HeaderComponent } from './header/header.component';
import { FooterComponent } from './footer/footer.component';
import { HomeComponent } from './home/home.component';
import { ServicosComponent } from './servicos/servicos.component';
import { SobreComponent } from './sobre/sobre.component';
import { ContatoComponent } from './contato/contato.component';

@NgModule({
  declarations: [
    AppComponent,
    HeaderComponent,
    FooterComponent,
    HomeComponent,
    ServicosComponent,
    SobreComponent,
    ContatoComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

---

## 4️⃣ app-routing.module.ts

```ts
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

import { HomeComponent } from './home/home.component';
import { ServicosComponent } from './servicos/servicos.component';
import { SobreComponent } from './sobre/sobre.component';
import { ContatoComponent } from './contato/contato.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'servicos', component: ServicosComponent },
  { path: 'sobre', component: SobreComponent },
  { path: 'contato', component: ContatoComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule {}
```

---

## 5️⃣ app.component.html (layout principal)

```html
<app-header></app-header>

<main>
  <router-outlet></router-outlet>
</main>

<app-footer></app-footer>
```

---

## 6️⃣ styles.css (CSS GLOBAL – PREMIUM)

```css
:root {
  --primary: #4a6cf7;
  --secondary: #1f2937;
  --bg: #f9fafb;
  --text: #374151;
  --white: #ffffff;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: 'Inter', Arial, sans-serif;
  background: var(--bg);
  color: var(--text);
}

.container {
  max-width: 1100px;
  margin: auto;
  padding: 40px 20px;
}

.btn {
  background: var(--primary);
  color: white;
  padding: 14px 28px;
  border-radius: 8px;
  font-weight: 600;
  display: inline-block;
}
```

---

## 7️⃣ HEADER

### header.component.html

```html
<header class="header">
  <div class="container header-flex">
    <h1 class="logo">Psicologia & Bem-estar</h1>
    <nav>
      <a routerLink="/">Início</a>
      <a routerLink="/servicos">Atendimentos</a>
      <a routerLink="/sobre">Sobre</a>
      <a routerLink="/contato">Contato</a>
    </nav>
  </div>
</header>
```

### header.component.css

```css
.header {
  background: var(--white);
  box-shadow: 0 2px 8px rgba(0,0,0,.05);
}

.header-flex {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  color: var(--primary);
}

nav a {
  margin-left: 20px;
  font-weight: 500;
}
```

---

## 8️⃣ HOME

### home.component.html

```html
<section class="hero">
  <div class="container hero-grid">
    <div>
      <h2>Cuidar da saúde emocional muda tudo</h2>
      <p>Atendimento psicológico humanizado e acolhedor.</p>
      <a class="btn" href="https://wa.me/55999999999" target="_blank">Agendar pelo WhatsApp</a>
    </div>
    <img src="https://images.unsplash.com/photo-1559027615-5c1c9333c8c0">
  </div>
</section>
```

### home.component.css

```css
.hero-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
}

.hero img {
  width: 100%;
  border-radius: 20px;
}
```

---

## 9️⃣ SERVIÇOS

```html
<div class="container">
  <h2>Atendimentos</h2>
  <div class="cards">
    <div class="card">Terapia Individual</div>
    <div class="card">Terapia de Casal</div>
    <div class="card">Ansiedade</div>
    <div class="card">Autoconhecimento</div>
  </div>
</div>
```

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 20px;
}

.card {
  background: white;
  padding: 30px;
  border-radius: 16px;
}
```

---

## 🔟 SOBRE

```html
<div class="container">
  <h2>Sobre mim</h2>
  <p>Psicóloga clínica com foco em acolhimento e desenvolvimento emocional.</p>
</div>
```

---

## 1️⃣1️⃣ CONTATO

```html
<div class="container">
  <h2>Contato</h2>
  <p>📍 Atendimento online e presencial</p>
  <p>📞 WhatsApp: (99) 99999-9999</p>
</div>
```

---

## 1️⃣2️⃣ FOOTER

```html
<footer class="footer">
  <div class="container">
    <p>© 2025 • Psicologia Clínica • CRP 00/0000</p>
  </div>
</footer>
```

```css
.footer {
  background: var(--secondary);
  color: white;
  text-align: center;
  padding: 20px;
}
```

---

## ✅ FINAL

```bash
ng serve
```

Acesse: [http://localhost:4200](http://localhost:4200)

✔️ Projeto limpo
✔️ Visual premium
✔️ Sem modules extras
✔️ Fácil de evoluir depois

