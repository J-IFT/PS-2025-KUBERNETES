# PS-2025-KUBERNETES

*PS = Projet Scolaire*

## 📚 Projet Scolaire | Kubernetes

Avril Mai 2025

Groupe : Yasmine, Colas, Théo et Juliette

### 📌 Consignes du projet :

Le projet consiste à déployer une application dans un cluster Kubernetes avec plusieurs étapes :

Installation du Cluster :

Créer un petit cluster Kubernetes (1 control plane, 2-3 workers).

Installer un Load Balancer (MetalLB) et un IngressController (Traefik ou ingress-nginx) via Helm.

Installation des StorageClass :

Installer le NFS CSI driver pour créer des PersistentVolume à partir d'un serveur NFS.

Installer le local-path-provisionner pour créer des volumes locaux à partir des répertoires des nœuds.

Déploiement de l'Application :

Déployer une application multi-composants (frontend, backend) avec une base de données (MariaDB ou PostgreSQL avec réplication via un Operator).

Exposer l'application via un Ingress ou LoadBalancer.

Ajouter des fonctionnalités de scalabilité et de tolérance aux pannes (autoscaling, limitations de ressources, mise à jour du Deployment, ajout de certificat TLS via cert-manager).

Supervision du Cluster :

Mettre en place le monitoring avec Prometheus et Grafana via kube-prometheus-stack déployé avec Helm.

Exposer l'accès à Grafana via un Ingress.

Bonus :

Créer une chart Helm pour déployer automatiquement toute la stack.

Configurer un modèle de déploiement A/B testing avec Flagger.

Ajouter des politiques de sécurité avec Kyverno.

Disponible ici : https://www.avenel.pro/cours/docker/projet_appli_kubernetes


### 🐱 Notre projet :
à remplir ici

### 💻 Applications et langages utilisés :

+ Visual studio code
+ Docker

## 🌸 Merci !
© J-IFT
