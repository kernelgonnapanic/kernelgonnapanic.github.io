---
title: React w 300 słowach
tags:
  - Frontend
  - React
  - Rekrutacja
  - Pierwsza praca w IT
thumbnailImagePosition: right
coverMeta: out
coverSize: partial
thumbnailImage: react.jpg
coverImage: react.jpg
date: 2019-01-25 16:00:00
---

Jestem właśnie na etapie poszukiwania pracy. I jak się okazuje rozmowy, które prowadzę, mogą być świetną inspiracją dla moich blogowych poczynań. Jedno z pytań, które zostały mi zadane w trakcie rekrutacji, brzmiało: “Czy mogłabyś w kilku zdaniach opowiedzieć czym jest React, do czego służy i jak działa?

<!-- more -->

Pierwsza myśl: whoa... jak tu teraz zebrać wszystko co wiem o tym frameworku, wyciągnąć z tego to, co najistotniejsze i przedstawić tak, by miało to ręce i nogi?

Druga myśl: “Dawaj Andzia” 💪

Myśl trzecia i ostateczna, która przyszła mi do głowy już po zakończeniu rozmowy kwalifikacyjnej: "Kurczę, to jest całkiem fajne pytanie rekrutacyjne". Aby móc w zwięzły sposób przedstawić ideę, trzeba ją dobrze rozumieć, wiedzieć co jest najistotniejsze, a bez czego można się obyć. Zadając takie pytanie możemy, oprócz zrozumienia tematu, sprawdzić w jaki sposób dana osoba mówi o technikaliach, czy umie sformułować i przekazać swoją wiedzę komuś innemu w przejrzysty sposób 💡.

Dlatego dziś, po raz drugi, podejmę się tego niełatwego zadania i postaram się upchnąć najważniejsze informacje o React w 300 słów. 300 słów to nie za mało, nie za dużo - tak w sam raz. Ocenę tego, jak mi poszło, pozostawiam Wam.

To jak? Lecimy?

## 300 słów i ... start!

**React** jest biblioteką pozwalającą na zarządzanie interfejsem użytkownika (UI) w aplikacji frontendowej. Jego cechą charakterystyczną jest to, że robi to w sposób deklaratywny (czyli poprzez zdefiniowanie efektu końcowego, a nie serii akcji np. dodaj/usuń element DOM).

### Komponenty

Głównym budulcem aplikacji w React są **komponenty**, dzięki którym możemy podzielić aplikację na małe, reużywalne części. Elementy te tworzymy przy użyciu klas zawierających metodę `render` lub zwykłych funkcji. Każdy z nich zawiera definicję części widoku, która jest najcześciej opisana przy użyciu JSX - rozszerzenia składni JS przypominającego HTMLa. W ramach JSX możemy korzystać z innych istniejących komponentów, tworząc w ten sposób strukturę drzewa.

Tworząc komponenty możemy również chcieć wykonać pewne operacje w konkretnych momentach ich "życia", np.&nbsp;po tym gdy zostały umieszczone w drzewie DOM lub gdy zostały uaktualnione po zmianie danych itp.

### State i props

Komponenty mogą również przechowywać i zarządzać stanem (state) oraz otrzymywać informacje od innych komponentów, przez które są używane (props). Zmiana stanu lub props uruchamia ponowne wyrenderowanie się komponentu tak, by odzwierciedlić zaistniałe zmiany na ekranie użytkownika. Eventy np.&nbsp;kliknięcie na element, obsługiwane są podobnie jak zdarzenia pochodzące z elementów DOM, z tą różnicą, że jako event handler zgłaszamy funkcję lub metodę naszej klasy, a nie stringa.

### VirtualDOM

React korzysta z mechanizmu VirtualDOM, dzięki któremu tylko niezbędne zmiany są nakładane na DOM (jest to ważne z&nbsp;punktu widzenia wydajności aplikacji, ponieważ wiele modyfikacji drzewa DOM może spowodować jej znaczący spadek). By to osiągnąć, framework utrzymuje pośrednią reprezentację drzewa, w&nbsp;postaci JavaScriptowych obiektów. Gdy następuje jakaś zmiana (stanu lub propsów), tworzy on nową reprezentację, a następnie porównuje ją ze starą. Identyfikowane są konieczne zmiany i tylko one są aplikowane na drzewo DOM.

Uff... Jest ciężko. Zostało tylko 30 słów. Zamiast jednak wykorzystać je sama, postanowiałm zostawić je Wam.
Co ważnego dodalibyście do tego opisu?

Do następnego!
Ania

_Photo by Pop & Zebra on Unsplash_
