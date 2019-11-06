# PIP3 AND VENV CHEATSHEET

## Best Practice

Structure like this:

myprojectfolder
|-venv
|-src
|-test

*dont forget to put venv in your .gitignore (prob just throw it in your global gitignore*

## PIP3

### What installed

`pip3 list` or `pip3 freeze` to just see your installs

## VENV

### Create new venv

`python3 -m venv <directory>`

### Activate / Deactivate

`source <director>/bin/activate` --> enter venv

`deactivate`

### Create requirements.txt

pip freeze > requirements.txt


