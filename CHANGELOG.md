# Journal des versions

Chaque version publiée ici devient une **release GitHub** portant l'installeur, et c'est ce
texte qui sert de notes de version. `release.ps1` lit la section correspondant au numéro
courant — donc une version sans section ne se publie pas.

Format : `## X.Y — titre`, puis les rubriques **Ajouté**, **Modifié**, **Corrigé**.

---

## 2.6 — Disques séparés et espace regagné visible

### Ajouté
- **Choix des volumes à analyser** : une pastille par disque, avec son espace libre. Un seul,
  plusieurs ou tous.
- **Lecteurs réseau** proposés en option. Ils sont **décochés par défaut** : les parcourir
  passe par le réseau, c'est lent, et ça peut réveiller un serveur en veille.
- **Une ligne par disque** : nature du support (SSD, disque dur, réseau, amovible), espace
  libre, capacité et nombre de fichiers parcourus.
- **Écart d'espace visible.** L'espace libre relevé au premier passage sert de référence :
  après un nettoyage, la ligne affiche « **+ 38,0 Go depuis le début de la session** » et la
  portion regagnée se dessine **en vert** dans la barre. Voir « 391 Go libres » ne dit rien ;
  voir le terrain repris dit exactement ce que le ménage a rapporté.

### Modifié
- L'arborescence des tailles couvre plusieurs volumes : la racine est virtuelle et porte les
  lettres de lecteur comme premier niveau.
- Après une suppression, l'espace libre est **relu sur le disque** plutôt que déduit de ce
  qu'on croit avoir supprimé. C'est le disque qui a le dernier mot.

### Corrigé
- Les fichiers **sans extension** passent enfin par le classement selon leur emplacement :
  la rubrique « Autres » descend de 115 à 101 Go.

---
## 2.5 — Tout le contenu classé : documents, images, vidéos, musique

### Ajouté
- **Classement par type de contenu** : vidéos, images, musique, documents, projets créatifs,
  modèles IA, archives, installateurs, code, données de jeux, bibliothèques audio, machines
  virtuelles, paquets et extensions. Chaque type avec sa taille, son nombre de fichiers et une
  **barre proportionnelle** — comparer douze longueurs est immédiat, comparer douze nombres
  ne l'est pas.
- **Clic sur un type** pour n'afficher que ses plus gros fichiers.
- **Détection des copies exactes** (même nom, même taille au dernier octet près). Sur la
  machine de test : **76,5 Go en double**. Rien n'est supprimé — ce n'est pas une preuve
  formelle — le bouton ouvre le dossier pour comparer.

### Modifié
- La rubrique « Autres » est passée de **450 Go à 115 Go** grâce aux familles ajoutées après
  avoir recensé les extensions réellement présentes : `.minizip` (90 Go de données Forza),
  `.aux` / `.bank` / `.multisample` (96 Go de bibliothèques de samples), `.tfc` / `.upk`
  (données Unreal), `.vhdx` (machines virtuelles), `.vsix` / `.jar`.
- Les fichiers **sans extension** — 46 Go et 323 000 fichiers — sont classés par emplacement :
  objets Git et `node_modules` en code, contenus de caches en temporaires.

### Corrigé
- Taille tronquée dans la liste des types : le libellé chevauchait le bouton de 38 px.
  `--layouttest` ne l'avait pas vu parce qu'il visitait la page Stockage **vide** — il la
  remplit désormais avant de mesurer.
- Chevauchements dans les lignes de fichiers après élargissement du libellé « copies ».

---
## 2.4 — Onglet Stockage

### Ajouté
- **Onglet « Stockage ».** Un parcours complet du disque en moins de 80 secondes
  (2,2 millions de fichiers), qui répond à une seule question : qu'est-ce qui prend de la
  place, et est-ce que je m'en sers ?
- **Logiciels et jeux, du plus gros au plus petit**, chacun avec son **icône**, sa taille
  réelle mesurée sur le disque, la **date du dernier lancement** et un bouton Désinstaller.
  Un logiciel volumineux non ouvert depuis plus de deux mois est signalé en ambre.
- **Un bouton qui libère les caches** directement depuis la vue, avec le montant récupérable
  affiché avant de cliquer.
- **Fichiers les plus lourds** avec leur date de dernier accès. Rien n'est supprimé
  automatiquement : ce sont tes fichiers, le bouton ouvre le dossier et tu décides.
- Jeux Steam et Epic reconnus par leurs manifestes, y compris les bibliothèques secondaires.
- **`--storetest`** et **`--icontest`** pour vérifier le moteur et l'extraction des icônes
  sans passer par l'interface.

### Modifié
- Taille réelle mesurée sur le disque au lieu de la valeur `EstimatedSize` du registre, qui
  est déclarative et souvent fausse ou absente.

### Corrigé
- **Double comptage des lanceurs.** Steam déclarait 160 Go et Epic Games Launcher 172 Go
  parce que leur emplacement d'installation contient les jeux — lesquels étaient en plus
  listés séparément. Ce qui appartient à un poste listé est maintenant déduit de son parent :
  Steam retombe à 1,3 Go, et les jeux apparaissent pour ce qu'ils sont.
- **Icône du désinstalleur affichée à la place de celle du logiciel** : `DisplayIcon` pointe
  souvent sur `unins000.exe`. Le binaire principal est préféré, avec repli progressif pour
  les greffons audio qui n'installent réellement que leur désinstalleur.
- **Jeux marqués « jamais vu »** : lancés par Steam ou Epic, ils n'apparaissent pas dans
  UserAssist puisque ce n'est pas l'Explorateur qui les démarre. On lit désormais l'heure
  d'accès de leur exécutable, y compris dans les sous-dossiers.
- Parcours passé de 110 à 80 secondes : `C:\Users` occupait un seul fil pendant que les
  autres avaient fini.

### Note
Le dossier Prefetch, source idéale pour dater le dernier lancement d'un programme, est vide
sur cette machine : **notre propre optimisation coupe le service SysMain sur SSD**. C'est un
effet de bord assumé — le gain au démarrage vaut la perte de cette statistique — mais il
fallait le dire. On se rabat sur UserAssist et sur les heures d'accès NTFS.

---
## 2.3 — Nettoyage des caches applicatifs et des caches de jeux

### Ajouté
- **Découverte automatique des caches d'applications et de jeux.** L'application ne se limite
  plus à une quinzaine d'emplacements fixes : elle explore `%LOCALAPPDATA%`, `%APPDATA%` et le
  dossier Steam et reconnaît les caches régénérables. Sur une machine de test : **1011
  emplacements, 56,4 Go récupérables** contre 8 Go auparavant.
- Caches désormais reconnus : navigateurs et applications Electron (`Cache`, `Code Cache`,
  `GPUCache`, `ShaderCache`, `cache2`), gestionnaires de paquets (`uv`, `pip`, `npm`),
  caches de shaders AMD `DxcCache` et `GLCache` et Intel, caches web Steam et Epic,
  journaux et rapports de plantage des jeux.
- **`--cachescan`** : liste ce qui serait effacé, avec les tailles, sans rien supprimer.

### Modifié
- **Le nettoyage fonctionne par liste blanche, jamais par liste noire.** Seuls les noms de
  dossiers explicitement reconnus comme régénérables sont touchés. Une liste noire finirait
  toujours par oublier un cas et effacerait quelque chose d'irremplaçable ; une liste blanche,
  au pire, oublie de nettoyer.
- Budget de mesure porté de 3 à 12 secondes : avec plus de mille emplacements, l'ancien budget
  n'aurait couvert qu'une fraction de ce qui est réellement effacé, et aurait affiché un
  chiffre faux.

### Corrigé
- Rien à corriger : cette version ajoute une capacité, elle ne répare pas de défaut.

### Sécurité du nettoyage
Dans un jeu Unreal, le jetable et l'irremplaçable sont **voisins dans le même dossier**
`Saved` : `Logs` et `Crashes` côtoient `Config` (qui contient `GameUserSettings.ini`,
c'est-à-dire les réglages graphiques), `SaveGames` (la progression), `Demos` (les replays
enregistrés par le joueur) et `Autosaves` (le travail dans l'éditeur).

Trois barrières cumulatives, vérifiées par 33 cas de test :

1. le chemin doit être sous une racine autorisée, séparateur compris ;
2. **aucun segment du chemin** ne doit être un dossier interdit — un dossier nommé `Cache`
   placé sous `SaveGames` reste hors de portée ;
3. le dossier doit figurer dans la liste des cibles déclarées.

Ne sont jamais touchés : sauvegardes, réglages, replays, captures d'écran, travaux
d'éditeur, données de session et de compte des navigateurs (`Local Storage`, `IndexedDB`,
`Cookies`), `userdata` de Steam, et la corbeille.

---

## 2.2 — Releases, notes de version et mise à jour par installeur

### Ajouté
- **Publication par release GitHub.** Chaque version crée une release portant l'installeur
  `BetterWindows-Setup-X.Y.exe` et l'exécutable portable, avec ses notes de version.
- **Notes de version affichées après une mise à jour.** L'application montre une fois, au
  premier lancement de la nouvelle version, ce qui a été ajouté, modifié et corrigé.
- **`release.ps1`** : compile, vérifie, étiquette, publie la release et téléverse les fichiers
  en une commande. Refuse de publier si les tests échouent ou si la version existe déjà.
- **`--tryupdate --dry`** : interroge la release distante et affiche ce qui serait installé,
  sans rien installer.

### Modifié
- **La mise à jour passe par l'installeur** quand l'application est installée : lui seul sait
  mettre à jour les raccourcis et l'entrée « Applications installées ». Une copie portable
  continue de se remplacer directement.
- **Redirections suivies mais revalidées.** Les fichiers de release passent par un CDN ; l'hôte
  est vérifié à chaque saut contre une liste d'hôtes GitHub connus.
- **JSON réellement désérialisé** au lieu d'être découpé à la main : une note de version
  contenant une accolade ou un guillemet ne casse plus la lecture.

### Corrigé
- Un tag de release illisible (`latest`, `2.2-beta`, vide) est refusé au lieu d'être comparé
  n'importe comment.

---

## 2.1 — Better Windows

### Ajouté
- **Mise à jour automatique** au lancement, silencieuse, avec conservation de la version
  précédente en `.old`.
- **Rubrique « Services Windows »** dans le menu. Enterrés en quatrième section d'un autre
  onglet, ils étaient introuvables.
- **Bouton « Capturer l'affichage »** dans l'en-tête : enregistre côte à côte les pixels
  réellement affichés et un rendu propre du même état, pour diagnostiquer un défaut de rendu
  au moment où il se produit.
- **Fondu entre les pages**, et rendu gelé pendant la reconstruction.
- Modes de vérification `--layouttest`, `--stresstest`, `--halotest`, `--flowtest`,
  `--handletest`, `--updatetest`.

### Modifié
- **L'application s'appelle Better Windows.** Les données sont migrées de
  `%LOCALAPPDATA%\WindowsChecker` vers `BetterWindows`, sauvegardes de registre comprises.
- **Rendu à la résolution réelle de l'écran** (DPI aware). Sur un écran à 250 %, Windows
  agrandissait jusqu'ici une image basse définition.
- **Barre latérale plaquée et pleine hauteur**, arrondie du seul côté du contenu.
- Espacements uniformisés : 12 px entre deux boutons, 20 px avant un texte d'explication.

### Corrigé
- **Coins des boutons en noir.** `ButtonBase` active `ControlStyles.Opaque`, donc Windows
  n'appelle jamais `OnPaintBackground` à l'écran ; le fond est désormais peint dans `OnPaint`.
- **81 chevauchements** entre contrôles, dont les descriptions des 74 lignes de l'onglet
  Démarrage qui passaient sous la valeur de RAM.
- Titres tronqués et libellés superposés dans Réglages avancés.
- Cadres arrondis tracés à la taille exacte du contrôle : plus de liseré de fond sur un bord.
- Résidus d'affichage au défilement et au redimensionnement.
- L'installeur ne pouvait pas lancer l'application en fin d'installation (erreur 740).

---

## 2.0 — Optimisation en un clic

### Ajouté
- Bouton **« TOUT OPTIMISER »** : capture avant, optimisations, nettoyage, capture après,
  comparatif chiffré.
- Détection automatique du profil (gaming / création / bureautique) d'après les composants et
  les logiciels installés.
- Banc de vitesse disque en accès non bufferisé, mesure du temps de démarrage de Windows et du
  temps de lancement d'une application.
- Installeur Inno Setup, Benchmark Lab.
