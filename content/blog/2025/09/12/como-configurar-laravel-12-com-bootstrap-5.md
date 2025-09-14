---
title: "Como Configurar Laravel 12 Com Bootstrap 5"
date: 2025-09-12T22:44:48-03:00
authors:
  - name: ArthurWillers
    link: https://github.com/ArthurWillers
    image: https://github.com/ArthurWillers.png
---

Neste post, vou compartilhar um passo a passo completo sobre como configurar um projeto Laravel 12 com Bootstrap 5, além do contexto pessoal que me motivou a criar este tutorial.

<!--more-->

## Por que este tutorial?

Minha jornada com Laravel começou durante um projeto de extensão na escola (técnico em informática integrado ao ensino médio), onde desenvolvi um software de gestão de estágios *(repositório privado da instituição)*. Na época, o Laravel já vinha configurado por padrão com [TailwindCSS](https://tailwindcss.com/), mas eu ainda não dominava esse framework e estava muito mais confortável com o [Bootstrap](https://getbootstrap.com/).

Enfrentei então um dilema: **"Como migrar do TailwindCSS para o Bootstrap em um projeto Laravel?"**

Procurei tutoriais sobre essa transição específica, mas não encontrei nada realmente completo ou atualizado. Acabei recorrendo a uma LLM para me ajudar (não lembro qual era na época). Embora possa parecer algo simples hoje, naquele momento foi uma configuração bem chatinha de fazer.

Por isso, decidi documentar todo o processo neste post - tanto para ajudar outros desenvolvedores que possam estar na mesma situação, quanto como uma **anotação pessoal** para quando eu precisar fazer isso novamente.

## Pré-requisitos

Vou considerar que você, leitor, não é um imbecil e já possui conhecimentos básicos de Laravel. Se não souber criar um projeto Laravel, siga a [documentação oficial](https://laravel.com/docs).

## Passo 1: Criando um projeto Laravel limpo

Vamos começar criando um novo projeto Laravel. Abra seu terminal e execute:

```bash {filename="bash"}
composer create-project laravel/laravel meu-projeto-laravel
cd meu-projeto-laravel
```

> Substitua `meu-projeto-laravel` pelo nome que desejar para seu projeto.

Após a instalação, você pode testar se tudo está funcionando executando:

```bash {filename="bash"}
php artisan serve
```

Em outro terminal, execute:

```bash {filename="bash"}
npm run dev
```

Acesse `http://localhost:8000` em seu navegador. Você deve ver a página inicial do Laravel.

## Passo 2: Removendo o TailwindCSS

Antes de instalar o Bootstrap, precisamos remover completamente o TailwindCSS que vem por padrão no Laravel. Vamos fazer uma limpeza completa:

### 2.1. Removendo dependências do TailwindCSS

```bash {filename="bash"}
npm uninstall tailwindcss @tailwindcss/vite
```

### 2.2. Limpando o arquivo CSS

Edite o arquivo `resources/css/app.css` e remova todo o conteúdo relacionado ao Tailwind:

```css {filename="resources/css/app.css"}
/* ANTES (com Tailwind v4) */
@import 'tailwindcss';

@source '../../vendor/laravel/framework/src/Illuminate/Pagination/resources/views/*.blade.php';
@source '../../storage/framework/views/*.php';
@source '../**/*.blade.php';
@source '../**/*.js';

@theme {
    --font-sans: 'Instrument Sans', ui-sans-serif, system-ui, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji',
        'Segoe UI Symbol', 'Noto Color Emoji';
}
```

Deixe o arquivo vazio ou apenas com comentários:

```css {filename="resources/css/app.css"}
/* DEPOIS (limpo) */
/* Aqui vamos importar o Bootstrap */
```

### 2.3. Atualizando o vite.config.js

O Laravel 12 vem com uma configuração específica do TailwindCSS v4. Remova a importação do plugin do Tailwind:

```javascript {filename="vite.config.js"}
/* ANTES (com TailwindCSS v4) */
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import tailwindcss from '@tailwindcss/vite'; // <-- Remover esta linha

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
        tailwindcss(), // <-- Remover esta linha
    ],
});
```

Deixe apenas a configuração básica do Laravel:

```javascript {filename="vite.config.js"}
/* DEPOIS (sem TailwindCSS) */
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
    ],
});
```

### 2.4. Verificando o package.json

Seu `package.json` deve ficar similar a isso após a remoção do TailwindCSS:

```json {filename="package.json"}
{
    "$schema": "https://json.schemastore.org/package.json",
    "private": true,
    "type": "module",
    "scripts": {
        "build": "vite build",
        "dev": "vite"
    },
    "devDependencies": {
        "axios": "^1.11.0",
        "concurrently": "^9.0.1",
        "laravel-vite-plugin": "^2.0.0",
        "vite": "^7.0.4"
    }
}
```

### 2.5. Limpando views (opcional)

A view `welcome.blade.php` que acompanha o Laravel por padrão utiliza classes do TailwindCSS e ficará sem estilo após a remoção do framework. Recomenda-se editar ou substituir esse arquivo para evitar estilos quebrados, adaptando-o para funcionar com Bootstrap ou criando uma nova página inicial conforme sua necessidade.

## Passo 3: Instalando e configurando Bootstrap 5

Agora vamos instalar o Bootstrap 5 e suas dependências. O Laravel 12 usa Vite como bundler, então vamos configurar tudo corretamente.

### 3.1. Instalando as dependências

Execute os seguintes comandos no terminal:

```bash {filename="bash"}
# Instala o Bootstrap e suas dependências
npm install bootstrap @popperjs/core

# Instala o Sass para compilar os estilos
npm install -D sass
```

Após a instalação, seu `package.json` deve ficar similar a isso:

```json {filename="package.json"}
{
    "$schema": "https://json.schemastore.org/package.json",
    "private": true,
    "type": "module",
    "scripts": {
        "build": "vite build",
        "dev": "vite"
    },
    "devDependencies": {
        "axios": "^1.11.0",
        "concurrently": "^9.0.1",
        "laravel-vite-plugin": "^2.0.0",
        "sass": "^1.92.1",
        "vite": "^7.0.4"
    },
    "dependencies": {
        "@popperjs/core": "^2.11.8",
        "bootstrap": "^5.3.8"
    }
}
```

### 3.2. Configurando os arquivos CSS

Vamos modificar o arquivo `resources/css/app.css` para importar o Bootstrap:

> **Importante:** Renomeie o arquivo de `app.css` para `app.scss` para habilitar o Sass:

```bash {filename="bash"}
mv resources/css/app.css resources/css/app.scss
```

```scss {filename="resources/css/app.scss"}
// 1. Customize as variáveis do Bootstrap aqui (opcional)
$primary: #0d6efd;
$secondary: #6c757d;

// 2. Importe o Bootstrap
@import 'bootstrap/scss/bootstrap';

// 3. Adicione seus estilos customizados aqui
.custom-button {
  border-radius: 10px;
  
  &:hover {
    transform: translateY(-2px);
    transition: transform 0.2s ease;
  }
}
```


### 3.3. Configurando o JavaScript

Edite o arquivo `resources/js/app.js` para incluir o Bootstrap:

```javascript {filename="resources/js/app.js"}
import './bootstrap';
import * as bootstrap from 'bootstrap';

// Disponibiliza o Bootstrap globalmente para outros scripts (opcional)
window.bootstrap = bootstrap;
```

### 3.4. Atualizando o Vite config

Certifique-se de que o `vite.config.js` está configurado corretamente (note a mudança de `.css` para `.scss`):

```javascript {filename="vite.config.js"}
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.scss', 'resources/js/app.js'],
            refresh: true,
        }),
    ],
});
```

## Passo 4: Testando a configuração

Vamos criar uma página simples para testar se o Bootstrap está funcionando corretamente.

### 4.1. Criando um layout base

Primeiro, vamos criar um layout base em `resources/views/layouts/app.blade.php`:

```html {filename="resources/views/layouts/app.blade.php"}
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Laravel com Bootstrap</title>
    @vite(['resources/css/app.scss', 'resources/js/app.js'])
</head>
<body>
    @yield('content')
</body>
</html>
```

### 4.2. Criando uma página de teste

Agora, vamos editar a view `resources/views/welcome.blade.php`:

```html {filename="resources/views/welcome.blade.php"}
@extends('layouts.app')

@section('content')
<div class="container mt-5">
    <div class="row">
        <div class="col-md-12">
            <h1 class="display-4 text-primary">Laravel + Bootstrap 5</h1>
            <p class="lead">Configuração funcionando perfeitamente!</p>
            
            <div class="alert alert-success" role="alert">
                <h4 class="alert-heading">Sucesso!</h4>
                <p>O Bootstrap 5 está funcionando corretamente em seu projeto Laravel.</p>
            </div>
            
            <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exemploModal">
                Testar Modal
            </button>
        </div>
    </div>
</div>

<!-- Modal de exemplo -->
<div class="modal fade" id="exemploModal" tabindex="-1" aria-labelledby="exemploModalLabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="exemploModalLabel">Modal de Teste</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                JavaScript do Bootstrap funcionando perfeitamente!
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Fechar</button>
            </div>
        </div>
    </div>
</div>
@endsection
```

### 4.3. Compilando os assets

Execute o comando para compilar os assets:

```bash {filename="bash"}
npm run dev
```

Para desenvolvimento, você pode usar o modo watch:

```bash {filename="bash"}
npm run dev -- --watch
```

Ou para produção:

```bash {filename="bash"}
npm run build
```

## Verificando o resultado

Agora execute o servidor Laravel:

```bash {filename="bash"}
php artisan serve
```

Acesse `http://localhost:8000` em seu navegador. Você deve ver:

- Estilos do Bootstrap aplicados
- Layout responsivo funcionando
- Componentes JavaScript (modal) funcionando

## Extra: Adicionando Bootstrap Icons

Para tornar seu projeto ainda mais completo, você pode adicionar os ícones oficiais do Bootstrap. Os Bootstrap Icons são uma biblioteca gratuita de ícones SVG de alta qualidade.

### Instalando Bootstrap Icons

```bash {filename="bash"}
npm install bootstrap-icons
```

### Configurando no CSS

Adicione a importação dos ícones no seu arquivo `app.scss`:

```scss {filename="resources/css/app.scss"}
// 1. Customize as variáveis do Bootstrap aqui (opcional)
$primary: #0d6efd;
$secondary: #6c757d;

// 2. Importe o Bootstrap
@import 'bootstrap/scss/bootstrap';

// 3. Importe os Bootstrap Icons
@import 'bootstrap-icons/font/bootstrap-icons.css';

// 4. Adicione seus estilos customizados aqui
.custom-button {
  border-radius: 10px;
  
  &:hover {
    transform: translateY(-2px);
    transition: transform 0.2s ease;
  }
}
```

### Usando os ícones

Agora você pode usar os ícones em suas views. Vamos atualizar nossa página de teste:

```html {filename="resources/views/welcome.blade.php"}
@extends('layouts.app')

@section('content')
<div class="container mt-5">
    <div class="row">
        <div class="col-md-12">
            <h1 class="display-4 text-primary">
                <i class="bi bi-bootstrap-fill"></i> Laravel + Bootstrap 5
            </h1>
            <p class="lead">Configuração funcionando perfeitamente!</p>
            
            <div class="alert alert-success" role="alert">
                <h4 class="alert-heading">
                    <i class="bi bi-check-circle-fill"></i> Sucesso!
                </h4>
                <p>O Bootstrap 5 e os ícones estão funcionando corretamente em seu projeto Laravel.</p>
            </div>
            
            <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exemploModal">
                <i class="bi bi-play-circle"></i> Testar Modal
            </button>
            
            <div class="mt-4">
                <h5>Exemplos de ícones:</h5>
                <p>
                    <i class="bi bi-house-fill text-primary"></i> Casa |
                    <i class="bi bi-envelope-fill text-info"></i> Email |
                    <i class="bi bi-telephone-fill text-success"></i> Telefone |
                    <i class="bi bi-gear-fill text-warning"></i> Configurações |
                    <i class="bi bi-heart-fill text-danger"></i> Favorito
                </p>
            </div>
        </div>
    </div>
</div>

<!-- Modal de exemplo -->
<div class="modal fade" id="exemploModal" tabindex="-1" aria-labelledby="exemploModalLabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="exemploModalLabel">
                    <i class="bi bi-chat-dots"></i> Modal de Teste
                </h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                <i class="bi bi-check2-all text-success"></i> JavaScript do Bootstrap funcionando perfeitamente!
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
                    <i class="bi bi-x-circle"></i> Fechar
                </button>
            </div>
        </div>
    </div>
</div>
@endsection
```

### Recursos úteis dos Bootstrap Icons

- **Biblioteca completa**: Mais de 1.800 ícones gratuitos
- **Formatos múltiplos**: SVG, ícone fonts, e sprites
- **Documentação**: [https://icons.getbootstrap.com/](https://icons.getbootstrap.com/)
- **Personalizáveis**: Você pode alterar cor, tamanho e estilo via CSS

### Exemplos de uso avançado

```html
<!-- Ícone com tamanho customizado -->
<i class="bi bi-star-fill" style="font-size: 2rem; color: gold;"></i>

<!-- Ícone como botão -->
<button class="btn btn-outline-primary">
    <i class="bi bi-download"></i> Download
</button>

<!-- Ícone em input -->
<div class="input-group">
    <span class="input-group-text">
        <i class="bi bi-search"></i>
    </span>
    <input type="text" class="form-control" placeholder="Pesquisar...">
</div>
```


## Conclusão

Pronto! Você agora tem um projeto Laravel 12 configurado com Bootstrap 5 funcionando perfeitamente.

Espero que este guia possa ajudar outros desenvolvedores que, assim como eu naquela época, se encontram perdidos entre frameworks e configurações. Às vezes, a melhor ferramenta é simplesmente aquela que você já conhece e domina.