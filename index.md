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

Note: avant de savoir 

---

<!-- .slide: class="title" -->

## Imaginez... un monde sans code style

```
var lol, HAHAHA_I_M_CONSTANT =function(     
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

---

<!-- .slide: class="title bg-python" -->

# Une chance de coder sous Python

---

## Tableau récapitulatif des *coding standards*

| Langage |	Statut| 	Nom |	Commentaires|
|---------|--------|-------|------------|
| PHP|Officiel |PHP-FIG / PSR |Récent, d'autres standards sont apparus avant|
|Javascript|	Communautaire	|ESLint	|C'est le bordel, mais eslint est le plus utilisé|
|Typescript|	Communautaire|		Google a pondu gts||
|Ruby|	Communautaire		|||
|Java|	HAhahaha	|	||
|Go|	Officiel|	gofmt|	Voir Effective Go|
|Rust|	Officiel|	rustfmt|	|
|Kotlin|	Officiel		|||
|C#	|Officiel		|||
|Python|	Officiel|	PEP8	||

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

Les **outils de base** pour vérifier tout ça :

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

---

<!-- .slide: class="title" data-background="#b5b42c url(theme-reveal/images/bg-lenin.jpg) no-repeat -60% bottom" -->

# Aller plus loin

Note: Les petites interrogations restantes que tout le monde se pose

---

## Nombre de caractères d'une ligne (en vrai)

Certains sont nazis avec 70 caractères, d'autres plus laxes 88 caractères car on est plus sur écran DOS.

Sur les docstring, c'est parfois 72, parfois plus...

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

## Formattage de chaînes

```python
"Bonjour %s, bienvenue chez %s" % ("la vie", "les bisounours")
```
```python
"Bonjour {}, bienvenue chez {}".format('Jean', 'nous')
```
```python
"Bonjour {0}, bienvenue chez {1}".format('Kévin', 'McDonald')
```
---

## Complexité cyclomatique

```python
for i in ma_liste:
    if i < 10:
        try:
            while true:
                answer = ask("why ???")
                if answer = "idontknow"
                    raise DontKnowEception
            except DontKnowEceptiona as e:
                for i in range(3):
                    print("ha")
```

## Maintenabilité

## Nombre de ligne de code par module

---

Encore des outils :

* **radon**/**xenon** : métriques de code
* **isort** : gère l'ordre, le regroupement et le style des imports de manière fine
* **McCabe** : analyse de complexité
* **pylama** : cominaison de `pycodestyle`, `pydocstyle`, `pyflakes`, `mccabe`, `pylint`, `radon`, `gjslint`
* **flake8** : combinaison de `PyFlakes`, `pycodestyle` et `mccabe`
* **black** : formatteur nazi

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

---

<!-- .slide: class="title bg-rocks"-->

# A quel moment vérifier ?

---

## Pendant l'écriture

Configurer son IDE : 
    
* Pycharm autoformatte où peut lancer un formatteur avec un raccourci

    * <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>L</kbd> sous Linux/Windows
    * <kbd>Cmd</kbd>+<kbd>Opt</kbd>+<kbd>L</kbd> sous Max OS

* Lancer le linter régulièrement en ligne de commande

---

## Avant de commiter

* Git pre-commit hook maison
* pre-commit.yml partagé

https://github.com/pre-commit/pre-commit-hooks
example https://github.com/django-extensions/django-extensions/blob/master/.pre-commit-config.yaml 

---

## Avec une Continuous Integration

* Travis
* GitlabCI

---

<!-- .slide: class="title alternate" -->

# Des questions ?

https://makinacorpus.github.io/maintenir-code-lisible/

