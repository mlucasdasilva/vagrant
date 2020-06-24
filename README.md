# Scripts Vagrant

Scripts para Vagrant com Virtualbox

*Read this in other languages: [English](README.md), [Portugues-BR](README.pt-br.md)

Estes scripts foram executadas em desktop host windows10 com os pacotes Vagrant e VirtualBox instalados

Requisitos do seu desktop:
- Instale VirtualBox (utilizei a versao 6.1.4)
- Instale Git  (utilizei a versao 2.26.0 for windows 64 bits)
- Instale Vagrant (utilizei a versao 2.2.7)

Com todos os componentes instalados basta fazer...
Utilizando um prompt de comandos, como o cmd.exe no windows10, va para um diretorio de trabalho e faça um "git clone <...>"
Após baixar o repositório do github...
Vá para o subdiretório do projeto que deseja iniciar, por exemplo, vagrant/docker-swarm e execute um "vagrant up".

Ao final, você pode remover todas as VMs criadas utilizando "vagrant destroy -f"
