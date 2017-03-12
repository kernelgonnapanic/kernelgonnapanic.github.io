---
title: Elm - początki.
tags:
  - Elm
  - Podstawy
  - Daj się poznać 2017
  - Frontend
thumbnailImagePosition: top
coverMeta: out
coverSize: partial
thumbnailImage: forest.jpg
coverImage: forest.jpg
date: 2017-03-08 22:39:00
---

Był czas na pogaduszki na temat projektu, a teraz pora na otwarcie edytora i zmierzenie się z konkretnymi problemami. Do dzieła!
<!-- more -->

Zdecydowałam się zacząć od oficjalnego tutoriala Elma dostępnego [tutaj](https://www.elm-tutorial.org/en/). Lecz również uciekać od niego, gdy poczuję, że chcę sobie sama poeksperymentować.

## Początki
Od pierwszego momentu czuję, że Elm chce być *inny*. Zacznijmy od pobierania potrzebnych modułów. W klasycznym JS mamy od tego `npm'a`, `node_modules` oraz `package.json`. W środowisku Elma moduły ściągamy za pomocą `elm'a`, przechowywane są w `elm-stuff` (tak, serio tak to nazwali), a listę zależności trzymamy w `elm-package.json`. Więc prawie tak samo, ale jednak inaczej. Czuję tu pewną hipsterskość ;)

Rozpoczęłam oczywiście od stworzenia komponentu z Hello world!.

## Pierwszy komponent
No cóż, poniższy kod nie powala złożonością, ale od tego zaczęłam.
```elm
module Hello exposing (..)

import Html exposing (text)

main =
    text "Hello world!"
```

Pytanie, które pojawia się teraz to: jak skompilować ten kod i wywołać w przeglądarce? Zaczęłam od rozwiązania wbudowanego w elm'a, która pozwala działać na szybko i nie musieć stawiać całego build systemu. Jest to `elm reactor`, który jest serwerem, który potrafi w locie kompilować kod napisany w Elmie. W ten sposób zobaczyłam swój upragniony "Hello world" w oknie przeglądarki. Let's go on!

## Dodajmy style
Mój "Hello world!" jest piękny i jest oczywiście dowodem mojej dominacji nad maszyną, ale nie chcemy z pewnością na tym poprzestać. Dołóżmy do tego więcej elementów i pobawmy się trochę stylami.

Po kilkunastu minutach mamy już kilka divów.
```elm
module Hello exposing (..)

import Html exposing (text, div, node)
import Html.Attributes exposing (class, rel, href)

css path =
  node "link" [ rel "stylesheet", href path ] []

main = 
    div [] [
        css "styles.css",
        div [class "hello"] [
            div [] [text "My timer"],
            div [] [text "25:00"],
            div [class "button"] [text "Start!"]
        ]
    ]
```

Żeby dodać style, nadal uruchamiając kod poprzez reactor'a musiałam się uciec do pewnej sztuczki, która jest widoczna powyżej i ręcznie wstawić link ze stylami.

Jak widać mamy już kilka divów wraz z atrybutami i zawartością. Na razie ominęłam temat sygnatur funkcji, zabiorę się do tego przy okazji. Następnym razem spróbujemy trochę ożywić naszą aplikację, by nie poprzestawać na renderowaniu smutnego htmla. Więc szykujcie się na wpis o architekturze aplikacji w Elmie.

Do usłyszenia!
Ania

P.S.
Elm serwuje nam naprawdę urocze błędy.
{% image center fig-100 clear zrzut.jpg  %}
