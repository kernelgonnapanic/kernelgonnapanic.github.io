---
title: "Identity & Data Security for Web Development"
tags:
  - Recenzje
  - Security
categories:
  - Techniczne
thumbnailImagePosition: right
thumbnailImage: security.jpg
coverMeta: out
coverSize: partial
coverImage: security.jpg
date: 2017-06-8 09:38:04
---

Piękne Zakopane przywitało mnie słońcem, lecz cudna pogoda trwała tylko dzień. Dzisiejszy deszcz ma jednak swoją dobrą stronę. Mam chwilę, by podzielić się z Wami moimi przemyśleniami odnośnie książki **"Identity & Data Security for Web Development"** autorstwa Jonathana LeBlanc i Tima Messerschmidta. <!--more-->Jest to część serii wydawnictwa o'Reilly skierowanej do web developerów, którą można rozpoznać po zielonym (właściwie morskim) kolorze okładek.

Kupując tę książkę, miałam co do niej spore oczekiwania. Wiedzy w temacie bezpieczeństwa stron internetowych nigdy za wiele. Czuję również, że moja znajomość tego tematu nie jest zbyt obszerna. Dodatkowo, porusza ona temat identyfikacji użytkownika w Internecie, co miało mi się przydać do projektu, który przygotowywałam na studiach. To wszystko sprawiło, że zdecydowałam się na zakup "Identity & Data Security for Web Development".

Niestety solidnie się zawiodłam.

Książka porusza dwa główne tematy - identyfikację i autoryzację użytkownika w Internecie oraz bezpieczeństwo aplikacji webowych. Zawiera sporo frgamentów kodu, napisanych w Node (za to plus), które mają za zadanie pokazać teoretyczne koncepty w praktyce. Autorzy zaczynają od wprowadzenia tematu bezpieczeństwa pokazując, że to człowiek jest najsłabszym ogniwem całego mechanizmu. Poźniej poruszają tematy haszowania haseł, różnych sposobów identyfikacji użytkownika, mechanizmów OAuth 2 i OpenID Connect. Mówią też o najbardziej popularnych atakach - XSS oraz CSRF i sposobach na zabezpieczenie się przed nimi. Na deser dostajemy jeszcze rozdział na temat protokołu SSL/TLS oraz symetrycznej i asymetrycznej kryptografii.

I jak tak teraz opisuje te tematy, czy też w momencie gdy czytałam spis treści tej książki, wydają mi się one bardzo ciekawe. Z chęcią dowiedziałabym się o nich więcej. Niestety przeczytana książka w małym stopniu przyczyniła się do zaspokojenia mojego pragnienia wiedzy.

W szczególności interesuje mnie temat OAutha i OpenID Connect - technologii powszechnie używanych w dzisiejszych czasach do przeprowadzenia procesu autentykacji i autoryzacji. Zdecydowanie za mało na ten temat wiem. Niestety suchy, książkowy wywód i duże fragmenty kodu nie przekazały istoty problemu, które te technologie rozwiązują. Nie dowiedziałam się również nic na temat motywacji, które stoją za tym, że proces autoryzacji za pomocą OAuth'a wygląda tak, a nie inaczej. Dużo bardziej cenię sobie książki, które zamiast gotowych rozwiązań kształtują w Tobie intuicję.

Podobnie było z tematem XSSów i innych ataków. Dowiedziałam się jakich pakietów npmowych użyć, by dostać (niejako w gratisie) zabezpieczenie przed nimi. Zabrakło mi jednak lepszego wyjaśnienia problemów, z którymi mierzymy się na co dzień i jakie zagrożenie stwarzają dla nas i naszych użytkowników.

Ogólnie, miałam nadzieję, że będę mogła polecić tę książkę, ale niestety nie mogę.  Zbyt duże skupienie na szczegółach implementacyjnych sprawiło, że w wielu miejsca autorom umknęła istota problemu. Szczególnie odradzam początkującym, którzy mają minimalną lub żadną wiedzę w temacie web security - zagłębianie się w treści tej książki może wywołać tylko większy mętlik w głowie. Jeśli jednak chcesz wiedzieć jakich narzędzi użyć korzystając ze stack'a Node + Express i masz już całkiem ugruntowaną wiedzę teoretyczną na te tematy - wtedy śmiało sięgaj. To jest coś czego tej książce odmówić nie można.

A Wy co ciekawego ostatnio przeczytaliście/czytacie? Powoli zbieram się do posta o programistycznych must-read. Liczę na Wasze sugestie w tym temacie!
