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

# 📝 Strings — Copier de la mémoire

## 🎯 Objectif

Comprendre :
- comment modifier le contenu de la mémoire pointée par un pointeur ;
- transférer les données d'un tableau vers un autre.

---

## 📚 Prérequis

Tu dois connaître :
- l'itération de tableaux avec un index `i` ;
- l'assignation de variables (` = `).

---

## 📝 Énoncé

Écris une fonction qui copie la chaîne pointée par `src` (y compris le caractère nul de fin `'\0'`) dans le tableau pointé par `dest`.
La fonction doit retourner `dest`.

```c
char	*ft_strcpy(char *dest, char *src);
```

---

> [!tip]- Indices et Tips
> ```text
> - Tu vas utiliser un index (par exemple i) pour parcourir en même temps src et dest.
> - À chaque tour de boucle, tu dois dire : "La case i de dest prend la valeur de la case i de src".
> - Attention piège : La boucle va s'arrêter au '\0' de src. Cela veut dire que le '\0' ne sera pas copié dans dest ! Tu dois le rajouter manuellement à la fin.
> - N'oublie pas de retourner le pointeur original de dest à la fin.
> ```

> [!check]- Correction
> ```c
> char	*ft_strcpy(char *dest, char *src)
> {
> 	int	i;
> 
> 	i = 0;
> 	while (src[i] != '\0')
> 	{
> 		dest[i] = src[i];
> 		i++;
> 	}
> 	dest[i] = '\0'; // Ajout manuel du caractère de fin
> 	return (dest);
> }
> ```