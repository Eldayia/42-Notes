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

# 🖨️ Strings — Afficher une chaîne

## 🎯 Objectif

Comprendre :
- comment avancer dans la mémoire ;
- comment afficher un caractère précis depuis une chaîne avec la fonction `write`.

---

## 📚 Prérequis

Tu dois connaître :
- l'exercice précédent (`ft_strlen`) ;
- la fonction `write`.

---

## 📝 Énoncé

Écris une fonction qui affiche une chaîne de caractères sur la sortie standard.

```c
void	ft_putstr(char *str);
```

---

> [!tip]- Indices et Tips
> ```text
> - N'oublie pas d'inclure <unistd.h> pour utiliser write.
> - Rappel : write(1, &caractere, 1) affiche un caractère.
> - Le & sert à donner l'adresse. Si str[i] est ton caractère, alors &str[i] est son adresse.
> - Comme pour ft_strlen, utilise une boucle while qui s'arrête lorsqu'elle rencontre le fameux '\0'.
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
> // ou while(str[i] != 0) ou while(str[i])
> ```

> [!check]- Correction compacte
> ```c
> #include <unistd.h>
> 
> void	ft_putstr(char *str)
> {
> 	int (i) = 0;
> 	while (str[i])
>		write(1, &str[i++], 1);
> }
> ```