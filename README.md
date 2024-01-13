![](https://img.shields.io/badge/Github-Actions-red.svg)

# GitHub Actions

[GitHub Actions](https://docs.github.com/fr/actions) est un service de [GitHub](https://github.com/) permettant d'automatiser, personnaliser et exécuter des _workflows_ (i.e. des tâches) de développement logiciel directement dans un dépôt [GitHub](https://github.com/).

Lien : https://docs.github.com/fr/actions

## Intégration continue

> Source Wikipédia :

[CI/CD](https://fr.wikipedia.org/wiki/CI/CD) (_Continuous Integration/Continuous Delivery_) est la combinaison des pratiques d'intégration continue et de livraison continue ou de déploiement continu.

Le [CI/CD](https://fr.wikipedia.org/wiki/CI/CD) comble le fossé entre les activités et les équipes de développement et d'exploitation en imposant l'automatisation de la création, des tests et du déploiement des applications. Les pratiques [DevOps](https://fr.wikipedia.org/wiki/Devops) modernes impliquent le développement continu, le test continu, l'intégration continue, le déploiement continu et la surveillance continue des applications logicielles tout au long de leur cycle de vie. La pratique CI/CD, ou pipeline CI/CD, constitue l'épine dorsale des opérations [DevOps](https://fr.wikipedia.org/wiki/Devops) modernes.

Il est donc possible de créer des flux d’intégration continue (CI) personnalisés directement dans un dépôt [GitHub](https://github.com/) avec [GitHub Actions](https://docs.github.com/fr/actions).


## Workflow

Un _workflow_ est un processus automatisé configurable qui comprend un ou plusieurs travaux.

Le _workflow_ est décrit dans un fichier `.yml` stocké dans l'arborescence `.github/workflows/`.

> Le fichier peut être créé directement à partir de l'interface web de GitHub dans l'onglet `Actions` puis `New workflow`. 
> [GitHub Actions](https://docs.github.com/fr/actions) propose alors des modèles prêts à l'emploi. On peut créer son propre _workflow_ en cliquant sur `set up a workflow yourself`. Un squelette est alors fourni.

Il faut commencer par donner un nom au fichier, par exemple : `build-cpp.yml`

Le _workflow_ doit avoir un **nom** :

```yml
name: C/C++ Build
```

Puis on définit l'évènement (_on_) déclencheur (_trigger_), ici un `git push` sur la branche principale `main` :

```yml
name: C/C++ Build
on:
  push:
    branches: [main]
```

Ensuite, on décrit **un ou plusieurs travaux (_jobs_) à exécuter (_runs-on_) sur une machine (virtuelle, par exemple Ubuntu), qui est généralement composé d'une ou plusieurs étapes (_steps_)** :

```yml
name: C/C++ Build
on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      # Extraction du dépôt
      - name: Checkout code
        uses: actions/checkout@v2

      # Exécute une commande
      - name: make
        run: make
```

_Remarque :_ Le mot clé `uses` permet de récupérer des actions existantes fournies par des contributeurs.

Il est possible d'associer un badge d'état (une image) à un _workflow_ puis l'intégrer dans le `README.md`.

Pour cela, il faut aller dans l'onglet `Actions` puis cliquer sur le _workflow_ (dans la liste à gauche). Il faut ensuite cliquer sur les trois petits points `...` (à droite de la zone de recherche) et sélectionner `Create status badge`. Une boîte de dialogue s'affiche et il faut récupérer le code Markdown (`Copy status badge Mardown`).

Ce code est à placer dans le fichier `README.md` du dépôt (généralement au tout début du fichier) pour afficher le badge sur la page d'accueil.

```markdown
[![C/C++ Build](https://github.com/<organisation>/<depot>/actions/workflows/build-cpp.yml/badge.svg)](https://github.com/<organisation>/<depot>/actions/workflows/build-cpp.yml)
```

Voi aussi : https://github.com/btssn-lasalle84/badges

## Exemples

- ![C++ Badge](https://img.shields.io/badge/C%2B%2B-00599C?logo=cplusplus&logoColor=fff&style=plastic)

    https://github.com/btssn-lasalle84/github-actions-cpp

- ![Qt Badge](https://img.shields.io/badge/Qt-41CD52?logo=qt&logoColor=fff&style=plastic)

    https://github.com/btssn-lasalle84/github-actions-qt

- ![PlatformIO](https://img.shields.io/badge/build%20with-PlatformIO-orange?logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB3aWR0aD0iMjUwMCIgaGVpZ2h0PSIyNTAwIiB2aWV3Qm94PSIwIDAgMjU2IDI1NiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiBwcmVzZXJ2ZUFzcGVjdFJhdGlvPSJ4TWlkWU1pZCI+PHBhdGggZD0iTTEyOCAwQzkzLjgxIDAgNjEuNjY2IDEzLjMxNCAzNy40OSAzNy40OSAxMy4zMTQgNjEuNjY2IDAgOTMuODEgMCAxMjhjMCAzNC4xOSAxMy4zMTQgNjYuMzM0IDM3LjQ5IDkwLjUxQzYxLjY2NiAyNDIuNjg2IDkzLjgxIDI1NiAxMjggMjU2YzM0LjE5IDAgNjYuMzM0LTEzLjMxNCA5MC41MS0zNy40OUMyNDIuNjg2IDE5NC4zMzQgMjU2IDE2Mi4xOSAyNTYgMTI4YzAtMzQuMTktMTMuMzE0LTY2LjMzNC0zNy40OS05MC41MUMxOTQuMzM0IDEzLjMxNCAxNjIuMTkgMCAxMjggMCIgZmlsbD0iI0ZGN0YwMCIvPjxwYXRoIGQ9Ik0yNDkuMzg2IDEyOGMwIDY3LjA0LTU0LjM0NyAxMjEuMzg2LTEyMS4zODYgMTIxLjM4NkM2MC45NiAyNDkuMzg2IDYuNjEzIDE5NS4wNCA2LjYxMyAxMjggNi42MTMgNjAuOTYgNjAuOTYgNi42MTQgMTI4IDYuNjE0YzY3LjA0IDAgMTIxLjM4NiA1NC4zNDYgMTIxLjM4NiAxMjEuMzg2IiBmaWxsPSIjRkZGIi8+PHBhdGggZD0iTTE2MC44NjkgNzQuMDYybDUuMTQ1LTE4LjUzN2M1LjI2NC0uNDcgOS4zOTItNC44ODYgOS4zOTItMTAuMjczIDAtNS43LTQuNjItMTAuMzItMTAuMzItMTAuMzJzLTEwLjMyIDQuNjItMTAuMzIgMTAuMzJjMCAzLjc1NSAyLjAxMyA3LjAzIDUuMDEgOC44MzdsLTUuMDUgMTguMTk1Yy0xNC40MzctMy42Ny0yNi42MjUtMy4zOS0yNi42MjUtMy4zOWwtMi4yNTggMS4wMXYxNDAuODcybDIuMjU4Ljc1M2MxMy42MTQgMCA3My4xNzctNDEuMTMzIDczLjMyMy04NS4yNyAwLTMxLjYyNC0yMS4wMjMtNDUuODI1LTQwLjU1NS01Mi4xOTd6TTE0Ni41MyAxNjQuOGMtMTEuNjE3LTE4LjU1Ny02LjcwNi02MS43NTEgMjMuNjQzLTY3LjkyNSA4LjMyLTEuMzMzIDE4LjUwOSA0LjEzNCAyMS41MSAxNi4yNzkgNy41ODIgMjUuNzY2LTM3LjAxNSA2MS44NDUtNDUuMTUzIDUxLjY0NnptMTguMjE2LTM5Ljc1MmE5LjM5OSA5LjM5OSAwIDAgMC05LjM5OSA5LjM5OSA5LjM5OSA5LjM5OSAwIDAgMCA5LjQgOS4zOTkgOS4zOTkgOS4zOTkgMCAwIDAgOS4zOTgtOS40IDkuMzk5IDkuMzk5IDAgMCAwLTkuMzk5LTkuMzk4em0yLjgxIDguNjcyYTIuMzc0IDIuMzc0IDAgMSAxIDAtNC43NDkgMi4zNzQgMi4zNzQgMCAwIDEgMCA0Ljc0OXoiIGZpbGw9IiNFNTcyMDAiLz48cGF0aCBkPSJNMTAxLjM3MSA3Mi43MDlsLTUuMDIzLTE4LjkwMWMyLjg3NC0xLjgzMiA0Ljc4Ni01LjA0IDQuNzg2LTguNzAxIDAtNS43LTQuNjItMTAuMzItMTAuMzItMTAuMzItNS42OTkgMC0xMC4zMTkgNC42Mi0xMC4zMTkgMTAuMzIgMCA1LjY4MiA0LjU5MiAxMC4yODkgMTAuMjY3IDEwLjMxN0w5NS44IDc0LjM3OGMtMTkuNjA5IDYuNTEtNDAuODg1IDIwLjc0Mi00MC44ODUgNTEuODguNDM2IDQ1LjAxIDU5LjU3MiA4NS4yNjcgNzMuMTg2IDg1LjI2N1Y2OC44OTJzLTEyLjI1Mi0uMDYyLTI2LjcyOSAzLjgxN3ptMTAuMzk1IDkyLjA5Yy04LjEzOCAxMC4yLTUyLjczNS0yNS44OC00NS4xNTQtNTEuNjQ1IDMuMDAyLTEyLjE0NSAxMy4xOS0xNy42MTIgMjEuNTExLTE2LjI4IDMwLjM1IDYuMTc1IDM1LjI2IDQ5LjM2OSAyMy42NDMgNjcuOTI2em0tMTguODItMzkuNDZhOS4zOTkgOS4zOTkgMCAwIDAtOS4zOTkgOS4zOTggOS4zOTkgOS4zOTkgMCAwIDAgOS40IDkuNCA5LjM5OSA5LjM5OSAwIDAgMCA5LjM5OC05LjQgOS4zOTkgOS4zOTkgMCAwIDAtOS4zOTktOS4zOTl6bS0yLjgxIDguNjcxYTIuMzc0IDIuMzc0IDAgMSAxIDAtNC43NDggMi4zNzQgMi4zNzQgMCAwIDEgMCA0Ljc0OHoiIGZpbGw9IiNGRjdGMDAiLz48L3N2Zz4=)

    https://github.com/btssn-lasalle84/github-actions-platformio

Voir aussi : des _workflows_ (Python, Android, Java, ...) pour la notation automatique (basée sur des tests logiciels) sont utilisés dans les devoirs [Github Classroom](https://classroom.github.com/)

    https://github.com/tvaira/github-classroom

---
©️ LaSalle Avignon - <thierry.vaira@gmail.com>
