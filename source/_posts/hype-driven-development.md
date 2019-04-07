---
title: Nie daj się ciemnej stronie mocy - czyli jak unikać hype'u?
thumbnailImagePosition: right
coverMeta: out
coverSize: partial
date: 2017-08-26 15:49:33
tags:
  - Code Europe
categories:
  - Techniczne
thumbnailImage: starwars.jpg
coverImage: starwars.jpg
---

Ciemna strona mocy kusiła rycerzy Jedi potężnymi możliwościami. Zwabieni perspektywą ogromnej siły powoli tracili kontrolę i wpadali w jej sidła. Z hype'm jest podobnie. Dzięki niemu zaczynasz myśleć, że kolejna technologia będzie rozwiązaniem na wszystkie Twoje problemy. Że ten nowiutki framework sprawi, że już nic Cię nie zaskoczy. Że możesz wszystko. Nie jesteś świadomy, że stąpasz bo bardzo cienkim lodzie i już całkiem niedługo to wszystko może się obrócić przeciwko Tobie.
<!--more-->

Zacznijmy od poznania naszego wroga. Jeśli nie wiesz czym jest hype, wystarczy, że pobędziesz we frontendowym środowisku przez kilka miesięcy. W tym czasie prawdopodobnie pojawi się i zniknie kilka frameworków, ktoś zacznie rozwijać forka jakiegoś narzędzia, przez twitter przeleje się kolejna fala entuzjastycznych postów o bibliotece X. W pewnym momencie nawet nie zauważysz, że bliżej Ci do ciemnej stony mocy. Zaczynasz podejmować decyzje w projekcie bazując na tych wszystkich zdarzeniach i opiniach. Twoje wyważone poglądy zmierzają w stronę: "Technologia Y jest świetna w każdych warunkach, bije na głowę wszystko inne". To tu to tam, dorzucasz nową bibliotekę do zależności twojego projektu. W końcu dochodzi do tego, że chcesz przepisywać frontend co 3 miesiące, na co raz to nowy framework. Jeśli tak jest, wiedz, że coś się dzieje.

Ale nie martw się. Świadomość tego, że coś jest na rzeczy, to już połowa sukcesu. Ponieżej znajdziesz kilka rad, które pozwolą Ci pozostać po jasnej stronie.

## All that noise
Zacznijmy od wylęgarni hype'u: Twittera. Gdy na scenie pojawi się kolejne narzędzie, na pewno dowiesz się o nim ze swojego walla. Jednak czerpanie wiedzy i inspiracji z Twittera może być zgubne. Przede wszystkim, raczenie się codziennie nowościami i sensacjami z tego źródła, może powodować poczucie, że twój projekt nie jest wystarczająco na czasie, a Ty jesteś do tyłu. Ludzie się w ten sposób nakręcają i przestają myśleć o prawdziwym celu naszej pracy - tworzeniu dobrych jakościowo aplikacji służących użytkownikowi. ( Nie ma tu nigdzie mowy o najnowszym frameworku, right?).
Dodatkowo, tweety są niebezpieczne z jeszcze jednego powodu. Są wystarczająco długie, żeby powiedzieć, że rozwiązanie X jest fajne, ale nie na tyle, żeby powiedzieć o wszystkich wadach i zaletach oraz pułapkach, które na Ciebie czekają.

{% image center fig-100 tweet.jpg  %}

Znalazłeś fajną biblioteczkę, którą wszyscy polecają. Rozważasz dodanie jej do projektu... Co powinnieneś zrobić, żeby mieć pewność, że nie skońcysz w ciemnym zakątku, zwabiony genialnymi perspektywami?

## Jaki jest Twój problem?
Tworzenie rozwiązania zawsze zaczynaj od określenia problemu, jaki przed Tobą stoi. Logiczne, right? (Może myślicie sobie: Ania przestań nas zarzucać takimi truizmami). Ale w czasie gdy non stop jesteśmy bombardowani potencjalnymi rozwiązaniami, bardzo łatwo się dać się zwieść i wrzucić do projektu coś, co może i rozwiązuje bardzo ważny problem, ale nie jest i nigdy nie był to nasz problem. A jak wszyscy wiemy, kolejna zależność, nowa abstrakcja to więcej kodu do rozumienia i utrzymywania, co często oznacza nowe problemy.
Szukaj rozwiązań do problemu, a nie na odwrót. Porzuć podejście:

> "Znalazłem fajną biblioteczkę, wszyscy ją polecają, gdzie by tu ją zastosować?"

na rzecz

> "Potrzebuję zredukować "time to interactive" do X sekund. Jak to osiągnąć?

## Nie oceniaj po okładce
Gdy już masz na oku konkretne rozwiązania (jeśli zastosowałeś się do poprzedniej rady, nie są to przypadkowe Twitterowe znaleziska), pora na sprawdzenie ich pod kątem technicznym. Czemu by nie zastosować w tym przypadku code review? Robimy je codziennie w naszych projektach, w tym wypadku też powinno się sprawdzić. Nigdy nie przestanę nawoływać do zaglądania do źródeł naszych zależności. Upewnienie się, że kod, który wprowadzasz do projektu wygląda znośnie jest twoim obowiązkiem. Nie ważne czy jest to fragment napisany przez twojego kolegę z zespołu czy twórcę biblioteki. Poza tym, to nie jest przecież czarna magia!
Przyjrzyj się również dokładnie stronie tego projektu na githubie. Ale nie sugeruj się tylko i wyłącznie liczbą gwiazdek. Przejrzyj kartę ze zgłoszonymi problemami (issues). Jeśli jest ich dużo, może świadczyć o dużej ilości bugów i niedoróbek (ale nie musi). Popatrz koniecznie na liczbę otwartych pull requestów (świadczy to o aktywności społeczności i maintainerów). Upewnij się, że projekt jest utrzymywany (sprawdź np. kiedy została wypuszczona ostatnia wersja). Jeśli biblioteka przeszła przez to szczelne sito, możesz spokojnie przejść do kolejnego punktu.

## Perspektywa biznesowa

Przed Tobą największe wyzwanie. Bo z pewnością jest takim zadanie sobie przez developera pytania: "Czy stać nas (pod względem czasu i finansów w projekcie) na zmianę, którą chcemy przeprowadzić. Wielu programistów nie przykłada wagi do takich rozważań, psioczy jedynie na menadżerów, którzy nie pozwalają się pobawić najnowszymi zabawkami. Lecz uważam, że powinniśmy zacząć.
W momencie, gdy pokażemy osobom, które zarządzają projektem, że troszczymy się o perspektywę finansową, a nasze propozycje poparte są konkretami, otworzymy pole do dyskusji w temacie wyborów technologicznych i ich kosztów. Uważam, że zadawanie sobie przez developera pytań:

> "Jakie konsekwencje będzie mieć zmiana frameworka w krótkim i długim okresie czasu?"
> "Kto zapłaci za czas nauki nowego rozwiązania?"
> "Jak nowe narzedzia wpłyną na czas tworzenia funkcjonalności i developers' experience?"
> "Jak wysoko wyceniamy wiedzę, którą zdobędziemy?"
> "Czy będziemy wspierać aplikację na tyle długo, żeby odczuć korzyści płynące ze zmiany technologii?"

może przynieść same korzyści.
Dodatkowo dochodzi kwestia ryzyka, o której już trochę wspominałam. Dodanie każdego fragmentu kodu wiąże się z różnymi niebezpieczeństwami: potencjalnymi bugami czy koniecznością utrzymywania tego kodu, gdy osoby, które robiły to do tej pory zrezygnują. Niektóre rozwiązania są bardzo nowoczesne i odkrywcze, ale wiążą się z większym ryzykiem, nie są dobrze przetestowane, nie mają dużej grupy użytkowników. W tym momencie musimy się zastanowić czy taki stopień ryzyka pasuje do naszej organizacji czy projektu. Granica będzie w innym miejscu dla doinwestowanego startupu z wieloma developerami, dla korporacji i dla agencji.

Okazuje się, że wcale nie tak trudno nie dać się porwać gorączce nowych frameworków. Programiści często śmieją się z frontendowców, jakoże w naszej branży hype jest najbardziej widoczny. Ale pamiętajcie, że to Wy, jako programiści, podejmujecie decyzje. A podążanie za rynkiem, ale rozważne i spokojne świadczy o waszym profesjonalizmie i dojrzałości.

May the force be with you!
Ania

PS
Od jutra (poniedziałek) zaczynam na moim Instagramie cykl - Praca programisty od kuchni :) Jeśli nie chcecie nic przegapić, polubcie mój profil.
<blockquote class="instagram-media" data-instgrm-captioned data-instgrm-version="7" style=" background:#FFF; border:0; border-radius:3px; box-shadow:0 0 1px 0 rgba(0,0,0,0.5),0 1px 10px 0 rgba(0,0,0,0.15); margin: 1px; padding-top:20px; width:99.375%; width:-webkit-calc(100% - 2px); width:calc(100% - 2px);"><div style="padding:8px;"> <div style=" background:#F8F8F8; line-height:0; margin-top:40px; padding:50.0% 0; text-align:center; width:100%;"> <div style=" background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAsCAMAAAApWqozAAAABGdBTUEAALGPC/xhBQAAAAFzUkdCAK7OHOkAAAAMUExURczMzPf399fX1+bm5mzY9AMAAADiSURBVDjLvZXbEsMgCES5/P8/t9FuRVCRmU73JWlzosgSIIZURCjo/ad+EQJJB4Hv8BFt+IDpQoCx1wjOSBFhh2XssxEIYn3ulI/6MNReE07UIWJEv8UEOWDS88LY97kqyTliJKKtuYBbruAyVh5wOHiXmpi5we58Ek028czwyuQdLKPG1Bkb4NnM+VeAnfHqn1k4+GPT6uGQcvu2h2OVuIf/gWUFyy8OWEpdyZSa3aVCqpVoVvzZZ2VTnn2wU8qzVjDDetO90GSy9mVLqtgYSy231MxrY6I2gGqjrTY0L8fxCxfCBbhWrsYYAAAAAElFTkSuQmCC); display:block; height:44px; margin:0 auto -44px; position:relative; top:-22px; width:44px;"></div></div> <p style=" margin:8px 0 0 0; padding:0 4px;"> <a href="https://www.instagram.com/p/BYTOn2Jgw58/" style=" color:#000; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:normal; line-height:17px; text-decoration:none; word-wrap:break-word;" target="_blank">Od jutra na Instagramie #pracaprogramistyodkuchni ☕📚💼💻</a></p> <p style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; line-height:17px; margin-bottom:0; margin-top:8px; overflow:hidden; padding:8px 0 7px; text-align:center; text-overflow:ellipsis; white-space:nowrap;">Post udostępniony przez Ania Konopka (@kernelgonnapanic) <time style=" font-family:Arial,sans-serif; font-size:14px; line-height:17px;" datetime="2017-08-27T14:23:03+00:00">27 Sie, 2017 o 7:23 PDT</time></p></div></blockquote> <script async defer src="//platform.instagram.com/en_US/embeds.js"></script>
