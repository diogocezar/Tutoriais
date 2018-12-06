# StyleGuide MEIFácil

Olá pessoa, tudo certinho?

Este tutorial tem como objetivo a criação de um guia de estilos para o desenvolvimento nas novas Stacks da MEI Fácil.

Para isso, vamos utilizar 4 principais ferramentas:

1. ESLint; (https://eslint.org/)
2. TSLint; (https://palantir.github.io/tslint/)
3. Prettier; (https://github.com/prettier/prettier)
4. Editor Config; (https://editorconfig.org/)

A idéia deste tutorial é manter de fato uma forma de compatibilidade entre os códigos escritos por diferentes programadores.

Por isso, é muito importante que sigam todas essas instruções para que todo o ambiente seja configurado corretamente.

Lembrando que todo esse tutorial foi baseado e foi adaptado deste material:

http://bit.ly/2Pkawj9

O importante é salientar a diferença entre o ESLint e o TSLint;

Ambos são ferramentas para ajudar na correção e padronização dos códigos, com a diferença que o ESLint é utilizado para JavaScript e o TSLint para TypeScript;

Alguns frameworks já trazem o ambiente instalado como por exemplo o Nest com o TSLint.

Mas, para a configuração do seu ambiente, recomenda-se seguir os próximos passos para realizar a configuração completa do seu ambiente;

## Instalando o ESLint

Dentro do projeto em questão, instale o ESLint:

```bash
$ yarn add eslint -D
# or
$ npm i eslint -D
```

O próximo passo é iniciar a sua configuração:

```bash
$ yarn run eslint --init
# or
$ ./node_modules/.bin/eslint --init
```

Com isso, algumas perguntas deverão ser respondidas, e vamos manter este padrão:

```
User popular style guide
```

Em seguida...

```
Airbnb
```

E depois...

Escolha se é um projeto em react ou não...

Ainda, escolha o formato JSON para o padrão de arquivo de configuração.

Por fim, ele irá instalar alguns pacotes adicionais para a configuração.

Algumas configurações devem ser ajustadas nos arquivos de configuração, para isso, em .eslintrc substitua por:

```JSON
{
	"extends": "airbnb-base",
	"rules": {
		"semi": [2, "never"]
	}
}
```

Este estilo utiliza o padrão do airbnb com alguns ajustes adicionais;

## Instalando o TSLint

Dentro do projeto em questão, instale o TSLint:

```bash
$ yarn add tslint -D
# or
$ npm i tslint -D
```

Depois execute da mesma forma o assistente do tslint:

```bash
$ yarn run tslint --init
# or
$ ./node_modules/.bin/tslint --init
```

O próximo passo é instalar a configuração do airbnb:

```bash
$ yarn add tslint-config-airbnb -D
# or
$ npm install tslint-config-airbnb --save-dev
```

O próximo passo é atualizar o tslint.json:

```JSON
{
	"defaultSeverity": "error",
	"extends": ["tslint-config-airbnb"],
	"jsRules": {},
	"rules": {
		"semicolon": [true, "never"]
	},
	"rulesDirectory": []
}
```

E por fim, configurar o prettier, atualizando o .prettierrc:

## Configurando as extensões

Você precisará instalar e ativar em seu VSCode as seguintes extensões:

1. ESLint
2. TSLint
3. Prettier

Depois disso ainda é necessário alterar algumas configurações do VSCode para que o ambiente se mantenha atualizado de acordo com o esperado.

Abra o arquivo JSON de configurações do usuário e adicione:

```JSON
"editor.formatOnPaste": true,
"editor.formatOnSave": true,
"prettier.eslintIntegration": true,
"prettier.tslintIntegration": true
```

Ao habilitar essas integrações, estamos dizendo para o nosso VSCode e para o nosso Prettier que as regras que estiverem especificadas nas definições dos arquivos eslintrc.json e tslintrc.json devem ser sobrescritas as regras do prettier.

## Utilizando algumas configurações personalizadas

Ainda, na raiz do projeto, crie um arquivo chamado .editorconfig, com o seguinte conteúdo:

```
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

## Importante

Não é necessário utilizar o .prettierrc para qualquer configuração do seu VSCode, pois estamos dizendo ao Prettier para usar os arquivos locais do ESLint e TSLint para sua formatação.

---

Depois disso, o seu ambiente está pronto e configurado!

Happy Hacking!
