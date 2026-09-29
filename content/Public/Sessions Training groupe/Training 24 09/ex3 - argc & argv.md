---
type: exercice
language: C
theme:
  - argc_argv
  - strings
level: 1
difficulty: debutant
status: ready
cssclasses:
  - teaching
---

# 🖥️ Arguments — Afficher les paramètres (ft_print_params)

## 🎯 Objectif

Comprendre :
- la signature complète de la fonction `main` ;
- à quoi sert `argc` (Argument Count) ;
- comment lire et manipuler `argv` (Argument Vector) qui est un `char **`.

---

## 📚 Prérequis

Tu dois connaître :
- `write` ;
- ta fonction `ft_putstr` des exercices précédents ;
- savoir compiler et exécuter un programme avec des arguments (`./a.out salut les amis`).

---

## 📝 Énoncé

Cette fois-ci, tu ne dois pas écrire juste une fonction, mais un **programme complet** (avec un `main`). 

Écris un programme qui affiche tous les arguments qu'il reçoit en ligne de commande, un par ligne, dans l'ordre où ils ont été donnés. 
Le nom du programme lui-même (qui est techniquement le premier argument) **ne doit pas** être affiché.

Si aucun argument n'est passé au programme, il ne doit rien afficher.

**Exemple attendu dans le terminal :**
```bash
$> gcc ft_print_params.c
$> ./a.out test1 test2 test3
test1
test2
test3
$> ./a.out
$>
```

---

> [!tip]- Indices et Tips
> ```text
> - La vraie signature du main en C est : int main(int argc, char **argv)
> - argc : C'est un int qui contient le nombre total d'arguments. S'il n'y a pas d'arguments, argc vaut 1 (car le nom du programme compte pour 1).
> - argv : C'est un tableau de strings (char **). 
> - Le nom du programme se trouve toujours dans argv[0].
> - Les arguments que tu tapes à côté commencent donc à l'index 1 (argv[1]).
> - Tu peux utiliser une boucle while qui va de i = 1 jusqu'à ce que i soit strictement inférieur à argc.
> - N'oublie pas d'ajouter ta fonction ft_putstr au-dessus de ton main pour pouvoir l'utiliser !
> ```

> [!check]- Correction
> ```c
> #include <unistd.h>
> 
> // On récupère notre fonction pour afficher une string
> void	ft_putstr(char *str)
> {
> 	int	i;
> 
> 	i = 0;
> 	while (str[i] != '\0')
> 	{
> 		write(1, &str[i], 1);
> 		i++;
> 	}
> }
> 
> // La signature complète du main
> int	main(int argc, char **argv)
> {
> 	int	i;
> 
> 	// On initialise i à 1 pour sauter argv[0] (le nom du programme)
> 	i = 1;
> 	
> 	// On boucle tant qu'on n'a pas atteint le nombre total d'arguments
> 	while (i < argc)
> 	{
> 		ft_putstr(argv[i]); // On affiche l'argument actuel
> 		write(1, "\n", 1);  // On ajoute le retour à la ligne
> 		i++;
> 	}
> 	
> 	return (0);
> }
> ```