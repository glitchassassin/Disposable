# Disposable VM's

This Repository is for providing a brief explanation on how to setup disposable development and red/blue team virtual environment. I will provide a Vagrant Base image of Ubuntu 18.04 LTS , as well as a Vagrant file so that you can pull down the base image that I created, and customize and repackage it to your liking. If you would like to create a base image based off of another distribution of Linux, here is a great article on doing so: https://www.sitepoint.com/create-share-vagrant-base-box/

---
## Requirements

* Basic understanding of Linux
* VirtualBox installed
* Vagrant installed
* Patience
---
## Preparing

#### Virtualbox
* VirtualBox Download: https://www.virtualbox.org/wiki/Downloads

#### Vagrant
* Vagrant Downloads: https://www.vagrantup.com/downloads.html

#### Ubuntu iso
* We will be using Ubuntu 18.04 LTS as our base image.

* Download link for the iso: http://releases.ubuntu.com/18.04.1/ubuntu-18.04.1-desktop-amd64.iso
---

## Using Vagrant to spin up a base image

At this point it is assumed that if you are reading this, you already have a basic understanding of VirtualBox and how to build a VM from an ISO. You will not need to know how to do this but it is advised to learn how to do so.

#### First clone down or download this repository
```
curl https://github.com/jck4/Disposable/archive/master.zip (Or just click)

git clone https://github.com/jck4/Disposable.git
```
#### Make the magic happen
From the same directory as this repository you should run.

```bash
vagrant up
```
This command will automatically download the base vagrant box, start it, and bring up the Ubuntu desktop. You can login to the desktop with the default password `vagrant`.
You can also ssh directly onto the box without a GUI with the command `vagrant ssh`.
From this point you can make whatever changes you want to this box and repackage it to have a fully customized ubuntu box setup exactly how you want it.

#### Bootstrapping the VM
If you don't want to add things and repackage the box, you can run inline or external bash scripts from the Vagrant file. You can throw any necessary apt packages that you may need into the `script.sh` file.

---

## Repackaging

#### On the VM run:

```bash
#This commands are to clean up all unnecessary files for the repackaging.
sudo apt-get autoremove
sudo apt-get clean
sudo dd if=/dev/zero of=/EMPTY bs=1M
sudo rm -f /EMPTY
sudo shutdown -h now
```

#### On your local run:

```bash
#This is to package the box
vagrant package --output newbox.box
# Feel free to replace newbox with whatever you want to name it.
vagrant box add newbox newbox.box
```

## Wrapping up
If Vagrant is something that you enjoy using, I suggest to check out the documenation on it. Vagrant is a very powerful tool for making hacker lives easier: https://www.vagrantup.com/docs/index.html
