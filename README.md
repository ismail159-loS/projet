# projet
quelques projets professionnels dans mon parcours professionnel.
# 🚀 Projet Docker Swarm avec HAProxy, Prometheus et Grafana

## 📌 Description
Ce projet met en place une architecture **Docker Swarm** pour assurer :
- Le **déploiement d’une application web** (Nginx avec réplication),
- L’**équilibrage de charge** avec **HAProxy**,
- La **supervision** et le **monitoring** avec **Prometheus**, **Grafana**, **cAdvisor** et **Node Exporter**.

L’objectif est de garantir la **haute disponibilité**, la **scalabilité** et la **sécurité** d’un cluster en environnement de production.

---

## 🏗️ Architecture
- **1 Manager Docker Swarm**
- **3 Workers Docker Swarm**
- **HAProxy** (Load Balancer)
- **Prometheus** (Collecte des métriques)
- **Grafana** (Visualisation)
- **cAdvisor + Node Exporter** (Supervision des containers et des nœuds)
- **Application Web (Nginx)** avec 3 réplicas

📌 Exemple d’architecture :  
```mermaid
graph TD
    User -->|HTTP/HTTPS| HAProxy
    HAProxy -->|Load Balance| Web1[Nginx Replica 1]
    HAProxy -->|Load Balance| Web2[Nginx Replica 2]
    HAProxy -->|Load Balance| Web3[Nginx Replica 3]

    Web1 --> Prometheus
    Web2 --> Prometheus
    Web3 --> Prometheus

    Prometheus --> Grafana
    cAdvisor --> Prometheus
    NodeExporter --> Prometheus

<img width="1544" height="710" alt="Capture d'écran 2025-07-04 174437" src="https://github.com/user-attachments/assets/7ab2afcf-5c87-4d0b-8b86-1037dc5845bf" />
<img width="1538" height="828" alt="Capture d'écran 2025-07-04 174500" src="https://github.com/user-attachments/assets/f5b22127-a6e7-4d42-b4e8-c7100cb350df" />
