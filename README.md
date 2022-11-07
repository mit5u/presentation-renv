# Support pour la présentation de {renv}

## Mode d'emploi

* Télécharger le dépôt en cliquant sur "Code" > "Download ZIP"
* Décompresser `presentation-renv-main.zip` à l'emplacement de votre choix
* Double-cliquer sur `pres_renv.html` pour ouvrir le diaporama dans le navigateur
* Utiliser les flèches droite/gauche pour naviguer dans le diaporama

## Éléments discutés en fin de séance

* mise à jour de {renv} au niveau du projet : `renv::upgrade()`
* [récupérer les dépendances d'un projet en cours](https://rstudio.github.io/renv/articles/renv.html) :
    * déclarations implicites : `renv::snapshot()` inclut uniquement les packages utilisés dans un script R du projet (chargés via `library()` ou `require()`) ; les fichiers/dossiers listés dans `.renvignore` ne sont pas pris en compte pour la détection de ces dépendances
    * déclaration explicite : on peut créer un fichier `DESCRIPTION` à la racine du projet, de façon similaire à ce qui est fait en développement de package, pour déclarer les dépendances (voir aussi `usethis::use_package()` pour alimenter facilement ce fichier)
    
```
Type: project
Description: Ceci est mon project.
Depends:
    tidyverse,
    devtools,
    shiny
Imports:
    data.table
```

Utiliser alors `renv::snapshot(type = "explicit")` pour conserver les versions des packages dont le nom est listé dans ce fichier. Alternativement, paramétrer `options(renv.settings.snapshot.type = "explicit")` dans le `.Rprofile` du projet pour que ce soit le comportement par défaut.

* suivre les packages/fonctions d'intérêt pour détecter les problèmes potentiels :
    * [itdepends](https://www.tidyverse.org/blog/2019/05/itdepends/) et [funspotr](https://github.com/brshallo/funspotr) : lister les packages et fonctions utilisés dans le projet
    * [rweekly](https://rweekly.org/#UpdatedPackages) : veille hebdomadaire sur l'actualité de R et les packages mis à jour
    * [diffify](https://diffify.com/R/) : comparaison des notes de mise à jour et des espaces de noms des différentes versions d'un package
    * [targets](https://books.ropensci.org/targets/walkthrough.html) : définition d'un pipeline reproductible pour identifier les éléments de code et les données qui ont changé depuis la dernière exécution
