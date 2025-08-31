* Système : Ubuntu 22.04+ ou Debian 12 (serveurs ou VMs)
* Docker : version ≥ 24
* Docker Swarm : activé (`docker swarm init`)
* Accès root ou utilisateur dans le groupe `docker`

## Cloner le projet
      git clone https://github.com/[ton-user]/[ton-projet].git
      cd [ton-projet]

## Créer le réseau overlay
      docker network create --driver overlay --attachable mon-projet-lb-net


### 3️Générer les certificats SSL (si besoin)

Si tu n’as pas déjà des certificats Let’s Encrypt, tu peux en créer des **auto-signés** :

    mkdir -p ssl
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
      -keyout ssl/privkey.pem -out ssl/fullchain.pem
    cat ssl/privkey.pem ssl/fullchain.pem > ssl/haproxy.pem

## Déployer le stack
    docker stack deploy -c docker-compose.yml mon-projet

## Vérifier l’état des services
    docker service ls


###  Accéder aux interfaces

* Site web (load balancing HAProxy)** : `http://<IP_manager>`
* Grafana** : `https://<IP_manager>:3000`
  Utilisateur par défaut : `admin / admin`
* Prometheus** : `http://<IP_manager>:9090`
* HAProxy Stats** : `http://<IP_manager>:8404`
* cAdvisor** : `http://<IP_node>:8080`

## Si vous modifiez un fichier (`prometheus.yml`, `haproxy.cfg`, etc.) :
      docker stack deploy -c docker-compose.yml mon-projet

##  Tests rapides

## Simuler une panne en stoppant un conteneur web :
        docker service scale mon-projet_web=2
 
## Ajouter un nouveau *worker* :
        docker swarm join --token <token> <manager_ip>:2377
  

 



