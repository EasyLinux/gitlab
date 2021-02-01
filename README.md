# Gitlab

* Auteur : Serge NOEL
* Contact: serge.noel@easylinux.fr
* Version: 0.8
* Description: Gitlab est un système de gestion de version de sources complet. Il dispose d'une grande base installée. Ce playbook installe la version <ce|ee>

Table des matières 
------------------
[[_TOC_]] (TOC)

## Introduction

Ce playbook permet l'installation de gitlab sur un serveur. Pour une installation **from scratch** suivre [ce lien](#installation-from-scratch) 

## Configuration du playbook

Pour lancer le playbook, il convient de créer un fichier var.yaml dont le contenu est repris ci-dessous.

* **domain**: est le nom dns du domaine 
* **fdqn_name**: est le nom de la machine
* **docker**: 
  * **true**: si l'installation doit utiliser un container docker (pas encore implémenté)
  * **false**: si l'installation se fait via les paquets

```yaml
# Definition du domaine windows
domain: <domaine.dns>
fdqn_name: <machine.domaine.dns>
# gitlab_version <gitlab-ce|gitlab-ee>  
gitlab_version: gitlab-ce
# Installation avec ou sans docker <false|true> 
docker: false
``` 

## Inventaire

Le fichier d'inventaire doit se nommer 'inventory' et contenir les éléments suivants :
```
[Gitlab]
  <adresse IP>
```

# Utilisation

Pour utiliser le playbook

* Créer un fichier *inventory* à la racine du projet
* Créer un fichier *var.yaml* à la racine du projet
* Faire un échange de clé ssh

```bash
$ ssh-keygen -t rsa
$ ssh-copy-id root@<machine cible>
``` 

* Lancer la commande

```bash
$ ansible-playbook Gitlab.yaml
```  

## Fonctionnement

Le playbook effectue plusieurs rôles :
* update: mise à jour de CentOS
* gitlab: installation de Gitlab

## Installation 'from scratch'

Pour utiliser ce playbook à partir de zéro, il convient de réaliser les étapes suivantes.

### Template

Utiliser un template, ou installer un serveur Linux (CentOS), avec les paquets suivant *openssh-server*,*python* 

### Disposer d'un poste de travail 

Il vous faut disposer d'un poste de travail capable de lancer des commandes *Ansible*. Un poste Linux est plus approprié.

### Installer *Ansible*

Suivant votre distribution, faire un 
```bash
yum install -y ansible git
```
ou
```bash
apt-get install -y ansible git 
```
### Récupérer les fichiers du dépôt

Se place dans un répoertoire, puis taper 

```bash 
git clone https://github.com/easylinux/gitlab.git 
cd gitlab
```

### Créer le fichier inventaire

```bash
cp inventory.sample inventory
vi inventory
```
Remplacer l'adresse IP par l'adresse de votre machine cible.
 
### Créer le fichier var.yaml

```bash
cp var.yaml.sample var.yaml
vi var.yaml
```

Ajouter le nom de domaine et le FDQN

### Echanger les clés SSH

```bash
ssh-keygen -t rsa
ssh-copy-id root@<ip>
```

### Lancer le play-book

```bash
ansible-playbook Gitlab.yaml
```

> **NB**: vous devez être dans le même répertoire que inventory pour lancer cette commande.



