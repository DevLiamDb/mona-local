<div align="right">

[🇬🇧 English](README.md) | 🇫🇷 Français

</div>

<div align="center">

<img src="docs/banner.gif" alt="Mona : le David de Michel-Ange en ASCII, balayé par une lumière" width="420">

# MONA

**Vois ton site comme le verrait un nouveau visiteur.**

[![Licence](https://img.shields.io/badge/licence-usage%20personnel-d9b877?labelColor=141413)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.10%2B-d9b877?labelColor=141413&logo=python&logoColor=white)](https://www.python.org/downloads/)
![Systèmes](https://img.shields.io/badge/Windows%20·%20macOS%20·%20Linux-8a8a84?labelColor=141413)
![IA](https://img.shields.io/badge/IA-tourne%20sur%20ton%20PC-9bc7a8?labelColor=141413)
![Modèles](https://img.shields.io/badge/mod%C3%A8les-ONNX%20inclus-9bc7a8?labelColor=141413&logo=onnx&logoColor=white)
![Chrome](https://img.shields.io/badge/capture-vrai%20Chrome-d9b877?labelColor=141413&logo=googlechrome&logoColor=white)
![Cloud](https://img.shields.io/badge/cloud-aucun-d98577?labelColor=141413)

<br>

**Tu as dessiné la page. Tu ne peux plus la voir pour la première fois.**

**Mona devine où se posent les yeux d'un nouveau visiteur, et te dit ce qui le gêne.**

*Créé par Liam DB, avec l'aide de l'IA.*

</div>

---

<div align="center">

<img src="docs/demo.gif" width="760" alt="Mona analyse une page web : animation en caractères, puis le rapport">

*Mona sur une page web : une statue en ASCII pendant le travail, puis le rapport.*

</div>

---

> J'ai créé Mona pour montrer aux designers web ce que voit un nouveau visiteur : elle ouvre ta page dans un Chrome de test, puis lance des modèles d'IA **sur ton propre PC** pour deviner le regard, estimer la réaction du cerveau et noter la lisibilité, sans rien envoyer. Le code et les modèles sont dans ce [dépôt GitHub](https://github.com/LiamLitle/mona-local), et j'explique la méthode et publie mes mesures sur [mona.devliam.com](https://mona.devliam.com).

<div align="center">
<table>
<tr>
<td align="center" width="16%">

**👁️ Regard**<br>
Une carte de chaleur<br>
de ce qu'on voit d'abord,<br>
avec 2 modèles

</td>
<td align="center" width="16%">

**🧠 Cerveau**<br>
Réponse de 20 zones<br>
visuelles du cortex<br>
(indicatif)

</td>
<td align="center" width="16%">

**📊 Note /100**<br>
Six vérifications<br>
de lisibilité, avec<br>
des conseils par écran

</td>
<td align="center" width="16%">

**🔎 Détecteur**<br>
Repère textes, boutons,<br>
images, champs, icônes<br>
sur toute capture

</td>
<td align="center" width="16%">

**🏠 100 % local**<br>
Pas de compte, pas<br>
de cloud, pas<br>
de suivi

</td>
<td align="center" width="16%">

**⚙️ S'adapte à ton PC**<br>
Lit ton processeur,<br>
ta mémoire, ta carte<br>
graphique, puis choisit

</td>
</tr>
</table>
</div>

---

## 📏 Pourquoi Mona

Un avis sur un design est facile à donner et difficile à vérifier. Mona donne des chiffres, mesurés sur des cas **jamais vus pendant l'apprentissage**.

| Quoi | Résultat |
|---|:---:|
| Regard comparé à de vrais regards (UEyes) | corrélation **0,68** |
| Regard sur des pages web d'un autre jeu de données (Imp1k) | corrélation **0,56** |
| Détecteur d'éléments (texte, bouton, image) | F1 **0,64** |
| Note depuis une image seule comparée à celle du code de la page | **5,5 points** sur 100 d'écart en moyenne |

Mona n'a pas toujours raison. Le modèle du cerveau vient d'un seul sujet : une indication, pas un diagnostic. Mona mesure la lisibilité et l'attention, **pas le goût**, et ne remplace ni un test avec de vraies personnes ni un audit d'accessibilité. La méthode et les limites sont sur le [site](https://mona.devliam.com/benchmarks.html).

---

## 🎯 À quoi ça sert

- **Vérifier un design avant de le montrer :** où va l'œil en premier, et est-ce le bon endroit ?
- **Trouver le bouton principal :** l'appel à l'action est-il visible dès le premier écran, qui compte pour la moitié de la note ?
- **Contraste et taille du texte :** un passage rapide de type WCAG sur chaque écran d'une longue page.
- **Maquettes et exports Figma :** dépose une image, le détecteur lit l'interface depuis les pixels.
- **Comparer deux versions :** analyse chacune, garde les deux rapports, compare les deux notes.
- **Tes sites, ton ordinateur :** pas besoin d'envoyer une maquette inédite à un outil en ligne.

---

## 📦 Installation

> Prérequis : **Python 3.10+**. Les modèles d'IA sont déjà dans le dépôt.
>
> Testé sur **Windows 11** et **Ubuntu** (WSL). macOS n'est pas encore testé.

[Télécharge le ZIP](https://github.com/LiamLitle/mona-local/archive/refs/heads/main.zip) ou clone le dépôt, puis :

| | |
|---|---|
| **Windows** | double-clique sur **`Mona.bat`** |
| **macOS, Linux** | lance **`./mona.sh`** |

La première fois, le lanceur installe tout : les paquets Python et le Chrome de test, environ 150 Mo, quelques minutes. Ensuite l'application s'ouvre tout de suite, dans sa propre fenêtre.

**Tu préfères le faire à la main ?**

```bash
pip install -r requirements.txt
python -m mona setup      # installe le Chrome de test, une seule fois
python -m mona            # ouvre l'application
```

Pour une fenêtre native à la place d'une fenêtre Chrome/Edge : `pip install -r requirements-app.txt`.

---

## 🚀 Utilisation

### 1. Analyser un site

Colle une adresse. Mona l'ouvre dans un Chrome de test en 1440 × 900, fait défiler jusqu'en bas (12 écrans au plus), lit les textes, tailles, couleurs et boutons de chaque écran, puis lance les modèles.

### 2. Analyser une image

Dépose une capture, une maquette ou un export Figma. Les images longues sont découpées en écrans, le **détecteur** repère les éléments de l'interface et le **plan B** reconstruit ce que le code de la page aurait donné. La note est alors indicative (environ 5,5 points d'écart).

### 3. Lire le rapport

Une carte du regard et une note pour chaque écran, une réaction du cerveau, un conseil par règle. Le premier écran compte pour la moitié de la note finale. Les rapports restent dans le stockage de l'application, sur ton PC. Exporte-les en JSON ou imprime-les en PDF.

### 4. Utiliser la ligne de commande *(facultatif)*

```bash
python -m mona analyze https://example.com    # analyser sans l'interface
python -m mona analyze capture.png            # analyser une image
python -m mona doctor               # ton PC, les réglages choisis par Mona, l'état des modèles
python -m mona serve                # serveur seul, sans fenêtre
```

### 5. Lancer les tests *(facultatif)*

```bash
python -m pytest
```

Variables d'environnement : `MONA_PORT`, `MONA_MAX_SCREENS` (12 par défaut), `MONA_HEADLESS=1` (cacher le Chrome de test), `MONA_HOME` (où sont rangés les réglages).

---

## 🗿 Les modèles d'IA

Mona contient **ses propres modèles d'IA**, dans [`models/`](models). Ils n'écrivent pas de texte et ne te parlent pas : chacun transforme une page en carte ou en liste.

| Modèle | Fichier | Ce qu'il fait |
|---|---|---|
| **Regard A et B** | `gaze_a.onnx`, `gaze_b.onnx` | Devinent où les yeux se posent. Leurs deux cartes sont moyennées. Appris sur des données de suivi du regard (62 personnes, 1 980 interfaces). |
| **Cerveau** | `brain.onnx` | Estime la réponse de 20 zones visuelles, en percentile face à environ 500 pages web. Appris sur des données d'IRM. Indicatif, hors de la note. |
| **Détecteur** | `detector.onnx` | Repère textes, boutons, images, champs et icônes sur une capture. |
| **Plan B** | `plan_b_params.json` | Transforme la sortie du détecteur en les mêmes informations que le code de la page. |

- **Où ils tournent :** sur ton processeur ou ta carte graphique, au format ONNX, avec onnxruntime. Pas de cloud, aucun appel d'API. [`mona/hardware.py`](mona/hardware.py) lit ton PC, choisit les threads et le parallélisme, et laisse un quart des cœurs libres.
- **Intégrité :** `models/MODELS.json` liste la taille et le SHA-256 de chaque fichier, pour vérifier qu'ils sont intacts.
- **Licences :** les données d'apprentissage et les poids pré-entraînés ont leurs propres conditions. Le modèle du cerveau dérive d'images réservées à la recherche et ne sert qu'à de la recherche non commerciale.

Le rôle, l'entrée, la sortie, les données d'apprentissage et la licence de chaque modèle sont dans [`docs/MODELS.md`](docs/MODELS.md).

---

<details>
<summary><b>🗂️ Structure des fichiers</b></summary>
<br>

```
mona-local/
├── Mona.bat · mona.sh    ← lanceurs en un clic ← COMMENCE ICI
├── models/               ← LES MODÈLES D'IA (*.onnx) + MODELS.json
├── mona/                 ← l'application
│   ├── ai/               ← fait tourner les modèles : regard, cerveau, détecteur, plan B
│   ├── capture.py        ← le Chrome de test : ouvrir, défiler, capturer
│   ├── rules.py          ← six règles de lisibilité et la note
│   ├── pipeline.py       ← enchaîne tout, signale l'avancement par événements
│   ├── server.py         ← API locale (127.0.0.1 seulement)
│   ├── desktop.py        ← lance le serveur, ouvre la fenêtre
│   ├── hardware.py       ← lit ton PC, choisit les réglages
│   └── web/              ← l'interface (fichiers simples, sans compilation)
├── docs/                 ← ARCHITECTURE.md, MODELS.md, bannière et démo
├── tests/                ← tests automatiques
├── tools/                ← scripts de maintenance
└── LICENSE, TERMS.md, PRIVACY.md, NOTICE.md
```

</details>

---

<details open>
<summary><b>📐 Les six règles de lisibilité</b></summary>
<br>

| Règle | Ce qu'elle vérifie | Dans la pratique |
|---|---|---|
| **Contraste du texte** | Contraste entre chaque texte et la couleur derrière | Un gris sur blanc qui échoue au WCAG est signalé |
| **Taille du texte** | Taille des textes qu'on lit | Texte courant trop petit pour lire confortablement |
| **Bouton principal** | L'action principale est-elle visible et facile à trouver | Un appel à l'action perdu parmi le reste |
| **Hiérarchie visuelle** | Une chose passe-t-elle clairement en premier | Tout a la même taille, rien ne guide |
| **Quantité de texte** | Combien de mots se disputent l'attention | Un mur de texte en haut de page |
| **Surcharge** | À quel point l'écran est chargé | Trop d'éléments qui se battent pour l'œil |

Chaque écran reçoit une note. Le premier écran compte pour la moitié de la note finale sur 100. Les règles sont dans [`mona/rules.py`](mona/rules.py) et reprises sur le site avec les mêmes seuils et les mêmes poids.

</details>

---

<details>
<summary><b>⚙️ Comment ça marche à l'intérieur</b></summary>
<br>

```
fenêtre ──► server.py ──► pipeline.py ──► capture.py (Chrome de test : ouvrir, défiler, lire)
(pywebview,   (FastAPI,       │
 ou appli      127.0.0.1)     ├── ai/  regard + cerveau + détecteur (ONNX, onnxruntime)
 Chrome/Edge)                 └── rules.py  six règles ──► note /100
```

- **Ouvrir :** le Chrome de test charge l'adresse dans une fenêtre de 1440 × 900. Pour une image, Mona la découpe en écrans de 900 px.
- **Lire :** pour chaque écran, le code de la page donne textes, tailles, couleurs et boutons. Pour une image, le détecteur les repère et le plan B reconstruit les mêmes informations.
- **Regarder :** deux modèles devinent où les yeux se posent et leurs cartes sont moyennées. Un modèle estime la réponse du cerveau.
- **Juger :** les six règles donnent une note par écran, puis la note finale sur 100.

Le schéma complet et la visite fichier par fichier sont dans [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md).

</details>

---

<details>
<summary><b>❓ FAQ</b></summary>
<br>

**C'est gratuit ?**
Oui, pour un usage personnel non commercial. Voir la licence plus bas.

**Puis-je m'en servir pour un client ou dans mon produit ?**
Pas sans l'accord écrit de l'auteur. Voir [LICENSE](LICENSE).

**Ça marche sur téléphone ?**
Non, c'est une application de bureau (Windows, macOS, Linux).

**C'est rapide ?**
Sur un PC récent, une image prend quelques secondes et une page une dizaine. `python -m mona doctor` montre ce que Mona a choisi pour ta machine.

**Où vont mes rapports ?**
Nulle part : ils restent dans le stockage de l'application, sur ton PC. Le seul trafic réseau est la visite du site que tu analyses.

**Faut-il une carte graphique ou un compte ?**
Non. Mona utilise une carte graphique si elle en trouve une, sinon elle tourne sur le processeur. Pas de compte, pas de clé d'API.

**Peut-elle analyser une page derrière une connexion, ou sur localhost ?**
Pas encore. Le Chrome de test ouvre des adresses publiques. Pour une page privée, fais une capture d'écran et dépose l'image.

</details>

---

## 📖 Histoire et crédits

<details>
<summary><b>🙏 Crédits : qui et quoi a fait Mona</b></summary>
<br>

Mona a été **écrit avec l'IA, et on le dit clairement.**

| Qui | Rôle |
|---|---|
| **Liam DB** | Créateur. L'idée, la direction, les décisions, les tests. |
| **[Claude Code](https://claude.com/claude-code)** (Anthropic) | A écrit le code du projet sous la direction de Liam DB. |

**Construit sur :** des données de suivi du regard (UEyes, Imp1k), des données d'IRM (THINGS), [ONNX Runtime](https://onnxruntime.ai/), [Playwright](https://playwright.dev/) et [FastAPI](https://fastapi.tiangolo.com/).

**Trouver le créateur :** [devliam.com](https://devliam.com) · [mona.devliam.com](https://mona.devliam.com)

La liste complète des données, modèles, bibliothèques et licences est dans [NOTICE.md](NOTICE.md). Pour citer Mona, utilise le bouton « Cite this repository » de GitHub ([CITATION.cff](CITATION.cff)).

</details>

---

## ⚖️ Licence

**Mona Personal Use License** ([LICENSE](LICENSE), avec traduction française)

✅ Gratuit pour toi : usage personnel, pédagogique, recherche
✅ Lire et modifier le code pour ton propre usage
✅ Tes rapports t'appartiennent
❌ Pas de redistribution, pas de vente, pas d'usage pour gagner de l'argent (travail pour un client et services en ligne compris)
❌ Pas d'entraînement d'autres modèles avec Mona
❌ Crédit obligatoire (« Mona by Liam DB ») dès que tu montres ou publies quelque chose qui s'en sert

C'est du *source disponible*, pas de l'open source. Pour tout le reste, demande d'abord à l'auteur.

[Conditions d'utilisation](TERMS.md) · [Confidentialité](PRIVACY.md) · [Données et licences tierces](NOTICE.md)

---

<div align="center">

Créé par Liam DB, avec l'aide de l'IA.

</div>

<sub>Mots-clés : analyse de page web, saillance visuelle, prédiction du regard, carte de chaleur de l'attention, audit UX, note de lisibilité, contraste WCAG, analyse de maquette Figma, détection d'éléments d'interface, ONNX, Playwright, application de bureau.</sub>
