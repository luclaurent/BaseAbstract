# Template d'abstract de projet de recherche

Ce modèle LaTeX est prêt à compiler avec XeLaTeX, BibTeX et `natbib`. Il peut aussi être configuré avec pdfLaTeX ou `biblatex`/Biber.

## Démarrage rapide

```sh
xelatex abstract.tex
bibtex abstract
xelatex abstract.tex
xelatex abstract.tex
```

Le fichier à personnaliser est `abstract.tex`. Les références sont stockées dans `references.bib` et les figures dans `figs/`.

## Français

### Présentation

Ce dépôt contient un modèle LaTeX pour rédiger un abstract de projet d'initiation à la recherche dans le cadre de l'IAE2 USAE2L-4 du Cnam.

Le document est conçu pour produire un document de **3 pages de cœur au maximum**, auquel peuvent s'ajouter une page de références et une page d'illustrations en annexe. Il propose une structure commune pour les rendus intermédiaire et final.

### Contenu du modèle

Le fichier `abstract.tex` contient notamment les sections suivantes :

- introduction, contexte et problématique ;
- objectifs ;
- méthodologie ;
- modèles mathématiques, physiques et/ou algorithmiques ;
- résultats attendus ou obtenus ;
- conclusion et perspectives ;
- références bibliographiques.

Une section `Instructions` rappelle également les éléments attendus pour le rendu intermédiaire et le rendu final.

### Prérequis

Installer une distribution LaTeX complète comprenant :

- XeLaTeX, recommandé pour la gestion des polices ;
- BibTeX (utilisé par défaut), Biber ou natbib ;
- les paquets LaTeX utilisés dans le document, notamment `biblatex`, `natbib`, `authblk`, `caption`, `subcaption`, `fancyhdr`, `graphicx`, `raleway` et `titlesec` ;
- la police Raleway, si elle n'est pas fournie par la distribution LaTeX.

Sur macOS, MacTeX est recommandé. Une installation complète de TeX Live convient également.

### Compilation

Depuis le répertoire du projet, la configuration natbib actuellement activée se compile avec BibTeX :

```sh
xelatex abstract.tex
bibtex abstract
xelatex abstract.tex
xelatex abstract.tex
```

La dernière compilation permet de mettre à jour les références croisées, la bibliographie et les signets PDF.

Pour utiliser `biblatex`, remplacer `\usenatbibtrue` par `\usenatbibfalse` dans `abstract.tex`. Pour utiliser Biber, conserver `\usenatbibfalse`, remplacer `backend=bibtex` par `backend=biber`, puis exécuter :

```sh
xelatex abstract.tex
biber abstract
xelatex abstract.tex
xelatex abstract.tex
```

Les commandes équivalentes avec `latexmk` sont :

```sh
latexmk -xelatex abstract.tex
latexmk -xelatex -use-biber abstract.tex  # après passage à backend=biber
```

#### Compilation avec pdfLaTeX

Le template peut également être compilé avec pdfLaTeX. La condition `\ifPDFTeX` active automatiquement `inputenc` pour ce moteur :

```sh
pdflatex abstract.tex
bibtex abstract
pdflatex abstract.tex
pdflatex abstract.tex
```

Avec le mode `biblatex` et Biber, utiliser `pdflatex` à la place de `xelatex` dans la procédure correspondante. XeLaTeX reste toutefois le moteur recommandé pour ce modèle.

Après un changement entre `natbib` et `biblatex`, supprimer les fichiers auxiliaires (`abstract.aux`, `abstract.bbl`, `abstract.bcf`, `abstract.blg`, `abstract.run.xml`, etc.) avant de recompiler.

### Personnalisation

1. Ouvrir `abstract.tex`.
2. Remplacer le titre, les noms, les affiliations et les informations de l'équipe.
3. Rédiger les sections demandées en conservant la structure attendue.
4. Remplacer `example-image` par le nom d'une figure du projet, si nécessaire.
5. Ajouter les figures dans `figs/`.
6. Remplacer les entrées d'exemple de `references.bib` par les références du projet.
7. Adapter les citations dans le texte et, en mode `biblatex`, la liste explicite des clés bibliographiques avant `\printbibliography`.
8. Compiler le document et vérifier les références, les liens et la mise en page.

Les illustrations complémentaires sont placées dans l'appendice. Le bloc `subfigure` permet de présenter deux images côte à côte ; chaque image possède sa propre légende et son propre label, par exemple `\ref{fig:annexe-a}` et `\ref{fig:annexe-b}`.

La commande `\cite{...}` réunit explicitement les références affichées dans la bibliographie. En mode `biblatex`, elle est placée avant `\printbibliography`; en mode `natbib`, la liste est produite par `\bibliography{references}`. Les clés utilisées doivent correspondre aux entrées présentes dans `references.bib`.

### Références bibliographiques

Les références sont gérées avec `biblatex` ou `natbib`. Le mode `natbib` est actuellement activé :

```latex
\newif\ifusenatbib
\usenatbibtrue
```

Pour revenir à `biblatex` avec BibTeX :

```latex
\usenatbibfalse
\usepackage[backend=bibtex, style=numeric, sorting=nyt, maxbibnames=3]{biblatex}
\addbibresource{references.bib}
```

Biber peut être choisi comme alternative au mode `natbib` en désactivant `natbib` et en sélectionnant le backend Biber :

```latex
\usepackage[backend=biber, style=numeric, sorting=nyt]{biblatex}
```

En mode `natbib`, le modèle utilise `plainnat` et `\bibliography{references}`. En mode `biblatex`, il utilise `\printbibliography`.

Les types d'entrées fournis à titre d'exemple comprennent les articles, livres, chapitres d'ouvrage, communications, thèses, mémoires, rapports, pages web, logiciels, jeux de données, normes et preprints.

### Arborescence

```text
.
├── abstract.tex       # Document LaTeX principal
├── references.bib     # Bibliographie BibTeX/BibLaTeX
├── figs/              # Figures et logo
├── .gitignore         # Fichiers LaTeX générés ignorés par Git
└── README.md          # Cette documentation
```

Les fichiers auxiliaires et les sorties de compilation (`.aux`, `.bbl`, `.bcf`, `.log`, `.pdf`, `.xdv`, etc.) sont exclus par `.gitignore`.

### Dépannage

- **BibTeX ou Biber ne trouve pas les références** : vérifier que le backend configuré correspond à la commande utilisée, puis compiler depuis le répertoire contenant `abstract.tex`.
- **Une référence n'apparaît pas** : vérifier que sa clé est présente dans `references.bib` et dans la commande `\cite{...}`.
- **Une figure est introuvable** : vérifier son nom et placer le fichier dans `figs/`.
- **La police Raleway est introuvable** : installer Raleway ou utiliser une distribution LaTeX complète.
- **L'en-tête est trop haut** : ajuster `\headheight` dans `abstract.tex` si le moteur signale un avertissement de `fancyhdr`.

---

## English

This LaTeX template is ready to compile with XeLaTeX, BibTeX, and `natbib`. It can also be configured for pdfLaTeX or `biblatex`/Biber.

### Quick Start

```sh
xelatex abstract.tex
bibtex abstract
xelatex abstract.tex
xelatex abstract.tex
```

Customize `abstract.tex`. Store references in `references.bib` and figures in `figs/`.

### Overview

This repository contains a LaTeX template for writing a research project abstract for the Cnam IAE2 USAE2L-4 research initiation course.

The document is designed for a **maximum of three pages of main content**, with an optional one-page bibliography and one-page appendix for illustrations. It provides a shared structure for the interim and final submissions.

### Template contents

The `abstract.tex` file includes the following sections:

- introduction, context, and research problem;
- objectives;
- methodology;
- mathematical, physical, and/or algorithmic models;
- expected or obtained results;
- conclusion and perspectives;
- references.

An `Instructions` section also summarizes the expected content for the interim and final submissions.

### Requirements

Install a complete LaTeX distribution including:

- XeLaTeX, recommended for font handling;
- BibTeX (used by default), Biber, or natbib;
- the LaTeX packages used by the document, including `biblatex`, `natbib`, `authblk`, `caption`, `subcaption`, `fancyhdr`, `graphicx`, `raleway`, and `titlesec`;
- the Raleway font if it is not provided by the LaTeX distribution.

On macOS, MacTeX is recommended. A complete TeX Live installation is also suitable.

### Compilation

From the project directory, the currently enabled natbib configuration is compiled with BibTeX:

```sh
xelatex abstract.tex
bibtex abstract
xelatex abstract.tex
xelatex abstract.tex
```

The final compilation updates cross-references, the bibliography, and PDF bookmarks.

To use `biblatex`, replace `\usenatbibtrue` with `\usenatbibfalse` in `abstract.tex`. To use Biber, keep `\usenatbibfalse`, replace `backend=bibtex` with `backend=biber`, then run:

```sh
xelatex abstract.tex
biber abstract
xelatex abstract.tex
xelatex abstract.tex
```

If `latexmk` is installed, the equivalent commands are:

```sh
latexmk -xelatex abstract.tex
latexmk -xelatex -use-biber abstract.tex  # after switching to backend=biber
```

#### Compilation with pdfLaTeX

The template can also be compiled with pdfLaTeX. The `\ifPDFTeX` condition automatically enables `inputenc` for this engine:

```sh
pdflatex abstract.tex
bibtex abstract
pdflatex abstract.tex
pdflatex abstract.tex
```

With `biblatex` and Biber enabled, replace `xelatex` with `pdflatex` in the corresponding workflow.

XeLaTeX remains the recommended engine for this template.

After switching between `natbib` and `biblatex`, remove auxiliary files (`abstract.aux`, `abstract.bbl`, `abstract.bcf`, `abstract.blg`, `abstract.run.xml`, and similar files) before recompiling.

### Customization

1. Open `abstract.tex`.
2. Replace the title, author names, affiliations, and team information.
3. Write the requested sections while keeping the expected structure.
4. Replace `example-image` with a project figure name when needed.
5. Add figures to `figs/`.
6. Replace the sample entries in `references.bib` with the project references.
7. Update the citations in the text and, in `biblatex` mode, the explicit list of bibliography keys before `\printbibliography`.
8. Compile the document and check the references, links, and layout.

Additional illustrations belong in the appendix. The `subfigure` blocks place two images side by side; each image has its own caption and label, for example `\ref{fig:annexe-a}` and `\ref{fig:annexe-b}`.

The `\cite{...}` command explicitly selects the references displayed in the bibliography. In `biblatex` mode it is placed before `\printbibliography`; in `natbib` mode the list is produced by `\bibliography{references}`. Its keys must match entries in `references.bib`.

### Bibliography

References are managed with `biblatex` or `natbib`. The `natbib` mode is currently enabled:

```latex
\newif\ifusenatbib
\usenatbibtrue
```

To switch back to `biblatex` with BibTeX:

```latex
\usenatbibfalse
\usepackage[backend=bibtex, style=numeric, sorting=nyt, maxbibnames=3]{biblatex}
\addbibresource{references.bib}
```

Biber can be selected as an alternative to `natbib` by disabling `natbib` and selecting the Biber backend:

```latex
\usepackage[backend=biber, style=numeric, sorting=nyt]{biblatex}
```

In `natbib` mode, the template uses `plainnat` and `\bibliography{references}`. In `biblatex` mode, it uses `\printbibliography`.

The sample bibliography includes entries for articles, books, book chapters, conference papers, theses, master's dissertations, reports, web pages, software, datasets, standards, and preprints.

### Project structure

```text
.
├── abstract.tex       # Main LaTeX document
├── references.bib     # BibTeX/BibLaTeX bibliography
├── figs/              # Figures and logo
├── .gitignore         # Ignored LaTeX-generated files
└── README.md          # This documentation
```

Auxiliary files and compilation outputs (`.aux`, `.bbl`, `.bcf`, `.log`, `.pdf`, `.xdv`, and others) are excluded by `.gitignore`.

### Troubleshooting

- **BibTeX or Biber cannot find the references**: check that the configured backend matches the command being used, then compile from the directory containing `abstract.tex`.
- **A reference does not appear**: check that its key exists in `references.bib` and in the `\cite{...}` command.
- **A figure cannot be found**: check its filename and place the file in `figs/`.
- **Raleway cannot be found**: install Raleway or use a complete LaTeX distribution.
- **The header is too tall**: adjust `\headheight` in `abstract.tex` if `fancyhdr` reports a warning.

## License and reuse

No license is currently specified for this template. Add the appropriate license information before distributing it outside the course or organization.
