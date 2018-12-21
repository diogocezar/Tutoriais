# NEST

Este tutorial tem como objetivo criar um guia de estudos para o Framework NestJS.

Toda a documentação oficial pode ser encontrada em: https://docs.nestjs.com/

## Introdução

O Nest é um framework para construção de aplicação back-end escaláveis. Utiliza JavaScript progressivo, construído com TypeScript (mas presenva a compatibilidade com JavaScript puro). Ainda, combina elementos de Programação Orientada a Objetos, Programação Funcional e Programação Funcional Reativa.

O Nest usa o express como base de sua implementação mas que pode ser facilmente trocado por uma outra implementação, como por exemplo o fastify.

## Instalação

```bash
$ npm i -g @nestjs/cli
```

## Primeiros Passos

### Linguagem

Você verá muito TypeScript, mas isso pode ser aprendido de forma progressiva, desta forma, é possível combinar TypeScript com JavaScript puro.

### Pré-requisitos

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

## Rodando a aplicação

```js
$ npm run start
```

O comnando inicia um servidor HTTP na porta definida no arquivo **src/main.ts**.

## Controllers

Para criação de controllers, utilizamos classes e **decorators**. Os decorators associam classes com metadados requeridos, permitindo que o Nest crie um mapa de roteamento.

## Roteamento

```js
import { Controller, Get } from "@nestjs/common";

@Controller("cats")
export class CatsController {
  @Get()
  findAll() {
    return "This action returns all cats";
  }
}
```

Para a criação de um controller utilizamos o decorator **@Controller()**. No **@Controller()**, podemos usar um prefixo que serve para indicar uma rota comum a todos handlers do controller, no caso foi especificado a rota comum **/cats**. O decorator **@Get()** informa o Nest para criar um endpoint para esta rota e mapear todas requisições para esse handler. Como foi declarado um prefixo para todas rotas **/cats**, o Nest irá mapear todos requisições /cats **GET** para este método. Quando uma requisição GET for feita para este endpoint, Nest irá retornar um status code 200 e sua resposta associada.

No exemplo, acima foi definido um endpoint para pegar os dados. Da mesma forma, é possível a criação de novos registros, utilizando o método **POST**.

```js
import { Controller, Get, Post } from "@nestjs/common";

@Controller("cats")
export class CatsController {
  @Post()
  create() {
    return "This action adds a new cat";
  }

  @Get()
  findAll() {
    return "This action returns all cats";
  }
}
```

O Nest fornece o restante dos endpoint decorators e são aplicados da mesma forma - **@Put()**, **@Delete()**, **@Patch()**. **@Options()**, **@Head()**, e **@All()**.

## Objetos de requisição

Muitos endpoints precisam de acesso aos detalhes da requisição. Por padrão, o Nest utiliza o objeto de requisição do Express. Para termos o acesso, podemos injetar um objeto de requisição no handler utilizando o **@Req()** decorator.

```js
import { Controller, Get, Req } from "@nestjs/common";

@Controller("cats")
export class CatsController {
  @Get()
  findAll(@Req() request) {
    return "This action returns all cats";
  }
}
```

O objeto request representa a requisição HTTP e possui diversas propriedades. Também podemos utilizar **decorators específicos**, tais como **@Body()** para ter acesso ao body da requisição.

## Rotas com parâmetros

Para definir rotas com parâmetros, podemos passar diretamente o parâmetro pelo caminho da rota.

```js
@Get(':id')
findOne(@Param() params) {
  console.log(params.id);
  return `This action returns a #${params.id} cat`;
}
```

## Payloads de requisição

O método **POST** anterior não recebe nenhum parâmetro do client-side. Podemos consertar isso utilizando o argumento **@Body()**.

Caso utilize TypeScript, é preciso criar um **DTO** (Data Transfer Object) schema. Este objeto define como os dados irão trafegar na rede. Podemos definir o DTO através de interfaces **TypeScript** ou classes. É recomendado a utilização de **classes**, pois as interfaces são removidas durante a transpilação do código, dessa forma o Nest não pode se referir a eles. Algumas funcionalidades do Nest permitem novas possibilidades quando possuem acesso ao metatipo da variável.

**DTO (Data Transfer Object)**

```js
export class CreateCatDto {
  readonly name: string;
  readonly age: number;
  readonly breed: string;
}
```

Podemos inserir o recém criado schema dentro do **CatsController**:

```js
@Post()
async create(@Body() createCatDto: CreateCatDto) {
  return 'This action adds a new cat';
}
```

## Exemplo de Controller utilizando os métodos HTTP

```js
import {
  Controller,
  Get,
  Post,
  Body,
  Put,
  Param,
  Delete
} from "@nestjs/common";

@Controller("cats")
export class CatsController {
  @Post()
  create(@Body() createCatDto) {
    return "This action adds a new cat";
  }

  @Get()
  findAll(@Query() query) {
    return `This action returns all cats (limit: ${query.limit} items)`;
  }

  @Get(":id")
  findOne(@Param("id") id) {
    return `This action returns a #${id} cat`;
  }

  @Put(":id")
  update(@Param("id") id, @Body() updateCatDto) {
    return `This action updates a #${id} cat`;
  }

  @Delete(":id")
  remove(@Param("id") id) {
    return `This action removes a #${id} cat`;
  }
}
```

## Importando o Controller no module

O Nest ainda não sabe da existência do **CatsController** e por isso não criará uma instância da classe.

Controllers sempre fazem parte do module, por isso temos um array de **controllers** no decorator **@Module()**. Neste importaremos o **CatsController**.

```js
import { Module } from "@nestjs/common";
import { CatsController } from "./cats/cats.controller";

@Module({
  controllers: [CatsController]
})
export class ApplicationModule {}
```

## Providers

Providers são classes JavaScript com um **@Injectable()** decorator. Basicamente, quase tudo pode ser considerado um provider. Todos eles podem injetar dependências através do **construtor**, permitindo a criação de várias relações.

Os controllers lidam com as requisições HTTP e devem passar as tarefas mais complexas para um **provider**.

**CatsService provider**

```js
import { Injectable } from '@nestjs/common';
import { Cat } from './interfaces/cat.interface';

@Injectable()
export class CatsService {
  private readonly cats: Cat[] = [];

  create(cat: Cat) {
    this.cats.push(cat);
  }

  findAll(): Cat[] {
    return this.cats;
  }
}
```

Aqui temos um provider com dois métodos. O **@Injectable()** decorator anexa os metadados, portanto o Nest sabe que esta classe é um provider.

Agora devemos importar esse **provider** dentro do **CatsController**

```js
import { Controller, Get, Post, Body } from '@nestjs/common';
import { CreateCatDto } from './dto/create-cat.dto';
import { CatsService } from './cats.service';
import { Cat } from './interfaces/cat.interface';

@Controller('cats')
export class CatsController {
  constructor(private readonly catsService: CatsService) {}

  @Post()
  async create(@Body() createCatDto: CreateCatDto) {
    this.catsService.create(createCatDto);
  }

  @Get()
  async findAll(): Promise<Cat[]> {
    return this.catsService.findAll();
  }
}
```

O provider é injetado na classe construtora.

## Importação do Provider no module

Precisamos informar o Nest da existência do Provider. Para isso o importaremos no **app.module.ts** colocando-o no vetor de providers.

```js
import { Module } from "@nestjs/common";
import { CatsController } from "./cats/cats.controller";
import { CatsService } from "./cats/cats.service";

@Module({
  controllers: [CatsController],
  providers: [CatsService]
})
export class ApplicationModule {}
```

## Módulos

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

Este módulo importa o módulo comum do nest, e também importamos um **Controller** e um **Provider**.

Podemos criar outros módulos agrupando funcionalidades em comum.

```js
import { Module } from "@nestjs/common";
import { CatsController } from "./cats.controller";
import { CatsService } from "./cats.service";

@Module({
  controllers: [CatsController],
  providers: [CatsService]
})
export class CatsModule {}
```

Aqui foi criado um módulo que agrupa funcionalidades relacionadas a **cats**. Devemos importar esse módulo no módulo raiz.

```js
import { Module } from "@nestjs/common";
import { CatsModule } from "./cats/cats.module";
import { AppController } from "./app.controller";
import { AppService } from "./app.service";

@Module({
  imports: [CatsModule],
  controllers: [AppController],
  providers: [AppService]
})
export class AppModule {}
```

## Middleware

Um middleware é uma função que é chamada antes do manipulador de rotas. Os middlewares possuem acesso as requisições e respostas. Por padrão, os middlewares no Nest são equivalentes aos do Express.

Os middlewares no Nest podem ser funções ou classes com um **@Injectable()** decorator. A classe precisa implementar o **NestMiddleware**, enquanto a função não precisa de um tratamento especial.

Exemplos de Middleware usando classes.

```js
import { Injectable, NestMiddleware, MiddlewareFunction } from "@nestjs/common";

@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  resolve(...args: any[]): MiddlewareFunction {
    return (req, res, next) => {
      console.log("Request...");
      next();
    };
  }
}
```

O método **resolve()** precisa retornar um middleware específico da biblioteca **(req, res, next) => any**.
