
# API OGE

## Progression du Développement de l'API

- [x] Obtenir les UE, pôles, matières, groupes de notes et notes à partir d'OGE
- [x] Sauvegarde des données dans un fichier et chargement des données depuis un fichier
- [ ] Gestion des semestres autres que le courant pour les notes
- [ ] Obtenir l'emploi du temps à partir d'OGE
- [ ] Gestion des dates différentes de celle actuelle pour l'emploi du temps

## Initialisation et Données

*Importer la librairie:*
```py
from oge import *
```

Afin de pouvoir naviguer dans les informations d'OGE, il est nécessaire de se connecter ain de récupérer les données ou de les charger depuis un fichier.
*Se connecter à OGE:*
```py
OGE.connect(username = 'XXXXXXXXXX', password = 'XXXXXXXXXX')
```

Comme expliqué précedemment, il est possible de charger les données depuis un fichier. Cependant, ce fichier est généré via une sauvegarde, qui est une méthode présente dans cette API.
*Charger les données depuis un fichier local:*
```py
OGE.loadData('chemin/vers/les/données')
```

*Sauvegarder les données dans un fichier local:*
```py
OGE.loadData('chemin/vers/les/données')
```



## Données Brutes et Racine
Lors de la connexion, l'API va générer des données brutes accessibles à tout moment et va également stocker ces données sous une forme plus structurée, permettant à l'utilisateur de naviguer plus facilement dans ces données.

*Obtenir les données brutes:*
```py
OGE.getRawData()
```

*Obtenir les données triée:*
```py
OGE.getData()
```
**Note:** En récupérant les données triées comme ci-dessus, l'élément récupéré sera une liste contenant chaque UE, qui elles-même contiennent le reste des informations les concernant.



## UE, Pôles, Matières, Notes

Chaque donnée possède trois attributs: un **nom**, un coefficient **coeff** et une liste d'objets possédant les attribus concernant la sous-catégorie de celle en cours.
Chaque donnée possède trois méthodes: une **moyenne** (calcul la moyenne en cours), une longueur **get<Catégorie>Count** et **find<Catégorie>ByNom** (<Catégorie> est évidemment remplacé par sa catégorie correspondante).

L'ordre des sous-attributs est le suivant:
Racine (**OGE**)
 ∟ UE (**UE(id)** ou **getData()\[index\]**)
    ∟ Pôles (**pole(id)** ou **poles\[index\]**)
       ∟ Matières (**matiere(id)** ou **matieres\[index\]**)
          ∟ Groupe de Notes (**note(id)** ou **notes\[index\]**)
             ∟ Note -> Possède trois attributs uniques: **note**, **max** et **coeff**



## Exemples


### 1ère UE

*Obtenir la 1ère UE:*
```py
OGE.UE(1)
```
ou
```py
OGE.getdata()[0]
```

*Obtenir la moyenne de la 1ère UE:*
```py
OGE.UE(1).moyenne()
```
ou
```py
OGE.UE(1).moyenne()
```

*Obtenir le nombre d'UE:*
```py
OGE.getUECount()
```



### 1er Pôle de la 1ère UE

*Obtenir le 1er pôle de la 1ère UE:*
```py
OGE.UE(1).pole(1)
```
ou
```py
OGE.UE(1).poles[0]
```

*Obtenir la moyenne du 1er pôle de la 1ère UE:*
```py
OGE.UE(1).pole(1).moyenne()
```
ou
```py
OGE.UE(1).poles[0].moyenne()
```

*Obtenir le nombre de pôles de la 1ère UE:*
```py
OGE.UE(1).getPoleCount()
```
ou
```py
OGE.getData()[0].getPoleCount()
```



### 1ère Matière du 1er Pôle de la 1ère UE

*Obtenir la 1ère matière du 1er pôle de la 1ère UE:*
```py
OGE.UE(1).pole(1).matiere(1)
```
ou
```py
OGE.UE(1).poles[0].matieres[0]
```

*Obtenir la moyenne de la 1ère matière du 1er pôle de la 1ère UE:*
```py
OGE.UE(1).pole(1).matiere(1).moyenne()
```
ou
```py
OGE.UE(1).poles[0].matieres[0].moyenne()
```

*Obtenir le nombre de matières du 1er pôle de la 1ère UE:*
```py
OGE.UE(1).pole(1).getMatiereCount()
```
ou
```py
OGE.UE(1).poles[0].getMatiereCount()
```



### 1er Groupe de Notes de la 1ère Matière du 1er Pôle de la 1ère UE

*Obtenir le 1er groupe de note de la 1ère matière du 1er pôle de la 1ère UE:*
```py
OGE.UE(1).pole(1).matiere(1).note(1)
```
ou
```py
OGE.UE(1).poles[0].matieres[0].notes[0]
```



*Obtenir la moyenne du 1er groupe de note de la 1ère matière du 1er pôle de la 1ère UE:*
```py
OGE.UE(1).pole(1).matiere(1).note(1).moyenne()
```
ou
```py
OGE.UE(1).poles[0].matieres[0].notes[0].moyenne()
```

*Obtenir le nombre de groupes de notes de la 1ère matière du 1er pôle de la 1ère UE:*
```py
OGE.UE(1).pole(1).matiere(1).getNoteCount()
```
ou
```py
OGE.UE(1).poles[0].matieres[0].getNoteCount()
```



### 1ère Note du 1er Groupe de Notes de la 1ère Matière du 1er Pôle de la 1ère UE

*Obtenir la 1ère note du 1er groupe de note de la 1ère matière du 1er pôle de la 1ère UE:*
```py
OGE.UE(1).pole(1).matiere(1).note(1).note(1)
```
ou
```py
OGE.UE(1).poles[0].matieres[0].notes[0].notes[0]
```

*Obtenir le nombre de notes du 1er groupe de notes de la 1ère matière du 1er pôle de la 1ère UE:*
```py
OGE.UE(1).pole(1).matiere(1).notes(1).getNoteCount()
```
ou
```py
OGE.UE(1).poles[0].matieres[0].notes[0].getNoteCount()
```


