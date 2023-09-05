---
description: >-
  El software de control de versiones diseñado por Linus Torvalds más usado en
  la actualidad.
cover: .gitbook/assets/Git_icon.svg.png
coverY: 0
---

# Git

## Recursos

* [Web oficial](https://git-scm.com/)
* [Referencia oficial](https://git-scm.com/docs)
* [Libro oficial ](https://git-scm.com/book/es/v2)(en español)
* [Cheat Sheet ](https://training.github.com/downloads/es\_ES/github-git-cheat-sheet/)

## Contenidos

## Instalación

* [Proceso de instalación en diferentes plataformas](https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Instalaci%C3%B3n-de-Git)\
  De entre las opciones que se sugieren para instalar Git en Windows, optaremos por realizar la instalación desde la web oficial de Git.

### Configuración

* `git config` \[ [referencia](https://git-scm.com/docs/git-config) | [ejemplo](https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Configurando-Git-por-primera-vez) ]
  * `--global user.name`
  * `--global user.email`
  * `--list`
* Fichero ".gitconfig" \[ [ejemplo](https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Configurando-Git-por-primera-vez#\_comprobando\_tu\_configuraci%C3%B3n) ]
* `git init` \[ [referencia](https://git-scm.com/docs/git-init) | [ejemplo](https://git-scm.com/book/es/v2/Fundamentos-de-Git-Obteniendo-un-repositorio-Git) ]
* Subdirectorio ".git" \[ [ejemplo](https://git-scm.com/book/es/v2/Fundamentos-de-Git-Obteniendo-un-repositorio-Git) ]

### Primeros pasos

* `git status` \[ [referencia](https://git-scm.com/docs/git-status) | [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) ]
* `git branch -m` \[ [referencia](https://git-scm.com/docs/git-branch#Documentation/git-branch.txt--m)]
* `git add` \[ [referencia](https://git-scm.com/docs/git-add) | [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) ]
* `git commit` \[ [referencia](https://git-scm.com/docs/git-commit) | [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) ]
  * `-m` \[ [referencia](https://git-scm.com/docs/git-commit#Documentation/git-commit.txt--mltmsggt) ]
* `git log` \[ [referencia](https://git-scm.com/docs/git-log) | [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History) ]
  * `--graph`: muestra de forma visual las diferentes ramas.
  * `--all`: visualiza todos los commits, incluyendo los commits futuros.
  * `--oneline`: muestra cada commit en una única línea.
* Aliases \[ [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases) ]
* `git checkout`&#x20;
  * `<fichero>` \[ [referencia](https://git-scm.com/docs/git-checkout) ]  \
    Deshace los últimos cambios del fichero indicado y lo deja en la versión del último commit.
  * `<ID>` \
    Nos permite movernos a un commit determinado.
* Fichero ".gitignore" \[ [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) ]

### Comandos avanzados

* git reset
* Fichero ".gitignore"
* git diff
* git checkout
* git reset --hard
* git reflog
* git tag
* git stash

### Ramas

* git branch
* git switch
* git merge
* git diff
* git branch -d
* Resolución de conflictos







