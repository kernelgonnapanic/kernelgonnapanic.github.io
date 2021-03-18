---
title: Jaka jest różnica między var, const i let?
tags:
  - Nauka programowania
  -
categories:
  - Techniczne
thumbnailImagePosition: top
coverMeta: out
coverSize: partial
thumbnailImage: hero.jpg
coverImage: hero.jpg
date: 2020-09-30 16:00
---

|                     |    var    |   let   | const |
| :-----------------: | :-------: | :-----: | :---: |
|       zakres        | funkcyjny | blokowy |       |
| ponowne przypisanie |    tak    |   tak   |  nie  |
|    wprowadzenie     |  JS 1.0   |   ES6   |  ES6  |

## Zakres

## Ponowne przypisanie

- nie pozwala na ponowne przypisanie, arrayki

## Podsumowanie

- w aplikacjach korzystających z ES6 -> const, chyba ze mutowanie - let, var raczej nie stosowane
- var - w aplikacjach bez transpilacji, które muszą wspierać starsze przeglądarki

**Zdjęcie od ThisisEngineering RAEng z Unsplash**
