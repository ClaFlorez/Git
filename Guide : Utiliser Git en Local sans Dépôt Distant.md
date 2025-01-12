# Guide : Utiliser Git en Local sans Dépôt Distant

## 🚀 Étape 1 : Installer Git
Assurez-vous d'avoir Git installé sur votre ordinateur. Si ce n'est pas le cas, [téléchargez-le ici](https://git-scm.com/) et installez-le.

## 🗂️ Étape 2 : Ouvrir Git Bash et Naviguer vers le Dossier
1. **Ouvrez Git Bash**.
2. **Naviguez vers le dossier de votre projet** en utilisant la commande `cd` :

```bash
cd /path/to/your/project
```

## 🛠️ Étape 3 : Initialiser le Dépôt Git
Initialisez un nouveau dépôt Git dans le dossier actuel avec la commande :

```bash
git init
```

Cela crée un dossier `.git` dans votre projet pour permettre à Git de suivre les modifications.

## ➕ Étape 4 : Ajouter des Fichiers à la Zone de Préparation
- Pour ajouter **tous les fichiers** du dossier actuel :

```bash
git add .
```

- Pour ajouter un **fichier spécifique** :

```bash
git add <nom_du_fichier>
```

## ✅ Étape 5 : Réaliser un Commit
1. Vérifiez l'état du dépôt :

```bash
git status
```

2. Confirmez les modifications avec un message descriptif :

```bash
git commit -m "Message descriptif du commit"
```

 3. Pour recouperer un ancien version :

```bash
git log
git checkout <commit ID>
```
## 🌿 Étape 6 : Gérer les Branches (Optionnel)
- Créer une nouvelle branche :

```bash
git branch <nom_de_la_branche>
```

- Changer de branche :

```bash
git checkout <nom_de_la_branche>
```

- Créer et changer de branche en une seule commande :

```bash
git checkout -b <nom_de_la_branche>
```

## 🔄 Étape 7 : Fusionner des Branches (Optionnel)
Pour fusionner une branche secondaire avec la branche principale :

```bash
git checkout main
git merge <nom_de_la_branche>
```

## 📜 Étape 8 : Vérifier l'Historique des Commits
Affichez l'historique des commits :

```bash
git log
```

## 📂 Utiliser le Fichier `.gitignore`
Pour ignorer certains fichiers ou répertoires, créez un fichier `.gitignore` à la racine de votre projet et ajoutez les chemins des fichiers ou dossiers que vous souhaitez ignorer.

## 📋 Exemples de Commandes
Voici quelques commandes utiles :

| Commande          | Description                              |
|-------------------|------------------------------------------|
| `git status`      | Vérifie l'état du dépôt.                 |
| `git log`         | Affiche l'historique des commits.        |
| `git branch`      | Gère les branches.                      |
| `git checkout`    | Change de branche.                      |
| `git merge`       | Fusionne des branches.                  |
| `git add`         | Ajoute des fichiers à la zone de préparation. |
| `git commit`      | Confirme les modifications.             |
| `git diff`        | Affiche les différences entre les versions. |

## 🏁 Conclusion
En suivant ces étapes, vous pouvez utiliser Git pour gérer les versions de vos fichiers localement, sans dépôt distant. Cela vous permettra de suivre les modifications, de créer des branches et de fusionner les changements de manière efficace.

---
🎉 **Bon codage !**

![image](https://github.com/user-attachments/assets/02f996b5-2626-4e30-b155-855a73807cc8)
