# M2 DL - Projet IVVQ - Docker + Heroku

**But**: Utilisation de Docker et déploiement du Web Service sur Heroku

En termes de *workflow*, procédez comme usuellement (création d'une branche spécifique, ajout de commits puis création d'une Pull Request pour les intégrer dans la branche maître).

### 1. Utilisation de Docker

- En vous appuyant sur le cours et sur la [documentation Docker de Travis CI](https://docs.travis-ci.com/user/docker),
modifiez votre configuration pour que Travis CI utilise `docker build` pour compiler et tester votre projet avec Maven.
- **Rappel** : en plus du `Dockerfile` que vous devrez concevoir en utilisant une image de base appropriée, n'oubliez pas de commiter un fichier `.dockerignore` qui ignorera tout sauf les fichiers utiles à la compilation.
- **Remarque** : Vous devrez vous assurer que la génération du rapport de couverture précédemment mise en place avec Codecov est toujours fonctionnelle. Celle-ci peut être déclenchée *via* une commande `docker run`, à l'intérieur du conteneur, vu que l'image `maven:3-jdk-8` contient `curl`, ou à l'extérieur, cf. la [documentation de Codecov](https://docs.codecov.io/docs/testing-with-docker) (on pourrait aussi utiliser un *job* Travis CI séparé).

### 2. Déploiement sur Heroku

Heroku est une plateforme permettant d'héberger des applications Web. Il est possible de créer un compte et de déployer une application gratuitement pour un usage restreint.
L'objectif de cette partie du TP est de déployer automatiquement votre application en utilisant Docker sur la plateforme Heroku en cas de succès du *build* sur Travis.

- Pour commencer, l'un d'entre vous (pas forcément tout le groupe) doit créer un compte sur [Heroku](https://www.heroku.com/).
- Mettez en oeuvre le déploiement de votre application sans passer par Travis en vous inspirant de
    [la documentation Heroku pour le déploiement d'images Docker](https://devcenter.heroku.com/articles/container-registry-and-runtime).  
    Résumé des commandes après avoir installé [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli#download-and-install) :
	```bash
	heroku login
	heroku container:login  # ou bien => sudo heroku container:login
	cd …/votre-projet
	heroku regions
	heroku create --region=eu nom-unique-de-votre-projet
	heroku container:push web
	heroku container:release web
	heroku logs
	heroku open
	```
- Une fois le déploiement "manuel" opérationnel, mettez en oeuvre le déploiement automatique *via* Travis en vous appuyant sur ces deux paragraphes de la documentation Heroku ([celui-ci](https://devcenter.heroku.com/articles/container-registry-and-runtime#pushing-an-existing-image) et [celui-là](https://devcenter.heroku.com/articles/container-registry-and-runtime#using-a-ci-cd-platform)).
- Vérifiez que l'application se déploie bien automatiquement *via* Travis.

> **Remarque** : Il est possible que vous rencontriez un problème de dépassement de quota RAM lors du déploiement manuel ou automatique dans Heroku de l'appli Java 8 dockerisée.
>
> Dans ce cas l'article suivant pourrait vous aider à solutionner ce problème :
>
> https://developers.redhat.com/blog/2017/03/14/java-inside-docker/

**Indication** : votre configuration Travis CI contiendra un fragment du style :

```
# cf. https://docs.travis-ci.com/user/docker/#branch-based-registry-pushes
deploy:
  provider: script
  script: bash docker_push
  on:
branch: master
```

en utilisant le script `docker_push` ci-dessous (TODO: MàJ
`$DOCKER_IMAGE`, `$PROJECT_NAME`)

```bash
#!/bin/bash
set -e

# HEROKU_AUTH_TOKEN is a Travis CI protected variable, generated using
# https://dashboard.heroku.com/account/applications then set in Travis
# cf. https://docs.travis-ci.com/user/environment-variables/#defining-variables-in-repository-settings
# and https://devcenter.heroku.com/articles/container-registry-and-runtime#logging-in-to-the-registry
# and https://docs.travis-ci.com/user/docker/#private-registry-login
echo "$HEROKU_AUTH_TOKEN" | docker login -u _ --password-stdin registry.heroku.com

docker push $DOCKER_IMAGE

docker logout

# cf. https://devcenter.heroku.com/articles/container-registry-and-runtime#api
# and https://toedter.com/2018/06/02/heroku-docker-deployment-update/
imageId=$(docker inspect $DOCKER_IMAGE --format="{{.Id}}")
payload="{\"updates\": [{\"type\": \"web\", \"docker_image\": \"$imageId\"}]}"
curl -n -X PATCH https://api.heroku.com/apps/$PROJECT_NAME/formation \
  -d "$payload" \
  -H "Content-Type: application/json" \
  -H "Accept: application/vnd.heroku+json; version=3.docker-releases" \
-H "Authorization: Bearer $HEROKU_AUTH_TOKEN"
```
