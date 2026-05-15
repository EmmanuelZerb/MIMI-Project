# Guide Git - Projet MIMI

> Guide pour travailler ensemble sur le projet Blender sans tout casser :)

---

## C'est quoi Git ?

Git est un systeme de **sauvegarde intelligente**. Chaque fois qu'on fait un "commit", Git prend une photo de tout le projet. Si on casse quelque chose, on peut revenir en arriere.

Pense a ca comme les **sauvegardes automatiques d'un jeu video** :
- Tu as une sauvegarde principale (`main`)
- Tu peux creer des sauvegardes paralleles pour tester des trucs (`branches`)
- Si ton test marche, tu le fusionnes dans la sauvegarde principale

---

## Les Branches (Le Git Flow)

On utilise 3 niveaux de branches :

```
main  --->  la version PROPRE et STABLE (jamais de travail direct dessus)
  |
  dev  --->  la branche de travail (on merge nos features ici)
    |
    feature/nom  --->  pour tester un truc specifique
```

### En pratique :

| Branche | Quand l'utiliser | Exemple |
|---------|-----------------|---------|
| `main` | Jamais directement. C'est la version finale | - |
| `dev` | Pour travailler au quotidien | Modifications generales |
| `feature/cheveux` | Pour une tache specifique | Ajouter les cheveux au perso |
| `feature/textures` | Pour une tache specifique | Travailler les textures |

---

## Workflow quotidien

### 1. Avant de travailler - RECUPERER les derniers changements

```bash
git checkout dev
git pull origin dev
```

Ca recupere ce que l'autre a fait. **Toujours faire ca avant de commencer !**

### 2. Creer une branche pour ta tache

```bash
git checkout dev                    # etre sur dev
git checkout -b feature/ma-tache    # creer ET aller sur la nouvelle branche
```

### 3. Travailler sur Blender

Ouvre `MIMI.blend`, fais tes modifs, sauvegarde normalement dans Blender.

### 4. Sauvegarder ta progression (Commit)

```bash
# Voir ce qui a change
git status

# Ajouter tes changements
git add MIMI.blend

# Sauvegarder avec un message clair
git commit -m "ajout texture sol salon"
```

**Messages de commit utiles :**

| Prefixe | Signification | Exemple |
|---------|--------------|---------|
| `ajout` | Nouveau truc | `ajout eclairage cuisine` |
| `fix` | Correction | `fix deformations bras` |
| `wip` | Travail en cours | `wip cheveux encore en cours` |
| `render` | Un rendu | `render vue salon angle 2` |

### 5. Envoyer sur GitHub (Push)

```bash
git push origin feature/ma-tache
```

### 6. Fusionner dans dev (Merge)

Quand ta feature est finie :

```bash
git checkout dev
git pull origin dev              # recuperer les derniers changements
git merge feature/ma-tache       # fusionner ta branche dans dev
git push origin dev              # envoyer sur GitHub
```

Si plus personne n'utilise la branche feature :
```bash
git branch -d feature/ma-tache   # supprimer la branche locale
```

---

## Commandes essentielles (cheat sheet)

### Navigation

| Commande | Ce que ca fait |
|----------|---------------|
| `git status` | Voir ou on en est |
| `git log --oneline` | Voir l'historique |
| `git branch` | Voir les branches |
| `git checkout dev` | Aller sur dev |
| `git checkout -b feature/nom` | Creer + aller sur une branche |

### Sauvegarder

| Commande | Ce que ca fait |
|----------|---------------|
| `git add MIMI.blend` | Selectionner les changements |
| `git commit -m "message"` | Sauvegarder |
| `git push origin dev` | Envoyer sur GitHub |

### Recuperer

| Commande | Ce que ca fait |
|----------|---------------|
| `git pull origin dev` | Recuperer les changements |
| `git fetch --all` | Voir ce qu'il y a sur GitHub |

### Annuler

| Commande | Ce que ca fait |
|----------|---------------|
| `git stash` | Mettre de cote ses changements |
| `git stash pop` | Recuperer ses changements mis de cote |
| `git checkout -- MIMI.blend` | Annuler les modifs non commitees (DANGER) |

---

## Les regles d'or

1. **TOUJOURS `git pull` avant de travailler** - sinon tu risques des conflits
2. **JAMAIS de travail direct sur `main`** - toujours passer par `dev`
3. **Commit souvent** - petit messages clairs > un gros message flou
4. **Push a chaque fin de session** - pour que l'autre puisse recuperer
5. **Une branche = une tache** - pas 50 trucs en meme temps

---

## En cas de conflit

Si vous avez modifie le meme fichier, Git peut bloquer :

```bash
# 1. Voir le conflit
git status

# 2. Ouvrir Blender, choisir la version qu'on garde
#    (Git ne peut pas fusionner automatiquement les .blend)

# 3. Resoudre et commit
git add MIMI.blend
git commit -m "fix: resolution conflit"
```

### Astuce anti-conflit pour Blender

Les fichiers `.blend` sont binaires - Git ne peut PAS les fusionner automatiquement.
**La meilleure strategie : ne travaillez pas sur le meme fichier en meme temps.**

Si vous devez :
- Utilisez **File > Append** dans Blender pour importer les objets de l'autre
- Ou travaillez dans des **Scenes differentes** dans le meme fichier
- Communiquez sur qui fait quoi :)

---

## Workflow visuel

```
           vous deux travaillez
                 |
    +------------+------------+
    |                         |
feature/cheveux        feature/textures
    |                         |
    |  commit + push          |  commit + push
    |                         |
    +-------> dev <-----------+
                |
          merge + push
                |
              main
```

---

## Premiere fois - Cloner le projet

Si ta copine doit recuperer le projet pour la premiere fois :

```bash
git clone https://github.com/Nyrocks/MIMI-Project.git
cd MIMI-Project
git checkout dev
```

Puis ouvrir `MIMI.blend` dans Blender, et c'est parti !

---

*Guide genere avec amour par Claude Code pour le projet MIMI*
