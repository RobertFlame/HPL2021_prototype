# HPL2021_prototype

Série 7:

Introduction aux objets

Buts
Dans cette série, vous travaillerez avec les bases de la programmation orientée objets. Vos
programmes seront modularisés sous forme de méthodes auxiliaires ainsi que sous forme de
classes comprenant des variables d'instance et des méthodes d'instance.

Exercice 1: Conception d'un programme OO simple (POO de
base, Niveau 0)
Le but de cet exercice est d'illustrer les notions d'objet et de classe au moyen d'un exemple
simple.
Il s'agit ici de définir une classe Rectangle représentant une abstraction (informatique) de ce
qu'est un rectangle : une largeur, une longueur et sa surface.
Commencez par ouvrir un fichier ManipRectangle.java et définissez­y la classe :

'''java
class Rectangle {
}
'''

Bien ! Prévoyons tout de suite d'utiliser notre toute première classe. Pour cela il faut déclarer une
variable de type Rectangle. Cela se fait comme pour n'importe quelle autre variable utilisée
jusque maintenant, la classe Rectangle étant simplement un nouveau type. La méthode main est
mise ici dans la classe ManipRectangle qui constitue le programme principal :
class ManipRectangle {
public static void main(String[] args) {
Rectangle rect;
}
}
Bon, jusque là pas grand chose de bien intéressant. Implémentons maintenant l'abstraction
"rectangle" en commençant par les deux attributs largeur et longueur.
Cela se fait comme suit :
class Rectangle {
double largeur;
double longueur;
}
Dotons notre classe d'une méthode constructeur construisant nos objets Rectangle et initialisant
leurs attributs. Notez que le constructeur a le même nom que la classe, et que dans le
programme principal la déclaration­initialisation d'un rectangle se fait en utilisant le constructeur.
class Rectangle {
double largeur;
double longueur;
//Le constructeur
public Rectangle(double uneLargeur, double uneLongueur) {
// largeur et longueur sont les attributs
// de la classe

largeur = uneLargeur;
longueur = uneLongueur;
}
// largeur et longueur sont les attributs
// de la classe
}
Pour le calcul de la surface, nous implémentons une méthode, c'est­à­dire un traitement propre à
la classe.
Les méthodes se déclarent comme les méthodes auxiliaires que vous connaissez jusqu'ici, sauf
qu'on n'utilise pas le mot clé static.
class Rectangle {
double largeur;
double longueur;
//Le constructeur
public Rectangle(double uneLargeur, double uneLongueur) {
largeur = uneLargeur;
longueur = uneLongueur;
}
// largeur et longueur sont les attributs
// de la classe
// La méthode pour le calcul de la surface
public double surface () {
return largeur * longueur;
}
}
On peut maintenant déjà tester notre programme :
class Rectangle {
double largeur;
double longueur;
public Rectangle(double uneLargeur, double uneLongueur) {
largeur = uneLargeur;
longueur = uneLongueur;
}
public double surface() {
return largeur * longueur;
}
}
class ManipRectangle {
public static void main(String[] args) {
Rectangle rect = new Rectangle(1.5,12.8);
System.out.println("Surface : " + rect.surface());
}
}
Compilez et exécutez ce programme.
Supposons maintenant que nous souhaitions modifier les valeurs des attributs dans le programme
principal:
...
class ManipRectangle {

public static void main(String[] args) {
Rectangle rect = new Rectangle(1.5, 12.8);
System.out.println("Surface : " + rect.surface());
rect.largeur = 3.2;
rect.longueur = 6.9;
}
}
Essayons maintenant d'affiner notre "style objet" en rendant privés les attributs et ne laissant
publiques que les méthodes :
class Rectangle {
private double largeur;
private double longueur;
public Rectangle(double uneLargeur, double uneLongueur){
largeur = uneLargeur;
longueur = uneLongueur;
}
public double surface() {
return largeur * longueur;
}
}
class ManipRectangle {
public static void main(String[] args) {
Rectangle rect = new Rectangle(1.5,12.8);
System.out.println("Surface : " + rect.surface());
rect.largeur = 3.2;
rect.longueur = 6.9;
}
}
Essayez de compiler ce programme. Que se passe­t­il?
Le message est assez clair : tout les attributs sont privés. Cela veut dire qu'on ne peut pas les
utiliser hors de l'objet (ils ne font pas partie de l'interface de l'objet).
En particulier, on n'a pas le droit de faire rect.largeur ! Ce n'est pas défini.
Pour rendre accessible depuis l'extérieur un attribut, il faut mettre en place les méthodes "get" et
"set" correspondantes (qui devront évidement être publiques !).
Cela se fait simplement, comme pour la méthode du calcul de surface. Dans la méthode main
l'accès aux attributs se fera désormais en passant par ces méthodes
L'intérêt est notamment que l'on peut faire faire à ces méthodes des contrôles d'intégrité sur les
données (de sorte à ne pas mettre n'importe quoi comme valeur aux attributs). L'accès direct aux
attributs, sans passer par des méthodes, n'offre pas cette sécurité.
class Rectangle {
private double largeur;
private double longueur;
public Rectangle(double uneLargeur, double uneLongueur){
largeur = uneLargeur;
longueur = uneLongueur;
}
public double surface() {
return largeur * longueur;

}
public double getLongueur() {
return longueur;
}
public double getLargeur() {
return largeur;
}
public void setLargeur(double l) {
if (l < 0) {
l = ‐l;
}
largeur = l;
}
public void setLongueur(double l) {
if (l < 0) {
l = ‐l;
}
longueur = l;
}
}
class ManipRectangle {
public static void main(String[] args) {
Rectangle rect = new Rectangle(1.5,12.8);
System.out.println("Surface : " + rect.surface());
rect.setLargeur(3.2);
rect.setLongueur(6.9);
System.out.println("Surface : " + rect.surface());
}
}
Recompilez. Ça fonctionne cette fois­ci et vous avez codé votre premier programme objet !

Exercice 2: MOOC (cours en ligne) (MOOC, Niveau 1)
Cette semaine vous devez visionner les vidéos de la semaine 1 et de la semaine 2 du MOOC.
Pour bien assimiler ce contenu, il est recommandé de faire les quiz des mêmes semaines: Quiz
«Classes et objets» et Quiz «Constructeurs».
Exercice 3: Calcul de surfaces (POO de base, Niveau 1)
Le fichier Surfaces.java contient les déclarations de trois classes: Surfaces, Terrain et Rectangle.
Attention: si vous avez fait le premier exercice, un classe Rectangle a déjà été créée dans le
projet de cette série. Pour éviter les incompatibilités, renommez là.
Pour cette exercice, la classe Rectangle définit des objets de type rectangle, la classe
Terrain définit des objets constitués de deux rectangles et permet de calculer leur surface
totale.
Etudiez le code contenu dans le fichier Surfaces.java pour en comprendre les structures et
fonctionnalités.
Incorporez le fichier dans Eclipse. Vérifiez, dans un terminal, dans le répertoire du
workspace correspondant à cette série, qu'il y a vraiment un fichier .class correspondant à
chaque classe déclarée dans le fichier compilé.

Toujours depuis le terminal, essayez de démarrer la classe Rectangle. Vous aurez un
message d'erreur (lequel ?) car cette classe n'a pas de méthode main et n'est donc pas
démarrable. Démarrez le programme à l'aide de la classe qui a une méthode main.
Modifiez le code comme suit:
Calculez la surface d'un terrain composé de 3 rectangles et de 2 cercles. Vous pouvez
soit entrer les données directement dans le code, soit demander à l'utilisateur de les
entrer au clavier. Par exemple, vous aurez une surface totale de 398.9999698556466
si vos 3 rectangles sont de largeur/hauteur 1.0/2.0, 3.0/4.0 et 5.0/6.0 et si vos 2
cercles sont de rayon 7.0 et 8.0
Dans ce but, il faut ajouter une classe Cercle au programme. Cette classe peut, par
exemple, avoir une variable d'instance rayon et une méthode d'instance
calculerSurface. La surface d'un cercle est calculée par la formule π · r
2
. Vous

pouvez utiliser la constante prédéfinie Math.PI.
Rappelez­vous que plusieurs classes peuvent utiliser le même nom pour leurs
méthodes d'instance. Il n'y a aucun conflit car une méthode d'instance est toujours
appelée à travers un objet d'une classe précise, ce qui permet de choisir la bonne
méthode à exécuter. Vous pouvez donc, par exemple, avoir une méthode
calculerSurface dans la classe Rectangle ainsi que dans la classe Cercle. Choisissez
toujours l'identificateur le plus parlant possible pour vos variables, méthodes et
classes.
Code donné:

Surfaces.java

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
/* Dans ce programme, les 2 réctangles sont encapsulés dans un objet
* de type Terrain qui s'occupe de calculer et d'afficher la surface
* totale. Le mot­clé private a été utilisé le plus possible dans
* toutes les classes. La classe Rectangle met aussi à disposition des
* méthodes get et set pour ses variables (il s'agit d'un service que
* le programmeur de la classe peut offrir à ses utilisateurs s'il le
* juge utile).
*/
class Surfaces {
public static void main(String[] args) {
// Construction d'un terrain:
Terrain t = new Terrain(1.0, 2.0, 3.0, 4.0);
t.afficherSurfaceTotale();
}
}
class Terrain {
private Rectangle r1;
private Rectangle r2;
public Terrain(double l1, double h1, double l2, double h2) {
// Construction des 2 rectangles définissant le terrain:
r1 = new Rectangle(l1, h1);
r2 = new Rectangle(l2, h2);
}
private double calculerSurfaceTotale() {
return r1.calculerSurface() + r2.calculerSurface();
}
public void afficherSurfaceTotale() {
double surfaceTotale = calculerSurfaceTotale();

37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70

System.out.println("La surface totale est " + surfaceTotale);
}
}
class Rectangle {
private double largeur;
private double hauteur;
public Rectangle(double largeur, double hauteur) {
this.largeur = largeur;
this.hauteur = hauteur;
}
public void setLargeur(double largeur) {
this.largeur = largeur;
}
public double getLargeur() {
return largeur;
}
public void setHauteur(double hauteur) {
this.hauteur = hauteur;
}
public double getHauteur() {
return hauteur;
}
public double calculerSurface() {
return (largeur * hauteur);
}
}

Exercice 4: Tutorial Eclipse 8 : Activer la vue Outline
(Eclipse, Niveau 0)
La vue "Outline" de Eclipse synthétise la structure du fichier courant en terme de classes, attributs et méthodes.
Ce tutorial vous montre comment activer cette vue.
En fait, il suffit de sélectionner "Window‐>Show View‐>Outline" dans le menu principal :

La vue "Outline" va alors apparaître. Vous pouvez changer la position de cette vue au moyen de la souris. Voici
un exemple de vue "Outline"pour le fichier Surfaces.java de l'exercice 2 de la série 6 :

Les icônes donnent le type de l'élément concerné ; par exemple :

Désigne une classe
Désigne un constructeur
Désigne un attribut privé
Désigne une méthode publique

Exercice 5: Banque (Transformation d'un programme non
OO en un programme OO, POO de base, Niveau 2)
Le fichier Banque1.java contient un programme bancaire qui est modularisé sous forme de
méthodes auxiliaires. Transformez­le en programme orienté objet sous le nom de Banque2.java
en suivant les étapes suivantes :
Etudiez le fonctionnement du programme. La banque a 2 clients. Chaque client a un compte
privé et un compte d'épargne avec des soldes différents. Le taux d'intérêt d'un compte
d'épargne est plus élevé que celui d'un compte privé. Les données de chaque client (nom,
ville et soldes) sont affichées avant et après le bouclement des comptes.
Réfléchissez aux objets que vous aimeriez utiliser dans votre programme et ajoutez les
classes correspondantes. Il peut s'agir d'objets de toute nature (client, maison, billet,
compte, relation bancaire etc.). N'oubliez pas que la modularisation n'est pas une science
exacte. Chaque programmeur décide des classes qu'il trouve utiles pour son programme.
C'est souvent l'étape la plus difficile d'un projet de programmation.
Transférez le code concernant les objets dans les classes. Utilisez le mot­clé private pour
encapsuler les variables et les méthodes d'instance qui ne seront pas utilisées à l'extérieur
de la classe. Chaque méthode (auxiliaire ou d'instance) devrait être courte et sans trop
d'instructions détaillées. Les identificateurs (noms des variables et des méthodes) devraient
être parlants.
Exemple d'exécution du programme:

Donnees avant le bouclement des comptes:
Client Pedro de Geneve
Compte prive: 1000.0 francs
Compte d'epargne: 2000.0 francs
Client Alexandra de Lausanne
Compte prive: 3000.0 francs
Compte d'epargne: 4000.0 francs
Donnees apres le bouclement des comptes:
Client Pedro de Geneve
Compte prive: 1010.0 francs
Compte d'epargne: 2040.0 francs
Client Alexandra de Lausanne
Compte prive: 3030.0 francs
Compte d'epargne: 4080.0 francs
Code donné:

Banque1.java

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
class Banque1 {
public static void main(String[] args) {
// Données pour tous les comptes privés (taux d'intérêt):
double taux1 = 0.01;
// Données pour tous les comptes d'épargne (taux d'intérêt):
double taux2 = 0.02;
// Données pour le premier client (nom et ville):
String nom1 = "Pedro";
String ville1 = "Geneve";
// Données pour le compte privé du premier client (solde):
double solde1PremierClient = 1000.0;
// Données pour le compte d'épargne du premier client (solde):
double solde2PremierClient = 2000.0;
// Données pour le deuxième client (nom et ville):
String nom2 = "Alexandra";
String ville2 = "Lausanne";

19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57

// Données pour le compte privé du deuxième client (solde):
double solde1DeuxiemeClient = 3000.0;
// Données pour le compte d'épargne du deuxième client (solde):
double solde2DeuxiemeClient = 4000.0;
// Afficher les données du premier client:
afficherClient(nom1, ville1, solde1PremierClient, solde2PremierClient);
// Afficher les données du deuxième client:
afficherClient(nom2, ville2, solde1DeuxiemeClient, solde2DeuxiemeClient);
// Bouclement du compte privé du premier client:
solde1PremierClient = bouclerCompte(solde1PremierClient, taux1);
// Bouclement du compte d'épargne du premier client:
solde2PremierClient = bouclerCompte(solde2PremierClient, taux2);
// Bouclement du compte privé du deuxième client:
solde1DeuxiemeClient = bouclerCompte(solde1DeuxiemeClient, taux1);
// Bouclement du compte d'épargne du deuxième client:
solde2DeuxiemeClient = bouclerCompte(solde2DeuxiemeClient, taux2);
// Afficher les données du premier client:
afficherClient(nom1, ville1, solde1PremierClient, solde2PremierClient);
// Afficher les données du deuxième client:
afficherClient(nom2, ville2, solde1DeuxiemeClient, solde2DeuxiemeClient);
}
static void afficherClient(String nom, String ville,
double solde1, double solde2) {
// Cette méthode affiche les données du client
System.out.println("Client " + nom + " de " + ville);
System.out.println(" Compte prive: " + solde1 + " francs");
System.out.println(" Compte d'epargne: " + solde2 + " francs");
}
static double bouclerCompte(double solde, double taux) {
// Cette méthode ajoute les intérêts au solde
double interets = taux * solde;
double nouveauSolde = solde + interets;
return nouveauSolde;
}
}
Banque avec des clientes (Niveau 1)
Vous avez bien noté que l'affichage du programme Banque1 ne fait pas de différence entre les
clientes et les clients. Ceci est facile à corriger dans la version orientée objets du programme,
par exemple en ajoutant une variable d'instance booléenne masculin à la classe Client (si vous en
avez une) et en testant sa valeur dans la méthode d'affichage. Modifiez votre programme, par
exemple sous le nom de Banque3, pour qu'il affiche "cliente" au lieu de "client" comme suit:

Donnees avant le bouclement des comptes:
Client Pedro de Geneve
Compte prive: 1000.0 francs
Compte d'epargne: 2000.0 francs
Cliente Alexandra de Lausanne
Compte prive: 3000.0 francs
Compte d'epargne: 4000.0 francs
Donnees apres le bouclement des comptes:
Client Pedro de Geneve
Compte prive: 1010.0 francs
Compte d'epargne: 2040.0 francs
Cliente Alexandra de Lausanne
Compte prive: 3030.0 francs
Compte d'epargne: 4080.0 francs

Exercice 6: Géométrie (POO de base, Niveau 2)
Ecrivez un programme Geometrie qui permet à l'utilisateur d'entrer les coordonnées (x, y) des
sommets d'un triangle. Le programme affiche ensuite le périmètre du triangle ainsi qu'un
message indiquant s'il s'agit d'un triangle isocèle. Votre programme doit être orienté objets.
Indications:
Un triangle est isocèle si au moins deux côtés ont la même longueur.
La formule pour calculer la distance entre deux points (x1, y1) et (x2, y2) est: racine
carrée de (x1 ­ x2)2 + (y1 ­ y2)2.
Java met à disposition la méthode Math.sqrt() pour calculer la racine carrée. Cette
méthode prend un nombre non­négatif en paramètre. Exemple:
double a = Math.sqrt(9.0); // la valeur 3.0 sera affectée à a
Exemple d'affichage du programme pour un triangle isocèle:

Construction d'un nouveau point
Veuillez entrer x : 0
Veuillez entrer y : 0
Construction d'un nouveau point
Veuillez entrer x : 2.5
Veuillez entrer y : 2.5
Construction d'un nouveau point
Veuillez entrer x : 0
Veuillez entrer y : 5
Périmètre : 12.071067811865476
Le triangle est isocèle
Dans cet exercice, vous élaborerez un programme orienté objets de manière indépendante pour
la première fois. Si vous n'avez pas le temps de faire cet exercice, n'oubliez pas d'en étudier le
corrigé.
Voici quelques indications en vrac qui peuvent vous être utiles. Ne les lisez pas si vous voulez
être complètement indépendant ...
Réfléchissez aux objets que vous aimeriez utiliser dans le programme. Vous pourriez par
exemple représenter le triangle par une classe Triangle et ses points par une classe Point.
Une troisième classe Geometrie pourrait héberger la méthode main.
Réfléchissez aux variables et méthodes d'instance qui seraient utiles pour les classes
Triangle et Point.
Un objet de type Point a typiquement les coordonnées x et y. Un objet de type Triangle a
trois sommets qui peuvent être représentés par des objets de type Point.
Les coordonnées des points peuvent par exemple être entrées dans le programme principal
à l'aide de la méthode scanner.nextDouble().
Le périmètre d'un triangle peut être calculé comme la somme des distances entre les trois
sommets.

Exercice 7: Supermarché (poo de base, Niveau 2)

Un supermarché souhaite que vous l’aidiez à afficher le total des achats enregistrés par ses
caisses. Il s’agit de compléter le programme Supermarche.java.
Voici les entités nécessaires pour modéliser le fonctionnement du supermarché :
les articles vendus : caractérisés par leur nom (une chaîne de caractères), leur prix
unitaire (un double) et une information indiquant si l’article est en action ou pas (un
booléen).
les achats : un achat est caractérisé par l’article acheté et la quantité achetée de cet
article.
les caddies : caractérisés par l’ensemble des achats qu’ils contiennent .
les caisses : chargées de scanner et enregistrer le contenu des caddies. Une caisse est
caractérisée par un numéro de caisse (un entier) et le montant total des achats qu’elle a
scanné (un double).
Le programme principal est fourni dans le fichier Supermarche.java. Il a pour but de faire afficher
le montant total de chaque caisse au bout d’une journée donnée. Commencez par l’étudier.
Il s’agit maintenant de coder les structures de données et les méthodes manquantes. Ces entités
doivent pouvoir être testées avec le programme principal fourni :

Supermarche.java

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
public class Supermarche {
public static void main(String[] args) {
// Les articles vendus dans le supermarché
Article choufleur = new Article("Chou­fleur extra", 3.50, false);
Article roman = new Article("Les malheurs de Sophie", 16.50, true);
Article camembert = new Article("Cremeux 100%MG", 5.80, false);
Article cdrom = new Article("C++ en trois jours", 48.50, false);
Article boisson = new Article("Petit­lait", 2.50, true);
Article petitspois = new Article("Pois surgeles", 4.35, false);
Article poisson = new Article("Sardines", 6.50, false);
Article biscuits = new Article("Cookies de grand­mere", 3.20, false);
Article poires = new Article("Poires Williams", 4.80, false);
Article cafe = new Article("100% Arabica", 6.90, true);
Article pain = new Article("Pain d'epautre", 6.90, false);
// Les caddies du supermarché
Caddie caddie1 = new Caddie();
Caddie caddie2 = new Caddie();
Caddie caddie3 = new Caddie();
// Les caisses du supermarché
// le premier argument est le numero de la caisse
// le second argument est le montant initial de la caisse.
Caisse caisse1 = new Caisse(1, 0.0);
Caisse caisse2 = new Caisse(2, 0.0);
// les clients font leurs achats
// le second argument de la méthode remplir
// correspond à une quantité
// remplissage du 1er caddie
caddie1.remplir(choufleur, 2);
caddie1.remplir(cdrom, 1);
caddie1.remplir(biscuits, 4);
caddie1.remplir(boisson, 6);
caddie1.remplir(poisson, 2);
// remplissage du 2eme caddie
caddie2.remplir(roman, 1);
caddie2.remplir(camembert, 1);

43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58

caddie2.remplir(petitspois, 2);
caddie2.remplir(poires, 2);
// remplissage du 3eme caddie
caddie3.remplir(cafe, 2);
caddie3.remplir(pain, 1);
caddie3.remplir(camembert, 2);
// Les clients passent à la caisse
caisse1.scanner(caddie1);
caisse1.scanner(caddie2);
caisse2.scanner(caddie3);
caisse1.totalCaisse();
caisse2.totalCaisse();
}
}

Dans le fichier Supermarche.java , déclarez les classes nécessaires à la modélisation du
supermarché, telles que suggérées ci­dessus.
Il vous est suggéré d'utiliser un ArrayList d'achats pour modéliser le contenu du caddie (voir
cours 4, pages 42 et 43).
Faites bien attention à l'encapsulation (les variables d'instances doivent être privées).
Les méthodes à implémenter dans la classe concernant les achats sont :
afficher() affichant les caractéristiques de l'article (son nom, son prix unitaire, la quantité
achetée et le prix de l’achat). De plus, si l’article concerné est en action, il faudra afficher
le texte "(1/2 prix)". Voici le modèle d’affichage pour afficher() :
Petit­lait : 2.5 x 6 = 7.5 Frs (1/2 prix)
où Petit‐lait est le nom de l’article, 2.5 son prix unitaire, 6 la quantité achetée, 7.5 le prix
de l’achat et (1/2 prix) une indication que l’article est en action (et donc à demi­prix). Cette
indication ne doit évidemment apparaitre que si l’article est en action.
toute autre méthode vous semblant nécessaire.
Pour les caddies :
remplir(..) conforme au programme principal fourni.
Réfléchissez à comment stocker le contenu du caddie (qui sera scanné par la suite).
toute autre méthode vous semblant nécessaire.
Pour les caisses :
totalCaisse() qui affiche son numéro et la valeur de son champ montant total selon la
forme de l’exemple suivant :
La caisse 1 a encaisse 121.15 Frs aujourd'hui.

où 1 est le numéro de la caisse et 121.15 le montant total. Vous supposerez que ce
montant total est stocké comme attribut (et qu'il est mis à jour par la méthode scanner(..),
ci­dessous).
scanner(...) : cette méthode, qui doit être conforme au programme principal fourni,
permet à la caisse d’afficher le ticket de caisse correspondant au contenu du caddie. Cette
méthode doit aussi mettre à jour le montant total de la caisse en y ajoutant le montant
des achats du caddie.
L’affichage tu ticket de caisse doit se faire selon le modèle ci­dessous et doit utiliser la
méthode afficher précédemment codée :

=========================================
14/10/11
Caisse numéro 2
100% Arabica : 6.9 x 2 = 6.9 Frs (1/2 prix)
Pain d'epautre : 6.9 x 1 = 6.9 Frs
Cremeux 100%MG : 5.8 x 2 = 11.6 Frs
Montant à payer : 25.4 Frs
=========================================
Pour afficher la date courante vous pouvez utiliser les instructions suivantes
Date dateCourante = new Date();
SimpleDateFormat formatDate = new SimpleDateFormat("dd/MM/yy");
System.out.println(formatDate.format(dateCourante));
Il faudra au préalable avoir fait les importations suivantes en début de fichier:
import java.util.Date;
import java.text.SimpleDateFormat;
toute autre méthode vous semblant nécessaire.
Une fois le programme complété, l'exécution du programme principal devrait ressembler à ceci:
=========================================
14/10/11
Caisse numero 1
Chou‐fleur extra : 3.5 x 2 = 7.0 Frs
C++ en trois jours : 48.5 x 1 = 48.5 Frs
Cookies de grand‐mere : 3.2 x 4 = 12.8 Frs
Petit‐lait : 2.5 x 6 = 7.5 Frs (1/2 prix)
Sardines : 6.5 x 2 = 13.0 Frs
Montant à payer : 88.8 Frs
=========================================
=========================================
14/10/11
Caisse numero 1
Les malheurs de Sophie : 16.5 x 1 = 8.25 Frs (1/2 prix)
Cremeux 100%MG : 5.8 x 1 = 5.8 Frs
Pois surgeles : 4.35 x 2 = 8.7 Frs
Poires Williams : 4.8 x 2 = 9.6 Frs
Montant à payer : 32.35 Frs
=========================================
=========================================
14/10/11
Caisse numero 2
100% Arabica : 6.9 x 2 = 6.9 Frs (1/2 prix)
Pain d'epautre : 6.9 x 1 = 6.9 Frs
Cremeux 100%MG : 5.8 x 2 = 11.6 Frs
Montant à payer : 25.4 Frs
=========================================
La caisse numero a encaisse 121.15 Frs aujourd'hui
La caisse numero a encaisse 25.40 Frs aujourd'hui

Dernière mise à jour: 04/11/2016 (Revision: 1.2)
