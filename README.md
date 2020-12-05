# flower_classification

## Travail fait par Belkassa Said et moi même Reguigui Yassine

Exercice en classe de Deep Learning :

1- Choisir une compétition sur Kaggle

2- Prendre le code d'un des participants, de préference utilisant pytorch mais n'importe quelle bibliothèque de DL est acceptée

3- Créer repo Github contenant :
  * Readme avec le contexte de la compétition, les données et les difficultés rencontrées
  * Notebook commenté
  * Noter les "astuces"
  
  
Compétion choisie : https://www.kaggle.com/nachiket273/flower-classification-lookahead-radam

## Données et contexte compétition

Cette compétition a été créée par Udacity pour avoir un classement ( officieux ) du Udacity PyTorch FB Challenge.
Nous avons un dataset consistant de 102 categories de fleurs differentes.
Nous avons :
- Dossier train contenant 102 dossiers pour chacune des classes de fleurs. Chaque dossier a entre 40 et 258 images
- Dossier valid contenant 102 dossiers pour chacune des classes de fleurs
- Dossier test contenant 819 images pour la submission de la compétition
- Fichier cat_to_name.json avec comme clé le numéro du dossier/classe et comme valeur le nom de la classe/fleur

## Astuces

- Cyclic Learning Rate ( CLR ) 
https://arxiv.org/abs/1506.01186

![Screenshot](clrexp.png)

Le CLR est un technique qui permet de trouver le meilleur Learning rate :

 1- On définit le minimum ou base de notre Learning rate appelé : base_lr
 
 2- On définit le maximum de notre Learning rate appelé : max_lr
 
 3- On fait osciller le Learning Rate entre base_lr et max_lr jusqu'à ce que la loss explose
 
 ![Screenshot](learing_rate_finder_lr_plot.png)

- Lookahead K steps forward, 1 step Back
https://arxiv.org/pdf/1907.08610.pdf

Le Lookahead est un optimizer pour le Stochastic Gradient Descente ( SGD ) dans notre cas qui permet d'améliorer la stabilité de l'apprentissage avec un cout en mémoire et de computation négligeables :

1- On initialise nos poids comme d'habitude pour le SGD et on lui attribue la characteristique de "slow_weight" ou poids lent

2- On fait k steps ou epochs avec SGD en utilisant des "fast_weights" ou poids rapide

 ![Screenshot](lookahead_2.PNG)

3- On fait une interpolation linéaire de l'espace de paramètres des fast_weights 

 ![Screenshot](lookahead_4.PNG)

4 - On repète autant de fois que l'on décide

