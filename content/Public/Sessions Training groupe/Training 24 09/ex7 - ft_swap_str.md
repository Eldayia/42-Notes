---
type: exercice
language: C
theme:
  - pointers_to_pointers
level: 3
difficulty: intermediaire
status: ready
cssclasses:
  - teaching
---

# 🔄 Pointeurs de pointeurs — Inverser deux strings

## 🎯 Objectif

Comprendre :
- ce qu'est un pointeur de pointeur (`char **`) ;
- comment modifier une variable qui est **déjà** un pointeur (`char *`).

---

## 📚 Prérequis

Tu dois connaître :
- le principe de l'échange (le fameux `swap` avec une variable temporaire) ;
- le déréférencement avec `*`.

---

## 📝 Énoncé

Écris une fonction qui échange le contenu de deux pointeurs sur des chaînes de caractères.
L'adresse contenue dans `a` doit aller dans `b`, et inversement.

```c
void	ft_swap_str(char **a, char **b);
```

---

> [!tip]- Indices et Tips
> ```text
> - Si tu veux modifier un int, tu envoies à ta fonction un int *. 
> - Logiquement, si tu veux modifier un char * (pour qu'il pointe sur une autre chaîne), tu dois envoyer à ta fonction un char ** !
> - Déclare une variable temporaire du même type que ce que tu veux échanger (ici, un char *).
> - Utilise l'opérateur * devant tes arguments pour accéder aux char * qu'ils contiennent (*a = le premier char *, *b = le second).
> ```

> [!check]- Correction
> ```c
> void	ft_swap_str(char **a, char **b)
> {
> 	char	*tmp;
> 
> 	tmp = *a;
> 	*a = *b;
> 	*b = tmp;
> }
> ```
> ```c
> #include <stdio.h> 
> int main(void) 
> { 
> 	char *str1 = "Bonjour"; 
> 	char *str2 = "Au revoir"; 
> 	printf("Avant : str1 = %s, str2 = %s\n", str1, str2); 
> 	// On passe les adresses de str1 et str2 (&) 
> 	ft_swap_str(&str1, &str2); 
> 	printf("Après : str1 = %s, str2 = %s\n", str1, str2); 
> 	return (0); 
> }
> ```