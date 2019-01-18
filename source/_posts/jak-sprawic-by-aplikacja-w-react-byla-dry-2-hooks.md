---
title: "Jak sprawić, by Twoja aplikacja w React była DRY? - Hooks"
tags:
  - React
  - Javascript
  - Dobre praktyki
  - Frontend
keywords:
  - React
  - Higher Order Components
  - dobre praktyki React
  - wzorce React
  - render prop
  - react hooks
thumbnailImagePosition: right
coverMeta: out
coverSize: partial
thumbnailImage: cracks.jpg
coverImage: cracks.jpg
date: 2018-12-04 19:35:00
---

Jeśli jesteście na bieżąco z newsami we frontendowym świecie, z pewnością słyszeliście już o wprowadzeniu do React nowego API o nazwie {% hl_text primary %} Hooks{%endhl_text%}. Postanowiłam przyjrzeć się mu lepiej i zobaczyć, jak możemy go porównać z rozwiązaniami, które wykorzystywaliśmy w React do tej pory.
<!--more-->

Rok temu, napisałam dla Was posta o wykorzystaniu `render propów` i `higher order components` do współdzielenia kodu między komponentami w aplikacjach React. Możecie go sobie odświeżyć [tutaj](https://kernelgonnapanic.pl/2017/10/29/jak-sprawic-by-aplikacja-w-react-byla-dry/). Myślę, że warto to zrobić, zanim pobiegniemy z tematem dalej. 
Jesteście już z powrotem? :) W tamtym czasie były to najbardziej popularne, specyficzne dla React, mechanizmy, dzięki którym nasze aplikacje mogły być bardziej DRY. Ostatnio jednak okazało się, że zespół tworzący React planuje wprowadzeniego nowego API, które ma nam to zadanie ułatwić. Przyjrzyjmy się temu, czym są hooki i jak mogą nam pomóc.

## Hooks - po co nowy mechanizm?

Myślę, że można stwierdzić, że komponenty wyższych rzędów (HOCs) i używanie render propów (i będącym tego odmianą mechanizm "children as a function") zostały już przez społeczność reactową całkiem dobrze przyjęte i szeroko stosowane. Można zapytać: po co w takim razie wprowadzać nowy mechanizm?

Otóż właśnie, wraz z szerokim użyciem wcześniej wymienionych technik, użytkownicy React doszli do wniosku, że czegoś im brakuje. Istniał np. problem z reużywaniem kodu obsługującego stan w komponentach. Jeżeli logika z tym związana była potrzebna w dwóch miejscach zazwyczaj trzeba było ją powielać, wspomagając się co najwyżej wydzielaniem "czystych" funkcji, które operowały na danych. Sam kod związany z ustawieniem początkowego stanu, jego uaktualnieniem itd. niestety trzeba było powtórzyć.

Dodatkowo, w sytuacjach gdy komponent obsługiwał kilka zachowań, kod, który był za nie odpowiedzialny, zaczynał się ze sobą przeplatać. Dla przykładu: zarówno funkcjonalność 1, jak i 2 miały część kodu w `componentDidMount` jak i `componentWillUnmount`. I trudno było je zgrabnie oddzielić, by móc korzystać z tego kodu w innym miejscu repozytorium.

Naprzeciw tym właśnie problemom wychodzi mechanizm Hooks. Pozwala on na korzystanie z dotyczasowych funkcjonalności React tj. lokalnego stanu, contextu, refs przy pomocy innego API, które ułatwia współdzielenie kodu. Jeśli chcecie poczytać więcej o motywacjach stojących za ich stworzeniem i szczegółach dotyczących ich użycia - zachęcam do zajrzenia do oficjalnej [dokumentacji](https://reactjs.org/docs/hooks-intro.html), która jest napisana prostym językiem i dużo objaśnia.

A my zabieramy się do działania i zobaczymy jak hooki wyglądają od strony kodu.

## Hooks w akcji

{% image left fig-50 hoc.gif %}

Żeby łatwiej nam się porównywało mechanizm hooków do render propów i HOC postanowiłam rozszerzyć przykład, który prezentowałam w pierwszym artykule o komponent korzystający z hooków. Przypomnijmy sobie, jak nasza mini-aplikacja wtedy wyglądała.

Naszym zadaniem było stworzenie animującego się header’a. Chcieliśmy, by początkowo był on przezroczysty (opacity: 0) i wraz ze scrollowaniem strony, był coraz bardziej widoczny (aż do opacity: 1). Końcowy efekt widoczny jest na gifie. 
<div style="clear:both"></div>
Dodatkowo komponent ten zaimplementowaliśmy na *3 sposoby*: 
1) bez współdzielenia kodu, 
2) z wykorzystaniem higher order component,
3) z wykorzystaniem komponentu używającego render prop.
Wersja 2 i 3 były przykładami na to jak możemy budować nasze komponenty, by były przyjazne ich reużywaniu.

Dziś naszym zadaniem jest stworzenie tego samego komponentu i sprawdzenie czy mechanizm hooków może nam w tym pomóc.

Dla przypomnienia zobaczmy naszą funkcjonalność w czystej formie, umieszczoną całą w jednym komponencie.

{% codeblock DummyPage.js lang:jsx https://github.com/kernelgonnapanic/hoc-render-callback-example/blob/master/src/pages/DummyPage.js DummyPage.js %}
class DummyPage extends Component {
  constructor() {
    super();
    this.state = {
      scrollPos: 0,
    };
  }
  calculateOpacity = () => {
    if (!this.state.scrollPos) return 0;
    if (this.state.scrollPos > 200) return 1;
    return this.state.scrollPos / 200;
  }
  handleScroll = (event) => {
    const scrollPos = event.target.scrollTop;
    this.setState({ scrollPos });
  }
  render() {
    return (
      <div className="relativeContainer">
        <div
          className="container"
          onScroll={this.handleScroll}
        >
          <Header
            opacity={this.calculateOpacity()}
            text="Dummy page"
          />
          <List type="dummy" />
        </div>
      </div>
    );
  }
}
{%endcodeblock%}

Teraz spróbujmy to przeorganizować, z użyciem hooków. Nasz nowy komponent wygląda tak:

{% codeblock PageWithHooks.js lang:jsx https://github.com/kernelgonnapanic/hoc-render-callback-example/blob/master/src/pages/PageWithHooks.js PageWithHooks.js %}
import useOpacityFromScroll from '../enhancers/useOpacityFromScrollHook';

const PageWithHooks = () => {
  const { opacity, handleScroll } = useOpacityFromScroll();
  return (
    <div className="relativeContainer">
      <div
        className="container"
        onScroll={handleScroll}
      >
        <Header
          opacity={opacity}
          text="Page with hooks"
          yellow
        />
        <List type="hooks"/>
      </div>
    </div>
  );
}
{%endcodeblock%}

Zastanówmy się jakie zmiany zaszły w tym komponencie. Przede wszystkim widzimy tutaj wywołanie nowej funkcji o nazwie `useOpacityFromScroll`. To tam schowała się cała nasza logika odpowiedzialna za odczytywanie pozycji scrolla i przeliczanie jej na wartość opacity. Jest to tzw. `custom hook`, ponieważ nie pochodzi bezpośrednio z Reacta, a został napisany przeze mnie. 

Dodatkowo, co bardziej spostrzegawczy, z pewnością zwrócili uwagę na to, że nasz komponent nie jest już klasą, a stał się komponentem funkcyjnym (czyli po prostu funkcją). Tu dochodzimy do kolejnego problemu, który hooki starają się rozwiązać. Do tej pory, by komponent mógł przechowywać stan, musiał być klasą, dziedziczącą po `React.Component`. Hooki dodają możliwość przechowywania stanu w komponentach funkcyjnych. Też was wkurzało refactorowanie funkcji na klasę, w momencie gdy uświadamialiście sobie, że potrzebujecie lokalnego stanu w komponencie? Wygląda na to, że mamy ten kłopot już z głowy ;)

## Custom hook

Najwyższy czas spojrzeć do stworzonego przez nas hooka.

{% codeblock useOpacityFromScrollHook.js  lang:jsx https://github.com/kernelgonnapanic/hoc-render-callback-example/blob/master/src/enhancers/useOpacityFromScrollHook.js useOpacityFromScrollHook.js  %}
const calculateOpacity = (scrollPos) => {
  if (!scrollPos) return 0;
  if (scrollPos > 200) return 1;
  return scrollPos / 200;
}

const useOpacityFromScroll = () => {
  const [scrollPos, setScroll] = useState(0);

  const handleScroll = (event) => {
    const scrollPos = event.target.scrollTop;
    setScroll(scrollPos);
  }

  return { opacity: calculateOpacity(scrollPos), handleScroll };
}

{%endcodeblock%}

Zacznijmy od przyjrzenia się funkcji `useOpacityFromScroll`. Jest to, jak już wspominałam, stworzony przez nas hook. Jego nazwa rozpoczyna się od `use`. Taką konwencję sugeruje dokumentacja i bazując na niej działają również lintery, które sprawdzają czy hooki są przez nas użyte w odpowiedni sposób.
W 8 linii możemy zobaczyć użycie hooka `useState`. Pochodzi on z Reacta i pozwala nam na korzystanie ze stanu. Ale wait? Nie mamy tu żadnego komponentu, jaki to jest stan w takim razie?

No i właśnie, hooki pozwalają nam na odłączenie logiki obsługi stanu od komponentu. To oznacza, że kod ten będzie obsługiwał stan komponentu, w którym zostanie wywołany. W naszym przypadku jest on wywołany z `PageWithHooks` i stanem tego komponentu będzie się zajmował. Co istotne, wydzielamy w ten sposób kod obsługujący stan, a nie sam stan. W ten sposób, gdy inny komponent np. `SmartPage` będzie również korzystał z tego hooka, jego stan nie będzie współdzielny ze stanem `PageWithHooks`. 

Do hooka `useState` podajemy wartość początkową stanu (w naszym przypadku jest to 0) i zwraca on, aktualną wartość scrolla i funkcję, która pozwala nam na jej modyfikowanie. My z kolei funkcję `setScroll` dodatkowo opakowujemy w taki sposób, by była w stanie przyjąć scroll event.

Wyliczoną wartość opacity i funkcję, która updatuje pozycję scrolla na podstawie eventu zwracamy z naszego hooka i korzystamy z nich w komponencie `PageWithHooks`.

## Hooks, hooks everywhere

Jeśli dalej czytasz, to szacun dla Ciebie :) Zostało nam tylko kilka ostatnich informacji. Zastanawiasz się może, jakie jeszcze hooki oferuje nam React. Mamy więc:
- `useState`, którego używaliśmy dzisiaj,
- `useEffect`, o którym za moment powiem trochę więcej,
- `useContext`, który, jak sama nazwa mówi, pozwala na dostęp do contextu,
- `useRef`, pozwalający na otrzymanie referencji do elementu DOMu.
i inne, o których możecie poczytać [tutaj](https://reactjs.org/docs/hooks-reference.html).

Hook `useEffect` pozwala na uruchamianie efektów. Czym one są? `Efekt` to funkcja, która jest wywoływana po tym, jak komponent zostanie wyrenderowany, a DOM zaktualizowany. W zamyśle twórców efekty pełnią w komponentach funkcyjnych podobną rolę, jak lifecycle hooki w klasach. Dzięki nim, jesteśmy np. w stanie zareagować na stan, który się zmienił i wykonać asynchroniczne zapytanie. Więcej o użyciu efektów dowiecie się [tu](https://reactjs.org/docs/hooks-effect.html).

Dodatkowo, pojawiło się już wiele hooków stworzonych przez społeczność, możecie je znaleźć np. w repozytorium [awesome react hooks](https://github.com/rehooks/awesome-react-hooks). Powstała również [strona](https://usehooks.com/), gdzie codziennie pojawia się ich nowe przykładowe użycie. To dużo fajnego materiału, dzięki któremu można bardziej wyczuć w jakich sytuacjach hooki okażą się pomocne.

Warto pamiętać, że wprowadzenie hooków do React planowane jest w wersji 16.7, która obecnie jest dostępna w wersji alpha. Z pewnością nie jest rozwiązanie gotowe do wprowadzania do produkcyjnych aplikacji, ale warto już zacząć uczyć się budować kod w oparciu o tę koncepcję. Dokumentacja również przestrzega przed przepisywaniem na "huraaaa" bardzo skomplikowanych komponentów i zaleca, by zacząć używanie hooków od nowo tworzonych komponentów i mało znaczących części aplikacji i kodu.

Post był długi i dużo się w nim działo. Jeśli dotrwałeś do tego momentu, to z pewnością twoje intuicje na temat hooków są już całkiem dobrze rozwinięte. Dajcie znać, czy warto pobawić się z tym tematem dalej, ilustrując sytuacje w których hooki pokazują swoją moc. Ciekawa jestem również, czy często używacie render propów i higher order components w swoim kodzie. Koniecznie podzielcie się swoimi przemyśleniami!

Do następnego!
Ania

*Photo by Joshua Brown on Unsplash*

