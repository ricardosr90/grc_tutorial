### Rádios Definidos por Software, 1s2022 - PPGEEC/Mackenzie

# Tutorial de instalação do UHD e do GNU Radio Companion

#### Por Prof. Dr. Cristiano Akamine (<cristiano.akamine@mackenzie.com.br>) e Ricardo Seriacopi Rabaça (ricardo_sr2@hotmail.com).

----

## <span style="color:red">*PRÉ-INSTALAÇÃO*</span>

#### **Ubuntu 18.04 LTS**
Antes de começar é importante atualizar o sistema, abrindo um terminal com “CTRL+T” e rodando os comandos:

```sh
sudo apt update
```
```sh
sudo apt upgrade
```

![update_image1.png](/images/update_image1.png)

![upgrade_image2.png](/home/ricardosr90/Documents/notes/images/upgrade_image2.png)

Também é necessário instalar as dependências para a versão do Ubuntu que estiver usando. 

> **Referência:**
https://wiki.gnuradio.org/index.php/UbuntuInstall#Install_Dependencies

Para `GRC 3.7` (*Python 2*): 
```sh
sudo apt install cmake git g++ libboost-all-dev python-dev \
python-mako python-numpy python3-numpy python-wxgtk3.0 python-sphinx \
python-cheetah swig libzmq3-dev libfftw3-dev libgsl-dev \
libcppunit-dev doxygen libcomedi-dev libqt4-opengl-dev python-qt4 \
libqwt-dev libsdl1.2-dev libusb-1.0-0-dev python-gtk2 python-lxml \
pkg-config python-sip-dev python-docutils python-requests \
python-ruamel.yaml python-setuptools python3-setuptools build-essential
```

Para `GRC 3.8` (*Python 3*): 
```sh
sudo apt install git cmake g++ libboost-all-dev libgmp-dev swig \
python3-numpy python3-mako python3-sphinx python3-lxml doxygen \
libfftw3-dev libsdl1.2-dev libgsl-dev libqwt-qt5-dev \
libqt5opengl5-dev python3-pyqt5 liblog4cpp5-dev libzmq3-dev \
python3-yaml python3-click python3-click-plugins python3-zmq \
python3-scipy libusb-1.0-0-dev python3-docutils python3-requests \
python3-ruamel.yaml python3-setuptools build-essential
```

#### **Ubuntu 20.04 LTS (Recomendado)**
Antes de começar é importante atualizar o sistema, abrindo um terminal com “CTRL+T” e rodando os comandos:

```sh
sudo apt update
```
```sh
sudo apt upgrade
```

![update_image3.png](/home/ricardosr90/Documents/notes/images/update_image3.png)

![upgrade_image4.png](/home/ricardosr90/Documents/notes/images/upgrade_image4.png)

Também é necessário instalar as dependências para a versão do Ubuntu que estiver usando. 

> **Referência:**
https://wiki.gnuradio.org/index.php/UbuntuInstall#Install_Dependencies

Para `GRC 3.8` (*Python 3*): 
```sh
sudo apt install git cmake g++ libboost-all-dev libgmp-dev swig \
python3-numpy python3-mako python3-sphinx python3-lxml doxygen \
libfftw3-dev libsdl1.2-dev libgsl-dev libqwt-qt5-dev libqt5opengl5-dev \
python3-pyqt5 liblog4cpp5-dev libzmq3-dev python3-yaml python3-click \
python3-click-plugins python3-zmq python3-scipy python3-docutils \
python3-requests python3-ruamel.yaml python3-setuptools \
build-essential libusb-1.0-0-dev
```

Para `GRC 3.9` (*Python 3*): 
```sh
sudo apt install git cmake g++ libboost-all-dev libgmp-dev swig \
python3-numpy python3-mako python3-sphinx python3-lxml doxygen \
libfftw3-dev libsdl1.2-dev libgsl-dev libqwt-qt5-dev \
libqt5opengl5-dev python3-pyqt5 liblog4cpp5-dev libzmq3-dev \
python3-yaml python3-click python3-click-plugins python3-zmq \
python3-scipy python3-docutils python3-requests python3-ruamel.yaml \
python3-setuptools build-essential libusb-1.0-0-dev pybind11-dev \
python3-matplotlib libsndfile1-dev libiio-dev libad9361-dev \
libsoapysdr-dev soapysdr-tools
```

----

## <span style="color:red">*INSTALAÇÃO*</span>

Existem três formas de instalar o GRC no Ubuntu:

* Pelos arquivos binários;
* Diretamente pelo código fonte;
* Usando o PyBombs.

----
### **INSTALAÇÃO USANDO OS ARQUIVOS BINÁRIOS**

A primeira opção de instalação é a mais simples e rápida, mas também tem o ponto negativo de não te dar acesso total ao conteúdo dos módulos nativos do GNU Radio Companion (GRC). Sendo assim, o usuário pode utilizar todos os blocos fornecidos junto com o programa (incluindo os exemplos de uso), porém, não são criados os arquivos locais contendo a pasta “lib” (com os arquivos .cc e .h). Este método já instala também o UHD e o VOLK.

Para instalar por este método é necessário seguir os passos descritos abaixo:

#### ***Ubuntu 18.04 LTS***

1. Caso já tenha instalado alguma versão anterior do GRC, é preciso desinstalar ela e retirar o PPA (*Personal Package Archives*, os repositórios deste tipo nada mais são do que servidores na internet onde se encontram os programas que não estão nos repositórios oficias da sua distribuição Linux) dela das configurações do sistema (Ubuntu). Informações sobre a desinstalação no final deste primeiro método;
2. Utilize o comando

```sh
sudo add-apt-repository ppa:gnuradio/gnuradio-master
```

> **Nota:**
> Para a última versão colocada no ramo “master” do Github. 
>
> **Atualização:**
> *Agosto/2021*: o GRC não é instalado e aparecem diversos erros no terminal.

ou o

```sh
sudo add-apt-repository ppa:gnuradio/gnuradio-releases
```

> **Nota:**
> Para a versão mais recente.
> **Atualização:**
> *Agosto/2021*: é instalada a versão 3.8.2 do GRC. Foi instalada a versão 3.10 do UHD automaticamente.

ou o

```sh
sudo add-apt-repository ppa:gnuradio/gnuradio-releases-3.8
```

> **Nota:**
> Para a última atualização da versão 3.8 do GRC.
> **Atualização:**
> *Agosto/2021*: é instalada a versão 3.8.3 do GRC. Foi instalada a versão 3.10 do UHD automaticamente.

ou o

```sh
sudo add-apt-repository ppa:gnuradio/gnuradio-releases-3.7
```

> **Nota:**
> Para a última atualização da versão 3.7 do GRC.
> **Atualização:**
> *Agosto/2021*: é instalada a versão 3.7.13.5 do GRC. Foi instalada a versão 3.10 do UHD automaticamente.

para adicionar o PPA desejado do GRC. 

Dessa forma, além de ser possível instalar uma versão do GRC apenas usando o APT (*Advanced Packaging Tool*), o PPA garante que o sistema buscará atualizações do programa quando o Ubuntu rodar o *Software Updater* ou caso seja digitada no terminal a sequência de comandos

```sh
sudo apt update
```
```sh
sudo apt upgrade
```

![add_ppa_image5.png](/home/ricardosr90/Documents/notes/images/add_ppa_image5.png)

3. Depois de adicionado o repositório desejado, é preciso rodar o comando 

```sh
sudo apt update
```
para atualizar a base de dados do APT;

4. Por fim, já é possível rodar o comando 

```sh
sudo apt install gnuradio
```
Esta etapa precisa de um “y” de “yes”, para autorizar o download dos arquivos e a instalação. Tudo será instalado automaticamente. Ao término deste processo, já é possível abrir a interface gráfica do GRC rodando o comando

```sh
gnuradio-companion
```

![install_grc_image6.png](/home/ricardosr90/Documents/notes/images/install_grc_image6.png)

![open_grc_image7.png](/home/ricardosr90/Documents/notes/images/open_grc_image7.png)

![grc_37_image8.png](/home/ricardosr90/Documents/notes/images/grc_37_image8.png)

> ***Observação 1:*** 
Nesse tutorial foi utilizada a opção de instalar a versão estável (3.7) colocada no ramo “releases-3.7” do Github e, como pode ser visto no terminal de abertura do GRC, foi instalada a versão 3.7.13.5.

> ***Observação 2:***
Caso apareça algum erro relacionado ao *canberra* como, por exemplo, aparecer no log do GRC: `BadDrawable (invalid Pixmap or Window parameter)` e os blocos gráficos não funcionarem, siga estes passos: 
> Abra com o editor de texto o arquivo “environment”, usando o comando 

```sh
sudo gedit /etc/environment
```
> e no final do arquivo, adicione a linha `QT_X11_NO_MITSHM=1` e salve ele. Isso já deve fazer os blocos gráficos voltarem a funcionar, mas para remover o *warning* do canberra no terminal, também é preciso rodar o comando 

```sh
sudo apt install libcanberra-gtk-module
```

> <span style="color:red">***Informações adicionais:***</span>
Utilizando a opção

```sh
sudo add-apt-repository ppa:gnuradio/gnuradio-releases
```
> e rodando o comando 

```sh
sudo apt-cache policy gnuradio
```
> serão mostradas as opções de versões disponíveis no repositório, além daquela que é instalada automaticamente no `sudo apt install gnuradio` (que foi a 3.8.2.0). Neste caso, aparecereu também a opção de instalar a versão 3.7.11.

![cache_policy_grc_ubuntu18.png](/home/ricardosr90/Documents/notes/images/cache_policy_grc_ubuntu18.png)

Como pode ser visto no terminal, é possível forçar a instalação da versão `3.7.11-10`.

Para isso, adicione a versão no comando de instalação 

```sh
sudo apt install gnuradio=3.7.11-10
```

![grc_install_cache_policy_ubuntu18.png](/home/ricardosr90/Documents/notes/images/grc_install_cache_policy_ubuntu18.png)

![grc_install_cache_policy_about_ubuntu18.png](/home/ricardosr90/Documents/notes/images/grc_install_cache_policy_about_ubuntu18.png)

5. Em alguns casos, pode acontecer de surgirem problemas ao usar o `gr_modtool`, quando se faz uso deste tipo de instalação. Para solucionar este problema, é preciso acessar a pasta “gr-newmod” usando o comando 

```sh
cd usr/share/gnuradio/modtool/templates/gr-newmod
```
e depois rodar o comando 

```sh
sudo py3clean
```
dentro dela. *OBS:* Este problema não ocorre mais a partir do Ubuntu 19.

> **Referência:**
https://wiki.gnuradio.org/index.php/InstallingGR#From_Binaries

Para desinstalar o GRC, quando se usa o APT para instalar, é preciso rodar o comando 

```sh
sudo apt purge gnuradio
```

depois o 

```sh
sudo apt remove gnuradio
```

e, para desinstalar os pacotes instalados com o GRC, o comando 

```sh
sudo apt autoremove
```
Sempre lembrar de remover o PPA adicionado, abrindo o "Software & Updates" no menú do sistema e retirando o "check" do PPA do gnuradio, na aba "Other Software".

![remove_ppa_master.png](/home/ricardosr90/Documents/notes/images/remove_ppa_master.png)



#### ***Ubuntu 20.04 LTS (Recomandado)***

1. Caso já tenha instalado alguma versão anterior do GRC, é preciso desinstalar ela e retirar o PPA dela das configurações do sistema (Ubuntu). Informações sobre a desinstalação no final
deste primeiro método;

2. Utilize o comando

```sh
sudo add-apt-repository ppa:gnuradio/gnuradio-master
```
> **Nota:**
> Para a última versão colocada no ramo “master” do Github. 
>
> **Atualização:**
*Agosto/2021*: é instalada a versão 3.10 do GRC (ainda em desenvolvimento). Foi instalada a versão 3.15 do UHD automaticamente.

ou o

```sh
sudo add-apt-repository ppa:gnuradio/gnuradio-releases
```
> **Nota:**
Para a versão mais recente.
> **Atualização:**
*Agosto/2021*: é instalada a versão 3.9.2 do GRC. Foi instalada a versão 3.15 do UHD automaticamente.

ou o

```sh
sudo add-apt-repository ppa:gnuradio/gnuradio-releases-3.8
```
> **Nota:**
Para a última atualização da versão 3.8 do GRC.
> **Atualização:**
*Agosto/2021*: é instalada a versão 3.8.3 do GRC. Foi instalada a versão 3.15 do UHD automaticamente.

ou o

```sh
sudo add-apt-repository ppa:gnuradio/gnuradio-releases-3.7
```
> **Nota:**
Para a última atualização da versão 3.7 do GRC.
> **Atualização:**
*Agosto/2021*: não foi possível adicionar o PPA para a versão 3.7. O GRC 3.7 já é uma versão mais antiga, que funciona bem no Ubuntu 18.04 LTS. Existem incompatibilidades de bibliotecas e pacotes, que não permitem que essa versão seja instalada da forma correta no Ubuntu 20.04 LTS.

para adicionar o PPA desejado do GRC. 

Dessa forma, além de ser possível instalar uma versão do GRC apenas usando o APT (*Advanced Packaging Tool*), o PPA garante que o sistema buscará atualizações do programa quando o Ubuntu rodar o *Software Updater* ou caso seja digitada no terminal a sequência de comandos

```sh
sudo apt update
```
```sh
sudo apt upgrade
```

![add_ppa_releases.png](/home/ricardosr90/Documents/notes/images/add_ppa_releases.png)

3. Depois de adicionado o repositório desejado, é preciso rodar o comando 

```sh
sudo apt update
```
para atualizar a base de dados do APT;

4. Por fim, já é possível rodar o comando 

```sh
sudo apt install gnuradio
```
Esta etapa precisa de um “y” de “yes”, para autorizar o download dos arquivos e a instalação. Tudo será instalado automaticamente. Ao término deste processo, já é possível abrir a interface gráfica do GRC rodando o comando

```sh
gnuradio-companion
```

![grc_version_39.png](/home/ricardosr90/Documents/notes/images/grc_version_39.png)

![grc_version_about_39.png](/home/ricardosr90/Documents/notes/images/grc_version_about_39.png)

> ***Observação 1:*** 
> Nesse tutorial foi utilizada a opção de instalar a última versão do GRC 3.9 e, como pode ser visto no terminal de abertura do GRC, foi instalada a versão 3.9.2.0 (é preciso verificar no site do gnuradio, para saber se não é uma versão ainda em desenvolvimento). Neste momento, Agosto/2021, a última versão lançada foi a 3.9 (https://www.gnuradio.org/), então não é recomendado o uso da 3.10 ainda.

> ***Observação 2:***
Caso apareça algum erro relacionado ao *canberra* como, por exemplo, aparecer no log do GRC: `BadDrawable (invalid Pixmap or Window parameter)` e os blocos gráficos não funcionarem, siga estes passos: 
> Abra com o editor de texto o arquivo “environment”, usando o comando 

```sh
sudo gedit /etc/environment
```
> e no final do arquivo, adicione a linha `QT_X11_NO_MITSHM=1` e salve ele. Isso já deve fazer os blocos gráficos voltarem a funcionar, mas para remover o *warning* do canberra no terminal, também é preciso rodar o comando 

```sh
sudo apt install libcanberra-gtk-module
```


> <span style="color:red">***Informações adicionais:***</span>
Utilizando a opção 

```sh
sudo add-apt-repository ppa:gnuradio/gnuradio-releases
```

> e rodando o comando 

```sh
sudo apt-cache policy gnuradio
```

> serão mostradas as opções de versões disponíveis no repositório, além daquela que é instalada automaticamente no `sudo apt install gnuradio` (que foi a 3.9.2.0, neste caso).

![cache_policy_grc.png](/home/ricardosr90/Documents/notes/images/cache_policy_grc.png)

Como pode ser visto no terminal, é possível forçar a instalação da versão `3.8.1.0~rc1-2build2`.

Para isso, adicione a versão no comando de instalação 

```sh
sudo apt install gnuradio=3.8.1.0~rc1-2build2
```

![grc_install_cache_policy.png](/home/ricardosr90/Documents/notes/images/grc_install_cache_policy.png)

![grc_install_cache_policy_about.png](/home/ricardosr90/Documents/notes/images/grc_install_cache_policy_about.png)

5. Em alguns casos, pode acontecer de surgirem problemas ao usar o `gr_modtool`, quando se faz uso deste tipo de instalação. Para solucionar este problema, é preciso acessar a pasta “gr-newmod” usando o comando 

```sh
cd usr/share/gnuradio/modtool/templates/gr-newmod
```
e depois rodar o comando 

```sh
sudo py3clean
```
dentro dela. *OBS:* Este problema não ocorre mais a partir do Ubuntu 19.

> **Referência:**
https://wiki.gnuradio.org/index.php/InstallingGR#From_Binaries

Para desinstalar o GRC, quando se usa o APT para instalar, é preciso rodar o comando 

```sh
sudo apt purge gnuradio
```

depois o 

```sh
sudo apt remove gnuradio
```

e, para desinstalar os pacotes instalados com o GRC, o comando 

```sh
sudo apt autoremove
```
Sempre lembrar de remover o PPA adicionado, abrindo o "Software & Updates" no menú do sistema e retirando o "check" do PPA do gnuradio, na aba "Other Software".

![remove_ppa_master.png](/home/ricardosr90/Documents/notes/images/remove_ppa_master.png)

----
### **INSTALAÇÃO USANDO O CÓDIGO FONTE (MÉTODO RECOMENDADO)**

A segunda maneira de instalar o GRC é pelo código fonte, onde o usuário faz o download de uma pasta “gnuradio” que contém todos os arquivos e pastas dos módulos nativos do programa e instala o programa passo a passo pelo terminal. 

> ***Nota:***
Este processo é um pouco mais demorado que o anterior. Porém, te dá controle total durante a instalação e te dá acesso aos códigos destes blocos nativos e também aos exemplos de *flow graph* disponibilizados pelo próprio GRC.

> <span style="color:red">***Informações iniciais:***</span>
> - O GRC será instalado por padrão no diretório `/usr/local`;
> - Desenvolver e rodar módulos e blocos no GRC, não requer que ele seja instalado pelo código fonte;
> - Se a distribuição utilizada for o Ubuntu, é preciso instalar algumas dependências e alguns pré-requisitos (https://wiki.gnuradio.org/index.php/UbuntuInstall#Install_the_Prerequisites);
> - Se o usuário tiver a intenção de usar o GRC com uma USRP (SDR), é obrigatório instalar o UHD antes de iniciar a instalação do GRC;
> - É possível instalar o GRC numa Raspberry Pi também (https://wiki.gnuradio.org/index.php/InstallingGRFromSource_on_Raspberry_Pi).


#### ***Ubuntu 18.04 LTS***

1. Siga os passos iniciais descritos na parte de Pré-instalação, localizada no início deste tutorial;
2. Para as versões 3.7 e 3.8 do GRC, a biblioteca VOLK (Vector Optimized Library of Kernels) ainda é considerada como um submodulo do próprio GRC. Sendo assim, não é necessária a instalação individual do VOLK antes do UHD e do GRC. Já para versão 3.9, é necessária a  instalação prévia e de forma separada do VOLK;
3. Como a versão 3.9 necessita de adaptações que dificultam a instalação no Ubuntu 18 (*pybind11*), este tutorial abordará a instalação completa das versões 3.7 e 3.8 do GRC;

##### <span style="color:orange">**Procedimento para o GRC 3.7 e para o GRC 3.8**</span>



<span style="color:green">***Instalando o UHD:***</span>

1. Crie uma pasta chamada “src” ou “source” dentro da sua $HOME, abrindo um terminal com “CTRL+T” e rodando

```sh
mkdir src
```

2. Acesse essa nova pasta com o comando
```sh
cd src
```
e baixe a pasta com os arquivos para instalar o UHD com o comando

```sh
git clone https://github.com/EttusResearch/uhd.git
```

![mkdir_build_image15.png](/home/ricardosr90/Documents/notes/images/mkdir_build_image15.png)

3. Acesse a pasta “uhd” com
```sh
cd uhd
```
e rode o comando
```sh
git tag -l
```
para exibir no terminal todas as versões disponíveis para instalação (navegue pela lista usando as setas para cima e para baixo do teclado);

![git_tag_image16.png](/home/ricardosr90/Documents/notes/images/git_tag_image16.png)

4. Encontre na lista a versão estável mais recente, decore a numeração dela e digite "CTRL+Z" para fechar a lista;

![git_tag_image17.png](/home/ricardosr90/Documents/notes/images/git_tag_image17.png)

5. Volte até a pasta "uhd" novamente e selecione a versão que você quer instalar com o comando “git checkout”, por exemplo:
```sh
git checkout v3.15.0.0
```

> ***Observação 1:***
Foi testada a instalação da versão 4.0, mas ocorreram diversos problemas. Para essa versão mais antiga do Ubuntu, a 18.04, recomenda-se utilizar as versões 3.14 ou 3.15 do UHD.

![git_checkout_image18.png](/home/ricardosr90/Documents/notes/images/git_checkout_image18.png)

6. Entre na pasta “host” com o comando
```sh
cd host
```
e crie uma nova pasta dentro dela chamada “build”, usando

```sh
mkdir build
```

7. Acesse a pasta “build” com
```sh
cd build
```

e rode o comando 
```sh
cmake ../
```

![cmake_uhd_image19.png](/home/ricardosr90/Documents/notes/images/cmake_uhd_image19.png)

![cmake_uhd_image20.png](/home/ricardosr90/Documents/notes/images/cmake_uhd_image20.png)


8. Para finalizar, rode
```sh
make
```
> <span style="color:blue">***Nota especial:***</span>
Existe uma maneira de executar o comando "make" de forma mais rápida, utilizando mais de um núcleo do computador. Por padrão o comando será processado por apenas um núcleo, porém, é possível obter a informação da quantidade de núcleos disponíveis no computador e utilizá-los em conjunto para agilizar esta etapa da instalação.

> O processo consiste em usar um comando adicional antes da execução do "make".

> Utilize o comando

```sh
lscpu
```

> para saber quantos núcleos a sua máquina possui.

![lscpu_v2](/home/ricardosr90/Documents/notes/images/lscpu_v2.png)

> Utilizando a resposta do comando "lscpu", conforme a imagem anterior exibe, o número de núcleos disponíveis para o computador deste exemplo é 4 (CPU(s): 4). Portanto, é possível usar até quatro núcleos para executar o comando "make" e agilizar esta etapa. 
> Neste exemplo, foram usados 3 núcleos dos 4 disponíveis, como pode ser visto na imagem a seguir.

```sh
make -j3
```

> Para outra quantidade de núcleos, basta substituir o número que aparece depois do "-j", neste caso "3", pelo número de núcleos disponíveis na sua máquina. Recomenda-se deixar um núcleo disponível para as outras atividades do computador.

![make_j3](/home/ricardosr90/Documents/notes/images/make_j3.png)

depois o 

```sh
make test
```
para analisar se todas as etapas do “make” foram feitas sem erros e, por fim, o 
```sh
sudo make install
```
e o 

```sh
sudo ldconfig
```


> ***Observação 2:***
Esta etapa, além de um pouco demorada, também exibe diversos *warnings* no terminal. Desde que não ocorra nenhum erro que encerre o processo, está tudo dentro da normalidade.

![make_uhd_image21.png](/home/ricardosr90/Documents/notes/images/make_uhd_image21.png)

![make_install_uhd_image22.png](/home/ricardosr90/Documents/notes/images/make_install_uhd_image22.png)


9. Abra com o editor de texto o arquivo “.bashrc”, que fica oculto na pasta inicial “home”. Basta abrir o gerenciador de arquivos (files) e teclar “CTRL+H” e depois clicar com o botão direito do mouse para abrir o “.bashrc” com o editor de texto (gedit);

![edit_bashrc_image23.png](/home/ricardosr90/Documents/notes/images/edit_bashrc_image23.png)

10. Adicione a linha
```sh
export LD_LIBRARY_PATH=/usr/local/lib
```
no final do arquivo e salve. Caso o `LD_LIBRARY_PATH` já esteja configurado com um caminho, apenas adicione
```sh
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
```
e salve o arquivo;

![export_ld_library_path_image24.png](/home/ricardosr90/Documents/notes/images/export_ld_library_path_image24.png)


11. Também é necessário adicionar a mesma linha no arquivo `/etc/bash.bashrc`, rodando o comando
```sh
sudo gedit /etc/bash.bashrc
```
para abri-lo e adicionando depois da última linha o
```sh
export LD_LIBRARY_PATH=/usr/local/lib
```

![export_ld_library_path_image25.png](/home/ricardosr90/Documents/notes/images/export_ld_library_path_image25.png)


12. Para configurar o USB é necessário abrir um novo terminal e usar o comando
```sh
cd src/uhd/host/utils
```
para ir até a pasta “utils”. Na sequência, digite os comandos
```sh
sudo cp uhd-usrp.rules /etc/udev/rules.d
```
depois o
```sh
sudo udevadm control --reload-rules
```
e, por fim, o
```sh
sudo udevadm trigger
```

13. Acesse a pasta “build” novamente, abrindo um novo terminal e rodando o comando
```sh
cd src/uhd/host/build
```
Rode no terminal novamente o
```sh
sudo ldconfig
```
e teste o sucesso da instalação rodando
```sh
uhd_find_devices
```
sem nenhuma USRP estar conectada ao computador ainda. A mensagem *No UHD Devices Found* deverá aparecer;

![uhd_find_devices_image26.png](/home/ricardosr90/Documents/notes/images/uhd_find_devices_image26.png)

14. Para já deixar as *UHD FPGA Images* baixadas no computador, rode o comando
```sh
sudo uhd_images_downloader
```

![uhd_images_downloader_image27.png](/home/ricardosr90/Documents/notes/images/uhd_images_downloader_image27.png)

<span style="color:green">***Instalando o GNU Radio Companion:***</span>

1. Volte para a pasta “src” ou “source” dentro da sua $HOME rodando

```sh
cd && cd src
```
e baixe os arquivos do GRC com o comando

```sh
git clone https://github.com/gnuradio/gnuradio.git
```

![clone_grc_image28.png](/home/ricardosr90/Documents/notes/images/clone_grc_image28.png)

2. Acesse a pasta “gnuradio” com
```sh
cd gnuradio
```
e rode o comando
```sh
git tag -l
```
para exibir no terminal todas as versões disponíveis para instalação (navegue pela lista usando as setas para cima e para baixo do teclado);

![git_tag_image29.png](/home/ricardosr90/Documents/notes/images/git_tag_image29.png)

3. Encontre na lista a versão estável mais recente, decore a numeração dela e digite "CTRL+Z" para fechar a lista;

![git_tag_image30.png](/home/ricardosr90/Documents/notes/images/git_tag_image30.png)

4. Volte até a pasta “gnuradio” e selecione a versão que você quer instalar com o comando “git checkout”, por exemplo:
```sh
git checkout v3.7.14.0
```

![git_checkout_image31.png](/home/ricardosr90/Documents/notes/images/git_checkout_image31.png)

5. Rode o comando
```sh
git submodule update --init --recursive
```
para atualizar os sub-módulos;


![volk_submodule_image32.png](/home/ricardosr90/Documents/notes/images/volk_submodule_image32.png)


6. Crie uma nova pasta chamada “build”, usando
```sh
mkdir build
```

7. Acesse a pasta “build” com 
```sh
cd build
```
e rode o comando
```sh
cmake ../
```

![cmake_grc_image33.png](/home/ricardosr90/Documents/notes/images/cmake_grc_image33.png)

![cmake_grc_image34.png](/home/ricardosr90/Documents/notes/images/cmake_grc_image34.png)

8. Para finalizar, rode
```sh
make
```


> <span style="color:blue">***Nota especial:***</span>
Existe uma maneira de executar o comando "make" de forma mais rápida, utilizando mais de um núcleo do computador. Por padrão o comando será processado por apenas um núcleo, porém, é possível obter a informação da quantidade de núcleos disponíveis no computador e utilizá-los em conjunto para agilizar esta etapa da instalação.

> O processo consiste em usar um comando adicional antes da execução do "make".

> Utilize o comando

```sh
lscpu
```

> para saber quantos núcleos a sua máquina possui.

![lscpu_v2](/home/ricardosr90/Documents/notes/images/lscpu_v2.png)

> Utilizando a resposta do comando "lscpu", conforme a imagem anterior exibe, o número de núcleos disponíveis para o computador deste exemplo é 4 (CPU(s): 4). Portanto, é possível usar até quatro núcleos para executar o comando "make" e agilizar esta etapa. 
> Neste exemplo, foram usados 3 núcleos dos 4 disponíveis, como pode ser visto na imagem a seguir.

```sh
make -j3
```

> Para outra quantidade de núcleos, basta substituir o número que aparece depois do "-j", neste caso "3", pelo número de núcleos disponíveis na sua máquina. Recomenda-se deixar um núcleo disponível para as outras atividades do computador.

![make_j3](/home/ricardosr90/Documents/notes/images/make_j3.png)


depois o 

```sh
make test
```
para analisar se todas as etapas do “make” foram feitas sem erros e, por fim, o 
```sh
sudo make install
```
e o 

```sh
sudo ldconfig
```

> ***Observação 1:***
Esta etapa, além de um pouco demorada, também exibe diversos *warnings* no terminal. Desde que não ocorra nenhum erro que encerre o processo, está tudo dentro da normalidade.

![make_grc_image35.png](/home/ricardosr90/Documents/notes/images/make_grc_image35.png)

![make_grc_image36.png](/home/ricardosr90/Documents/notes/images/make_grc_image36.png)


A partir deste ponto já é possível rodar em um novo terminal 
```sh
gnuradio-companion
```
para ver se o programa abre corretamente.

![open_grc_image37.png](/home/ricardosr90/Documents/notes/images/open_grc_image37.png)


> ***Observação 2:***
Caso apareça que existe erro no `PYTHONPATH` e no `LD_LIBRARY_PATH`, é só seguir estes passos adicionais (<span style="color:red">**Referência**</span>:
<https://wiki.gnuradio.org/index.php/ModuleNotFoundError#B._Finding_the_Python_library>):

![pythonpath_error_image38.png](/home/ricardosr90/Documents/notes/images/pythonpath_error_image38.png)

9. Rode
```sh
gnuradio-config-info --prefix
```
no terminal para saber qual é o seu prefixo de instalação (exemplo: `/usr/local`);

10. Agora encontre a sua biblioteca *Python* com
```sh
find {your-prefix} -name gnuradio | grep "packages"
```
Por exemplo:
```sh
find /usr/local -name gnuradio | grep "packages"
```

![grc_folder_image39.png](/home/ricardosr90/Documents/notes/images/grc_folder_image39.png)


11. Configure o `PYTHONPATH` e o `LD_LIBRARY_PATH` dentro do arquivo `/.bashrc`. Para encontrar esse arquivo é preciso abrir o gerenciador de arquivos na `$HOME` e pressionar as teclas “CTRL+H” para exibir os arquivos e pastas ocultos. Abra o `.bashrc`, clicando no arquivo com o
botão direito do mouse e selecionando a opção “abrir com editor de texto”. Vá até o final do conteúdo do arquivo e adicione as duas linhas responsáveis pela exportação do `PYTHONPATH` e do `LD_LIBRARY_PATH`;

![export_ld_library_path_image40.png](/home/ricardosr90/Documents/notes/images/export_ld_library_path_image40.png)

> ***Observação 3:***
Exemplo das linhas que devem ser adicionadas:

```sh
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
export PYTHONPATH=/usr/local/lib/python2.7/dist-packages:/usr/local/lib/python2.7/site-packages:$PYTHONPATH
```

> ***Observação 4:***
Caso a linha referente ao `LD_LIBRARY_PATH` já esteja no arquivo (por ter sido adicionada na instalação do UHD), adicione apenas a do `PYTHONPATH`.

12. Caso o seu prefixo não seja `/usr/local`, é só substituir este pedaço nas linhas acima;

![export_ld_library_path_image41.png](/home/ricardosr90/Documents/notes/images/export_ld_library_path_image41.png)

13. Salve o arquivo “.bashrc” e rode no terminal (dentro da pasta "build")
```sh
sudo ldconfig
```

14. Rode
```sh
gnuradio-companion
```
em um novo terminal e veja se o programa abre normalmente;


15. Faça um teste rodando o exemplo `dial_tone.grc`, para saber se está tudo funcionando corretamente (caminho do arquivo pode ser visto na imagem abaixo). Execute o *flow graph* e verifique se, além de rodar normalmente, ele também emite som durante a execução.

![test_grc_image42.png](/home/ricardosr90/Documents/notes/images/test_grc_image42.png)

![test_grc_image43.png](/home/ricardosr90/Documents/notes/images/test_grc_image43.png)

![test_grc_image44.png](/home/ricardosr90/Documents/notes/images/test_grc_image44.png)


> ***Observação 5:***
Caso apareça algum erro relacionado ao *canberra* como, por exemplo, aparecer no log do GRC: `BadDrawable (invalid Pixmap or Window parameter)` e os blocos gráficos não funcionarem, siga estes passos: 
> Abra com o editor de texto o arquivo “environment”, usando o comando 

```sh
sudo gedit /etc/environment
```
> e no final do arquivo, adicione a linha `QT_X11_NO_MITSHM=1` e salve ele. Isso já deve fazer os blocos gráficos voltarem a funcionar, mas para remover o *warning* do canberra no terminal, também é preciso rodar o comando 

```sh
sudo apt install libcanberra-gtk-module
```

> <span style="color:red">***Informações adicionais:***</span>
Foi testada também a opção de instalar a versão 3.8 (usando estes mesmos passos) e tudo ocorreu da mesma forma e com os mesmos resultados. Vale ressaltar que a versão 3.8 já utiliza o *Python* 3, portanto, aqueles caminhos de correção dos problemas com o `PYTHONPATH` e o `LD_LIBRARY_PATH` ficam diferentes. Rodando o comando do passo **10**, será exibido o caminho correto.

____

#### ***Ubuntu 20.04 LTS (Recomendado)***

1. Siga os passos iniciais descritos na parte de Pré-instalação, localizada no início deste tutorial;

2. Para as versões 3.7 e 3.8 do GRC, a biblioteca VOLK (Vector Optimized Library of Kernels) ainda é considerada como um submodulo do próprio GRC. Sendo assim, não é necessária a instalação individual do VOLK antes do UHD e do GRC. Já para versão 3.9, é necessária a  instalação prévia e de forma separada do VOLK;

> ***Referência:***
https://wiki.gnuradio.org/index.php/InstallingGR#For_the_GNU_Radio_Master_Branch

3. Como a versão 3.10 ainda não foi lançada e a 3.7 não funciona no Ubuntu 20.04, este tutorial abordará a instalação completa das versões 3.8 e 3.9 do GRC;



##### <span style="color:orange">**Procedimento para o GRC 3.8**</span>



###### <span style="color:green">***Instalando o UHD***</span>

1. Crie uma pasta chamada “src” ou “source” dentro da sua $HOME, abrindo um terminal com “CTRL+T” e rodando
```sh
mkdir src
```

2. Acesse essa nova pasta com o comando

```sh
cd src
```
e baixe a pasta com os arquivos para instalar o UHD com o comando

```sh
git clone https://github.com/EttusResearch/uhd.git
```

![clone_uhd_image45.png](/home/ricardosr90/Documents/notes/images/clone_uhd_image45.png)

3. Acesse a pasta “uhd” com
```sh
cd uhd
```
e rode o comando
```sh
git tag -l
```
para exibir no terminal todas as versões disponíveis para instalação (navegue pela lista usando as setas para cima e para baixo do teclado);

4. Encontre na lista a versão estável mais recente, decore a numeração dela e digite "CTRL+Z" para fechar a lista;

![git_tag_image46.png](/home/ricardosr90/Documents/notes/images/git_tag_image46.png)

5. Volte até a pasta "uhd" novamente e selecione a versão que você quer instalar com o comando “git checkout”, por exemplo:
```sh
git checkout v4.0.0.0
```

> ***Observação 1:***
Foi testada a instalação das versões 3.15 e 4.1 e também funcionaram. Recomenda-se utilizar as versões mais recentes do UHD.

![git_checkout_image47.png](/home/ricardosr90/Documents/notes/images/git_checkout_image47.png)

6. Entre na pasta “host” com o comando
```sh
cd host
```
e crie uma nova pasta dentro dela chamada “build”, usando

```sh
mkdir build
```

7. Acesse a pasta “build” com
```sh
cd build
```

e rode o comando 
```sh
cmake ../
```

![cmake_uhd_image48.png](/home/ricardosr90/Documents/notes/images/cmake_uhd_image48.png)

![cmake_uhd_image49.png](/home/ricardosr90/Documents/notes/images/cmake_uhd_image49.png)


8. Para finalizar, rode
```sh
make
```


> <span style="color:blue">***Nota especial:***</span>
Existe uma maneira de executar o comando "make" de forma mais rápida, utilizando mais de um núcleo do computador. Por padrão o comando será processado por apenas um núcleo, porém, é possível obter a informação da quantidade de núcleos disponíveis no computador e utilizá-los em conjunto para agilizar esta etapa da instalação.

> O processo consiste em usar um comando adicional antes da execução do "make".

> Utilize o comando

```sh
lscpu
```

> para saber quantos núcleos a sua máquina possui.

![lscpu_v2](/home/ricardosr90/Documents/notes/images/lscpu_v2.png)

> Utilizando a resposta do comando "lscpu", conforme a imagem anterior exibe, o número de núcleos disponíveis para o computador deste exemplo é 4 (CPU(s): 4). Portanto, é possível usar até quatro núcleos para executar o comando "make" e agilizar esta etapa. 
> Neste exemplo, foram usados 3 núcleos dos 4 disponíveis, como pode ser visto na imagem a seguir.

```sh
make -j3
```

> Para outra quantidade de núcleos, basta substituir o número que aparece depois do "-j", neste caso "3", pelo número de núcleos disponíveis na sua máquina. Recomenda-se deixar um núcleo disponível para as outras atividades do computador.

![make_j3](/home/ricardosr90/Documents/notes/images/make_j3.png)


depois o 

```sh
make test
```
para analisar se todas as etapas do “make” foram feitas sem erros e, por fim, o 
```sh
sudo make install
```
e o 

```sh
sudo ldconfig
```

> ***Observação 2:***
Esta etapa, além de um pouco demorada, também exibe diversos *warnings* no terminal. Desde que não ocorra nenhum erro que encerre o processo, está tudo dentro da normalidade.

![make_uhd_image50.png](/home/ricardosr90/Documents/notes/images/make_uhd_image50.png)

![make_uhd_image51.png](/home/ricardosr90/Documents/notes/images/make_uhd_image51.png)


9. Abra com o editor de texto o arquivo “.bashrc”, que fica oculto na pasta inicial “home”. Basta abrir o gerenciador de arquivos (files) e teclar “CTRL+H” e depois clicar com o botão direito do mouse para abrir o “.bashrc” com o editor de texto (gedit);

![edit_bashrc_image52.png](/home/ricardosr90/Documents/notes/images/edit_bashrc_image52.png)

10. Adicione a linha
```sh
export LD_LIBRARY_PATH=/usr/local/lib
```
no final do arquivo e salve. Caso o `LD_LIBRARY_PATH` já esteja configurado com um caminho, apenas adicione
```sh
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
```
e salve o arquivo;

![edit_bashrc_image53.png](/home/ricardosr90/Documents/notes/images/edit_bashrc_image53.png)


11. Também é necessário adicionar a mesma linha no arquivo `/etc/bash.bashrc`, rodando o comando
```sh
sudo gedit /etc/bash.bashrc
```
para abri-lo e adicionando depois da última linha o
```sh
export LD_LIBRARY_PATH=/usr/local/lib
```

![export_ld_library_path_image54.png](/home/ricardosr90/Documents/notes/images/export_ld_library_path_image54.png)


12. Para configurar o USB é necessário abrir um novo terminal e usar o comando
```sh
cd src/uhd/host/utils
```
para ir até a pasta “utils”. Na sequência, digite os comandos
```sh
sudo cp uhd-usrp.rules /etc/udev/rules.d
```
depois o
```sh
sudo udevadm control --reload-rules
```
e, por fim, o
```sh
sudo udevadm trigger
```

13. Acesse a pasta “build” novamente, abrindo um novo terminal e rodando o comando
```sh
cd src/uhd/host/build
```
Rode no terminal novamente o
```sh
sudo ldconfig
```
e teste o sucesso da instalação rodando
```sh
uhd_find_devices
```
sem nenhuma USRP estar conectada ao computador ainda. A mensagem *No UHD Devices Found* deverá aparecer;

![uhd_find_devices_image55.png](/home/ricardosr90/Documents/notes/images/uhd_find_devices_image55.png)

14. Para já deixar as *UHD FPGA Images* baixadas no computador, rode o comando
```sh
sudo uhd_images_downloader
```

![uhd_images_downloader_image56.png](/home/ricardosr90/Documents/notes/images/uhd_images_downloader_image56.png)

###### <span style="color:green">***Instalando o GNU Radio Companion***</span>

1. Volte para a pasta “src” ou “source” dentro da sua $HOME rodando

```sh
cd && cd src
```
e baixe os arquivos do GRC com o comando

```sh
git clone https://github.com/gnuradio/gnuradio.git
```

![clone_grc_image57.png](/home/ricardosr90/Documents/notes/images/clone_grc_image57.png)

2. Acesse a pasta “gnuradio” com
```sh
cd gnuradio
```
e rode o comando
```sh
git tag -l
```
para exibir no terminal todas as versões disponíveis para instalação (navegue pela lista usando as setas para cima e para baixo do teclado);


3. Encontre na lista a versão estável mais recente, decore a numeração dela e digite "CTRL+Z" para fechar a lista;

![git_tag_image58.png](/home/ricardosr90/Documents/notes/images/git_tag_image58.png)

4. Volte até a pasta “gnuradio” e selecione a versão que você quer instalar com o comando “git checkout”, por exemplo:
```sh
git checkout v3.8.2.0
```

![git_checkout_image59.png](/home/ricardosr90/Documents/notes/images/git_checkout_image59.png)

5. Rode o comando
```sh
git submodule update --init --recursive
```
para atualizar os sub-módulos;


6. Crie uma nova pasta chamada “build”, usando
```sh
mkdir build
```

7. Acesse a pasta “build” com 
```sh
cd build
```
e rode o comando
```sh
cmake -DCMAKE_BUILD_TYPE=Release -DPYTHON_EXECUTABLE=/usr/bin/python3 ../
```

![cmake_grc_image60.png](/home/ricardosr90/Documents/notes/images/cmake_grc_image60.png)

![cmake_grc_image61.png](/home/ricardosr90/Documents/notes/images/cmake_grc_image61.png)

8. Para finalizar, rode
```sh
make
```

> <span style="color:blue">***Nota especial:***</span>
Existe uma maneira de executar o comando "make" de forma mais rápida, utilizando mais de um núcleo do computador. Por padrão o comando será processado por apenas um núcleo, porém, é possível obter a informação da quantidade de núcleos disponíveis no computador e utilizá-los em conjunto para agilizar esta etapa da instalação.

> O processo consiste em usar um comando adicional antes da execução do "make".

> Utilize o comando

```sh
lscpu
```

> para saber quantos núcleos a sua máquina possui.

![lscpu_v2](/home/ricardosr90/Documents/notes/images/lscpu_v2.png)

> Utilizando a resposta do comando "lscpu", conforme a imagem anterior exibe, o número de núcleos disponíveis para o computador deste exemplo é 4 (CPU(s): 4). Portanto, é possível usar até quatro núcleos para executar o comando "make" e agilizar esta etapa. 
> Neste exemplo, foram usados 3 núcleos dos 4 disponíveis, como pode ser visto na imagem a seguir.

```sh
make -j3
```

> Para outra quantidade de núcleos, basta substituir o número que aparece depois do "-j", neste caso "3", pelo número de núcleos disponíveis na sua máquina. Recomenda-se deixar um núcleo disponível para as outras atividades do computador.

![make_j3](/home/ricardosr90/Documents/notes/images/make_j3.png)


depois o 
```sh
make test
```
para analisar se todas as etapas do “make” foram feitas sem erros e, por fim, o 
```sh
sudo make install
```
e o 

```sh
sudo ldconfig
```

![make_grc_image62.png](/home/ricardosr90/Documents/notes/images/make_grc_image62.png)

> ***Observação 1:***
Esta etapa, além de um pouco demorada, também exibe diversos *warnings* no terminal. Desde que não ocorra nenhum erro que encerre o processo, está tudo dentro da normalidade.


A partir deste ponto já é possível rodar em um novo terminal 
```sh
gnuradio-companion
```
para ver se o programa abre corretamente.


> ***Observação 2:***
Caso apareça que existe erro no `PYTHONPATH` e no `LD_LIBRARY_PATH`, é só seguir estes passos adicionais (<span style="color:red">**Referência**</span>:
<https://wiki.gnuradio.org/index.php/ModuleNotFoundError#B._Finding_the_Python_library>):

![pythonpath_error_image38.png](/home/ricardosr90/Documents/notes/images/pythonpath_error_image38.png)

9. Rode
```sh
gnuradio-config-info --prefix
```
no terminal para saber qual é o seu prefixo de instalação (exemplo: `/usr/local`);

10. Agora encontre a sua biblioteca *Python* com
```sh
find {your-prefix} -name gnuradio | grep "packages"
```
Por exemplo:
```sh
find /usr/local -name gnuradio | grep "packages"
```

![grc_folder_image63.png](/home/ricardosr90/Documents/notes/images/grc_folder_image63.png)


11. Configure o `PYTHONPATH` e o `LD_LIBRARY_PATH` dentro do arquivo `/.bashrc`. Para encontrar esse arquivo é preciso abrir o gerenciador de arquivos na `$HOME` e pressionar as teclas “CTRL+H” para exibir os arquivos e pastas ocultos. Abra o `.bashrc`, clicando no arquivo com o
botão direito do mouse e selecionando a opção “abrir com editor de texto”. Vá até o final do conteúdo do arquivo e adicione as duas linhas responsáveis pela exportação do `PYTHONPATH` e do `LD_LIBRARY_PATH`;


> ***Observação 3:***
Exemplo das linhas que devem ser adicionadas:

```sh
export PYTHONPATH=/usr/local/lib/python3/dist-packages:/usr/local/lib/python3/site-packages:$PYTHONPATH
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
```

> ***Observação 4:***
Caso a linha referente ao `LD_LIBRARY_PATH` já esteja no arquivo (por ter sido adicionada na instalação do UHD), adicione apenas a do `PYTHONPATH`.

12. Caso o seu prefixo não seja `/usr/local`, é só substituir este pedaço nas linhas acima;

![export_ld_library_path_image64.png](/home/ricardosr90/Documents/notes/images/export_ld_library_path_image64.png)

13. Salve o arquivo “.bashrc” e rode no terminal (dentro da pasta "build")
```sh
sudo ldconfig
```

14. Rode
```sh
gnuradio-companion
```
em um novo terminal e veja se o programa abre normalmente;

![open_grc_image65.png](/home/ricardosr90/Documents/notes/images/open_grc_image65.png)

15. Faça um teste rodando o exemplo `dial_tone.grc`, para saber se está tudo funcionando corretamente (caminho do arquivo pode ser visto na imagem abaixo). Execute o *flow graph* e verifique se, além de rodar normalmente, ele também emite som durante a execução.

![test_grc_image42.png](/home/ricardosr90/Documents/notes/images/test_grc_image42.png)

![test_grc_image66.png](/home/ricardosr90/Documents/notes/images/test_grc_image66.png)


> ***Observação 5:***
Caso apareça algum erro relacionado ao *canberra* como, por exemplo, aparecer no log do GRC: `BadDrawable (invalid Pixmap or Window parameter)` e os blocos gráficos não funcionarem, siga estes passos: 
> Abra com o editor de texto o arquivo “environment”, usando o comando 

```sh
sudo gedit /etc/environment
```
> e no final do arquivo, adicione a linha `QT_X11_NO_MITSHM=1` e salve ele. Isso já deve fazer os blocos gráficos voltarem a funcionar, mas para remover o *warning* do canberra no terminal, também é preciso rodar o comando 

```sh
sudo apt install libcanberra-gtk-module
```



##### <span style="color:orange">**Procedimento para o GRC 3.9:**</span>



###### <span style="color:green">***Instalando o UHD***</span>

A instalação do UHD é feita da mesma forma nas versões 3.8 e 3.9 do GRC. Portanto, pode-se seguir os mesmos 14 passos de instalação mostrados na seção ***Procedimento para o GRC 3.8***.

> ***Nota:***
> Após a instalação do UHD, para o `GRC 3.9`, é necessária a instalação individual do VOLK, já que ele não é mais um sub-módulo do GRC.



###### <span style="color:green">***Instalando o VOLK***</span>



1. Volte para a pasta “src” ou “source” dentro da sua $HOME rodando

```sh
cd && cd src
```

e baixe os arquivos do VOLK com o comando

```sh
 git clone --recursive https://github.com/gnuradio/volk.git
```

![git_clone_volk_grc39_u20.png](/home/ricardosr90/Documents/notes/images/git_clone_volk_grc39_u20.png)

2. Acesse a pasta “volk” com

```sh
cd volk
```

3. Crie uma nova pasta chamada “build”, usando

```sh
mkdir build
```

4. Acesse a pasta “build” com 

```sh
cd build
```

e rode o comando

```sh
cmake -DCMAKE_BUILD_TYPE=Release -DPYTHON_EXECUTABLE=/usr/bin/python3 ../
```

![cmake_volk_grc39_u20.png](/home/ricardosr90/Documents/notes/images/cmake_volk_grc39_u20.png)

![cmake_volk_grc39_u20_finish.png](/home/ricardosr90/Documents/notes/images/cmake_volk_grc39_u20_finish.png)

5. Para finalizar, rode

```sh
make
```



> <span style="color:blue">***Nota especial:***</span>
> Existe uma maneira de executar o comando "make" de forma mais rápida, utilizando mais de um núcleo do computador. Por padrão o comando será processado por apenas um núcleo, porém, é possível obter a informação da quantidade de núcleos disponíveis no computador e utilizá-los em conjunto para agilizar esta etapa da instalação.

> O processo consiste em usar um comando adicional antes da execução do "make".

> Utilize o comando

```sh
lscpu
```

> para saber quantos núcleos a sua máquina possui.

![lscpu_v2](/home/ricardosr90/Documents/notes/images/lscpu_v2.png)

> Utilizando a resposta do comando "lscpu", conforme a imagem anterior exibe, o número de núcleos disponíveis para o computador deste exemplo é 4 (CPU(s): 4). Portanto, é possível usar até quatro núcleos para executar o comando "make" e agilizar esta etapa. 
> Neste exemplo, foram usados 3 núcleos dos 4 disponíveis, como pode ser visto na imagem a seguir.

```sh
make -j3
```

> Para outra quantidade de núcleos, basta substituir o número que aparece depois do "-j", neste caso "3", pelo número de núcleos disponíveis na sua máquina. Recomenda-se deixar um núcleo disponível para as outras atividades do computador.

![make_j3](/home/ricardosr90/Documents/notes/images/make_j3.png)



depois o 

```sh
make test
```

para analisar se todas as etapas do “make” foram feitas sem erros e, por fim, o 

```sh
sudo make install
```

e o 

```sh
sudo ldconfig
```

![make_volk_grc39_u20.png](/home/ricardosr90/Documents/notes/images/make_volk_grc39_u20.png)



###### <span style="color:green">***Instalando o GNU Radio Companion***</span>

1. Volte para a pasta “src” ou “source” dentro da sua $HOME rodando

```sh
cd && cd src
```

e baixe os arquivos do GRC com o comando

```sh
git clone https://github.com/gnuradio/gnuradio.git
```

![git_clone_grc39_u20.png](/home/ricardosr90/Documents/notes/images/git_clone_grc39_u20.png)

2. Acesse a pasta “gnuradio” com

```sh
cd gnuradio
```

e rode o comando

```sh
git tag -l
```

para exibir no terminal todas as versões disponíveis para instalação (navegue pela lista usando as setas para cima e para baixo do teclado);


3. Encontre na lista a versão estável mais recente, decore a numeração dela e digite "CTRL+Z" para fechar a lista;

![git_tag_grc39_u20.png](/home/ricardosr90/Documents/notes/images/git_tag_grc39_u20.png)

4. Volte até a pasta “gnuradio” e selecione a versão que você quer instalar com o comando “git checkout”, por exemplo:

```sh
git checkout v3.9.2.0
```

![git_checkout_grc39_u20.png](/home/ricardosr90/Documents/notes/images/git_checkout_grc39_u20.png)


5. Crie uma nova pasta chamada “build”, usando

```sh
mkdir build
```

6. Acesse a pasta “build” com 

```sh
cd build
```

e rode o comando

```sh
cmake -DCMAKE_BUILD_TYPE=Release -DPYTHON_EXECUTABLE=/usr/bin/python3 ../
```

![cmake_grc39_u20.png](/home/ricardosr90/Documents/notes/images/cmake_grc39_u20.png)

7. Para finalizar, rode

```sh
make
```



> <span style="color:blue">***Nota especial:***</span>
> Existe uma maneira de executar o comando "make" de forma mais rápida, utilizando mais de um núcleo do computador. Por padrão o comando será processado por apenas um núcleo, porém, é possível obter a informação da quantidade de núcleos disponíveis no computador e utilizá-los em conjunto para agilizar esta etapa da instalação.

> O processo consiste em usar um comando adicional antes da execução do "make".

> Utilize o comando

```sh
lscpu
```

> para saber quantos núcleos a sua máquina possui.

![lscpu_v2](/home/ricardosr90/Documents/notes/images/lscpu_v2.png)

> Utilizando a resposta do comando "lscpu", conforme a imagem anterior exibe, o número de núcleos disponíveis para o computador deste exemplo é 4 (CPU(s): 4). Portanto, é possível usar até quatro núcleos para executar o comando "make" e agilizar esta etapa. 
> Neste exemplo, foram usados 3 núcleos dos 4 disponíveis, como pode ser visto na imagem a seguir.

```sh
make -j3
```

> Para outra quantidade de núcleos, basta substituir o número que aparece depois do "-j", neste caso "3", pelo número de núcleos disponíveis na sua máquina. Recomenda-se deixar um núcleo disponível para as outras atividades do computador.

![make_j3](/home/ricardosr90/Documents/notes/images/make_j3.png)



depois o 

```sh
make test
```

para analisar se todas as etapas do “make” foram feitas sem erros e, por fim, o 

```sh
sudo make install
```

e o 

```sh
sudo ldconfig
```

![make_grc39_u20_finish.png](/home/ricardosr90/Documents/notes/images/make_grc39_u20_finish.png)

> ***Observação 1:***
> Esta etapa, além de um pouco demorada, também exibe diversos *warnings* no terminal. Desde que não ocorra nenhum erro que encerre o processo, está tudo dentro da normalidade.


A partir deste ponto já é possível rodar em um novo terminal 

```sh
gnuradio-companion
```

para ver se o programa abre corretamente.


> ***Observação 2:***
> Caso apareça que existe erro no `PYTHONPATH` e no `LD_LIBRARY_PATH`, é só seguir estes passos adicionais (<span style="color:red">**Referência**</span>:
> <https://wiki.gnuradio.org/index.php/ModuleNotFoundError#B._Finding_the_Python_library>):

![pythonpath_error_image38.png](/home/ricardosr90/Documents/notes/images/pythonpath_error_image38.png)

8. Rode

```sh
gnuradio-config-info --prefix
```

no terminal para saber qual é o seu prefixo de instalação (exemplo: `/usr/local`);

9. Agora encontre a sua biblioteca *Python* com

```sh
find {your-prefix} -name gnuradio | grep "packages"
```

Por exemplo:

```sh
find /usr/local -name gnuradio | grep "packages"
```

![grc_folder_image63.png](/home/ricardosr90/Documents/notes/images/grc_folder_image63.png)


10. Configure o `PYTHONPATH` e o `LD_LIBRARY_PATH` dentro do arquivo `/.bashrc`. Para encontrar esse arquivo é preciso abrir o gerenciador de arquivos na `$HOME` e pressionar as teclas “CTRL+H” para exibir os arquivos e pastas ocultos. Abra o `.bashrc`, clicando no arquivo com o botão direito do mouse e selecionando a opção “abrir com editor de texto”. Vá até o final do conteúdo do arquivo e adicione as duas linhas responsáveis pela exportação do `PYTHONPATH` e do `LD_LIBRARY_PATH`;


> ***Observação 3:***
> Exemplo das linhas que devem ser adicionadas:

```sh
export PYTHONPATH=/usr/local/lib/python3/dist-packages:/usr/local/lib/python3/site-packages:$PYTHONPATH
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
```

> ***Observação 4:***
> Caso a linha referente ao `LD_LIBRARY_PATH` já esteja no arquivo (por ter sido adicionada na instalação do UHD), adicione apenas a do `PYTHONPATH`.

11. Caso o seu prefixo não seja `/usr/local`, é só substituir este pedaço nas linhas acima;

![export_ld_library_path_image64.png](/home/ricardosr90/Documents/notes/images/export_ld_library_path_image64.png)

12. Salve o arquivo “.bashrc” e rode no terminal (dentro da pasta "build")

```sh
sudo ldconfig
```

13. Rode

```sh
gnuradio-companion
```

em um novo terminal e veja se o programa abre normalmente;

![grc39_installed_u20.png](/home/ricardosr90/Documents/notes/images/grc39_installed_u20.png)

![grc39_about_u20.png](/home/ricardosr90/Documents/notes/images/grc39_about_u20.png)

14. Faça um teste rodando o exemplo `dial_tone.grc`, para saber se está tudo funcionando corretamente (caminho do arquivo pode ser visto na imagem abaixo). Execute o *flow graph* e verifique se, além de rodar normalmente, ele também emite som durante a execução.

![grc39_dial_tone_path_u20.png](/home/ricardosr90/Documents/notes/images/grc39_dial_tone_path_u20.png)

![grc39_dial_tone_executing_u20.png](/home/ricardosr90/Documents/notes/images/grc39_dial_tone_executing_u20.png)


> ***Observação 5:***
> Caso apareça algum erro relacionado ao *canberra* como, por exemplo, aparecer no log do GRC: `BadDrawable (invalid Pixmap or Window parameter)` e os blocos gráficos não funcionarem, siga estes passos: 
> Abra com o editor de texto o arquivo “environment”, usando o comando 

```sh
sudo gedit /etc/environment
```

> e no final do arquivo, adicione a linha `QT_X11_NO_MITSHM=1` e salve ele. Isso já deve fazer os blocos gráficos voltarem a funcionar, mas para remover o *warning* do canberra no terminal, também é preciso rodar o comando 

```sh
sudo apt install libcanberra-gtk-module
```






----
### **INSTALAÇÃO USANDO O PYBOMBS**

A terceira maneira de instalar o GRC é pelo Pybombs, que funciona como um método híbrido entre a instalação usando os arquivos binários e a usando o código fonte. Neste modelo, o próprio Pybombs já detecta o sistema operacional em uso e carrega diversas configurações. 

> ***Nota:***
> Este processo é um pouco demorado, como o anterior, mas é todo automatizado (o próprio Pybombs instala na sequência correta todos os componentes do sistema e deixa o GRC pronto para o uso). Além disso, esse método também te dá acesso aos códigos dos blocos nativos e também aos exemplos de *flow graph* disponibilizados pelo próprio GRC.


> ***Referência:***
> https://github.com/gnuradio/pybombs#pybombs

#### ***Ubuntu 18.04 LTS***

Os passos iniciais dos outros métodos também devem ser seguidos para este. Portanto, logo depois de instalar o Ubuntu, foi feito o *update*, o *upgrade* e também o comando para instalar as dependências do GRC (Pré-instalação).

> ***Nota inicial:***
> Foram feitas algumas tentativas de instalar o `GRC 3.7` por este método e surgiram muitos erros e problemas durante o processo de instalação e configuração. Sendo assim, este tutorial abordará a instalação do `GRC 3.8` no Ubuntu 18.04 LTS. O processo é idêntico no Ubuntu 20.04 LTS. 

###### <span style="color:green">***Instalando o PYBOMBS***</span>

1. Se já tiver uma versão do PYBOMBS instalada usando o *Python* 2, é preciso desinstalar com o comando
```sh
sudo pip uninstall pybombs
```

2. Caso não tenha o *Python* 3 instalado, rode os comandos
```sh
sudo apt install python3
```
e
```sh
sudo apt install python3-pip
```

3. Depois de tudo isso, instale o PYBOMBS com 
```sh
sudo pip3 install --upgrade git+https://github.com/gnuradio/pybombs.git
```
![install_pybombs_grc38_u18.png](/home/ricardosr90/Documents/notes/images/install_pybombs_grc38_u18.png)



###### <span style="color:green">***Instalando o GNU Radio Companion***</span>


1. Usando o Pybombs, é possível instalar a versão 3.8 chamada de `gnuradio-default`. Essa opção será usada nos próximos passos;

2. Crie uma pasta para a instalação do GRC, por exemplo, dentro da $HOME, uma pasta chamada `gnuradio`. Faça isso abrindo um terminal (CTRL+T) e digitando
```sh
mkdir gnuradio
```
e acesse a pasta com
```sh
cd gnuradio
```

![mkdir_grc_image68.png](/home/ricardosr90/Documents/notes/images/mkdir_grc_image68.png)


3. Configure o Pybombs com o comando
```sh
pybombs auto-config
```
e
```sh
pybombs recipes add-defaults
```

![pybombs_config_image69.png](/home/ricardosr90/Documents/notes/images/pybombs_config_image69.png)


4. Instale o GRC (versão 3.8) com
```sh
pybombs prefix init ~/gnuradio -R gnuradio-default
```

> ***Nota:***
Este processo é demorado, pois instala tanto o UHD e o VOLK, como o GRC.


![pybombs_grc_install_image70.png](/home/ricardosr90/Documents/notes/images/pybombs_grc_install_image70.png)

![pybombs_grc_install_image71.png](/home/ricardosr90/Documents/notes/images/pybombs_grc_install_image71.png)

![pybombs_finish_install_gr38_u18.png](/home/ricardosr90/Documents/notes/images/pybombs_finish_install_gr38_u18.png.png)

5. Após instalado, é possível abrir o GRC com o comando

```sh
pybombs run gnuradio-companion
```

![pybombs_run_grc38_u18.png](/home/ricardosr90/Documents/notes/images/pybombs_run_grc38_u18.png)

> ***Observação 1:***
> Para testar o funcionamento do GRC, abra a interface dele e abra um exemplo localizado em `~/gnuradio/src/gnuradio/gr-audio/examples/grc/dial_tone.grc`. Execute o *flow graph* e verifique se, além de rodar normalmente, ele também emite som durante a execução.

![pybombs_run_grc38_u18_example.png](/home/ricardosr90/Documents/notes/images/pybombs_run_grc38_u18_example.png)


5. Para verificar a versão instalada do UHD, utilize o comando

```sh
pybombs run uhd_find_devices
```
> **Atualização:**
> *Agosto/2021*: é instalada a versão 3.8.3 do GRC. Foi instalada a versão 3.15 do UHD automaticamente.

![pybombs_uhd_version_grc38_u18.png](/home/ricardosr90/Documents/notes/images/pybombs_uhd_version_grc38_u18.png)


> ***Observação 2:***
Caso apareça algum erro relacionado ao *canberra* como, por exemplo, aparecer no log do GRC: `BadDrawable (invalid Pixmap or Window parameter)` e os blocos gráficos não funcionarem, siga estes passos: 
> Abra com o editor de texto o arquivo “environment”, usando o comando 

```sh
sudo gedit /etc/environment
```
> e no final do arquivo, adicione a linha `QT_X11_NO_MITSHM=1` e salve ele. Isso já deve fazer os blocos gráficos voltarem a funcionar, mas para remover o *warning* do canberra no terminal, também é preciso rodar o comando 

```sh
sudo apt install libcanberra-gtk-module
```



> ***Observação 3:***
Caso apareça que existe erro no `PYTHONPATH` e no `LD_LIBRARY_PATH`, é só seguir estes passos adicionais (<span style="color:red">**Referência**</span>:
<https://wiki.gnuradio.org/index.php/ModuleNotFoundError#B._Finding_the_Python_library>):

![pybombs_pythonpath_image74.png](/home/ricardosr90/Documents/notes/images/pybombs_pythonpath_image74.png)


6. Configure o `LD_LIBRARY_PATH` dentro do arquivo `/.bashrc`. Para encontrar esse arquivo é preciso abrir o gerenciador de arquivos na `$HOME` e pressionar as teclas “CTRL+H” para exibir os arquivos e pastas ocultos. Abra o `.bashrc`, clicando no arquivo com o
botão direito do mouse e selecionando a opção “abrir com editor de texto”. Vá até o final do conteúdo do arquivo e adicione a linha responsável pela exportação do `LD_LIBRARY_PATH`;

![pybombs_export_ld_library_path_image75.png](/home/ricardosr90/Documents/notes/images/pybombs_export_ld_library_path_image75.png)


> ***Observação 3:***
Exemplo da linha que deve ser adicionada:

```sh
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
```


7. Rode
```sh
pybombs run gnuradio-companion
```
em um novo terminal e veja se o programa abre normalmente.





#### ***Ubuntu 20.04 LTS (Recomendado)***

Os passos iniciais dos outros métodos também devem ser seguidos para este. Portanto, logo depois de instalar o Ubuntu, foi feito o *update*, o *upgrade* e também o comando para instalar as dependências do GRC (Pré-instalação).

> ***Nota inicial:***
> Como o processo de instalação do GRC 3.8 por este método é idêntico ao utilizado para o Ubuntu 18.04 LTS, pode-se utilizar a sequência de passos da seção anterior.
