---

A resposta rápida para esta questão é: hash tables.

Com hash tables você consegue através de uma chave agrupar qualquer tipo de informação. No caso de caracteres repetidos em uma string a chave é o próprio caractere. Os passos para conseguir isso são os seguintes:

 - Declare um map entre char e int (como contador);
 - Faça um loop caractere por caractere da string;
 - Incremente o contador para cada caractere que passar;
 - O contador está pronto, imprima o map.

Em C++ um código que faz isso seria como o abaixo:

```
void MatchingCharacters(string s)
{
    map<char, int> m; // declarar um map entre char e int
    for_each(s.begin(), s.end(), [&m](char c) { m[c] += 1; }); // loop caractere a caractere incrementando contador para cada um
    for( auto c: m ) {
      cout << c.first << ": " << c.second << "\n";
    }
}
```

---
categories: []
date: 2019-07-10 00:08:25-03:00
tags: null
title: Como Publicar Seu Blog Em Hugo Para Ebook
