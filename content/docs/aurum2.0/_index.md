---
title: "Aurum2.0"
layout: "docs"
---

O Aurum2.0 é um software de gestão financeira pessoal que estou desenvolvendo para resolver problemas que encontro em soluções existentes. A maioria dos softwares disponíveis são confusos, não atendem meus critérios de organização ou são pagos (assinaturas).

Existem muitos softwares desse tipo, um deles é o [Maybe Finance](https://github.com/maybe-finance/maybe), porém ele é focado para rodar localmente com apenas um usuário (é possível ter mais usuários, mas todos compartilham o mesmo controle).

## Por que Aurum2.0? Onde está o 1.0?

Você pode estar se perguntando: "Se esse é o 2.0, cadê o 1.0?" 

Bom, ele existe e está disponível no meu GitHub: [Aurum v1.0](https://github.com/ArthurWillers/Aurum). A primeira versão foi desenvolvida usando um Starter Kit do Laravel com TALL Stack, onde a principal diferença é o Livewire. Escolhi esse kit para acelerar o desenvolvimento, já que vinha com views prontas e utilizava FluxUI, uma biblioteca incrível de componentes Blade preparados para Livewire.

### O Problema da Primeira Versão

Eu queria acelerar ao máximo o desenvolvimento porque estava de férias e precisava começar a usar na semana seguinte - e consegui! Mas a que custo?

Acabei utilizando muita IA generativa (LLMs) para desenvolvê-lo, o que resultou em muitas "gambiarras". Não considero algo bem feito e que foi efetivamente desenvolvido por mim.

### O Desafio dos Gráficos

Além disso, eu queria implementar gráficos interativos. As principais bibliotecas para isso são Chart.js e ApexCharts.js, mas ambas tinham um problema fundamental: a incompatibilidade com a atualização dinâmica do Livewire.

**O problema específico:**
- Quando o usuário mudava o mês, os dados atualizavam no front-end
- A página não recarregava (comportamento esperado do Livewire)
- **MAS** os dados dos gráficos não atualizavam
- Os gráficos só mudavam se a página fosse manualmente recarregada

Gastei bastante tempo tentando resolver isso, mas não consegui encontrar uma solução (talvez por ser algo "complexo", ou porque eu sou muito burro).

### A Solução Temporária

Contornei o problema implementando um gráfico de barras simples que mostra:
- As 3 categorias com mais despesas
- As 3 categorias com mais receitas

## Aurum2.0: A Nova Versão

A versão 2.0 foi desenvolvida com uma abordagem mais cuidadosa e tecnologias que resolvem os problemas identificados na primeira versão. O objetivo foi criar uma base de código mais limpa, sustentável e, acima de tudo, que fosse um reflexo do meu próprio aprendizado, sem as "gambiarras" da primeira tentativa.

Nesta nova fase, optei por uma stack diferente para ter mais controle sobre a interatividade, especialmente nos gráficos que foram um grande desafio na v1. A ideia é construir algo sólido que eu possa evoluir com o tempo.

### Sobre esta Documentação

O objetivo deste `README` é contar a história do Aurum, compartilhando as motivações, os desafios enfrentados e as decisões que moldaram o projeto. É um diário de bordo do desenvolvimento, mostrando a jornada de um programador criando uma ferramenta para si mesmo.

Então, só para alinharmos as expectativas: esta não é uma documentação técnica, daquelas cheias de diagramas e detalhes sobre o código. **Por enquanto**, o foco é outro.

A ideia aqui é contar a história do projeto e servir como um guia rápido. Você vai encontrar uma explicação sobre as **funcionalidades** e um passo a passo para a **instalação**, mas não vamos nos aprofundar em como as coisas funcionam "por debaixo dos panos".
