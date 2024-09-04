# Instalação e Configuração do WSL2 e JetBrains Toolbox no WSL

## 1. Pré-requisitos

Primeiro de tudo, você precisa ter o [WSL2 instalado e configurado](https://learn.microsoft.com/pt-br/windows/wsl/). Além disso, você pode ajustar as configurações de recurso do seu WSL no arquivo de texto `.wslconfig` (em `C:\Users\UserName`) e ajustar os parâmetros conforme necessário. Consulte a [documentação do WSL para mais detalhes](https://learn.microsoft.com/pt-br/windows/wsl/wsl-config).

### Exemplo de parâmetros:

```bash
# Configuração global do WSL
[wsl2]

# Limite da memória da VM
memory=4GB

# Quantidade de processadores virtuais
processors=2

# Usar o localhost do Windows
localhostforwarding=true

# Forçar os aplicativos que usam OpenGL a renderizar dentro do WSL
# Evita problemas com o Nautilus e outros programas que exigem renderização
LIBGL_ALWAYS_SOFTWARE=1
```

## 2. Atualizando o WSL

Com essas configurações feitas, abra o seu WSL e execute a atualização. Eu estarei usando o Ubuntu, e se você instalou o WSL com o comando `wsl --install`, você também estará.

```bash
sudo apt update
```

## 3. Instalando o Nautilus e o Fuse

Você precisará instalar o Nautilus (explorador de arquivos do Ubuntu) e o Fuse (ferramenta de execução). Consulte o [wiki do Fuse](https://github.com/AppImage/AppImageKit/wiki/FUSE) para mais informações.

```bash
sudo apt install nautilus
sudo apt install fuse
```

## 4. Baixando e Instalando o JetBrains Toolbox

Faça o download do [JetBrains Toolbox App](https://www.jetbrains.com/toolbox-app/). Escolha a opção `.tar.gz (Linux 64-bit x86)`.

O download será feito fora do WSL, então, será necessário mover o arquivo para o diretório do WSL. Você pode acessá-lo no Explorador de Arquivos do Windows em: `\\wsl.localhost\Ubuntu\home\UserName`.

### Extração do arquivo:

Após mover o arquivo para o Linux, execute os seguintes comandos para descompactar e extrair o arquivo:

```bash
sudo tar -xzf jetbrains-toolbox-2.4.2.32922.tar.gz -C /opt
```

Entre na pasta extraída e execute o programa:

```bash
cd /opt
cd jetbrains-toolbox-2.4.2.32922/
./jetbrains-toolbox
```

## 5. Executando o Toolbox

O **Toolbox** será aberto via _Nautilus_ (explorador do Ubuntu). Siga as instruções na interface gráfica (abrir, continuar, aceitar licença, escolher tema). A interface de instalação das IDEs estará disponível. É recomendável instalar as IDEs na versão **Community Edition** caso você não tenha a licença da versão Ultimate.

## 6. Criando Atalhos para Executar as IDEs no Windows

Após a instalação das IDEs, você pode criar atalhos para executá-las de forma mais prática no Windows. Para isso, copie os arquivos `.desktop` para um diretório onde o Windows possa identificá-los.

```bash
cd ~/.local/share/applications
sudo cp *.desktop /usr/share/applications
```

Agora, os atalhos estarão disponíveis, e os programas exibidos no Windows terão um ícone de pinguim 🐧.

## 7. Finalizando o Uso do WSL

**IMPORTANTE**: Sempre que terminar de utilizar o **espaço de desenvolvimento WSL**, abra o PowerShell e execute o seguinte comando:

```bash
wsl --shutdown
```

Isso interromperá o processo `Vmmem`, economizando recursos da sua máquina. Para uma melhor gestão de terminais, recomendo o uso do [Windows Terminal](https://apps.microsoft.com/detail/9n0dx20hk701?hl=pt-br&gl=BR).

### Agradecimentos

Vídeo do [CodaRam](https://www.youtube.com/watch?v=v-e8MRhNkmU) sobre o assunto, com as devidas alterações.