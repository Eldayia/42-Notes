---
type: exercice
language: C
theme:
  - strings
  - pointers_to_pointers
  - arrays
level: 3
difficulty: intermediaire
status: ready
cssclasses:
  - teaching
---

# 📚 Pointeurs de pointeurs — Le tableau de strings

## 🎯 Objectif

Comprendre :
- comment naviguer dans un tableau contenant plusieurs chaînes de caractères ;
- l'utilisation typique d'un `char **` (comme pour le `argv` du `main`).

---

## 📚 Prérequis

Tu dois connaître :
- `ft_putstr` (pour afficher les strings) ;
- les boucles sur un tableau à deux dimensions.

---

## 📝 Énoncé

Écris une fonction qui prend un tableau de chaînes de caractères (terminé par un pointeur `NULL`) en paramètre, et qui affiche chaque chaîne suivie d'un retour à la ligne (`'\n'`).

```c
void	ft_print_strs(char **strs);
```

---

> [!tip]- Indices et Tips
> ```text
> - Un char **strs est juste un tableau où chaque case est une string (char *).
> - strs[0] est la première string, strs[1] est la deuxième, etc.
> - Au lieu de chercher un '\0' (qui marque la fin d'UNE string), ici on cherche un pointeur NULL (qui marque la fin du TABLEAU de strings).
> - N'hésite pas à recoder rapidement ton ft_putstr au-dessus de cette fonction pour pouvoir l'appeler proprement.
> ```

> [!check]- Correction
> ```c
> #include <unistd.h>
> 
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
> void	ft_print_strs(char **strs)
> {
> 	int	i;
> 
> 	i = 0;
> 	while (strs[i] != NULL)
> 	{
> 		ft_putstr(strs[i]);
> 		write(1, "\n", 1);
> 		i++;
> 	}
> }
> ```