---
title: "Czy na pewno wiesz czym jest frontend?"
tags:
  - Kopendium Frontendu
  - Frontend
  - Nauka programowania
categories:
  - Techniczne
thumbnailImagePosition: right
coverMeta: out
coverSize: partial
thumbnailImage: laptop.jpg
coverImage: laptop.jpg
date: 2018-11-05 16:00:00
---

Kilka miesięcy temu miałam okazję zmierzyć się z nietypowym dla mnie zadaniem. Na co dzień obracam się głównie w towarzystwie programistów, moi rodzice są po informatyce, moi znajomi są programistami, ogólnie większość moich towarzyskich interakcji odbywa się z ludźmi, którzy mniej lub bardziej się w temacie programowania i Internetu orientują. Dlatego wyzwaniem dla mnie stało się zadane mi przez laika pytanie: A kim to ten **frontendowiec** jest?
<!-- more -->

Einstein podobno kiedyś powiedział: “Jeśli nie potrafisz wytłumaczyć czegoś sześciolatkowi, sam tego nie rozumiesz”. Dlatego pytanie, które otrzymałam, potraktowałam jako wyzwanie - przecież to świetna okazja na sprawdzenie siebie. Czy i Wy jesteście gotowi na małą powtórkę?

Zacznijmy od początku...

W przypadku platformy webowej frontendem nazywamy aplikację, która uruchamiana jest w przeglądarce i z którą użytkownik  wchodzi w interakcję bezpośrednio. Zazwyczaj mówi się o niej w kontekście trzech elementów: HTML-a, CSS-a i kodu JavaScript.

**HTML** odpowiada za strukturę tego, co jest wyświetlane w przeglądarce, opisuje, z jakich elementów strona się składa i jakie mają one znaczenie (czy są nagłówkiem, nawigacją czy główną treścią strony).
Na podstawie pliku html, który przeglądarka otrzymała od serwera www, tworzy sobie ona wewnętrzną reprezentację opisującą elementy, które znajdują się na stronie. 

Za pomocą **CSS-a** określamy jak poszczególne części strony będą wyglądać (kolory, kształty, ich położenie). Mamy do dyspozycji wiele sposobów definiowania styli (nadając elementom klasy, identyfikatory, za pomocą tagów html czy atrybutów) i wiele właściwości, które przeglądarki i standard CSS pozwalają nam zdefiniować. Ale jest to zdecydowanie temat na osobny artykuł ;)

Jeśli chodzi o **JavaScript**, to w skrócie można by powiedzieć, że odpowiada on za zachowanie elementów strony. Ale na potrzeby tego artykułu to zbyt duże uproszczenie. Mając te podstawy, warto tę kwestię dalej rozwinąć. 

## Rodzaje stron

Strony i aplikacje różnią się między sobą, możemy je podzielić np. na:
### 1) strony statyczne
Klient (przeglądarka) pobiera pliki html i css, które są statyczne. W formie gotowych plików czekają sobie gdzieś na serwerze, aż jakaś przeglądarka o nie zapyta. Gdy potrzebna jest zmiana treści takiej strony konieczna jest edycja tych plików i ponowne wgranie ich na serwer.
### 2) strony dynamiczne, renderowane po stronie serwera (multi-page app)
Pliki html generowane są przez aplikację po stronie serwera na żądanie tzn. w momencie gdy przeglądarka o nie zapyta. Ten sposób pozwala nam w dużo większym stopniu na dostosowanie treści i wyglądu strony. Dane pobierane są zazwyczaj z bazy danych, dzięki temu jesteśmy w stanie pokazać każdemu użytkownikowi np. dane o jego profilu. W ten sposób strony generuje Symfony, Ruby on Rails, Django etc.
Nawigowanie do kolejnej strony (lub podstrony) powoduje wyrenderowanie przez aplikację na serwerze kolejnego html'a i zwrócenie go przeglądarce.
### 3) strony dynamiczne renderowane po stronie serwera, z dodatkiem skryptów JS
Są to aplikacje opisane w poprzednim punkcie, rozszerzone dodatkowo o możliwości jakie daje nam JavaScript. Zazwyczaj skrypty te są napisane z użyciem vanilla JS (tzn. bez dodatkowych bilbiotek/frameworków) lub korzystają z jQuery (obecnie często róznież np. z Vue). Dodatek JavaScriptu pozwala na rozszerzenie możliwości aplikacji i jej warstwy wizualnej - pozwala na dodatkowe animacje, pokazywanie i chowanie elementów na stronie, pobieranie danych z serwera, bez konieczności przeładowania strony itd.
### 4) aplikacje SPA (single-page app)
Ewolucja stron i aplikacji webowych zaprowadziła nas właśnie w to miejsce. Obecnie bardzo dużo z nich tworzonych jest w ten sposób. Być może znacie pojęcie single-page application (SPA), ale czy zastanowiliście się co to dokładnie oznacza? Co właściwie określamy jako "single-page"? Nad tym tematem musimy się pochylić bardziej.

Aplikacje single-page to takie, w których JavaScript gra pierwsze skrzypce. Kod JS zyskuje nowe odpowiedzialności, o których zaraz sobie opowiemy.

W przypadku aplikacji single-page, plik, który przeglądarki otrzymują od serwera wygląda zazwyczaj podobnie do tego poniżej. (W tym miejscu zaznaczam, że dla uproszczenia nie bierzemy tu pod uwagę możliwości renderowania naszej aplikacji FE po stronie serwera (SSR)).
{% codeblock lang:html %}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <link rel="shortcut icon" href="/favicon.ico">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="theme-color" content="#000000">
    <title>SPA</title>
    <link href="/dist/main-b51b4a8b.css" rel="stylesheet"> // (1)
  </head>
  <body>
    <div id="root"></div> // (3)
    <script type="text/javascript" src="/dist/main-a2dkfh.js"></script> // (2)
  </body>
</html>
{% endcodeblock %}

Jak możemy zauważyć nie jest on zbyt rozbudowany. Posiada link do styli (1), tag, który definiuje nam gdzie znaleźć skrypt naszej aplikacji (2) oraz jeden pusty div (3). Gdzie jest cała nasza treść?

A właśnie, w przypadku aplikacji SPA, ich zawartość jest tworzona z poziomu kodu JavaScript. W celu ułatwienia tego zadania korzysta się zazwyczaj z frameworków np. React, Vue.js czy Angular. Dopiero za pomocą JSa budujemy wszystkie elementy, które pojawią się w naszej aplikacji. Tu przydaje się też ten pusty div. To od niego frameworki zaczynają budowę, "bootstrapują się" i to w tym miejscu pojawi się zawartość naszej strony, po tym jak zostanie uruchomiony kod JS.

### Skąd bierzemy dane?
Oczywiście, w większości rozbudowanych aplikacji, potrzebujemy również skomunikować się z serwerem. Pewne dane, chcemy z serwera ściągnąć. Pewne rzeczy chcemy zapisać w bazie danych, by inni użytkownicy mieli do nich dostęp. Części danych nie chcemy udostępniać byle komu, dlatego potrzebujemy by serwer przeprowadził autentykację i tym samym stwierdził tożsamość naszego użytkownika.
W przypadku aplikacji SPA tego typu potrzeby są zaspokajane prz użyciu mechanizmu zapytań asynchronicznych (AJAX). Pozwalają one na wykonanie zapytania http do serwera, które nie przerywa działania aplikacji frontendowej i nie powoduje przeładowania strony. Gdy przeglądarka otrzyma na nie odpowiedź przekazuje ją do aplikacji, gdzie jest obsługiwana asynchronicznie.

### Czemu mówimy single page?

W przypadku multi-page app, dla każdej podstrony generowany jest nowy plik html z jej zawartością. Możecie się teraz zastanowić co się dzieje, gdy przechodzimy na kolejny widok w naszej aplikacji SPA: czy dostaniemy w tym wypadku inny plik index.html? 

Odpowiedź brzmi: NIE i to z dwóch powodów.


{%image fig-100 directions.jpg %}

Jeśli ta nawigacja odbędzie się w ramach naszej aplikacji (np. poprzez kliknięcie na link do podstrony umieszczony w belce z nawigacją) wtedy zostanie obsłużona przez router. 

**Router** to taka część aplikacji SPA, która dba o to by dla każdego URLa, będącego podstroną w naszej aplikacji, wyrenderować odpowiadający mu widok. 

Spójrzmy na przykład:

{% blockquote %}
Powiedzmy, że `http://example.com/` jest głównym adresem, pod którym znajdziemy naszą aplikację. Jeśli na głównym widoku znajdziemy link do `http://example.com/about` i klikniemy na niego, to właśnie odpowiedzialnością routera będzie podmienienie zawartości strony i wyświetlenie widoku z informacjami o mnie.
{% endblockquote %}

Zauważcie, że wszystko to dzieje się w przeglądarce i jest zarządzane przez JavaScript. Żadne zapytanie nie jest wykonywane do serwera i nie zwraca on ani nie generuje nowego pliku html. Widać tu różnicę między single i multi page app.

A co się stanie w takiej sytuacji?

{% blockquote %}
Będąc pod adresem `http://example.com/about` kliknęliśmy na przycisk "Odśwież" w przeglądarce. Tego typu akcja nie jest już obsługiwana przez router aplikacji. Zapytanie leci do serwera. I co widzimy? Dostajemy ten sam index.html, który otrzymaliśmy poprzednio, a znów to router dba o to, by wyświetlić treść (widok), która odpowiada danemu adresowi. W naszym przypadku są to informacje o mnie.
{% endblockquote %}

Podsumowując, w przypadku single-page app, zawartość strony nie jest przesyłana z serwera w pliku html. Jest ona tworzona w przeglądarce przez kod JavaScript. O tym, co dokładnie zostanie wyświetlone decyduje zazwyczaj router aplikacji, który renderuje odpowiednią zawartość bazując na ścieżce i podstronie na jaką ona wskazuje (a o przypadku SSR opowiemy sobie już przy innej okazji).

Uff, sporo informacji jak na jeden raz. Mam nadzieję, że dzięki temu artykułowi poukładały się Wam w głowie podstawy  związane z aplikacjami frontendowymi. Szykuję w najbliżej przyszłości więcej podobnych postów, so stay tuned ;)

Ania

*Photos by Dean Pugh and Dave Clubb on Unsplash*