---
title: 5 rzeczy których nie wiecie o JavaScript
tags:
  - Frontend
  - JavaScript
  - 5 rzeczy
categories:
  - Techniczne
thumbnailImagePosition: right
coverMeta: out
coverSize: partial
thumbnailImage: 5rzeczy2.jpg
coverImage: 5rzeczy2.jpg
date: 2018-12-18 11:53:00
---

Wspomnienie o JavaScript w mieszanym (pod względem używanego języka) środowisku programistycznym zazwyczaj powoduje duże poruszenie. Wielu programistów nienawidzi lub śmieje się z JSa, lecz część go uwielbia. Mi bliżej do drugiej kategorii. Podejrzewam, że gdyby nie JS, to pewnie nie zostałabym programistką. Używam go do tworzenia aplikacji webowych i mobilnych, od dawna planuje również pobawić się więcej Node.js. Dziś chciałabym Wam przedstawić kilka ciekawostek na temat tego języka, o których mogliście jeszcze nie słyszeć.
<!--more-->

Starałam się zebrać ciekawe informacje, dziwności oraz fakty, które mnie zaskoczyły. Parzcie kawę i zaczynamy!

## 1. 6 znaków

Okazuje się, że używając JavaScriptu jesteśmy w stanie zapisać dowolny fragment kodu używając tylko 6 (sic!) znaków. Wyobraź sobie, że każdy z twoich produkcyjnych skryptów można przekształcić w dużą, naprawdę ogromną, ilość nawiasów, wykrzykników i plusów, a jego działanie pozostanie takie samo.
Narzędziem, które konwertuje dowolny kod do 6 znaków i które nosi adekwatną, bądź co bądź, nazwę możecie się pobawić tutaj -> [JSFuck](http://www.jsfuck.com/).

{% image center fig-100 clear numbers.png  %}

Przekształcenia, które są przez tę stronę wykonywane bazują na różnych dziwactwach JSa (możecie je znaleźć w [tym](https://github.com/aemkei/jsfuck/blob/master/jsfuck.js) miejscu). Czy wiedzieliście na przykład, że dodanie do siebie dwóch pustych tablic daje w rezultacie stringa?
PS Nie dziwię się czemu ludzie żartują z JSa.

## 2. Zbudujmy lepszy JavaScript

Pewnie często słyszycie, że jakaś nowa funkcjonalność JavaScriptu jest w "stage 2" czy "stage 3". Poszczególne poziomy mówią o tym, jak bardzo zaawansowane są prace nad nią i jak bardzo jesteśmy pewni, że wejdzie ona do języka właśnie w takiej formie. Ale czy wiedzieliście, że na Githubie istnieje [repozytorium](https://github.com/tc39/proposals), gdzie możemy przeglądać wszystkie propozycje, począwszy od stage 1? Oprócz przejrzenia samych proposali zachęcam do głębszego pogrzebania w tym repo. Można tam znaleźć np. [minutki](http://tc39.github.io/tc39-notes/) ze spotkań komitetu TC39, który zajmuje się standardem języka JavaScript.
{% image center fig-100 clear proposals.png  %}


## 3. Pobawmy się nazwami zmiennych!

Specyfikacja języka JavaScript nakłada pewne zasady dotyczące tego, jak możemy nazywać zmienne. I pewnie większość z Was wie o tym, że muszą się one zaczynać od litery, mogą zawierać liczby, podkreślnik czy znak dolara i że nie możemy używać słów kluczowych języka jako identyfikatorów. Ale czy na pewno jest to takie proste? Mieliście kiedyś szansę przyjrzeć się bliżej tym regułom? Rezultatem moich wczorajszych poszukiwań i prób jest poniższa lista. Okazuje się, że tak naprawdę mamy do wyboru wiele znaków pochodzących z różnych języków (hebrajski, arabski, tamilski, greka). 
W ten sposób nasze zmienne nigdy już nie będą nudne (oczywiście nie polecam tego typu działań na kodzie produkcyjnym 😉).
```
const நன்றி = "thank you";
const ꜛꜛꜛꜛ = -42;
const ꜜꜜꜜꜜ = 42;
const π = 3.14;
const a𝟘𝟙𝟚𝟛 = "a0123";
const a𝟬𝟭𝟮𝟯 = "a0123";
const <﹏ಠ﹏ಠ﹏> = "nah";
```
Na [tej](https://mothereff.in/js-variables) stronie możecie poeksperymentować samemu, a znajdująca się w [tym](https://stackoverflow.com/questions/1661197/what-characters-are-valid-for-javascript-variable-names) wątku lista może Wam pomóc w odnalezieniu ciekawych znaków.

## 4. A co z nazwami właściwości obiektów?

Bawiliśmy się już nazywaniem zmiennych, teraz zobaczmy co będzie się działo przy nazywaniu właściwości obiektu. Z pomocą przychodzi nam kolejna [strona](https://mothereff.in/js-properties). 

Załóżmy, że tworzymy obiekt o takiej strukturze:
```js
const a = {
  123e123: 42
};
```
Jak myślicie, jak możemy się odwołać do właściwości, która przechowuje liczbę 42? 
```js
a['1.23e+125'] // 42
```
Okazuje się, że chcąc lub niekoniecznie, utworzyliśmy nazwę właściwości, która jest liczbą zapisaną w notacji wykładniczej. I teraz żeby ją odczytać również musimy zastosować notację wykładniczą, lecz w ustandaryzowanej wersji `1.23e+125`, z przecinkiem po pierwszej cyfrze znaczącej.

Ciekawiej robi się, gdy nasza liczba przestaje się mieścić w zakresie. Dla przykładu, do takiej własności musimy się odwołać przez:
```js
const b = {
  123e9999999: 42
};

b['Infinity'] // 42
```
Oczywiście wszystko jest spowodowane faktem, że dla JSa nazwy tych właściwości są liczbami. Jeśli chcemy, żeby te ciągi zostały potraktowane jako stringi, wystarczy dodać apostrofy. 

## 5. Node i Deno

Czy wiedzieliście, że twórca Node'a - Ryan Dahl - tworzy nowe środowisko uruchomieniowe dla JavaScriptu? Mimo tego, że Node jest obecnie bardzo popularny i często używany, Ryan zauważa w jego architekturze skutki wielu źle podjętych decyzji. Nauczony doświadczeniami tworzy nową platformę - Deno, która ma inaczej rozwiązywać zależności, uruchamiać kod w sandbox z ograniczonymi prawami dostępu do dysku i sieci, no i zawierać wsparcie dla TypeScripta out-of-the-box. Jeśli chcecie posłuchać więcej o tym, co konretnie Ryan Dahl uważa za swoje błędy przy projektowaniu Node'a i jak Deno wychodzi im na przeciw, gorąco zachęcam do obejrzenia!
<br/>
{% youtube M3BM9TB-8yA %}

Jeśli miałabym powiedzieć, który punkt mnie najbardziej zaskoczył to chyba czwóreczka. O wielu quirkach JSa wiedziałam, ale o tym nie miałam pojęcia. Jednak po przemyśleniu, jest to całkiem logiczne zachowanie. 

A co dla Was jest najbardziej zaskakujące/ciekawe?

Ania


*Photo by Toa Heftiba on Unsplash*

