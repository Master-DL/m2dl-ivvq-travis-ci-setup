# M2 DL - Projet IVVQ - Docker + Heroku

**But**: Utilisation de Docker et déploiement du Web Service sur Heroku

En termes de *workflow*, procédez comme usuellement (création d'une branche spécifique, ajout de commits puis création d'une Pull Request pour les intégrer dans la branche maître).

### 1. Utilisation de Docker

- En vous appuyant sur le cours et sur la [documentation Docker de Travis CI](https://docs.travis-ci.com/user/docker),
modifiez votre configuration pour que Travis CI utilise `docker build` pour compiler et tester votre projet avec Maven.
- Rappel : en plus du `Dockerfile` que vous devrez concevoir en utilisant une image de base appropriée, n'oubliez pas de commiter un fichier `.dockerignore` qui ignorera tout sauf les fichiers utiles à la compilation.
- Remarque : Vous devrez vous assurer que la génération du rapport de couverture mise en place dans la Partie 2 est toujours fonctionnelle.

### 2. Déploiement sur Heroku

Heroku est une plateforme permettant d'héberger des applications Web. Il est possible de créer un compte et de déployer une application gratuitement pour un usage restreint.
L'objectif de cette partie du TP est de déployer automatiquement votre application en utilisant Docker sur la plateforme Heroku en cas de succès du *build* sur Travis.

- Pour commencer, l'un d'entre vous (ou le binôme complet) doit créer un compte sur [Heroku](https://www.heroku.com/).
- Mettez en oeuvre le déploiement de votre application sans passer par Travis en vous inspirant de
 [la documentation Heroku pour le déploiement d'images Docker](https://devcenter.heroku.com/articles/container-registry-and-runtime).
- Une fois le déploiement "manuel" opérationnel, mettez en oeuvre le déploiement automatique via Travis en vous appuyant sur ces deux paragraphes de la documentation Heroku ([celui-ci](https://devcenter.heroku.com/articles/container-registry-and-runtime#pushing-an-existing-image) et [celui-là](https://devcenter.heroku.com/articles/container-registry-and-runtime#using-a-ci-cd-platform)).
- Vérifiez que l'application se déploie bien automatiquement via Travis.

> **Remarque** : Il est possible que vous rencontriez un problème de dépassement de quota RAM lors du déploiement manuel ou automatique dans Heroku de l'appli Java 8 dockerisée.
>
> Dans ce cas l'article suivant pourrait vous aider à solutionner ce problème :
>
> https://developers.redhat.com/blog/2017/03/14/java-inside-docker/
