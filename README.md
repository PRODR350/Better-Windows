# Better Windows

**Un logiciel Windows natif qui analyse ta machine, comprend pourquoi elle rame, l'optimise en un clic — et te prouve le résultat avec un comparatif chiffré avant / après.**

Tout est **réversible** : un point de restauration système et une sauvegarde du registre sont créés avant la moindre modification.

[**⬇ Télécharger la dernière version**](https://github.com/PRODR350/Better-Windows/releases/latest)

---

## Ce qu'il fait

### ⚡ Optimiser en un clic
Capture des performances **avant**, optimisations, nettoyage, capture **après**, comparatif chiffré. Aucune case à cocher : le catalogue s'adapte tout seul à la machine.

Le profil est détecté automatiquement d'après les composants et les logiciels installés :

| Profil | Détecté quand |
|---|---|
| **Gaming** | carte graphique dédiée **+** jeux ou launchers |
| **Création** | carte graphique dédiée **+** logiciels de création, sans jeux |
| **Bureautique** | **aucune** carte graphique dédiée |

Jeux **et** logiciels de création ? Le profil devient « Gaming (+ création préservée) » : optimisation gaming complète, sans casser ce dont Photoshop ou Premiere ont besoin.

### 📊 Ce qui est mesuré
Pas des estimations : des mesures.

- Temps de démarrage de Windows, lu dans le journal que Windows tient lui-même
- Temps de lancement d'une application — reflet direct de la charge de fond
- Banc de vitesse disque en **accès non bufferisé** (sinon Windows sert depuis le cache et le chiffre ne veut rien dire), IOPS 4K et latence
- CPU au repos, mémoire, processus, services actifs
- Programmes, services tiers et tâches lancés au démarrage

### 💽 Stockage
Un parcours complet du disque en moins de 80 secondes, pour répondre à une seule question : **qu'est-ce qui prend de la place, et est-ce que je m'en sers ?**

- Logiciels et jeux du plus gros au plus petit, avec leur icône, leur taille réellement mesurée et la **date du dernier lancement**
- Tout le contenu classé : vidéos, images, musique, documents, projets créatifs, modèles IA, archives, bibliothèques audio, données de jeux…
- Détection des **copies exactes**
- Les caches jetables, avec le montant récupérable affiché avant de cliquer
- Plusieurs disques, lecteurs réseau en option, et l'**espace regagné** affiché après chaque nettoyage

### 🛡️ Services Windows
Les services que l'optimisation peut couper, chacun avec son interrupteur. Tu peux en **rallumer un seul** sans rien annuler d'autre : il reprend son type de démarrage d'origine et redémarre immédiatement.

### 🚀 Démarrage, 🖥️ Logiciels, 🌙 Repos, 🔍 Diagnostic, 🎮 GPU
Ce qui se lance tout seul, ce qui tourne en ce moment, ce que consomme la machine quand tu ne fais rien, tous les constats classés par impact, et les réglages du pilote graphique.

---

## Le nettoyage ne casse rien

Dans un jeu Unreal, le jetable et l'irremplaçable sont **voisins dans le même dossier** :

```
FortniteGame\Saved\Logs                  ← jetable
FortniteGame\Saved\Crashes               ← jetable
FortniteGame\Saved\Config                ← TES RÉGLAGES GRAPHIQUES
FortniteGame\Saved\SaveGames             ← TA PROGRESSION
FortniteGame\Saved\Demos                 ← TES REPLAYS
UnrealEditorFortnite\Saved\Autosaves     ← TON TRAVAIL DANS L'ÉDITEUR
```

Le nettoyage fonctionne donc par **liste blanche**, jamais par liste noire : seuls les noms de dossiers explicitement reconnus comme régénérables sont touchés. Une liste noire finirait par oublier un cas et effacerait quelque chose d'irremplaçable ; une liste blanche, au pire, oublie de nettoyer.

**Jamais touchés** : sauvegardes, réglages, replays, captures d'écran, travaux d'éditeur, cookies et sessions des navigateurs, `userdata` de Steam, et la corbeille.

---

## Mise à jour automatique

L'application se met à jour toute seule au lancement, depuis les releases de ce dépôt. Rien à faire.

Une installation classique passe par l'installeur silencieux — lui seul sait mettre à jour les raccourcis et l'entrée « Applications installées ». Une copie portable se remplace directement, en conservant la version précédente.

Tout échec est silencieux : hors ligne, en avion, derrière un proxy, l'application démarre normalement.

---

## Installation

| | |
|---|---|
| **Installeur** | Dossier `Program Files`, raccourcis, désinstalleur, choix des composants, français et anglais. |
| **Portable** | Copie `BetterWindows.exe` où tu veux et double-clique. |

Tes données vivent dans `%LOCALAPPDATA%\BetterWindows` — sauvegardes de registre, captures et rapports. Elles ne sont **pas** supprimées par une désinstallation, pour que tu puisses toujours annuler une optimisation.

> Désinstaller **n'annule pas** les optimisations. Pour revenir en arrière, utilise « Annuler la dernière optimisation » **avant** de désinstaller.

**Windows 10 ou 11, 64 bits.** Droits administrateur requis : l'application écrit dans le registre système et pilote des services.

---

## Licence

**Logiciel propriétaire. Tous droits réservés.**

Ce dépôt ne distribue que des binaires. Le code source n'est pas public. La copie, la modification, la décompilation, la rétro-ingénierie et la redistribution ne sont pas autorisées.

© PRODR350
