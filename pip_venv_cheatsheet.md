# PIP3 AND VENV CHEATSHEET

## Best Practice

Structure like this

```
myprojectfolder
|-.venv
|-src
|-test
```

*Note: Dont forget to put .venv in your .gitignore (prob just throw it in your global gitignore)*

## PIP3

### What installed

`pip3 list` or `pip3 freeze` to just see your installs

## VENV

```bash
# create venv called .env
python3 -m venv .env

# activate the environment
source .env/bin/activate

# deactivate the environment
deactivate
```

### Keeping Track of Requirements

```bash
# save imports to requirements.txt
pip freeze > requirements.txt

# install what is in requirements.txt
pip install -r requirements.txt
```


