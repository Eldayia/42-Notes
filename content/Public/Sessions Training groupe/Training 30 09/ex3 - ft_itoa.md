---
type: exercice
language: C
theme:
  - malloc
  - strings
level: 3
difficulty: intermediaire
status: ready
cssclasses:
  - teaching
---

# 🔢 Allocation dynamique — Transformer un nombre en chaîne (ft_itoa)

## 🎯 Objectif

Comprendre :
- comment calculer **à l'avance** la taille exacte à allouer ;
- comment remplir une chaîne en partant de la fin ;
- comment gérer les cas limites : `0`, les négatifs et `-2147483648`.

---

## 📚 Prérequis

Tu dois connaître :
- `malloc` et la protection de son retour ;
- `/ 10` (enlève le dernier chiffre) et `% 10` (récupère le dernier chiffre) ;
- la conversion chiffre -> caractère : `5 + '0'` donne `'5'`.

---

## 📝 Énoncé

Écris une fonction qui prend un `int` et le convertit en chaîne de caractères allouée avec `malloc`.
La fonction retourne cette nouvelle chaîne (terminée par `'\0'`), ou `NULL` si l'allocation échoue.

```c
char	*ft_itoa(int nbr);
```

Exemples : `42` -> `"42"`, `-7` -> `"-7"`, `0` -> `"0"`, `-2147483648` -> `"-2147483648"`.

---

> [!tip]- Indices et Tips
> ```text
> - Étape 1 : compter les caractères. Divise une copie du nombre par 10 jusqu'à ce qu'il vaille 0 (1 tour = 1 chiffre).
> - Ajoute 1 caractère si le nombre est négatif (pour le '-') ET 1 si le nombre vaut 0 (sinon ta boucle compte 0 chiffre).
> - Étape 2 : malloc(sizeof(char) * (len + 1)) -> +1 pour le '\0'. Protège le malloc !
> - Étape 3 : remplis de la DROITE vers la GAUCHE avec n % 10 + '0', puis n = n / 10.
> - Piège : -2147483648 ne rentre pas dans un int une fois positif (max = 2147483647).
>   Astuce : copie le nombre dans un long avant de faire n = -n.
> - Dans ton main : n'oublie pas de free() chaque chaîne retournée.
> ```

> [!check]- Correction
> ```c
> #include <stdlib.h>
> 
> char	*ft_itoa(int nbr)
> {
> 	char	*str;
> 	long	n;
> 	long	tmp;
> 	int		len;
> 
> 	n = nbr; // long : -2147483648 devient positif sans overflow
> 	// 1. Compter : 1 case pour le '-' ou pour le "0"
> 	len = (n <= 0);
> 	tmp = n;
> 	while (tmp != 0)
> 	{
> 		tmp = tmp / 10;
> 		len++;
> 	}
> 	// 2. Allouer et protéger
> 	str = (char *)malloc(sizeof(char) * (len + 1));
> 	if (str == NULL)
> 		return (NULL);
> 	str[len] = '\0';
> 	// 3. Cas particuliers
> 	if (n == 0)
> 		str[0] = '0';
> 	if (n < 0)
> 	{
> 		str[0] = '-';
> 		n = -n;
> 	}
> 	// 4. Remplir depuis la fin
> 	while (n > 0)
> 	{
> 		len--;
> 		str[len] = n % 10 + '0';
> 		n = n / 10;
> 	}
> 	return (str);
> }
> ```
> ```c
> #include <stdio.h>
> 
> int	main(void)
> {
> 	int		tests[5] = {42, -7, 0, 2147483647, -2147483648};
> 	char	*str;
> 	int		i;
> 
> 	i = 0;
> 	while (i < 5)
> 	{
> 		str = ft_itoa(tests[i]);
> 		if (str != NULL)
> 		{
> 			printf("%d -> \"%s\"\n", tests[i], str);
> 			free(str);
> 		}
> 		i++;
> 	}
> 	return (0);
> }
> ```
