**1. Configuration en Local**
+ Afin de pouvoir lancer l'application python il faut prendre une version plus récente de flask, par exemple ```Flask>=2.2.0```

**2. Dockerization** 
+ Création des différents Dockerfile puis d'un fichier compose afin de tester en local.
+ ```client = MongoClient('mongodb://localhost:27017/')``` -> changer localhost par le nom du service mongo car l'app appel la bdd depuis le conteneur. Ici, ```mongo-service```. 
+ Pas besoin de changer l'adresse qui est localhost lors de l'appel des services depuis le front pour le moment car le front appel les services depuis l'extérieur de docker (depuis la machine)
+ J'ai du changer la ligne ``` app.run(port=3001)``` en ``` app.run(host='0.0.0.0', port=3001)``` pour que l'application accepte les connexions de ma machine.
+ Créer repo depuis l'interface web de DockerHub
+ Tagger l'image
+ Push l'image

**3 & 4. Pipeline & Versionning** 
+ Pour github avec dockerhub :
	+ Créer un repo sur Github et y tranverser tous les fichiers
	+ Créer un fichier yaml dans le répertoire ```./github/workflows```
	+ Décrire les différentes étapes du CI dans le fichier yaml
	+ Générer un token d'authentification sur DockerHub
	+ Se rendre dans l'interface des secrets de github actions
	  ``${URL_DU_REPOT_GITHUB}/settings/secrets/actions
	+ Renseigner le token et l'username
* Dans le fichier donné, lors d'un push/merge/pull-request sur les branches main ou version/** une image est crée et envoyée sur le repository DockerHub
* Lors d'une action sur une branche ```version/**```, une image avec le tag ```image:**``` sera crée, si l'action est sur la branche main, une image avec le tag ```image:latest``` sera crée
* Ex: 
	* Je pousse sur la branche version/1.0.1 sur git
	* Une image user-service:1.0.1 (pour les autres services également, mais pour l'exemple) est crée et poussée sur DockerHub
	* Je fais une pull request vers main depuis ma branche version/1.0.1
	* Une image user-service:latest est crée et poussée sur DockerHub

**6. Déploiement avec ArgoCD**
+ Installer minkikube
 + Installer argo cd 
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
+ Créer un fichier de déploiement et l'appeler par exemple ``deploy-argo.yaml``
+ Y décrire les différentes specs du projet telles que la source, le namespace
+ ``kubectl apply -f {{NOM_DU_FICHIER}}``
+ 