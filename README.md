# Mini_Projet
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/samar-guicha/Mini_Projet/main?filepath=notebook.ipynb)
## Introduction
<p>
Dans ce projet on va utiliser diverses techniques de manipulation des données pour explorer différents aspects de l’histoire de Lego.

La base de données comprend des données sur chaque ensemble LEGO qui a déjà été vendu; les noms des ensembles, quelles briques ils contiennent, quelle couleur les briques sont, etc.</p>

<p><img src="img/lego-bricks.jpeg" alt="lego"></p>


## A propos de dataset
Schéma de la base de données Lego <br><br>
![schema](https://rebrickable.com/static/img/diagrams/downloads_schema_v3.png)

<br><br>



| Dataset | Description | colonnes |
|--|--|--|
| `colors.csv` | Ce fichier contient des informations sur les couleurs LEGO, y compris un identifiant unique pour chaque couleur, son nom, et la valeur RVB approximative, et si elle est transparente | `id` Identifiant unique pour cette couleur. <br><br>`name` Le nom de la couleur. <br><br> `rgb` La couleur RVB approximative. <br><br> `is_trans` Que la couleur donnée soit transparente/translucide ou non.|
| `inventories.csv` | Ce tableau contient des informations sur les inventaires, y compris un identifiant unique, sa version et le numéro d’ensemble. | `id` Identifiant unique pour cette saisie d’inventaire.<br><br> `version` numéro de version. <br><br> `set_num` Set number (de `sets.csv`). |
| `inventory_parts.csv` | Ce tableau contient les inventaires des pièces d’information, y compris un numéro d’identification unique, le numéro de pièce, la couleur de la pièce, combien sont inclus et s’il s’agit d’une pièce de rechange. | `inventory_id` ID unique pour l’inventaire dans lequel cette partie apparaît. C’est le même que la valeur id dans `inventories.csv`. <br><br> `part_num` Identifiant unique pour la pièce. <br><br> `color_id` ID unique pour la couleur, selon `colors.csv`. <br><br> `quantity` Le nombre d’exemplaires de cette partie inclus dans le set ! <br><br> `is_spare` WQue ce soit ou non une pièce de rechange. Les pièces de rechange sont des pièces supplémentaires non nécessaires pour terminer l’ensemble. |
| `inventory_sets.csv` | Ce fichier contient des renseignements sur les stocks inclus dans les ensembles, y compris le numéro d’inventaire, le numéro d’ensemble et la quantité de ces stocks qui sont inclus. | `inventory_id` Numéro d’inventaire unique de `inventories.csv`. <br><br> `set_num` Unique set ID from `sets.csv`. <br><br> `quantity` La quantité des stocks inclus. |
| `part_categories.csv` | Cet ensemble de données comprend des informations sur la catégorie de pièce (quel type de pièce il s’agit) et un identifiant unique pour cette catégorie de pièce. | `id` Identifiant unique pour la catégorie de pièce. <br><br> `name` La catégorie de la partie. |
| `part_relationships.csv` | Cet ensemble de données comprend des informations sur les différentes relations entre les parties. | `rel_type` Type de relation de la pièce. <br><br> `child_part_num` Pièce d’identité de catégorie enfant. <br><br> `parent_part_num` Code d’identification unique de la catégorie mère  |
| `parts.csv` | Cet ensemble de données comprend des informations sur les pièces Lego, y compris un numéro d’identification unique, le nom de la pièce, et de quelle catégorie de pièce elle provient. | `part_num` Identifiant unique pour la pièce. <br><br> `name` nom de la pièce. <br><br> `part_cat_id` Identifiant unique de la catégorie de pièce (de `part_categories.csv`). |
| `sets.csv` | Ce fichier contient des informations sur les jeux LEGO, y compris un numéro d’identification unique, le nom de l’ensemble, l’année de sa sortie, son thème et le nombre de parties qu’il comprend. | `set_num` Unique set ID. <br><br> `name` Le nom de l’ensemble. <br><br> `year` Année de publication de l’ensemble. <br><br> `theme_id` ID unique pour le thème utilisé pour l’ensemble(de`themes.csv`). <br><br> `num_parts` Le nombre de pièces incluses dans l’ensemble. |
| `themes.csv` | Ce fichier contient des informations sur les thèmes lego. Chaque thème reçoit un numéro d’identification unique, un nom, et (s’il fait partie d’un thème plus grand) de quel thème il fait partie. | `id` Thème unique ID. <br><br> `name` nom du thème. <br><br> `parent_id` ID unique pour le thème plus large, s’il y en a un. |


<br>
## Colors dataset
```python
colors = pd.read_csv('datasets/colors.csv')
display(colors.head())
```

|   | id |      name      |   rgb  | is_trans | 
|:-:|:--:|:--------------:|:------:|:--------:|
| 0 | -1 | Unknown        | 0033B2 | f        |
| 1 | 0  | Black          | 05131D | f        |
| 2 | 1  | Blue           | 0055BF | f        |
| 3 | 2  | Green          | 237841 | f        |
| 4 | 3  | Dark Turquoise | 008F9B | f        |

<br>
<p>Il serait intéressant d’explorer la distribution des couleurs transparentes par rapport aux couleurs non transparentes.</p>

<p><img src='img/1.png' alt="image1"></p>

<hr>
## Sets dataset
<br>

```python
sets = pd.read_csv('datasets/sets.csv')
display(sets.head())
```

|   | set_num |            name            | year | theme_id | num_parts |
|:-:|:-------:|:--------------------------:|:----:|:--------:|:---------:|
| 0 |   00-1  |       Weetabix Castle      | 1970 |    414   |    471    |
| 1 |  0011-2 |      Town Mini-Figures     | 1978 |    84    |     12    |
| 2 |  0011-3 | Castle 2 for 1 Bonus Offer | 1987 |    199   |     2     |
| 3 |  0012-1 |     Space Mini-Figures     | 1979 |    143   |     12    |
| 4 |  0013-1 |     Space Mini-Figures     | 1979 |    143   |     12    | 

<p>Voyons comment le nombre d’ensembles a changé au fil des ans</p>

<p><img src='img/2.png' alt="image2"></p>


<br>

<p>Observons également l’évolution des thèmes au fil des ans</p>

<p><img src='../img/3.png' alt="image3"></p>