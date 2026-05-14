# Projet CI/CD Flask avec Jenkins et Docker

## Description

Ce projet présente la mise en place d’un pipeline CI/CD complet pour une application Flask en utilisant Jenkins, Docker et GitHub.

L’objectif est d’automatiser :
- le clonage du code source depuis GitHub
- la construction de l’image Docker
- le déploiement automatique de l’application Flask

---

# Technologies utilisées

- Python
- Flask
- Docker
- Jenkins
- Git & GitHub

---

# Structure du projet

```bash
Projet-Jenkins/
│
├── app.py
├── requirements.txt
├── Dockerfile
├── Jenkinsfile
└── templates/
    └── index.html


Étapes du projet
1. Création de l’application Flask

Création d’une application Flask simple avec :

fichier app.py
template HTML
fichier requirements.txt
2. Création du Dockerfile

Le Dockerfile permet :

d’utiliser une image Python
d’installer les dépendances Flask
de copier le projet
d’exécuter l’application

Commande utilisée :

docker build -t flask-cicd .
3. Initialisation Git

Initialisation du dépôt Git :

git init
git add .
git commit -m "Projet Jenkins"

Création de la branche de développement :

git branch dev
git checkout dev
4. Publication sur GitHub

Connexion du projet au dépôt GitHub :

git remote add origin https://github.com/julesy19/Projet-Jenkins.git
git push -u origin dev
Installation de Jenkins avec Docker
Création du conteneur Jenkins
docker run -d ^
  --name jenkins ^
  -p 9090:8080 ^
  -p 50000:50000 ^
  -v jenkins_home:/var/jenkins_home ^
  -v /var/run/docker.sock:/var/run/docker.sock ^
  jenkins/jenkins:lts
Configuration de Jenkins
Accès à Jenkins
http://localhost:9090
Récupération du mot de passe administrateur
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
Installation de Docker dans Jenkins

Connexion au conteneur Jenkins :

docker exec -u 0 -it jenkins bash

Installation de Docker :

apt update
apt install docker.io -y

Vérification :

docker --version

Autorisation d’accès au socket Docker :

chmod 666 /var/run/docker.sock
Jenkins Pipeline

Le pipeline automatise :

le clonage du projet GitHub
le build Docker
la suppression de l’ancien conteneur
le déploiement automatique

<=======================================>

Jenkinsfile  file

pipeline {
    agent any

    stages {

        stage('Clone GitHub') {
            steps {
                git branch: 'dev',
                url: 'https://github.com/julesy19/Projet-Jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-cicd .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop flask-app || true'
                sh 'docker rm flask-app || true'
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name flask-app flask-cicd'
            }
        }
    }
}
Déploiement

Une fois le pipeline exécuté avec succès, l’application est disponible sur :

http://localhost:5000
Résultat

Ce projet démontre :

l’automatisation CI/CD
l’intégration continue avec Jenkins
le déploiement continu avec Docker
l’utilisation de GitHub pour la gestion du code source
Texte collé(52).txt
Document

Ton pipeline CI/CD a été exécuté avec succès dans Jenkins.

Les étapes réalisées automatiquement :

récupération du code depuis GitHub
build de l’image Docker flask-cicd
installation des dépendances Flask
suppression de l’ancien conteneur
déploiement du nouveau conteneur flask-app

Le message final :

Finished: SUCCESS

confirme que le pipeline fonctionne correctement 🎉

Ton application Flask est maintenant déployée sur :

http://localhost:5000

Tu peux aussi ajouter dans ton README.md une section résultat :

# Résultat du Pipeline

Le pipeline Jenkins exécute automatiquement les étapes suivantes :

1. Clone du dépôt GitHub
2. Construction de l’image Docker
3. Installation des dépendances Flask
4. Suppression de l’ancien conteneur
5. Déploiement automatique de l’application

Résultat final :

```bash
Finished: SUCCESS

Application accessible sur :

http://localhost:5000
