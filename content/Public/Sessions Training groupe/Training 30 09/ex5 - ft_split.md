---
type: exercice
language: C
theme:
  - malloc
  - strings
  - pointers_to_pointers
level: 4
difficulty: avance
status: ready
cssclasses:
  - teaching
---

# ✂️ Allocation dynamique — Découper une chaîne en mots (ft_split)

## 🎯 Objectif

Comprendre :
- comment allouer un tableau de strings (`char **`) **et** chaque string qu'il contient ;
- pourquoi on compte les mots **avant** d'allouer ;
- comment terminer un tableau de strings par `NULL` ;
- comment tout libérer proprement (les mots, puis le tableau).

---

## 📚 Prérequis

Tu dois connaître :
- `ft_strdup` (copier une chaîne dans de la mémoire allouée) ;
- `ft_print_strs` (parcourir un `char **` jusqu'au `NULL`) ;
- `malloc` avec `sizeof(char *)`.

---

## 📝 Énoncé

Écris une fonction qui découpe une chaîne en mots.
Les mots sont séparés par des espaces (`' '`), des tabulations (`'\t'`) ou des retours à la ligne (`'\n'`). Plusieurs séparateurs à la suite, au début ou à la fin ne créent **pas** de mot vide.

La fonction retourne un tableau de strings alloué, dont la dernière case vaut `NULL`.

```c
char	**ft_split(char *str);
```

Exemple : `"  Hello   42\tParis \n"` -> `{"Hello", "42", "Paris", NULL}`.

---

> [!tip]- Indices et Tips
> ```text
> - Découpe le problème en petites fonctions : is_sep(c), count_words(str), dup_word(start, len).
> - count_words : saute les séparateurs, si tu n'es pas sur '\0' c'est un nouveau mot (count++), puis saute les lettres du mot. Recommence.
> - Allocation du tableau : malloc(sizeof(char *) * (nb_mots + 1)) -> +1 pour le NULL final.
>   ATTENTION : c'est sizeof(char *) (un pointeur, 8 octets) et pas sizeof(char) !
> - Pour chaque mot : repère où il commence et sa longueur, puis alloue len + 1 et copie-le (comme ft_strdup, mais avec une longueur limitée).
> - Si un malloc de mot échoue, libère les mots déjà créés et le tableau avant de retourner NULL.
> - Dans ton main : affiche chaque mot entre crochets [mot] pour voir s'il reste des espaces, puis free chaque mot, PUIS le tableau.
> - Teste les cas pièges : "", "     ", "un", "  un  ".
> ```

> [!check]- Correction
> ```c
> #include <stdlib.h>
> 
> int	is_sep(char c)
> {
> 	return (c == ' ' || c == '\t' || c == '\n');
> }
> 
> int	count_words(char *str)
> {
> 	int	count;
> 	int	i;
> 
> 	count = 0;
> 	i = 0;
> 	while (str[i] != '\0')
> 	{
> 		while (str[i] != '\0' && is_sep(str[i]))
> 			i++;
> 		if (str[i] != '\0')
> 			count++;
> 		while (str[i] != '\0' && !is_sep(str[i]))
> 			i++;
> 	}
> 	return (count);
> }
> 
> char	*dup_word(char *start, int len)
> {
> 	char	*word;
> 	int		i;
> 
> 	word = (char *)malloc(sizeof(char) * (len + 1));
> 	if (word == NULL)
> 		return (NULL);
> 	i = 0;
> 	while (i < len)
> 	{
> 		word[i] = start[i];
> 		i++;
> 	}
> 	word[i] = '\0';
> 	return (word);
> }
> 
> char	**free_all(char **tab, int w)
> {
> 	while (w > 0)
> 	{
> 		w--;
> 		free(tab[w]);
> 	}
> 	free(tab);
> 	return (NULL);
> }
> 
> char	**ft_split(char *str)
> {
> 	char	**tab;
> 	int		i;
> 	int		w;
> 	int		len;
> 
> 	// 1. Allouer le tableau : 1 case par mot + 1 pour NULL
> 	tab = (char **)malloc(sizeof(char *) * (count_words(str) + 1));
> 	if (tab == NULL)
> 		return (NULL);
> 	i = 0;
> 	w = 0;
> 	while (str[i] != '\0')
> 	{
> 		// 2. Sauter les séparateurs
> 		while (str[i] != '\0' && is_sep(str[i]))
> 			i++;
> 		// 3. Mesurer le mot
> 		len = 0;
> 		while (str[i + len] != '\0' && !is_sep(str[i + len]))
> 			len++;
> 		// 4. Copier le mot
> 		if (len > 0)
> 		{
> 			tab[w] = dup_word(&str[i], len);
> 			if (tab[w] == NULL)
> 				return (free_all(tab, w));
> 			w++;
> 			i = i + len;
> 		}
> 	}
> 	tab[w] = NULL; // 5. Fin du tableau
> 	return (tab);
> }
> ```
> ```c
> #include <stdio.h>
> 
> void	test_split(char *str)
> {
> 	char	**words;
> 	int		i;
> 
> 	words = ft_split(str);
> 	if (words == NULL)
> 		return ;
> 	printf("\"%s\" ->", str);
> 	i = 0;
> 	while (words[i] != NULL)
> 	{
> 		printf(" [%s]", words[i]);
> 		free(words[i]); // On libère chaque mot...
> 		i++;
> 	}
> 	printf(" [NULL]\n");
> 	free(words); // ... puis le tableau
> }
> 
> int	main(void)
> {
> 	test_split("  Hello   42\tParis \n");
> 	test_split("un");
> 	test_split("");
> 	test_split("     ");
> 	return (0);
> }
> ```
