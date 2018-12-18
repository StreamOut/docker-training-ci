Commencer par créer 3 machine:
  - docker-machine create --driver digitalocean --digitalocean-access-token <TOKEN> --digitalocean-size 512mb --digitalocean-image ubuntu-16-04-x64 malo-jenkins
  - docker-machine create --driver digitalocean --digitalocean-access-token <TOKEN> --digitalocean-size 4gb --digitalocean-image ubuntu-16-04-x64 malo-nexus
  - docker-machine create --driver digitalocean --digitalocean-access-token <TOKEN> --digitalocean-size 512mb --digitalocean-image ubuntu-16-04-x64 malo-gitlab

se connecter sur malo-nexus
  - Installer docker compose :
      - curl -L "https://github.com/docker/compose/releases/download/1.23.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
      - chmod +x /usr/local/bin/docker-compose
  - Lancer le docker-compose:
    - docker-compose up -d
  - récuperer l'adresse de la machine
    - ip a
  - se déconnecter de malo-nexus

sur la machine host :
  - configurer le repo nexus dans le navigateur avec l'addresse ip de malo-nexus

- se connecter sur malo-jenkins
  - Installer docker compose :
    - curl -L "https://github.com/docker/compose/releases/download/1.23.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    - chmod +x /usr/local/bin/docker-compose
  - Lancer le docker-compose:
    - docker-compose up -d
  - modifier le fichier /etc/docker/daemon.json le créer si il n'existe pas:
~~~
{
    "insecure-registries" : ["ip-malo-nexus:8082"]
}
~~~
  - relancer le docker
    - service docker restart

- se connecter sur malo-gitlab
  - git clone docker-gitlab
  - Installer docker compose :
    - curl -L "https://github.com/docker/compose/releases/download/1.23.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    - chmod +x /usr/local/bin/docker-compose
  - Lancer le docker-compose:
    - docker-compose up -d
