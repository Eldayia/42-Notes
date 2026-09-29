---
type: exercice
language: C
theme:
  - strings
level: 2
difficulty: intermediaire
status: ready
cssclasses:
  - teaching
---

# 🔣 Strings — Transformer une chaîne en nombre (ft_atoi)

## 🎯 Objectif

Comprendre :
- comment convertir un caractère chiffre en valeur : `'7' - '0'` donne `7` ;
- comment construire un nombre chiffre par chiffre (`result * 10 + chiffre`) ;
- comment parcourir une chaîne en plusieurs étapes (espaces, signe, chiffres).

---

## 📚 Prérequis

Tu dois connaître :
- le parcours d'une chaîne avec un index `i` ;
- la table ASCII (les chiffres `'0'` à `'9'` se suivent) ;
- `ft_itoa` (l'opération inverse, exercice précédent).

---

## 📝 Énoncé

Écris une fonction qui convertit le début de la chaîne pointée par `str` en `int` et le retourne, comme la fonction `atoi` de la librairie standard (`man 3 atoi`).

La chaîne peut commencer par des espaces blancs (`' '`, `'\t'`, `'\n'`, `'\v'`, `'\f'`, `'\r'`), suivis d'**un** signe optionnel `'+'` ou `'-'`, suivi de chiffres. La conversion s'arrête au premier caractère qui n'est pas un chiffre.

```c
int	ft_atoi(const char *str);
```

Exemples : `"42"` -> `42`, `"   -123abc"` -> `-123`, `"+7"` -> `7`, `"abc"` -> `0`, `"--5"` -> `0`.

---

> [!tip]- Indices et Tips
> ```text
> - Découpe en 3 boucles/étapes : 1) sauter les espaces blancs, 2) lire UN signe, 3) lire les chiffres.
> - Espaces blancs : ' ' ou de '\t' (9) à '\r' (13) -> (c == ' ' || (c >= 9 && c <= 13)).
> - Garde le signe dans une variable (sign = 1, et sign = -1 si tu vois un '-').
> - Pour chaque chiffre : result = result * 10 + (str[i] - '0'). Ex : "42" -> 0*10+4 = 4 -> 4*10+2 = 42.
> - Retourne result * sign à la fin.
> - Dès que tu tombes sur autre chose qu'un chiffre, tu t'arrêtes : "12a34" donne 12.
> - Attention : dans la version de la piscine (C04), il peut y avoir PLUSIEURS signes ("---5" = -5, on compte les '-').
>   Lis bien le sujet le jour de l'exam pour savoir quelle version est demandée !
> - Dans ton main : compare ton résultat avec le vrai atoi (#include <stdlib.h>) sur les mêmes chaînes.
> ```

> [!check]- Correction
> ```c
> int	ft_atoi(const char *str)
> {
> 	int	i;
> 	int	sign;
> 	int	result;
> 
> 	i = 0;
> 	// 1. Sauter les espaces blancs
> 	while (str[i] == ' ' || (str[i] >= '\t' && str[i] <= '\r'))
> 		i++;
> 	// 2. Lire un signe (un seul)
> 	sign = 1;
> 	if (str[i] == '-' || str[i] == '+')
> 	{
> 		if (str[i] == '-')
> 			sign = -1;
> 		i++;
> 	}
> 	// 3. Construire le nombre chiffre par chiffre
> 	result = 0;
> 	while (str[i] >= '0' && str[i] <= '9')
> 	{
> 		result = result * 10 + (str[i] - '0');
> 		i++;
> 	}
> 	return (result * sign);
> }
> ```
> ```c
> #include <stdio.h>
> #include <stdlib.h>
> 
> int	main(void)
> {
> 	char	*tests[8] = {"42", "   -123abc", "+7", "abc", "--5",
> 		"\t\n 0012", "12a34", ""};
> 	int		i;
> 
> 	i = 0;
> 	while (i < 8)
> 	{
> 		// On compare avec le vrai atoi
> 		printf("\"%s\" -> ft_atoi = %d | atoi = %d\n",
> 			tests[i], ft_atoi(tests[i]), atoi(tests[i]));
> 		i++;
> 	}
> 	return (0);
> }
> ```
