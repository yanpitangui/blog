---
title: "Iniciando uma api em .NET rapidamente com um boilerplate"
date: 2023-05-10T21:56:13-03:00
draft: false
tags: [boilerplate, todo, dotnet, api]
translationKey: "api-boilerplate"
---

## O que é um boilerplate de API?

Um boilerplate de API é um modelo pré-construído que fornece uma estrutura básica e um conjunto de funcionalidades para criar uma API da Web. Ele inclui componentes essenciais, como roteamento, integração de banco de dados, tratamento de erros e recursos de segurança que geralmente são necessários na maioria dos projetos de API.

## Por que você deveria se preocupar com isso?
O uso de um boilerplate de API pode acelerar significativamente o processo de desenvolvimento inicial por vários motivos:

Fornece uma estrutura estruturada e consistente: um boilerplate de API oferece uma estrutura clara e estruturada para começar, garantindo que a base de código permaneça organizada e consistente. Também ajuda os desenvolvedores a evitar gastar tempo e esforço decidindo sobre a melhor arquitetura e estrutura para o projeto.

Economiza tempo e esforço: com um boilerplate de API, os desenvolvedores podem evitar as tarefas repetitivas de criar funcionalidades semelhantes do zero, como autenticação e tratamento de erros. Isso permite que os desenvolvedores se concentrem na criação de recursos exclusivos de sua API, em vez de escrever código boilerplate.

Aumenta a confiabilidade: o uso de um boilerplate pré-criado garante que a API seja construída com as melhores práticas em mente e é menos provável que tenha erros ou vulnerabilidades comuns. Isso poupa os desenvolvedores da dor de cabeça de erros de depuração ou correção de problemas de segurança que poderiam ter sido evitados com um boilerplate.

Facilita a colaboração: os boilerplates da API geralmente são de código aberto e podem ser personalizados pela equipe de desenvolvimento de acordo com suas necessidades específicas. Isso facilita a colaboração entre os membros da equipe e garante que todos trabalhem com a mesma base de código, reduzindo a probabilidade de conflitos decorrentes de diferentes estilos e práticas de codificação.

No geral, um boilerplate de API fornece uma base sólida para o desenvolvimento de uma API, permitindo que os desenvolvedores se concentrem na criação de recursos exclusivos de seu aplicativo, melhorando a produtividade e, finalmente, entregando uma API de alta qualidade mais rapidamente.


## Boilerplates em dotnet
Em dotnet, é possível utilizar templates de múltiplas maneiras. 
Alguns, devem ser instalados via ```dotnet new --install NomeDoTemplate```, como [Dotnet-Boxed](https://github.com/Dotnet-Boxed/Templates) e [Akka.NET](https://github.com/akkadotnet/akkadotnet-templates).

O mais famoso, [ASP.NET Boilerplate](https://github.com/aspnetboilerplate/aspnetboilerplate) é bastante configurável e contém muitas variações de tecnologias, desde integração com React e Angular a implementação de multitentant e toda a configuração do template é feita através do site. Existem templates free e premiums.

Outra maneira, também conveniente, é fazer o clone/download/fork do repositório, como é o caso de [netcore-boilerplate](https://github.com/lkurzyniec/netcore-boilerplate) e [dotnet-api-boilerplate](https://github.com/yanpitangui/dotnet-api-boilerplate).

Este último, criado e desenvolvido por mim ao longo do tempo, é produto de uma tentativa de aprender fazendo. 
Foi sendo melhorado de acordo com que adquiri experiência no mercado e estudei mais a fundo questões como design e arquitetura de aplicações.

Como este é o que mais conheço, será o que terá o exemplo de utilização a seguir.

## Como utilizar o boilerplate

### Maneira recomendada
<iframe src="https://scribehow.com/embed/Criando_um_repositorio_a_partir_de_um_template__XfCpSqLmTumICXDzDB86pQ?skipIntro=true" width="100%" height="640" allowfullscreen frameborder="0"></iframe>


