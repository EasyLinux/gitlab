# Gitlab

* Auteur : Serge NOEL
* Contact: serge.noel@easylinux.fr
* Version: 0.8
* Description: Gitlab est un système de gestion de version de sources complet. Il dispose d'une grande base installée. Ce playbook installe la version <ce|ee>

## Introduction

Ce playbook permet l'installation de gitlab sur un serveur.

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


## Fonctionnement

Le playbook effectue plusieurs rôles :
* update: mise à jour de CentOS
* gitlab: installation de Gitlab