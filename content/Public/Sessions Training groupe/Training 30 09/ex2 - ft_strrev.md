---
type: exercice
language: C
theme:
  - strings
  - pointers
level: 2
difficulty: debutant
status: ready
cssclasses:
  - teaching
---

# 🔁 Strings — Inverser une chaîne (ft_strrev)

## 🎯 Objectif

Comprendre :
- comment modifier une chaîne **sur place** (sans en créer une nouvelle) ;
- comment utiliser deux positions en même temps (le début et la fin) ;
- pourquoi on ne peut pas modifier une chaîne littérale (`"Bonjour"`).

---

## 📚 Prérequis

Tu dois connaître :
- `ft_strlen` ;
- l'échange de deux valeurs avec une variable temporaire.

---

## 📝 Énoncé

Écris une fonction qui inverse une chaîne de caractères **sur place** (en modifiant directement la chaîne reçue) et qui la retourne.

```c
char	*ft_strrev(char *str);
```

Exemple : `"Bonjour"` devient `"ruojnoB"`.

---

> [!tip]- Indices et Tips
> ```text
> - Commence par calculer la longueur de la chaîne (len).
> - Le dernier caractère utile est à l'index len - 1 (à len, il y a le '\0' : on n'y touche pas !).
> - Échange str[0] avec str[len - 1], puis str[1] avec str[len - 2], etc.
> - Tu dois t'arrêter au MILIEU (i < len / 2). Si tu vas jusqu'au bout, tu ré-inverses tout et tu retombes sur la chaîne de départ !
> - Piège du main : char *str = "Bonjour"; est en lecture seule -> segfault si tu la modifies.
>   Utilise un tableau : char str[] = "Bonjour";
> ```

> [!check]- Correction
> ```c
> char	*ft_strrev(char *str)
> {
> 	int		i;
> 	int		len;
> 	char	tmp;
> 
> 	len = 0;
> 	while (str[len] != '\0')
> 		len++;
> 	i = 0;
> 	while (i < len / 2)
> 	{
> 		tmp = str[i];
> 		str[i] = str[len - 1 - i];
> 		str[len - 1 - i] = tmp;
> 		i++;
> 	}
> 	return (str);
> }
> ```
> ```c
> #include <stdio.h>
> 
> int	main(void)
> {
> 	char	str1[] = "Bonjour"; // Tableau modifiable (pas char *)
> 	char	str2[] = "ab";
> 	char	str3[] = "";
> 
> 	printf("%s\n", ft_strrev(str1)); // ruojnoB
> 	printf("%s\n", ft_strrev(str2)); // ba
> 	printf("[%s]\n", ft_strrev(str3)); // []
> 	return (0);
> }
> ```
