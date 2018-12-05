# NEST

Este tutorial tem como objetivo criar um guia de estudos para o Framework NestJS.

Toda a documentação oficial pode ser encontrada em: https://docs.nestjs.com/

## Introdução

O Nest é um framework para construção de aplicação back-end escaláveis. Utiliza JavaScript progressivo, construído com TypeScrip (mas presenva a compatibilidade com JavaScript puro). Ainda, combina elementos de Programação Orientada a Objetos, Programação Funcional e Programação Funcional Reativa.

O Nest usa o express como base de sua implementação mas que pode ser facilmente trocado por uma outra implementação, como por exemplo o fastify.

## Instalação

```bash
$ npm i -g @nestjs/cli
```

## Primeiros Passos

### Linguagem

Você verá muito TypeScript, mas isso pode ser aprendido de forma progressiva, desta forma, é possível combinar TypeScript com JavaScript puro.

### Prerequisitos

Para que o nestjs funcione você precisa pelo menos da versão do node >= 8.9.0

### Configuração

Para iniciar um novo projeto:

```bash
$ nest new project
```

Você poderá escolher algumas configurações iniciais do projeto.

### Estrutura de pastas

Em node_modules estão os módulos do NPM;

Em src estão os códigos do projeto;

Em test estão os testes unitários do projeto;

Dando uma olhada mais especial em src, temos:

```
src
    app.controller.ts
    app.module.ts
    main.ts
```

main.ts é o arquivo de entrada, onde o framework inicia.

Podemos notar que este arquivo importa um módulo chamado 'AppModule'

```js
import { NestFactory } from "@nestjs/core";
import { AppModule } from "./app.module";

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

Neste exemplo, temos o core do Nest instanciando um novo módulo, o único do nosso projeto.

Depois, é iniciado o serviço que fica escutando em uma porta específica.

No nest, temos um conceito de módulos. Podemos pensar que os módulos são agrupamentos de funcionalidades em comum.

Dando uma olhada no módulo App, temos:

```js
import { Module } from "@nestjs/common";
import { AppController } from "./app.controller";
import { AppService } from "./app.service";

@Module({
  imports: [],
  controllers: [AppController],
  providers: [AppService]
})
export class AppModule {}
```

Este módulo importa o módulo comum do nest, e também outros 2 conceitos principais: AppController e AppService.
