# Fonctions de lissage par transitions sigmoïdes (smooth)

Ce dépôt contient des fonctions Python pour créer des fonctions continues et lisses par interpolation entre plusieurs fonctions définies sur différents intervalles, grâce à des transitions sigmoïdales douces.

---

## Fonctions principales

### `smooth(fonctions, bornes, precision=10)`

* **But** : Combiner plusieurs fonctions 1D en une fonction unique lisse avec des transitions sigmoïdales entre intervalles.
* **Paramètres** :

  * `fonctions` : liste de fonctions `f_i(x)`.
  * `bornes` : liste des points de transition sur l’axe x (longueur = len(fonctions) - 1).
  * `precision` : contrôle la raideur des transitions (par défaut 10, plus grand = transition plus rapide).
* **Usage** :

```python
f_lisse = smooth([f1, f2, f3], [-1, 1])
y = f_lisse(x)
```

Renvoie une fonction `f_lisse(x)` lisse, qui interpole les fonctions données en changeant progressivement autour des bornes.

---

### `smooth2D(precision, fonctions, bornes, axe="x")`

* **But** : Créer une fonction 2D lissée selon un axe donné (x ou y) à partir d’une liste de fonctions `f_i(x, y)` avec transitions sigmoïdales.
* **Paramètres** :

  * `precision` : raideur des sigmoïdes.
  * `fonctions` : liste de fonctions 2D `f_i(x, y)`.
  * `bornes` : bornes de transition sur l’axe spécifié (len = len(fonctions) - 1).
  * `axe` : `'x'` ou `'y'`, axe selon lequel effectuer la transition.
* **Usage** :

```python
f_2d = smooth2D(10, [f1_2d, f2_2d, f3_2d], [-1, 1], axe="x")
z = f_2d(X, Y)
```

Renvoie une fonction lisse 2D `f_2d(x, y)` avec transitions progressives selon l’axe choisi.

---

### `smooth2Dxy(precision, fonctions_x, bornes_x, fonctions_y, bornes_y)`

* **But** : Générer une fonction 2D lissée avec transitions croisées à la fois selon x ET y, à partir de deux listes indépendantes de fonctions.
* **Paramètres** :

  * `precision` : raideur des sigmoïdes.
  * `fonctions_x` : liste de fonctions `f_i(x, y)` pour transitions selon x.
  * `bornes_x` : bornes de transition sur x.
  * `fonctions_y` : liste de fonctions `g_i(x, y)` pour transitions selon y.
  * `bornes_y` : bornes de transition sur y.
* **Usage** :

```python
f_2dxy = smooth2Dxy(10, fonctions_x, bornes_x, fonctions_y, bornes_y)
z = f_2dxy(X, Y)
```

Retourne une fonction lissée 2D où les transitions sigmoïdales se font indépendamment selon x et y.

---

## Notes

* Toutes les fonctions retournent une fonction Python qui peut être évaluée sur des scalaires ou des tableaux NumPy.
* Les transitions sigmoïdales assurent une continuité et une dérivabilité arbitrairement bonne suivant le paramètre `precision`.
* Ces fonctions sont utiles pour créer des transitions douces entre plusieurs modèles ou comportements définis par morceaux.

---

## Exemple rapide

```python
import numpy as np
import matplotlib.pyplot as plt

# Exemple de fonctions 1D
f1 = lambda x: np.sin(x)
f2 = lambda x: np.cos(x)
f = smooth([f1, f2], [0], precision=20)

x = np.linspace(-2, 2, 100)
plt.plot(x, f(x))
plt.show()
```

Voir ce [notebook](Smoothing.ipynb) sinon, pour des exemples plus détaillés.

---
