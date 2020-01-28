# M2 DL - Démarrage du projet IVVQ - Travis CI

## Environnement de développement

Vous travaillez en quadrinôme avec des machines disposant des logiciels Git, IntelliJ et Java 8.
Vous pouvez travaillez sur vos propres machines à condition d'installer ces trois logiciels :

- Git : <https://git-scm.com/downloads>
- IntelliJ IDEA édition **Utimate** : <https://www.jetbrains.com/idea/download/>  
  (en souscrivant au [Pack Student](https://www.jetbrains.com/student/) avec votre adresse …@univ-tlse3.fr)
- JDK 8 : <https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html>

## Étape 1 - Création du squelette de projet Spring-Boot

Dans la suite de ce TD, le terme "M1" désigne le premier membre de votre équipe et "M2+" désigne les trois autres membres. Les énoncés des questions préfixés par "M1:" sont à réaliser par M1 uniquement alors que les énoncés préfixés par "M2+:" sont à réaliser par les trois autres membres (et le préfixe "M'" désignera n'importe quel membre).

- M1: Lancer IntelliJ puis l'assistant de création de projet Spring-Boot
  (File > New > Project… > **Spring Initializr** > **JDK 8**)
- M1: Sélectionner le **groupId** `fr.univ-tlse3.m2dl.votre-groupe`
  (en remplaçant la chaîne `votre-groupe` par votre nom de code) puis
  l'**artifactId** correspondant à votre projet (en minuscules, sans
  point).  Renommer et raccourcir si besoin le paquetage proposé (qui
  **ne doit pas comporter de trait-d'union, mais peut comporter un
  underscore**), et conserver la version `0.0.1-SNAPSHOT`.
- M1: Sélectionner les dépendances suivantes :
  - Web → Web
  - Template Engines → Thymeleaf
  - SQL → {JPA, H2}
- M1: Créer un `.gitignore` (ignorant au moins `target/`, `*.iml` et `.idea/`)
- M1: Créer un fichier `README.md` avec le titre du sujet choisi (`# Titre…`)
- M1: Commiter le `.gitignore`, le `README.md` et le squelette de projet
- M1: Ajouter au moins le plugin Jxr à votre `pom.xml` et testez la compilation en faisant `mvn clean test site`
- M1: Commiter et pousser sur GitHub
- M2+: Cloner le projet en ligne de commande (idéalement *via* SSH en
  faisant `git clone git@github.com:M2DL/….git`)
- M2+: Importer le projet Maven dans IntelliJ :
  <kbd>File → New → Project-from-Existing-Sources…</kbd>, choisir
  `Import project from external model: Maven`, puis un JDK 8.

## Étape 2 - Mise en place de l'intégration continue

Le membre "M1" de cette étape peut bien sûr être différent du "M1" de
l'étape 1, et préparer cette étape en pair-(quadri?)-programming !

- Créer un compte sur la plateforme [Travis CI](https://travis-ci.com/) en vous authentifiant via votre compte Github.
- M1: Créer une branche nommée par exemple `setup-ci`
- M1: En s'aidant de vos connaissances sur Maven et de la
  [documentation de travis-ci.com](https://docs.travis-ci.com/)
  (**pas** travis-ci.org), créer un fichier `.travis.yml` permettant
  de tester votre projet sur la plateforme Travis CI.
- M1: Commiter et pousser votre branche sur GitHub
- M1: Ouvrir une **Pull Request** (PR) correspondant à l'intégration
  possible de votre branche dans *master*.
- M1: Vérifier que le *build* automatique est bien activé pour votre
  projet sur https://travis-ci.com/organizations/M2DL/repositories
- M2+: Inspecter le résultat du *build* sur **Travis CI** et sur
  GitHub (directement dans la PR). Y a-t-il eu un seul *build* ou bien
  deux ? Pourquoi ?
- M2+: Commenter le code du `.yml` dans la PR, en suggérant éventuellement des améliorations  
  (*Indication : la commande `mvn install -DskipTests=true
  -Dmaven.javadoc.skip=true -B -V` proposée par défaut pour le champ
  `install:` est sous-optimale…*)
- M': Pour tester la configuration : pousser un commit avec un **test
  JUnit qui échoue volontairement**.
- M': Ajouter un **badge Travis CI (en Markdown) reflétant l'état de
  la branche `master`** dans le `README.md`
- M': Récupérer la dernière version de la branche, faire un
  **rebase-interactif** pour nettoyer l'historique local et enlever le
  commit qui échoue, puis pousser avec `git push --force-with-lease origin setup-ci`
- M': Vérifier que le *build* réussit, puis merger dans *master*.

## Étape 3 - Documentation du projet

- M1: Créer une PR pour documenter le **choix de votre sujet** dans le
  fichier `README.md`
- M2+: Valider et intégrer la PR
- M1: Créer une page **Definition of Done** sur le Wiki (ou une issue
  du même nom qui restera ouverte) pour documenter votre définition de
  fini (cette définition pourra évoluer, pour le moment vous n'êtes
  pas obligés de parler de couverture).
