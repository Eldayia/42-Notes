---
type: exercice
language: C
theme:
  - malloc
  - strings
level: 2
difficulty: intermediaire
status: ready
cssclasses:
  - teaching
---

# 🧠 Allocation dynamique — Dupliquer une chaîne (ft_strdup)

## 🎯 Objectif

Comprendre :
- pourquoi on utilise `malloc` (pour qu'une variable survive à la fin de la fonction) ;
- comment calculer la taille mémoire nécessaire pour une string ;
- comment "protéger" un `malloc` en vérifiant son retour.

---

## 📚 Prérequis

Tu dois connaître :
- `malloc` et la librairie `<stdlib.h>` ;
- `sizeof` ;
- compter les caractères d'une chaîne (comme `ft_strlen`).

---

## 📝 Énoncé

La fonction `ft_strdup` (string duplicate) permet de créer une copie exacte d'une chaîne de caractères. 
Mais contrairement à ton `ft_strcpy` d'avant, la destination n'existe pas encore ! Tu dois demander au système d'exploitation de te donner de la mémoire avec `malloc`.

Écris la fonction `ft_strdup` qui alloue suffisamment de mémoire, copie la chaîne `src` dedans, et retourne le pointeur vers cette nouvelle chaîne.

```c
char	*ft_strdup(char *src);
```

---

> [!tip]- Indices et Tips
> ```text
> - Tu vas devoir compter la taille de 'src' pour savoir combien d'octets demander à malloc.
> - N'oublie pas : une chaîne a besoin d'une case de plus pour stocker le '\0' de fin ! La taille à allouer est donc (longueur + 1) * sizeof(char).
> - Si malloc échoue (par exemple, plus de mémoire sur l'ordinateur), il retourne NULL. Tu dois TOUJOURS vérifier si le pointeur retourné par malloc est NULL et retourner NULL si c'est le cas.
> - Une fois la mémoire allouée et protégée, c'est comme un ft_strcpy classique.
> ```

> [!check]- Correction
> ```c
> #include <stdlib.h>
> 
> char	*ft_strdup(char *src)
> {
> 	char	*dest;
> 	int		i;
> 	int		len;
> 
> 	// 1. Calculer la longueur de src
> 	len = 0;
> 	while (src[len] != '\0')
> 		len++;
> 
> 	// 2. Allouer la mémoire (longueur + 1 pour le '\0')
> 	dest = (char *)malloc(sizeof(char) * (len + 1));
> 	
> 	// 3. Protéger le malloc
> 	if (dest == NULL)
> 		return (NULL);
> 
> 	// 4. Copier la chaîne
> 	i = 0;
> 	while (src[i] != '\0')
> 	{
> 		dest[i] = src[i];
> 		i++;
> 	}
> 	dest[i] = '\0';
> 	
> 	// 5. Retourner la nouvelle chaîne
> 	return (dest);
> }
> ```