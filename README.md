# Scripts Vagrant

Vagrant scripts for Virtualbox

*Leia em outras línguas: [English](README.md), [Portugues-BR](README.pt-br.md)

These scripts were executed in windows10 host with Vagrant and VirtualBox packages:

Requisites:
- Install VirtualBox (tested with version 6.1.4)
- Install Git  (tested with version 2.26.0 for windows 64 bits)
- Install Vagrant (tested with version 2.2.7)

With all components installed you just need to do...
Using some command line utilility, like cmd.exe in windows10, go to some workdir, do a "git clone <...>"
After download the the repository from github...
Go to the desired projet/stack subdir, eg: vagrant/docker-swarm-4nodes and then execute "vagrant up". 
You can also start just one specific VM with the command "vagrant up <<vm name>>", eg: "vagrant up sd_docker01"

In the end you can remove all VMs created with "vagrant destroy -f"
