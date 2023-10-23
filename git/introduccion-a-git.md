---
description: >-
  El software de control de versiones diseñado por Linus Torvalds más usado en
  la actualidad.
cover: ../.gitbook/assets/Git_icon.svg.png
coverY: 0
---

# Introducción a Git

## Recursos

* [Web oficial](https://git-scm.com/)
* [Referencia oficial](https://git-scm.com/docs)
* [Libro oficial ](https://git-scm.com/book/es/v2)(en español)
* [Cheat Sheet ](https://training.github.com/downloads/es\_ES/github-git-cheat-sheet/)
* [Tutorial de Git de W3Schools](https://www.w3schools.com/git/)

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
  * \-s \[ [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) ]
* `git branch -m` \[ [referencia](https://git-scm.com/docs/git-branch#Documentation/git-branch.txt--m)]
* `git add` \[ [referencia](https://git-scm.com/docs/git-add) | [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) ]
  * `--all`: Añade al área de stage todos los cambios (ficheros nuevos, modificados y eliminados). Es equivalente a `-a`
* `git commit` \[ [referencia](https://git-scm.com/docs/git-commit) | [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) ]
  * `-m` \[ [referencia](https://git-scm.com/docs/git-commit#Documentation/git-commit.txt--mltmsggt) ]
  * `-a`: automáticamente añade al área de stage todos los cambios que afecten a tracked files.
* `git log` \[ [referencia](https://git-scm.com/docs/git-log) | [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History) ]
  * `--graph`: muestra de forma visual las diferentes ramas.
  * `--all`: visualiza todos los commits, incluyendo los commits futuros.
  * `--oneline`: muestra cada commit en una única línea.
* `git diff` \[ [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) ]
* `git rm --cached` \[ [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) ]
* Aliases \[ [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases) ]
* `git checkout`&#x20;
  * `<fichero>` \[ [referencia](https://git-scm.com/docs/git-checkout) ]  \
    Deshace los últimos cambios del fichero indicado y lo deja en la versión del último commit.
  * `<ID>` \
    Nos permite movernos a un commit determinado.
* Fichero ".gitignore" \[ [ejemplo](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) ]

### Ramas

* `git branch` \[ [ejemplo](https://git-scm.com/book/es/v2/Ramificaciones-en-Git-%C2%BFQu%C3%A9-es-una-rama%3F) ]: Crea una nueva rama
* `git checkout/switch` \[  [ejemplo](https://git-scm.com/book/es/v2/Ramificaciones-en-Git-%C2%BFQu%C3%A9-es-una-rama%3F) ]
  * `git checkout -b <rama>`: Crea una nueva rama y se cambia a ella en un único comando
* `git merge` \[ [ejemplo](https://git-scm.com/book/es/v2/Ramificaciones-en-Git-Procedimientos-B%C3%A1sicos-para-Ramificar-y-Fusionar) ]
* `git branch -d`: Elimina una rama
* `git branch -v` \[ [ejemplo](https://git-scm.com/book/es/v2/Ramificaciones-en-Git-Gesti%C3%B3n-de-Ramas) ]: Muestra las ramas locales
* `git branch -a`: Muestra todas las ramas (locales y remotas)
* `git log --oneline --decorate --graph --all`: Muestra gráficamente el log, incluyendo los commits posteriores al actual. No muestra el detalle de cada commit. Únicamente su id corto.
* `git push -u origin <nombrederama>:` Sube la rama \<nombrederama> desde nuestro repositorio local a GitHub.
* [Traer a nuestro repositorio local una rama creada previamente en GitHub](https://www.w3schools.com/git/git\_branch\_pull\_from\_remote.asp?remote=github)



###







