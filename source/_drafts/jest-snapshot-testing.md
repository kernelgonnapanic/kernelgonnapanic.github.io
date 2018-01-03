---
title: "Snapshot testing - a co to takiego? [Frontend testing #2]"
tags:
  - Testowanie
  - Javascript
  - Tutoriale
  - Frontend
thumbnailImagePosition: top
coverMeta: out
coverSize: partial
thumbnailImage: camera.jpg
coverImage: camera.jpg
date: 2017-10-13 07:35:00
---


<!--excerpt-->
Hej wszystkim!
Przybywam dziś z kolejnym artykułem z serii o testowaniu. Wiem, że już trochę wody w rzece upłynęło od ostatniego, ale nic straconego.

- masz aplikacje w react, angular, vue bazujaca na komponenetach
- proces
  - renderujesz do stringa
  - zapisujesz w repo
  - porównujesz, sprawdzasz czy sie zgadza
  - reviewujesz zmiany

Po co to?
- sprawdzasz jak komponent wyglada w różnych stanach
- jesli masz inline style sprawdzasz rowniez jakie style sa nalozone na poszczegolne elementy
- jesli nie sprawdzasz np. klasy

O czym musisz pamiętać?
- review snapshotów
- nie zastąpi testowania funkcjonalnego komponentów (co sie stanie po kliku i tak dalej)
