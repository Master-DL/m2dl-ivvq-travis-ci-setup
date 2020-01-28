# M2 DL - Projet IVVQ - Codecov

## Exigences

Créer un compte sur la plateforme [Codecov](https://codecov.io/) en vous authentifiant via votre compte GitHub.

Implémenter la configuration requise dans une branche (+ Pull Request)
avant de l'intégrer dans la branche `master` de votre projet :

* Ajouter maven-failsafe-plugin (pour `mvn verify`) à votre POM

* En vous appuyant sur la
  [documentation de Codecov](https://docs.codecov.io/docs), configurer
  votre projet pour qu'en cas de succès, le serveur de Travis CI
  envoie le rapport des tests cobertura sur Codecov (vous utiliserez
  le plugin Maven JaCoCo, pas Cobertura)
* Contrainte : séparer le lancement des tests unitaires (`mvn test`)
  et d'intégration (`mvn verify`) et instrumentaliser les tests avec
  JaCoCo dans les deux cas
* Modifier le fichier de configuration de Travis CI pour pousser les
  résultats de couverture dans [Codecov](https://codecov.io/) après
  chaque lancement des tests, en utilisant respectivement les *flags*
  `unit` et `integration`
* Veiller à limiter la "redondance" (pour ne pas lancer deux fois les
  mêmes tests unitaires)
  
Si ce n'est pas déjà fait, rédiger une première version de votre
politique de tests (en spécifiant la couverture attendue, etc.) dans
votre *Définition de Fini*.

## Références

* <http://maven.apache.org/surefire/maven-failsafe-plugin/usage.html>
* <https://mvnrepository.com/artifact/org.jacoco/jacoco-maven-plugin/0.8.3>
* [SO: Jacoco report for maven multimodule project](https://stackoverflow.com/a/37672302/9164010) et
  [Creating code coverage reports for unit and integration tests with the JaCoCo Maven plugin](https://www.petrikainulainen.net/programming/maven/creating-code-coverage-reports-for-unit-and-integration-tests-with-the-jacoco-maven-plugin/)
* <https://docs.codecov.io/docs/flags>
* [SO: Prevent unit tests but allow integration tests](https://stackoverflow.com/a/17932772/9164010)
