---
title: To żyje! Elm w akcji.
tags:
  - Elm
  - Daj się poznać 2017
  - Frontend
categories:
    - Techniczne
thumbnailImagePosition: right
coverMeta: out
coverSize: partial
thumbnailImage: nasa.jpg
coverImage: nasa.jpg
date: 2017-03-18 15:23:00
---

Kolejny odcinek zmagań z Elmem przed nami. Dziś timer ożyje. Będziemy mieć okazję zobaczyć jak wygląda architektura aplikacji w Elmie i czemu może się Wam wydawać znajoma.<!--more--> Let's start!

W poprzednim wpisie pokazałam jak, za pomocą Elma, możemy wyrenderować kilka divów. Ale od kilku DOM elementów do pełnej aplikacji jeszcze daleko. Dziś nadamy timerowi trochę ram i obsłużymy pierwsze kliknięcia. Na razie nie poświęcałam zbędnego czasu na stylowanie, więc wybaczcie wizualne koszmarki. Na rozprawienie się z nimi też przyjdzie pora.

Swoje poszukiwania na temat "Jak wygląda aplikacja w Elmie?" zaczęłam od tutoriala. Lecz nie jest on zbyt obszerny i szybko przestał mi wystarczać. Dużo więcej zrozumiałam przeglądając kod przykładowej appki - [tutaj](https://github.com/sporto/elm-tutorial-app). Nie wiem jak inni, ale ja na przykładach uczę się najwięcej.

Chcąc, by aplikacja ożyła dodałam do niej możliwość ustawienia liczby minut, od której mamy odliczać. Na razie użyłam do tego stringów, ale z pewnością szybko się to zmieni.

Jeśli chodzi o podstawowe części składowe architektury elmowej aplikacji to mamy tutaj:

- model: jest to stan naszej aplikacji. Dodatkowo obok niego definiujemy również funkcję init, która zwraca stan, od którego aplikacja zacznie swoje działanie

```elm
type alias Model =
    String

init : ( Model, Cmd Msg )
init =
    ( "10:00", Cmd.none )
```
- messages: wiadomości sygnalizują zdarzenia, które mają miejsce w naszej aplikacji

```elm
type Msg
  = SetTimer String
```
- view: widok renderujemy na podstawie stanu naszej aplikacji (w tym przypadku przekazuje stan do komponentu `timer`)

```elm
view : Model -> Html Msg
view model =
    timer model
```
- update: mamy również funkcję, która jest wywoływana przez program, przy każdym pojawieniu się wiadomości. Modyfikuje ona stan aplikacji i może zwracać commandy (o nich kiedy indziej)

```elm
update : Msg -> Model -> ( Model, Cmd Msg )
update msg model =
    case msg of
        Messages.SetTimer number ->
            ( number, Cmd.none )
```
- subskrypcje: za ich pomocą nasłuchujemy na zewnętrze wejście (np. ruchy myszką), na razie z nich nie korzystałam

Potrzebujemy również `program`, który zbiera wszystkie te elementy i sprawia, że nasza aplikacja ożywa.

Pełne źródła można oczywiście znaleźć na [githubie](https://github.com/kernelgonnapanic/timer).

Dla Was pozostawiam zagadkę. Co przypomina Wam taka struktura aplikacji? Podobieństwo do dużo bardziej popularnej obecnie technologii jest uderzające. Dajcie znać w komentarzu co myślicie.

Ania
