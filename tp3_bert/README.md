# TP BERT

Les exercices de ce TP, les instructions et le code sont entièrement contenus dans le Notebook `tp_bert.ipynb`, que vous allez trouver dans ce répertoire. Il y a deux méthodes pour l'ouvrir et l’exécuter, dont la première est vivement conseillée parce que ca vous évite d'installer du software sur votre machine locale. En outre, l’exécution du code sera plus rapide.

## Méthode 1: Google Colab

- Inscrivez-vous à Google Colab (si vous n'avez pas déjà de compte Google) et demandez l’accès.
- Sinon, vous pouvez ouvrir un nouveau fichier Colab depuis [votre compte Google Drive](https://drive.google.com/drive/my-drive) en cliquant sur `+ New->More->Google Colaboratory`
- Une fois que vous avez obtenu l'accès à un fichier Colab, vous pouvez télécharger un Notebook en utilisant `fichier->Upload Notebook`. Téléchargez le fichier `tp_bert.ipynb`.
- Pour activer l’utilisation de GPU pour votre notebook: `Runtime->Change runtime type->Hardware Accelerator->GPU` .

## Méthode 2: conda environment

Installez [Miniconda3](https://docs.conda.io/en/latest/miniconda.html) (Anaconda3 marche aussi), ensuite, placez-vous dans le répertoire de ce TP (avec `cd home/username/mypath`) et exécutez les commandes suivantes dans l'ordre:

**Note**: `pip install transformers[torch]` installe la version CPU de Pytorch. Si vous avez une GPU sur votre machine, installez d'abord PyTorch pour GPU en suivant les instructions [ici](https://pytorch.org/get-started/locally/#start-locally).

````
conda create --name bertenv python
conda activate bertenv
pip install transformers[torch]
conda install -c conda-forge notebook
conda install scikit-learn
conda install -c conda-forge ipywidgets
pip install tensorboardX
````

Maintenant, vous pouvez ouvrir `tp_bert.ipynb`, il suffit de lancer la commande `jupyter notebook` dans le répertoire de travail.
