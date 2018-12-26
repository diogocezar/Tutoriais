# Instalação do Bash no Windows

Para se obter um ambiente Linux dentro do windows, é necessário que se esteja utilizando o Windows10.

Caso isso não seja possível, paleativamente, pode-se utilizar o terminal git bash, que vem junto com o git for windows, disponível em: https://git-scm.com/downloads

Mas, assumindo que temos um ambiente com Windows 10.

## Passo 1 - Atualização

Certifique-se que o seu sistema operacional esteja atualizado. Caso não esteja, siga os procedimentos necessários para atualizá-lo.

## Passo 2 - Instalação

Siga este tutorial oficial de instalação:

https://docs.microsoft.com/en-us/windows/wsl/install-win10

Utilize a versão Ubuntu.

Não se esqueça de iniciar a nova instalação seguindo:

https://docs.microsoft.com/en-us/windows/wsl/initialize-distro

## Passo 3 - Hyper.JS

Agora, podemos instalar programa para ajudar bastante com a aparência de nossa stack, além disso, com ele é possível a instalação de alguns plugins que facilitam bastante o nosso desenvolvimento.

Basta fazer o download e instalar o Hyper aqui:

https://hyper.is/

Opcionalmente, eu recomendo a utilização do tema Dracula, disponível aqui:

https://draculatheme.com/hyper/

Para instalar o tema, pressione <kbd>Ctrl</kbd> + <kbd>,</kbd> para trazer as configurações do Hyper.

Procure pela sessão `plugins: [` e edite adicionando o tema desejado:

```
plugins: [
    "hyper-dracula
],
```

## Passo 4 - Configurar o Hyper para Acessar o Bash do Ubuntu

Ao abrir o Hyper, no windows, notamos que abrimos um console nativo, mas não queremos isso... queremos que ele abra o bash do ubuntu que acabamos de instalar.

Para isso, utilize novamente <kbd>Ctrl</kbd> + <kbd>,</kbd> para trazer as configurações do Hyper.

Ache a sessão em que temos a configuração `shell : `

E altere para:

```shell: 'C:\\Windows\\System32\\bash.exe'```

## Passo 5 - Criando uma Senha de Root

Eventualmente vamos precisar utilizar o comando `sudo` por isso precisamos criar uma senha para o superusuário no Linux.

```bash
$ sudo su
$ passwd
```

Com isso, será solicitada a senha para o usuário root, e poderá ser utilizada todas as vezes que necessário.

## Passo 5 - Atualizando o seu ambiente Linux

Muitas vezes, temos a atualização de uma série de pacotes no Linux, para isso, recomendo que essa ação seja feita pelo menos uma vez por semana, e também, agora que acabamos de instalar o ambiente:

```bash
$ sudo apt-get update
$ sudo apt-get upgrade
```

Com isso teremos certeza que o sistema estará atualizado para as próximas instalações.

## Passo 6 - Instalando o GIT

Devemos instalar o ambiente do Git dentro do ambiente Linux, para isso, vamos utilizar um comando de instalação padrão no ambiente, que poderá ser utilizado para instalar outras funcionalidades:

```bash
$ sudo apt-get install git
```

## Passo 7 - Instalando o ZSH

Essa ferramenta incrementa uma serie de funcionalidades no Bash, para instalá-lo basta utilizar os comandos:

```bash
$ sudo apt-get install zsh
```

Agora precisaremos editar o arquivo `~/.bashrc`.

Este arquivo fica na "raiz" dos seus diretório dentro do linux, disponível em `/home/<seu_usuario>`

Este arquivo é o reponsável por executar uma série de comando assim que o bash for inicializado.

Por isso, precisamos aqui dizer que ao invés de abrir o bash tradicional, precisamos abrir o bash do zsh!

Vamos precisar de uma forma de editar arquivos dentro do terminal, recomendo o nano que é bem intuitivo, então...

```bash
$ nano ~/.bashrc
```
Adicione o comando screenfetch 
```bash
$ sudo apt install screenfetch
```

Adicione isso para fazer com que o ZSH seja o padrão!

```bash
screenfetch
bash -c zsh
# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

# If not running interactively, don't do anything
case $- in
```

## Passo 8 - Instalar o Oh My ZSH

Esse kra é um complemente essencial para o ZSH que vai permitir uma serie de plugins adicionais.

Para isso basta executar o comando:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

Agora vamos alterar o tema do Oh My ZSH, existem vários e isso vai de acordo com a sua preferência, no momento, vamos utilizar o tema: powerlevel9k

Para instalá-lo com o Oh My ZSH, basta rodar o comando:

```bash
$ git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
```
Agora precisamos editar algumas coisas, então:

```bash
$ nano ~/.zshrc
```

Esse é o arquivo de configuração do Zsh, agora podemos então aplicar o tema e algumas configurações adicionais:

```bash
# Set name of the theme to load. Optionally, if you set this to "random"
# it'll load a random theme each time that oh-my-zsh is loaded.
# See https://github.com/robbyrussell/oh-my-zsh/wiki/Themes
#ZSH_THEME="robbyrussell"
ZSH_THEME="powerlevel9k/powerlevel9k"
POWERLEVEL9K_MODE="nerdfont-complete"
POWERLEVEL9K_PROMPT_ON_NEWLINE=true
```

Note que comentamos o tema default e colocamos o novo tema.

Além disso também definimos para que os comandos sejam executados em outra linha.

A linha que contém: `POWERLEVEL9K_MODE="nerdfont-complete"` é opcional e leva em consideração a utilização de um sistema operacional nativo, para isso, pode-se opcionalmente instalar os pacotes de fontes para uma melhor aparência. 

Mais detalhes podem ser vistos em:

* https://github.com/ryanoasis/nerd-fonts
* https://github.com/bhilburn/powerlevel9k/#installation

Para o windows é interessante a intalação de algumas fontes específicas descritas aqui:

http://bit.ly/2r7Yfoh

## Passo 9 - Plugins Adicionais

Recomendo fortemente a instalação dos plugins:

* zsh-syntax-highlighting
* zsh-autosuggestions

As instruções para sua instalação podem ser encontradas aqui: http://bit.ly/2r3Ofg3

## Passo 10 - Coisas Legais

Eventualmente pode ser bacana dar uma personalizada, isso é totalmente opcional, mas fica o link:

http://bit.ly/2GoEO0t

## Conclusão

É isso pessoal, espero que todos possam serguir os passos e dessa forma, teremos um ambiente comum a todos os colaboradores ;)

Toda a colaboração neste tutorial é sempre bem vinda!

Qualquer dúvida, basta enviar um e-mail para: diogo.batista@meifacil.com

Cya!
