---
type: exercice
language: C
theme:
  - strings
  - pointers
level: 1
difficulty: debutant
status: ready
cssclasses:
  - teaching
---

# 📏 Strings — Compter les caractères

## 🎯 Objectif

Comprendre :
- ce qu'est une chaîne de caractères en C (un tableau de `char`) ;
- l'importance du caractère nul `'\0'` (ou `0`) qui marque la fin ;
- comment parcourir un pointeur.

---

## 📚 Prérequis

Tu dois connaître :
- les variables ;
- les boucles `while` ;
- les pointeurs basiques.

---

## 📝 Énoncé

Écris un programme qui compte le nombre de caractères dans une chaîne (sans compter le `'\0'`) et qui retourne ce nombre.

```c
int	ft_strlen(char *str);
```

---

> [!tip]- Indices et Tips
> ```text
> - Un pointeur char *str pointe sur la première case de la chaîne (str[0]).
> - En C, une chaîne se termine TOUJOURS par le caractère '\0'. 
> - Tu dois créer un compteur (un int), initialisé à 0. 
> - Tant que tu n'es pas sur le '\0', tu incrémentes ton compteur pour avancer de case en case.
> - str[i] est équivalent à dire "le caractère à l'index i".
> ```

> [!check]- Correction
> ```c
> int	ft_strlen(char *str)
> {
> 	int	i;
> 
> 	i = 0;
> 	while (str[i] != '\0')
> 	{
> 		i++;
> 	}
> 	return (i);
> }
> ```
> ```c
> int main(void)
> {
> 	 char *str;
> 	 int size;
> 	 
> 	 *str = "Hello World";
> 	 size = ft_strlen(str);
> }
> ```