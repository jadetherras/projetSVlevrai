#Projet programmation orientée objet (SSV)

##REPONSES du groupe *N* (*Reibel Mathieu* & *Therras Jade*) 

*************************************************
##Q1.1

-on utilise les fonctions contains() et isColliding() pour realiser les traitements des operateurs, afin d'eviter la duplication de code relative à ces fonctionnalités. On a déjà fait une surcharge de fonction pour l'opérateur >.

*************************************************
##Q1.2


-L'operateur << est externe, il n'y aurait pas de sens d'écrire out.operator<<(class) car cela demanderait de modifier la class de out.
Les operateur =, > et & definit entre deux circularBody sont en internes, puisqu'ils demandent de conparer les éléments de différentes instances d'une même classe. On préserve ainsi l'encapsulation.
Pour l'opérateur > entre un circularBody et un Vec2d, on compare des types différents donc définir en interne n'aurait pas de sens même si cela reste possible, on définit donc en externe.

*************************************************
##Q1.3


-La plupart des gros objets (CircularBody et Vec2d) passent par référence constante, sauf quand il doivent être modifiés (on enlève le const pour les set). Un passage par valeur fait une copie lourde, les minimiser permet une optimisation du programme.
pour l'operateur > défini en externe, on est obligé de faire une copie puisque l'acces aux méthodes donne la posibiliter de modifier les accès privés.

*************************************************
##Q1.4


-De manière générale, on recherche les méthodes ne devant modifier aucun argument, les prédicats, comme les méthodes get dont le rôle est de retourner les attributs, les méthodes de contains et isColliding.

*************************************************
##Q2.1

-Puisque qu'une boite de Pétri EST un objet circulaire, on fait en sorte que la classe PetriDish hérite de la classe CircularBody. Ainsi, PetriDish est une sous-classe de CircularBody.

*************************************************
##Q2.2

-La fonction addBacterium et addNutriment retournent des booléens pour savoir si l'ajout de bactéries et nutiments ont été réalisés avec succès. Quant à la fonction drawOn, elle dessine la boîte de Pétri. Ces trois fonctions ne modifient donc pas les attributs de la classe PetriDish : ce sont des prédicats.

*************************************************
##Q2.3

-Pour éviter la copie d'une boite de Pétri, on agit sur le constructeur de copie en écrivant la ligne suivante : "PetriDish (const PetriDish& Petri)=delete" qui interdit l'initialisation d'une boîte de Petri par copie d'une autre. Ensuite, on interdit l'affectation en agissant sur l'opération "=" via cette ligne "PetriDish& operator=(const PetriDish& Petri)=delete".

*************************************************
##Q2.4

-Puisqu'il est absurde de faire vivre des bactéries et laisser des nutriments sans boîte, il est indispensable que l'effacement de la boîte de Pétri implique celui des bactérie et des nutiments.
Ainsi, dans le codage du destructeur de la classe PetriDish, nous devons effacer les tableaux de pointeurs "bacteries" et "nutriments" en utilisant la méthode "reset"

*************************************************
##Q2.7

-Nos nutriments sont des corps circulaires, donc des circularbody avec des caracteristiques propres supplementaire. On peut donc definir la class nutriment comme une sous-classe de circular body, en utilisant "class Nutriment : public CircularBody" pour modeliser la tournure "est un" liant les deux classes.

*************************************************
##Q2.8

-on cherche toujours à modeliser un maximum, et a aider à la représentation. Utiliser la classe Quantity permet d'être plus précis sur la nature du double. On pourrait par exemple utiliser deux doubles pour représenter une quantité et une température, mais ce sont deux notions totalement différentes ! définir des types plus spécifique permet donc de rendre compte de ces nuances et d'empêcher au programmeur de se perdre dans son code.

*************************************************
##Q2.9

-on doit ajouter une méthode pour ajouter les nutriments, soit void addNutriment(Nutriment *nutriments); à notre class Lab. On doit ensuite pouvoir dessiner les Nutriments, on modifie donc la méthode drawOn de la class PetriDish, afin de permettre l'ajoue de l'ensemble des éléments.

*************************************************
##Q2.10

-en utilisant Application::getAppEnv on a acces au lab, il suffit ensuite d'utiliser la methode getTemperature pour prendre connaissance sans getter de la temperature de la boite de petri associée.

*************************************************
##Q2.11

- premierement, il ne faut pas oublier le lien entre rayon et quantite pour les nutriments en ecrivant la fonction update, pour voir les éléments grossir en fonction de la quantite.
On code les méthodes update et verifie que les méthode drawn prenne bien en compte les nutriments, dessinant alors en continue en fonction du changement de rayon.

*************************************************
##Q2.12

- pour modifier la temperature on ajoute les methodes decreaseTemperature() et increaseTemperature() pour les class Lab (appelé dans Application) et PetriDish. la classe Lab se contente d'appeler la classe PetriDish pour modifier la boite.
Pour permettre un reset de la température dans différent cas et sans duplication de code, on realise une methode resetTemp() dans lab, permettant comme sont nom l'indique de revenir à la valeur par défaut. Par la suite on code resetTemp() aussi dans Petridish. on l'appelle ensuite dans les methode reset, lié à la touche R. Pour la touche C on appelle aussi la fonction via Lab dans Application.
