# Gitlab

* Auteur : Serge NOEL
* Contact: serge.noel@easylinux.fr
* Version: 0.8
* Description: Gitlab est un système de gestion de version de sources complet. Il dispose d'une grande base installée. Ce playbook installe la version <ce|ee>

[[_TOC_]]
## Introduction

Ce playbook permet l'installation de gitlab sur un serveur. Pour une installation **from scratch** suivre ce lien

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
