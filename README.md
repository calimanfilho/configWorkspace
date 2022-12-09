## Configuração do meu Workspace
Esse repositório terá o passo a passo utilizado para configurar meu ambiente de trabalho com Windows e Linux.

## Debloat no Windows 11 (Em Construção)
Utilizar o [Win Debloat Tools](https://github.com/LeDragoX/Win-Debloat-Tools) que é uma coleção de _scripts_ que permitem ajustar o Windows 10+ melhorando o desempenho, aumentando a privacidade e realizando outras alterações.

## Subsistema Windows para Linux (Windows Subsystem for Linux - WSL2)
A primeira coisa que deve ser feita é instalar o WSL2 pelo Windows PowerShell com `wsl --install`, e depois o Windows Terminal pela Microsoft Store.

> ℹ️ **_INFO_**  
> Caso seja utilizado a disitribuição Ubuntu, ela é automaticamente instalada, mas para o Arch Linux a Microsoft ainda não possui suporte oficial, mas distribuição pode ser baixada pelo projeto https://github.com/yuk7/ArchWSL. 


## Temas do Windows Terminal
Será colocado o tema Dracula no Windows Terminal Themes, para isso deve ser aberto o https://windowsterminalthemes.dev/?theme=Dracula, clicar em `Get theme` para copiar as configurações em ````````````````JSON```````````````` para o _clipboard_, agora deve ser acessado as configurações do Terminal e ir em `Abrir o arquivo JSON`, e após o último tema deve ser colocado uma virgula e colar o JSON copiado anteriormente.

```json
{
  "name": "Dracula",
  "black": "#000000",
  "red": "#ff5555",
  "green": "#50fa7b",
  "yellow": "#f1fa8c",
  "blue": "#bd93f9",
  "purple": "#ff79c6",
  "cyan": "#8be9fd",
  "white": "#bbbbbb",
  "brightBlack": "#555555",
  "brightRed": "#ff5555",
  "brightGreen": "#50fa7b",
  "brightYellow": "#f1fa8c",
  "brightBlue": "#bd93f9",
  "brightPurple": "#ff79c6",
  "brightCyan": "#8be9fd",
  "brightWhite": "#ffffff",
  "background": "#1e1f29",
  "foreground": "#f8f8f2",
  "selectionBackground": "#44475a",
  "cursorColor": "#bbbbbb"
}
```
Para mudar a configuração deve ser acessado o Ubuntu no menu, ir em Aparência e mudar o tema para Dracula.


# Shell
Será instalado o `Zsh` para substituir o `Bash`:

```bash
sudo apt install zsh -y
```

Próximo passo é instalar o [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh), estrutura de código aberto voltada para a comunidade para gerenciar a configuração do Zsh:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
O script solicitará para mudar o _default_ _shell_ para Zsh, basta confirmar.

Para verificar o _shell_ padrão basta utilizar `grep calimanfilho /etc/passwd`, senco `calimanfilho` o nome de usuário.

Caso não tenha sido alterado, poderá ser usado o comando `chsh -s $(which zsh)`.

Agora será baixado o tema para o Zsh, o [Powerlevel10k](https://github.com/romkatv/powerlevel10k), com o comando:

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

Após o `download` será necessário alterar o tema do Zsh para `ZSH_THEME="powerlevel10k/powerlevel10k"` no `~/.zshrc`, e seguir os procedimentos abaixo:

1. Baixar as fontes indicadas pelo Zsh no GitHub:
    * [MesloLGS NF Regular.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf)
    * [MesloLGS NF Bold.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf)
    * [MesloLGS NF Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf)
    * [MesloLGS NF Bold Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf)

2. Clicar duas vezes em cada arquivo e clicar em "Instalar". Isso tornará a fonte `MesloLGS NF` disponível para todos aplicativos em seu sistema.

3. Configurar o Windows Terminal para usar a fonte, em Configurações (`Ctrl + ,`), clicar no perfil `Ubuntu`, clicar em Aparência e definir a fonte como MesloLGS NF.

Por fim, ao fechar e abrir o Terminal irá aparecer o assistente de configuração do `Powerlevel10k`, caso não apareça, basta utilizar o `p10k configure`, agora basta selecionar as configurações desejadas e o novo _shell_ estará pronto.


# Editor de Texto
Como editor padrão será utilizado o Visual Studio Code, como outra opção pode ser utilizado o VSCodium que é uma alternativa mais leve e com maior privacidade. Também será configurado o Vim para uso do editor de texto no Terminal, em específico o _fork_ do Vim chamado de Neovim, com uma IDE chamada de LunarVim. 

A [instalação do Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim) será feita de forma manual, nesse documento será instalado o Neovim 0.9.0, atualmente no repositório do Ubuntu ainda não possui a v0.9.0, a solução será compilar do zero (ou baixar um AppImage quando disponível).

Antes de tudo deve ser removido a versão atual do Neovim no sistema, caso tenha alguma:

```bash
sudo apt remove neovim --purge
sudo apt autoremove autoclean clean
```

Agora será instalado as dependências necessárias:

```bash
sudo apt update
sudo apt install git build-essential cmake git pkg-config libtool g++ libunibilium4 libunibilium-dev ninja-build gettext libtool libtool-bin autoconf automake unzip curl doxygen lua-term lua-term-dev luarocks
```

E clonar o repositório do projeto Neovim para a máquina local:

```bash
git clone https://github.com/neovim/neovim
cd neovim
make CMAKE_BUILD_TYPE=RelWithDebInfo
sudo make install
```
> ℹ️ **_INFO_**  
> Se ocorrer problema ao ler o lfs do Lua, deve ser instalado o LuaRocks com `sudo luarocks install luafilesystem`.

As vezes a equipe de desenvolvimento do Neovim disponibiliza uma versão AppImage em _releases_, se não houver, haverá binários já prontos [aqui](https://github.com/neovim/neovim/releases).

Para verificar se ocorreu tudo certo na instalação, pode ser executado o comando `/usr/local/bin/nvim --version`.

Após o termino da instalação do Neovim, deverá ser [instalado o LunarVim](https://www.lunarvim.org/docs/installation) com o script a seguir:

```bash
bash <(curl -s https://raw.githubusercontent.com/lunarvim/lunarvim/master/utils/installer/install.sh)
```

Se tudo deu certo o _script_ será executado, e perguntará se será necessário instalar as dependências do NodeJS, Python e Rust, nesse exemplo para todas as opções será informado `no`.

Como o `lvim` ainda não foi adicionado nas configurações do _shell_, ele poderá ser executado com o comando `~/.local/bin/lvim`.

Agora deverá ser adicionado o _PATH_ do `nvim` e do `lvim` no `~/.zshrc`, para que o comando possa ser executado sem a necessidade de informar o caminho completo. Para isso deverá ser executado o `vim ~/.zshrc`, e adicionar ao fim do arquivo a linha abaixo:

```bash
export PATH=/usr/local/bin:$HOME/.local/bin:$PATH
```

É necessário fechar e abrir o terminal para que as configurações do _PATH_ sejam validadas.

Nas configurações do `lvim` será retirado o número de linha relativo, para isso deve ser aberto o `~/.config/lvim/config.lua` e alterado a opção `vim.opt.relativenumber = true` para `vim.opt.relativenumber = false`.


## _Plugins_ Úteis
Serão listados alguns `plugins` interessantes para conhecimento, mas só será mostrado a instalação dos que serão utilizados:

* [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting): Destaca os comandos enquanto eles são digitados. Se o comando estiver correto, ele será exibido na cor verde, caso contrário, o comando ficará em vermelho.

* [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions): Sugere comandos conforme se digita com base no histórico.

* [bat](https://github.com/sharkdp/bat): Clone do cat com realce de sintaxe e integração com o Git.

* [exa](https://github.com/ogham/exa): Substituto moderno para ls, suporta ícones com o sinalizador `--icons`.

* [fd](https://github.com/sharkdp/fd): Uma alternativa rápida e fácil para pesquisar, já instalado pelo LunarVim.

Será instalado o _plugin_ `bat` com:
```bash
sudo apt install bat
```

O outro _plugin_ que será instalado é o `exa`, caso seja utilizado a versão do Ubuntu 20.10 (Groovy Gorilla) ou superior, pode ser instalado com:

```bash
sudo apt install exa
```

Caso contrário, terá que ser feita a instalação manual seguindo os procedimentos a seguir:

Deve ser obtida a _tag_ da versão mais recente de lançamento do exa e atribui-lá à variável `EXA_VERSION`:

```bash
EXA_VERSION=$(curl -s "https://api.github.com/repos/ogham/exa/releases/latest" | grep -Po '"tag_name": "v\K[0-9.]+')
```

Realiza o `download` do arquivo `zip` da página de lançamento do repositório `exa` dando o nome de `exa.zip`:

```bash
curl -Lo exa.zip "https://github.com/ogham/exa/releases/latest/download/exa-linux-x86_64-v${EXA_VERSION}.zip"
```

Extrai somente o arquivo binário da pasta `/bin/exa` do arquivo ZIP e move para `/usr/local`:

```bash
sudo unzip -q exa.zip bin/exa -d /usr/local
```

Agora o comando `exa` está disponível para todos os usuários, o arquivo `.zip` já pode ser excluído:

```bash
rm -rf exa.zip
```

Para checar se tudo foi instalado corretamente, pode ser utilizado o comando `exa --version`.

Depois dos _plugins_ instalados serão adicionados os `alias` a seguir no arquivo `.zshrc` para facilitar o uso do comando:

```bash
alias ls="exa --icons"
alias bat="batcat --style=auto"
```

Lembrar de fechar e abrir o terminal para as configurações serem validadas.

## Ferramentas
O `asdf` é uma ferramenta que permite gerenciar várias versões e linguagens de `frameworks`, ele está sendo mensionado para ficar registrado caso futuramente seja necessário.


## Observações e Dicas
Lembrar de realiza a copia das chaves privadas para o diretório `$HOME/.ssh/` no Ubuntu, de modo ideal as chaves poderiam ter sido compactada com `tar`, para que ao descompactar utilizando o `tar xvfz` as permissões sejam mantidas, caso tenha sido compactada de outra maneira deverá ser executado o `sudo chmod -R 600 .ssh` para que seja dado permissão de leitura e escrita para o usuário e os outros não poderem ler nem listar os arquivos do diretório.

Além disso, pode ser criado um `link simbólico` da pasta de usuário do PC físico no diretório do usuário no Ubuntu, com o comando:

 ```bash
ln -s /mnt/c/Users/Esmael\ Caliman\ Filho Windows
```


## Roadmap

Será listado algumas ferramentas que faltaram (ou não) nesse documento, para posteriormente serem estudadas e incluídas.

- [ ] [Win Debloat Tools](https://github.com/LeDragoX/Win-Debloat-Tools)
- [ ] [Cargo](https://github.com/rust-lang/cargo)
- [ ] [CLI gcloud](https://cloud.google.com/sdk/docs/install?hl=pt-br)
- [ ] [AWS CLI](https://aws.amazon.com/pt/cli/)
- [ ] [Docker](https://docs.docker.com/desktop/install/linux-install/)
- [ ] [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [ ] [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- [ ] [Terraform](https://developer.hashicorp.com/terraform/downloads)


## Referências

Espaço para listar os artigos e vídeos que foram utilizados para a criação do documento.

* [Como Compilar o Neovim do Zero](https://terminalroot.com.br/2022/05/como-compilar-o-neovim-do-zero.html)
* [O Melhor Setup Dev com Arch e WSL2](https://youtu.be/sjrW74Hx5Po)
* [Rewritten in Rust: Modern Alternatives of Command-Line Tools](https://zaiste.net/posts/shell-commands-rust/)