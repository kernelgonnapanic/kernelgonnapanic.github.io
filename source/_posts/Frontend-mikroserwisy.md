---
title: Frontend - a co powiecie na mikroserwisy?
tags:
  - Frontend
  - Microservices
categories:
  - Techniczne
thumbnailImagePosition: right
coverMeta: out
coverSize: partial
thumbnailImage: microservices.jpg
coverImage: microservices.jpg
date: 2017-02-12 12:06:00
---


A dziś kilka słów o temacie, który chodzi za mną już od dłuższego czasu, a dokładnie od momentu, gdy przeczytałam **"Budowanie mikrousług" Newmana**. Naszą dzisiejszą podróż z mikroserwisami w frontendzie zaczniemy od ...
<!-- more-->

### Historii pewnego start-upu

Załóżmy, że mamy start-up, mamy aplikację, mamy zespół developerski. Zespół pracuje nad aplikacją, dowozi sprinty, aplikacja sobie rośnie. Dodatkowo okazuje się, że produkt, który tworzymy, podoba się użytkownikom. Pojawiają się nowe feature'y, pojawiają się też nowi ludzie w zespole.

Aplikacja rośnie jeszcze bardziej, aż do momentu gdy tworzy ją kilkudziesięciu developerów. No i zaczyna się problem.

Niepostrzeżenie pojawiają się kłopoty. Managerowie muszą uporać się z zarządzaniem taką ilością osób, z ustalaniem priorytetów, z koordynowaniem zmian wprowadzanych przez nie. Z każdym releasem jesteśmy zobowiązani przeprowadzać testy regresyjne dla całego systemu, bo nigdy nie możemy być pewni czy nasz kod, nie będzie miał dziwnych side-effectów w zupełnie innej części aplikacji. Jesteśmy zablokowani w kwestii technologii, bo cały nasz ogromny codebase z niej korzysta. Developerzy blokują się nawzajem, ich zmiany stale na siebie nachodzą, bo konteksty w aplikacji nie są dobrze oddzielone. Zaczynamy być coraz wolniejsi...

### A może tak skala micro?

Może jednak jest już jakieś rozwiązanie na te problemy, co? Okazuje się, że nie tak odlegli nam (mam nadzieję) backendowcy już sobie takowe rozwiązanie obmyślili. Odpowiedzią na te zagwozdki mają być **MIKROSERWISY**.

Co to takiego?

W tej koncepcji, zamiast tworzyć jeden, wielki, skomplikowany system, który jest w stanie obsłużyć wszystkie nasze wymagania biznesowe tworzymy szereg małych serwisów, które robią dobrze jedną rzecz, komunikują się i współpracują, by te wymagania spełnić.

Za każdą z takich małych aplikacji stoi zespół, który opiekuje się nią w całym cyklu software developmentu, czyli od powstania wymagań (np. historyjek użytkownika) aż do wdrożenia jej na produkcję. Ma on dużą swobodę w wyborze technologii, pod warunkiem, że dostarcza interfejs w postaci, której oczekują od niego inne systemy.

Mała aplikacyjka jest niezależna w kontekście technologii, w kontekście releasów, opiekuje się powierzonym jej ograniczonym kontekstem (w myśl domain driven design). A programiści mogą w efektywny sposób dostarczać część systemu, za którą są odpowiedzialni.

### A jak to wygląda w rzeczywistości?

W realu wiele systemów skierowała się w tę stronę. Oczywiście nie jest to silver bullet, który sam z siebie naprawia wszystkie problemy pierwszego świata. Jednak w połączeniu ze zwinną organizacją zespołów, sensownie ustawionymi procesami w organizacji i odpowiednią infrastrukturą potrafi wiele zdziałać.

### Ale co z frontem?

No właśnie. I tu jest pewien problem. Cała ta mikroserwisowa burza ominęła aplikacje frontendowe. I myślę, że w dużej mierze spowodowane jest to specyfiką środowiska, jakim jest przeglądarka. Ale przyjrzymy się temu zjawisku bliżej.

Jest wiele pomysłów na to, jak wdrożyć idee, które stoją za koncepcją mikroserwisów w świat frontendu. Żaden z nich nie przyjął się jednak na tyle, by móc stwierdzić, że jest to "way-to-go".

Dziś chciałabym przyjrzeć się dwóm z tych pomysłów, resztę zostawimy sobie na następny raz ;)

### Kilka aplikacji

Zacznijmy od idei, który na pierwszy rzut oka wydaje się całkiem sensowna. Skoro nasza aplikacja jest już bardzo duża, może podzielmy ją na kilka mniejszych?

W ten sposób uzyskamy kilka niezależnych aplikacji SPA, które z punktu widzenia użytkownika tworzą jednak jeden produkt.

Z plusów, które posiada takie rozwiązanie możemy wymienić:
- zespoły pracujące nad poszczególnymi aplikacjami mogą releasować swój kod niezależnie,
- są również niezależne pod kątem technologii (innym pytaniem jest to czy zawsze powinny z tego korzystać),
- uzyskujemy oddzielenie kontekstów, ale nie zawsze tak drobnoziarniste, jakbyśmy tego oczekiwali.

Jednak są też minusy takiego rozwiązania:
- performance,
- potencjalne ryzyko duplikacji kodu,
- techniczne problemy z komunikacją między aplikacjami (najczęściej poprzez url),
- trudności w komunikacji między zespołami mogą powodować, że z punktu widzenia użytkownika końcowego produkt okazuje się niespójny.

### Pakiety NPM

Do problemu można też podejść od innej strony. Zamiast dzielić produkt na kilka aplikacji, możemy wyodrębnić z naszej bazy kodu te części, które zarządzają konkretnymi funkcjonalnościami i używać ich jako biblioteki. W ten sposób nasza aplikacja ma wiele wersjonowanych zależności, które są publikowane np. w ramach naszego prywatnego NPMa.

Jakie są plusy takiego rozwiązania?
+ zdecydowanie uzyskujemy separację kontekstów (każdy moduł jest testowalny niezależnie, określa pewien interfejs, za pomocą którego współpracuje z innymi częściami systemu),
+ takie moduły mogą być tworzone przez niezależne zespoły.

A jakie wady?
- zazwyczaj konieczność utrzymywania wielu wersji modułu na raz (nie wszyscy klienci zaczynają od razu używać nowej wersji biblioteki),
- konieczne jest prowadzenie prawdziwego, porządnego sem-ver'a, by dobrze komunikować klientom zaistnienie zmian, które zmieniają dotychczasowy kontrakt,
- mamy nadal do czynienia z główną aplikacją, która tylko korzysta z pomocniczych bibliotek,
- biblioteki takie są zależnościami build-time, tzn. że aby funkcjonalność zaimplementowana w ramach takiej biblioteki została doręczona do użytkownika, musimy zazwyczaj wypuścić nową wersję naszej biblioteki, a następnie wyreleasować aplikację, która z niej korzysta. Ten dodatkowy krok powoduje, że zespół stojący za rozwojem danej biblioteki nie jest do końca niezależny oraz znacząco wydłuża czas oczekiwania na pewne funkcjonalności (w szczególności, gdy proces releasowania aplikacji jest bardzo wolny i kosztowny).

Wystarczy już na dziś tych rozważań. W kolejnej części zmierzymy się z dalszymi pomysłami na implementację mikroserwisów we frontendowym świecie. Porozmawiamy m.in o web componentach, iframe'ach i layout service'ach takich jak Taylor.

Podzielcie się koniecznie waszą opinią i doświadczeniami z korzystania z takich rozwiązań. Jestem bardzo ciekawa!

Ania
