
# Lire et écrire du texte dans le terminal

Le fichier `stdio.h` est une bibliothèque en langage C qui contient des fonctions pour gérer les entrées et sorties standards (**st**an**d**ard **i**nputs and **o**utputs). Les entrées et les sorties standard, cela peut se résumer aux fichiers et au terminal (techniquement sous UNIX le terminal est un fichier aussi, mais nous verrons cela plus tard).

Comme son nom l'indique, il est possible de gérer à la fois les entrées et les sorties avec cette librairie , nous allons donc pouvoir à la fois *lire* et *écrire* du texte dans le terminal et dans les fichiers.

Pour utiliser les fonctions de `stdio.h`, il faut l'inclure dans notre fichier :

```c
#include <stdio.h>

int main() {
    // nous pouvons utiliser les fonctions de stdio.h ici !
    return 0;
}
```

Nous allons commencer par les deux fonctions qui permettent de lire et écrire dans le terminal : `printf` et `scanf`.

## Afficher du texte printf

La fonction `printf` permet d'afficher du texte et des variables suivant un format défini (le **f** dans `printf` est pour « *formatted* »).

Nous alons commencer par afficher du texte, sans variables au milieu. On peut juste donner une chaîne de caractère et `printf`
l'affichera :

```c
// dans la fonction main
printf("Bonjour !\n");
```

Cette fonction, comme toutes les fonctions de `stdio` que nous allons utiliser n'ajoute pas de retour à la ligne automatiquement,
il faut donc finir la chaîne par un `\n`.

On peut utiliser une chaîne de caractère spéciale pour afficher la valeur de variables. Le premier argument de `printf` est toujours une chaîne de caractère, mais on marque les endroits où on veut que nos variables apparaissent avec des séquences spéciales.
Ces séquences sont composées d'un `%` suivant d'une lettre qui indique comment interpréter la variable à afficher.

Les principales lettres à connaître sont :

- `d` pour les nombres en base **d**ix ;
- `c` pour les **c**aractères ;
- `f` pour les **f**lottants ;
- `s` pour les chaînes de caractère (**s**tring) ;

Les variables à afficher viennent ensuite dans les arguments de `printf`. Elles doivent être
dans le même ordre que leur emplacement dans la chaîne. Voici un exemple qui affiche deux variables :

```c
// toujours dans la fonction main
int age = 19;
char *nom = "Corrèze";

printf("Le département numéro %d est la %s !", age, nom);
```

### Pourquoi est-ce que c'est si compliqué ?

On pourrait se demander pourquoi on ne peut pas juste additionner les chaînes, comme en Python :

```python
ville = "Grenoble"
print("Bienvenue à " + ville + " !")

# ou
print("Bienvenue à", ville, "!")
```

En réalité, la façon dont fonctionne le C fait qu'il est bien plus simple d'utiliser la technique
des chaînes de caractères avec des `%`. Nous sommes aussi obligés de mettre une lettre après
ces `%` parce que même si nos variables ont un type connu au moment de la compilation
(Nous pourrions donc pense que le compilateur sait qu'un `int` doit s'afficher comme un nombre décimal, et un `char *`
comme une chaîne de caractères, etc), cette information de type est perdue au moment de la compilation. Cela signifie que lorsque notre fonction est appelée, le programme ne sait plus quelle variable est de quel type. En plus de cela, il est possible de choisir d'utiliser différentes représentations pour un même type : par exemple les nombres sont souvent affichés en base 10, mais quand on fait de l'informatique ça peut être
utile de les afficher en binaire (avec **`%b`**) ou en héxadécimal (avec **`%x`**).

Pour résumer, cette façon un peu compliquée d'écrire un `print` est un mal nécessaire, et est parfois utile
quand on veut choisir une représentation différente de celle par défaut.

## Lire du texte

Nous allons maintenant voir comment utiliser `scanf` pour lire du texte tapé au clavier.

Cette fonction est similaire à `printf` : le premier argument est aussi une chaîne
indiquant le format attendu, puis nous avons les variables qui correspondent à chacun des `%`.

La différence est que `scanf` va écrire ce qui a été lu dans ces variables au lieu de les lire
pour les afficher. Il faut donc passer des pointeurs vers ces variables, sinon leur valeur sera
copiée pour `scanf` et elles ne pourront pas vraiment être modifiées.

Nous verrons la notion de pointeur plus tard durant cette année, pour l'instant, vous pourrez vous contenter d'admettre que le signe **&** indique l'adresse de la variable en mémoire (c'est donc un pointeur).

Voici un exemple qui permet de lire un nombre au clavier :

```c
int nombre;
scanf("%d", &nombre);

printf("Vous avez écrit %d\n", nombre);
```

Maintenant, que ce passe-t-il si ce qui est tapé ne correspond pas au format demandé ? Par exemple si
on tape `abcd` dans l'exemple ci-dessus, qu'est-ce qui est affiché à la fin ? La réponse est que la ou
les variables qui devaient être modifiées ne le seront pas.

Dans le cas où les variables ne sont pas initialisées ça peut être assez grave : même sans valeur précise,
de la place en mémoire est réservée pour chaque variable. Le souci c'est que cette mémoire peut avoir servi
à d'autre choses avant, et donc les valeurs par défaut des variables non-initialisées ne sont pas forcément
celles auxquelles on peut s'attendre.

Cela signifie qu'il faut toujours donner une valeur par défaut à ses variables (que ça soit pour les utiliser avec `scanf` ou pour un autre usage), car sinon votre programme peut avoir un comportement inattendu. 

# Exercices

## Exercice 1 :

Demander à l'utilisateur de taper son âge dans la console et l'afficher

## Exercice 2 :

Demander à l'utilisateur de taper son nom dans la console et afficher "Bonjour **nom de l'utilisateur**"

## Exercice 3 :

Demander à l'utilisateur de taper son âge et afficher : 

- "Vous êtes majeur en france et aux états-unis" si l'age est supérieur ou égal à 21
- "Vous êtes majeur en france mais pas aux états-unis" si l'age est compris entre 18 et 21 ans
- "Vous êtes mineur en france et aux états-unis" si l'age est inférieur à égal à 18


