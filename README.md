# Git et GitHub — initiation pour le cours au Collège CDI

Ce guide présente le contrôle de versions depuis zéro, avec des exercices pour Windows et PowerShell. Exécutez les exercices dans un dossier distinct, `pratique-git-cdi`, pour préserver vos travaux de cours.

## 1. Comprendre les concepts

Git conserve l’historique d’un projet sur votre ordinateur. GitHub héberge des dépôts en ligne et facilite la collaboration. Un commit local fonctionne sans Internet ; l’accès au dépôt GitHub nécessite une connexion.

| Terme | Signification |
| --- | --- |
| Dépôt | Projet et historique de ses versions |
| Commit | État enregistré, accompagné d’un message |
| Branche | Ligne de développement |
| `main` | Nom habituel de la branche principale |
| `origin` | Nom habituel du dépôt distant configuré |
| Clone | Copie locale d’un dépôt et de son historique |
| Push | Envoi des commits vers le dépôt distant |
| Pull | Récupération et intégration des changements distants |
| Merge | Fusion de branches |
| Pull request (PR) | Proposition de changements à examiner avant leur intégration |

## 2. Installer et configurer Git

Installez Git depuis https://git-scm.com/downloads et créez un compte sur https://github.com. Rouvrez PowerShell après l’installation.

```powershell
git --version
git config --global user.name "Votre Nom"
git config --global user.email "votre-adresse@example.com"
git config --global init.defaultBranch main
git config --global --list
```

Remplacez le nom et l’adresse par vos informations. Ces valeurs identifient l’auteur des commits ; elles ne vous connectent pas à GitHub. Pour protéger votre adresse personnelle, utilisez l’adresse `noreply` indiquée dans les paramètres de votre compte GitHub.

## 3. Créer un dépôt local

Dans le dossier où vous rangez vos exercices :

```powershell
mkdir pratique-git-cdi
cd pratique-git-cdi
git init -b main
"# Ma pratique Git au College CDI" | Set-Content -Encoding utf8 README.md
git status
```

Git crée un dossier caché `.git`. Le README apparaît d’abord comme non suivi (`untracked`).

## 4. Enregistrer une première version

```text
Modification du fichier → git add → préparation → git commit → version enregistrée
```

```powershell
git add README.md
git diff --staged
git commit -m "Ajouter la presentation du projet"
git status
git log --oneline
```

Enregistrer un fichier dans l’éditeur ne crée pas de commit. `git add` prépare son contenu actuel. Si vous le modifiez ensuite, exécutez à nouveau `git add` pour inclure la nouvelle modification.

## 5. Modifier et comparer

```powershell
"Je commence a apprendre le controle de versions." | Add-Content -Encoding utf8 README.md
git diff
git add README.md
git diff --staged
git commit -m "Ajouter un objectif d'apprentissage"
git log --oneline
```

`git diff` montre les changements non préparés ; `git diff --staged` montre ce qui sera enregistré dans le prochain commit. Rédigez des messages précis, par exemple « Ajouter le formulaire de contact ».

## 6. Publier sur GitHub

Sur GitHub, créez un dépôt nommé `pratique-git-cdi`. Choisissez sa visibilité selon les consignes du cours. Pour cet exercice démarré localement, créez le dépôt distant vide, sans README, licence ni `.gitignore`.

Remplacez `VOTRE-UTILISATEUR` dans la commande :

```powershell
git remote add origin https://github.com/VOTRE-UTILISATEUR/pratique-git-cdi.git
git remote -v
git push -u origin main
```

`origin` désigne la connexion au dépôt. L’option `-u` configure le suivi de la branche distante ; les envois suivants peuvent utiliser simplement `git push`.

Avec HTTPS, Git Credential Manager peut ouvrir le navigateur pour vous authentifier. Le mot de passe ordinaire de votre compte GitHub ne sert pas de mot de passe Git pour HTTPS.

## 7. Récupérer une modification distante

Modifiez le README sur GitHub et enregistrez un commit sur `main`. Avec un dossier de travail local propre, exécutez :

```powershell
git status
git pull --ff-only
```

Le README local contient désormais la modification distante. `--ff-only` refuse de créer une fusion si les historiques ont divergé : il faut alors examiner la situation.

```powershell
git fetch origin
```

`fetch` actualise les références distantes sans intégrer leurs changements dans votre branche de travail.

## 8. Cloner un dépôt existant

Si le professeur fournit un dépôt, copiez son URL et utilisez :

```powershell
git clone https://github.com/PROPRIETAIRE/DEPOT.git
cd DEPOT
git status
```

Remplacez les noms de l’exemple. `init` démarre un dépôt dans un dossier ; `clone` copie un dépôt existant. Cloner ne vous donne pas le droit d’envoyer des changements : suivez la procédure du professeur, qui peut demander un accès collaborateur ou un fork (copie du dépôt sur votre compte).

## 9. Travailler sur une branche et créer une PR

Commencez avec votre travail enregistré et votre branche principale à jour :

```powershell
git switch main
git pull --ff-only
git switch -c ajouter-notes
"# Notes du cours" | Set-Content -Encoding utf8 notes.md
git add notes.md
git commit -m "Ajouter les notes du cours"
git push -u origin ajouter-notes
```

Sur GitHub, ouvrez **Pull requests → New pull request**. Choisissez `main` comme branche de destination et `ajouter-notes` comme branche source. Examinez les changements, ajoutez une description et créez la PR. Dans votre dépôt d’exercice, fusionnez-la avec **Merge pull request**.

Actualisez ensuite votre copie locale :

```powershell
git switch main
git pull --ff-only
```

Le cycle de collaboration est : branche → modifications → commits → push → PR → révision → fusion.

## 10. Résoudre un conflit

Un conflit apparaît lorsque Git ne peut pas combiner automatiquement certains changements. Consultez `git status` pour identifier les fichiers et l’opération en cours.

```text
  <<<<<<< HEAD
Titre local
  =======
Titre de l'autre branche
  >>>>>>> autre-branche
```

Éditez le fichier pour conserver le résultat souhaité et supprimez les marqueurs. Pour terminer une fusion conflictuelle :

```powershell
git add README.md
git commit
```

Vérifiez le résultat avant de l’envoyer. Les instructions de fin diffèrent si le conflit survient pendant un rebase ; suivez alors les indications de `git status`.

## 11. Corriger des erreurs

| Besoin | Commande | Résultat |
| --- | --- | --- |
| Retirer un fichier de la préparation | `git restore --staged README.md` | Conserve les modifications dans le fichier |
| Abandonner les modifications non préparées | `git restore README.md` | Restaure le contenu préparé du fichier |
| Annuler un commit partagé | `git revert IDENTIFIANT` | Crée un nouveau commit qui inverse les changements |

**Attention : `git restore README.md` supprime les modifications non préparées de ce fichier.** Examinez `git diff` avant de l’utiliser. Retrouvez l’identifiant d’un commit avec `git log --oneline`. Si vous utilisez `revert`, partez d’un dossier de travail propre ; des conflits restent possibles.

## 12. Ignorer certains fichiers

Un fichier `.gitignore` peut contenir :

```gitignore
.env
node_modules/
*.log
```

Il permet d’ignorer les fichiers correspondants qui ne sont pas déjà suivis. Il ne retire pas les fichiers suivis ni les données présentes dans l’historique. N’enregistrez jamais de mots de passe ou de clés d’accès dans le dépôt.

## 13. Routine pour les travaux du cours

Au début, avec le travail précédent enregistré :

```powershell
git switch main
git status
git pull --ff-only
git switch -c travail-01
```

Après les modifications, remplacez `nom-du-fichier` par le fichier concerné :

```powershell
git diff
git add nom-du-fichier
git diff --staged
git commit -m "Decrire le changement"
git push -u origin travail-01
```

Pour les envois suivants sur cette branche, utilisez `git push`. Créez une PR si la procédure du cours le demande.

## Objectif de la première séance

- Créer un dépôt local et enregistrer deux commits.
- Publier le projet sur GitHub.
- Récupérer une modification faite sur GitHub.
- Créer une branche et la fusionner au moyen d’une PR.
- Expliquer la différence entre enregistrer un fichier, faire un commit et faire un push.

## Documentation officielle

- [Configuration initiale](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)
- [Enregistrement des changements](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)
- [Travail avec les dépôts distants](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)
- [Publication d’un projet local sur GitHub](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github)
- [Authentification HTTPS](https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git)
- [Exercice GitHub : branches et pull requests](https://docs.github.com/en/get-started/using-github/hello-world)
- [Conflits de fusion](https://docs.github.com/en/pull-requests/reference/merge-conflicts)
