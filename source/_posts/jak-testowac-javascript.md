---
title: "Javascript - to test or not to test? [Frontend testing #1]"
tags:
  - Testowanie
  - Javascript
  - Tutoriale
  - Frontend
thumbnailImagePosition: right
coverMeta: out
coverSize: partial
thumbnailImage: jak-testowac.jpg
coverImage: jak-testowac.jpg
date: 2017-07-29 15:12:00
---
"Testy, hmmm... testy... Ja przepraszam bardzo, ale czy ktoś je kiedykolwiek widział we frontendowym repozytorium? Ja rozumiem że na backendzie, ale żeby na frontendzie? No chyba się tym programistom w głowach poprzewracało i za dużo czasu mają"

Czyżby?
<!--more-->

Hej wszystkim!
Tematem mojej dzisiejszej pogawędki będzie testowanie. A właściwie będzie to wstęp do dłuższej dyskusji, która (mam nadzieję) będzie się toczyć na blogu, w postaci serii postów. (Trzymajcie kciuki za mój zapał).

Zanim jednak zaczniemy rozważać konkretne narzędzia, techniki, ich plusy i minusy, zacznijmy od zadania sobie ważnego pytania - po co to komu?
Sceptyków (jak ten ze wstępu) znajdziemy w najszej branży trochę. "Nie mam czasu na pisanie testów", "To za dużo wysiłku", "Jaki ja mam z tego zysk?". Spróbujmy dziś rozprawić się z choć częścią tych wymówek.

# Frontend nie potrzebuje testów
Ja wiem, wiem. My, frontendowcy, nie powinniśmy się nawet nazywać programistami, skoro robimy sobie stronki w htmlu. A tak na poważnie, zdajemy sobie sprawę z tego, że frontend to obecnie zazwyczaj pokaźnych rozmiarów i całkiem skomplikowana aplikacja. I w kontekście testów nie różni się w żaden sposób od backendu. Mamy kod, chcemy się upewnić czy działa on poprawnie, czyli tak, jak tego oczekujemy. I nie ma tu znaczenia, czy jest uruchamiany na serwerze, w przeglądarce czy na urządzeniu mobilnym jako natywna aplikacja.

# Nie mam czasu na pisanie testów
Jeśli nie masz czasu na pisania testów, wtedy z pewnością będziesz musiał znaleźć go na naprawianie bugów.
Czasem mam wrażenie, że wymówka "brakiem czasu" w temacie pisania testów jest spowodowana tak naprawdę brakiem umiejętności i znajomości narzędzi. Zawsze gdy robimy coś po raz pierwszy, wydaje się to niekomfortowe i obciążające, ale gdy wejdzie nam to w krew, okazuje się, że nie zajmuje to wcale aż tak dużo czasu.
Uważam również, że nie powinniśmy podchodzić do tego tematu zero-jedynkowo. Jesteśmy w stanie kontrolować jak dużo czasu przeznaczamy na testowanie i na które części kodu patrzymy ze szczególną uwagą. Jeśli mamy ograniczony czas, możemy kierować swoje wysiłki w miejsca, które tego najbardziej potrzebują. Myślę, że i w tym przypadku działa zasada Pareto, czyli teoria wedle której 20% wkładanego wysiłku, odpowiada za 80% procent ostatecznego zysku. Czasem niewiele dobrze napisanych testów daje o wiele więcej zysku niż 100% pokrycie kodu.

# Jaki ja mam z tego zysk?
Oprócz lepszego snu (lub w ogóle obecności snu) w noc po releasie to w sumie nic.
Nie no, żartuję. Ale z pewnością świadomość posiadania dobrych testów dodaje wiele spokoju do developmentu. Ja uwielbiam tę swobodę refaktorowania, w momencie gdy wiem, że ktoś tam z tyłu za mną stoi (testy, testy), patrzy mi na klawiaturę i jest w stanie złapać mnie za rękę, gdy robię coś głupiego.

Lecz oprócz zdrowia psychicznego programistów i ich długiego, niczym niezmąconego snu, testowanie ma inne korzyści. Pozwala np. na utrzymanie stałego tempa developmentu, mimo ciągłego wzrostu aplikacji i bazy kodu. Często, gdy aplikacja się powiększa, dodawanie kolejnych funkcjonalności jest coraz większym problemem, a zmiany w istniejącym kodzie są coraz bardziej niebezpieczne. Testy pozwalają ograniczyć ryzyko związane ze zmianami. W ten sposób zwraca się, często z nawiązką, czas na nie poświęcony.

Mam nawet wrażenie, że kod, który programista pisze, mając z tyłu głowy konieczność napisania do niego testów, jest bardziej uporządkowany, mniej "związany ze sobą", bardziej modułowy, a co za tym idzie łatwiejszy do testowania. Skutkuje to tym, że taki kod jest później również łatwiejszy do utrzymywania i mniej oporny na rozszerzanie.

A skoro już wiemy po co, teraz warto dowiedzieć się jak. Szykujcie się na porządną dawkę informacji o dostępnych narzędziach w kolejnych artykułach.

Ania

PS
Jakimi narzędziami w szczególności jesteście zainteresowani? Uchylając rąbka tajemnicy powiem, że na pewno pojawi się Jest, Enzyme, może również Detox jako narzędzie do e2e dla aplikacji natywnych. Chciałabym też powiedzieć kilka słów na temat visual regression testing. Będzie się działo!
