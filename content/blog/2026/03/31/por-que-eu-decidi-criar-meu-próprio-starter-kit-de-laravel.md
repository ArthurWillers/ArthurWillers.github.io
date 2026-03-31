---
title: "Por que eu decidi criar meu próprio Starter Kit de Laravel"
date: 2026-03-31T13:13:00-03:00
authors:
  - name: ArthurWillers
    link: https://github.com/ArthurWillers
    image: https://github.com/ArthurWillers.png
---

Neste post, apresento as motivações por trás da criação deste starter kit baseado no Laravel 13, detalho as escolhas tecnológicas e forneço um guia direto para que você possa utilizá-lo como ponto de partida em seus próprios projetos, garantindo foco total na implementação das regras de negócio desde o primeiro comando.

<!--more-->

## Por que?

Desenvolver aplicações web do zero exige, invariavelmente, lidar com tarefas repetitivas de configuração inicial: setup de autenticação, integração de frameworks CSS e criação de componentes básicos de interface. Com o objetivo de otimizar esse processo, desenvolvi o [James Laravel Base Template](https://github.com/ArthurWillers/james-laravel-base-template).

Como já comentei no meu [último post](../../../../2025/09/12/como-configurar-laravel-12-com-bootstrap-5/), minha jornada no Laravel começou com um projeto de extensão no ensino médio, e lá eu fiz tudo do zero, inclusive troquei o [Tailwind CSS](https://tailwindcss.com/) pelo [Bootstrap](https://getbootstrap.com/).

Após isso, sentindo uma "dor" minha por não haver um software de controle financeiro pessoal da forma que eu queria, e gratuito, decidi desenvolver o Aurum (que posteriormente foi descontinuado para dar lugar ao [Aurum2.0](https://github.com/ArthurWillers/Aurum2.0)), cuja "documentação" você pode ver [aqui!](../../../../../docs/aurum2.0/).

Sendo assim, com o Aurum2.0 eu construí uma boa estrutura de componentes e tudo mais, usando [Tailwind CSS](https://tailwindcss.com/) e Alpine.js (e, é claro, o Blade do Laravel), além de utilizar o [Laravel Fortify](https://laravel.com/docs/13.x/fortify). Posteriormente, fiz outros projetos (alguns estão no [meu GitHub](https://github.com/ArthurWillers), outros não), em que, para agilizar o desenvolvimento, copiei alguns arquivos do Aurum2.0 (a partir de agora vou chamar apenas de "Aurum", mas considere sempre a segunda versão). Com isso, percebi que seria uma boa ideia criar um template com esses arquivos (isso após muito tempo conversando com uma LLM para tentar achar alguma coisa para desenvolver).

Então comecei a pensar em como fazer o template e pus a mão na massa (durante uma aula de matemática discreta).

// no processo de escrita.
