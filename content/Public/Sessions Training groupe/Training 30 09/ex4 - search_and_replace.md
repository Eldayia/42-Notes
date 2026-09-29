---
type: exercice
language: C
theme:
  - argc_argv
  - strings
level: 2
difficulty: debutant
status: ready
cssclasses:
  - teaching
---

# 🖥️ Arguments — Rechercher et remplacer (search_and_replace)

## 🎯 Objectif

Comprendre :
- comment vérifier **le nombre** d'arguments avec `argc` ;
- comment accéder à un caractère précis d'un argument : `argv[2][0]` ;
- comment vérifier qu'un argument ne contient qu'**un seul** caractère.

---

## 📚 Prérequis

Tu dois connaître :
- l'exercice `argc & argv` du 24/09 ;
- `write` ;
- la notation `argv[i][j]` (le caractère `j` de l'argument `i`).

---

## 📝 Énoncé

Écris un **programme** qui prend 3 arguments :
1. une chaîne de caractères ;
2. une lettre à chercher ;
3. une lettre de remplacement.

Le programme affiche la chaîne en remplaçant toutes les occurrences de la 2ᵉ lettre par la 3ᵉ, suivie d'un `'\n'`.

Si le nombre d'arguments n'est pas 3, ou si le 2ᵉ ou le 3ᵉ argument n'est pas **un seul caractère**, le programme affiche seulement `'\n'`.

**Exemple attendu dans le terminal :**
```bash
$> ./search_and_replace "salut la piscine" "i" "o" | cat -e
salut la poscone$
$> ./search_and_replace "banana" "a" "u" | cat -e
bununu$
$> ./search_and_replace "banana" "z" "x" | cat -e
banana$
$> ./search_and_replace "banana" "an" "x" | cat -e
$
$> ./search_and_replace "banana" "a" | cat -e
$
```

---

> [!tip]- Indices et Tips
> ```text
> - 3 arguments + le nom du programme = argc doit valoir 4.
> - argv[2] est une string. La lettre à chercher est donc argv[2][0].
> - "Un seul caractère" veut dire : argv[2][0] n'est pas '\0' ET argv[2][1] est '\0'. Pareil pour argv[3].
> - Parcours argv[1] caractère par caractère : si c'est la lettre cherchée, affiche la lettre de remplacement, sinon affiche le caractère tel quel.
> - Le '\n' final est affiché dans TOUS les cas : mets-le en dehors du if.
> - Teste avec | cat -e pour voir le '\n' (il apparaît sous forme de $).
> ```

> [!check]- Correction
> ```c
> #include <unistd.h>
> 
> int	main(int argc, char **argv)
> {
> 	int	i;
> 
> 	// 3 arguments, et argv[2] / argv[3] font exactement 1 caractère
> 	if (argc == 4 && argv[2][0] != '\0' && argv[2][1] == '\0'
> 		&& argv[3][0] != '\0' && argv[3][1] == '\0')
> 	{
> 		i = 0;
> 		while (argv[1][i] != '\0')
> 		{
> 			if (argv[1][i] == argv[2][0])
> 				write(1, &argv[3][0], 1);
> 			else
> 				write(1, &argv[1][i], 1);
> 			i++;
> 		}
> 	}
> 	write(1, "\n", 1); // Toujours affiché
> 	return (0);
> }
> ```
