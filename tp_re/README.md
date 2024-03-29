# TP Relation Extraction

# Intro

Dans ce TP, nous allons travailler à l'implémentation d'un pipeline pour l'extraction de relations neuronales, qui se basera sur deux éléments fondamentaux:

1. un système de reconnaissance d'entités nommées (NER),
2. un modèle neuronal pour l'extraction de relations (NRE), basé sur BERT.

## NER, NRE, what ?

**NER - Named Entity Recognition**: localiser et classer les entités mentionnées dans un texte dans des catégories prédéfinies telles que des noms de personnes, des organisations, des lieux, des dates, etc :

![](ner.png)

**NRE - Neural Relation Extraction**: découvrir les relations sémantiques entre les entités d'un texte en utilisant des méthodes d'apprentissage profond :

![](nre.png)

# À Rendre

Chaque exercice de ce TP prévoit une réponse sous forme textuelle ou de code. Toute réponse doit être écrite dans `tp_re.ipynb`, dans une ou plusieurs cellules en dessous de l’énoncé de chaque exercice.

Vous rendrez un répertoire compressé `tp_re_nom1_nom2.zip` avec le contenu du répertoire `tp_re.zip` dont le fichier `tp_re.ipynb` aura été mis à jour avec vos réponses.

# Setup

Les exercices de ce TP, les instructions et le code sont entièrement contenus dans le Notebook `tp_re.ipynb`, que vous allez trouver dans ce répertoire. Il y a deux méthodes pour l'ouvrir et l’exécuter, dont la première est vivement conseillée parce que ca vous évite d'installer du software sur votre machine locale. En outre, l’exécution du code sera plus rapide.

## Méthode 1: Google Colab

- Inscrivez-vous à Google Colab (si vous n'avez pas déjà de compte Google) et demandez l’accès.
- Sinon, vous pouvez ouvrir un nouveau fichier Colab depuis [votre compte Google Drive](https://drive.google.com/drive/my-drive) en cliquant sur `+ New->More->Google Colaboratory`
- Une fois que vous avez obtenu l'accès à un fichier Colab, vous pouvez télécharger un Notebook en utilisant `fichier->Upload Notebook`. Téléchargez le fichier `tp_re.ipynb`.

## Méthode 2: conda environment

Installez [Miniconda3](https://docs.conda.io/en/latest/miniconda.html) (Anaconda3 marche aussi), ensuite, placez-vous dans le répertoire de ce TP (avec `cd home/username/mypath`) et exécutez les commandes suivantes dans l'ordre:

**Note**: `pip install transformers[torch]` installe la version CPU de Pytorch. Une CPU est toute à fait suffisante pour ce TP.

````
conda create --name bertenv python
conda activate bertenv
pip install transformers[torch]
conda install -c conda-forge notebook
````

Maintenant, vous pouvez ouvrir `tp_re.ipynb`, il suffit de lancer la commande `jupyter notebook` dans le répertoire de travail. Si vous avez besoin d'installer d'autres libraries dans votre environment avec `pip` ou `conda`, essayez de prioriser `conda` si possible.

