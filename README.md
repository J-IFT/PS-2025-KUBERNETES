# PS-2025-KUBERNETES

*PS = Projet Scolaire*

## 📚 Projet Scolaire | Kubernetes

Avril Mai 2025

Groupe : Yasmine, Colas, Théo et Juliette

### 📌 Consignes du projet :

Projet déploiement applicatif dans Kubernetes
Date : 2024 / 2025
Mis à jour : 3/31/2025
Fichier source (Github)
Fichier source (Sourcehut)
Exporter en PDF
Installation du Cluster
Exercice
Mettre en place un petit cluster Kubernetes (1 control plane, 2 à 3 workers). On ne demande pas de déployer un vrai cluster de production !
En cas d’installation on-premise, installer un Load Balancer MetalLB via Helm.
Installer un IngressController, par exemple traefik ou ingress-nginx via Helm.
Lien
Pour plus d’information sur le déploiement d’un cluster Kubernetes, voir le projet dédié : https://www.avenel.pro/cours/docker/projet_install_kubernetes 🌎
Voir aussi la page https://www.avenel.pro/cours/docker/kubernetes-cheatsheet 🌎 pour l’installation des dépendances.
Installation des StorageClass
En s’aidant de la cheatsheet Kubernetes, installer :

Le NFS CSI driver for Kubernetes 🌎 pour créer automatiquement des PersistentVolume depuis un serveur NFS
Le local-path-provisionner de Rancher 🌎 pour créer automatiquement des PersistentVolume basés sur hostPath (répertoires locaux aux Node : perte du Node = perte de la donnée !).
Tip
Pourquoi avoir besoin d’une StorageClass générant des PV locaux ?

Beaucoup d’opérateurs créent des StatefulSets adaptées à la production : ceux-ci instancient des PersistentVolumeClaim pour référencer des PV, ce qui permet de générer dynamiquement des volumes depuis du storage (en principe distribué). Le local-path-provisionner permet de simuler cet usage en utilisant du storage local (et donc peu adapté à la production !)

Tip
Pour installer un serveur NFS simple on pourra utiliser une VM Ubuntu :

#!/usr/bin/env bash

# Installation et configuration d'un serveur NFS (dans une VM)
sudo apt install -y nfs-server
sudo mkdir -p /data
sudo /bin/sh -c 'echo "/data *(rw,sync,no_subtree_check,no_root_squash)" >> /etc/exports'
sudo systemctl restart nfs-kernel-server
## check
sudo exportfs
# /data           <world>
Vérifier la bonne installation des StorageClass :

$ kubectl get storageclasses.storage.k8s.io
NAME                   PROVISIONER             RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
local-path (default)   rancher.io/local-path   Delete          WaitForFirstConsumer   false                  26h
nfs-csi                nfs.csi.k8s.io          Delete          Immediate              true                   8m29s
Déploiement de l’application
Une fois le cluster installé, nous allons y déployer une application réalisée par vos soins. Cette application doit être multi-composants (frontend, backend, …) et utiliser une base de données. On recommande l’utilisation de fichiers de manifeste yml pour créer les ressources Kubernetes.

Exercice
Créer des images Docker pour votre application puis pusher ces images sur un dépôt public (docker hub, ghcr.io, etc) ou privé.
Mettre en place une base de données répliquée en utilisant un Operator déployé par Helm, par exemple mariadb-galera pour MariaDB / MySQL, et Zalando Postgres Operator 🌎 pour Postgresql
Déployer votre application dans le cluster avec réplication. : Deployment, Service, ConfigMaps et Secrets.
Exposer votre application à l’extérieur via un ingress (traefik ou ingress-nginx) ou un LoadBalancer dédié à l’application.
Réfléchir à la Scalabilité et la tolérance aux pannes :
Mise à jour du Deployment de votre application
Autoscaling avec Horizontal Pod Autoscaler
Limitation de ressources
Droits du cluster
Ajouter un certificat TLS (autosigné s’il n’est pas possible de le générer via Let’s Encrypt) grâce à certmanager déployé via Helm
Tip
On testera la partie H/A du déploiement applicatif :

Tester la suppression d’un conteneur / Pod
Tester la déconnexion d’un worker node
Vérifier la réconciliation des ressources
Vérifier le scaling automatique en cas de pic de charge :
Supervision
Le monitoring d’un cluster Kubernetes avec Prometheus pour la collecte des métriques et Grafana pour leur visualisation est une solution courante pour collecter, stocker et visualiser les métriques du cluster, des pods et des applications. Nous allons mettre en place cette infrastructure de monitoring.

Exercice
Mettre en place la supervision du cluster via kube-prometheus-stack (Prometheus + Grafana) déployé via Helm
Exposer l’accès à Grafana à l’extérieur du cluster via un ingress : ingress-nginx
Lien
Se référer au TP sur Prometheus et Grafana : https://www.avenel.pro/cours/docker/tp_prometheus_grafana_k8s 🌎

Bonus
Quelques bonus après avoir réalisé les parties précédentes :

Exercice
Créer une chart Helm spécifique à votre application pour déployer toute la stack automatiquement.
Configurer l’Ingress pour permettre un modèle de déploiement de type A/B testing.
Utiliser Flagger pour des modèles de déploiement plus complexes.
Ajouter des politiques de sécurité grâce à Kyverno.

Disponible ici : https://www.avenel.pro/cours/docker/projet_appli_kubernetes


### 🐱 Notre projet :
à remplir ici

### 💻 Applications et langages utilisés :

+ Visual studio code
+ Docker

## 🌸 Merci !
© J-IFT
