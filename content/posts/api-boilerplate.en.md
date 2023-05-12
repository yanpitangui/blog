---
title: "Starting a .NET api quickly with a boilerplate"
date: 2023-05-10T21:56:13-03:00
draft: false
tags: [boilerplate, todo, dotnet, api]
translationKey: "api-boilerplate"
---

## What is an API boilerplate?

An API boilerplate is a pre-built template that provides a basic structure and set of functionalities for creating a web API. It includes essential components such as routing, database integration, error handling, and security features that are commonly required in most API projects.

## Why should you care about it?
Using an API boilerplate can significantly speed up the initial development process for several reasons:

Provides a Structured and Consistent Framework: An API boilerplate offers a clear and structured framework to start from, ensuring that the codebase remains organized and consistent. It also helps developers to avoid spending time and effort deciding on the best architecture and structure for the project.

Saves Time and Effort: With an API boilerplate, developers can avoid the repetitive tasks of building similar functionalities from scratch, such as authentication and error handling. This allows developers to focus on building the unique features of their API instead of writing boilerplate code.

Increases Reliability: Using a pre-built boilerplate ensures that the API is built with best practices in mind and is less likely to have common errors or vulnerabilities. This saves developers from the headache of debugging errors or fixing security issues that could have been avoided with a boilerplate.

Facilitates Collaboration: API boilerplates are usually open-source and can be customized by the development team according to their specific needs. This facilitates collaboration among team members and ensures that everyone is working with the same codebase, reducing the likelihood of conflicts arising from different coding styles and practices.

Overall, an API boilerplate provides a solid foundation for developing an API, allowing developers to focus on building the unique features of their application, improving productivity, and ultimately delivering a high-quality API faster.

## Boilerplates in dotnet
In dotnet, it is possible to use templates in multiple ways.
Some must be installed via ```dotnet new --install TemplateName```, such as [Dotnet-Boxed](https://github.com/Dotnet-Boxed/Templates) and [Akka.NET](https:/ /github.com/akkadotnet/akkadotnet-templates).

The most famous one, [ASP.NET Boilerplate](https://github.com/aspnetboilerplate/aspnetboilerplate) is quite configurable and contains many variations of technologies, from React and Angular integration to multitentant implementation and all template configuration is made through the website. There are free and premium templates.

Another convenient way is to clone/download/fork the repository, as is the case with [netcore-boilerplate](https://github.com/lkurzyniec/netcore-boilerplate) and [dotnet-api-boilerplate] (https://github.com/yanpitangui/dotnet-api-boilerplate).

The latter, created and developed by me over time, is the product of an attempt to learn by doing.
It was being improved as I gained experience in the market and studied issues such as application design and architecture in more depth.

As this is the one I know the most, it will be the one that will be used in the following example.

## How to use the boilerplate
<iframe src="https://scribehow.com/embed/Creating_a_repository_from_a_template__wtmg_1aXTOGPcsDWvtplRg?skipIntro=true" width="100%" height="640" allowfullscreen frameborder="0"></iframe>
After that, just clone the project and follow the [README.MD](https://github.com/yanpitangui/dotnet-api-boilerplate/blob/main/README.md) instructions, which involve removing the "hero" classes/resources and creating the classes/resources that meet your project's business needs.