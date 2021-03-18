---
title: 5 rzeczy, których nauczyłam się o testowaniu na frontendzie
tags:
  - 5 rzeczy
  - Frontend
  - Frontend testing
categories:
  - Techniczne
coverMeta: out
coverSize: partial
thumbnailImage: hero.jpg
coverImage: hero.jpg
date: 2020-10-26 20:00:00
---

Od kilku miesięcy prowadzę zajęcia dla osób, które chcą nabyć lub uzupełnić swoje front-endowe umiejętności. Jednym z zagadnień, o którym często rozmawiamy i trenujemy jest pisanie dobrych testów. Te zajęcia to dla mnie również dobra okazja, by uporządkować sobie moje doświadczenia z testowaniem i poukładać w głowie to, jak ja podchodzę do tego tematu. Czym kieruję się pisząc testy? Jakie zadaje sobie pytania? Jakie praktyki stosuje? Odpowiedzi znajdziecie w dalszej części artykułu.

<!-- more --->

## Testujemy funkcjonalność, a nie fragment kodu

Do pisania testów można podejść z nastawieniem: "Zastanówmy się jak napisać test, który przetestuje tę linijkę kodu...". Szczególnie łatwo jest wpaść w ten tok myślenia, gdy jesteśmy bardzo przywiązani do narzędzia do mierzenia pokrycia kodu testami (code coverage). Czemu takie podejście nie jest najszczęśliwsze? Rozumując w ten sposób duzo łatwiej jest nam napisać test, który będzie bardzo związany z jego obecną formą i będzie testował nieistotne detale implementacyjne. Wyprodukujemy więcej testów, code coverage wzrośnie, ale najprawdopodobniej sprawimy, ze trudniej bedzie ten kod modyfikować.

Jak inaczej mozemy zdecydować jaki test powinniśmy napisać jako kolejny? W miarę pracy nad testami wypracowałam sobie kilka pytań, które pojawiają się w mojej głowie, gdy siadam do pisania testów. W takich sytuacjach pytam siebie - "Czego oczekuję od tego fragmentu kodu?", a takze "Czego inne części systemu oczekują od tego komponentu (jaki kontrakt powinien zachowywać)?". Analizując kontrakt (np. w przypadku komponentów Reactowych - propsy, które komponent przyjmuje) - zadaję sobie pytanie - czy jest jakieś niestandardowe uzycie, o którym nie pomyślałam, a jest przez kontrakt dopuszczalne. Zadaje sobie rowniez pytanie o cel istnienia danego komponentu i upewniam się, ze sprawdzam w ramach testu czy ten cel jest realizowany. A co gdy się okaze, ze jakies linie tego kodu są nieprzetestowana? Przyglądam się im - czasem nakierowuje mnie to na jakiś aspekt funkcjonalności, o którym zapomniałam. A często zostawiam nieotestowane, bo nie są istotne.

{% image center fig-100 clear notebook.jpg  %}

<br/>
## Jeden komponent, a mnóstwo testów i mnóstwo mockowania

## Chcę zobaczyć czerwony test

Gdy piszemy testy, korzystając z TDD (test driven development), co chwila przechodzimy przez cykl: <span style="color:red">czerwony test</span> -> <span style="color: green">zielony test</span> -> **refactor**. Pozwala nam to pisać testy, które nie skupiają się na implementacji oraz tworzyć tylko tyle kodu, ile jest potrzebne do realizacji danej funkcjonalności.
Jeśli chodzi o mnie, to ja nie zawsze stosuje TDD. Często mój kod powstaje zanim go otestuje. Jednak jedną praktyką, która na stałe weszła do mojego programistycznego toolboxa jest: "Zawsze zobacz test, który jest czerwony". Jedną z pułapek, w którą możemy wpaść, gdy piszemy testy do kodu, który już istnieje, jest stworzenie wiecznie zielonego testu. Taki test na pierwszy rzut oka wygląda jakby robił swoją robotę, my jesteśmy szczęśliwi bo przechodzi, ale może się okazać, że de facto niczego nie testuje (bo np. źle go stworzyliśmy, popełniliśmy jakiś błąd). Z tego właśnie powodu lubię sprawdzać, czy gdy popsuję daną funkcjonalność, to test to wykryje i zapali się na czerwono. Jest to dla mnie jeden z

## A co z code coverage?

Mierzyć? Nie mierzyć? Wyznaczać cele odnośnie pokrycia kodu? Wedlug mnie duzo zalezy od tego, w jakim zespole jesteśmy, na jakim etapie zycia jest nasz projekt. Ja lubię wiedzieć jak wygląda sytuacja, czasem uzywam rowniez zasady, ze nie chcemy aby pokrycie znacznie spadlo (chcemy, by nowy kod byl tworzony z testami). Jednak nie lubię ustalania konkretnych celów odnosnie pokrycia testami

## Zysk vs cena testów

Jakie jest wasze podejście do testowania? Kiedy i co warto testować? Jakie praktyki stosujecie pisząc testy? Chętnie poznam Wasze punkty widzenia na ten temat. Dajcie znać w komentarzu.

** Zdjęcia autorstwa Craig Philbrick i Andrew Neel na Unsplash**
