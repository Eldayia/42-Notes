---
type: exercice
language: C
theme:
  - malloc
  - arrays
level: 2
difficulty: intermediaire
status: ready
cssclasses:
  - teaching
---

# 🔢 Allocation dynamique — Le tableau d'entiers (ft_range)

## 🎯 Objectif

Comprendre :
- l'importance cruciale de `sizeof()` quand on alloue autre chose que des `char` ;
- allouer et remplir un tableau d'entiers (`int *`).

---

## 📚 Prérequis

Tu dois connaître :
- `malloc` ;
- la différence de taille en mémoire entre un `char` (1 octet) et un `int` (souvent 4 octets).

---

## 📝 Énoncé

Écris une fonction `ft_range` qui retourne un tableau de `int`. 
Ce tableau doit contenir toutes les valeurs comprises entre `min` (inclus) et `max` (exclus).
Si la valeur `min` est supérieure ou égale à `max`, la fonction doit retourner un pointeur `NULL`.

```c
int	*ft_range(int min, int max);
```

---

> [!tip]- Indices et Tips
> ```text
> - Contrairement aux strings, un tableau d'entiers ne se termine PAS par un '\0'. Tu dois juste allouer le nombre exact de cases.
> - Combien de cases faut-il ? La formule mathématique est simple : (max - min). Par exemple, entre 2 et 5, il y a 3 nombres (2, 3 et 4).
> - ATTENTION : Un int ne prend pas 1 octet en mémoire ! Tu dois faire malloc(sizeof(int) * nombre_de_cases).
> - Gère le cas d'erreur (min >= max) dès le début de ta fonction pour retourner NULL.
> - Utilise un index (par exemple i) partant de 0 pour remplir ton tableau, pendant que tu insères les valeurs de 'min' jusqu'à 'max'.
> ```

> [!check]- Correction
> ```c
> #include <stdlib.h>
> 
> int	*ft_range(int min, int max)
> {
> 	int	*tab;
> 	int	i;
> 	int	size;
> 
> 	if (min >= max)
> 		return (NULL);
> 
> 	size = max - min;
> 	// Allocation en utilisant sizeof(int) !
> 	tab = (int *)malloc(sizeof(int) * size);
> 	if (tab == NULL)
> 		return (NULL);
> 
> 	i = 0;
> 	while (min < max)
> 	{
> 		tab[i] = min;
> 		i++;
> 		min++;
> 	}
> 	
> 	return (tab);
> }
> ```