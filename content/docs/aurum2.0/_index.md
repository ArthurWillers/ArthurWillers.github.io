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

### O Desenvolvimento

Depois da experiência com a primeira versão, o lema para o Aurum 2.0 foi: **"fazer do jeito certo, sem pressa"**. O objetivo não era apenas ter o software funcionando, mas construir algo que eu tivesse orgulho de ter escrito, com uma base sólida e fácil de manter.

Esta parte é um pouco mais "técnica", mas o foco é compartilhar as decisões e o *porquê* por trás delas, e não detalhar cada linha de código.

#### A Escolha da Stack: O Simples que Funciona

Diferente da v1, onde usei o TALL Stack para acelerar, na v2.0 eu voltei para o básico e robusto. A escolha foi:

* **Backend: Laravel 12** Não tinha por que mudar. O Laravel é um framework que adoro, extremamente produtivo e com uma comunidade gigante. Usei a estrutura padrão MVC (Model-View-Controller) que ele oferece, o que mantém tudo organizado.

* **Frontend: Blade com um toque de JavaScript** O maior problema da v1 foi a reatividade dos gráficos com o Livewire. Para a v2.0, decidi simplificar. A maior parte da interface é renderizada pelo servidor com o Blade, o que é ótimo para a performance e simplicidade. Para a interatividade, como nos dropdowns, a ideia é usar Alpine.js.

#### Resolvendo o Problema dos Gráficos

Inicialmente, meu plano para evitar o problema da v1 era mais complexo, envolvendo bibliotecas de JavaScript como ApexCharts. No entanto, com o passar do tempo, percebi que estava complicando demais para o que eu realmente precisava.

A verdade é que para exibir barras de progresso simples, não é necessária uma biblioteca externa.

No final, a solução foi aprimorar a **mesma abordagem que usei como contorno na v1**, só que bem melhor:

1.  **Busca dos Dados no Backend:** O `DashboardController` no Laravel é responsável por buscar os dados brutos: a soma total de receitas, o total de despesas e os valores somados de cada categoria. Ele apenas entrega os números para a view.
2.  **Cálculo e Renderização no Blade:** A "mágica" acontece diretamente no frontend, mas sem JavaScript. Os gráficos são, na verdade, barras de progresso feitas com HTML. O cálculo do percentual de cada categoria é feito na própria view com o Blade, que então define a largura (`width`) da barra usando CSS.

Essa abordagem não só resolveu o problema de reatividade de forma definitiva, como também deixou o carregamento da página mais rápido, sem a necessidade de carregar bibliotecas JavaScript pesadas.

Além disso, melhorei a funcionalidade: em vez de mostrar apenas as 3 categorias principais como na v1, agora o dashboard exibe **todas** as categorias que tiveram movimentação no mês, dando uma visão muito mais completa e útil dos seus gastos e ganhos.