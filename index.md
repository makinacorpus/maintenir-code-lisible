---
title: Maintenir un code lisible
theme: theme-reveal/makina.css
verticalSeparator: <!--v-->
revealOptions:
    transition: 'slide'
---

<!-- .slide: class="title logo" data-background="#b5b42c" -->

# Maintenir un code lisible

### Sébastien Corbin

---

<!-- .slide: class="programme bg-lion-left" -->

# Préparez-vous

Attention, danger, risque de :

- hémorragie rétinienne 
- hystérie soudaine
- malaise vagal
- nausée

Les premiers rangs risquent d'être arrosés par les derniers

Note:

Avant de savoir qu'est ce qu'un code lisible il faut se rappeler ce qu'est un code illisible

---

<!-- .slide: class="title" -->

## Imaginez... un monde sans code style

```
var lol, HAhaHA_I_M_notCONSisTANT =function(     
){return lol;;;;;;;;;;;
                            ;;;;;}; lol=
"Coucou"; alert(HAHAHA_I_M_CONSTANT(
)[ '0' ])
```


```
function zoubida(lavabo)


{
	if(confirm           (lavabo)) for (;;) return true; else {
	  return false
}}
```

Note:
Bon alors là j'ai pris un language bizarre qui permet de faire du caca

---

Connaissez-vous l'indentation inversée ?

```
    for(int i = 0; i < 10; i++)
        {
myFunc();
        }
    if(something)
        {
// do A
        }
    else
        {
// do B
    }
```

Oui oui, ça existe 
https://stackoverflow.com/q/218123
https://softwareengineering.stackexchange.com/q/1338

---

## Et avec python ?

* Syntaxe claire
* Pas d'accolades
* Indentation obligatoire
* Moins de parenthèses
* Pas de bloc anonymes
* Peu de mots-clés

Mais python peut aussi faire de mauvaises syntaxes

```
if ((((bar == None)))): bar = 2
```
```
bar = 3; print(bar)
```

**Défi :** créez/trouvez un obduscateur en Python !

Note:
Les parenthèses peuvent être illimitées, les points virgules acceptés,
mais beaucoup de concepts sont fermés (exemple des lambda)

---

<!-- .slide: class="title bg-python" -->

# Une chance de coder sous Python

---

## Tableau récapitulatif des *coding standards*

| Langage |	Statut| 	Nom |	Commentaires|
|---------|--------|-------|------------|
| PHP|[Officiel](https://www.php-fig.org/psr/psr-2/) |PHP-FIG / PSR |Récent, d'autres standards sont apparus avant|
|Javascript|	Communautaire	|[ESLint](https://eslint.org/docs/developer-guide/code-conventions)	|C'est le bordel, mais eslint est le plus utilisé|
|Typescript|	Communautaire|		Google a pondu [gts](https://github.com/google/ts-style)||
|Ruby|	Communautaire		|||
|Java|	[Officiel](https://www.oracle.com/technetwork/java/codeconvtoc-136057.html)	| ||
|Go|	Officiel|	gofmt|	Voir Effective Go|
|Rust|	Officiel|	rustfmt|	|
|C#	|[Officiel]()		|||
|Python|	Officiel|	[PEP8](https://www.python.org/dev/peps/pep-0008/)	||

---

## Introduction à la PEP8

- indentation de 4 espaces
- ligne de 79 caractères
- imports sur plusieurs lignes
- utf-8 par défaut
- snake_case pour variables et fonctions/méthodes
- CamelCase pour classes

Ensuite chaque framework/bibliothèque/projet a son propre coding standard.

---

<!-- .slide: class="title" data-background="#b5b42c" -->

# Un outil de prédilection :
# le *linter*

Note:

* Logical Lint
    * Code errors
    * Code with potentially unintended results
    * Dangerous code patterns
* Stylistic Lint
    * Code not conforming to defined conventions

---

Les **outils de base** pour vérifier la compatibilité PEP8 :

* **pylint** : vérificateur d'erreurs de syntaxe
* **pyflakes** : vérificateur d'erreurs de syntaxe
* **autoflake** : formatteur automatique basé sur `pyflakes`
* **pycodestyle** : vérificateur de style (anciennement pep8)
* **autopep8** : formatteur automatique basé sur `pycodestyle`
* **yapf** : formatteur automatique
* **mypy** : vérificateur de typage statique
* **pychecker** : † projet mort †
* **pep8ify** : † projet mort †
* **pyntch** : † projet mort †

http://meta.pycqa.org

Note:

On pourrait penser que tous ces linters se tirent la bourre
mais ils sont regroupés sous un même groupe de travail
nommé PyCQA (pour Python Code Quality Authority)

---

<!-- .slide: class="title" data-background="#b5b42c url(theme-reveal/images/bg-lenin.jpg) no-repeat -60% bottom" -->

# Aller plus loin

Note: 

Malgré une PEP8 relativement complète, elle reste laxe sur certains point
il reste donc des petites interrogations que tout le monde se pose

---

## Nombre de caractères d'une ligne (en vrai)

Certains sont nazis avec 70 caractères, d'autres plus laxes 88 caractères car on est plus sur écran DOS.

Sur les docstring, c'est parfois 72, parfois plus...

Note:

Limite héritée des écrans touts petits, toujours en vigeur 
car il est plus facile de scanner un code sur une courte colonne 
qu’en faisant des aller-retours constant

Imaginez un journal ecrit sans colonnes

---

## Wrapping (retour à la ligne)

Des arguments/paramètres

```python
my_super_long_method_name(super_long_argument1, super_long_argument2, super_long_argument3)
```
```python
my_super_long_method_name(super_long_argument1, super_long_argument2, 
                          super_long_argument3)
```
```python
my_super_long_method_name(
    super_long_argument1, super_long_argument2, super_long_argument3
)
```
```python
my_super_long_method_name(
    super_long_argument1, 
    super_long_argument2, 
    super_long_argument3
)
```

Note:

Plusieurs écoles, choisissez la votre, mais avec la dernière vous pouvez 
vous retrouvez avec des fichiers énormes en terme de lignes

---

D'une callchain

```python
result = MyLongClassName.my_long_method_name(arg1).my_chained_call(arg4, arg5).my_chained_call2()
```

```python
result = MyLongClassName.my_long_method_name(arg1)\
                        .my_chained_call1(arg4, arg5)\
                        .my_chained_call2()
```

```python
result = MyLongClassName.my_long_method_name(
    arg1
).my_chained_call1(
    arg4, arg5
).my_chained_call2()
```

```python
result = (
    MyLongClassName.my_long_method_name(arg1)
    .my_chained_call1(arg4, arg5)
    .my_chained_call2()
)
```

Note:
Surtout, restez consistents

---

Des imports

```python
from mon_package import ma_methode_1, ma_methode_2, ma_methode_3, ma_methode_4, ma_methode_5
```

```python
from mon_package import ma_methode_1, ma_methode_2, ma_methode_3, ma_methode_4,\
                        ma_methode_5
```
```python
from mon_package import (ma_methode_1, ma_methode_2, ma_methode_3, ma_methode_4,
                         ma_methode_5)
```
```python
from mon_package import (
    ma_methode_1, ma_methode_2, ma_methode_3, ma_methode_4, ma_methode_5
)
```
```python
from mon_package import (
    ma_methode_1, 
    ma_methode_2, 
    ma_methode_3, 
    ma_methode_4, 
    ma_methode_5,
)
```
et ça continue avec les listes, les dictionnaires, etc...

---

## Virgules en fin de ligne

```python
def ma_methode_au_nom_super_long(
    argument1, argument2=None, argument3=None, argument4=None, argument5=None,
    argument6=None, argument7=None, argument8=None, arg9=None, *args, **kwargs
):
```
Doit-on la retirer pour éviter de dépasser les 79 caractères ?


## Apostrophes

Double ou simple quote ? Forcé ou non ?


## Formatage de chaînes

```python
"Bonjour %s, bienvenue chez %s" % ("la vie", "les bisounours")
```
```python
"Bonjour {}, bienvenue chez {}".format('Jean', 'nous')
```
```python
"Bonjour {0}, bienvenue chez {1}".format('Kévin', 'McDonald')
```

Note:
bon là en l'occurence il n'est censé rien y avoir puisque c'est `kwargs`

Pour le formatage, certains n'accepte plus l'ancienne notation et d'autre force le nommage des placeholders

---

## Complexité cyclomatique

```python
for i in ma_liste:
    if i < 10:
        try:
            while True:
                answer = ask("why ???")
                if answer == "idontknow":
                    raise DontKnowException
        except DontKnowException as e:
            for i in range(3):
                print("ha")
```

## Maintenabilité

Indice allant de 0 à 100 avec :

* 85+ : maintenabilité bonne
* 65-85 : maintenabilité moyenne
* < 65 : maintenabilité difficile

## Nombre de ligne de code par module

Note:
vérifier que tout connait le principe de complexité cyclomatique
Ce sont des métrique poussées et parfois peu représentatrices

---

Encore des outils :

* **radon**/**xenon** : métriques de Halstead
* **isort** : gère l'ordre, le regroupement et le style des imports de manière fine
* **McCabe** : analyse de complexité
* **pylama** : combinaison de `pycodestyle`, `pydocstyle`, `pyflakes`, `mccabe`, `pylint`, `radon`, `gjslint`
* **flake8** : combinaison de `PyFlakes`, `pycodestyle` et `mccabe`
* **black** : formatteur nazi

Note:
S'arrêter sur isort
Préciser que pylama et flake8 se repose sur les épaule de géants
Pylama un peu plus complexe à configurer
Black est récent, très rapide, peu d'options donc on le lance et on oublie, 
très utile dans les grosses équipe car peu de config possible

---

## Tox

Sert à automatiser les tests, pratique car son fichier de config `tox.ini` est lu par *flake8* et *isort* notamment

```ini
[tox]
skipsdist = true
envlist =
    flake8
    isort

[testenv]
deps = -rdev-requirements.txt

[testenv:flake8]
deps = flake8
commands = flake8 .

[testenv:isort]
deps =
  -rdev-requirements.txt
  isort>=4.2.13
commands = isort --check-only -e

[flake8]
max-complexity = 8
exclude = .tox,__pycache__,*/migrations/*
ignore = F403,F405

[isort]
combine_as_imports = true
multi_line_output = 5
include_trailing_comma = true
skip = migrations,.tox
not_skip = __init__.py
known_django = django
known_first_party = accounts, common, messaging
sections = FUTURE,STDLIB,DJANGO,THIRDPARTY,FIRSTPARTY,LOCALFOLDER
```

---

## Et le bon vieux **grep** ?!?

```python
import pdb; pdb.set_trace()
import ipdb; ipdb.set_trace()
print("Je passe ici")
```
```javascript
console.log("toto");
alert("lol");
```

Qui c'est qu'à pas fini son merge ?!?

```
Si vous avez des questions :
<<<<<<< HEAD
c'est pas maintenant.
=======
c'est à la fin du talk.
>>>>>>> branch-a
```

Note:
Que celui ou celle qui n'a jamais oublié un pdb en prod crie kamoulox maintenant

---

<!-- .slide: class="title bg-rocks"-->

# A quel moment vérifier ?

---

## Pendant l'écriture

Configurer son IDE : 
    
* Pycharm autoformatte ou peut lancer un formatteur avec un raccourci

    * <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>L</kbd> sous Linux/Windows
    * <kbd>Cmd</kbd>+<kbd>Opt</kbd>+<kbd>L</kbd> sous Max OS

* Lancer le linter régulièrement en ligne de commande

---

## Avant de commiter

* Hook git de pre-commit maison

```bash
# à mettre dans votre-projet/.git/hooks/pre-commit et à rendre executable
#!/bin/bash

source ~/.virtualenvs/votre-projet/bin/activate

echo "Checking for syntax"
if ! flake8 || ! isort -e --check-only
then
    echo ""
    echo "Correct the errors above"
    exit 1
fi
```

Un exemple en python https://gist.github.com/streeter/1376856

---

## Avant de commiter

Fichier de configuration partagé avec [pre-commit](https://pre-commit.com/)

* `pip install pre-commit` ou `brew install pre-commit`

```yaml
# .pre-commit-config.yaml
-   repo: git://github.com/pre-commit/pre-commit-hooks
    sha: v0.9.1
    hooks:
    -   id: trailing-whitespace
    -   id: check-ast
    -   id: check-docstring-first
    -   id: check-merge-conflict
    -   id: debug-statements
    -   id: end-of-file-fixer
    -   id: flake8
-   repo: git://github.com/RobinRamael/pre-commit-isort.git
    hooks:
    -   id: isort
```

* `pre-commit install`

Possibilité d'ajouter ses propres hooks, tout ça, en python

---

## Avec une Continuous Integration

* Travis CI

```yaml
dist: trusty
language: python
python:
  - "3.6"
install:
  - pip install -r dev-requirements.txt
  - pip install flake8 isort
script:
  - flake8 .
  - isort -e --check-only
```

* GitlabCI

```yaml
image: python:3.6

before_script:
  - pip install -r dev-requirements.txt
tests:
  script:
    - flake8 .
    - isort -e --check-only
```

---

<!-- .slide: class="title alternate" -->

# Des questions ?

https://makinacorpus.github.io/maintenir-code-lisible/

