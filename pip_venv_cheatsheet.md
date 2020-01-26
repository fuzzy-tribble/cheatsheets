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

### Create new venv called .env

```
python3 -m venv .env
```

### Activate / Deactivate

`source .env/bin/activate`

`deactivate`

### Create requirements.txt

```bash
# save imports to requirements
pip freeze > requirements.txt

# install what is in requirements.txt
pip install -r requirements.txt
```


