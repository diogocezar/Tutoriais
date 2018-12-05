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
```

O próximo passo é iniciar a sua configuração:

```bash
$ yarn run eslint --init
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

## Instalando o TSLint

Dentro do projeto em questão, instale o TSLint:

```bash
$ yarn add tslint -D
```

Depois execute da mesma forma o assistente do tslint:

```bash
$ tslint --init
```

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

## Utilizando algumas configurações personalizadas

Utilize este setup de configurações para o ESLint:

```JSON
{
	"parser": "babel-eslint",
	"env": {
		"browser": true,
		"jest": true
	},
	"plugins": ["react", "jsx-a11y", "import"],
	"extends": "airbnb",
	"rules": {
		"react/jsx-filename-extension": [
			"error",
			{
				"extensions": [".js", ".jsx"]
			}
		],
		"react/jsx-indent": ["error", "tab"],
		"react/jsx-indent-props": ["error", "tab"],
		"semi": [2, "never"],
		"indent": ["error", "tab"],
		"no-tabs": 0,
		"quotes": [2, "single", "avoid-escape"],
		"global-require": "off",
		"import/prefer-default-export": "off",
		"no-unused-expressions": [
			"error",
			{
				"allowTaggedTemplates": true
			}
		]
	}
}
```

Para isso, basta editar o conteúdo do arquivo .eslintrc.json com o conteúdo acima.

Utilize este setup de configurações para o TSLint:

```JSON

```

Ainda, na raiz do projeto, crie um arquivo chamado .editorconfig, com o seguinte conteúdo:

```
root = true

[*]
indent_style = tab
indent_size = 4
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

Depois disso, o seu ambiente está pronto e configurado!

Happy Hacking!
