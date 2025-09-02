---
title: "Hello, World!"
layout: hextra-home
---

{{< hextra/hero-badge >}}
  <div class="hx:w-2 hx:h-2 hx:rounded-full hx:bg-primary-400"></div>
  <span>Bem-vindo ao meu espaço!</span>
{{< /hextra/hero-badge >}}

<div class="hx:mt-6 hx:mb-6">
{{< hextra/hero-headline >}}
  Hello, World!
{{< /hextra/hero-headline >}}
</div>

<div class="hx:mb-6">
{{< hextra/hero-subtitle >}}
  Um espaço onde escrevo sobre coisas.
{{< /hextra/hero-subtitle >}}
</div>

<div class="hx:mt-6"></div>

{{< hextra/feature-grid >}}
  {{< hextra/feature-card
    title="Sobre Mim"
    subtitle="Um pouco sobre minha jornada e interesses."
    icon="user"
    link="/about"
    class="hx:min-h-[280px]"
    style="background: radial-gradient(ellipse at 50% 80%,rgba(194,97,254,0.1),hsla(0,0%,100%,0));"
  >}}
  {{< hextra/feature-card
    title="Projetos"
    subtitle="Explore os projetos em que estou trabalhando."
    icon="briefcase"
    link="/docs"
    class="hx:min-h-[280px]"
    style="background: radial-gradient(ellipse at 50% 80%,rgba(59,130,246,0.1),hsla(0,0%,100%,0));"
  >}}
  {{< hextra/feature-card
    title="Blog"
    subtitle="Meus artigos sobre... sobre."
    icon="book-open"
    link="/blog"
    class="hx:min-h-[280px]"
    style="background: radial-gradient(ellipse at 50% 80%,rgba(16,185,129,0.1),hsla(0,0%,100%,0));"
  >}}
{{< /hextra/feature-grid >}}