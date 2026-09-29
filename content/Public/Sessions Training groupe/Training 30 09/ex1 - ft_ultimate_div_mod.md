---
type: exercice
language: C
theme:
  - pointers
level: 2
difficulty: debutant
status: ready
cssclasses:
  - teaching
---

# 🎯 Pointeurs — Division et modulo sur place

## 🎯 Objectif

Comprendre :
- la différence entre `a` (l'adresse) et `*a` (la valeur pointée) ;
- comment une fonction `void` peut "retourner" plusieurs résultats grâce aux pointeurs ;
- pourquoi il faut parfois sauvegarder une valeur avant de l'écraser.

---

## 📚 Prérequis

Tu dois connaître :
- l'opérateur `/` (division entière) et `%` (modulo) ;
- le déréférencement avec `*` ;
- le principe du `swap` avec une variable temporaire (`ft_swap_str` du 24/09).

---

## 📝 Énoncé

Écris une fonction qui divise les valeurs pointées par `a` et `b`.
Le résultat de la division est stocké dans l'`int` pointé par `a`.
Le reste de la division est stocké dans l'`int` pointé par `b`.

On considère que `*b` n'est jamais égal à `0`.

```c
void	ft_ultimate_div_mod(int *a, int *b);
```

Puis écris un `main` qui vérifie que `a = 42` et `b = 10` donnent `a = 4` et `b = 2`.

---

> [!tip]- Indices et Tips
> ```text
> - a est une adresse. *a est l'int qui se trouve à cette adresse. On calcule avec *a et *b, jamais avec a et b.
> - Le piège : si tu écris d'abord *a = *a / *b, la valeur de départ de *a est perdue... et le modulo sera faux !
> - Solution : sauvegarde *a dans une variable temporaire (un int) avant de modifier quoi que ce soit.
> - Dans ton main, tu crées deux int normaux et tu envoies leurs adresses : ft_ultimate_div_mod(&a, &b).
> ```

> [!check]- Correction
> ```c
> void	ft_ultimate_div_mod(int *a, int *b)
> {
> 	int	tmp;
> 
> 	tmp = *a;       // On sauvegarde la valeur de départ
> 	*a = tmp / *b;
> 	*b = tmp % *b;
> }
> ```
> ```c
> #include <stdio.h>
> 
> int	main(void)
> {
> 	int	a;
> 	int	b;
> 
> 	a = 42;
> 	b = 10;
> 	printf("Avant : a = %d, b = %d\n", a, b);
> 	ft_ultimate_div_mod(&a, &b);
> 	printf("Après : a = %d, b = %d\n", a, b); // a = 4, b = 2
> 	return (0);
> }
> ```
