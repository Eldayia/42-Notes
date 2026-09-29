---
type: exercice
language: C
theme:
  - main
  - tests
level: 1
difficulty: debutant
status: ready
cssclasses:
  - teaching
---

# 🧪 Main — Tester ses fonctions

## 🎯 Objectif

Comprendre :
- pourquoi on écrit un `main` de test pour **chaque** fonction rendue à l'exam ;
- comment appeler une fonction selon son prototype (valeur, adresse, tableau) ;
- comment afficher un résultat pour vérifier qu'il est correct ;
- qu'on doit `free` ce qui a été alloué par la fonction testée.

---

## 📚 Prérequis

Tu dois connaître :
- les fonctions de la séance du 24/09 (`ft_strlen`, `ft_strdup`, `ft_range`) ;
- `printf` (autorisé dans tes tests, **pas** dans ton rendu) ;
- l'opérateur `&` pour donner l'adresse d'une variable.

---

## 📝 Énoncé

À l'exam, la moulinette ne te dit rien avant d'avoir corrigé : c'est à **toi** de tester. On te donne uniquement des prototypes, ton travail est d'écrire un `main` qui les appelle et affiche le résultat.

Pour chacun des prototypes suivants, écris un `main` qui teste la fonction avec **au moins 3 cas** dont un cas limite (chaîne vide, zéro, négatif, bornes inversées…).

```c
int		ft_strlen(char *str);
void	ft_swap(int *a, int *b);
char	*ft_strdup(char *src);
int		*ft_range(int min, int max);
```

Rappels :
- `ft_swap` échange les valeurs pointées par `a` et `b`.
- `ft_range` retourne un tableau des entiers de `min` (inclus) à `max` (exclu), ou `NULL` si `min >= max`.

**Exemple attendu dans le terminal :**
```bash
$> cc -Wall -Wextra -Werror ft_strlen.c main.c
$> ./a.out
ft_strlen("Hello") = 5
ft_strlen("") = 0
ft_strlen("42 Paris") = 8
```

---

> [!tip]- Indices et Tips
> ```text
> - Avant d'écrire le main, lis le prototype : que prend la fonction ? que retourne-t-elle ?
> - Retourne un int -> stocke-le dans un int et affiche-le avec printf("%d\n", ...).
> - Prend un int * -> crée un int normal, puis envoie son adresse : ft_swap(&a, &b).
> - Retourne un char * alloué -> affiche-le avec "%s", puis free() le résultat.
> - Retourne un int * -> tu dois connaître la taille (ici max - min) pour le parcourir, et tester le NULL avant.
> - Teste TOUJOURS les cas limites : "", 0, nombres négatifs, min == max.
> - Compile avec -Wall -Wextra -Werror comme la moulinette.
> - Piège de l'exam : si le sujet demande une fonction, NE RENDS PAS le main ! Mets-le dans un fichier à part (main.c) ou supprime-le avant de push.
> ```

> [!check]- Correction
> ```c
> #include <stdio.h>
> #include <stdlib.h>
> 
> int		ft_strlen(char *str);
> void	ft_swap(int *a, int *b);
> char	*ft_strdup(char *src);
> int		*ft_range(int min, int max);
> 
> void	test_strlen(void)
> {
> 	printf("ft_strlen(\"Hello\") = %d\n", ft_strlen("Hello"));
> 	printf("ft_strlen(\"\") = %d\n", ft_strlen(""));
> 	printf("ft_strlen(\"42 Paris\") = %d\n", ft_strlen("42 Paris"));
> }
> 
> void	test_swap(void)
> {
> 	int	a;
> 	int	b;
> 
> 	a = 21;
> 	b = 42;
> 	printf("Avant : a = %d, b = %d\n", a, b);
> 	ft_swap(&a, &b); // On envoie les ADRESSES
> 	printf("Après : a = %d, b = %d\n", a, b);
> }
> 
> void	test_strdup(char *src)
> {
> 	char	*copy;
> 
> 	copy = ft_strdup(src);
> 	if (copy == NULL)
> 	{
> 		printf("ft_strdup a retourné NULL\n");
> 		return ;
> 	}
> 	printf("src = \"%s\" | copie = \"%s\" | adresses différentes : %d\n",
> 		src, copy, src != copy);
> 	free(copy); // Ce que la fonction alloue, le main le libère
> }
> 
> void	test_range(int min, int max)
> {
> 	int	*tab;
> 	int	i;
> 
> 	tab = ft_range(min, max);
> 	printf("ft_range(%d, %d) = ", min, max);
> 	if (tab == NULL)
> 	{
> 		printf("NULL\n");
> 		return ;
> 	}
> 	i = 0;
> 	while (i < max - min)
> 	{
> 		printf("%d ", tab[i]);
> 		i++;
> 	}
> 	printf("\n");
> 	free(tab);
> }
> 
> int	main(void)
> {
> 	test_strlen();
> 	test_swap();
> 	test_strdup("Bonjour");
> 	test_strdup("");
> 	test_range(2, 6);
> 	test_range(-3, 1);
> 	test_range(5, 5);
> 	return (0);
> }
> ```
