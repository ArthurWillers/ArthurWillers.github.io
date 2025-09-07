---
title: "01. Arquiteturas e Tecnologias"
layout: "docs"
---

Este documento descreve a arquitetura do software Aurum 2.0 e as principais tecnologias utilizadas em seu desenvolvimento.

## Padrão Arquitetural

A aplicação segue o padrão arquitetural **MVC (Model-View-Controller)**, que é o padrão fundamental do framework Laravel. A estrutura do projeto é organizada da seguinte forma:

-   **Models:** Responsáveis pela interação com o banco de dados e pela representação das regras de negócio. Estão localizados em `app/Models`.
-   **Views:** Responsáveis pela camada de apresentação (a interface do usuário). Utilizam a sintaxe do Blade e estão localizadas em `resources/views`.
-   **Controllers:** Atuam como intermediários, recebendo as requisições, processando os dados (com a ajuda dos Models) e enviando as respostas para as Views. Estão localizados em `app/Http/Controllers`.

## Tecnologias do Backend

O backend é o coração da aplicação, responsável por toda a lógica de negócio, segurança e manipulação de dados.

-   **Linguagem:** **PHP 8.2+**
-   **Framework:** **Laravel 12+**
-   **Gerenciador de Pacotes PHP:** **Composer**
-   **Banco de Dados:** A aplicação é compatível com **MySQL**, **PostgreSQL** e **SQLite**, utilizando o ORM Eloquent do Laravel para a abstração do banco.
-   **Autenticação:** O sistema de autenticação (login, registro, recuperação de senha) é gerenciado pelo **Laravel Fortify**, oferecendo uma base segura e customizável.
-   **Servidor Web:** A aplicação é projetada para rodar em servidores como **Nginx** ou **Apache**.

## Tecnologias do Frontend

O frontend é responsável por tudo que o usuário vê e interage no navegador.

-   **Engine de Template: Blade**, o motor de templates nativo do Laravel, usado para construir as views de forma dinâmica.
-   **Framework CSS: Tailwind CSS**, um framework *utility-first* que permite a criação de interfaces customizadas de forma rápida e eficiente.
-   **JavaScript: AlpineJS**, um framework reativo e declarativo que permite adicionar comportamento e interatividade diretamente no HTML.
-   **Build Tool: Vite**, utilizado para compilar e otimizar os assets do frontend (CSS e JavaScript) de forma extremamente rápida.
-   **Gerenciador de Pacotes JS:** **NPM (Node Package Manager)**.